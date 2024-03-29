# Úvod do AI – cvičení

## A*

- u Dijkstra v nekonečném grafu použijeme hashovací tabulku
- v A* heuristice nevybíráme vrcholy u podle vzdálenosti od startu, ale přičteme k ní heuristiku vzdálenosti od cíle
	- v domácím úkolu to vrací heuristiku nula (tzn. je to Dijkstra)
	- chceme, aby byla heuristika nezáporná
	- heuristika by neměla přestřelovat skutečnou vzdálenost
		- tzn. měla by být *přípustná*
		- pokud přestřelí, může se stát, že nalezená cesta nebude nejkratší
	- v reálném světě je vhodná heuristika vzdálenost vzdušnou čarou
- heuristika
	- přípustnost $0\leq h(u)\leq c^*(u)$
	- monotonie $0\leq h(u)\leq h(v)+c(u,v)$
- příklady metrik, jejich vlastnosti pro silniční síť
	- Euklidovská – je přípustná, je i monotónní
		- $h(u,t)\leq h(u,v)+h(v,t)\leq c(u,v)+h(v,t)$
			- z trojúhelníkové nerovnosti a přípustnosti
			- přičemž $h(x,t)=h(x)$
	- Manhattanská – přestřeluje (kdyby cesta vedla diagonálně), takže není přípustná, tudíž není ani monotónní
	- maximová (Chebyshevova) – je přípustná (maximum je menší rovno Euklidovi)
- k důkazu monotonie metriky potřebujeme trojúhelníkovou nerovnost dané metriky a její přípustnost
- monotonie implikuje přípustnost
- existují nemonotónní přípustné heuristiky
- monotonii potřebujeme, abychom se při prohledávání posouvali ve směru cíle
- Sokoban
	- nepříliš dobrá (ale monotónní) heuristika – pro každou krabici vzdálenost od nejbližšího cíle, přes to součet
		- monotónní je, protože v každém kroku se sníží nejvýš o jedna
	- chtěli bychom najít přiřazení krabic, které má nejmenší celkovou cenu
		- hledáme minimální vážené perfektní párování – to jde v lineárním čase
	- chceme řešit vzdálenost panáčka, takže do heuristiky započteme vzdálenost panáčka od nejbližší krabice minus jedna
	- když je krabice v rohu, tak se nemůžeme dostat nikam dál
		- takže je to nepřípustný stav
		- můžeme algoritmu o tom stavu vůbec neříkat
		- můžeme nastavit heuristiku na „nekonečno“
- vlastnosti A*
	- $f(u)=h(u)+g(u)$, kde $h$ je heuristika, $g$ je vzdálenost ze startu do $u$
	- uvažujme monotónní heuristiku
	- hodnoty $f(u)$ jsou neklesající na všech nejkratších cestách ze startu
		- $h(u)+g(u)\leq h(v)+g(v)$
		- $h(u)\leq h(v)+g(v)-g(u)$
		- pro $u,v$ na nejkratší cestě
			- $h(u)\leq h(v)+c(u,v)$
	- A* prozkoumává stavy v pořadí, ve kterém hodnoty $f(u)$ neklesají
- kombinování heuristik
	- afinní kombinace $\alpha h_1+(1-\alpha)h_2$, kde $\alpha\in[0,1]$
	- maximová kombinace $\max\set{h_1,h_2}$
	- přípustnost je jednoduché ukázat
	- jsou-li heuristiky monotónní, je monotónní jejich kombinace?
		- afinní
			- máme
				- $h_1(u)\leq h_1(v)+c(u,v)$
				- $h_2(u)\leq h_2(v)+c(u,v)$
			- chceme $\alpha h_1(u)+(1-\alpha)h_2(u)\leq c(u,v)+\alpha h_1(v)+(1-\alpha)h_2(v)$
			- stačí přenásobit ty dvě rovnosti $\alpha$ a $(1-\alpha)$ a sečíst
		- maximová
			- $\max\set{h_1(u),h_2(u)}$ se BÚNO rovná $h_1(u)\leq c(u,v)+h_1(u)$
			- $\leq c(u,v)+\max\set{h_1(v),h_2(v)}$
	- maximum je vždycky větší (blíž reálné hodnotě) než afinní
	- typicky nechceme strávit hodně času výpočtem heuristiky
	- dává smysl vymyslet několik heuristik a pak použít jejich maximum
	- k domácímu úkolu
		- je fajn se podívat do zdrojáků
		- kratší řešení jsou typicky lepší

## CSP

- NP-úplný problém
- na vstupu
	- proměnné
	- domény (pro každou proměnnou jedna)
	- podmínky
- typické podmínky
	- nerovnost
	- all_different(…)
	- logické spojky
	- aritmetika
- dva hlavní problémy
	- solving
		- algoritmy: backtracking, forward check, look ahead
		- backtracking
			- zkusím ohodnotit proměnnou
			- zkontroluju constraints
			- když constraints jsou splněny, ohodnotím další proměnnou
				- jinak zkusím jiné ohodnocení
				- když žádné ohodnocení nefunguje, vrátím fail
		- forward check
			- při backtrackingu začínám v proměnné A
			- přiřadím jí hodnotu, ostatní prvky z domény vyškrtnu
			- přejdu do proměnné B
			- podívám se na všechny hrany (constraints), které vedou z B do již přiřazených proměnných (?)
				- proškrtám prvky v doméně B, které constraints nemůžou splnit
		- look ahead
			- jako forward check
			- pokud zmenším doménu, zkontroluju hrany, které do ní vedou (?)
	- modelování
- jak najít chromatické číslo?
	- binární vyhledávání?
	- pro náš úkol je lepší po jednom zvyšovat $k$ (počet barev)
	- začít u hodnoty o jedno vyšší než nejvyšší stupeň vrcholu
- tvorba SAT klauzulí
	- aspoň jeden … disjunkce
	- nejvýš jeden … konjunkce přes disjunkce všech dvojic negací
	- nejvýš $k$ … konjunkce disjunkcí negací všech $k+1$-tic
	- alespoň $k$ … převedeme na nejvýše $n-k$ negací
- jakmile máme k CSP úloze k dispozici testy, je jasné, co máme dát do constraints

## Automatické plánování

- v domácím úkolů nepoužívat typování objektů – „typovat“ klasicky unárními predikáty
- v SISu jsou nahrávky přednášek
- PDDL robot s chapadly
	- neexistenční kvantifikátor nemůžeme použít, tak tam dáme pomocný predikát `free` (chapadlo je prázdné)
	- při move nechceme přesouvat všechny věci, které robot drží – místo toho je zrušíme z místnosti a dáme mu je do ruky
	- predikáty definujeme tak, aby se úloha zapisovala co nejjednodušeji
- u neorientovaného grafu je potřeba vyjmenovat oba směry hran
- PDDL v základní verzi neumí negace předpokladů
- hanojské věže
	- při přesunu potřebujeme znát disk nahoře na cílové tyči – přidáme si další argument
	- typové predikáty nepotřebujeme, protože relaci „menší“ definujeme jenom pro disky a stůl (a nic není větší než stůl, takže ho nemůžeme přesouvat)
- v domácím úkolu je potřeba akce nazvat správně a mít správné pořadí argumentů kvůli testu

## Pravděpodobnost

- výsledek akce nemusí být deterministický, nemáme kompletní informaci o stavu apod.
- 
