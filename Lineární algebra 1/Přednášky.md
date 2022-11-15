# Lineární algebra: přednášky

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
- i-tý jednotkový vektor
	- na pozici i má jedničku, všude jinde nuly
	- jednotková matice se skládá z jednotkových vektorů
- matice a lineární zobrazení $f: x \mapsto Ax$
	- $A \in R^{m×n}$
	- $f: R^n→R^m$
	- $f(x)=Ax$
- numerická stabilita při řešení soustav – pozor na zaokrouhlení!
- Hilbertova matice
- řešení nestability – pomocí parciální pivotizace
- interpolace polynomem

## Grupy

- algebraická struktura tvořená množinou spolu s binární operací, která je asociativní, má neutrální prvek a každý prvek má svou inverzi
- Abelova grupa – je komutativní
- konečná grupa $Z_5$ kde $3+4=2$ protože $7\mod 5=2$
- neabelovské grupy
- negrupy – sčítání na přirozených číslech (chybí inverze), odčítání (není asociativní)
- důkaz jedné z vlastností
	- $a \circ c = b \circ c \quad /\circ c^{-1}$
	- $a \circ c \circ c^{-1} = b \circ c \circ c^{-1}$
	- $a \circ e = b \circ e$
	- $a = b$
- permutace
- symetrická grupa
- tělesa – mají dvě operace
- 0a = 0a + 0 = 0a + 0a – 0a = (0 + 0)a – 0a = 0a – 0a = 0
- $Z_n$ je těleso $\iff n$ je prvočíslo
- jak sestrojit těleso o velikosti $p^n$?
	- prvky jsou polynomy
	- GF

## Vektorové prostory

- vektorový prostor nad tělesem T je množina V s operacemi sčítání vektorů a násobení vektoru skalárem
	- těleso T má neutrální prvky 0 pro sčítání a 1 pro násobení
	- (V, +) je Abelova brupa, neutrální prvek značíme o, inverzní k v značíme –v
	- platí asociativita, distributivita (pro skaláry i vektory), jednička je neutrální u násobení vektoru skalárem
- značení
	- vektory = prvky vektorového prostoru V, značíme latinkou (bez šipek)
	- skaláry = prvky tělesa T, značíme řeckými písmeny
- příklady
	- artimetický prostor $\mathbb{R}^n$ nad $\mathbb{R}$
	- obecněji $\mathbb{T}^n$ nad $\mathbb{T}$ (axiomy vektorového prostoru pak vyplývají z vlastností tělesa)
	- prostor matic
	- prostor P reálných polynomů proměnné x
	- prostor $\mathcal{P}^n$ polynomů z P stupně nanejvýš n (nemůže být vždycky n, aby tam byl neutrální prvek při sčítání)
- vektorový prostor $\mathcal{F}$
	- prvky – reálné funkce $f:\mathbb R → \mathbb R$
	- součet vektorů – (f + g)(x)
	- vynásobení vektoru skalárem – 3f(x)
- tvrzení (základní vlastnosti vektorových prostorů
	- 0v = o
	- $\alpha$o = o
	- …
- podprostor
	- buď V vektorový prostor nad T – pak U je podprostorem V, pokud tvoří vektorový prostor nad T se stejně vektorovými operacemi
	- značení $\Subset$
	- dva triviální podprostory prostoru V jsou V a $\{o\}$
	- libovolná přímka v rovině procházející počátkem je podprostorem $\mathbb R^2$, jiná ne
	- $\mathcal P^n \Subset \mathcal P \Subset \mathcal C \Subset \mathcal F$
	- podprostory musí být nad stejným tělesem
	- vlastnost „býti podprostorem“ je tranzitivní
	- průnik podprostorů je podprostor
	- sjednocení podprostorů nemusí být podprostor
- lineární obal množiny W … span(W)
	- průnik všech podprostorů, které obsahují množinu W → nejmenší možný podprostor obsahující množinu W
	- pokud W je podprostorem prostoru V, pak W = span(W)
- generátory
	- span(W) = U → W generuje prostor U, prvky množiny W jsou generátory prostoru U
	- prostor U se nazývá konečně generovaný, jestliže je generovaný nějakou konečnou množinou vektorů
	- hledáme co nejmenší počet generátorů
	- existují množiny, které nejsou konečně generované – např. množina funkcí
- lineární kombinace
	- je to kombinace konečně mnoha vektorů (pro jednoduchost)
- pomocí lineárních kombinací můžeme vygenerovat celý lineární obal konečné množiny vektorů
- řešení rovnic, nadroviny
- matice
- lineární nezávislost – pokud součet nějakých násobků vektorů je nulový vektor pouze tehdy, když jsou všechny koeficienty nulové
	- nenulový vektor je lineárně nezávislý
	- nulový vektor je lineárně závislý
	- prázdná množina je lineárně nezávislá
	- příklad
		- sloupce regulární matice ($Ax=0 \implies x=0$)
- vektory jsou lineárně závislé právě tehdy, když se jeden z nich dá vyjádřit jako lineární kombinace ostatních
- vektory jsou lineárně závislé $\iff$ můžu z nich jeden vyloučit a pořád mi to bude generovat stejný vektorový podprostor
- báze = lineárně nezávislý systém generátorů
	- báze prostoru V je tedy minimální systém generátorů prostoru V
	- systém vektorů = uspořádaná množina vektorů
	- v $\mathbb{R}^n$ kanonická báze $e_1, e_2, \dots, e_n$
- každý vektor prostoru se dá vyjádřit jako jednoznačná lineární kombinace bazických vektorů
- souřadnice vektoru vzhledem k bázi
- dimenze
- lineárně nezávislých vektorů musí být méně (nebo stejně), než jaká je dimenze prostoru
	- pokud je jich stejně, tak tvoří bázi
- dimenze podprostoru je menší nebo rovna dimenzi prostoru (pokud se dimenze rovnají, tak se podprostor rovná prostoru)
- všechny možné podprostory podle dimenzí, Haasův diagram
- spojení podprostorů
