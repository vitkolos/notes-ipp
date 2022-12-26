# Zkouška

## Úvod

- Příklad: Technika důkazu indukcí a sporem
	- věta: Prvočísel je nekonečně mnoho.
	- důkaz sporem
		- kdyby $p_1,\dots,p_n$ byla všechna prvočísla
		- $\zeta := p_1\cdot p_2 \cdot \ldots\cdot p_n$
		- $(\zeta +1)\mod p_i=1 \implies \zeta + 1$ není dělitelné žádným prvočíslem a je větší než všechna $p_i\implies\zeta+1$ by také muselo být prvočíslo ↯
	- věta: $\forall n \in \mathbb N: 2^0+2^1+2^2+\dots+2^n=2^{n+1}-1$
	- důkaz indukcí podle n
		- $2^0=2^1-1$
		- indukční krok
			- IP: $2^0+2^1+2^2+\dots+2^n=2^{n+1}-1$
			- chceme: $2^0+2^1+2^2+\dots+2^n+2^{n+1}=2^{n+2}-1$
			- z IP: $2^{n+1}-1+2^{n+1}=2^{n+2}-1\quad \square$
- Definice: Operace s čísly: sumy, produkty, horní a dolní celá část
	- prázdná suma se rovná nule, prázdný produkt jedné
	- horní celá část se značí $\lceil x \rceil$, zaokrouhluje nahoru
	- dolní celá část se značí $\lfloor x \rfloor$, zaokrouhluje dolů
- Definice: Množinové operace: rovnost, inkluze, sjednocení, průnik, rozdíl, symetrická diference, potence (množina podmnožin), mohutnost (počet prvků)
	- symetrická diference $A\bigtriangleup B=(A\setminus B)\cup(B\setminus A)$
	- potence $2^A:=\lbrace B | B\subseteq A\rbrace$
- Definice: Uspořádané k-tice a kartézský součin
	- uspořádaná dvojice $(x,y)$
		- lze zavést pomocí klasických množin jako $\lbrace \lbrace x \rbrace, \lbrace x,y\rbrace\rbrace$
		- uspořádaná k-tice $(x_1,\dots,x_k)$
	- kartézský součin $A\times B:=\lbrace(a,b)|a\in A, b\in B \rbrace$
		- $A^k:=\underbrace{A\times A \times \dots \times A}_k$

## Relace

- Definice: Relace mezi množinami, relace na množině
	- (binární) relace mezi množinami $X,Y$ je podmnožina $X\times Y$
	- relace na množině $X$ je podmnožina $X^2$
	- značení – pro relaci $R$ mezi $X,Y:xRy \equiv (x,y)\in R$
- Příklad: Příklady relací: prázdná, univerzální, diagonální
	- prázdná $\emptyset$
	- univerzální $X\times Y$
	- diagonální $\Delta_X := \lbrace (x,x)|x\in X\rbrace$, např. rovnost $x=y$
- Definice: Operace s relacemi: inverze, skládání
	- inverze
		- k relaci $R$ mezi $X,Y$ lze definovat inverzní relaci $R^{-1}$ mezi $Y,X$, přičemž $R^{-1} := \lbrace(y,x)|(x,y)\in R\rbrace$
	- skládání
		- pro relaci $R$ mezi $X,Y$ a relaci $S$ mezi $Y,Z$ lze definovat složenou relaci $T=R\circ S$ mezi $X,Z$
		- $xTz \equiv \exists y \in Y: xRy \land ySz$
		- $R\circ \Delta_Y =R,\quad \Delta_X\circ R = R$
		- značení skládání funkcí: $(f\circ g)(x)=g(f(x))$
