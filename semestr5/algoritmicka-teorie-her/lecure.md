# Algorithmic Game Theory

- game theory
	- we want to mathematically model the interactions between rational agents
- normal-form game … $(P,A,u)$
	- $P$ … finite set of $n$ players
	- $A=A_1\times\dots\times A_n$ … set of action profiles
		- $A$ … set of all possible states of the game
		- $A_i$ … set of actions available to player $i$
	- $u=(u_1,\dots,u_n)$
		- $u_i:A\to\mathbb R$ … utility function for player $i$
		- assigns happiness of each player to every possible state of the game
		- sometimes is used cost function instead, $c_i=-u_i$
	- knowing the utility function, every player $i$ choose an action $a_i$ from $A_i$ (all players at the same time)
- strategies
	- prescription how player $i$ chooses his actions from $A_i$
	- pure strategy $s_i$ of player $i$ is an action from $A_i$
		- "select a single action and play it"
		- pure-strategy profile … $(s_1,\dots,s_n)$ where $s_i\in A_i$ for each player $i$
	- mixed strategy $s_i$ of player $i$ is a probability distribution over $A_i$
		- $\forall a_i\in A_i:s_i(a_i)\in[0,1]$ so that $\sum_{a_i\in A_i} s_i(a_i)=1$
		- $s_i(a_i)$ … probability that $i$ chooses $a_i$ as their action
		- $S_i$ … set of all mixed strategies of player $i$
		- mixed-strategy profile … $(s_1,\dots,s_n)$ where $s_i\in S_i$ for each player $i$
	- every pure strategy is a special case of a mixed strategy
- expected payoff
	- in $G=(P,A,u)$, the expected payoff for player $i$ of the mixed-strategy profile $s=(s_1,\dots,s_n)$ is $$u_i(s)=\sum_{a=(a_1,\dots,a_n)\in A}u_i(a)\cdot \prod_{j=1}^n s_j(a_j)$$
- linearity of the expected payoff
	- $u_i(s)=\sum_{a_i\in A_i}s_i(a_i)\cdot u_i(a_i;s_{-i})$
	- notation
		- $s_{-i}=(s_1,\dots,s_{i-1},s_{i+1},\dots,s_n)$
		- $(s'_i;s_{-i})=(s_1,\dots,s_{i-1},s'_i,s_{i+1},\dots,s_n)$
- normal form games – examples
	- games for two players
	- bimatrix games – we can use two matrices to express utilities
	- prisoner's dilemma – testify × remain silent
		- paradoxically, the only stable solution is when both testify
	- matching pennies
		- each player chooses heads or tails
		- if pennies match, player 1 wins, otherwise player 2 wins
		- zero-sum game (as well as rock-paper-scissors)
	- battle of sexes (manželský spor)
		- (husband, wife)
		- football × opera
		- if they disagree → (0,0)
			- they attend the events separately
		- if they agree
			- (football, football) → (2,1)
			- (opera, opera) → (1,2)
		- there's not a best outcome/solution
	- game of chicken (hra na zbabělce)
		- two drives drive towards each other on a collision course
		- turn × go straight
		- (turn, turn) → (0,0)
		- (turn, go straight) → (1,-1)
		- (go straight, turn) → (1,-1)
		- (go straight, go straight) → (-10,-10)
			- both die
- best response of player $i$ to a strategy profile $s_{-i}$
	- mixed strategy $s^*_{-i}$ such that $u_i(s_i^*;s_{-i})\geq u_i(s'_i;s_{-i})$ for each $s_i'\in S_i$
	- if player $i$ knew the strategies of other players, the player would choose this one
	- it maximizes his expected payoff if others play $s_{-i}$
- Nash equilibrium
	- for a normal-form game $G=(P,A,u)$ of $n$ players, a Nash equilibrium (NE) in $G$ is a strategy profile (…)
- remarks
	- neither best responses nor Nash equilibria are determined uniquely
	- rock-paper-scissors – unique mixed Nash equilibrium (both players play everything with probability 1/3)
	- battle of sexes – three Nash equilibria, two pure and one mixed
	- in every game, there is a Nash equilibrium
- preparations for the proof of Nash's theorem
	- the proof is essentially topological
	- we need Brouwer fixed-point theorem
	- df: for $d\in\mathbb N$, a subset $X$ of $\mathbb R^d$ is compact $\equiv$ $X$ is closed and bounded
	- df: $Y\subseteq\mathbb R^d$ is convex $\equiv$ every line segment containing two points from $Y$ is fully contained in $Y$
		- formally: $(\forall x,y\in Y)(\forall t\in[0,1]):tx+(1-t)y\in Y$
	- df: for $n$ affinely independent point s $x_1,\dots,x_n\in\mathbb R^d$, an $(n-1)$-simplex $\Delta_n$ on $x_1,\dots,x_n$ is the set of convex combinations of the points $x_1,\dots,x_n$
		- each simplex is a compact convex set in $\mathbb R^d$
	- lemma
		- (…)
	- Brower's Fixed Point Theorem
		- $\forall d\in\mathbb N$, let $K$ be a non-empty compact convex set in $\mathbb R^d$ and $f:K\to K$ be a continuous mapping
		- then, there exists a fixed point $x_0\in K$ for $f$, that is, $f(x_0)=x_0$
