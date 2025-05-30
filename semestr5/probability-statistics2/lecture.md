# Probability and Statistics 2

## Markov chains

- example 1
	- machine in 2 states – working × broken
	- w → b … probability 0.01
	- w → w … 0.99
	- b → w … 0.9
	- b → b … 0.1
- example 2
	- a fly which may get caught in a web … absorbing states
- df: stochastic process (náhodný proces)
	- sequence of random variables $X_0,X_1,\dots$ such that "all probabilities are defined"
		- e.g. $P(X_0=1\land X_1=2\land X_3=0)$ is defined
- df: Markov process/chain
	- stochastic process such that
		- $\exists$ finite/countable set $S:\text{Im}X_t\subseteq S\;\forall t$
			- elements of $S$ … states
			- $t$ … time
		- $(\forall i,j\in S)(\exists p_{ij}\in [0,1])(\forall t)(\forall a_0,a_1,\dots,a_t,a_{t+1})$
	- notes
		- this is a discrete time Markov chain
		- discrete space … $|S|\leq |\mathbb N|$
		- time-homogeneous
			- $p_{ij}$ not depeding on $t$
		- Markov condition
			- only applies if the condition probabilities are defined
		- Markov condition … "forgetting the past"
- df: transition matrix $P=(p_{ij})$
- df: transition diagram/graph
	- vertices … $S$
	- directed edges … $\set{(i,j):p_{ij}\gt 0}$
- observation: every row of $P$ sums to 1
- Markov chain is equivalent to a random walk on the transition diagram
	- from state $i$ we go to $j$ with the probability of $p_{ij}$ independent of the past
- in example 1, assume $X_0$, what is $P(X_2=w)$?
	- $P(X_1=w)=p_{11}=0.99$
	- $P(X_2=w)=p_{11}\cdot p_{11}+p_{12}\cdot p_{21}=0.99\cdot 0.99+0.01\cdot 0.9$
		- using the total probability theorem
- probability mass function (PMF, pravděpodobnostní funkce) for $X_0,X_1,\dots$
	- $\pi_i^{(t)}=P(X_t=i)$
		- $t\in\mathbb N_0$
		- $i\in S$
- theorem
	- $\pi^{(t+1)}=\pi^{(t)}\cdot P$
		- where $\pi^{(t)}=(\pi_1^{(t)},\dots,\pi_n^{(t)})$ row vector
	- proof … definition of matrix multiplication & total probability theorem
- theorem
	- $P(X_0=a_0,X_1=a_1,\dots,X_t=a_t)=\pi_{a_0}^{(0)}\cdot P_{a_0a_1}\cdot P_{a_1a_2}\cdot\ldots\cdot P_{a_{t-1}a_t}$
	- proof by induction
- df: probability of $k$-step transition … $r_{ij}(k)$
	- $r_{ij}(k)=P(X_{t+k}=j\mid X_t=i)$
	- $r_{ij}(1)=P(X_{t+1}=j\mid X_t=i)=p_{ij}$
	- it is independent of $t$
- theorem (Chapman-Kolmogorov)
	- $\forall$ Markov chain, $\forall i,j,k:$
		- $r_{ij}(k+1)=\sum_{u=1}^n r_{iu}(k) p_{uj}$
		- $r_{ij}(k+\ell)=\sum_{u=1}^n r_{iu}(k) r_{uj}(\ell)$
		- $r_{ij}(k)=(P^k)_{ij}$
	- proof
		- 1 is a special case of 2 ($r_{uj}(1)=p_{uj})$
		- $1\implies 3$ … matrix multiplication & induction
		- …
- df: $j$ is accessible from $i$ (where $i,j\in S$)
	- $i\to j$
	- $j\in A(i)$
	- $j$ is accessible from $i\equiv$ $\exists t:\underbrace{P(X_t=j\mid X_0=i)}_{r_{ij}(t)}\gt 0$
	- $\iff$ in the transition digraph exists directed path $i\to j$ of length $t$
