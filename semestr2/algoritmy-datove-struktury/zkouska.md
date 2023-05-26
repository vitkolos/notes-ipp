# Zkouška

## Definice algoritmu

- Definice: Výpočetní model RAM
	- není náhodný, ale po paměti umí skákat libovolně
	- počítá s celými čísly (vše ostatní můžeme reprezentovat čísly)
	- paměť = pole indexované čísly (záporné buňky obvykle slouží pro pracovní data, nezáporné pro vstup a výstup)
	- výpočet: v paměti dostaneme vstup, provádíme instrukce (dokud nenastane halt), v paměti odevzdáme výstup (zbytek paměti může obsahovat cokoliv – před spuštěním výpočtu i po jeho konci)
	- definujeme základní aritmetické, logické a řídicí instrukce
		- operandem může být `literál`, `[adresa]`, `[[nepřímá adresace]]`
		- uložení: `kam ← co`
		- operace: `kam ← a OP b`, kde OP může být `+-*/&|^«»`
		- `halt` (za programem implicitní)
		- `goto KAM`
			- návěští lze umístit před libovolný řádek
		- `if a REL b goto KAM`
			- místo goto by tam mohl být i jiný příkaz kromě if
			- REL může být `=, <>, <, >, <=, >=`
	- doba běhu programu je rovna celkovému počtu provedených instrukcí
	- spotřebovanou paměť definujeme jako rozdíl mezi nejvyšším a nejnižším použitým indexem paměti
	- časová a paměťová složitost pak odpovídá maximu ze spotřeby času a paměti přes všechny vstupy dané velikosti
	- do časové složitosti nepočítáme načtení vstupu
	- podobně do prostorové složitosti nepočítáme vstup, do nějž se nezapisuje, ani výstup, pokud se jenom zapíše a pak už se nečte (takhle se někdy definuje pracovní prostor výpočtu)
	- je potřeba omezit kapacitu paměťové buňky
		- jednotková cena instrukce – omezíme šířku slova na W bitů
		- logaritmická cena instrukce – cena odpovídá počtu bitů operandů včetně adres (je přesný, ale nepohodlný na přemýšlení o algoritmech)
		- relativní logaritmická cena instrukce – u polynomiálně velkých čísel je cena jednotková, u obrovských čísel se cena zvyšuje (tohle budeme reálně používat – i když se k tomu budeme obvykle chovat jako k jednotkové ceně instrukce)
- Definice: Čas a prostor konkrétního výpočtu, časová a prostorová složitost
	- pro různé úlohy používáme různé parametrizace vstupu (tedy velikost vstupu může být trochu něco jiného – někdy počet čísel, někdy jejich hodnota…)
	- doba běhu pro vstup x
		- $t(x):=$ součet cen provedených instrukcí (může být $\infty$)
	- časová složitost výpočtu
		- $T(n):= \text{max}\lbrace t(x)\mid x \text{ vstup velikosti }n\rbrace$
	- prostor běhu pro vstup x
		- $s(x):=$ max. adresa – min. adresa + 1
		- máme na mysli maximální a minimální adresy navštívené během výpočtu
	- prostorová složitost výpočtu
		- $S(n):= \text{max}\lbrace s(x)\mid x \text{ vstup velikosti }n\rbrace$
	- takhle jsme definovali složitosti v nejhorším případě, někdy se může hodit i průměrný případ
- Definice: Asymptotická notace: O, Ω, Θ
	- $f\in O(g)\equiv\exists c\,\forall^*n\;f(n)\leq c\cdot g(n)$
		- $f,g:\mathbb N\to\mathbb R$
		- $\forall^*n$ … pro všechna $n$ až na konečně mnoho výjimek (existuje $n_0$ takové, že pro všechna větší $n$ už to platí)
	- $f\in \Omega(g)\equiv\exists c\,\forall^*n\;f(n)\geq c\cdot g(n)$
	- $\Theta(g):= O(g)\cap \Omega(g)$

## Základní grafové algoritmy

- Algoritmus: Prohledávání do šířky (BFS)
	- zpracování určitého vrcholu = odeberu ho z fronty, podívám se na sousední vrcholy a pokud jsou nenavštívené, tak je označím jako otevřené a přidám je do fronty ke zpracování, zpracovávaný vrchol zavřu
	- algoritmus začíná přidáním prvního vrcholu do fronty (to je ten vrchol, ze kterého graf prohledáváme)
	- algoritmus končí, jakmile je fronta prázdná
	- složitost $\Theta(n+m)$
	- klasifikace hran – rozdělíme vrcholy na vrstvy (podle toho, jak je BFS prochází ve vlnách)
		- stromová hrana – prošli jsme po ní při BFS
		- příčná hrana – v rámci vrstvy
		- zpětná hrana – do předchozí vrstvy nebo i o několik vrstev dozadu
		- „dopředně příčná“ hrana – do následující vrstvy
		- neexistuje hrana, která by vedla o víc než jednu vrstvu dopředu
