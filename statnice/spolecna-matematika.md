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
- Součet řady a částečný součet řady
- Geometrická řada, harmonická řada
- Reálné funkce jedné reálné proměnné
	- limita funkce v bodě
		- definice, aritmetika limit
		- vztah s uspořádáním
		- limita složené funkce
	- funkce spojité na intervalu
		- nabývání mezihodnot
		- nabývání maxima
- Derivace a její aplikace
	- definice a základní pravidla pro výpočet
	- l’Hospitalovo pravidlo
	- vyšetření průběhu funkcí: extrémy, monotonie a konvexita/konkavita
	- Taylorův polynom (limitní forma)
- Integrály a jejich aplikace
	- primitivní funkce: definice a metody výpočtu (substituce, per-partes)
	- Riemannův integrál: definice, souvislost s primitivní funkcí (Newtonovým integrálem)
	- aplikace
		- odhady součtu řad (konečných i nekonečných)
		- obsahy rovinných útvarů
		- objemy a povrchy rotačních útvarů v prostoru
		- délka křivky

## 2. Algebra a lineární algebra

## 3. Diskrétní matematika

## 4. Teorie grafů

## 5. Pravděpodobnost a statistika

## 6. Logika
