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