- df: $i\leftrightarrow j$ ($i$ and $j$ communicate) $\equiv i\in A(j)\land j\in A(i)$
- theorem: $\leftrightarrow$ is an equivalence relation
- proof
	- reflexive: $i\in A(i)$ … $t=0$ in the definition
	- symmetric: the formula $i\in A(j)\land j\in A(i)$ is symmetric
	- transitive: in the digraph $\exists$ path $i$ to $j$, $\exists$ path $j$ to $k$ $\implies\exists$ walk $i\to k$
- decomposition of the transition digraph to components of strong connectivity $\equiv$ finding equivalence classes of $\leftrightarrow$
- df: a state $i\in S$ is recurrent if we return to it with probability 1
	- it is transient otherwise
	- česky rekurentní, tranzientní
- df: Markov chain is irreducible if $\forall i,j\in S:i\leftrightarrow j$
- df: $T_i=\min\set{t\geq 1:X_t=i}$
	- $T_i=\infty$ if the set is empty (there is no such $t$)
	- $T_i$ … random variable
	- $f_{ij}(n)=P(\text{we get to }j\text{ first at time }n\mid X_0=i)=P(T_j=n\mid X_0=i)$
		- we define it for $n\gt 0$
	- $f_{ij}=P(T_j\lt\infty\mid X_0=i)=\sum_{n\geq 1} f_{ij}(n)$
- $i$ is transient
	- $f_{ii}\lt 1$ … probability of ever getting back
	- $\iff P(T_i=\infty)\gt 0$
	- $\iff P(\text{get back infinitely often})\lt 1$
- example – random walk on a line
	- with probability 1/2 we go to the left
	- $f_{00}(2)=(\frac12)^2+(\frac12)^2=\frac12$
	- $f_{00}(1)=f_{00}(3)=\dots=0$
	- $f_{00}(4)=\frac{1}{2^4}\cdot 2$
		- $r_{00}(4)\neq f_{00}(4)$
		- $r_{00}(4)=\frac{1}{2^4}\cdot 4$
	- is 0 recurrent?
		- by definition, we should add $f_{00}(2)+f_{00}(4)+\dots$ and check if it equals 1
		- theorem: $i$ is a recurrent state $\iff\sum_{n=1}^\infty r_{ii}(n)=\infty$
			- $B_n=\begin{cases} 1&\text{ if }X_n=i\\ 0 &\text{ otherwise}\end{cases}$
				- we got back
				- $\mathbb E(B_n\mid X_0=i)=P(X_n=i\mid X_0=i)=r_{ii}(n)$
			- $r_{00}(2n)=$ probability that out of the $2n$ steps, $n$ were to the left, $n$ were to the right
				- $=\frac1{2^{2n}}\cdot{2n\choose n}\doteq\frac c{\sqrt n}$ … see Matoušek, Nešetřil
			- $\sum_{n=1}^\infty \frac{c}{\sqrt n}=\infty$ (taught in calculus)
			- $\mathbb E(T_0\mid X_0=0)=\infty$ (we did not prove that)
- theorem
	- if $i\leftrightarrow j$, then either both $i$ and $j$ are recurrent or both $i$ and $j$ are transient
- for finite Markov chains
	- $C$ … equiv class of $\leftrightarrow$ in a finite Markov chain
	- $C$ is recurrent ($\forall i\in C$ is recurrent) $\iff(\forall i \in C)(\forall j\in S):$ if $i\to j$ then $j\in C$
		- → $C$ is closed
