# Algoritmizace: přednášky

- https://ksvi.mff.cuni.cz/~topfer/
- prezentaci budeme mít k dispozici online, často bude rozšířená oproti přednášce, budou tam ukázkové programy
- [kurz v Moodlu](https://dl1.cuni.cz/course/view.php?id=8186#section-3)
- zkouška
	- společné pořadavky a zkušební termíny pro obě paralelky
	- přihlašování přes SIS
	- je nutné mít zápočet
	- povinná písemná část, nepovinná ústní
- materiály
	- Pavel Töpfer: Algoritmy a programovací techniky
	- programátorské kuchařky KSP
	- https://pruvodce.ucw.cz
	- https://www.algovision.org

## Algoritmus

- Konečná posloupnost elementárních příkazů, jejichž provádění umožňuje pro každá přípustná vstupní data mechanickým způsobem získat po konečném počtu kroků příslušná výstupní data.
- vlastnosti algoritmu – konečnost, hromadnost, resultativnost, jednoznačnost, determinismus (nebude na zkoušce :)
	- determinismus – po provedení každého kroku je jednoznačně určeno, který krok se bude provádět dále
- formální modely algoritmu – rekurzivní funkce, Turingův stroj, lambda kalkul, RAM počítač
- popis a zápis algoritmu – slovní popis v přirozeném jazyce, pseudokód, program (zjednodušená konstrukce programovacího jazyka)
- největší společný dělitel
- správnost Eukleidova algoritmu
	1. konečnost = výpočet pro jakákoliv vstupní data skončí
		- na začátku výpočtu i stále v jeho průběhu je x > 0, y > 0
		- v každém kroku výpočtu se hodnota x+y sníží alespoň o 1 -> nejpozději po x+y krocích výpočet skončí, je tedy konečný
	2. parciální správnost
- problém stabilních manželství
- složitost – časová a prostorová

### Efektivita algoritmu

- efektivita algoritmu – funkce velikosti vstupních dat
	- přesné vyjádření časové složitosti je obtížné a zbytečné, podstatná je řádová rychlost růstu této funkce pro rostoucí N
	- zanedbáním pomaleji rostoucích členů a konstant získáme **asymptotickou časovou složitost**, např. $O(N^2)$
		- symbol "velké O"
		- $f\in O(g)$
			- funkce f se dá shora odhadnout funkcí g (až na multiplikativní konstantu a pro dostatečně velká n)
			- $f,g: \mathbb{N}→\mathbb{R}^+$
			- $f\in O(g) \iff \exists c > 0\ \exists n_0\ \forall n>n_0: 0\leq f(n) \leq c \cdot g(n)$
		- jde o odhad shora
	- opačný odhad zdola $f \in \Omega(g)$
	- přesný odhad $f \in \Theta(g)$
		- $f \in \Theta(g) \iff f \in O(g)\land f \in \Omega(g)$
- asymptotická časová složitost
	- typické třídy asymptotické časové složitosti algoritmů $\Theta(1), \Theta(\log{N}), \Theta(n), \Theta(N \cdot \log{N}), \Theta(N^2), \Theta(N^3), \dots, \Theta(2^N), \Theta(N!)$
	- problém batohu
	- někdy se používá f = O(g), což není formálně zcela správné, protože O(g) je třída funkcí
- složitost algoritmu v různých případech – v nejlepším (prakticky se nepoužívá), nejhorším (používá se nejčastěji) a průměrném (je obtížné odvodit tuto složitost)
	- algoritmus problému stabilních manželství – v nejhorším případě $\Theta(n)$, v nejlepším případě $\Theta(n^2)$
- složitost problému – složitost nejlepšího algoritmu (z hlediska časové složitosti), kterým lze řešit daný problém; odvození bývá často obtížné, pro řadu problémů neznáme
	- složitost problému vnitřního třídění – $O(n \cdot \log{n})$
- rozklad čísla na cifry
- test prvočíselnosti
	- zkouším všechny dělitele od 2 do $N-1 → O(N)$
	- zkouším všechny dělitele od 2 do $N/2 → O(N)$
	- zkouším všechny dělitele od 2 do $\sqrt{N} → O(\sqrt{N}) = O(N^\frac{1}{2})$ – asymptoticky lepší
		- nepoužíváme odmocninu, ale druhou mocninu (násobení)
	- přestanu při nalezení prvního dělitele – také $O(\sqrt{N})$
	- stačí zkusit číslo 2 a pak jen liché dělitele lichých čísel
- hledání všech prvočísel od 2 do N
	- pomalý způsob $O(N^\frac{3}{2})$ – pro každé číslo zkouším, jestli je prvočíslo (viz výše)
	- Eratosthenovo síto – vyškrtáváme násobky prvočísel
		- složitost $O(N\cdot \log{\log{N}})$

## Dlouá čísla

- Python to umí sám
- číslo uložíme po cifrách – seznam cifer (uložíme jako pole čísel)
- operace po cifrách jako na základní škole
- lze ukládat cifry po trojicích apod.
- desetinné číslo – evidujeme polohu desetinné čárky

## Vyhodnocení polynomu v bodě

- úloha: vyhodnocení polynomu v bodě x (dosazení konkrétního x do polynomu)
	- přímý výpočet podle uvedeného předpisu – kvadratická složitost (cca n^2 násobení, n sčítání)
	- Hornerovo schéma – n násobení, n sčítání → lineární složitost
		- příklad použití algoritmu – vstup čísla po znacích, konverze číselného stringu na integer
- operace s polynomy
	- nejdříve polynom uložíme do pole – index v poli odpovídá mocnině (první prvek v poli je absolutní člen)

## Řadicí algoritmy

- třídění sléváním (merge sort)
	- časová složitost $\Theta(n \log_2 n)$
		- počet porovnání v každé hladině – n
		- počet hladin – log n
	- prostorová složitost – potřebuju další pole délky $n$
- k dokázání přesného odhadu složitosti lze dokázat, že to jde udělat s danou složitostí a že to nejde lépe
- problém třídění n dat – musíme udělat $\log_2 n!$ porovnání
	- https://www.itnetwork.cz/algoritmy/razeni/dolni-odhad-casove-slozitosti-problemu-trideni
	- $\log n! = n \log n$
		- Stirlingova formule
		- $(\frac{n}{2})^\frac{n}{2} < n! < n^n$ (logaritmujeme)
- třídění počítáním (counting sort)
	- O(n + R)
		- R … rozsah hodnot
- přihrádkové třídění (bucket sort)
	- pythonovský i klasický způsob
	- u klasického způsobu mám v poli uložené indexy, kam umístit prvek s danou hodnotou
	- je stabilní – zachovává pořadí prvků se stejnou hodnotou klíče
- víceprůchodové přihrádkové třídění (radix sort)
	- u velkého R (rozsahu hodnot)
	- rozdělíme klíč na části – nejprve třídíme podle dolní (méně významné) části klíče, poté podle horní (významnější) části
	- díky stabilitě třídění se zachová uspořádání z předchozích fází třídění
- merge sort funguje při zapisování do souboru
- u merge sortu má smysl slučovat tři nebo čtyři úseky
- použitím vnitřního třídění k prvotnímu roztřídění pole snížím počet vstupně výstupních operací
- tim sort – kombinuje insertion sort a merge sort (merge sort se používá až na větší úseky)

## Ukládání dat

- int – ve dvojkové soustavě
- 32bit nebo 64bit

### Datové struktury

- seznam vs. pole
	- rychlejší je práce s polem, seznamy mají více možností (i když často zbytečných)
	- pole v Pythonu – knihovny array, numpy
	- operace na seznamu
		- úpravy středu seznamu – lineární složitost
		- úpravy konce – lineární (pokud chybí paměť), ale průměrně konstantní časová složitost
	- pokud na konci seznamu chybí paměť, tak není možné provést append – Python tedy seznam přesune jinam (realokuje), přidá mu víc místa (aby se tam vešlo ještě x dalších prvků)
	- realokace s přidělením dvojnásobku paměti
		- takhle to Python nedělá, ale je to názorné
		- pro 1000 appendů 9 realokací
		- amortizovaná složitost konstantní
- spojové seznamy – poměrně pracné pro programátora, někdy fungují rychleji, v Pythonu se implementuje ručně (v programu mám uložený odkaz na první prvek seznamu, ten odkazuje na další prvek atd., na konci je uzemnění – v Pythonu None)
- abstraktní datové typy
	- zásobník (stack)
		- řada dat, na jedné straně dno, na druhé vrchol
		- data se přidávají na vrchol a odebírají se také jediné z vrcholu
		- v Pythonu lze implementovat na seznamu nebo na spojovém seznamu
	- fronta (queue)
		- z jedné strany se prvky přidávají, z druhé odebírají
		- jak řešit odebírání prvků z paměti
			- při odebrání posouvám prvky – lineární složitost
			- při odebrání většího množství prvků posouvám prkvy
			- posouvám až ve chvíli, kdy nemám volné místo
			- kruhová fronta – při přetečení se přidává na začátek paměti (v programu ukládám začátek a konec fronty, ty modulím kapacitou)
		- deque – knihovní implementace fronty (double-ended queue), umožňuje přidávat i odebírat zprava i zleva
		- při implementaci fronty pomocí spojového seznamu je na konci seznamu příchod, na začátku odchod, ukládám dvojici odkazů (na první a poslední prvek)
	- halda (heap)
		- nepamatuje si pořadí příchodu prvků
		- prvky musí být porovnatelné (definováno vzájemné uspořádání)
		- odebírá se nejmenší prvek
		- typické operace – přidat prvek, určit hodnotu minimálního prvku, odebrat minimální prvek
		- požadujeme časovou složitost všech operací $O(\log N)$
		- haldu si představujeme jako binární strom, který ovšem typicky implementujeme v poli (pokud nultý prvek pole necháme prázdný, tak bude počítání indexů trochu jednodušší)
		- pro každý uzel musí platit, že jeho hodnota je menší (nebo rovna) než hodnota obou synů
		- výška binárního stromu
			- pro nevyvážený (degenerovaný) strom – až $n$
			- pro vyvážený strom – $\log_2 n$
			- průměrně $2\log_{2} n$
		- výška haldy = horní celá část z $\log_2 N$
		- při přidávání prvku přidáváme na konec a bubláme nahoru
		- při odebírání prvku odebereme nejmenší (ze začátku), poslední přesuneme místo něj a bubláme dolů (prohazujeme s menším ze synů)
		- haldování v lineárním čase
			- vytvářím malé haldy na konci seznamu, postupuju nahoru a probublávám prvky směrem dolů
			- idea spočívá v tom, že u původního postupu má před sebou hodně prvků dlouhou bublací cestu (halduje se shora), zatímco u tohoto rychlého postupu má před sebou málo prvků dlouhou bublací cestu (halduje se zespoda)
	- prioritní fronta
		- prvky se předbíhají podle priority
		- typická je implementace pomocí haldy
		- pokud záleží na pořadí prvků téže priority, řeší se pomocí front uvnitř haldy
	- slovník
		- dvojice klíč – hodnota
		- operace: vyhledej, vlož, vymaž
		- někdy se označuje jako asociativní pole nebo mapa
		- typicky implementace pomocí hešování
		- časová složitost přístupu k prvku je v průměru konstantní, ale v nejhorším případě lineární vzhledem k počtu prvků

## Rekurze

- objekt je definován pomocí sebe sama
- rekurzivní algoritmus
- rekurzivní volání funkce
- implementace rekurzivního algoritmu bez použití rekurzivní funkce může být výhodnější
- ukončení rekurze
	- v Pythonu maximální povolená hloubka rekurze 1012
	- v jiných jazycích může nastat chyba stack overflow (přetečení zásobníku volání funkcí)
- Fibonacciho posloupnost
	- řešení pomocí čisté rekurze je neefektivní (exponenciální složitost)
	- chytrá rekurze
		- kešování hodnot, memoizace – mezivýsledky ukládám do pole
		- dynamické programování – jdu zespodu
- doplnění znamének
	- rekurzivně generujeme binární strom
	- ořezávání stromu se může vyplatit – u téhle konkrétní úlohy nelze (jednoduše) určit algoritmus ořezávání
- rozklad čísla na součet kladných celých sčítanců
	- vybereme z nich ty nerostoucí, abychom tam neměli několik permutací jednoho rozkladu
	- není to binární strom, ale je prořezaný, jak se dá

## Binární stromy

- hodí se nám „spojákové“ ukládání (tedy pomocí pointerů v objektu)
- „haldové“ ukládání v poli je neefektivní, protože nám můžou vznikat prázdná místa
- průchod do hloubky
	- v každém vrcholu provedeme zvolenou akci
	- varianty průchodu
		- preorder – nejprve zpracuje vrchol, pak jde postupně do obou jeho podstromů
		- inorder – nejprve jde do levého podstromu, pak zpracuje vrchol, nakonec jde do pravého podstromu
		- postorder – nejprve jde postupně do obou podstromů vrcholu, pak zpracuje vrchol samotný
	- lze procházet bez rekurze pomocí zásobníku
- průchod do šířky
	- stačí použít algoritmus se zásobníkem a místo zásobníku v něm použít frontu
	- složitost (viz prezentace)
	- binární strom bude u zkoušky
- binární vyhledávací strom
	- datová struktura pro ukládání a vyhledávání dat podle klíče
	- pro každý vrchol platí
		- všechny záznamy uložené v levém podstromu mají menší klíč
		- všechny záznamy uložené v pravém podstromu mají větší klíč
	- musí platit pro všechny záznamy v podstromu – nestačí bezprostředně mezi uzly
	- časová složitost algoritmu vyhledávání je v nejhorším případě určena výškou stromu (u degenerovaného stromu až N)
	- v průměrném případě výška O(log N)
	- vyvažování stromu – je algoritmicky náročné
	- přidávání hodnoty – algoritmem vyhledávání dojdu k odkazu None a tam hodnotu přidám
	- odebrání hodnoty
		- pokud nemá syny – triviální
		- pokud má jednoho syna – triviální
		- pokud má dva syny – najdu maximum v levém podstromu nebo minimum v pravém podstromu
			- tohle maximum/minimum má nejvýše jednoho syna, takže ho umíme smazat
	- existuje binární vyhledávací strom se zarážkou
		- používali jsme seznam se zarážkou – hledané x jsme dali na konec, takže jsme nemuseli řešit vytečení ze seznamu
		- u stromu se zarážkou nasměrujeme všechny listy (které by normálně směřovaly na None) na zarážku
	- vyvážené stromy
		- dokonale vyvážený binární strom
			- pro každý uzel platí, že počet uzlů v jeho levém a pravém podstromu se liší nejvýše o 1
			- nejlepší možné vyvážený, výška stromu s N uzly je $\lceil\log{N}\rceil$
			- lze snadno postavit z předem známé množiny hodnot
			- je obtížné ho udržovat
			- proto se používají slabší definice vyváženosti
		- výškově vyvážený strom (AVL)
		- na začátku sestavím dokonale vyvážený, poté ho udržuju ve stavu výškové vyváženosti
		- stavění stromu – viz prezentace
		- balance
		- rotace pro zajímavost v prezentaci, ale nebude zkoušeno


## Prohledávání stavového prostoru

- hledání pokladu v bludišti
	- zkouším postupně všechny cesty
	- bludiště obecně není strom (procházím typicky nějaký spojitý graf)
		- může vzniknout situace, že dojdu na křižovatku, na které už jsem byl
	- název algoritmu
		- prohledávání do hloubky, prohledávání s návratem
		- DFS (depth-first search), backtracking
- proskákání šachovnice koněm – příliš časově náročné
- urychlení prohledávání do hloubky
	- ořezávání – v průběhu vyhodnocuji, jestli má smysl postupovat ve stromu dál
		- osm dam na šachovnici (aby se dvě navzájem neohrožovaly)
			- bez ořezávání – zkoušet všechny výběry 8 polí z 64
			- základní ořezávání – na každém řádku právě jedna dáma, po umístění všech osmi dam otestovat kolize
			- lepší ořezávání – hned při umišťování každé dámy testovat kolize s dámami umístěnými na předchozích řádcích
		- magické čtverce
	- heuristika – odhad, kde je asi větší šance na nalezení řešení (u úloh, kde hledám jedno řešení) → podle toho určím pořadí procházení variant možných pokračování
		- u koně volím ty umístění, z nichž mám nejmenší počet možných dalších kroků
- prohledávání stavového prostoru do šířky – breadth-first search (BFS), algoritmus „vlny“
	- souběžně zkoušíme všechny možné varianty pokračování výpočtu až do nalezení řešení úlohy – v každé vrstvě zkoušíme všechny možnosti zleva doprava
	- může být paměťově velmi náročné, až nepoužitelné
	- vždy najde nejkratší možné řešení co do počtu kroků
	- k nalezení samotné cesty je potřeba „zpětný chod“
- zkouška
	- ve zkouškovém období
	- informace na moodlu, ukázka úloh z minulého ročníku
	- velká písemka každý týden ve zkouškovém v pondělí dopoledne, termíny společné pro obě paralelky v N1
	- potřebujeme zápočet
	- termíny budou vypsány kolem Vánoc
	- povinná písemná a nepovinná ústní část
	- v písemné části asi 4 příklady
	- úlohy vyřešíme, součástí některých úloh je i napsat funkci v Pythonu, ale není naší povinností ji odladit, nebudou se kontrolovat detaily syntaxe, jde hlavně o princip
	- zkoušku budeme řešit v Moodlu, budeme moct používat vlastní notebook s Moodlem (takže můžeme používat prezentace z přednášek)
	- je možná i papírová varianta
	- kdo dostane 2 nebo 3 a bude si chtít zlepšit známku, bude moct přijít na ústní část zkoušky – výsledná známka se bude skládat ze dvou známek (může být lepší nebo i horší)

- minimax
	- na tahu bílého se hledá maximum, na tahu černého minimum
	- u malých her se dá postavit celý strom
	- řeší se průchodem do hloubky (klasický backtracking), v listech se výsledek ohodnotí (výhra = 1, prohra = 0, remíza = –1)
	- někdy se používá negamax – prohazuje se znaménko, protože $\text{min}(a,b) = -\text{max}(-a,-b)$
	- u velkých her rozvíjím hru do určité hloubky, pak to zaříznu (čím větší hloubka, tím chytřejší tahy)
		- v té hloubce se na pozice zavolá statická ohodnocovací funkce, která každou z nich ohodnotí
		- často se ohodnocení vylepšuje tak, že pokud je koncová pozice „živá“ (nastávají výrazné změny na herním poli), tak se strom počítá ještě o úroveň níž
	- ořezávání stromu
		- ztrátové
			- provedu statické ohodnocení po několika málo vrstvách
			- část nejhorších pozic odmítnu, zbytek rozvíjím dál
		- bezztrátové – alfa-beta-prořezávání
			- využívá principu minimaxu – jeden hráč hledá minimum, druhý maximum, tedy v některých situacích není potřeba dopočítávat další varianty hry
			- dá se přidat heuristika – procházím postupně do uzlů, které mají lepší (nebo naopak horší) výsledek statického ohodnocení
- rozděl a panuj (divide et impera)
	- metoda rekurzivního návrhu algoritmu (programu)
	- problém se rozdělí na dva podproblémy, které se obvykle řeší lépe, z jejich řešení se dá sestavit řešení původního problému
	- je problematické použít tuto metodu u úloh, kdy jednotlivé podúlohy jsou na sobě závislé (mají společné části) – viz Fibonacci
	- vyhodnocení aritmetického výrazu
	- hanojské věže
		- abych přenesl celou věž z A na B, musím nejdřív dostat horní část na C, potom přesunout spodní kotouč z A na B a pak na něj přenést horní část
	- mergesort
		- rozdělujeme na půl
		- sléváme
	- quicksort
		- vyberu číslo (pivot) – typicky náhodně nebo uprostřed pole
		- prvky rozdělím na menší, rovné a větší než pivot
		- dá se třídit na místě – jdu zleva a zprava, hledám větší/menší, až najdu, tak prohodím a jedu dál
		- v průměru počítá nejrychleji ze všech algoritmů – O(N log N)
		- v nejhorším případě kvadratický (když volím špatné pivoty)
		- pokud chci garantovanou složitost, tak quicksort není dobrá volba
		- volba pivota
			- jeden náhodně vybraný prvek
			- vzorkování – medián ze tří náhodně zvolených prvků
			- náhodný výběr + ověření, zda je alespoň 1/4 prvků menších a 1/4 prvků větších
			- nalezení mediánu tříděného úseku (existuje algoritmus, který hledá v lineárním čase) – zajistí složitost O(N log N), ale v průměru bude pomalejší, protože vzroste multiplikativní konstanta