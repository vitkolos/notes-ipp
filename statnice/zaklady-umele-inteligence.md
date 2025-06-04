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
	- graph search si navíc ukládá „uzavřenost“ vrcholu (jestli už jsme vrchol viděli)
		- takže nenastávají problémy s cykly
		- kvůli tomu, že stavový prostor může být nekonečný, neinicializujeme všechny vrcholy, ale místo toho použijeme hešovací tabulku
	- i tree search lze použít k prohledávání grafů s cykly, ale může se chovat divně
	- u prohledávání DAGů tree search nezaručuje, že se prohledané stavy nebudou opakovat (opakovat se můžou, pokud do stejného vrcholu vedou dvě orientované cesty)
- neinformované prohledávání (DFS, BFS, uniform-cost search)
	- BFS (fronta)
		- nejmělčí neexpandovaný vrchol je zvolen k expanzi
		- úplný pro konečně větvící grafy
		- optimální – pokud je cena cesty nerostoucí funkce hloubky
		- časová a prostorová složitost $O(b^{d+1})$, kde $b$ je stupeň větvení (branching factor, maximální výstupní stupeň) a $d$ je hloubka nejbližšího cíle
		- problém je s prostorovou složitostí
	- DFS (zásobník)
		- nejhlubší neexpandovaný vrchol je zvolen k expanzi
		- úplný pro graph search
			- úplný = nalezne řešení vždy, když existuje (a v opačném případě hlásí, že řešení neexistuje)
		- neúplný pro tree search (pokud algoritmus pustíme na grafu, který není strom)
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
	- = constraint satisfaction problem (CSP)
	- konečná množina proměnných
	- domény – konečné množiny možných hodnot pro každou proměnnou
	- konečná množina podmínek (constraints)
		- constraint je relace na podmnožině proměnných
		- constraint arity = počet proměnných, které podmínka omezuje
	- chceme přípustné řešení (feasible solution)
		- úplné konzistentní přiřazení hodnot proměnným
		- konzistentní … všechny podmínky jsou splněny
	- CSP můžeme řešit tree-search backtrackingem
		- úpravou proměnných v určitém pořadí můžeme získat větší efektivitu
		- můžeme pročistit hodnoty, které zjevně nesplňují podmínky
			- příklad
				- $a\in\set{3,4,5,6,7}$
				- $b\in\set{1,2,3,4,5}$
				- constraint: $a\lt b$
				- ale např. $a=6$ vůbec nedává smysl
				- odstraněním nekonzistentních hodnot dostaneme $a\in \set{3,4}$, $b\in\set{4,5}$
			- můžeme použít metodu hranové konzistence
- hranová konzistence (algoritmus AC-3)
	- = arc consistency (arc … orientovaná hrana)
	- uvažujme binární podmínky
		- libovolnou n-ární podmínku lze převést na balík binárních podmínek
	- každá binární podmínka odpovídá dvojici orientovaných hran v síti podmínek (vrcholy odpovídají proměnným)
		- pokud je mezi dvěma proměnnými více podmínek, můžeme je sloučit do jedné (abychom neměli multigraf)
	- orientovaná hrana $(V_i,V_j)$ je hranově konzistentní $\equiv$ pro každé $x\in D_i$ existuje $y\in D_j$ takové, že přiřazení $V_i=x$ a $V_j=y$ splní všechny binární podmínky pro $V_i,V_j$
		- může platit, že $(V_i,V_j)$ je hranově konzistentní, ale $(V_j,V_i)$ není
	- CSP je hranově konzistentní $\equiv$ každá hrana je hranově konzistentní (v obou směrech)
	- algoritmus AC-3
		- začínám se všemi hranami (podmínkami) ve frontě
		- postupně beru hrany z fronty a pro každou odstraním nekonzistentní prvky z domény
		- pokud jsem odstranil nějaké prvky z domény, musím zopakovat kontrolu pro hrany směřující do dané proměnné (kromě hrany opačné k té aktuálně zpracované)
		- složitost $O(cd^3)$, kde $c$ je počet podmínek, $d$ je velikost domény
			- $O(d^2)$ … kontrola konzistence
			- každá podmínka se ve frontě může objevit nejvýše $d$-krát, protože se z dané domény dá odstranit nejvýše $d$ prvků
		- optimální algoritmus má složitost $O(cd^2)$
	- hranová konzistence je typ lokální konzistence, negarantuje globální konzistenci
	- arc consistency (AC) vs. forward checking (FC)
		- FC je jednodušší (a rychlejší) než AC, slouží ke stejnému účelu – zrychlení prohledávání
		- FC na základě přiřazení do proměnné (v daném kroku prohledávání) pročistí domény dosud nepřiřazených proměnných
		- AC k tomu navíc zajišťuje vzájemnou kompatibilitu domén nepřiřazených proměnných
