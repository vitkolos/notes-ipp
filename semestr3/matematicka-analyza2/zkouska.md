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
- Definice: Podprostor
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
	- $V\subseteq(X,d)$ je uzavřená v $(X,d)$, jestliže každá posloupnost $(x_n)_n\subseteq V$ konvergentní v $X$ má $\lim_n x_n\in V$
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
- Topologické pojmy
- Ekvivalentní a silně ekvivalentní metriky; silně ekvivalentní metriky v $\mathbb E_n$
- Stejnoměrná spojitost
- Součiny a projekce

## Kompaktní prostory

- Definice, podprostory, součiny
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
