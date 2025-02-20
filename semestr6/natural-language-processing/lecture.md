# Lecture

- credit
	- homeworks
	- attendance to practicals is mandatory, 3 absences allowed at maximum
	- final test

## Probability, information theory

- sample space $\Omega$
- event $A$ as a set of basic outcomes
	- $A\subseteq\Omega$
- we can estimate the probability of event $A$ by experiment
	- we divide the number of $A$ occurring by the number of experiments
	- maximum likelihood estimation
- axioms
	- $p(A)\in[0,1]$
	- $p(\Omega)=1$
	- $p(\bigcup A_i)=\sum p(A_i)$
- joint probability, conditional probability
- estimating conditional probability
- Bayes rule
- independence
- chain rule
- golden rule of statistical NLP
- expectation
- entropy
	- nothing can be more uncertain than the uniform distribution
- perplexity
	- $G(p)=2^{H(p)}$
- joint entropy, conditional entropy
- entropy is non-negative
- chain rule
	- $H(X,Y)=H(Y\mid X)+H(X)$
- $H(Y\mid X)\leq H(Y)$
- other properties of entropy
- coding interpretation
	- entropy … the least average number of bits needed to encode a message
- KL distance (divergence)
- mutual information
	- $I(X,Y)=D(p(x,y)\Vert p(x)p(y))$
	- we can derive that $I(X,Y)=H(X)-H(X\mid Y)$
		- by symmetry $I(X,Y)=H(Y)-H(Y\mid X)$
- cross-entropy
