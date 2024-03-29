# Pravděpodobnost a statistika

- aplikace pravděpodobnosti
	- $f,g$ polynomy stupně $d$
	- test $f=g$?
- $\Omega$ … prostor všech možných výsledků
	- u hrací kostky $\Omega=\set{1,\dots,6}=[6]$
	- u hodu 3 kostkami $\Omega=[6]\times[6]\times[6]$
	- u hodu $\infty$ kostkami $\Omega=$ množina nekonečných posloupností čísel z $[6]$
	- u hodu na terč … je to ten terč $\subseteq\mathbb R^2$
	- u doby běhu programu … $[0,\infty]$
	- u počtu osob na přednášce … $\mathbb N_0$
- $\mathcal F$ … prostor jevů (event space)
	- $\mathcal F\subseteq\mathcal P(\Omega)$
	- množiny, které nás zajímají
	- $\mathcal F=\mathcal P(\Omega)$ jde jen pro $|\Omega|\leq |\mathbb N|$
- df: $\mathcal F\subseteq\mathcal P(\Omega)$ je prostor jevů, pokud…
	- $\emptyset,\Omega\in\mathcal F$
	- $A\in\mathcal F\implies A^C=\Omega\setminus A\in\mathcal F$
	- $A_1,A_2,\dots\in\mathcal F\implies\bigcup A_i\in F$
- …
- df: pravděpodobnost
- df: pravděpodobnostní prostor
- u reálného terče je pravděpodobnost, že trefím konkrétní bod, rovna nule
	- takže neplatí implikace $P(A)=0\implies A=\emptyset$
- příklad: spojitý pravděpodobnostní prostor
	- $\Omega\subseteq\mathbb R^d$
	- $f:\Omega\to[0,\infty)$
	- $P(A)=\int_A f$
	- musí platit $\int_\Omega f=1$

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
