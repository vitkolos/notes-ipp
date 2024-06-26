# Pravděpodobnost a statistika

- Definice: Prostor jevů, pravděpodobnost, pravděpodobnostní prostor
	- $\Omega$ … prostor všech možných výsledků
		- u hrací kostky $\Omega=\set{1,\dots,6}=[6]$
	- $\mathcal F$ … prostor jevů (event space)
		- $\mathcal F\subseteq\mathcal P(\Omega)$
		- množiny, které nás zajímají
		- $\mathcal F=\mathcal P(\Omega)$ jde jen pro $|\Omega|\leq |\mathbb N|$
	- $\mathcal F\subseteq\mathcal P(\Omega)$ je prostor jevů, pokud…
		- $\emptyset,\Omega\in\mathcal F$
		- $A\in\mathcal F\implies A^C=\Omega\setminus A\in\mathcal F$
		- $A_1,A_2,\ldots\in\mathcal F\implies\bigcup A_i\in \mathcal F$
	- pozorování
		- $A_1,A_2\in\mathcal F\implies A_1\cup A_2\in\mathcal F$ (z 3. bodu definice, všechny ostatní množiny nekonečného sjednocení jsou prázdné)
		- $A_1,A_2\in\mathcal F\implies A_1\cap A_2\in\mathcal F$
			- jelikož $A_1\cap A_2=(A_1^C\cup A_2^C)^C\in\mathcal F$
	- $P:\mathcal F\to[0,1]$ je pravděpodobnost, pokud…
		- $P(\Omega)=1$
		- $P(\bigcup A_i)=\sum P(A_i)$ pro $A_1,A_2,\ldots\in \mathcal F$ po dvou disjunktní
	- pozorování
		- $P(\emptyset)=0$
		- $P(A_1\cup A_2)=P(A_1)+P(A_2)$
	- jistý jev … $P(A)=1$
	- nemožný jev … $P(A)=0$
		- u reálného terče je pravděpodobnost, že trefím konkrétní bod, rovna nule
			- takže neplatí implikace $P(A)=0\implies A=\emptyset$
	- pravděpodobnostní prostor … $(\Omega,\mathcal F,P)$
		- příklad: spojitý pravděpodobnostní prostor
			- $\Omega\subseteq\mathbb R^d$
			- $f:\Omega\to[0,\infty)$
			- $P(A)=\int_A f$
			- musí platit $\int_\Omega f=1$
- Věta: Základní vlastnosti jevů
	- $P(A)+P(A^C)=1$
		- $\Omega=A\cup A^C$
		- $1=P(\Omega)=P(A)+P(A^C)$
			- lze použít, protože $A\cup A^C=\emptyset$
	- …
- Podmíněná pravděpodobnost
	- …

---

- diskrétní náhodné veličiny
	- příklad: dva hody kostkou
		- zajímá nás součet
		- 1. varianta – pravděpodobnostní prostor budou součty
			- jednotlivé pravědpodobnosti jsou různé
		- lepší varianta – uspořádané dvojice, co na kostkách může padnout
			- uniformní prostor
			- $X(\omega)=\omega_1+\omega_2$ … příklad náhodné veličiny
			- $Y(\omega)=\omega_1\cdot\omega_2$
	- df: pro $(\Omega,\mathcal F,P)$ pravděpodobnostní prostor je $X$ diskrétní náhodná veličina $\equiv$ $X:\Omega\to\mathbb R\land \text{Im}(X)$ je konečný spočetný $\land$ ještě jedna podmínka
	- Im je obor hodnot
- …
- poznámka: náhodná veličina $X$ nám určí pravděpodobnostní prostor
	- $\Omega'=\text{Im}(X)$
	- $\mathcal F'=\mathcal P(\Omega')$
	- $p(x)=P(X=x)$
	- tomu se říká distribuce $X$
	- $p=p_X$
		- pravděpodobnostní funkce $X$
		- probability mass function … pmf $X$
