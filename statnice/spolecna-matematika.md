# Společná matematika

## 1. Základy diferenciálního a integrálního počtu

- Posloupnosti reálných čísel a jejich limity (definice)
	- posloupnost s hodnotami v množině $M$ je zobrazení z $\mathbb N$ do $M$
	- nechť $(a_n)$ je reálná posloupnost a $L \in \mathbb R^*$
	- pokud $(\forall\varepsilon\gt 0)(\exists n_0\in\mathbb N):(n\geq n_0\implies |a_n-L|\lt\varepsilon)$, píšeme, že $\lim a_n=L$ nebo $\lim_{n\to\infty}a_n=L$ nebo $a_n\to L$, a řekneme, že posloupnost $(a_n)$ má limitu $L$
	- pro $L\in \mathbb R$ mluvíme o vlastní limitě a pro $L=\pm\infty$ o limitě nevlastní
	- posloupnost, která má vlastní limitu, konverguje (pokud ji nemá, tak diverguje)
	- každá posloupnost reálných čísel má nejvýše jednu limitu
- Aritmetika limit
	- nechť $(a_n),(b_n)$ jsou posloupnosti reálných čísel takové, že $\lim a_n=a$ a $\lim b_n=b$
	- pak…
		- $\lim\,(a_n+b_n)=a+b$
		- $\lim\,(a_nb_n)=ab$
		- pokud $b_n\neq 0$ pro každé $n\gt 0$, pak $\lim\,(a_n/b_n)=a/b$
	- to vše platí za předpokladu, že je výraz na pravé straně definován
		- neurčité výrazy (nejsou definované): součet nekonečen s různými znaménky, součin nekonečna s nulou, podíl nekonečen, dělení reálného čísla nulou
	- pokud je $(a_n)$ omezená a $(b_n)$ konverguje k nule, pak $\lim\,(a_nb_n)=0$
		- tzn. limita $(a_n)$ nemusí existovat
- Limity a uspořádání
	- nechť $(a_n),(b_n)$ jsou posloupnosti reálných čísel takové, že mají limity $\lim a_n=a$ a $\lim b_n=b$
	- když $a\lt b$, tak existuje $n_0$, že $n\gt n_0\implies a_n\lt b_n$
	- a naopak, když $a_n\leq b_n$ pro každé $n\gt n_0$, pak $a\leq b$
	- poznámka: může se stát, že $\forall n:a_n\lt b_n$, ale $\lim a_n=\lim b_n$
		- např. uvažujme $a_n=1-\frac1n\lt b_n=1$, přičemž $\lim a_n=\lim b_n=1$
- Věta o dvou policajtech
	- nechť posloupnosti $(a_n),(b_n),(c_n)\subseteq\mathbb R$ splňují
		- $\lim a_n=\lim b_n=a\in\mathbb R$
		- $\forall n\gt n_0:a_n\leq c_n\leq b_n$
	- pak $(c_n)$ konverguje a $\lim c_n=a$
	- platí to i pro nevlastní limity – tam nám stačí jeden policajt
- Součet řady a částečný součet řady
	- nekonečná řada (reálných čísel) je výraz $$\sum_{n=1}^\infty a_n=a_1+a_2+a_3+\dots$$
		- kde $(a_n)_{n\geq 1}$ je posloupnost reálných čísel
	- ($n$-tý) částečný součet řady se značí $s_n$ a je to součet jejích prvních $n$ členů ($s_n=a_1+a_2+\dots+a_n$)
	- pokud existuje vlastní limita posloupnosti $(s_n)$ částečných součtů dané řady, mluvíme o *konvergentní* řadě a limita $\lim s_n$ je jejím *součtem*
	- pokud $\lim s_n$ neexistuje nebo je nevlastní, je daná řada *divergentní*
- Geometrická řada, harmonická řada
	- geometrická řada
		- $\sum_{n=0}^\infty q^n=1+q+q^2+q^3+\dots$
		- $q\in\mathbb R$ je parametr zvaný *kvocient*
		- pro součet geometrické řady platí $$\sum_{n=0}^\infty q^n=\begin{cases}\frac1{1-q} &-1\lt q\lt1\\ +\infty &q\geq 1\\\text{neexistuje}&q\leq -1\end{cases}$$
		- vyplývá to ze vzorce pro částečný součet $s_n=\frac{q^n-1}{q-1}$
	- harmonická řada
		- $\sum_{n=1}^\infty\frac 1n=1+\frac12+\frac13+\dots$
		- diverguje, přestože její prvky konvergují k nule
	- pro řady tvaru $\sum_{n=1}^\infty\frac1{n^s}$ obecně platí, že konvergují pro $s\gt 1$ a divergují pro $s\leq 1$
