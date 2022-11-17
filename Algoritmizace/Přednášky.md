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