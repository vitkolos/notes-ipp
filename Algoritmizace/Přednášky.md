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