- Limita funkce v bodě: definice, aritmetika limit
	- okolí bodu je interval $U(a,\delta)=(a-\delta,a+\delta)$
		- okolí nekonečen definujeme jako $U(+\infty,\delta)=(1/\delta,+\infty)$, podobně pro $-\infty$
		- definujeme také pravé okolí bodu $U^+(a,\delta)=[a,a+\delta)$, podobně levé okolí $U^-$
		- prstencová okolí bodu $a\in\mathbb R$ definujeme jako obyčejná okolí s vyjmutým bodem $a$, značí se jako $P(a,\delta)$ apod.
	- řekneme, že funkce $f$ má v bodě $a\in\mathbb R^*$ limitu $A\in\mathbb R$, když $(\forall\varepsilon\gt 0)(\exists\delta\gt 0):x\in P(a,\delta)\implies f(x)\in U(A,\varepsilon)$
		- zapisujeme $\lim_{x\to a}f(x)=A$
		- poznámka: limita funkce $f$ v bodě $a$ nezávisí na její hodnota v $a$, funkce $f$ dokonce ani nemusí být v $a$ definovaná
		- pokud místo prstencového okolí $P$ použijeme pravé prstencové okolí $P^+$, dostaneme definici limity zprava, značí se $\lim_{x\to a^+}f(x)$
			- obdobně lze definovat limitu zleva
			- pokud $\lim_{x\to a^+}f(x)=\lim_{x\to a^-}f(x)=A$, pak $\lim_{x\to a}f(x)=A$
			- naopak pokud jsou limity zprava a zleva různé, limita neexistuje
		- podobně jako u posloupnosti – pokud limita funkce existuje, je jednoznačně určena
		- limitu funkce lze rovněž definovat pomocí posloupnosti
- Limita funkce v bodě: vztah s uspořádáním
- Limita funkce v bodě: limita složené funkce
- Funkce spojité na intervalu: nabývání mezihodnot
- Funkce spojité na intervalu: nabývání maxima
- Derivace – definice a základní pravidla pro výpočet
- L’Hospitalovo pravidlo
- Vyšetření průběhu funkcí: extrémy, monotonie a konvexita/konkavita
- Taylorův polynom (limitní forma)
- Primitivní funkce: definice a metody výpočtu (substituce, per-partes)
- Riemannův integrál: definice, souvislost s primitivní funkcí (Newtonovým integrálem)
- Aplikace integrálů: odhady součtu řad (konečných i nekonečných)
- Aplikace integrálů: obsahy rovinných útvarů
- Aplikace integrálů: objemy a povrchy rotačních útvarů v prostoru
- Aplikace integrálů: délka křivky

## 2. Algebra a lineární algebra

- Algebraické struktury
	- grupy a podgrupy, permutace
	- tělesa a speciálně konečná tělesa
- Soustavy lineárních rovnic
	- maticový zápis, elementární řádkové úpravy, odstupňovaný tvar matice
	- Gaussova a Gaussova-Jordanova eliminace, popis množiny řešení
- Matice
	- operace s maticemi a základní typy matic, hodnost matice
	- regulární a inverzní matice
- Vektorové prostory
	- vektorový prostor, lineární kombinace, lineární závislost a nezávislost, lineární obal, systém generátorů
	- Steinitzova věta o výměně, báze, dimenze, souřadnice
	- vektorové podprostory, zejména maticové (řádkový, sloupcový, jádro) a jejich dimenze
- Lineární zobrazení
	- definice, maticová reprezentace lineárního zobrazení, matice složeného zobrazení
	- obraz a jádro lineárních zobrazení
	- isomorfismus prostorů
- Skalární součin
	- skalární součin, norma indukovaná skalárním součinem
	- Pythagorova věta, Cauchyho-Schwarzova nerovnost, trojúhelníková nerovnost
	- ortonormální systémy vektorů, Fourierovy koeficienty, Gramova-Schmidtova ortogonalizace
	- ortogonální doplněk, ortogonální projekce, projekce jako lineární zobrazení
	- ortogonální matice a jejich vlastnosti
- Determinanty
	- definice a základní vlastnosti determinantu (multiplikativnost, determinant transponované matice, vztah s
	regularitou a vlastními čísly)
	- Laplaceův rozvoj determinantu
	- geometrická interpretace determinantu
- Vlastní čísla a vlastní vektory
	- definice, geometrický význam a základní vlastnosti vlastních čísel, charakteristický polynom, násobnost vlastních čísel
	- podobnost a diagonalizovatelnost matic, spektrální rozklad
	- symetrické matice, jejich vlastní čísla a spektrální rozklad
- Positivně semidefinitní a positivně definitní matice
	- charakterizace a vlastnosti, vztah se skalárním součinem, vlastními čísly
	- Choleského rozklad (znění věty a praktické použití)

## 3. Diskrétní matematika

## 4. Teorie grafů

## 5. Pravděpodobnost a statistika

## 6. Logika
