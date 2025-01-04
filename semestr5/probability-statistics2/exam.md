# Exam

## Markov Chains

## Bayesian Statistics

## Conditional Expectation

## Balls & Bins

- Really useful approximation
	- $1-x\approx e^{-x}$
	- example usage: birthday paradox
		- $(1-\frac1{365})(1-\frac2{365})\dots(1-\frac{k-1}{365})\approx e^{-\frac{k(k-1)}{2\cdot 365}}$
		- because $1-\frac1{365}\approx e^{-\frac1{365}}$ etc.
- Union bound
	- for events $A_1,A_2,\ldots$ it holds that $P(\bigcup A_i)\leq \sum P(A_i)$
	- therefore $P(\text{none of }A_i)\geq 1-\sum P(A_i)$
- Balls and bins model
	- we will be throwing $m$ balls randomly into $n$ bins
	- $X_i$ … number of balls in bin $i$
- How many bins are empty?
	- $P(X_i=0)=(1-\frac1n)^m\approx e^{-\frac mn}$
	- $I_i=1$ if $X_i=0$ (otherwise 1)
	- $\mathbb E(\sum_i I_i)=\sum_i\mathbb EI_i\approx ne^{-\frac mn}$
- How many balls are in bin $i$?
	- $X_i\sim \text{Bin}(m,\frac 1n)\approx\text{Pois}(\frac mn)$
	- $\mathbb EX_i=\frac mn$
- Max-load likely upper bound
	- definition: max-load … $\max\set{X_1,\dots,X_n}$
	- theorem: for large enough $n$ we have $P(\text{maxload}\geq\frac{3\log\log n}{\log n})\leq\frac1n$
	- proof
		- …
- Max-load likely lower bound
	- theorem: for large enough $n$ we have $P(\text{maxload}\leq\frac{\log\log n}{\log n})\leq\frac1n$
	- proof
		- …
- Exact case vs. Poisson case
	- theorem: any event that happens with probability $\leq p$ in the Poisson case happens with probability $\leq p\cdot e\sqrt m$ in the exact case
	- proof
		- …

## Stochastic Processes

- Bernoulli process
	- infinite sequence of independent identically distributed Bernoulli trials
	- sequence of RVs $X_1,X_2,\dots$ that are independent and each follows $\text{Ber}(p)$ distribution
	- $X_k=1$ … success/arrival at time $k$
- Quantities of a Bernoulli process
	- $N_t$ … number of successes up to time $t$
		- $N_t\sim\text{Bin}(t,p)$
		- $\mathbb E[N_t]=t\cdot p$
	- $T_k$ … time of the $k$-th success
	- $L_k=T_k-T_{k-1}$
		- waiting time
		- memory-less
		- $L_k\sim\text{Geom}(p)$
			- $\mathbb E[L_k]=\frac1p$
			- $P(L=l)=(1-p)^{l-1}\cdot p$
	- $T_k$ properties
		- $T_k=L_1+\dots+L_k$
		- by linearity $\mathbb E[T_k]=\frac kp$
		- $T_k$ has Pascal distribution of order $k$
		- $P(T_k=t)=\begin{cases}{t-1\choose k-1}p^{k}(1-p)^{t-k} & \text{for }t\geq k\\ 0& \text{otherwise}\end{cases}$
- Alternative description of a Bernoulli process
	- we can describe the situation by the interarrival times
	- i.i.d. random variables $L_1,L_2,\ldots\sim\text{Geom}(p)$
	- $T_k=L_1+\dots+L_k$
	- $X_k=1$ whenever $T_t=k$ for some $t$
	- clearly, the sequence $X_1,X_2,\dots$ is a Bernoulli process
- Merging of Bernoulli processes
	- two independent Bernoulli processes, $Z_i=X_i\lor Y_i$
	- $BP(p)\text{[merge with]}BP(q)=BP(1-(1-p)(1-q))$
	- $=BP(p+q-pq)$
- Splitting of Bernoulli processes
	- $X_i,Y_i,Z_i$
	- if $Z_i=0$, then $X_i=Y_i=0$
	- if $Z_i=1$, then with probability $q$ we set $(X_i,Y_i)=(1,0)$, otherwise $(X_i,Y_i)=(0,1)$
- Poisson process
	- continuous time
	- $T_1,T_2,T_3,\dots$ are the times of individual arrivals
	- $N_t$ … number of arrivals up to time $t$
	- $\lambda$ … intensity (how many successes per unit of time)
	- $N_t\sim\text{Pois}(\lambda\cdot t)$
	- $L_k\sim\text{Exp}(\lambda)$
	- $T_k$ has Erlang distribution, $\mathbb E[T_k]=\frac k\lambda$
