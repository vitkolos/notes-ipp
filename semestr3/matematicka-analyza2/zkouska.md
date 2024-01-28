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

- Věta: Kompaktní prostor, podprostor, součin
	- definice: metrický prostor $(X,d)$ je kompaktní, obsahuje-li v něm každá posloupnost konvergentní podposloupnost
	- tvrzení: podprostor kompaktního prostoru je kompaktní, právě když je uzavřený
		- mějme posloupnost v uzavřeném podprostoru, tato posloupnost má podposloupnost s limitou v kompaktním prostoru – z uzavřenosti tato limita musí být v podprostoru
		- mějme posloupnost v otevřeném podprostoru, ta má limitu mimo podprostor – každá její podposloupnost má tu stejnou limitu mimo podprostor, tedy daná posloupnost není konvergentní v podprostoru
	- tvrzení: je-li podprostor $Y$ metrického prostoru $(X,d)$ kompaktní, pak je $Y$ uzavřený v $(X,d)$
		- mějme posloupnost v kompaktním podprostoru, která konverguje k $y\in X$, potom každá její podposloupnost konverguje k $y$, tudíž musí být $y\in Y$
	- definice: metrický prostor $(X,d)$ je omezený, jestliže pro nějaké $K$ platí $\forall x,y\in X:d(x,y)\lt K$
	- tvrzení: každý kompaktní prostor je omezený
		- posloupnost $(x_n)_n$, kde $d(x_0,x_n)\gt n$, nemá žádnou omezenou podposloupnost, tedy nemá konvergentní podposloupnost (neboť ta je vždy omezená), což je spor
	- věta: součin konečně mnoha kompaktních prostorů je kompaktní
	- důkaz – stačí pro součin dvou prostorů
		- mějme posloupnost $((x_n,y_n))_n$ v $X\times Y$
		- zvolíme konvergentní podposloupnost $(x_{k_n})_n$ posloupnosti $(x_n)_n$ a konvergentní podposloupnost $(y_{k_{l_n}})_n$ posloupnosti $(y_{k_n})$
		- pak je posloupnost $((x_{k_{l_n}},y_{k_{l_n}}))_n$ zjevně konvergentní podposloupností původní posloupnosti
- Věta: Kompaktní podprostory $\mathbb E_n$
	- věta: podprostor euklidovského prostoru $\mathbb E_n$ je kompaktní, právě když je omezený a uzavřený
	- důkaz
		- již jsme dokázali, že kompaktnost implikuje uzavřenost a omezenost
		- mějme $Y\subseteq\mathbb E_n$ omezený a uzavřený
		- z omezenosti vyplývá, že pro dostatečně velký součin (uzavřených) intervalů $J$ platí $Y\subseteq J\subseteq\mathbb E_n$
			- intervaly jsou kompaktní, jejich součin je taky kompaktní (viz věta výše)
		- $Y$ je uzavřený v $\mathbb E_n$, tedy je uzavřený i v $J$
