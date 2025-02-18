---
title: "1. Martingales in discrete time"
date: 2024-02-03 17:28:46 +0900
categories: [Mathematics, Stochastic Calculus]
tags: [Stochastic Calculus] # TAG names should always be lowercase

author: rouxist
math: true
---

[https://www.math.uchicago.edu/~lawler/inprogress](https://www.math.uchicago.edu/~lawler/inprogress)

## 1.1 Conditional expectation

---

2023.10.15, 2024.02.03

Conditional Expectation은 이 책 전체를 Permeate하는 개념.

- r.v. $X$의 expectation $$\mathcal{E}[X]$$ trial의 결과에 대한 정보가 없을 때 $X$에 대한 **best guess**라고 볼 수 있음

- $$X,Y$$가 joint density $$f(x,y)$$를 가지고 marginal density $$f(x)=\int_{-\infty}^{\infty}{f(x,y)dy}$$일 때  
  Conditional density는 $$f(y \vert x)=\frac{f(x,y)}{f(x)}$$이다.

- 이를 이용해 Conditional Expectation은 $$E[Y \vert X]=\int_{-\infty}^{\infty}{y \ f(y \vert X)dy}=\frac{\int_{-\infty}^{\infty}{y \ f(X,y)dy}}{f(X)}$$ 인데 (5p)  
   $$E[Y \vert X]$$도 $X$**에 대한 확률변수**이므로 $X$에 대한 기댓값을 구하면

  $$
  \begin{aligned}
  \mathbb{E}(E[Y \vert X]) & = \int_{-\infty}^{\infty}{\mathbb{E}[Y \vert X = x] f(x)dx} \\
  & = \int_{-\infty}^{\infty}{ \biggr[ \int_{-\infty}^{\infty}{y \ f(y \vert x)dy} \biggr] f(x)dx} \\
  & = \int_{-\infty}^{\infty}{  \int_{-\infty}^{\infty}{y \ f(x,y)dy}dx} \\
  & = \mathbb{E}[Y]
  \end{aligned}
  $$

  <span style="color:gray">2학년 1학기 확률통계론에서 $$E[Y]=E[E[Y \vert X]]$$라고 배웠던 그 내용.</span>  
  <span style="color:gray">책에서는 일반적인 expectation은 $$\mathbb{E}$$로, conditional expectation은 $E$로 표기</span>

  즉 데이터 $$X_1, X_2, ... , X_n$$ 을 관찰하면 **best prediction** $$E[Y|X_1, X_2, ... , X_n]$$을 구할 수 있고,  
  그 best prediction을 all possible values X_1, X_2, ... , X_n에 대해 average하면 **best prediction of Y**를 구할 수 있다. <span style="color:gray">($$X_1, X_2, ... , X_n$$ 은 r.v.)</span> 즉 $$\mathbb{E}[Y]=\mathbb{E}[E[Y \vert \mathcal{F}_n]]$$

- 이 책에서는 Conditional Expectation $$E[Y \vert \mathcal{F}_n]$$ 을 다음을 만족하는 **r.v.** 라고 정의한다.

  - $$E[Y \vert \mathcal{F}_n]$$ is $$\mathcal{F}_n{\text -}measurable$$
  - For every $$\mathcal{F}_n{\text -}measurable$$ event $A$, $$\mathbb{E}[E[Y \vert \ \mathcal{F}_n]1_A]=\mathbb{E}[Y1_A]$$

- 이는 다음과 같은 property들을 가진다.

  - measurable이면 상수처럼 작용
    - If $Y$ is $$\mathcal{F}_n{\text -}measurable$$ , then $$E[Y \vert \mathcal{F}_n] = Y$$
    - 반대로 $$E[Y \vert \mathcal{F}_0] = \mathbb{E}[Y] \because \mathcal{F}_0$$ means no information
    - If $Z$ is $$\mathcal{F}_n{\text -}measurable$$ r.v., then $$E[YZ \vert \mathcal{F}_n] = Z \cdot E[Y \vert \mathcal{F}_n]$$
  - Independence, Linearity, Tower Property (7p)

- Example 1.1.1 ~ 1.1.3

- Filtration $$\mathcal{F}_n$$ 의 정의에서 비현실적일 수 있는 부분은 시간이 지나도 정보를 잃지(lost) 않는다고 보는 점 (9p)

## 1.2 Martingales

---

2024.02.03

A model of a **fair game**.  
여기서 말하는 'fair'는 흡사 미시경제 choice under uncertainty에서 배우는 **'공정'한 보험, '공정'한 도박처럼 기댓값이 0인 경우**를 의미하는 것으로 보임.

- A sequence of r.v. $$M_0, M_1, ...$$ 은 다음 조건을 만족할 때 **martingale w.r.t. the** $$\mathcal{F}_n$$ 라고 한다.

  - n에 대해 $$M_n$$ 은 $$\mathcal{F}_n{\text -}measurable$$ r.v.이고 $$ \mathbb{E}[\lvert M_n \rvert] < \infty$$ 이다.
  - If $$m < n$$, then $$E[M_n \vert \mathcal{F}_m]=M_m$$. <span style="color:gray">또는 $$E[M_n - M_m \vert \mathcal{F}_m]=0$$</span>
    - $$\forall n, E[M_{n+1} \vert \mathcal{F}_n]=M_n$$ 에 conditional expectation의 tower property를 적용하면 $$m < n$$ 에 대해서도 모두 적용 가능. <span style="color:gray">$$E[M_{n+2} \vert \mathcal{F}_n]=M_n$$ 처럼</span> (10p)

### Example 1.2.1.

위 example에서 이어짐. independent한 $$X_1, X_2,...$$ 에 대해 $$\mathbb{E}[X_j]=0$$이고 $$S_n=X_1+...+X_n$$ 이면 $$E[S_n \vert \mathcal{F}_m]=S_m$$ 이 성립. 이는 $$S_n$$ **이 martingale w.r.t.** $$\mathcal{F}_n$$ 이라는 뜻

### Example 1.2.3. Discrete stochastic integral

$$M_j$$는 대상 자산의 가격, $$B_j$$는 베팅금(음수는 숏), $$W_n$$이 winnigs라 하고 $$W_n=\sum_{j=1}^{n}{B_j[M_j-M_{j-1}]}=\sum_{j=1}^{n}{B_j\Delta M_j}$$ 라 하면 $$W_n$$ **은 martingale** w.r.t. $$\mathcal{F}_n$$ **이다.**

### Example 1.2.4. Martingale betting strategy

유명한 베팅금을 두 배씩 올리는 전략을 모델링함.
$$B_1=1, B_j=2^{j-1}$$ 이라 하면 $$W_n=\sum_{j=1}^{n}{B_j\Delta M_j}=\sum_{j=1}^{n}{B_jX_j}$$  
 $n$ 번의 게임을 다 질 확률이 $$\frac{1}{2^n}$$ 인데, **무한히 시도해서 이길 확률을 1로 만들면** $$W_{\infty}=\lim_{n \rightarrow \infty} W_n=1$$ 이 되고  
 $$1 = \mathbb{E}[W_{\infty}] > \mathbb{E}[W_0] = 0$$ 이 된다.

- Example 1.2.3과 1.2.4의 차이가 말하는 것은, **finite time 내에는 martingale을 이길 수(beat) 없다는 것**이다.

- 위와 같이 $$E[M_n \vert \mathcal{F}_m] \ge M_m$$ 이면 **Submartingale**. (14p)  
  <span style="color:gray">sub, super라는 네이밍은 harmonic function과 맞춘 것</span>

## 1.3 Optional sampling theorem

---

2024.02.03

Optional sampling theorem 또는 Optional stopping theorem은 Discrete stochastic integral의 special case로  
특정 stopping time에서의 martingale의 기댓값은 initial expected value와 같음을 의미.[^fn1]  
<span style="color:gray">다시 한 번, 유한한 시간 내에서는 martingale을 이길 수 없다는 의미</span>

### Theorem 1.3.1. Optional Sampling Theorem I

- stoppin time $T$ 와 martingale w.r.t. $$\mathcal{F}_n$$ 인 $$M_n$$ 에 대해  
  $$for \ each \ n, \mathbb{E}[M_{n \wedge T}] = \mathbb{E}[M_0]$$ <span style="color:gray">where $$n \wedge T = min\{n,T\}$$</span>

<span style="color:red">skip</span>

## 1.4 Martingale convergence theorem

---

2024.02.03

### Theorem 1.4.1. Martingale Convergence Theorem

- martingale w.r.t. $$\mathcal{F}_n$$ 인 $$M_n$$ 에 대해 $$\mathbb{E}[\lvert M_n \rvert] \le C \forall n$$ 인 $$C < \infty$$ 이 존재하면, $$\lim_{n \rightarrow \infty} M_n=M_{\infty}$$ 인 **r.v.** $$M_{\infty}$$이 존재한다.
- example 1.2.4에서 $$1 = \mathbb{E}[W_{\infty}] > \mathbb{E}[W_0] = 0$$ 이었던 것럼, $$\mathbb{E}[M_{\infty}]=\mathbb{E}[M_0]$$ 를 따르지 않는다.
- 증명 생략 (19~21p)

### <span style="color:red">Polya's urn</span>

- time $$n=0$$ 에는 빨간 공과 초록 공이 1개씩 있고, 매번 하나를 꺼내서 색을 본 후 같은 색의 공 2개를 다시 넣음. 각 색의 공의 개수는 $$R_n, G_n$$ 이라 하면 $$R_n + G_n = n + 2$$ 성립
- 어느 순서에서 어느 색의 공을 뽑았는지와 관련이 없으니 **Markov Property**도 있음
- $$M_n=\frac{R_n}{R_n+G_n}$$ 이라 하면 $$M_n$$ 은 martingale w.r.t. $$\mathcal{F}_n$$ 이면서 martingale convergence theorem도 만족함.
- 이와 유사한 Bayesian statistics 예시: $$Bern(\theta)$$ 를 따르는 시행의 결과만 보고 $$\theta$$ 값을 근사하기 ($$\theta$$ 의 확률로 성공)
  - $$\theta$$ 를 **어떤 prior distribution을 따르는 r.v.로 가정**. 처음에는 **prior distributino이 Uniform(0,1)이라 가정**
  - 관찰을 통해 **어떤 posterior distribution를 업데이트 해나감.**
  - $n$ 번의 시도 후 총 성공 횟수를 $$S_n=k$$ 라 하면, posterior의 conditional expectation $$\mathbb{E}[\theta \vert S_n=k]=\frac{S_n+1}{n+2}$$ 로 polya's urn에서의 martingale과 같은 형태가 됨. ($$S_n+1$$이 빨간 공의 개수라고 본다면)
  - 그렇다면 martingale convergence theorem을 이용해 law of large number를 통해 $$\theta$$ 를 근사하는 것으로 볼 수 있음.

## 1.5 Square integrable martingales

---

2024.02.03

$$\mathbb{E}[M_n^2]<\infty \ for \ each \ n$$ 이면 martingale $$M_n$$ 은 **square integrable**이라 한다.

- r.v. $$X, Y$$ 가 $$\mathbb{E}[XY]=\mathbb{E}[X]\mathbb{E}[Y]$$ 이면 **orthogonal**하다고 함. (1)
  - r.v.들이 independent이면 orthogonal이지만, orthogonal이라고 항상 independent하지는 않음.
  - 또한 r.v. $$X_1, ... , X_n$$ 이 모두 mean zero이며 **pairwise orthgonal**하면, $$\mathbb{E}[X_jX_k]=0 for j \ne k$$ 이고 $$\mathbb{E}[(X_1, ... , X_n)^2]=\sum_{j=1}^{n}{\mathbb{E}[X_j]^2}$$ 이 성립한다. (2)

### Proposition 1.5.1

Martingale의 increment가 항상 independent하지는 않지만, **sqaure integrable mantingale의 increment는 항상 orthogonal하다.** (25p)

- Square integrable martingale $$M_n$$ w.r.t. the $$\mathcal{F}_n$$ 에 대해, $$for \ m < n, \mathbb{E}[(M_{n+1}-M_n)(M_{m+1}-M_m)] = 0$$  
  <span style="color:gray">위의 (1)에 따라 martingale의 increments는 orthogonal함</span>
- $$\forall n, \mathbb{E}[M_n^2]=\mathbb{E}[M_0^2]+\sum_{j=1}^{n}{\mathbb{E}[(M_j-M_{j-1})^2]}$$  
   <span style="color:gray"> 위의 (2)</span>

<br>
<span style="color:gray"> 증명 생략</span>

## 1.6 Integrable with respect to random walk

---

2024.02.03

mean zero, variance $$\sigma^2$$ 의 i.i.d.인 r.v. $$X_1, X_2, ...$$ 에 대해 $$S_n=X_1+...+X_n, \mathcal{F}_n = filtration \ generated \ by \ X_1, ... , X_n$$ 이라 하자.
$$\mathcal{F}_{n-1}{\text -}measurable$$ 인 $$J_n$$ 에 대해 integral of $$J_n$$ w.r.t. $$S_n$$ 은 다음과 같이 정의된다.

$$Z_n=\sum_{j=1}^{n}{J_jX_j}=\sum_{j=1}^{n}{J_j \Delta S_j}$$

그리고 이 integral 만족하는 다음의 세 가지 중요한 property들은:

1. Martingale Property: $$Z_n$$ 은 martingale w.r.t. $$\mathcal{F}_n$$ 이다. (Section 1.2 참고)
2. Linearity: $$\sum_{j=1}^{}{(aJ_j+bK_j) \Delta S_j}=a\sum_{j=1}^{}{J_j \Delta S_j}+b\sum_{j=1}^{}{K_j \Delta S_j}$$
3. Variance rule: $$Var\biggr[ \sum_{j=1}^{n}{J_j \Delta S_j} \biggr]=\mathbb{E}\biggr[ (\sum_{j=1}^{n}{J_j \Delta S_j})^2 \biggr]=\sigma^2\sum_{j=1}^{n}{J_j^2}$$

## 1.7 A maximal inequality

---

2024.02.03

### Theorem 1.7.1.

$$Y_n$$ 이 nonnegative submartingale w.r.t. $$\mathcal{F}_n$$ 이고 $$\overline{Y}=max\{Y_0, Y_1, ... , Y_n\}$$ 이면 다음이 성립한다.

$$\forall a > 0, \ \mathbb{P}\{\overline{Y}_n \ge a \} \le a^{-1}\mathbb{E}[Y_n]$$

<span style="color:gray">형태는 Markov Inequality와 유사한 모습. $$P(X\ge a) \le a^{-1}\mathbb{E}[X]$$</span>  
<span style="color:gray">증명 생략</span>

### Corollary 1.7.2.

$$M_n$$ 이 square integrable martingale w.r.t. $$\mathcal{F}_n$$ 이고 $$\overline{M}=max\{\lvert Y_0 \rvert, \lvert Y_1 \rvert, ... , \lvert Y_n \rvert\}$$ 이면 다음이 성립한다.

$$\forall a > 0, \ \mathbb{P}\{\overline{M}_n \ge a \} \le a^{-2}\mathbb{E}[M_n^2]$$

$$\mathbb{E}[M_n^2]<\infty \ for \ each \ n$$ 이면 martingale $$M_n$$ 은 **square integrable**이라 한다.

## 1.8 Exercises

---

(Skip)

## References

---

[^fn1]: [https://en.wikipedia.org/wiki/Optional_stopping_theorem](https://en.wikipedia.org/wiki/Optional_stopping_theorem){:target=”\_blank”}