- stationary distribution / steady state distribution
	- df: $\pi:S\to [0,1]$ such that $\sum_{i\in S}\pi_i=1$ is called a stationary distribution if $\text{``}\pi P=\pi\text{"}$
		- $\forall i:\sum_i\pi_i p_{ij}=\pi_j$
	- if $\pi^{(0)}$ (the PMF of $X_0$) is $\pi$, then $\pi^{(1)}$ is $\pi$ as well
	- $\pi^{(1)}=\pi^{(0)}P$
- theorem: if a Markov chain is finite, aperiodic (→ not periodic) and irreducible, then
	1. $\exists$ unique stat. distribution $\pi$
	2. $\forall i:\lim_{n\to\infty}(P^n)_{ij}=\pi_j$
- example of periodic Markov chain: two states, we change the state with probability 1
- df: $i\in S$ has period $d_i:=\text{gcd}\set{t:r_{ii}(t)\gt 0}$
	- $i\in S$ is aperiodic if $d_i=1$
- df: $i$ is null recurrent if $i$ is recurrent and $\mathbb E(T_i\mid X_0=i)=\infty$
	- $i$ is positive recurrent if $i$ is recurrent and $\mathbb E(T_i\mid X_0=i)\lt\infty$
- example: random walk on a line
- theorem
	- if $i,j\in S$, $i\leftrightarrow j$, then
		- $d_i=d_j$
		- $i$ is transient $\iff j$ is trainsient
		- $i$ is recurrent $\iff j$ is recurrent
		- $i$ is null recurrent $\iff j$ is null recurrent
		- $i$ is positive recurrent $\iff j$ is positive recurrent
	- these are properties of the class of $\leftrightarrow$
- theorem
	- if a Markov chain is irreducible, aperiodic and finite, then
		- there exists a unique stationary distribution $\pi$: $\pi P=\pi$
		- $\forall ij:\lim(P^t)_{ij}=\pi_j$
			- $P(X_t=j\mid X_0=i)\doteq\pi_j$
	- actually, MC does not have to be finite, it suffices if all states are positive recurrent (?)
	- steady state (?)
		- if $\pi^{(0)}=\pi$ then $\pi^{(1)}=\pi$
- the proof is not easy, here is a cheat proof
	- $Pj=Ij$ (row sums are 1)
	- $(P-I)j=0$
	- $P-I$ is sungular matrix
	- $\exists x:x(P-I)=0\implies xP=x$
	- $\pi=\frac xc$ such that $\sum \pi_i=1$
	- problem
		- $x$ may have negative coordinates
		- to fix: use Perron-Frobenius theorem
		- the correct proof is shown in class of probabilistic techniques
- to find $\pi$, solve system of linear equations $\pi P=\pi$, add $\sum_{i\in S}\pi_i=1$
	- $\pi$ describes long-term behavior of the MC
	- Page Rank (original google search) … MC model of people browsing WWW
	- given $\pi$, we can find a MC such that $\pi$ is its stationary distribution; then we can run the MC to generate random objects with distribution $\pi$
		- Markov chain Monte Carlo (MCMC)
- detailed balance equation
	- MC may have this property
	- $\forall i\neq j:\pi_iP_{ij}=\pi_jP_{ji}$
- to imagine this: ant colony moving independently according to a Markov chain
	- stationary distribution $\iff$ the same number of ants at each state at each time – ants don't "accumulate"
- detailed balance equation implies $\pi P=\pi$
	- detailed balance equation is stronger than $\pi P=\pi$
- MCMC algo. sketch
	- choose aperiodic irreducible digraph
	- $p_{ij}=\min\set{1,\frac{\pi _j}{\pi_i}}\cdot C$
	- $p_{ji}=\min\set{1,\frac{\pi_i}{\pi_j}}\cdot C$
	- choose $C$ such that
		- $\forall i:\sum_{j\neq i} p_{ij}\lt 1$
		- df. $p_{ii}=1-\sum_{j\neq i}p_{ij}\gt 0$
		- $\implies d_i=1$
	- tune the process to make convergence fast
- absorbing state $i:p_{ii}=1$
	- $A$ … set of absorbing states
	- question 1: which $i\in A$ we end at?
	- question 2: how fast?
- example: $0\in A$ (?)
	- $a_i=P(\exists t:X_t=0\mid X_0=i)$
- $\mu_i=\mathbb E(T\mid X_0=i)$
	- $T=\min\set{t: X_t\in A}$
- theorem: $(a_i)_{i\in S}$ are the unique solution to
	- $a_0=1$
	- $a_i=0$ if $i\in A,\,i\neq 0$
	- $a_i=\sum_j p_{ij}\cdot a_j$ otherwise
- theorem: $(\mu_i)_{i\in S}$ are unieque solutions to
	- $\mu_i=0$ if $i\in A$
	- $\mu_i=1+\sum_j p_{ij}\mu_j$ if $i\notin A$
- proof
	- $P(\exists t:X_t=0\mid X_0=0)=1$
	- $P(\exists t: X_t=0\mid X_0=i\in A\setminus\set{0})=0$
	- $i\notin A$
		- $B_j=\set{\exists t:X_t=0}$
		- $P(B_i)=\sum_{j\in S} p_{ij}\cdot \underbrace{P(B_i\mid X_1=j)}_{P(B_j)=a_j}$
- example: drunk person on their way home
	- $A=\set{0}$
	- $\mu_0=0$
	- $\mu_1=1+\frac12\mu_0+\frac12\mu_2$
	- $\mu_2=1+\frac12\mu_1+\frac12\mu_3$
	- $\mu_{n-1}=1+\frac12\mu_{n-2}+\frac12\mu_{n}$
	- $\mu_n=1+\mu_{n-1}$
	- solution
		- $\mu_1=2n-1$
		- $\mu_n=n^2$
		- $\mu_{i}\leq n^2$
- 2-SAT problem
	- input: $\varphi=(x_1\lor x_2)\land(x_3\lor\neg x_1)\land\ldots$
		- clauses with exactly 2 literals
	- output: a satisfying assignment OR “unsatisfiable”
	- there exists a polynomial algorithm
	- we will show a randomized algorithm
		1. arbitrarily initialize $(x_1,\dots,x_n)$
		2. while $\varphi$ has an unsatisfied clause
			- choose one of the unsatisfied clauses and change one of its variables
		3. return $(x_1,\dots,x_n)$
	- repeat (2) $\leq2mn^2$ times
		- then, if $\varphi$ is still unsatisfied, return “unsatisfiable”
		- this may introduce errors
	- theorem: the algorithm makes an error with probability $\leq 2^{-m}$
	- proof
		- $x_1^*,\dots,x_n^*$ … one of the satisfying assignments
		- $D_t$ the number of $i$ such that $x_i\neq x_i^*$ at time $t$
			- $t=0,1,\dots,2mn^2$
			- $0\leq D_t\leq n$
			- $D_t=0\implies$ we found a solution
		- situation
			- we assume that clause $(x_1\lor x_2)$ is unsatisfied at time $t$ and we choose it
			- $\implies x_1=x_2=F$
				- $(x_1\neq x_2)$
				- ($x_2\neq\neg x_1)$ … we could remove such clauses
			- $\implies x_1^*\lor x_2^*$ is $T$
			- we randomly switch $x_1$ or $x_2$ which increases or decreases $D$
			- …
	- we can get a 3-SAT randomized algorithm with $(\frac43)^n$ time complexity this way
- Hidden Markov Model (HMM)
	- not observable $(X_t)$ … Markov chain
	- observable $(Y_t)$ … $Y_t$ is obtained from $X_t$
	- widely aplplicable
	- smart algorithm (Vitebri algorithm)

## Probability

- what is probability?
	- $P:\mathcal F\to[0,1]$ such that
		- $P(\Omega)=1$
		- $P(\bigcup A_n)=\sum P(A_n)$ if disjoint
- where to find/use it?
	- randomized algorithms
	- is it possible to have true randomness?
		- hardware methods to sample random bits
		- software methods
			- their independence can be “weak” (for statistics) or “strong” (for cryptography)
- probabilistic method
	- we prove that some graph exists by showing that random graph has certain property with probability greater than zero
	- $G(n,p)$ … graph with vertices $1,\dots,n$
		- $\forall i,j:i\sim j$ with probability $p$ (all independent)
	- $P(G(n,\frac12)$ has no $K_k$ nor $\overline K_k$ as an induced subgraph$)\gt 0$ if $n\leq 2^{k/2}$
	- thus $\exists G$ on $2^{k/2}$ vertices with no induced $K_k$ nor $\overline K_k$
	- Ramsey theorem
- statistics
	- frequentist
		- $P(A)=$ number of good / number of all
		- “in long term repetition”
		- repeat a random experiment independently $n$ times
		- observe that $A$ happens $k$ times
		- $P(A):=k/n$
	- Bayesian
		- P(it will rain tomorrow)
		- subjective probability → betting
			- does satisfy axioms!
		- “random universe”
			- $\Omega$ = set of all possible universes
- Bayes theorem
- MAP (maximum a posteriori)
- $\hat\theta_\text{MAP}=\text{argmax}_\theta\,p_{\Theta\mid X}(\theta\mid x)$
	- $\hat\theta$ is a point estimate for $\Theta$
- that equals $\text{argmax}\,p_\Theta(\hat\theta)\cdot p_{X\mid\Theta}(x\mid\theta)$ as we can ignore the normalization constant
- Beta function
	- $B(\alpha,\beta)=\int_0^1x^{\alpha-1}(1-x)^{\beta-1}=\frac{(\alpha-1)!(\beta-1)!}{(\alpha+\beta-1)!}$
- Beta distribution
	- $f_\Theta(x)=\frac1{B(\alpha,\beta)}x^{\alpha-1}(1-x)^{\beta-1}$
- $(\ln f)'=(c+(\alpha-1)\ln x+(\beta-1)\ln (1-x))'={\alpha-1\over x}-{\beta-1\over 1-x}$
	- in the maximum, this will be equal to zero
	- maximum … $\frac{\alpha-1}{\alpha-1+\beta-1}$
- …
- LMS point estimate
	- LMS = least mean square
	- estimate such that $\mathbb E((\Theta-\hat\theta)^2\mid X=x)$ is minimal
	- to compute it
		- …
- example: measurement error with a normal distribution
- often, the constant in the denominator does not matter
- from posterior $f_{\Theta\mid X}$ we can find
	- point extimates
		- MAP
		- LMS
	- interval estimates
		- confidence intervals (in classical statistics) → credible sets $S$
- sampling
	- rejection sympling
	- MCMC sampling
		- Monte Carlo Markov chains
		- Metropolis Hastings method
		- we construct a MC from the probability distribution we want
		- we run the MC for long enough
- LMS
- $\Theta\mid X=x$
	- mean … LMS = $\min\mathbb E((\Theta-\hat\theta)^2\mid X=x)$
	- median … $\min\mathbb E(|\Theta-\hat\theta|\mid X=x)$
	- modus … MAP
- conditional independence
	- events
		- $A\perp B\iff P(A\cap B)=P(A)\cdot P(B)$
		- $A\perp_C B\iff P(A\cap B\mid C)=P(A\mid C)\cdot P(B\mid C)$
			- $A,B$ are independent conditionally given $C$
	- it is possible (even typical) that $A\perp_C B$, $A\perp_{C^C} B$, but not $A\perp B$
- conditional expectation
	- $\mathbb E(Y\mid X=x)$ vs. $\mathbb E(Y\mid X)$
	- $\mathbb E(Y\mid X=x)=g(x)$ … number
	- $\mathbb E(Y\mid X)=g(X)$ … random variable
	- we proved that $\mathbb E(\mathbb E(Y\mid X))=\mathbb E(g(X))=\mathbb EY$
		- “law of iterated expectation”
	- basic task of statistics
		- estimate one quantity (Y) given data/measurement (X)
	- example: groups of students, their exam results
	- estimator
		- $\hat Y=\mathbb E(Y\mid X)=g(X)$
	- $\tilde Y=\hat Y-Y$
	- we proved that $\mathbb E(\tilde Y\mid X)=0$
		- therefore $\mathbb E(\tilde Y)=\mathbb E(\mathbb E(\tilde Y\mid X))=0$
	- also, $\text{cov}(\tilde Y,\hat Y)=0$
		- they are uncorellated
	- note
		- uncorellated $\impliedby$ independent
		- uncorellated $\centernot\implies$ independent
	- conditional variance
	- iterated variance / eve's rule
		- $\text{var }Y=\mathbb E(\text{var}(Y\mid X))+\text{var}(\mathbb E(Y\mid X))$
		- intragroup variance + intergroup variance
- birthday paradox
	- $1-x\approx e^{-x}$
- balls into bins
	- $m$ balls
	- $n$ bins
	- $X_i$ … number of balls in bin $i$
	- birthday paradox … $P(\max X_i\geq 2)$
- questions
	- how many bins are used?
	- approximation of $X_i$
	- max load … $\max\set{X_1,\dots,X_n}$
- $P(X_i=0)=(1-\frac1n)^m\approx e^{-\frac mn}$
	- $I_i=1$ if $X_i=0$ (otherwise 1)
	- $\mathbb E(\sum_i I_i)=\sum_i\mathbb EI_i\approx ne^{-\frac mn}$
- distribution of $X_i$
	- $X_i\sim \text{Bin}(m,\frac 1n)\approx\text{Pois}(\frac mn)$
	- $\mathbb EX_i=\frac mn$
- applications
	- bucket sort
	- hash collisions
- exact case vs. Poisson case
	- theorem: any event that happens with probability $\leq p$ in the Poisson case happens with probability $\leq p\cdot e\sqrt m$ in the exact case
- bernoulli process, poisson process
	- …
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

## Moment generating functions

- today: proof of CLT, proof of Chernoff inequality
- given a random variable $X$, we define $M_X:\mathbb R\to\mathbb R$
- $M_X(s):=\mathbb E(e^{sX})$
- $\forall X:M_X(0)=\mathbb E(e^{0x})=1$
- $X\sim\text{Ber}(p)$
	- $M_X(s)=p\cdot e^{s\cdot 1}+(1-p)\cdot e^{s\cdot 0}$
	- $M_X(s)=1-p+pe^s$
	- note: $e^s=1+s+\frac{s^2}2+\frac{s^3}{3!}+\dots=\sum_{k=0}^\infty\frac{s^k}{k!}$
	- $M_X(s)=1+p(s+\frac{s^2}2+\frac{s^3}{3!}+\dots)$
- theorem: $M_X(s)=\sum_{k=0}^\infty\mathbb E[X^k]\cdot \frac{s^k}{k!}$
	- $\mathbb E[X^k]$ … $k$-th moment of $X$
- proof
	- $\mathbb E[e^{sX}]=\mathbb E[\sum\frac{(sX)^k}{k!}]=\mathbb E[\sum X^k\frac{s^k}{k!}]=\sum\mathbb E[X^k\frac{s^k}{k!}]=\sum_{k=0}^\infty\mathbb E[X^k]\cdot \frac{s^k}{k!}$
- back to Ber(p)
	- $\mathbb EX=[s^1]M_X(s)=p$
		- this notation selects the coefficient of the $s^1$ in the GF
	- $\mathbb EX^2=[\frac{s^2}{2!}]M_X(s)=p$
- $X\sim N(0,1)$
	- $M_X(s)=\mathbb E[e^{sX}]\overset{\text{LOTUS}}{=}\int_{-\infty}^\infty e^{sx}f_X(x)\text { d}x$
	- …
	- $M_X(s)=e^{s^2/2}$
- theorem: $M_{aX+b}(s)=e^{sb}M_X(as)$
- proof: …
- example usage
	- $X\sim N(\mu,\sigma^2)$
	- $\frac{X-\mu}{\sigma}=Y\sim N(0,1)$
	- $X=\sigma Y+\mu$
	- $M_X(s)=e^{\mu s}\cdot e^{\sigma^2 s^2/2}$
- theorem
	- let $X,Y$ be RVs such that $(\exists\varepsilon\gt 0)(\forall s\in (-\varepsilon,\varepsilon)):M_X(s)=M_Y(s)\in\mathbb R$
	- then $F_X=F_Y$
- example
	- $X_1\sim N(\mu_1,\sigma^2_1)$
	- $X_2\sim N(\mu_2,\sigma^2_2)$
	- $\implies X_1+X_2\sim N(\mu,\sigma^2)$
	- proof
		- $M_{X_1}=\text{exp}(\mu_1s+\sigma_1^2s^2/2)$
		- $M_{X_2}=\text{exp}(\mu_2s+\sigma_2^2s^2/2)$
		- …
- theorem
	- $X,Y$ independent $\implies M_{X+Y}=M_X\cdot M_Y$
- proof
	- $M_{X+Y}(s)=\mathbb E[e^{s(X+Y)}]=\mathbb E[e^{sX}\cdot e^{sY}]=\mathbb E[e^{sX}]\cdot \mathbb E[e^{sY}]=M_X(s)\cdot M_Y(s)$
- example
	- $X\sim\text{Bin}(n,p)$
	- $M_X(s)=(1-p+pe^s)^n$
- theorem
	- $Y,X_1,X_2,X_3,\dots$ RVs
	- $(\exists\varepsilon\gt 0)(\forall s\in (-\varepsilon,\varepsilon)):\lim_{n\to\infty} M_{X_n}(s)=M_Y(s)$
	- $F_Y$ is continuous
	- then $X_n\xrightarrow d Y$
		- $\lim_{n\to\infty} F_{X_n}(s)=F_Y(s)$
- theorem (CLT)
	- $X_1,X_2,\dots$ i.i.d. (independent identically distributed) RVs
	- $\mathbb EX_i=\mu$, $\text{var} X_i=\sigma^2$
	- $Y_n:=\frac{X_1+\dots+X_n-n\mu}{\sqrt{n}\sigma}$
	- $Y_n\xrightarrow d N(0,1)$
		- that is $\lim_{n\to\infty}F_{Y_n}(t)=\Phi(t)$
- proof
	- we may assume $\mu=0$
		- otherwise, we would set $X_n'=X_n-\mu$
		- variance would not change
		- the formula for $Y_n$ also would not change (we subtract $n\mu$ there)
	- $M_{X_i}(s)=1+as+bs^2+O(s^3)\quad(s\doteq 0)$
		- $a=\mu=0$
		- $b=\frac12\mathbb EX_i^2=\frac12(\sigma^2-\mu^2)=\frac12\sigma^2$
	- $M_{X_i}(s)=1+\frac{\sigma^2}2s^2+O(s^3)$
	- $M_{Y_n}(s)=\prod M_{X_i}\left(\frac s{\sqrt n\sigma}\right)$
	- we will use the previous theorem for $Y,Y_1,Y_2,\dots$
	- we need to show that $\lim M_{Y_n}(s)=M_Y(s)$
		- or that $\lim_{n\to\infty}M_{X_n}(\frac s{\sqrt n\sigma})^n=e^{s^2/2}$
	- $M_{X_n}(\frac s{\sqrt n\sigma})^n=…=\text{exp}(n\ln(1+\frac{s^2}{2n}+O(s^3))$
	- …
- theorem (Chernoff inequality)
	- …
- application
	- set balancing
	- discrepancy
	- we have subsets $S_1,\dots,S_n\subseteq[m]$
	- we want $T\subseteq[m]$ such that it almost disects every $S_i$
	- $D_i=|T\cap S_i|-|S_i\setminus T|$
	- $\text{disc}(T)=\max D_i$
	- use random $T$!
	- $D_i=\sum_{j=1}^{|S_i|}X_j$
	- $\forall a_j\in S_i:X_j$ indicator ($X_j=1\iff a_j\in T$)
	- $P(D_i\geq t)\leq e^{-\frac{t^2}{2|S_i|}}$
	- …
	- idea: it is useful to have an inequality (Chernoff) that holds always, we don't need to worry if our $n$ is big enough
