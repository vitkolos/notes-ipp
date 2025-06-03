# Základy umělé inteligence

## Řešení úloh prohledáváním

- formulace úlohy
	- agent – vnímá prostředí pomocí senzorů, aktuátory mu umožňují jednat
		- racionální agent
			- zvolí akci, která maximalizuje jeho výkon
		- simple reflex agent
			- observation → action
		- model-based reflex agent
			- past state + past action + observation → state
			- state → action
		- goal-based agent
			- state + goal → action
	- reprezentace stavů agenta
		- atomic – stav je blackbox
			- dá se použít prohledávání
		- factored – stav je vektor
			- dá se použít constraint satisfaction, výroková logika, plánování
		- structured – stav je sada objektů, ty jsou propojeny
			- dá se použít (predikátová) logika prvního řádu
	- problem solving agent – typ goal-based agenta
		- atomická reprezentace stavů
		- cíl = množina cílových stavů
		- akce = přechody mezi stavy
		- hledáme posloupnost akcí, kterými se dostaneme z výchozího do nějakého cílového stavu
		- očekáváme, že prostředí je plně pozorovatelné, diskrétní, statické a deterministické
		- příklad – Lloydova patnáctka
			- ne všechny stavy jsou dosažitelné – zachovává se parita permutace
	- formulace problému
		- budeme potřebovat abstrakci prostředí (odstraníme detaily z prostředí)
			- validní abstrakce = abstraktní řešení můžeme expandovat do reálného řešení
			- užitečná abstrakce = vykonávání akcí v řešení je jednodušší než v původním problému
		- dobře definovaný problém
			- výchozí stav
			- přechodový model `(state, action) -> state`
			- goal test (funkce, která odpoví true/false podle toho, zda je daný stav cílový)
- stromové vs. grafové prohledávání
	- udržujeme si hranici (frontier) prozkoumané oblasti
	- graph-search si navíc ukládá „uzavřenost“ vrcholu (jestli už jsme vrchol viděli)
		- takže nenastávají problémy s cykly
		- kvůli tomu, že stavový prostor může být nekonečný, neinicializujeme všechny vrcholy, ale místo toho použijeme hešovací tabulku
	- i tree-search lze použít k prohledávání grafů s cykly, ale může se chovat divně
	- u prohledávání DAGů tree-search nezaručuje, že se prohledané stavy nebudou opakovat (opakovat se můžou, pokud do stejného vrcholu vedou dvě orientované cesty)
- neinformované prohledávání (DFS, BFS, uniform-cost search)
	- BFS (fronta)
		- nejmělčí neexpandovaný vrchol je zvolen k expanzi
		- úplný pro konečně větvící grafy
		- optimální – pokud je cena cesty nerostoucí funkce hloubky
		- časová a prostorová složitost $O(b^{d+1})$, kde $b$ je stupeň větvení (branching factor, maximální výstupní stupeň) a $d$ je hloubka nejbližšího cíle
		- problém je s prostorovou složitostí
	- DFS (zásobník)
		- nejhlubší neexpandovaný vrchol je zvolen k expanzi
		- úplný pro graph-search
			- úplný = nalezne řešení vždy, když existuje (a v opačném případě hlásí, že řešení neexistuje)
		- neúplný pro tree-search (pokud algoritmus pustíme na grafu, který není strom)
		- suboptimální – nesměřuje k cíli
		- časová složitost $O(b^m)$, kde $m$ je maximální hloubka libovolného vrcholu
		- prostorová složitost $O(bm)$
		- pokud použijeme backtracking (generujeme jenom jednoho následníka místo všech), tak nám stačí dokonce jenom $O(m)$ paměti
			- DFS využívá to, že nám stav může vrátit všechny následníky (pak je držíme v paměti)
			- backtracking v daném vrcholu generuje jednoho následníka (takže všechny ostatní nemusíme držet v paměti)
				- ale někdy se nedá generovat jenom jeden následník
	- rozšíření BFS o funkci určující cenu kroku (tedy cenu hrany)
		- Dijkstrův algoritmus
		- taky se tomu říká uniform-cost search
		- $g(n)$ označuje cenu nejlevnější cesty ze startu do $n$
		- místo fronty použijeme prioritní frontu