- Poisson process interval independence
	- for any sequence $0\leq t_0\lt t_1\dots\lt t_k$
	- RVs $(N_{t_i}-N_{t_{i+1}})$
		- are independent
		- each one follows $\text{Pois}(\lambda(t_{i+1}-t_i))$
- Merging of Poisson process
	- $PP(\lambda)\text{[merge with]}PP(\lambda')=PP(\lambda+\lambda')$
- Splitting of Poisson process
	- for each success of $PP(\lambda)$, we toss a coin with probability $p$ (with probability $p$, the success is counted as valid)
	- the resulting process is $PP(\lambda p)$

## Non-parametric Tests

- Permutation test
	- two-sample test
	- A/B testing
		- $A$ … control group (no treatment)
		- $B$ … group with treatment applied
		- is the $A$ vs. $B$ difference only random?
	- we observe … $T(A,B)$
		- $T$ … test statistic
		- example: $T=\bar A-\bar B$
	- $\mathcal F=\set{T(\pi(A\cup B))\mid \pi\in S_{m+n}}$
	- p-value: percentage of $\mathcal F$ more extreme than observed $T(A,B)$
	- speed-up … we use only $k$ random samples from $S_{m+n}$
	- for paired test, we only permute $X_i$ with $Y_i$
- Signed test
	- paired test
		- pairs $X_i,Y_i$
		- $Z_i=Y_i-X_i$
	- $H_0$ … $P(X_i\gt Y_i)=\frac12$
	- count number of pairs where $Z_i\gt 0$ (there was a measurable improvement after the treatment)
	- use $\text{Bin}(n,\frac12)$ to get the p-value
- Wilcoxon signed rank test
	- paired test
	- procedure
		- let $X_i$ be the difference $B_i-A_i$
		- sort by absolute value, assign ranks ($R_i$)
		- calculate $T$ (or $T^+$ or $T^-$, it does not matter)
			- $T^+=\sum_{X_i\gt 0}R_i$
			- $T^-=\sum_{X_i\lt 0} R_i$
			- $T=T^+-T^-=\sum R_i\cdot\text{sign}(X_n)$
		- compare with scores for measurements with random $+/-$ signs
	- we use stronger null hypothesis
		- $H_0:$ median = 0 & distribution of $X$ is symmetric
		- note: $X$ is symmetric $\iff A,B$ have the same continuous distribution ([source](https://stats.stackexchange.com/questions/348057/wilcoxon-signed-rank-symmetry-assumption))
- Mann-Whitney U-test
	- two-sample test
		- we have two populations, $X$ and $Y$
		- we get $X_1,\dots,X_m$ and $Y_1,\dots,Y_n$
		- usually, $m\neq n$
	- $S(X_i,Y_j)=\begin{cases} 1 & X_i\gt Y_j\\ \frac12 & X_i=Y_j \\ 0 & X_i\lt Y_j\end{cases}$
	- $U=\sum_{i=1}^m\sum_{j=1}^nS(X_i,Y_j)$
	- sign test is a paired variant of this
	- we use the same approach as in the permutation test with $U$ instead of $T=\bar X_m-\bar Y_n$
	- alternative view: we sort $X\cup Y$ and count pairs “$X_i$ before $Y_j$”
	- when to use it?
		- numerical data … real numbers (weight, time, price) → permutation test
		- ordinal data … classes (light/medium/heavy, quick/slow) → $U$-test

## Moment Generating Functions and their applications

- Markov bound
	- for $X$ nonnegative
	- $\forall a\geq 1:P(X\geq a\cdot \mu)\leq\frac1a$
- Chebyshev bound
	- $\forall a\geq 0:P(|X-\mu|\geq a\cdot\sigma)\leq\frac1{a^2}$
- Chernoff bound
	- for $X=\sum_{i=1}^nX_i$ where $X_i\sim\text{Ber}(p_i)$ are independent
	- $\mu=\sum_{i=1}^np_i$
	- $\forall\delta\in(0,1]:P(X\geq (1+\delta)\cdot\mu)\leq e^{-\mu\delta^2/3}$
	- $\forall\delta\in(0,1):P(X\leq(1-\delta)\cdot\mu)\leq e^{-\mu\delta^2/2}$
	- note: there are many more alternative bounds