- pozorování: $\sum_{x\in\text{Im}(X)}p_X(x)=1$
- příklady diskrétní náhodné veličiny
	- Bernoulliho rozdělení/distribuce
		- $X=1$ s pravděpodobností $p$
		- $X=0$ s pravděpodobností $1-p$
		- $p_X(1)=p$
		- $p_X(0)=1-p$
		- $X\sim\text{Ber}(p)$
	- indikátorová náhodná veličina
		- jev $A\in\mathcal F$
		- $\omega\in A$
		- $I_A(\omega)=1$, pokud $\omega\in A$
		- $I_A(\omega)=0$, pokud $\omega\notin A$
		- $I_A\sim\text{Ber}(P(A))$
	- geometrické rozdělení – „čas úspěchu“
		- házíme kostkou
		- $X$ … kolikátým hodem padla první šestka
		- $p=\frac16$
		- $P(X=1)=p$
		- $P(X=k)=(1-p)^{k-1}\cdot p$
		- takové veličině se říká geometrická, značí se $X\sim\text{Geo}(p)$
	- binomické rozdělení
	- Poissonovo rozdělení
- střední hodnota – $\mathbb E$xpectation
	- $X$ je diskrétní náhodná veličina
	- $\mathbb EX=\sum_{x\in\text{Im}X} x\cdot P(X=x)$
	- pokud má $\sum$ smysl
	- tedy pokud $\sum |x|\cdot p(x)\leq\infty$
- pozorování: pokud $\Omega$ je konečný/diskrétní
	- $\mathbb EX=\sum_{\omega\in\Omega} X(\omega)\cdot P(\set{\omega})$

---

- kdy nás zajímá střední hodnota?
	- pro opakované jevy
- survival function, funkce přežití … $s(t)=P(X\gt t)$
- věta
	- $X$ je diskrétní náhodná veličina, $\text{Im}\,X\subseteq\set{0,1,2,\dots}$
	- $\mathbb EX=\sum_{n=0}^\infty P(X\gt n)$
- důkaz
	- $\mathbb EX=1p(1)+2p(2)+3p(3)+\dots$
	- $=p(1)+p(2)+p(3)+\dots$
		- $P(X\gt 0)$
	- $+\,p(2)+p(3)+\dots$
		- $P(X\gt 1)$
	- $+\,p(3)+\dots$
- pozorování
	- pro $A\subseteq\mathbb R$
	- $P(X\in A)=\sum_{a\in A} p_X(a)$
- příklad
	- $X\sim\text{Geo}(p)$
	- $\mathbb EX=\sum_n P(X\gt n)=\sum_n(1-p)^n=\frac1{1-(1-p)}=\frac1p$
- df: rozptyl náhodné veličiny $X$
	- $\text{Var}(X)=\mathbb E((X-\mathbb EX)^2)$
	- $\sigma_X=\sigma(X)=\sqrt{\text{Var}(X)}$
	- $cv=\frac{\sigma_X}{\mathbb EX}$ … variační koeficient
- věta: $\text{Var}(X)=\mathbb E(X^2)-(\mathbb E(X))^2=\mathbb EX(X-1)+\mathbb EX-\mathbb E(X)^2$
- důkaz
	- $\mu:=\mathbb EX$
	- $\text{Var}(X)=\mathbb E((X-\mu)^2)=\mathbb E(X^2-2\mu X+\mu^2)=\mathbb E(X^2)-2\mu\mathbb EX+\mathbb E\mu^2=$
	- $=E(X^2)-2\mathbb\mu^2+\mu^2=\mathbb E(X^2)-\mu^2$
	- $\mathbb E(X^2-X)=\mathbb E(X(X-1))=\mathbb E(X^2)-\mathbb EX$
- příklad
	- $X\sim\text{Ber}(p)$
	- …
- …

## Náhodné vektory

- příklad – dva hody kostkou
- df: sdružená pravděpodobnostní funkce (joint pmf)
	- $p_{X,Y}(x,y)=P(X=x\land Y=y)$
- z $p_{X,Y}$ lze odvodit $p_X$ a $p_Y$
- ale z $p_X,p_Y$ nelze odvodit $p_{X,Y}$
- věta
	- $p_X(x)=\sum_{y\in\text{Im}\, Y}p_{X,Y}(x,y)$
	- podobně pro $p_Y(y)$
- důkaz
	- je to disjunktní sjednocení, takže sčítám pravděpodobnosti
- věta – PNS pro vektory

## Statistika

- boxplot
	- čára uvnitř krabice – medián
	- krabice pod čárou – 1. kvartil
	- krabice na čárou – 3. kvartil
	- celá krabice … IQR (interquartile range)
	- čáry mimo krabici – ve vzdálenosti 1.5×IQR
		- nebo tam, kde jsou nejvzdálenější hodnoty (tedy můžou mimo čáry, ale čáry nebudou sahat mimo data)
- spojitá křivka → je to nějaká fikce
- postup
	- máme populaci $\Omega$
	- zajímá nás parametr $\theta$ (nebo $\vartheta$)
	- $\Theta$ … množina všech parametrů
	- provedeme měření
	- měření může být zavádějící, vzorek musí být reprezentativní
	- $X_1,\dots,X_n\sim F$ náhodný výběr z rozdělení s distribucí $F$
		- nezávislé stejně rozdělené náhodné veličiny
		- $\forall i:F$ je distribuční funkce $X_i$
	- realizace
	- naměřená data $x_1,\dots,x_n$
	- $x_i=X_i(\omega)$ … naměřená hodnota náhodné veličiny $X_i$
- neparametrická statistika … malé předpoklady na $F$
- parametrická statistika … $F$ je z množiny rozdělení popsané parametrem $\theta$
	- například
		- $\text{Exp}(\lambda)$ s parametrem $\theta=\lambda$
		- $U(0,a)$ s parametrem $\theta=a$
		- $N(\mu,\sigma^2)$ s parametrem $\theta=(\mu,\sigma^2)$
- příklad
	- náhodný výběr $X_1,\dots,X_n$ doby běhu programu
	- $p=P(X_i\gt 100\text{ ms})$
	- data $x_1,\dots,x_n\in\mathbb R^+$
		- $x_i$ … realizace
	- statistika … funkce naměřených dat
		- $t(x_1,\dots,x_n)$ … číslo (estimate)
		- $T(X_1\dots,X_n)$ … náhodná veličina (estimator)
	- 1. možnost odhadu
		- $\frac{|\set{i:x_i\gt 100}|}{n}$ = $\hat p$ … odhad $p$
	- 2. možnost
		- $X_i\sim N(\mu,\sigma^2)$
	- $P(X_i\gt 100)=1-P(X_i\lt 100)=1-\Phi(\frac{100-\mu}{\sigma})$ pokud $X_i\sim N(\mu,\sigma^2)$
	- $\hat\mu=\overline{X_n}=\frac{X_1+\dots+X_n}n$ … výběrový průměr – příklad statistiky
	- $\widehat{\sigma^2}=\frac1{n-1}\sum_{i=1}^n(X_i-\overline{X_n})^2$ … výběrový rozptyl
	- $\hat\sigma =\sqrt{\widehat{\sigma^2}}=\hat S_n$

### Bodový odhad

- $\hat\theta$ … odhad parametru $\theta$ – je to náhodná veličina závislá na měření (statistika)
- $\text{bias}(\hat\theta)=\mathbb E(\hat\theta-\theta)$
	- vychýlení
- $\hat\theta$ je nevychýlený/unbiased
	- $\text{bias}(\hat\theta)=0$
	- $\mathbb E(\hat\theta)=\theta$
- asymptoticky nevychýlený
	- $\text{bias}(\hat\theta)\to 0$
- $\hat\theta_n$ je konzistentní odhad $\theta\iff\hat\theta_n\xrightarrow{p}\theta$
- $\forall\epsilon\gt0:P(|\hat\theta_n-\theta|\gt\varepsilon)\to0$
- příklad
	- zákon velkých čísel
	- $\overline{X_n}$ je konzistentní odhad $\mathbb EX$
	- $\text{MSE}(\hat\theta)=\mathbb E(\hat\theta-\theta)^2$
		- MSE … mean squared error (střední kvadratická odchylka)
- věta: $\text{MSE}(\hat\theta)=\text{bias}(\hat\theta)^2+\text{var}(\hat\theta)$
- důkaz
	- $\text{var}(X)=\mathbb EX^2-(\mathbb EX)^2$
	- $\text{var}(\hat\theta)=\text{var}(\hat\theta-\theta)=\mathbb E(\hat\theta-\theta)^2-[\mathbb E(\hat\theta-\theta)]^2=\text{MSE}(\hat\theta)-\text{bias}(\hat\theta)^2$
- věta
	- $\overline{X_n}=\frac1n\sum_{i=1}^n X_i$
	- $\widehat{S_n^2}=\frac1{n-1}\sum_{i=1}^n(X_i-\overline{X_n})^2$
	- $\to \overline{X_n}$ je konzistentní nevychýlený odhad $\mu$
	- $\to \widehat{S_n^2}$ je konzistentní nevychýlený odhad $\sigma^2$
	- důkaz odložíme
- jak hledat odhady?
	- metoda momentů
		- $r$-tý moment $X:\mathbb EX^r=m_r(\theta)$
			- závislé na neznámém parametru
		- $r$-tý výběrový moment $\frac1n\sum_{i=1}^nX_i^r=\widehat{m_r(\theta)}$
			- dobrý odhad pro $r$-tý moment $X$
			- náhodná veličina závislá na měření
		- …
	- metoda maximální věrohodnosti (MV, maximal likelihood ML)
		- $\hat\theta_{ML}=\text{argmax}_\theta\;p(x;\theta)$
			- $\text{argmax}_\theta\;f(x;\theta)$
			- abych se nemusel rozhodovat mezi $p$ a $f$, budu používat $L$
		- …
- testy
	- 1-výběrový
	- 2-výběrový
	- párový
- lineární regrese
	- $x_i$ … nezávislá proměnná, predictor
	- $y_i$ … závislá proměnná, response
	- cíl … $y=\theta_0+\theta_1x$
		- $\theta_0$ … intercept
		- $\theta_1$ … slope
	- chybu měříme pomocí kvadratické odchylky $\sum_{i=1}^n(y_i-(\theta_0+\theta_1x_i))^2$
	- řešení
		- $\hat\theta_1=\frac{cov(x,y)}{var(x)}$
		- $\hat\theta_0=\bar y-\theta_1\bar x$
	- zavádějící proměnná (confounding variable) – není v datech, ale kdybychom ji přidali, všechno by dávalo větší smysl
	- Simpsonův paradox – jedna strana vítězí v jednotlivých kategoriích, ale dohromady vítězí ta druhá
	- neparametrická statistika
		- empirická distribuční funkce
	- frekventistická vs. bayesovská statistika
	- generování náhodných veličin
		- uniformní rozdělení $U(0,1)$ – dejme tomu, že ho máme (je těžké ho generovat)
		- diskrétní náhodná veličina – uděláme rozklad intervalu od nuly do jedné tak, aby $P(X=i)=|A_i|$, kde $|A_i|$ je část intervalu
		- inverzní transformace
			- $Q_X(p)=F_X^{-1}(p)$ pro $X$ spojitou
			- $Q_X=\min\set{x:F_X(x)\geq p}$
			- věta: $F^{-1}(U)$ má distribuční funkci $F$
				- kde $U\sim U(0,1)$
		- rejection sampling
			- generujeme uniformně náhodně bod $(x,y)$ pod křivkou $f_X$
			- pak $x$ má hustotu $f_X$
