# Zkouška

## Relační algebra

- operace
	- množinové $R\cup S,\;R\cap S,\;R\setminus S,\; R\times S$
	- selekce $R(\text{cond})$
	- projekce $R[\text{attr1},\text{attr2}]$
	- spojení $R[\text{cond}]S$
	- přirozené spojení $R*S$
	- přejmenování $R\braket{\text{attr1}\to\text{x1},\text{attr2}\to\text{x2}}$
	- dělení $R\div S$
- přirozené spojení
	- spojení na základě atributů se stejným názvem v obou tabulkách
	- pokud ho chceme použít na dvě stejné tabulky, je potřeba rozumně použít projekci
- dělení
	- vrací největší možný výsledek takový, aby jeho kartézský součin s dělitelem byl „podmnožinou“ dělence
	- příklad
		- A … tabulka s dvojicemi (film, herec)
		- B … tabulka se jmény herců
		- A ÷ B … tabulka s názvy takových filmů, v nichž hrají všichni herci s tabulky B

## Normální formy a funkční závislosti

- normální formy
	- 1NF
		- všechny atributy jsou atomického typu (nejsou to seznamy, objekty apod.)
		- předpokládáme, že platí
	- 2NF
		- 1NF + neexistuje závislost neklíčového atributu na **části** klíče
	- 3NF
		- 1NF + neexistuje tranzitivní závislost neklíčového atributu na klíči
		- alternativně: 1NF + každá závislost patří do jedné ze tří skupin:
			- triviální: nadmnožina → podmnožina
			- závislost na (nad)klíči
			- atribut vpravo je součástí nějakého klíče
	- BCNF
		- 1NF + každý atribut je přímo závislý na klíči
		- alternativně: dovoluje jen triviální závislosti a závislost na (nad)klíči
- funkční závislosti
	- rozepsání na elementární závislosti
		- tak, aby byl jeden atribut na pravé straně
		- závislosti s více atributy vpravo prostě „rozepíšu“
	- redukce redundantních atributů
		- máme závislosti, kde vpravo je jeden atribut, vlevo jich ale může být více
		- jsou všechny atributy vlevo potřeba?
			- pokud odeberu určitý atribut z levé strany, bude výsledná funkční závislost součástí uzávěru?
			- uzávěr $X^+$ množiny atributů $X$ podle množiny funkčních závislostí $F$ = všechny atributy, které jsou funkčně závislé na $X$ podle $F$
				- jejich závislost lze odvodit pomocí [Armstrongových axiomů](https://en.wikipedia.org/wiki/Armstrong%27s_axioms)
		- jinými slovy
			- máme $X\to y$, uvažujeme o odebrání atributu $a\in X$
			- $a$ můžeme odebrat, pokud $y\in (X\setminus\set{a})^+$ podle $F$
	- odstranění redundantních závislostí
		- závislost je redundantní, pokud může být odvozena z ostatních
		- takto testujeme každou závislost – vyjmeme ji a zkoušíme, zda ji lze odvodit z ostatních závislostí
		- závislost $X\to y$ můžeme odebrat, pokud $y\in X^+$ podle $F\setminus\set{X\to y}$
	- po postupné aplikaci těchto tří kroků (rozepsání, redukce atributů, odstranění závislostí) bychom měli získat minimální pokrytí množiny funkčních závislostí
	- nalezení klíčů
		- terminologie
			- množinu všech atributů označíme $A$
			- nadklíč $X$ je taková množina atributů, že $X^+=A$
			- klíč $K$ je taková množina atributů, že $K$ je redukovaný superklíč
				- takových klíčů může být více
		- nalezení 1\. klíče
			- uvažujeme funkční závislost $A\to A$, kde $A$ je množina všech atributů
			- použijeme algoritmus redukce redundantních atributů
		- nalezení dalších klíčů
			- máme známý klíč $K$ a závislost $X\to Y$ takovou, že průnik $K\cap Y$ je neprázdný a $X\not\subseteq K$ (tedy $X$ obsahuje nějaké atributy navíc)
			- pak $K'=(K\cup X)\setminus Y$ je nadklíč $R(A)$, neporovnatelný s $K$ inkluzí
				- ten musíme opět redukovat
	- možný postup dekompozice
		- …
		- bezztrátové spojení
			- pokud provádíme dekompozici relací podle funkčních závislostí, přirozeným spojením rozložených relací získáme původní relaci
			- ale může dojít ke ztrátě funkčních závislostí
				- mohli bychom přidat další tabulku se ztracenou závislostí
	- zachování závislostí při dělení podle normálních forem
		- …

## Transakce

- uspořádatelnost rozvrhu
- konfliktní uspořádatelnost
- pohledová uspořádatelnost
- zamykací protokol
- 2PL
- S2PL

## Teorie

### Multimédia

- Popište naivní způsob, jak rozšířit Tabulku pro potřeby hledání v obrázcích. Jaké jsou možnosti a omezení tohoto přístupu?
- Definujte klasický podobnostní model pro dva obrázky, vysvětlete z jakých funkcí se skládá. Na „toy example” ukažte princip hledání v DB, kde je 5 obrázků.
- Definujte moderní podobnostní model pro text a obrázek, vysvětlete z jakých funkcí se skládá. Na „toy example” ukažte princip hledání v DB, kde je 5 obrázků.
- Popište Bayesovský model pro hledání za pomocí zpětné vazby. Popište všechny kroky jedné iterace.

### Moderní DB systémy

- Popište limity relačního modelu pro Big Data, které jsou popsány v přednášce.
- Key-value – popište model, jaké podporuje základní funkce, názvosloví tabulek atp. v Riak, na jaké úkoly je model vhodný a na jaké ne.
- Column-family – popište model, jaké podporuje základní funkce, názvosloví tabulek atp. v Cassandra, na jaké úkoly je model vhodný a na jaké ne.
- Document DB – popište model, jaké podporuje základní funkce, názvosloví tabulek atp. v MongoDB, na jaké úkoly je model vhodný a na jaké ne.
- Graph DB – popište model, jaké podporuje základní funkce, na jaké úkoly je model vhodný a na jaké ne.

### Datové struktury a optimalizace

- Nad jakými sloupci je vhodné vytvořit index založený na B+-stromu / bitmapách? Uveďte příklad.
- Popište změny v rychlosti databázových operací nad tabulkou po vytvoření (no)clusterovaného indexu nad nějakým sloupcem.
- Popište hlavní rozdíly mezi clusterovaným a neclusterovaným indexem.
- Popište (ne)výhody použití tříděného souboru oproti souboru netříděnému (heap-file) z hlediska rychlosti DB operací pro ukládání záznamů tabulky.
