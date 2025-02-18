---
title: "dW^2=dt, dt^2=0, dWdt=0"
date: 2024-06-21 14:57:43 +0900
categories: [Mathematics, Stochastic Calculus]
tags: [Stochastic Calculus] # TAG names should always be lowercase

author: rouxist
math: true
---

## $$dW^2=dt, dt^2=0, dWdt=0$$

---

[Ito's lemma](https://rouxist.github.io/posts/math_sc_part-3/#33-itôs-formula){:target=”\_blank”}를 유도할 때에 필요한 그 내용,

$$dW^2=dt$$

$$dt^2=0$$

$$dWdt=0$$

의 유도 과정에 대해 (~~지난 5월 8일쯤 하라는 공부는 안하고~~) 알아보았다.

<br>

### Mean-Square Convergence

---

$$\lim_{n \rightarrow 0} \mathbb{E}[(X_n - X)^2]=0$$

일반적인 변수가 아닌 **확률변수**의 수렴에 대해 논할 때 사용될 수 있다. $$X_n \rightarrow X \ \text{as} \  n \rightarrow \infty$$ 의 의미를 가진다.

<br>

### $$dW^2=dt$$

---

$dW^2=dt$ 역시 $W_t$ 라는 확률변수가 포함된 식이고, mean-square convergence를 이용하여 이 등식이 성립함을 보이게 된다.

$\int_0^t dW_s^2 = \lim_{n \rightarrow \infty} \sum_{k=1}^n \Delta W_{t_k}^2$ 이므로 <span style="color:gray">(where $$\Delta W_{t_k} = W_{t_k}-W_{t_{k-1}}, \Delta t = \frac{t}{n}, \quad 0<t_1<t_2<\cdots<t$$)</span>

mean-square convergence 식에서 $$X_n=\sum_{k=1}^n \Delta W_{t_k}^2, \ X=t$$라고 보면

$$\lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\Bigl(\sum_{k=1}^n \Delta W_{t_k}^2 - t \Bigl)^2\Bigr] = 0$$

이제 식을 전개해보면

$$\lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\Bigl(\sum_{k=1}^n \Delta W_{t_k}^2 \Bigl)^2 -2t (\sum_{k=1}^n \Delta W_{t_k}^2 \Bigl) + t^2 \Bigr] = 0$$

$$\lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\Bigl(\sum_{k=1}^n \Delta W_{t_k}^2 \Bigl)^2 \Bigr] -2t \cdot \mathbb{E} \Bigr[(\sum_{k=1}^n \Delta W_{t_k}^2 \Bigl)\Bigr] + t^2 = 0$$

**첫 번째 항**을 먼저 보면

$$
\begin{aligned}
\lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\Bigl(\sum_{k=1}^n \Delta W_{t_k}^2 \Bigl)^2 \Bigr] &= \lim_{n \rightarrow \infty} \mathbb{E}[( \Delta W_{t_1}^2 +  \Delta W_{t_2}^2 + \cdots +  \Delta W_{t_n}^2)^2] \\
&= \lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\sum_{k=1}^n \Delta W_{t_k}^4 \ + \ 2\sum_{0\le i < j \le n} \Delta W_{t_i}^2 \Delta W_{t_j}^2 \Bigr] \\
&= \lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\sum_{k=1}^n \Delta W_{t_k}^4 \Bigr] + 2 \mathbb{E}\Bigr[\sum_{0\le i < j \le n} \Delta W_{t_i}^2 \Delta W_{t_j}^2 \Bigr] \\
&= \lim_{n \rightarrow \infty} \sum_{k=1}^n \ \mathbb{E}\Bigr[\Delta W_{t_k}^4 \Bigr] + 2 \sum_{0\le i < j \le n} \mathbb{E}\Bigr[\Delta W_{t_i}^2 \Delta W_{t_j}^2 \Bigr] \\
&= \lim_{n \rightarrow \infty} \sum_{k=1}^n 3(\Delta t_k)^2 \ + \ 2\sum_{0\le i < j \le n} \Delta t_i \Delta t_j  && \cdots \ \text{(1)}\\
&= \lim_{n \rightarrow \infty} \sum_{k=1}^n 3\frac{t^2}{n^2} \ + \ 2\sum_{0\le i < j \le n} \frac{t}{n} \frac{t}{n}  \\
&= \lim_{n \rightarrow \infty} 3n\frac{t^2}{n^2} \ + \ n(n-1) \frac{t}{n} \frac{t}{n} && \cdots \ \text{(2)}\\
&= t^2
\end{aligned}
$$

#### (1) : $\mathbb{E}[X^4]=3\sigma^4$

