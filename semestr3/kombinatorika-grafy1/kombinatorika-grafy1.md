# Kombinatorika a grafy 1

## Odhady na kombinatorické funkce

- $n!=\prod_{i=1}^ni$
- lemma: $n^{n/2}\leq n!\leq n^n$
	- horní odhad jednoduchý
	- dolní odhad
		- součin prvního a posledního, druhého a předposledního, … prvku součinu faktoriálu je vždy $\geq n$
		- aby byl počet činitelů faktoriálu sudý, použijeme $(n!)^2$
		- takže $(n!)^2=\prod_{i=1}^n(i\cdot(n+1-i))\geq n^n$
		- proto $n!\geq n^{n/2}$
		- to, že $i(n+1-i)\geq n$, lze dokázat graficky pomocí funkce $f(x)=x(n+1-x)$
	- důsledek $\sqrt n\leq \sqrt[n]{n!}\leq n$
	- $\sqrt[n]{n!}$ se chová trochu jako $\frac n2$
- věta: $e(\frac ne)^n\leq n!\leq en(\frac ne)^n$
	- u zkoušky můžeme použít libovolný korektní důkaz (obecně u všech vět)
	- důkaz 1: indukcí s využitím $e^x\geq 1+x$
	- důkaz 2: odhad pomocí integrálu $\ln(n!)=\sum_{i=1}^n\ln(i)=\sum_{i=2}^n\ln(i)$
		- schodovitá plocha, kde schod má šířku 1 a výšku $\ln(i)$ má obsah daný uvedeným součtem
		- obsah schodovité plochy je zdola odhadnutý obsahem plochy pod křivkou logaritmu
		- $\ln(n!)\geq\int_1^n\ln(x)\,dx=[x\ln(x)-x]^n_1=(n\ln n-n+1)=:I_n$
		- $n!\geq e^{I_n}=e^{n\ln n-n+1}=e(\frac ne)^n$
		- obdobně dolní odhad
			- $\ln((n-1)!)\leq I_n$
			- $e^{I_n}\geq(n-1)!\implies n\cdot e^{I_n}\geq n!\implies n\cdot e(\frac ne)^n\geq n!$
	- důkaz 3: jen $(\frac ne)^n\leq n!$
		- víme z analýzy, že $e^x=1+x+\frac{x^2}{2}+\frac{x^3}{3!}+\dots+\frac{x^k}{k!}+\dots=\sum^\infty_{k=0}\frac{x^k}{k!}$
		- pro $x\geq 0:e^x\geq\frac {x^n}{n!}$ (protože Taylorova řada určitě někde obsahuje $x^n\over n!$)
		- tedy $n!\geq \frac{x^n}{e^x}\implies n!\geq \frac{n^n}{e^n}=(\frac ne)^n$ (platí to pro libovolné $x\geq 0$, takže dosadíme $x=n$)
- kombinační číslo ${n\choose k}=\frac{n!}{k!(n-k)!}=\frac{n\cdot(n-1)\cdots(n-k+1)}{k\cdot(k+1)\cdots1}$
	- jeho odhad…
- pozorování: ${n\choose k}={n\choose n-k}$
- ${2m\choose m}$
- fakt: kombinační čísla v jednom řádku Pascalova trojúhelníku zleva doprava do poloviny rostou, od poloviny klesají
- fakt: $\sum_{k=0}^n{n\choose k}=2^n=(1+1)^n$
- pozorování: $\frac{2^{2m}}{2m+1}\leq{2m\choose m}\leq 2^{2m}$
- věta: $\forall m\in\mathbb N:\frac{2^{2m}}{2\sqrt{m}}\leq {2m\choose m}\leq {2^{2m}\over\sqrt{2m}}$
- důkaz
	- definujme $P:=\frac{2m\choose m}{2^{2m}}$ a dokažme $\frac1{2\sqrt{m}}\leq P\leq \frac{1}{\sqrt{2m}}$
	- …

## Vytvořující (generující) funkce

- definice: vytvořující funkce posloupnosti $(a_n)_{n=0}^\infty$ reálných čísel je funkce proměnné $x$ definovaná jako součet $f(x)=\sum_{n=0}^\infty a_n(x^n)$
	- tato funkce nemusí být dobře definovaná pro všechna reálná čísla (dokonce se může stát, že nebude definovaná pro žádné reálné číslo kromě nuly)
	- pro nás bude praktické, když bude definovaná na okolí nuly (více než jednobodovém)
- fakt: pokud existuje $K\gt 0$ taková, že $\forall n:|a_n|\leq K^n$ (posloupnost se dá shora odhadnout nějakou exponenciální funkcí), tak řada $\sum_{n=0}^\infty a_nx^n$ konverguje na $(-\frac 1K,\frac 1K)$ absolutně stejnoměrně
- navíc má $f(x)=\sum_{n=0}^\infty a_nx^n$ derivace všech řádů na $(-\frac 1K,\frac 1K)$, které se dají spočítat „derivováním člen po členu“
	- $f'(x)=\sum_{n=0}^\infty a_nnx^{n-1}$
	- $f''(x)=\sum_{n=0}^\infty a_nn(n-1)x^{n-2}$
	- $f(x)=a_0+a_1x+a_2x^2+a_3x^3+\dots$
	- $f'(x)=a_1+2a_2x+3a_3x^2+\dots$
	- $f''(x)=2a_2+3\cdot 2a_3+\dots$
	- $f^{(n)}(x)=n!\cdot a_n+\dots$
- důsledek
	- $f(0)=a_0$
	- $f'(0)=a_1$
	- $f''(0)=2a_2$
	- $f^{(n)}(0)=n!\cdot a_n$
	- takže $a_n=\frac{1}{n!} f^{(n)}(0)$
- fakt: vytvořující funkce lze mezi sebou násobit jako polynomy, výsledek je vytvořující funkcí posloupnosti $a_0b_0,a_0b1+a_1b0,\dots$, této posloupnosti se říká konvoluce posloupností $(a_n)_{n=0}^\infty$ a $(b_n)_{n=0}^\infty$
- užití vytvořujících funkcí
	- 
