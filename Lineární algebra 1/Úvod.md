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
	- ![ref](přílohy/ref.jpg)
	- řádky 1, ..., r jsou nenulové
	- řádky r + 1, ..., m jsou nulové
	- pod každým pivotem (tečka na obrázku) jsou samé nuly
	- ...
	- bázický a nebázický sloupec
- hodnost matice
	- počet nenulových řádků po převodu do odstupňovaného tvaru, značíme $rank(A)$
- algoritmus REF(A)
	- buď $A \in \mathbb{R}^{m×n}$
	1) $i:=1, j:=1$
	2) **if** $a_{kl} = 0$ pro všechna $k \geq i$ a $l \geq j$, then konec
	3) j := min{l; l>= j, akl not 0 pro nějaké k >= i} (přeskočíme nulové podsloupečky)
	4) urči $a_{kj} \neq 0$, k>= i a vyměň řádky Ai* a Ak* (nyní je na pozici pivota hodnota $a_{ij} \neq 0$)
	5) pro všechna k>i polož Ak* := Ak* - akj/aij Ai* (druhá elementární úprava)
	6) polož i := i + 1, j := j + 1 a jdi na krok 2
- algoritmus (Gaussova eliminace)
	- buď dána soustava rovnic (A | b), kde A náleží R^m×n, b náleží R^m
	- převedeme rozšířenou matici soustavy (A | b) na odstupňovaný tvar (A' | b') a označíme r = rank (A | b)
	- nyní nastala právě jediná z následujících tří situací
		- soustava nemá řešení
			- pokud poslední soupec je bázický, čili v posledním sloupci je pivot, tudíž rank(A) < rank(A | b)
			- nula se rovná něčemu nenulovému
		- soustava má alespoň jedno řešení
			- soustava má jediné řešení – pokud r = n, pivoty jsou na diagonále, poslední sloupec je nebázický
			- soustava má nekonečně mnoho řešení – pokud r < n, v matici je více nebázických sloupců
				- bázické proměnné jsou ty, které odpovídají bázickým sloupcům
				- nebázické proměnné jsou ty zbývající... parametry...
- řešitelnost soustavy a hodnost matice
	- hodnost matice (A | b) udává řešitelnost a počet významných rovnic v soustavě
	- Frobeniova věta:  
	  Soustava (A | b) má alespoň jedno řešení právě tehdy, když $rank(A) = rank(A | b)$.

- důkaz komutativity
	- A + B = B + A
	- (A + B)ij = aij + bij
	- (B + A)ij = bij + aij
	- aij + bij = bij + aij, neboť aij, bij jsou reálná čísla, mezi nimiž platí při sčítání komutativita

## Cvičení

- http://elif.cz/LA_2223_2.html
- elif@kam.mff.cuni.cz
- zápočet
	- písemky + aktivita
		- na začátku každého cvičení písemka na 5–10 minut, za každou lze získat 10 bodů (celkem 110)
		- za aktivitu v hodině lze získat dohromady 10 bodů
		- celkem alespoň 60 ze 120 bodů
	- domácí úkoly
		- alespoň 60 ze 120 bodů
		- na webu
		- ideálně jako jeden soubor
		- když pošleme dřív, tak nám může dát možnost si to opravit
		- deadline je začátek následujícího cvičení
	- když budeme mít víc než 80 bodů, tak bude na konci semestru možnost to nějak vyřešit

- popis přímky v rovině
	- obecná rovnice
		- ax + by + c = 0
		- $(a,b) \neq (0,0)$
		- (a, b) je normálový vektor
	- parametrický popis
		- $(a,b)+t\cdot (u,v)=(x,y), t \in \mathbb{R}$
		- $(u,v) \neq (0,0)$
- popis roviny v prostoru ($\mathbb{R^3}$)
	- $ax+by+cz+d=0$
		- $(a,b,c)\neq (0,0,0)$
	- $(x,y,z)=(a,b,c)+s\cdot (u_1,u_2,u_3)+t\cdot (v_1, v_2,v_3), s, t \in R$
		- $(u_1,u_2,u_3)\neq (0,0,0)$
		- $(v_1,v_2,v_3)\neq (0,0,0)$
		- jeden vektor se nesmí rovnat k-násobku druhého
- přímka v prostoru
	- parametricky pomocí jednoho nenulového vektoru
	- rovnicový popis (jako průnik dvou rovin) – neobjeví se teďka na písemce, viz sešit
- kolmost vektorů – jejich skalární součin je nulový

- 1.2 najděte rovnicové vyjádření roviny popsané bodem (3,2,1) a směrovými vektory (1,1,1) a (2,-1,0)
	- je potřeba najít normálový vektor
- 1.3 najděte parametrický popis roviny $2x_1 + 3x_2 + x_3 = 4$
	- existuje více řešení

### Gaussova eliminační metoda

matice soustavy vs. rozšířená matice soustavy (s pravými stranami rovnic)
elementární úpravy
odstupňovaný tvar (REF)

- pokud je matice v REF (o m řádcích a n sloupcích)
	- pak existsuje řádek r, kde první až r-tý řádek jsou nenulové, řádky r + 1 až m jsou nulové
	- pro $p_i=min\{j:a_{ij} \pm 0\}$ platí p1 < p2 < ... < pr
	- pozice (1,p1) ... (r,pr) nazýváme pivoty
	- hodnost matice rank(A) je počet nenulových řádků REF(A)
- redukovaný odstupňovaný tvar (RREF)
	- REF a navíc $a_{1p_1} = a_{rp_r} = 1$
	- $\forall i \in \{1 ... r\}: a_{1p_i} = a_{2p_i} = a_{(i-1)p_1} = 0$
- počítání viz sešit
- na příští písemce pouze analytika (bez Gaussovky)
- doma spočítat úkol, dále 2c a připravit se na písemku