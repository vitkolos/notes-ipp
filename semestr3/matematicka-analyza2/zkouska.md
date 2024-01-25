# Zkouška

tyto výpisky jsou založeny na [poznámkách Viktora Soukupa, Lukáše Salaka a Tomáše Slámy](https://slama.dev/poznamky/matematicka-analyza-ii/)

## Metrické prostory

- Definice: Metrický prostor, příklady, $\mathbb E_n$
	- metrický prostor je uspořádaná dvojice $(X,d)$, kde $X$ je množina a $d:X\times X\to\mathbb R$ je funkce, pro níž platí ($\forall x,y,z\in X$)
		- $d(x,y)\geq 0$
		- $d(x,y)=0\iff x=y$
		- $d(x,y)=d(y,x)$
		- $d(x,z)\leq d(x,y)+d(y,z)$ … trojúhelníková nerovnost
	- příklady
		- $(\mathbb R,|x-y|)$
		- $(\mathbb C,|x-y|)$
		- euklidovský prostor $\mathbb E_n$ je metrický prostor $(\mathbb R^n,d)$, kde $d(x,y)=\sqrt{\sum_i(x_i-y_i)^2}$
			- tzn. $d(x,y)=\lVert x-y\rVert$, kde $\lVert u\rVert=\sqrt{\braket{u|u}}$
		- diskrétní prostor $(X,d)$, kde $d(x,y)=1$ pro $x\neq y$
		- prostor funkcí $(F(a,b),d)$
			- $F(a,b)$ … množina všech omezených funkcí na intervalu $\braket{a,b}$
			- $d(f,g)=\sup\Set{|f(x)-g(x)|\mid a\leq x\leq b}$
- Definice: Podprostor metrického prostoru
	- mějme $(X,d)$ metrický prostor a podmnožinu $Y\subseteq X$
	- tato podmnožina tvoří podprostor $(Y,d')$, kde $d'(x,y)=d(x,y)$
- Definice: Spojité zobrazení, konvergence
	- zobrazení $f:(X,d)\to (Y,d')$ je spojité, platí-li $(\forall x,y\in X)(\forall\varepsilon\gt 0)(\exists\delta\gt 0):d(x,y)\lt\delta\implies d'(f(x),f(y))\lt\varepsilon$
		- složení spojitých zobrazení je spojité
	- pro posloupnost $(x_n)_n$ definujeme $\lim_n x_n=x$ takto: $(\forall\varepsilon\gt 0)(\exists n_0):n\geq n_0\implies d(x,x_n)\lt\varepsilon$
		- pokud limita existuje, jde o konvergentní posloupnost
- Věta: Spojitost a konvergence
	- věta: zobrazení $f:(X_1,d_1)\to (X_2,d_2)$ je spojité, právě když pro každou konvergentní posloupnost $(x_n)_n$ v $(X_1,d_1)$ posloupnost $(f(x_n))_n$ konverguje v $(X_2,d_2)$ a platí $\lim_nf(x_n)=f(\lim_nx_n)$
	- důkaz
		- $\implies$
			- mějme $f$ spojitou a konvergentní posloupnost $(x_n)_n$, kde $\lim_n x_n=x$
			- ze spojitosti můžeme pro $\varepsilon\gt 0$ zvolit $\delta\gt0$ tak, aby $d_1(x,y)\lt\delta\implies d_2(f(x),f(y))\lt\varepsilon$
			- podle konvergence existuje $n_0$ takové, že pro $n\geq n_0$ je $d_1(x_n,x)\lt\delta$
			- tedy pro $n\geq n_0$ máme $d_2(f(x_n),f(x))\lt\varepsilon$
			- tudíž $\lim_nf(x_n)=f(\lim_nx_n)$
		- $\impliedby$ obměnou
			- nechť $f$ není spojitá
			- tzn. $(\exists x\in X_1)(\exists\varepsilon_0\gt 0)(\forall\delta\gt 0)(\exists x(\delta)):$ $d_1(x,x(\delta))\lt\delta\land d_2(f(x),f(x(\delta)))\geq\varepsilon_0$
			- položme $x_n=x(\frac1n)$
			- pak $\lim_nx_n=x$, ale $(f(x_n))_n$ nemůže konvergovat k $f(x)$
- Definice: Okolí, otevřené a uzavřené množiny
	- epsilonové okolí … $\Omega(x,\varepsilon)=\set{y\mid d(x,y)\lt\varepsilon}$
	- obecné okolí bodu $U$ bodu $x$ je taková podmnožina, že existuje $\varepsilon\gt0$ takové, že $\Omega(x,\varepsilon)\subseteq U$
		- nadmnožina okolí je okolí
		- průnik dvou okolí je okolí
	- $U\subseteq(X,d)$ je otevřená, je-li okolím každého svého bodu
		- $\emptyset$ a $X$ jsou otevřené
		- sjednocení otevřených množin je otevřené
		- průnik dvou otevřených množin je otevřený
	- $A\subseteq(X,d)$ je uzavřená v $(X,d)$, jestliže každá posloupnost $(x_n)_n\subseteq A$ konvergentní v $X$ má $\lim_n x_n\in A$
	- nejde o dichotomii
	- tvrzení: $A\subseteq (X,d)$ je uzavřená v $(X,d)$, právě když $X\setminus A$ je otevřená
		- když $X\setminus A$ není otevřená (má nějaký „problémový bod“ $x$, jehož libovolně malé epsilonové okolí není celé v $X\setminus A$), tak se dá najít posloupnost v $A$ s limitou v $x\notin A$
		- když $X\setminus A$ je otevřená a kdyby existovala posloupnost v $A$ s limitou v $x\notin A$, tak epsilonové okolí $x$ není v $A$, tedy pro dost velké $n$ se prvky posloupnosti musí dostat mimo $A$, což je spor
- Definice: Uzávěr
	- vzdálenost bodu od množiny
		- $d(x,A)=\inf\set{d(x,a)\mid a\in A}$
	- uzávěr množiny $A$
		- $\overline A=\set{x\mid d(x,A)=0}$
	- uzávěr je množina všech limit konvergentních posloupností v dané množině
	- uzávěr je uzavřená množina (dokonce nejmenší uzavřená množina obsahující původní množinu)
- Věta: Spojitost a vzory otevřených a uzavřených podmnožin
	- věta
		- mějme metrické prostory $(X_1,d_1),(X_2,d_2)$ a zobrazení $f:X_1\to X_2$
		- potom jsou následující tvrzení ekvivalentní
			1. $f$ je spojité
			2. pro každý bod $x\in X_1$ a každé okolí $V$ bodu $f(x)$ existuje okolí $U$ bodu $x$ takové, že $f[U]\subseteq V$
			3. pro každou otevřenou $U$ v $X_2$ je vzor $f^{-1}[U]$ otevřený v $X_1$
			4. pro každou uzavřenou $A$ v $X_2$ je vzor $f^{-1}[A]$ uzavřený v $X_1$
			5. pro každou $A\subseteq X_1$ je $f[\overline A]\subseteq\overline{f[A]}$
	- důkaz
		- $1.\iff2.$
			- definice spojitosti říká, že ke každému okolí $\Omega(f(x),\varepsilon)$ existuje okolí $\Omega(x,\delta)$ takové, že $f[\Omega(x,\delta)]\subseteq\Omega(f(x),\varepsilon)$
			- dále rozšíříme na obecné okolí
		- $2.\implies 3.$
			- máme otevřenou množinu $V$
			- máme $x\in f^{-1}[V]$, tedy $f(x)\in V$, kde $V$ je okolí $f(x)$
			- existuje $U$ okolí $x$ takové, že $f[U]\subseteq V$
			- $U\subseteq f^{-1}f[U]\subseteq f^{-1}[V]$
			- takže $f^{-1}[V]$ je okolí $x$
			- otevřenost plyne z toho, že to platí pro všechny $f(x)\in V$ (respektive $x\in f^{-1}[V]$)
		- $3.\iff 4.$
			- vzorové zobrazení $M\mapsto f^{-1}[M]$ zachovává doplňky podmnožin
		- $4.\implies 5.$
			- $\overline M\subseteq f^{-1}[\overline{f[M]}]$ (vzor uzávěru je uzavřený)
			- $f[\overline M]\subseteq\overline{f[M]}$
		- $5.\implies 2.$
			- použijeme to, že vzor zachovává doplňky
- Definice: Topologické pojmy
	- vzájemně jednoznačné spojité zobrazení $f:(X_1,d_1)\to(X_2,d_2)$ takové, že i inverzní $f^{-1}$ je spojité, se nazývá homeomorfismus a o $X_1,X_2$ mluvíme jako o homeomorfních prostorech
	- vlastnost, pojem nebo definice je topologická, zachovává-li se při homeomorfismech
	- příklady topologických vlastností a pojmů: konvergence, otevřenost a uzavřenost, uzávěr, okolí, spojitost (stejnosměrná nikoliv)
- Definice: Ekvivalentní a silně ekvivalentní metriky; silně ekvivalentní metriky v $\mathbb E_n$
	- $d_1,d_2$ jsou ekvivalentní, pokud je zobrazení $(X,d_1)\to(X,d_2)$ homeomorfismus
	- $d_1,d_2$ jsou silně ekvivalentní, existují-li kladné konstanty $\alpha,\beta$ takové, že $\alpha\cdot d_1(x,y)\leq d_2(x,y)\leq\beta\cdot d_1(x,y)$
	- silně ekvivalentní metriky v $\mathbb E_n$
		- $d(x,y)=\sqrt{\sum_i(x_i-y_i)^2}$
		- $\sigma(x,y)=\max_i{|x_i-y_i|}$
	- důkaz silné ekvivalence $d$ a $\sigma$
		- triviálně $\sigma\leq d$ … stačí vzít největší sčítanec pod odmocninou
		- nahrazením všech sčítanců tím největším získáme $d(x,y)\leq\sqrt n\cdot\sigma(x,y)$
- Definice: Stejnoměrná spojitost
	- zobrazení $f:(X,d)\to(Y,d')$ je stejnoměrně spojité, pokud…
		- $(\forall\varepsilon)(\exists\delta)(\forall x)(\forall y):d(x,y)\lt\delta\implies d'(f(x),f(y))\lt\varepsilon$
	- rozdíl vůči (klasické) spojitosti spočívá v pořadí kvantifikátorů – u spojitosti je to $(\forall x)(\forall y)(\forall\varepsilon)(\exists\delta)$
	- např. $f(x)=x^2$ je spojitá funkce, ale není stejnoměrně spojitá
- Věta: Součiny a projekce
	- pro $(X_i,d_i),\,i=1,\dots,n$ definujme na kartézském součinu $\prod_{i=1}^n X_i$ vzdálenost $d(x,y)=\max_id_i(x_i,y_i)$
	- takto získaný prostor $(\prod_iX_i,d)=\prod_i(X_i,d_i)$ nazýváme součinem prostorů $(X_i,d_i)$
	- věta
		1. $\forall j\in\set{1,\dots,n}$ projekce $p_j:\prod_i(X_i,d_i)\to(X_j,d_j)$, kde $p_j(x)=x_j$, je spojité zobrazení
		2. jsou-li $f_j:(Y,d')\to(X_j,d_j)$ libovolná spojitá zobrazení, potom jednoznačně určené zobrazení $f:(Y,d')\to\prod_i(X_i,d_i)$ splňující $p_j\circ f=f_j$, totiž zobrazení definované předpisem $f(y)=(f_1(y),\dots,f_n(y))$, je spojité
	- důkaz
		1. zjevně $\sigma(x_j,y_j)\leq\sigma((x_1,\dots,x_j,\dots,x_n),(y_1,\dots,y_j,\dots,y_n))$
		2. plyne z použití zde zadefinované metriky $d(x,y)$

## Kompaktní prostory

- Definice: Kompaktní prostor, podprostor, součin
- Kompaktní podprostory $\mathbb E_n$
- Obraz kompaktního prostoru
- Maxima a minima spojitých funkcí na kompaktních podmnožinách
- Stejnoměrná spojitost v kompaktním kontextu
- Cauchyovské posloupnosti a konvergence
- Úplný prostor, kompaktnost implikuje úplnost

## Reálné funkce více proměnných

- Proč se nemůžeme omezit na spojitost v jednotlivých proměnných
- Reálné funkce a jejich definiční obory (vhodné podprostory $\mathbb E_n$)

## Parciální derivace

- Definice a jejich slabost (ani spojitost není implikována)
- Totální diferenciál, geometrická interpretace (lineární aproximace)
	- V případě jedné proměnné existence totálního diferenciálu a derivace je totéž
- Spojité parciální derivace a totální diferenciál
- Výpočet: aritmetická pravidla
- Složená zobrazení a Řetězové pravidlo
- Lagrangeova formule
- Parciální derivace vyšších řádů
- Záměnnost

## Věty o implicitních funkcích

- Úloha, porozumění problému
- Nejjednodušší případ: $F(x, y) = 0$, role $\partial F\over\partial y$
- Jacobian a jeho role
- Obecná věta, porozumění tomu, co se děje
- Substituční metoda aspoň pro dvě rovnice
- Aplikace: Lokální extrémy, věta o vázaných extrémech, jak se používá
- Aplikace: Regulární zobrazení

## Riemannův integrál v jedné proměnné

- Opakování, geometrická interpretatce, obsahy atd.
- Rozdělení intervalu
- Existence pro spojité funkce, role stejnoměrné spojitosti
- Základní věta analýzy, Riemannův integrál a primitivní funkce

## Riemannův integrál ve více proměnných

- Až do existence pro spojité funkce (stačí pochopit podrozdělení jako rozklad na systém cihliček) zcela analogické s jednou proměnnou
- Fubiniho věta, jak ji používáme
- Poznámky o Lebesgueově integrálu: zejména praktická informace že smíme počítat jako s Riemannovým integrálem plus pravidlo $\int\lim f_n=\lim\int f_n$ pro stejně omezené $f_n$
- Co se dá udělat s kompaktními obory hodnot které nejsou intervaly
- Substituce (jen intuitivně; role Jacobiánu)