- informované prohledávání (algoritmus A*, přípustné a konzistentní heuristiky)
	- best-first search
		- pro vrchol máme ohodnocovací funkci $f(n)$
		- $f(n)$ použijeme v Dijkstrově algoritmu místo $g(n)$
		- máme heuristickou funkci $h(n)$, která pro daný vrchol označuje odhadovanou cenu nejlevnější cesty do cílového stavu
		- best-first je třída algoritmů, kde máme uzly ohodnoceny nějakou funkcí a vybíráme nejmenší z nich
		- greedy best-first search
			- $f(n)=h(n)$
			- není optimální ani úplný
		- A\* algoritmus
			- $f(n)=g(n)+h(n)$, kde $h(n)$ je heuristika
			- optimální a úplný
			- typicky mu dojde paměť dřív než čas
	- co chceme od heuristiky $h(n)$ u algoritmu A*
		- přípustnost – $h(n)$ musí být menší rovna nejkratší cestě z daného vrcholu do cíle, musí být nezáporná
		- monotónnost (= konzistence)
			- mějme vrchol $n$ a jeho souseda $n'$
			- $c(n,a,n')$ je cena přechodu z $n$ do $n'$ (akcí $a$)
			- heuristika je monotónní, když $h(n)\leq c(n,a,n')+h(n')$
		- tvrzení: monotonie implikuje přípustnost, opačná implikace neplatí
		- tvrzení: pro monotónní heuristiku jsou hodnoty $f(n)$ neklesající po libovolné cestě
		- tvrzení: pokud je $h(n)$ přípustná, pak je A* u tree search optimální
			- do cíle nevedou žádné suboptimální cesty, takže si vystačíme s důkazem optimality Dijkstrova algoritmu
		- tvrzení: pokud je $h(n)$ monotónní, pak je A* u graph search optimální
			- s nemonotónní heuristikou jsme mohli najít suboptimální cestu do cíle
	- když heuristika $h_2$ dává větší hodnoty než $h_1$, tak se říká, že $h_2$ dominuje $h_1$
		- pokud je $h_2$ přípustná a pokud se $h_2$ nepočítá výrazně déle než $h_1$, tak je $h_2$ zjevně lepší než $h_1$

## Splňování omezujících podmínek

- problém splňování podmínek
- hranová konzistence (algoritmus AC-3)
- algoritmus hledání řešení (MAC)

## Logické uvažování

- základy výrokové logiky (konjunktivní a disjunktivní normální forma)
- algoritmus DPLL
- dopředné a zpětné řetězení (Hornovské klauzule)
- rezoluce

## Pravděpodobnostní uvažování

- základy teorie pravděpodobnosti (úplná sdružená distribuce, nezávislost, Bayesovo pravidlo)
- pravděpodobnostní uvažování (vysčítání, normalizace)
- Bayesovské sítě: konstrukce a vztah k úplné sdružené distribuci
- Bayesovské sítě: exaktní odvozování (enumerace, eliminace proměnných)
- Bayesovské sítě: aproximační odvozování (Monte Carlo, zamítání, vážení věrohodností)

## Reprezentace znalostí

- situační kalkulus, problém rámce
- Markovské modely – filtrace, predikce, vyhlazování, nejpravděpodobnější průchod
- skryté Markovské modely (HMM) vs. dynamické Bayesovské sítě

## Automatické plánování

- formulace plánovacího problému (definice operátoru)
- dopředné a zpětné plánování

## Markovské rozhodovací procesy (MDP)

- formulace problému (výpočet užitku, strategie)
- Bellmanova rovnice
- iterace hodnot, iterace strategií
- POMDP (základní definice)

## Hry a teorie her

- algoritmy Minimax a alfa-beta prořezávání
- základy teorie her (vězňovo dilema, Nashovo ekvilibrium)
- mechanism design (typy aukcí)

## Strojové učení

- základní druhy učení (s učitelem, bez učitele, zpětnovazební)
- rozhodovací stromy (definice, konstrukce)
- regrese, SVM (základní principy)
- Bayesovské učení, EM algoritmus
- pasivní zpětnovazební učení (definice, metody ADP a TD)
- aktivní zpětnovazební učení (definice, explorace vs. exploitace, Q-učení, SARSA)
