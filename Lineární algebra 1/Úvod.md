# Úvod

- kam.mff.cuni.cz/~hladik/LA
- sehnat skripta

## Soustavy lineárních rovnic

- matice
	- reálná matice typu m × n je obdélníkové schéma (tabulka) reálných čísel (v kulatých závorkách)
	- prvek na pozici $(i,j)$ matice A (i-tý řádek, j-tý sloupec) značíme $a_{ij}$ nebo $A_{ij}$
	- ...
- vektor
	- sloupcový vektor – matice typu n × 1
	- řádkový vektor – matice typu 1 × n
	- standardně uvažujeme vektory sloupcové
	- množina n-rozměrných vektorů se značí $\mathbb{R}^n$
	- obecné matice značíme velkými písmeny, vektory malými písmeny
- $*$ notace
	- i-tý řádek matice A se značí $A_{i*}$
	- j-tý sloupec matice A se značí $A_{*j}$
- soustava lineárních rovnic
	- mějme soustavu m lineárních rovnic o n neznámých
$$
\begin{aligned}
a_{11}x_1+a_{12}x_2+\dots+a_{1n}=b_1\\
a_{11}x_1+a_{12}x_2+\dots+a_{1n}=b_1
\end{aligned}
$$ ...
- 
	- matice soustavy je matice levé strany
	- rozšířená matice soustavy obsahuje i pravou stranu (b)
- geometrický význam soustavy rovnic
	- nejprve případ m = n = 2, tedy dvě rovnice o dvou neznámých
		- za obecných předpokladů ($a_{11} \not= 0$ nebo $a_{21} \not= 0$) popisuje první rovnice přímku v rovině R^2 a analogicky druhá rovnice
		- řešení soustavy leží v průsečíku dvou přímek
	- tři rovnice o třech neznámých – průnik rovin může být i prázdná množina
	- obecně rovnice určují tzv. nadroviny
- elementární řádkové úpravy
	1. vynásobení i-tého řádku reálným číslem $\alpha \not= 0$ (tj. vynásobí se všechny prvky řádku)
	2. přičtení $\alpha$-násobku j-tého řádku k i-tému, přičemž $i \not= j$ a $\alpha \in \mathbb{R}$
	3. výměna i-tého a j-tého řádku
- tvrzení: elementární řádkové operace zachovávají množinu řešení soustavy
	- idea důkazu – základní myšlenkou je ukázat, že elementární úpravou se množina řešení nemění
- výměna řádků pomocí ostatních úprav
	- od j-tého řádku odečtu i-tý
	- j-tý řádek přičtu k i-tému (na i-tém je nyní j-tý)
	- od j-tého odečtu j-tý (na j-tém je nyní $-$i-tý)
	- j-tý řádek vynásobím $-1$
- odstupňovaný tvar matice (REF)
	- ![[ref.jpg]]
	- řádky 1, ..., r jsou nenulové
	- řádky r + 1, ..., m jsou nulové
	- pod každým pivotem je nula (?)
	- ...
	- bázický a nebázický sloupec
- hodnost matice
	- počet nenulových řádků po převodu do odstupňovaného tvaru, značíme $rank(A)$
	- 