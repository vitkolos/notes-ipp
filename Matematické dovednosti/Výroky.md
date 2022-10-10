# Výroky

## Klíčové výrazy

- elementární výroky $A, B, C, A_1, A_2, \dots$
- logické spojky
	- a = konjunkce $\land$
	- nebo = disjunkce $\lor$
	- implikace $\implies$
		- $(A \implies B) \equiv (\neg A \lor B)$
		- $(A \implies B) \equiv (\neg B \implies \neg A)$
	- ekvivalence $\iff$
		- $(A \iff B) \equiv ((A \implies B) \land (B \implies A))$
	- negace $\neg A \equiv \bar{A}$
		- $\neg (\neg A)$
- závorky $( )$

## Vlastnosti spojek

- komutativita – konjunkce, disjunkce, ekvivalence
- asociativita – konjunkce, disjunkce
- dvojí implikace
	- Jestliže mrzne, tak pokud prší, tvoří se námraza.
	- $((M \land P) \implies L) \equiv (M \implies (P \implies L))$
- distributivita – u konjunkce a disjunkce funguje oběma způsoby, stejný princip u množinových operací průniku a sjednocení
	- $A \land (B \lor C) \equiv (A \land B) \lor (A \land C)$
	- $A \lor (B \land C) \equiv (A \lor B) \land (A \lor B)$
- odvození konjunkce z disjunkce a obráceně
	- $(A \lor B) \equiv \neg (\neg A \land \neg B)$
	- $(A \land B) \equiv \neg (\neg A \lor \neg B)$
- odvození konjunkce a disjunkce z implikace
	- $(A \land B) \equiv \neg (A \implies \neg B)$
- všechny logické operace pomocí jedné spojky se dvěma parametry – spojka NAND nebo NOR

## Negace spojek

