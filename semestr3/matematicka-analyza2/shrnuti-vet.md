# Shrnutí některých vět

- implicitní funkce
	- znění: pro funkci $F(x,y)=0$ definovanou v okolí nějakého bodu a rovnou nule v daném bodě, která má spojité parciální derivace (a derivace podle $y$ není nulová), můžeme najít funkci, která odpovídá $y$ a má spojité parciální derivace
	- derivace podle $y$ je nenulová, ať je BÚNO kladná
	- v obdélníku jsou extrémy
	- nejdříve najdeme funkci
		- vezmeme funkci $\varphi_x$ jedné proměnné (pro pevné $x$)
		- ta má kladnou derivaci, takže roste, zároveň je prostá
		- přesně uprostřed okna je nulová
		- najdeme ostatní $y$, aby byla $\varphi_x$ nulová
		- tím dostaneme hledanou funkci
	- pak dokážeme její spojitost a vzorec pro derivaci
		- začneme s $0=F(x+h,f(x+h))-F(x,f(x))$
		- z $f(x+h)$ uděláme $f(x)+(f(x+h)-f(x))$
		- použijeme Lagrangeovu větu a chain rule
		- nakonec dostaneme $\frac{f(x+h)-f(x)}h=$ minus podíl parciálních derivací
		- z toho máme přímo derivaci a ta je spojitá, protože parciální derivace jsou spojité
		- z toho můžeme odvodit i spojitost, přičemž jako $\varepsilon$ použijeme $|h|\cdot\frac Ka$