- Definice: Funkce (zobrazení) a jejich druhy: prosté (injektivní), na (surjektivní), vzájemně jednoznačné (bijektivní)
	- funkce z množiny X do množiny Y je relace A mezi X a Y t. ž. $(\forall x\in X)(\exists! y\in Y):xAy$
	- funkce $f:X\to Y$ je…
	- prostá (injektivní) $\equiv \nexists x,x' \in X: x \neq x' \land f(x)=f(x')$
	- na Y (surjektivní) $\equiv (\forall y \in Y)(\exists x \in X): f(x)=y$
	- vzájemně jednoznačná (bijektivní) $\equiv (\forall y \in Y)(\exists! x \in X):f(x)=y$
		- taková funkce je tedy prostá i „na“
		- k takové funkci existuje inverzní funkce $f^{-1}$ z Y do X
- Definice: Vlastnosti relací: reflexivita, symetrie, antisymetrie, transitivita
	- relace R na X je…
	- reflexivní $\equiv \forall x \in X: xRx$
		- $\Delta_X \subseteq R$
	- symetrická $\equiv \forall x,y \in X: xRy \implies yRx$
		- $R=R^{-1}$
	- antisymetrická $\equiv \forall x,y \in X: xRy \land yRx \implies x=y$
	- tranzitivní $\equiv \forall x,y,z \in X: xRy \land yRz \implies xRz$
		- $R\circ R \subseteq R$
- Definice: Ekvivalence, ekvivalenční třída, rozklad množiny
	- relace R na X je ekvivalence $\equiv$ R je reflexivní & symetrická & tranzitivní
		- např. rovnost čísel, rovnost mod K, geometrická podobnost
	- ekvivalenční třída prvku $x \in X:R[x]=\lbrace y \in X | xRy\rbrace$
	- množinový systém $\mathcal S\subseteq 2^X$ je rozklad množiny $X \equiv$
		- $\forall A \in \mathcal S: A \neq \emptyset$
		- $\forall A,B\in \mathcal S: A\neq B \implies A \cap B = \emptyset$
		- $\bigcup_{A\in \mathcal S}A=X$
- Věta: Vztah mezi ekvivalencemi a rozklady
	- věta
		- (1) $\forall x \in X: R[x]\neq \emptyset$
		- (2) $\forall x,y \in X:$ buď $R[x]=R[y]$, nebo $R[x] \cap R[y]=\emptyset$
		- (3) $\lbrace R[x] | x \in X\rbrace$ (množina všech ekvivalenčních tříd) určuje ekvivalenci R jednoznačně
	- důkaz
		- (1) ekvivalence je reflexivní, tedy nutně platí $x \in R[x]$, tudíž je ta ekvivalenční třída neprázdná
		- (2) dokážeme, že pokud nejsou disjunktní, tak se rovnají
			- platí $R[x]\cap R[y]\neq \emptyset$
			- dokazujeme $R[x]=R[y]$, stačí nám $R[x]\subseteq R[y]$ (opačnou inkluzi lze dokázat podobným způsobem)
			- víme $\exists t \in R[x]\cap R[y]$
				- tedy platí xRt, tRx, yRt, tRy
			- chceme $\forall a \in R[x]: a \in R[y]$
			- dále aplikujeme tranzitivitu
			- $aRx \land xRt \implies aRt$
			- $aRt \land tRy \implies aRy$
		- (3) na základě ekvivalenčních tříd lze jednoznačně určit, zda jsou prvky x a y ekvivalentní, neboť stačí najít ekvivalenční třídu obsahující y a zjistit, zda je v této třídě také x

## Uspořádání

- Definice: Uspořádání částečné a lineární, uspořádaná množina, ostré uspořádání
	- relace R na množině X je (částečné) uspořádání $\equiv$ R je reflexivní & antisymetrická & tranzitivní
	- (částečně) uspořádaná množina $(X,R)$
		- zkráceně ČUM
		- R je (částečné) uspořádání na X
	- prvky $x,y \in X$ jsou porovnatelné $\equiv xRy \lor yRx$
	- uspořádání je lineární $\equiv \forall x,y\in X$ porovnatelné
		- (všechny prvky množiny jsou navzájem porovnatelné)
	- částečné uspořádání (nebo pouze uspořádání) je obecný pojem, některá taková uspořádání jsou navíc lineární
	- ostré uspořádání – každému uspořádání $\leq$ na X přiřadíme relaci $<$ na X: $a < b \equiv a \leq b \land a \neq b$ 
		- pozor – ostré uspořádání není speciálním případem uspořádání (protože není reflexivní)
		- vlastnosti ostrého uspořádání – ireflexivní, antisymetrické, tranzitivní
- Příklady uspořádání: dělitelnost, inkluze podmnožin, lexikografické
	- dělitelnost $(\mathbb N^+,\backslash)$
		- $2\backslash 4$
		- $4,6$ neporovnatelné
		- dělitelnost na reálných čísel (bez nuly) není uspořádání, protože $(-1)\backslash1\land 1\backslash (-1)$ (není antisymetrické)
	- inkluze $(2^X,\subseteq)$
		- $\lbrace 1 \rbrace \subseteq \lbrace 1,3 \rbrace$
		- $\lbrace 1,2 \rbrace, \lbrace 2,3 \rbrace$ neporovnatelné
	- lexikografické uspořádání
		- abeceda: $(X, \leq)$
		- Df: $(X^2,\leq_{lex})$
		- $(a_1, a_2) \leq_{lex} (b_1, b_2) \equiv a_1 \lt b_1 \lor (a_1=b_1 \land a2\leq b_2)$
		- $(X^k, \leq_{lex})$
		- $(X^*, \leq_{lex})$
			- X* – konečné posloupnosti prvků z X
		- pokud je slovo krátké, doplníme ho mezerami ze začátku abecedy
- Definice: Hasseův diagram, relace bezprostředního předchůdce
	- Hasseův diagram graficky zachycuje vztahy mezi prvky ČUM (porovnatelné prvky jsou spojeny, větší prvky jsou výše)
	- $x$ je bezprostředním předchůdcem $y$ v uspořádání $\leq$ $\equiv x\lt y \land (\nexists z: x\lt z \land z \lt y)$
- Definice: Minimální/maximální a nejmenší/největší prvek
	- prvek $x\in X$ je nejmenší $\equiv \forall y \in X: x\leq y$
	- prvek $x\in X$ je minimální $\equiv \nexists y \in X: y\lt x$
	- x je nejmenší $\implies$ x je minimální
	- v Hassově diagramu
		- z minimálního prvku dolů nevede žádná spojnice
		- nejmenší prvek je nejníž v diagramu, existuje do něj cesta z libovolného jiného prvku
- Věta: Konečná neprázdná uspořádaná množina má minimální a maximální prvek
	- důkaz
		- zvolíme $x_1 \in X$ libovolně
		- buď je $x_1$ minimální, nebo $\exists x_2 \lt x_1$
		- buď je $x_2$ minimální, nebo $\exists x_3\lt x_2$
		- atd.
		- po konečně mnoha krocích nalezneme minimální prvek, protože jinak by X měla nekonečně mnoho různých prvků, což je spor s konečností
- Definice: Řetězec a antiřetězec
	- pro $(X,\leq)$ ČUM:
	- $A\subseteq X$ je řetězec $\equiv \forall a,b \in A: a,b$ jsou porovnatelné
	- $A \subseteq X$ je antiřetězec (nezávislá množina) $\equiv \nexists a,b$ různé & porovnatelné
- Definice: parametry α a ω
	- $\omega(X,\leq)$ je délka nejdelšího řetězce = maximum z délek řetězců (výška uspořádání)
	- $\alpha(X,\leq)$ je délka nejdelšího antiřetězce (šířka uspořádání)
- Věta: O Dlouhém a Širokém
	- věta: pro každou konečnou ČUM $(X,\leq)$ platí $\alpha(X,\leq)\cdot \omega(X,\leq)\geq |X|$
	- důkaz: TODO

## Kombinatorické počítání

- Věta: Počet funkcí mezi množinami
	- věta: počet $f:N\to M=m^n$
		- pro $|N|=n, |M|=m;\quad m,n\gt 0$
	- důkaz indukcí podle $n$
		- $n=1\quad \text{\#}f=m=m^1$
		- .
- Věta: Počet prostých funkcí mezi množinami
- Definice: Klesající mocnina
- Definice: Charakteristická funkce podmnožiny
- Věta: Počet všech podmnožin
- Věta: Počet podmnožin sudé a liché velikosti
- Věta: Počet permutací na množině
- Věta: Počet uspořádaných k-tic bez opakování a k-prvkových podmnožin
- Definice: Notace pro množinu všech k-prvkových podmnožin
- Definice: Kombinační číslo (binomický koeficient), Pascalův trojúhelník
- Věta: Základní vlastnosti kombinačních čísel
- Věta: Binomická věta
- Věta: Princip inkluze a exkluze
- Příklad: Problém šatnářky: počet permutací bez pevného bodu
- Věta: Odhad faktoriálu: $n^{n/2} \leq n! \leq ((n+1)/2)^n$
- Věta: Odhad kombinačního čísla: $(n/k)^k \leq C(n,k) \leq n^k$
- Věta: Odhad prostředního kombinačního čísla: $4^n/(2n+1) \leq C(2n,n) \leq 4^n$

## Grafy

- Definice: Graf, vrchol, hrana, V(G), E(G)
- Definice: Standardní grafy: úplný, prázdný, cesta, kružnice
- Definice: Bipartitní graf, úplný bipartitní graf
- Definice: Isomorfismus grafů
- Definice: Stupeň vrcholu, k-regulární graf, skóre grafu
- Věta: Vztah mezi součtem stupňů a počtem hran, princip sudosti
- Věta: Věta o skóre
- Definice: Podgraf, indukovaný podgraf
- Definice: Cesta, kružnice, sled a tah v grafu
- Definice: Souvislý graf, relace dosažitelnosti (ekvivalence), komponenty souvislosti
- Věta: Dosažitelnost sledem je totéž jako dosažitelnost cestou
- Definice: Matice sousednosti
- Věta: Počet sledů délky k lze získat z k-té mocniny matice sousednosti
- Definice: Vzdálenost v grafu (grafová metrika)
- Věta: Trojúhelníková nerovnost pro vzdálenost
- Definice: Grafové operace: přidání/odebrání vrcholu/hrany, dělení hrany, kontrakce hrany
- Definice: Otevřený a uzavřený eulerovský tah
- Věta: Věta o existenci uzavřeného eulerovského tahu
- Definice: Orientovaný graf, podkladový graf, vstupní a výstupní stupeň, vyváženost vrcholu
- Definice: Silná a slabá souvislost orientovaných grafů
- Věta: Uzavřené eulerovské tahy v orientovaných grafech

## Stromy

- Definice: Strom, les, list
- Věta: Lemma o koncovém vrcholu
- Věta: Je-li l list grafu G, pak G je strom, právě když G-l je strom.
- Věta: Pět ekvivalentních charakteristik stromu
- Definice: Kostra grafu
- Věta: Graf má kostru, právě když je souvislý.

## Rovinné kreslení grafů

- Definice: Rovinné nakreslení grafu a jeho stěny (neformálně)
- Definice: Rovinný graf, topologický graf
- Příklad: K5 a K3,3 nejsou rovinné.
- Věta: Hranice stěny je nakreslením uzavřeného sledu (bez důkazu).
- Definice: Stereografická projekce
- Věta: Graf jde nakreslit do roviny, právě když jde nakreslit na sféru.
- Příklad: Vnější stěnu lze zvolit.
- Věta: Kuratowského věta (bez důkazu)
- Věta: Eulerova formule pro souvislé rovinné grafy (v+f=e+2)
- Věta: Maximální rovinný graf je triangulace.
- Věta: Maximální počet hran rovinného grafu
- Věta: V rovinném grafu existuje vrchol stupně nejvýše 5.
- Věta: Počet hran a vrchol nízkého stupně v rovinných grafech bez trojúhelníků

## Barvení grafů

- Definice: Obarvení grafu k barvami, barevnost
- Příklad: Barevnost úplných grafů, cest a kružnic
- Věta: Ekvivalentní tvrzení: graf má barevnost nejvýše 2, graf je bipartitní, graf neobsahuje lichou kružnici.
- Věta: Barevnost ≥ klikovost
- Příklad: Princip barvení indukcí: stromy jsou 2-obarvitelné, rovinné grafy 6-obarvitelné
- Věta: Barevnost ≤ maximální stupeň + 1
- Věta: Věta o 5 barvách
- Věta: Věta o 4 barvách (bez důkazu)

## Pravděpodobnost

- Definice: Pravděpodobnostní prostor diskrétní, konečný, klasický
- Definice: Jev elementární, jev složený, pravděpodobnost jevu
- Příklad: Jev se také dá popsat logickou formulí.
- Příklad: Bertrandův paradox s kartičkami
- Definice: Podmíněná pravděpodobnost
- Věta: Věta o úplné pravděpodobnosti
- Věta: Bayesova věta
- Definice: Jevy nezávislé a po dvou nezávislé
- Definice: Součin pravděpodobnostních prostorů, projekce
- Definice: Náhodná veličina
- Příklad: Logické formule s náhodnými veličinami dávají jevy.
- Definice: Střední hodnota
- Věta: Věta o linearitě střední hodnoty
- Definice: Indikátor náhodného jevu
- Příklad: Použití indikátorů k výpočtu střední hodnoty

## Různé

- Věta: Erdősovo-Szekeresovo lemma o monotónních podposloupnostech
- Příklad: Existence de Bruijnovy posloupnosti (konstrukce pomocí orientovaných eulerovských tahů)
- Příklad: Klasifikace platónských těles pomocí rovinných grafů