- algoritmus hledání řešení (MAC)
	- chceme zkombinovat AC a backtracking
	- problém uděláme hranově konzistentní
	- po každém přiřazení obnovíme hranovou konzistenci
	- této technice se říká *look ahead* nebo *constraint propagation* nebo *udržování hranové konzistence* (MAC, maintaining arc consistency)
	- kontroly FC/AC jsou v polynomiálním čase, kdežto strom stavů se větví exponenciálně

## Logické uvažování

- základy výrokové logiky (konjunktivní a disjunktivní normální forma)
	- viz [Společná matematika](spolecna-matematika.md)
	- výrokovou logiku lze použít k logickému odvozování znalostí na základě znalostní báze
- algoritmus DPLL
	- literál $\ell$ má čistý výskyt ve $\varphi$, pokud se $\ell$ vyskytuje ve $\varphi$ a opačný literál $\overline\ell$ se ve $\varphi$ nevyskytuje
		- takový literál můžu nastavit na 1
		- to neovlivní splnitelnost výroku, ale zmenší to množinu modelů, které jsem schopen nalézt
	- algoritmus
		- dokud $\varphi$ obsahuje jednotkovou klauzuli $\ell$, ohodnoť $\ell=1$ a proveď jednotkovou propagaci
			- každou klauzuli obsahující $\ell$ odstraníme (protože je takto splněna)
			- $\overline\ell$ odstraníme ze všech klauzulí, které ho obsahují (protože $\overline\ell$ nemůže zajistit splnění dané klauzule)
		- dokud existuje literál $\ell$, který má ve $\varphi$ čistý výskyt, ohodnoť $\ell=1$ a odstraň klauzule obsahující $\ell$
		- pokud $\varphi$ neobsahuje žádnou klauzuli, je splnitelný
		- pokud $\varphi$ obsahuje prázdnou klauzuli, není splnitelný
		- jinak zvol dosud neohodnocenou výrokovou proměnnou $p$ a zavolej algoritmus rekurzivně na $\varphi\land p$ a na $\varphi\land\neg p$
	- algoritmus běží v exponenciálním čase
	- praktické poznámky
		- čistý výskyt se zas tak moc nepoužívá
		- jednotková propagace
			- hledám klauzule o jedné proměnné
			- je v zásadě ekvivalentní hranové konzistenci
		- ke zkoušení hodnot proměnných se používá tree search
- dopředné a zpětné řetězení (Hornovské klauzule)
	- mám dotaz $\alpha$, ten vyjádřím jako výrokovou formuli
		- znalostní bázi $KB$ vyjádřím jako teorii
		- zajímá mě, zda $KB\models\alpha$ (to platí, právě když $KB\land\neg\alpha$ je nesplnitelné)
	- řetězení můžeme použít, pokud znalostní báze obsahuje pouze Hornovy klauzule
		- Hornova klauzule = disjunkce literálů, z nichž nejvýše jeden je pozitivní
		- Hornovu klauzuli $\neg p\lor\neg q\lor\neg r\lor s$ lze zapsat jako implikaci $p\land q\land r\implies s$
	- forward chaining … data-driven reasoning
		- $p\land q\land r\implies s$
		- pokud vím, že platí $p$, pak převedu na $q\land r\implies s$
		- jakmile se počet předpokladů sníží na 0, vím, že $s$ platí
		- je to v podstatě speciální případ použití rezolučního pravidla
			- rezolvuju to, co vím, s libovolnou klauzulí
		- algoritmus
			- každá proměnná má počítadlo proměnných, které na ni ukazují
			- postupně beru pravdivé proměnné, snižuju počítadla u proměnných, na které ukazují
			- jakmile u proměnné klesne počítadlo na nulu, zařadím mezi pravdivé proměnné
	- backward chaining … goal-driven reasoning
		- něco mě zajímá – pokouším se to odvodit
			- najdu klauzule, kde je nějaký literál z $\alpha$ na pravé straně implikace
			- tak dostanu další literály, které musím dokázat
			- postupuju tak dlouho, dokud se nedostanu k faktům (literálům, o nichž vím, že platí)
		- tohle se používá v Prologu
		- opět vlastně používám rezoluční pravidlo
			- to, co chci zjistit, rezolvuju s libovolnou klauzulí
	- forward chaining prochází spoustu klauzulí, které nás nezajímají – backward chaining může mít výrazně menší složitost