- Algoritmus: Prohledávání do hloubky (DFS)
	- lze implementovat rekurzí nebo jako BFS se zásobníkem místo fronty
	- na začátku jsou všechny vrcholy neviděné
	- DFS(v):
		- stav(v) ← otevřený
		- pro vw $\in E$
			- pokud stav(w) = neviděný
				- DFS(w)
		- stav(v) ← zavřený
	- DFS spouštíme z nějaké vrcholu – navštívíme všechny vrcholy z něj dosažitelné
	- opakované DFS – algoritmus nespouštíme pouze pro jeden určitý vrchol, ale pro všechny (neviděné) vrcholy grafu → projdeme všechny komponenty souvislosti
		- stejného efektu lze docílit přidáním jednoho superzdroje, který bude připojen ke všem vrcholům grafu
	- složitost $\Theta(n+m)$
- Definice: Klasifikace hran v DFS
	- v orientovaném grafu
		- stromová hrana – hrana, po které jsme při DFS prošli
		- zpětná hrana – vede do předka (do otevřeného vrcholu)
		- dopředná hrana – vede do potomka (do uzavřeného vrcholu)
		- příčná hrana – vede do uzavřeného vrcholu v jiné větvi (není ani předkem, ani potomkem)
		- hrana nemůže být příčná v opačném směru – taková hrana je stromová
	- v neorientovaném grafu – každou hranu vidíme dvakrát
		- poprvé stromová, podruhé zpětná
		- poprvé zpětná, podruhé dopředná
		- hrana nemůže být poprvé dopředná, protože taková hrana je stromová
		- hrana nemůže být poprvé příčná, protože podruhé by byla příčná v opačném směru, což nejde
		- pokud ignorujeme druhé návštěvy, tak existují jenom stromové a zpětné hrany
	- klasifikaci lze určit i na základě uzávorkování průchodu vrcholy, když při otevření vrcholu $v_i$ napíšeme $(_i$ a při jeho uzavření $)_i$
	- místo uzávorkování lze rovněž použít „hodiny“ a každému vrcholu nastavit čas otevření (in) a čas uzavření (out)
- Algoritmus: Hledání mostů v neorientovaných grafech
	- Df: $e\in E(G)$ je most $\equiv G-e$ má více komponent než $G$
		- $e$ není most $\iff e$ leží na kružnici
	- zpětná hrana není nikdy most (leží na kružnici), tedy stačí poznat, zda stromová hrana leží na kružnici
	- stromová hrana $xy$ není most $\iff\exists$ zpětná hrana $ab$, kde $a$ leží v $T(y)$ (podstromu $y$) a $b$ v něm neleží
	- Df: $\text{low}(v):=\text{min}\lbrace \text{in}(b)\mid ab$ je zpětná hrana s $a\in T(v)\rbrace$
	- `low` pro $v$ je minimum z `low` synů $v$ a `in` zpětných hran z $v$ (respektive `in` vrcholu, do nějž zpětná hrana z $v$ vede)
	- stromová hrana $xy$ není most $\iff\text{low}(y)\lt y$
	- stačí nám upravené DFS, běží v čase $\Theta(n+m)$

## Algoritmy pro orientované grafy

- Algoritmus: Detekce cyklů pomocí DFS
	- lemma: na každém cyklu leží alespoň jedna zpětná hrana
		- mějme cyklus, na něm vrchol s minimálním `out`em
		- tedy další vrchol na cyklu bude mít větší `out`
		- tím získáváme hranu, na níž roste `out` – to platí pouze pro zpětné hrany
	- opačná implikace je jednoduchá (zpětná hrana nutně tvoří cyklus)
	- tedy stačí pustit opakované DFS a hledat zpětné hrany
	- věta: graf je DAG $\iff$ opakované DFS nenajde zpětnou hranu
- Definice: Acyklický orientovaný graf (DAG), zdroj, stok
	- DAG je orientovaný graf bez cyklů :)
	- zdroj je vrchol s $\text{deg}^{\text{in}}(v)=0$
	- stok je vrchol s $\text{deg}^{\text{out}}(v)=0$
	- lemma: každý DAG má alespoň jeden zdroj a stok
	- pro DAG $G$ je $G^T$ graf vzniklý otočením šipek u $G$, je taky DAG (protože transpozice cyklu je cyklus), dojde k prohození zdrojů a stoků
- Definice: Topologické uspořádání DAGu
	- topologické uspořádání grafu $G=(V,E)$ je lineární uspořádání $\leq$ na $V$ takové, že $\forall uv\in E: u\leq v$
	- může jich být víc
- Algoritmus: Konstrukce topologického uspořádání
	- postupným odtrháváním zdrojů (vezmeme libovolný vrchol, jdeme proti šipkám do zdroje, tento zdroj umístíme do uspořádání a odtrhneme ho z grafu) – to je ale složité na efektivní implementaci
	- opakované DFS opouští vrcholy v pořadí opačném topologickému uspořádání (důkaz přes klesající `out` na hraně a nepřítomnost zpětných hran)
