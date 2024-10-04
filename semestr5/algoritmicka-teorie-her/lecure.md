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