- rezoluce
	- mám dotaz $\alpha$, ten vyjádřím jako výrokovou formuli
		- znalostní bázi $KB$ vyjádřím jako teorii
		- zajímá mě, zda $KB\models\alpha$ (to platí, právě když $KB\land\neg\alpha$ je nesplnitelné)
	- $KB\land\neg\alpha$ převedeme do CNF → dostaneme množinu klauzulí (formuli $S$)
	- použijeme rezoluci (zkonstruujeme rezoluční zamítnutí formule $S$)
		- použitím rezolučního pravidla z klauzulí $\varphi\lor p$ a $\psi\lor\neg p$ dostaneme $\varphi\lor\psi$
		- zkoušíme spolu rezolvovat postupně všechny dvojice klauzulí
		- pokud v průběhu dostaneme prázdnou klauzuli, máme rezoluční důkaz $\alpha$ z $KB$
		- pokud se dostaneme do stavu, kdy nelze použít rezoluční pravidlo na žádnou dvojici klauzulí, tak víme, že neplatí $KB\models\alpha$

## Pravděpodobnostní uvažování

- základy teorie pravděpodobnosti (úplná sdružená distribuce, nezávislost, Bayesovo pravidlo)
	- viz [Společná matematika](spolecna-matematika.md)
	- pravděpodobnostní uvažování umožňuje agentovi zacházet s nejistotou
	- zdroji nejistoty jsou částečná pozorovatelnost (nelze snadno zjistit současný stav) a nedeterminismus (není jisté, jak akce dopadne)
	- agent si pamatuje belief state – pravděpodobnostní distribuce přes všechny možné stavy světa, v nichž se agent může nacházet
- pravděpodobnostní uvažování (vysčítání, normalizace)
	- někdy si můžeme udělat tabulku všech možností a určit jejich pravděpodobnosti (full joint probability distribution)
		- odpověď lze vyjádřit z ní (této metodě se říká enumeration, výčet) – ale u velkých tabulek je někdy potřeba posčítat příliš mnoho hodnot
	- $P(Y)=\sum_z P(Y\mid z)\cdot P(z)$
	- $P(Y\mid e)=\frac{P(Y\land e)}{P(e)}$
		- typicky nemusíme znát $P(e)$, stačí použít $\alpha P(Y\land e)$, kde $\alpha$ je normalizační konstanta
	- velkou tabulku můžeme někdy reprezentovat menším způsobem – pokud jsou proměnné podmíněně nezávislé
	- Bayesovo pravidlo … $P(Y\mid X)=\frac{P(X\mid Y)P(Y)}{P(X)}=\alpha P(X\mid Y) P(Y)$
		- lze odvodit z definice podmíněné pravděpodobnosti
		- pomůže nám při přechodu z příčinného k diagnostickému směru
			- $P(\mathrm{effect} \mid \mathrm{cause})$ … casual direction (příčinný směr), obvykle známý
			- $P(\mathrm{cause} \mid \mathrm{effect})$ … diagnostic direction (diagnostický směr), obvykle chceme zjistit
			- známe důsledky; chceme zjistit, jaké příčiny k nim mohly vést
	- naivní bayesovský model
		- $P(\text{Cause}, \text{Effect}_1, \dots, \text{Effect}_n) = P(\text{Cause})\prod_iP(\text{Effect}_i\mid\text{Cause})$
		- předpokládáme nezávislost důsledků
	- chain rule
		- $P(x_1,\dots,x_n)=\prod_iP(x_i\mid x_{i-1},\dots,x_1)$
		- využívá product rule (lze odvodit z definice podmíněné pravděpodobnosti)
- Bayesovské sítě: konstrukce a vztah k úplné sdružené distribuci
	- TODO
- Bayesovské sítě: exaktní odvozování (enumerace, eliminace proměnných)
	- TODO
- Bayesovské sítě: aproximační odvozování (Monte Carlo, zamítání, vážení věrohodností)
	- TODO

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