- Fubiniho věta
	- znění: když místo přes součin intervalů integrujeme postupně přes každý z nich zvlášť, dostaneme správný výsledek
	- zvolíme rozdělení velkého intervalu (tedy součinu) takové, že máme $\int f-\varepsilon\leq s(f,P)\leq S(f,P)\leq\int f+\varepsilon$
	- jako $F(x)$ položíme integrál přes první proměnnou
	- zjevně horní součet těchto integrálů bude menší než horní součet $S(f,P)$
	- podobně dolní součet integrálů bude větší než dolní součet $s(f,P)$
	- takže jsme tyhle součty narvali doprostřed té nerovnosti
	- pro epsilon dostáváme rovnost integrálů $\int_{J'}F\int_Jf$
- záměnnost parciálních derivací
	- požadujeme spojitost parciálních derivací
	- uvažujeme funkci $F(h)$, kde jakoby derivujeme podle obou proměnných zároveň
	- položíme $\varphi_h(y)$ a $\psi_h(x)$ a s jejich pomocí získáme dvě vyjádření pro $F(h)$
		- pro ilustraci:
		- $\varphi_h(y)=f(x+h,y)-f(x,y)$
		- $F(h)=\frac1{h^2}(\varphi_h(y+h)-\varphi_h(y))$
	- dvakrát použijeme Lagrangeovu větu o střední hodnotě
	- nakonec limitíme
- chain rule
	- znění: derivace složené funkce je součet přes jednotlivé proměnné vnější funkce – sčítanec je součin parciální derivace vnější funkce podle $k$-té proměnné a derivace $k$-té vnitřní funkce
	- vnější funkce musí mít totální diferenciál
	- začneme s $\frac1h(F(x+h)-F(x))$
	- přepíšeme jako $f(g(\dots))$
	- $g(x+h)$ rozepíšeme na $g(x)+(g(x+h)-g(x))$
	- použijeme rovnici pro totální diferenciál
	- limitíme
	- nakonec zobecníme pro funkce více proměnných (z derivace složené funkce uděláme parciální derivaci složené funkce) a máme řetězové pravidlo
- spojitá funkce na kompaktním intervalu
	- znění: spojité zobrazení z kompaktní množiny je stejnoměrně spojité
	- důkaz obměnou – uvažujeme zobrazení, které není stejnoměrně spojité
	- tzn. pro dvojici $x,y$ blíž než delta jsou $f(x),f(y)$ dál než epsilon
	- pro každou deltu existuje nějaká taková dvojice $x,y$, uděláme z nich dvě posloupnosti $(x_n)_n$ a $(y_n)_n$
	- jejich limity se rovnají, limity jejich obrazů se nerovnají
	- tedy zobrazení není spojité
- totální diferenciál a spojitost + hodnoty parciálních derivací
	- spojitost
		- chceme $\lim_{x\to y}f(x)-f(y)$
		- zkusíme použít rovnici pro totální diferenciál (přičemž $h=x-y$, $a+h=x$, $a=y$)
		- zlimitíme pro $x\to y$
	- hodnoty
		- vezmeme $h$, co má nulové všechny složky kromě jedné
		- dosadíme do rovnice pro totální diferenciál a podělíme tím $h_k$
		- limitíme
		- na jedné straně dostaneme vzorec pro parciální derivaci, na druhé limitu $A_k+\mu(h)$, což je $A_k$
- spojité parciální derivace a totální diferenciál
	- zadefinujeme si pomocné $h^{(i)}$ jako $i$ nul a dál složky z původního $h$
	- vyjádříme $f(a+h)-f(a)$ jako součet mnoha dvojic členů, které se skoro všechny odečtou
	- na jednu dvojici použijeme Lagrangeovu větu a zapíšeme ji jako parciální derivaci vynásobenou $h_k$
	- ze součtu „vytáhneme“ člen $\frac{\partial f(a)}{\partial x_k}$, který tam původně nebyl, takže ho musíme zase odečíst
	- součet vynásobíme a vydělíme $\lVert h\rVert$
	- tím dostaneme $\mu(h)$ a zjistíme, že limití k nule
- vázané extrémy
	- znění
		- mějme funkce $f,g_1,\dots,g_k$ definované na otevřené množině $D\subseteq\mathbb E_n$, přičemž $g_i$ určují oblast (jsou tam rovny nule), kde hledáme extrémy funkce $f$
		- požadujeme spojité parciální derivace všech funkcí
		- mějme matici $M_{ij}=\frac{\partial g_i}{\partial x_j}$ s maximální hodností ($k$) v každém bodě oboru $D$
		- jestliže $f$ nabývá lokálního extrému, tak existují lambdy takové, že pro $i$ od jedné do $n$ platí $\frac{\partial f(a)}{\partial x_i}+\sum_{j=1}^k\lambda_j\cdot\frac{\partial g_j(a)}{\partial x_i}=0$
	- vezmeme regulární čtvercovou podmatici z $M$ s rozměry $k\times k$ (BÚNO zleva)
	- pomocí $g_i$ a věty o implicitních funkcích dostaneme $k$ funkcí v $n-k$ proměnných (při aplikaci používáme prvních $k$ proměnných jako $y$ a zbylých $n-k$ proměnných jako $x$)
	- těmi nahradíme prvních $k$ proměnných v $f$, čímž dostaneme funkci $F$ v $n-k$ proměnných, jejíž parciální derivace musí být nulové, aby tam byl extrém
	- použijeme chain rule na derivaci $F$ a na derivaci všech $g_i$, budeme to potřebovat v dalším kroku
	- z regularity $M$ (nenulovosti determinantu) vidíme, že rovnice s lambdami funguje pro prvních $k$ sloupců, ale musíme to ještě dokázat pro zbylých $n-k$
	- dosadíme výrazy, které nám vyšly z chain rule
	- nakonec nám tam vyleze rovnice s lambdami, která je nulová, takže se celý výraz sečte na nulu
- Lagrangeova věta ve více proměnných
	- znění: $f(y)-f(x)=\sum_j\frac{\partial f(x+\theta(y-x))}{\partial x_j}(y_j-x_j)$
	- položíme $F(t)=f(x+t(y-x))$
	- to zderivujeme pomocí chain rule
	- zjevně $f(x)=F(0)$ a $f(y)=F(1)$
	- použijeme Lagrangeovu větu na $f(y)-f(x)=F(1)-F(0)=F'(\theta)(1-0)=F'(\theta)$
- Lebesgueův integrál
	- zásadní: pro funkce omezené $K$ platí $\lim\int f=\int\lim f$
	- když existuje Riemannův integrál, tak je stejný jako Lebesgueův
	- když existuje integrál pro jednotlivé množiny, tak existuje pro jejich sjednocení
	- když existuje integrál pro každou funkci v posloupnosti a posloupnost je monotónní, tak limita integrálů je integrál limity
	- když jsou funkce posloupnosti omezeny funkcí s konečným integrálem a jejich integrál existuje, tak je integrál limity limita integrálů
