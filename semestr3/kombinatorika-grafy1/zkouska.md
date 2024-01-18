# Zkouška

Kromě uvedených [pojmů](#pojmy) a [tvrzení](#tvrzení) se u zkoušky můžete setkat i s počítacími nebo teoretickými příklady.

## Pojmy

U následujících pojmů byste měli umět zformulovat definici a na jednoduchém příkladu ukázat, že té definici rozumíte.

- vytvořující funkce
	- vytvořující funkce posloupnosti $(a_n)_{n=0}^\infty$ reálných čísel je funkce proměnné $x$ definovaná jako součet $f(x)=\sum_{n=0}^\infty a_nx^n$
- Catalanova čísla
	- binární strom je zakořeněný strom, jehož každý vnitřní vrchol má 2 potomky, na pořadí potomků záleží
	- $C_n$ … počet binární stromů s $n$ vnitřními vrcholy
	- $(C_n)_{n=0}^\infty$ jsou Catalanova čísla
	- rekurentní tvar
		- $C_0=1$
		- $C_{n+1}=\sum_{i=0}^n C_iC_{n-i}$ pro $n\gt 0$
	- explicitní vzorec: $C_n=\frac1{n+1}{2n\choose n}$
- projektivní rovina
	- projektivní rovina je hypergraf $(X,\mathcal P)$ takový, že platí tři axiomy:
	- A1: $(\forall x,y\in X,\;x\neq y)(\exists! p\in\mathcal P):\set{x,y}\subseteq p$
		- dva různé body určují právě jednu přímku
	- A2: $\forall p,q\in\mathcal P,\;p\neq q:|p\cap q|=1$
		- každé dvě přímky mají jeden průsečík
	- A3: $(\exists Č\subseteq X,\;|Č|=4)(\forall p\in\mathcal P):|p\cap Č|\leq 2$
		- existuje množina čtyř bodů „v obecné poloze“ (žádné tři z nich neleží na přímce)
	- prvky $X$ … body
	- prvky $\mathcal P$ … přímky
- řád konečné projektivní roviny
	- KPR má řád $n\in\mathbb N$, pokud každá její přímka má $n+1$ bodů
	- tedy řád KPR := velikost přímky – 1
- hypergraf
	- hypergraf je dvojice $(V,H)$, kde $H$ je množina podmnožin $V$, tj. $H\subseteq\mathcal P(V)$
- incidenční graf hypergrafu
	- graf incidence hypergrafu $(V,H)$ je bipartitní graf s partitami $V$ a $H$, kde mezi $x\in V$ a $h\in H$ vede hrana $\iff x\in h$
- dualita projektivních rovin
	- mějme projektivní rovinu $(X,\mathcal P)$; potom duální projektivní rovina k $(X,\mathcal P)$ je hypergraf $(X^*,\mathcal P^*)$, kde
		- $X^*=\mathcal P$,
		- pro $x\in X$ definujme $x^*\coloneqq\set{p\in\mathcal P:x\in p}$
			- $x^*$ … přímky, které procházejí $x$
		- $\mathcal P^*=\set{x^*\mid x\in X}$
	- v podstatě obrátíme incidenční graf
- toková síť
	- tokovou síť tvoří
		- $V$ … množina vrcholů
		- $E$ … množina orientovaných hran, $E\subseteq V\times V$
		- $z\in V$ … zdroj
		- $s\in V\setminus\set{z}$ … spotřebič / stok
		- $c:E\to [0,+\infty)$ … $c(e)$ je kapacita hrany $e$
	- definice umožňuje mít hrany oběma směry, připouští také smyčky, ty však z hlediska toků v sítích nejsou nijak užitečné
	- poznámka: ze stoku může vycházet orientovaná hrana, podobně do zdroje může vést hrana
- tok
	- tok v síti $(V,E,z,s,c)$ je funkce $f:E\to[0,+\infty)$ splňující
		- $\forall e\in E:0\leq f(e)\leq c(e)$
		- $\forall x\in V\setminus \set{z,s}:$ součet toků do vrcholu $x$ se rovná součtu toků z vrcholu (formálně pomocí sum) … Kirchhoffův zákon
- velikost toku
	- velikost toku $f$ v síti $(V,E,z,s,c)$ je $w(f)\coloneqq f[\text{Out}(z)]-f[\text{In}(z)]$
	- kde Out(z) a In(z) jsou množiny hran do, respektive ze zdroje a $f[A]\coloneqq\sum_{e\in A}f(e)$ pro $A\subseteq E$
- maximální tok
	- maximální tok je tok, který má největší velikost
- řez v síti
	- řez v síti $(V,E,z,s,c)$ je množina hran $R\subseteq E$ taková, že každá orientovaná cesta ze $z$ do $s$ obsahuje aspoň jednu hranu $R$
- kapacita řezu
	- kapacita řezu $R$ … $c(R)=\sum_{e\in R}c(e)$
- elementární řez
	- $E(A,B)\coloneqq E\cap (A\times B)$
	- tedy $E(A,B)=\set{uv\in E\mid u\in A\land v\in B}$
	- elementární řez je $E(A,B)$ pro $A\subseteq V,\;B=V\setminus A$
		- přičemž $z\in A,\;s\in B$
- minimální řez
	- minimální řez je řez, který má ze všech řezů nejmenší kapacitu
- nenasycená a zlepšující cesta
	- nenasycená cesta pro $f$ je neorientovaná cesta $x_1e_1x_2e_2\dots x_ke_kx_{k+1}$, kde $\forall i:$ buď $e_i=(x_i,x_{i+1})$ ($e_i$ je dopředná hrana), nebo $e_i=(x_{i+1},x_i)$ ($e_i$ je zpětná hrana) a navíc platí
		- pro každou dopřednou hranu $e_i$ platí $f(e_i)\lt c(e_i)$
		- pro každou zpětnou hranu $e_i$ platí $f(e_i)\gt 0$
	- zlepšující cesta pro $f$ je nenasycená cesta ze $z$ do $s$
- párování v grafu
	- párování v grafu $G=(V,E)$ je množina hran $M\subseteq E$ taková, že žádný vrchol nepatří do více než jedné hrany $M$
- vrcholové pokrytí v grafu
	- vrcholové pokrytí v $G=(V,E)$ je množina vrcholů $C\subseteq V$ taková, že každá hrana obsahuje aspoň 1 vrchol z $C$
- systém různých reprezentantů v hypergrafu
- hranový a vrcholový řez v grafu
- hranová a vrcholová souvislost grafu
- hranově a vrcholově k-souvislý graf
- klika a nezávislá množina v grafu
- Hammingova vzdálenost a Hammingova váha
- minimální vzdálenost kódu
- $(n, k, d)$-kód
- lineární kód
- generující matice
- kódování
- dekódování
- duální kód
- kontrolní matice lineárního kódu
- Hammingovy kódy

## Tvrzení

U následujících tvrzení se očekává, že je budete umět zformulovat a (není-li uvedeno jinak) i dokázat.

- Odhady kombinatorických funkcí: $e(n/e)^n\leq n!\leq en(n/e)^n$, $(n/k)^k\leq{n\choose k}\leq(en/k)^k$, $\frac{2^{2m}}{2\sqrt m}\leq{2m\choose m}\leq\frac{2^{2m}}{\sqrt{2m}}$
- Odvození vytvořující funkce pro rekurentně zadanou posloupnost
- Zobecněná binomická věta
- Rozklad racionální funkce na parciální zlomky (bez důkazu) a jeho využití při práci s vyvořujícími funkcemi
- Odvození vzorečku pro Catalanova čísla, definovaná jako počet binárních zakořeněných stromů
- Odvození vlastností konečných projektivních rovin: počet bodů, počet přímek, počet bodů v jedné přímce, počet přímek procházejících jedním bodem
- Duální projektivní rovina je opravdu projektivní rovina
- Konstrukce projektivních rovin z konečných těles
- Existence maximálního toku v obecné síti (bez důkazu)
- Charakterizace maximálního toku pomocí neexistence zlepšující cesty a pomocí řezu odpovídající kapacity; minimaxová věta o toku a řezu
- Fordův–Fulkersonův algoritmus, jeho důsledek pro celočíselnost maximálního toku a pro existenci maximálního toku v síti s racionálními kapacitami
- Souvislost mezi velikostí největšího párování a nejmenšího vrcholového pokrytí v obecném grafu
- Kőnigova–Egerváryho věta
- Hallova věta v grafové a hypergrafové verzi
- Mengerovy věty pro hranovou a vrcholovou souvislost (Mengerova věta pro hranovou souvislost je též někdy označována jako „Fordova–Fulkersonova věta“)
- Lemma o uších pro 2-souvislé grafy
- Cayleyho vzorec pro počet stromů na n vrcholech
- Spernerova věta
- Počet hran v grafu bez C4
- Počítání dvěma způsoby (znalost obecného postupu)
- Ramseyova věta v grafové verzi a ve verzi pro barvení hran úplného grafu (i s více než dvěma barvami)
- Ramseyova věta pro hypergrafy v konečné a nekonečné verzi (bez důkazu)
- Kőnigovo lemma o nekonečné cestě ve stromě, jeho použití při odvození konečné Ramseyovy věty z nekonečné
- Použití generující matice ke kódování
- Použití kontrolní matice k ověření, zda je slovo kódové
- Souvislost minimální vzdálenosti kódu se sloupci kontrolní matice
- Konstrukce Hammingových kódů a jednoznačnost jejich dekódování
- Singletonův, Hammingův a Gilbertův–Varshamovův odhad na parametry kódů
