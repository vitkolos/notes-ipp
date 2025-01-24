# Zkouška

## Normal-form games

- Definition: Normal-form game
	- hra v normální tvaru je trojice $(P,A,u)$
	- $P$ … konečná množina $n$ hráčů
	- $A=A_1\times\dots\times A_n$ je množina akčních profilů
		- $A_i$ … množina akcí $i$-tého hráče
	- $u=(u_1,\dots,u_n)$, kde $u_i:A\to\mathbb R$ je užitková funkce $i$-tého hráče
- Definition: Strategies
	- čistá (pure) strategie $s_i$ hráče $i$ je akce z $A_i$
		- profil čistých strategií je $n$-tice čistých strategií (akcí) – za každého z $n$ hráčů je tam jedna
	- smíšená (mixed) strategie $s_i$ hráče $i$ je pravděpodobnostní distribuce přes $A_i$
		- tedy $s_i(a_i)\in[0,1]$ a $\sum_{a_i\in A_i}s_i(a_i)=1$
		- profil smíšených strategií je $n$-tice smíšených strategií
	- každá čistá strategie je smíšená
- Definition: Expected payoff
	- ve hře $G=(P,A,u)$ je expected payoff (střední hodnota výplatní funkce) pro hráče $i$ z profilu smíšených strategií $s$ je $$u_i(s)=\sum_{a\in A} u_i(a)\cdot \underbrace{\prod_{j=1}^n s_j(a_j)}_{P(a)}$$
	- platí linearita střední hodnoty výplatní funkce $$u_i(s)=\sum_{a_i\in A_i} s_i(a_i)\cdot u_i(a_i;s_{-i})$$
- Example: Five basic games
	- vězňovo dilema
	- matching pennies
	- battle of sexes
	- game of chicken
	- bitva o duši Gothamu

## Nash equilibrium

- Definition: Best response
- Definition: Nash equilibrium
- Theorem: Nash’s Theorem
- Definition: Pareto optimality

## Zero-sum games

- Definition: Zero-sum game and its representation
- Theorem: Worst-case optimal strategies and NE
- Theorem: The Duality Theorem
- Theorem: The Minimax Theorem

## Bimatrix games

- Definition: Bimatrix game, nondegenerate bimatrix game
- Theorem: Best response condition
- Algorithm: Support enumeration
- Definition: Best response polyhedra, best response polytope
- Theorem: NE and Best response polyhedra/polytope
- Algorithm: Vertex enumeration
- Algorithm: Lemke–Howson algorithm
- Theorem: Computational complexity of NASH

## Other notions of equilibria

- Definition: $\varepsilon$-Nash equilibrium
- Theorem: Algorithmic aspects of $\varepsilon$-Nash equilibria
- Definition: Correlated equilibrium (CE)
- Theorem: Properties of correlated equilibria

## Regret minimization

- Definition: Regret minimization model
- Definition: External regret
- Theorem: External regret as a suitable metric
- Algorithm: Greedy algorithm
- Algorithm: Randomized greedy algorithm
- Algorithm: Polynomial weights algorithm
- Algorithm: No-regret dynamics

## Applications of regret minimization

- Theorem: Modern proof of the Minimax Theorem
- Definition: Coarse correlated equilibrium (CCE)
- Theorem: Converging to CCE
- Definition: Internal and swap regret
- Algorithm: No-swap-regret dynamics
- Theorem: Reduction from external regret to swap regret
- Theorem: Converging to CE

## Games in extensive form

- Definition: Extensive game, (im)perfect-information game
- Definition: Strategies in extensive games
- Definition: Games of perfect recall, Kuhn’s theorem
- Definition: Sequence form
- Theorem: Using the sequence form to find NE

## Mechanism design

- Definition: Single item auction
- Definition: Dominant strategy, social surplus, awesome auction
- Theorem: Vickrey’s auction is awesome
- Definition: Single parameter environment
- Example: Some single parameter environments
- Theorem: Myerson’s lemma

## Applications of mechanism design

- Definition: Social surplus, Bayesian model
- Theorem: Maximizing expected revenue
- Theorem: Vickrey with reserve price is optimal
- Theorem: The Bulow–Klemperer theorem
- Definition: Knapsack auction
- Theorem: 2-approximation for knapsack auctions
- Definition: Multi-parameter mechanism design
- Theorem: VCG mechanism
- Theorem: Revelation principle