이 내용은 [이 포스트](https://rouxist.github.io/posts/math_etc_expectation-rv-to-power/){:target=”\_blank”}에 정리되어있음

#### (2) : cross product term의 항 개수

- $0\le i < j \le n$ 인 $i,j$의 조합의 수를 구하면 ${n \choose 2}=\frac{n(n-1)}{2}$ 이므로 대입하면 총 $2\cdot \frac{n(n-1)}{2} = n(n-1)$개이다.
- 또는 시그마 앞에 곱해진 2를 떼고 한 번에 생각할 수도 있다. $0\le i \le n, 0\le j \le n$ 인 $i,j$의 조합의 수는 ${n \choose 1} \cdot {n \choose 1} = n \cdot n = n^2$이고, 여기서 제곱 항의 개수는 $n$개이니 cross product term의 개수는 총 $n^2-n=n(n-1)$이 된다.

<br>

이제 **두 번째 항**을 보면

$$
\begin{aligned}
\mathbb{E} \Bigr[(\sum_{k=1}^n \Delta W_{t_k}^2 \Bigl)\Bigr] &= \mathbb{E} \Bigr[(\sum_{k=1}^n \Delta t_k \Bigl)\Bigr] \\
&= \sum_{k=1}^n \mathbb{E} \bigr[ \Delta t_k \bigr] \\
&= \sum_{k=1}^n \mathbb{E} \bigr[ \frac{t}{n} \bigr] \\
&= \sum_{k=1}^n \frac{t}{n}  \\
&= n \cdot \frac{t}{n}  \\
&= t
\end{aligned}
$$

그리고 앞의 항 $-2t$를 곱해주면 $-2t^2$이 된다.

이제 세 항의 모두 합쳐주면, $$t^2 -2t^2+t^2=0$$이 성립한다. 따라서 $$dW^2=dt$$ 이다.

<br>

### $$dWdt=0$$

이번엔 mean-square convergence 식에 $$X_n=\sum_{k=1}^n \Delta W_{t_k} \Delta t_k, \ X=0$$이라고 보면

$$\lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\Bigl(\sum_{k=1}^n \Delta W_{t_k} \Delta t_k \Bigl)^2\Bigr] = 0$$

이다.

$$
\begin{aligned}
\lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\Bigl(\sum_{k=1}^n \Delta W_{t_k} \Delta t_k \Bigl)^2\Bigr] &= \lim_{n \rightarrow \infty} \mathbb{E} \Bigr[ \Bigl( \Delta W_{t_1} \Delta t_1 + \Delta W_{t_2} \Delta t_2 + \cdots +\Delta W_{t_n} \Delta t_n \Bigl)^2 \Bigr]\\
&= \lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\sum_{k=1}^n \Delta W_{t_k}^2 \Delta t_k^2 \ + \ 2\sum_{0\le i < j \le n} \Delta W_{t_i} \Delta W_{t_j} \Delta t_i \Delta t_j \Bigr] \\
&= \lim_{n \rightarrow \infty} \mathbb{E}\Bigr[\sum_{k=1}^n \Delta W_{t_k}^2 \Delta t_k^2 \Bigr] + 2 \mathbb{E}\Bigr[\sum_{0\le i < j \le n} \Delta W_{t_i} \Delta W_{t_j} \Delta t_i \Delta t_j \Bigr] \\
&= \lim_{n \rightarrow \infty} \sum_{k=1}^n \ \mathbb{E}\Bigr[\Delta W_{t_k}^2 \Delta t_k^2 \Bigr] + 2 \sum_{0\le i < j \le n} \Delta t_i \Delta t_j \cdot  \mathbb{E}\Bigr[\Delta W_{t_i} \Delta W_{t_j} \Bigr] && \cdots \ \text{(1)} \\
&= \lim_{n \rightarrow \infty} \sum_{k=1}^n (\Delta t_k)^3 \\\
&= \lim_{n \rightarrow \infty} \sum_{k=1}^n \frac{t^3}{n^3} \\
&= \lim_{n \rightarrow \infty} n\frac{t^3}{n^3} \\
&= 0
\end{aligned}
$$

#### (1) : Independent increments

[Brownian motion의 정의](https://rouxist.github.io/posts/math_sc_part-2/#24-brownian-motion){:target=”\_blank”}에 의해 $\Delta W_{t_j}$ 와 $\Delta W_{t_j} $는 독립이므로, $\mathbb{E}\Bigr[\Delta W_{t_i} \Delta W_{t_j} \Bigr]=\mathbb{E}\Bigr[\Delta W_{t_i} \Bigr] \mathbb{E}\Bigr[ \Delta W_{t_j} \Bigr]$ 이고 각각의 값이 0이므로 두 번째 항의 값은 0이 된다.

따라서 $$dWdt=0$$ 이다.

<br>

### $$dt^2=0$$

이번엔 확률변수가 포함되어있지 않기 때문에 mean-square convergence일 필요도 없다. 구분구적법을 떠올리면

$$
\begin{aligned}
\int_0^t ds^2 &= \lim_{n \rightarrow \infty} \sum_{k=1}^n \Delta t_k^2\\
&= \lim_{n \rightarrow \infty} \sum_{k=1}^n \frac{t^2}{n^2}\\
&= \lim_{n \rightarrow \infty} n \frac{t^2}{n^2}\\
&= 0
\end{aligned}
$$

따라서 $$dt^2=0$$ 이다.

<br/><br/>

2024.06.21

## References

---

[https://sine-qua-none.tistory.com/33](https://sine-qua-none.tistory.com/33){:target=”\_blank”}
[https://youtu.be/MXP57g4fXYs?si=ZJ-Fgu5CKd9_6Bus](https://youtu.be/MXP57g4fXYs?si=ZJ-Fgu5CKd9_6Bus){:target=”\_blank”}

[^fn1]:
