# Zkouška

## Definice

- definice funkce, funkce prostá, na a bijekce (př. 1)
	- funkce $f$ z množiny $A$ do množiny $B$ je každá taková uspořádaná trojice $(A,B,f)$, že $f\subset A\times B$ a pro každé $a\in A$ existuje právě jedno $b\in B$, že $afb$
		- píšeme, že $f:A\to B$ a že $f(a)=b$
	- funkce $f:X\to Y$ je prostá $\equiv f(x)=f(x')\implies x=x'$
	- funkce $f:X\to Y$ je na $\equiv f[X]=Y$
	- $f$ je bijekce (vzájemně jednoznačná) $\equiv f$ je na a je prostá
- supremum a infimum v lineárním uspořádání (př. 1)
	- $(A,\lt)$ buď lineární uspořádání a nechť $B\subset A$
	- prvky $\sup(B):=\min(H(B))$ a $\inf(B):=\max(D(B))$ v $A$, existují-li, nazveme supremem a infimem množiny $B$
		- $H(B)$ je množina horních mezí, tedy prvků $h\in A$ takových, že $\forall b\in B: b\leq h$
		- obdobně je $D(B)$ množina dolních mezí
- (nejvýše) spočetná a nespočetná množina (př. 1)
	- $X$ je nekonečná, když existuje prostá funkce $f:\mathbb N\to X$
	- $X$ je konečná, když není nekonečná
	- $X$ je spočetná, když existuje bijekce $f:\mathbb N\to X$
	- $X$ je nejvýše spočetná, je-li konečná nebo spočetná
	- $X$ je nespočetná, když není nejvýše spočetná
- vlastní a nevlastní limita posloupnosti, podposloupnost (př. 2)
	- nechť $(a_n)$ je reálná posloupnost a $L \in \mathbb R^*$
	- pokud $\forall\varepsilon\,\exists n_0\,(n\geq n_0\implies a_n\in U(L,\varepsilon))$, píšeme, že $\lim a_n=L$ nebo $\lim_{n\to\infty}a_n=L$ nebo $a_n\to L$, a řekneme, že posloupnost $(a_n)$ má limitu $L$
	- pro $L\in \mathbb R$ mluvíme o vlastní limitě a pro $l\in\pm\infty$ o limitě nevlastní
	- posloupnost mající vlastní limitu konverguje, jinak diverguje
- liminf a limsup posloupnosti (př. 3)
	- nechť $A\in \mathbb R^*$ a $(a_n)\subset\mathbb R$; řekneme, že $A$ je hromadný bod posloupnosti $(a_n)$, je-li limitou nějaké její podposloupnosti; $H(a_n)$ je množina těchto hromadných bodů
	- limes inferior a limes superior dané posloupnosti $(a_n)$ definujeme po řadě jako $\lim\inf a_n :=\min(H(a_n))$ a $\lim\sup a_n:=\max(H(a_n))$
- řada, částečný součet řady, součet řady (př. 3)
	- (nekonečnou) řadou rozumíme posloupnost $(a_n)\subset\mathbb R$
	- jejím součtem rozumíme limitu $\sum a_n=\sum_{n=1}^\infty a_n=a_1+a_2+\dots := \lim(a_1+a_2+\dots+a_n)$, když existuje
	- posloupnost $(a_1+a_2+\dots+a_n)$ sestává z takzvaných částečných součtů (řady)
	- má-li řada vlastní součet, pak konverguje, jinak diverguje
- geometrická řada a její součet, absolutně konvergentní řada (př. 4)
	- geometrické řady jsou řady $\sum_{n=0}^\infty q^n=1+q+q^2+\dots$ s parametrem $q\in\mathbb R$ zvaným kvocient
	- mějme částečný součet $s_n:=1+q+q^2+\dots+q^{n-1}$
		- $qs_n=q+q^2+q^3+\dots+q^n$
		- $s_n=1+q+q^2+\dots+q^{n-1}$
		- $qs_n-s_n=q^n-1$
		- $s_n=\frac{q^n-1}{q-1}=\frac 1{1-q}+\frac{q^n}{q-1}$
		- pak stačí určit $\lim s_n$ pro dané $q$
	- $\sum^\infty_{n=0}q^n=\begin{cases} +\infty & \text{pro }q\geq 1 \\ \frac{1}{1-q} & \text{pro }|q|\lt 1 \\ \text{neexistuje} & \text{pro }q\leq -1 \end{cases}$
	- řada $\sum a_n$ je absolutně konvergentní, konverguje-li řada $\sum |a_n|$
- limita funkce, jednostranná limita funkce (př. 4 a 5)
	- limita
		- nechť $A,L\in\mathbb R^*,\,M\subset\mathbb R,\,A$ je limitní bod množiny $M$ a $f:M\to\mathbb R$ je funkce
		- pokud $\forall\varepsilon\,\exists\delta:f[P(A,\delta)\cap M]\subset U(L,\varepsilon)$, píšeme $\lim_{x\to A}f(x)=L$ a řekneme, že funkce $f$ má v $A$ limitu $L$
	- limita zleva (obdobně zprava)
		- nechť $A,L\in\mathbb R^*,\,M\subset\mathbb R,\,A$ je levý limitní bod množiny $M$ a $f:M\to\mathbb R$ je funkce
		- pokud $\forall\varepsilon\,\exists\delta:f[P^-(A,\delta)\cap M]\subset U(L,\varepsilon)$, píšeme $\lim_{x\to A^-}f(x)=L$ a řekneme, že funkce $f$ má v bodě $A$ limitu zleva rovnou $L$
- exponenciála, logaritmus, kosinus a sinus (př. 4)
	- pro každé $x\in\mathbb R$ položíme $e^x=\exp(x):=\sum_{n=0}^\infty\frac{x^n}{n!}=1+x+{x^2\over 2}+{x^3\over 6}+\dots:\mathbb R\to \mathbb R$
	- $\log := \exp^{-1}:(0,+\infty)\to\mathbb R$
	- $\forall t\in\mathbb R$ nechť $\cos t:=\sum_{n=0}^\infty\frac{(-1)^nt^{2n}}{(2n)!}$ a $\sin t:=\sum_{n=0}^\infty\frac{(-1)^nt^{2n+1}}{(2n+1)!}$
- spojitost funkce v bodě, jednostranná spojitost funkce v bodě (př. 5)
	- nechť 
- asymptotické symboly $O,\,o,\,\sim$ (př. 5)
- kompaktní, otevřená, uzavřená množina (př. 6)
- globální, lokální a ostré extrémy funkce (př. 6)
- derivace funkce, jednostranná derivace funkce (př. 7)
- standardní definice tečny (d. 9, př. 7)
- derivace vyšších řádů (d. 8, př. 8)
- (ryze) konvexní a konkávní funkce (d. 10, př. 8)
- inflexní bod (d. 14, př. 8)
- svislé asymptoty a asymptoty v nekonečnu (př. 8)
- Taylorův polynom funkce (d. 1, př. 9), Taylorova řada funkce (d. 5, př. 9)
- primitivní funkce (d. 8, př. 9)
- stejnoměrná spojitost (d. 19, př. 6)
- (nevlastní) Newtonův integrál funkce (d. 7, př. 10 a d. 1, př. 11)
- Riemannův integrál (d. 1, př. 12) a množina míry 0 (d. 11, př. 12)
- Henstock-Kurzweilův integrál (d. 11, př. 13)
- délka grafu funkce, plocha mezi grafy, objem rotačního tělesa (př. 14)

## Věty bez důkazů



## Věty s důkazy


