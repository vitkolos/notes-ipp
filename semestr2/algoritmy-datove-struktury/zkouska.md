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
- Algoritmus: Prohledávání do hloubky (DFS)
	- lze implementovat rekurzí nebo jako BFS se zásobníkem místo fronty
	- na začátku jsou všechny vrcholy neviděné
	- DFS(v):
		- stav(v) ← otevřený
		- pro vw $\in E$
			- pokud stav(w) = neviděný
				- DFS(w)
		- stav(v) ← zavřený
	- opakované DFS – algoritmus nespouštíme pouze pro jeden určitý vrchol, ale pro všechny (neviděné) vrcholy grafu → projdeme všechny komponenty souvislosti
		- stejného efektu lze docílit přidáním jednoho supervrcholu, který bude připojen ke všem vrcholům grafu
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
	- `low` pro $v$ je minimum z `low` synů $v$ a `in` zpětných hran z $v$
	- stromová hrana $xy$ není most $\iff\text{low}(y)\lt y$
	- běží v čase $\Theta(n+m)$

## Algoritmy pro orientované grafy

- Algoritmus: Detekce cyklů pomocí DFS
- Definice: Acyklický orientovaný graf (DAG), zdroj, stok
- Definice: Topologické uspořádání DAGu
- Algoritmus: Konstrukce topologického uspořádání
- Příklad: Princip indukce podle topologického uspořádání
- Algoritmus: Počet cest mezi dvěma vrcholy v DAGu
- Definice: Silná souvislost, její komponenty, graf komponent
- Algoritmus: Rozklad grafu na komponenty silné souvislosti

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
