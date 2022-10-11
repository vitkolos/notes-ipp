# Úvod

## Cvičení

- kam.mff.cuni.cz/~tancer
- Kapitoly z diskrétní matematiky
- https://matematika.reseneulohy.cz
- https://stream.cuni.cz, nahrávka na YouTube (Diskrétní matematika Nešetřil)
- diskrétní matematika – protipól ke spojité matematice
- často konečné objekty
- důkazy matematickou indukcí

### Příklady

- 6. topinky – za 6 minut
	- 2 minuty opékat 1A, 2A
	- 2 minuty 1B, 3A
	- 2 minuty 2B, 3B
- 1. indukce – viz sešit 
	- lze indukovat tak, že dokážeme platnost tvrzení pro $n = 1$, $n = 2$ a následně pro $n + 2$

## Přednáška

- zkouška
	- teorie z přednášek – umět definovat, formulovat tvrzení, dokázat je
	- nemusíme si pamatovat důkazy z přednášek
	- je potřeba, abychom na zkoušce předvedli cokoliv, co funguje
- https://mj.ucw.cz/vyuka/dm/

### Definice

* $a \backslash b$ (a dělí b)
	* $a \backslash b \equiv \exists c : b = a \cdot c$
* prvočíslo

$definice \rightarrow tvrzení \xrightarrow{důkaz} věta$

- lemma – pomocné tvrzení sloužící k dokázání větší věty
- definicí zavádíme pojem pomocí jednodušších pojmů
- axiomatický přístup – definice objektů pomocí jejich vlastností (axiomů)

### Důkazy

- důkaz sporem
	- budeme předpokládat, že tvrzení neplatí, následně dokážeme, že je nemožné, aby tomu tak bylo
	- příklad
		- **Tvrzení:** Prvočísel je nekonečně mnoho.
		- **Důkaz:** sporem: Nechť $p_1, p_2, \dots, p_n$
		- viz sešit
- důkaz indukcí
	- chceme: $\forall n \in \mathbb{N}: \phi(n)$
	- poznámka: do přirozených čísel na této přednášce řadíme nulu
	- uděláme: $\phi(0)$, indukční krok $\forall n(\phi(n) \Rightarrow \phi(n+1))$
	- příklad
		- **Tvrzení:** $2^0 + 2^1 + \dots + 2^n = 2^{n+1}-1$
		- **Dk:** indukcí podle n
			1) zákl. případ: $n=0$ ......... 1=1
			2) krok: IP: 

### Relace

- vztahy mezi dvojicemi objektů
- např. rovnost přirozených čísel
- "krabička" se dvěma vstupy (na pořadí záleží) → vrátí nám ano nebo ne
- můžeme vyjmenovat všechny dvojice, pro které nám krabička vrátí ano
- kartézský součin $X × Y := \{(x,y) | x \in X, y \in Y\}$
- Df: Relace mezi množinami X, Y je libovolná podmnožina X × Y.
- Relace na množině X ... mezi X, X.

- příklad – pro X = {1, 2, 3, 4, 5}
	- $(x,y) \in R$ zkrátíme na xRy
	- rovnost
		- R = {(1,1), (2,2), (3,3), (4,4), (5,5)}
		- diagonální relace – $\Delta_X := \{(x,x) | x \in X\}$
	- dělitelnost x \\ y
	- $x+y \leq 5$
	- $\emptyset$ prázdná relace
	- X × Y univerzální relace

- Df: pro relace $R \subseteq X × Y$ definujeme inverzní relaci $R^{-1} \subseteq Y × X$
	- $\forall x \in X, \forall  \in Y: yR^{-1}x \equiv xRy$
- Df: pro relace $R \subseteq X×Y$ a $S \subseteq Y×Z$ definujeme jejich složení $R \circ S \subseteq X×Z:$
	- $\forall x \in X, \forall z \in Z: x(R \circ S)z \equiv (\exists y \in Y: xRy \& ySz)$
- příklad
	- $R \subseteq X×Y, \Delta_Y$
	- $R\circ \Delta_Y = R$