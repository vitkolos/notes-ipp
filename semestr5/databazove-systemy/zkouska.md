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
- normální formy
	- 1NF
		- všechny atributy jsou atomického typu (nejsou to seznamy, objekty apod.)
		- předpokládáme, že platí
	- 2NF
		- 1NF + neexistuje závislost neklíčového atributu na **části** klíče
	- 3NF
		- 1NF + neexistuje **tranzitivní** (nepřímá) závislost neklíčového atributu na klíči
		- alternativně: 1NF + každá závislost patří do jedné ze tří skupin:
			- triviální: nadmnožina → podmnožina
			- závislost na (nad)klíči
			- atribut vpravo je součástí nějakého klíče
	- BCNF
		- 1NF + každý atribut je přímo závislý na klíči
		- alternativně: dovoluje jen triviální závislosti a závislost na (nad)klíči
			- tedy je silnější než 3NF
- dekompozice
	- cíl: aby byl výsledek v 3NF nebo BCNF
	- možný postup dekompozice
		- vyberu první závislost, která brání normální formě $X\to y$
			- relaci rozdělím na dvě
			- jedna relace bude odpovídat $X\to y$
			- v druhé bude vše kromě $y$
				- místo závislostí $y\to *$ tam budou jejich tranzitivní alternativy $X\to *$
			- případně tento krok opakuju
		- bezztrátové spojení
			- pokud provádíme dekompozici relací podle funkčních závislostí, přirozeným spojením rozložených relací získáme původní relaci
		- ale může dojít ke ztrátě funkčních závislostí
			- např. v situaci $a → b$, $b → c$, $c → d$, $d → e$
				- pokud vyjmeme $b→c$, ztratí se závislost $c\to d$ (místo ní tam bude $b\to d$, což platí tranzitivně, ale už ne původní závislost)
			- mohli bychom přidat další tabulku se ztracenou závislostí
	- zachování závislostí při dělení podle normálních forem
		- řetízek funkčních závislostí $a\to b\to c\to d\to e$ jsme dělili od prostředka
		- mohli bychom ho ale dělit od kraje, tak se nám žádná závislost neztratí
		- asi dává největší smysl začít od konce (takže závislostí $d\to e$, která porušuje 3NF)

## Transakce

- transakce
	- časová posloupnost operací, která končí příkazem commit nebo abort
	- plánovač zpracovává několik transakcí najednou – řídí, jaká operace se provede dřív
	- rozvrh = pořadí provedení operací
- uspořádatelnost rozvrhu
	- sériový rozvrh – transakce (jejich operace) se provádějí postupně, pro $n$ transakcí existuje $n!$ sériových rozvrhů
	- pro zvýšení efektivity dává smysl střídavě provádět operace z různých transakcí
		- ale prolínání nemůže být libovolné – u dvojic s alespoň jedním zápisem závisí na pořadí operací (dvojice read/read může být v libovolném pořadí)
	- rozvrh je uspořádatelný (serializable), pokud je ekvivalentní libovolnému sériovému rozvrhu
- konfliktní uspořádatelnost
	- konfliktní dvojice: $R(A)\to R(A)$, $R(A)\to W(A)$, $W(A)\to R(A)$
		- operace jsou v různých transakcích
		- šipka odpovídá časové posloupnosti
	- dva rozvrhy jsou konfliktně ekvivalentní, pokud mají stejnou množinu konfliktních dvojic
	- rozvrh je konfliktně uspořádatelný, pokud je konfliktně ekvivalentní nějakému sériovému rozvrhu
	- konfliktní uspořádatelnost nezohledňuje zotavitelnost (abort/rollback) ani insert/delete na databázových objektech
	- detekce konfliktní uspořádatelnosti – pomocí precedenčního grafu
		- vrcholy jsou commitnuté transakce
		- orientované hrany odpovídají konfliktním dvojicím
		- rozvrh je konfliktně uspořádatelný, pokud je graf acyklický
- pohledová uspořádatelnost
	- slabší než konfliktní uspořádatelnost
		- využíváme zde toho, že pokud do konkrétní položky $n$-krát zapisujeme (kde $n\geq 3$) a mezi těmito zápisy ji nečteme, můžeme prvních $n-1$ zápisů provést v libovolném pořadí
	- dva rozvrhy jsou pohledově ekvivalentní pokud platí tyto 3 podmínky:
		- pokud operace $O$ čte počáteční hodnotu $X$ v jednom rozvrhu, platí to i ve druhém
		- pokud operace $O$ zapisuje koncovou hodnotu $X$ v jednom rozvrhu, platí to i ve druhém
		- pokud operace $O_1$ čte $X$ zapsané operací $O_2$, platí to i ve druhém
	- pohledově uspořádatelný rozvrh je pohledově ekvivalentní nějakému sériovému rozvrhu
- zotavitelnost
	- ze všech konfliktních dvojic vyznačíme ty, kde dochází ke čtení nepotvrzených dat
		- poznámka: pokud k jednomu čtení vede („konfliktní“) šipka ze dvou zápisů,  „zotavitelná“ šipka bude jen z toho posledního (protože to jsou ta nepotvrzená data, která se reálně čtou)
	- tak vznikne graf (snad acyklický), který určuje pořadí commitů a případně abortů
- zamykací protokol
	- operace
		- $S(A)$ … zamčení sdíleného zámku
		- $X(A)$ … zamčení exkluzivního zámku
		- $U(A)$ … odemčení zámku
	- dobrá formovanost transakcí
		- před $R$ aspoň $S$
		- před $W$ aspoň $X$
		- na konci vše korektně odemknuté
- 2PL (2fázový zamykací protokol)
	- po prvním unlocku už se nesmí zamykat → nejdřív se zamyká, pak se odemyká
	- každý vyhovující rozvrh je konfliktně uspořádatelný, nemusí být zotavitelný
- S2PL (striktní 2fázový zamykací protokol)
	- explicitní unlock je zakázaný
	- odemčení

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
