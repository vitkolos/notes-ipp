# Exam

## Markov Chains

## Bayesian Statistics

## Conditional Expectation

## Balls & Bins

- Really useful approximation
	- $1-x\approx e^{-x}$
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

---

- questions
	- max load … $\max\set{X_1,\dots,X_n}$
- applications
	- bucket sort
	- hash collisions
- exact case vs. Poisson case
	- theorem: any event that happens with probability $\leq p$ in the Poisson case happens with probability $\leq p\cdot e\sqrt m$ in the exact case

## Stochastic Processes

## Non-parametric Tests

- statistics – descriptive vs. inferential
	- descriptive – describe what we observed
	- inferential – deduce properties of a larger set
		- how many people are left-handed?
		- we can observe this on a small sample of people
	- observational study vs. randomized study (RCT, randomized control trial)
	- treatment – what you do to experimental units
	- example
		- experimental units … students
		- treatment … which tutorial student attends
			- placebo, control group
		- observational study → we let the students decide which tutorial to attend
		- randomized study → we assign the tutorials to students (randomly)
	- confounders
		- people can get better because they believe they are treated
	- random $\neq$ arbitrary
		- haphazard
	- statistics – parametric vs. non-parametric
		- parametric → observations from parametrized random variables
		- t-test
		- permutation test
- example: earbuds
	- black (4.3/5) vs. navy blue (4/5)
	- descriptive statistics
	- observational study
- example: alpacas
	- permutation test
	- https://www.jwilber.me/permutationtest/
	- we observe … $T(X,Y)$
	- $Z:=X,Y$
	- $\mathcal F=\set{T(\pi(Z))\mid \pi\in S_{m+n}}$
	- p-value: percentage of $\mathcal F$ more extreme than observed
	- speed-up … we use only $k$ random samples from $S_{m+n}$
- tests
	- one-sample test
	- two-sample test
	- paired test
		- quality of wool before/after treatment
		- give black & blue to $n$ testers, ask each tester to score both
			- randomize the order of testing the color
		- use one-sample test on $D_i=X_i-Y_i$
- parametrized statistics … t-test (assuming normal distribution)
- non-parametric version … paired test & permutation test
	- for paired test, we only permute $X_i$ with $Y_i$
- sign test
	- $Y_i=$ "sign of $X_i$"
- example
	- 10 values
	- $H_0$ … median = 0
	- sign $S\sim\text{Bin}(10,\frac12)$
	- one-sided test … $F_S(3)=P(S\leq 3)=0.17$
	- two-sided test … $P(S\leq 3\lor S\geq 7)=0.34$
	- but we are suspicious
		- we can rank absolute values (from lowest to highest) and write the averages of the ranks (for rank 3–5 → the average will be 4)
		- we can multiply that by the sign ($S$)
- test procedure (Wilcoxon signed rank test)
	- data … $X_1,\dots,X_n$
	- ranks of $|X_i|$ … $R_1,\dots,R_n$
	- $T^+=\sum_{X_i\gt 0}R_i$
	- $T^-=\sum_{X_i\lt 0} R_i$
	- $T=T^+-T^-=\sum R_i\cdot\text{sign}(X_n)$
	- $T^++T^-=\sum i=\frac {n(n+1)}2$
	- we will use stronger null hypothesis
		- $H_0:$ median = 0 & distribution is symmetric
	- assuming $H_0$… (and ignoring ties)
		- $T=\sum_{i=1}^n i\cdot V_i$
		- $V_i=\begin{cases}+1 \text{ prob. } 1/2\\ -1\end{cases}$
		- $V_i^+=0/1$
			- $\sim\text{Ber}(\frac12)$
		- $T^+=\sum i\cdot V_i^+$
		- $V_i$ … independent
		- what can we do?
			- we can compute CDF of $T$
			- we can apply CLT to approximate (can we really?)
- back to our example
	- `wilcox` test in R → $0.07$
	- what is correct? $0.07$ or $0.17$?
	- it depends on what we can assume
		- sign test
		- Wilcoxon signed rank test
		- Student's t-test
- power of test
	- $1-P(\text{type II error})$
	- to increase, we have two choices
		- we can get more data
		- or we can make stronger assumptions
			- but we should not cheat – if it is obvious that the data is not normally distributed, we should not say they are
- paired test
	- $X_i=A_i-B_i$
	- null hypothesis … the procedure did not help nor hurt
		- the distribution may be very weird
		- but it will be symmetrical
	- if $A_i,B_i$ have same distribution, then $A_i-B_i$ has distribution symmetrical around 0, median 0
- Mann-Whitney U-test
	- $U=\sum_{i=1}^m\sum_{j=1}^nS(X_i,Y_j)$
	- $S(X_i,Y_j)=\begin{cases} 1 & X_i\gt Y_j\\ \frac12 & X_i=Y_j \\ 0 & X_i\lt Y_j\end{cases}$
	- 2-sample test
	- we have two populations, $X$ and $Y$
		- we get $X_1,\dots,X_m$ and $Y_1,\dots,Y_n$
		- usually, $m\neq n$
	- sign test is a paired variant of this
	- we use the same approach as in the permutation test with $U$ instead of $T=\bar X_m-\bar Y_n$
- types of data
	- numerical … real numbers (weight, time, price)
		- → permutation test
	- ordinal … classes (light/medium/heavy, quick/slow)
		- → $U$-test
- bootstrapping
	- data $X_1,\dots,X_n$ iid
	- sample mean $\bar X_n=\frac1n\sum_{i=1}^n X_i$
		- distr. of $\bar X_n:\mathbb E \bar X_n=\mathbb E X_i=\mu$
		- variance of $\bar X_n:\text{var}\bar X_n=\frac1n\sigma^2$
		- CLT: $\bar X_n$ has $\approx$ Normal distribution $N(\mu,(\frac\sigma{\sqrt n})^2)$
		- $P(\bar X_n\lt a)$ can be approximated by the normal distribution $N$
	- now, we want the same of a different parameter
		- $M$ … median of $X_i$
		- $\hat M=$ sample median: “middle value of $X_1,\dots,X_n$”
		- $X_{\set{1}},\dots,X_{\set{n}}$ … sorted data
		- $\hat M=X_{\set{\frac n2}}$
			- estimator function of data we use to estimate the true $M$
	- bootstrapping … sampling with repetition from $X_1,\dots,X_n$
		- we can approximate the distribution of $\hat M$
	- interval estimate for median $M$
		- $M^*$ … bootstrapped median (median of the one set of bootstrapped data)
		- $M_\alpha^*=\set{x:P(M^*\leq x)=\alpha}$
		- this method is simple and does not depend on the distribution of the data

## Moment Generating Functions and their applications