- Příklad: Princip indukce podle topologického uspořádání
	- mějme topologické uspořádání $v_1,\dots,v_n$
	- počítáme počet cest z vrcholu $v_i$ do všech vrcholů grafu
	- pro $j\lt i:c(v_j)=0$
	- $c(v_i)=1$
	- pro $j\gt i$ induktivně $c(v_j)=\sum c(p)$, kde $p$ jsou vrcholy, z nichž vede hrana do $v_j$
- Algoritmus: Počet cest mezi dvěma vrcholy v DAGu
	- indukcí přes topologické uspořádání, v čase $\Theta(n+m)$
- Definice: Silná souvislost, její komponenty, graf komponent
	- buď $\leftrightarrow$ binární relace na vrcholech grafu definovaná tak, že $x\leftrightarrow y$, právě když existuje orientovaná cesta jak z $x$ do $y$, tak z $y$ do $x$
	- relace $\leftrightarrow$ je ekvivalence, ekvivalenční třídy indukují podgrafy = komponenty silné souvislosti
	- graf je silně souvislý, má-li jednu komponentu (tedy pro každé dva vrcholy existuje cesta tam i zpět)
	- graf komponent $\mathcal C(G)$ má za vrcholy komponenty silné souvislosti grafu $G$, hrany mezi vrcholy vedou právě tehdy, když mezi danými komponentami vedou hrany v původním grafu
	- lemma: graf komponent je DAG (kdyby existoval cyklus, tak by se takto provázané komponenty slily do jedné)
- Algoritmus: Rozklad grafu na komponenty silné souvislosti
	- opakované DFS v $G^T$, při opouštění vrcholu ho dáme na zásobník
	- beru vrcholy ze zásobníku a pro vrcholy bez přiřazené komponenty provádím DFS
		- kdykoliv narazím na vrchol bez přiřazené komponenty, nastavím mu komponentu na „aktuální vrchol“ (to je ten vrchol, který jsem vzal ze zásobníku) a zanořím se (spustím rekurzivně DFS)

## Nejkratší cesty

- Definice: Vzdálenost v grafu
- Věta: Trojúhelníková nerovnost pro vzdálenost
- Algoritmus: Dijkstrův algoritmus
- Příklad: Implementace Dijkstrova algoritmu pomocí haldy
- Algoritmus: Obecný relaxační algoritmus
- Algoritmus: Bellmanův-Fordův algoritmus

## Minimální kostry

- Algoritmus: Jarníkův algoritmus
- Věta: Lemma o řezech
- Věta: Jednoznačnost minimální kostry
- Algoritmus: Borůvkův algoritmus
- Algoritmus: Kruskalův algoritmus
- Algoritmus: Union-Find

## Vyhledávací stromy

- Definice: Rozhraní slovníku, množiny a jejich uspořádaných verzí
- Definice: Binární vyhledávací strom (BVS)
- Algoritmus: Operace Find, Insert a Delete v BVS
- Definice: Dokonale vyvážený strom
- Definice: AVL strom
- Věta: Odhad hloubky AVL stromu
- Definice: Rotace hrany stromu
- Algoritmus: Operace Insert a Delete v AVL stromech

## (a,b)-stromy

- Definice: Vícecestný vyhledávací strom a (a,b)-strom
- Věta: Odhad hloubky (a,b)-stromu
- Algoritmus: Operace Insert a Delete v (a,b)-stromech
- Příklad: Volba parametrů (a,b)-stromu

## Písmenkové stromy (trie)

- Definice: Definice trie
- Algoritmus: Operace Find, Insert a Delete v trii
- Příklad: Použití trie k reprezentaci čísel

## Hešování

- Definice: Hešování s řetězci v přihrádkach
- Algoritmus: Operace Find, Insert a Delete v hešování s řetězci
- Algoritmus: Dynamické rozšiřování tabulky
- Definice: c-univerzální systém funkcí
- Věta: Konstrukce 1-univerzálního systému pomocí skalárního součinu
- Věta: Průměrná složitost operací při náhodné volbě hešovací funkce z c-univerzálního systému

## Rozděl a panuj

- Algoritmus: Třídění sléváním (Mergesort)
- Algoritmus: Násobení n-ciferných čísel v čase O(nlog23)
- Věta: Kuchařková věta (Master theorem)
- Algoritmus: Strassenův algoritmus na násobení matic (vzorce nezkouším)

## Třídění a vyhledávání

- Algoritmus: Quickselect – hledání k-tého nejmenšího prvku
- Věta: Průměrná časová složitost Quickselectu při náhodné volbě pivota
- Algoritmus: k-tý nejmenší prvek v lineárním čase (algoritmus s pěticemi)
- Algoritmus: Quicksort
- Věta: Průměrná časová složitost Quicksortu při náhodné volbě pivota

## Dynamické programování

- Algoritmus: Nejdelší rostoucí podposloupnost
- Algoritmus: Editační vzdálenost řetězců
- Algoritmus: Konstrukce optimálního BVS
- Algoritmus: Floydův-Warshallův algoritmus na výpočet vzdáleností v grafu
- Příklad: Princip dynamického programování
- Příklad: Grafová interpretace dynamického programování