- Věta: Obraz kompaktního prostoru
	- tvrzení: buď $f:(X,d)\to(Y,d')$ spojité zobrazení a buď $A\subseteq X$ kompaktní, potom je $f[A]$ kompaktní
	- důkaz
		- buď $(y_n)_n$ posloupnost v $f[A]$
		- zvoljme $x_n\in A$, aby $y_n=f(x_n)$
		- posloupnost $(x_n)_n$ má konvergentní podposloupnost $(x_{k_n})_n$
		- $(y_{k_n})_n=(f(x_{k_n}))_n$ je konvergentní podposloupnost posloupnosti $(y_n)_n$
- Věta: Maxima a minima spojitých funkcí na kompaktních podmnožinách
	- tvrzení: buď $(X,d)$ kompaktní, potom každá spojitá funkce $f:(X,d)\to\mathbb R$ nabývá maxima i minima
	- důkaz
		- podprostor $Y=f[X]\subseteq\mathbb R$ je kompaktní
		- $Y$ je tedy omezená množina a musí mít supremum $a$ a infimum $b$
		- zřejmě $d(a,Y)=d(b,Y)=0$
		- $Y$ je uzavřená, proto $a,b\in Y$
- Věta: Stejnoměrná spojitost v kompaktním kontextu
	- věta: buď $f:X\to Y$ spojité zobrazení, $X$ kompaktní, potom $f$ je stejnoměrně spojité
	- důkaz – obměnou (zobrazení není stejnoměrně spojité, pak není spojité)
		- uvažujme epsilon takové, že pro každé delta existuje dvojice $x,y$ takové, že jsou si blíž než delta, ale $d(f(x),f(y))\geq\varepsilon$
		- z dvojicí sestavíme posloupnosti $(x_n)_n$ a $(y_n)_n$ – obě mají konvergentní podposloupnosti, ty volíme tak, aby si odpovídaly (jako v důkazu kompaktnosti součinu), mají stejnou limitu
		- limity funkčních hodnot se zjevně nerovnají (to je negace tvrzení ekvivalentnímu spojitosti zobrazení)
	- tvrzení: je-li $(X,d)$ kompaktní a je-li $f:(X,d)\to(Y,d')$ vzájemně jednoznačné spojité zobrazení, je to homeomorfismus
- Věta: Cauchyovské posloupnosti a konvergence
	- definice: posloupnost $(x_n)_n$ v metrickém prostoru $(X,d)$ je Cauchovská, jestliže $(\forall\varepsilon\gt 0)(\exists n_0):m,n\geq n_0\implies d(x_m,x_n)\lt\varepsilon$
	- pozorování: každá konvergentní posloupnost je Cauchyovská
	- tvrzení: má-li Cauchyovská posloupnost konvergentní podposloupnost, potom konverguje (k limitě té posloupnosti)
	- důkaz
		- nechť $(x_n)_n$ je Cauchyovská a nechť $x$ je limita její konvergentní podposloupnosti $(x_{k_n})_n$
		- od nějakého $n_1$ platí $d(x_m,x_n)\lt\varepsilon$
		- od nějakého $n_2$ platí $d(x_{k_n},x)\lt\varepsilon$
		- jako $n_0$ vezmeme to větší z nich, od něj pak platí $d(x_n,x)\leq d(x_n,x_{k_n})+d(x_{k_n},x)\lt 2\varepsilon$
- Definice: Úplný prostor, kompaktnost implikuje úplnost
	- definice: metrický prostor $(X,d)$ je úplný, jestliže v něm každá Cauchyovská posloupnost $(X,d)$ konverguje
	- tvrzení: podprostor úplného prostoru je úplný, právě když je uzavřený
	- tvrzení: každý kompaktní prostor je úplný
		- Cauchyovská posloupnost má z kompaktnosti konvergentní podposloupnost, a tedy konverguje (podle tvrzení výše)
	- věta: součin úplných prostorů je úplný; speciálně, $\mathbb E_n$ je úplný
	- důsledek: podprostor $Y$ euklidovského prostoru $\mathbb E_n$ je úplný, právě když je tam uzavřený

## Reálné funkce více proměnných

- Příklad: Proč se nemůžeme omezit na spojitost v jednotlivých proměnných
	- mějme funkci $f(x,y)=\begin{cases}\frac{(x-y)^2}{x^2+y^2}&\text{pro }(x,y)\neq(0,0)\\ 1&\text{pro }(x,y)=(0,0)\end{cases}$
	- pokud bychom $y$ vzali jako parametr a sledovali spojitost podle $x$, funkce by byla spojitá – podobně pro $x$ jako parametr
	- ale $f(x,x)$ se vždy rovná 0, kdežto $f(0,0)=1$
	- nezajímá nás spojitost v jednotlivých proměnných – to jsou jen některé „procházky“ po hodnotách funkce, nás zajímají všechny takové „cesty“
- Definice: Reálné funkce a jejich definiční obory (vhodné podprostory $\mathbb E_n$)
	- definice: reálná funkce v $n$ proměnných … $f:D\to\mathbb R,\;D\subseteq\mathbb E_n$
	- definiční obory jsou často poměrně složité množiny

## Parciální derivace

- Definice: Parciální derivace a jejich slabost (ani spojitost není implikována)
	- vezměme $\phi_k(t)=f(x_1,\dots,x_{k-1},t,x_{k+1},\dots,x_n)$
	- parciální derivace funkce $f$ podle $x_k$ (v bodě $(x_1,\dots,x_{k-1},t,x_{k+1},\dots,x_n)$) je derivace funkce $\phi_k$ (v bodě $t$)
	- tzn. $\lim_{h\to 0}\frac{f(x_1,\dots,x_{k-1},x_k+h,x_{k+1},\dots,x_n)-f(x_1,\dots,x_n)}{h}$
	- značíme $\frac{\partial f(x_1,\dots,x_n)}{\partial x_k}$ nebo $\frac{\partial f}{\partial x_k}(x_1,\dots,x_n)$
	- když $\frac{\partial f(x_1,\dots,x_n)}{\partial x_k}$ existuje pro všechna $(x_1,\dots,x_n)$ v nějaké oblasti $D$, máme funkci $\frac{\partial f}{\partial x_k}:D\to\mathbb R$
	- parciální derivace tedy může být číslo (hodnota limity výše) nebo tato funkce
	- parciální derivace geometricky odpovídá tečně funkce v daném bodě rovnoběžné s příslušnou osou
	- existence parciálních derivací neimplikuje spojitost (viz protipříklad na spojitost v jednotlivých proměnných)
- Definice: Totální diferenciál, geometrická interpretace (lineární aproximace)
	- *v případě jedné proměnné existence totálního diferenciálu a derivace je totéž*
	- tvrzení ekvivalentní s existencí standardní derivace
		- existuje $\mu$ konvergující k 0 při $h\to 0$ a $A$ takové, že $f(x+h)-f(x)=Ah+|h|\cdot\mu(h)$
	- geometrický pohled: $f(x+h)-f(x)=Ah$ vyjadřuje tečnu ke grafu funkce v bodě $(x,f(x))$
	- aproximační pohled: $|h|\cdot\mu(h)$ je jakási malá chyba při aproximaci funkce $f$ v okolí bodu $x$ jako lineární funkce v $h$
	- parciální derivace vyjadřují směry dvou tečných přímek – my chceme tečnou rovinu (tu dostaneme z totálního diferenciálu)
	- pro $x\in\mathbb E_n$ definujme $\lVert x\rVert=\max_i|x_i|$
	- funkce $f$ má totální diferenciál v bodě $x$, existuje-li funkce $\mu$ spojitá v okolí $U$ bodu $o$ taková, že $\mu(o)=0$, a čísla $A_1,\dots,A_n$, pro která $f(a+h)-f(a)=\sum_{k=1}^nA_kh_k+\lVert h\rVert\mu(h)$
		- pomocí skalárního součinu také $f(a+h)-f(a)=\braket{A|h}+\lVert h\rVert\mu(h)$
	- tvrzení: nechť má funkce $f$ totální diferenciál v bodě $a$, potom je spojitá v $a$ a má všechny parciální derivace v $a$ s hodnotami $\frac{\partial f(a)}{\partial x_k}=A_k$
	- důkaz spojitosti
		- chceme $\lim_{x\to y} f(x)=f(y)$, tedy $\lim_{x\to y} f(x)-f(y)=0$
		- dosadíme do rovnice totálního diferenciálu (a+h … x, a … y)
		- $|f(x)-f(y)|\leq|A(x-y)|+|\mu(x-y)|\cdot\lVert x-y\rVert$
		- limita $|A(x-y)|+|\mu(x-y)|\cdot\lVert x-y\rVert$ pro $x\to y$ je rovna nule
	- důkaz hodnot parciálních derivací
		- z rovnice totálního diferenciálu máme $\frac{f(x_1,\dots,x_{k-1},x_k+h,x_{k+1},\dots,x_n)-f(x_1,\dots,x_n)}{h}=A_k+\frac{\lVert(0,\dots,h,\dots,0)\rVert\cdot\mu((0,\dots,h,\dots,0))}{h}$
		- limita pravé strany je zjevně $A_k$
- Věta: Spojité parciální derivace a totální diferenciál
	- věta: nechť má $f$ spojité parciální derivace v okolí bodu $a$, potom má v bodě $a$ totální diferenciál
	- důkaz
		- položme $h^{(0)}=h,\;h^{(1)}=(0,h_2,\dots,h_n),\;h^{(2)}=(0,0,h_3,\dots,h_n),\;\dots,\;h^{(n)}=o$
		- máme $f(a+h)-f(a)=\sum_{k=1}^n(f(a+h^{(k-1)})-f(a+h^{(k)}))=M$
			- v té sumě se většina členů odečte, proto se to rovná výrazu nalevo
		- podle Lagrangeovy věty (v jedné proměnné) existují $0\leq\theta_k\leq 1$ takové, že $f(a+h^{(k-1)})-f(a+h^{(k)})=\frac{\partial f(a_1,\dots,a_{k-1},a_k+\theta_kh_k,a_{k+1}+h_{k+1},\dots,a_n+h_n)}{\partial x_k}\cdot h_k$
		- tedy $M=\sum\frac{\partial f(a_1,\dots,a_{k-1},a_k+\theta_kh_k,a_{k+1}+h_{k+1},\dots,a_n+h_n)}{\partial x_k}h_k=$
		- $=\sum\frac{\partial f(a)}{\partial x_k}h_k+\sum\left(\frac{\partial f(a_1,\dots,a_{k-1},a_k+\theta_kh_k,a_{k+1}+h_{k+1},\dots,a_n+h_n)}{\partial x_k}-\frac{\partial f(a)}{\partial x_k}\right)h_k=$
		- $=\sum\frac{\partial f(a)}{\partial x_k}h_k+\lVert h\rVert\sum\left(\frac{\partial f(a_1,\dots,a_{k-1},a_k+\theta_kh_k,a_{k+1}+h_{k+1},\dots,a_n+h_n)}{\partial x_k}-\frac{\partial f(a)}{\partial x_k}\right){h_k\over\lVert h\rVert}$
		- položme $\mu(h)=\sum\left(\frac{\partial f(a_1,\dots,a_{k-1},a_k+\theta_kh_k,a_{k+1}+h_{k+1},\dots,a_n+h_n)}{\partial x_k}-\frac{\partial f(a)}{\partial x_k}\right){h_k\over\lVert h\rVert}$
		- jelikož $\left|\frac{h_k}{\lVert h\rVert}\right|\leq 1$ a jelikož jsou funkce $\frac{\partial f}{\partial x_k}$ spojité, $\lim_{h\to o}\mu(h)=0$
	- máme tedy implikace: spojité parciální derivace $\implies$ totální diferenciál $\implies$ parciální derivace
- Definice: Výpočet parciálních derivací – aritmetická pravidla
	- jsou stejná jako pro obyčejné derivace
	- pravidlo pro skládání se liší
- Složená zobrazení a řetězové pravidlo
	- věta
		- nechť má $f(x)$ totální diferenciál v bodě $a$
		- pro $k=1,\dots,n$
			- nechť mají $g_k(t)$ derivace v bodě $b$
			- nechť je $g_k(b)=a_k$
		- položme $F(t)=f(g(t))=f(g_1(t),\dots,g_n(t))$
		- potom má $F$ derivaci v $b$, totiž $F'(b)=\sum_{k=1}^n\frac{\partial f(a)}{\partial x_k}\cdot g'_k(b)$
	- důkaz
		- $\frac1h(F(b+h)-F(b))=\frac1h(f(g(b+h))-f(g(b)))=$
		- $=\frac1h\biggl(f\Bigl(g(b)+(g(b+h)-g(b))\Bigl)-f(g(b))\biggr)=$
			- do rovnice totálního diferenciálu dosazujeme: x … g(b), h … (g(b+h)-g(b))
		- $=\sum_{k=1}^n A_k\frac{g_k(b+h)-g_k(b)}h+\mu(g(b+h)-g(b))\cdot\max_k\frac{|g_k(b+h)-g_k(b)|}h$
		- ze spojitosti funkcí $g_k$ v $b$ vyplývá $\lim_{h\to 0}\mu(g(b+h)-g(b))=0$
		- z toho, že $g_k$ mají derivace, vyplývá, že $\max_k\dots$ je omezené v dostatečně malém okolí nuly
		- limita posledního sčítance je tedy nula
		- $F'(b)=\lim_{h\to 0}\frac1h(F(b+h)-F(b))=\lim_{h\to0}\sum_{k=1}^nA_k\frac{g_k(b+h)-g_k(b)}h=$
		- $=\sum A_k\lim\frac{g_k(b+h)-g_k(b)}h=\sum\frac{\partial f(a)}{\partial x_k}\cdot g'_k(b)$
			- tady vycházíme z tvrzení o hodnotách parciálních derivací
	- důsledek – řetězové pravidlo
		- nechť má $f(x)$ totální diferenciál v bodě $a$
		- pro $k=1,\dots,n$
			- nechť mají funkce $g_k(t_1,\dots,t_r)$ parciální derivace v $b=(b_1,\dots,b_r)$
			- nechť je $g_k(b)=a_k$
		- potom má funkce $(f\circ g)(t_1,\dots,t_r)=f(g(t))=f(g_1(t),\dots,g_n(t))$ všechny parciální derivace v $b$ a platí $\frac{\partial(f\circ g)(b)}{\partial t_j}=\sum_{k=1}^n\frac{\partial f(a)}{\partial x_k}\cdot\frac{\partial g_k(b)}{\partial t_j}$
- Lagrangeova formule
- Parciální derivace vyšších řádů
- Záměnnost

## Věty o implicitních funkcích

- Úloha implicitních funkcí, porozumění problému
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
