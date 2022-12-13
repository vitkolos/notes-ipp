# Diskrétní matematika

## Cvičení

- https://kam.mff.cuni.cz/~tancer/Diskretka/
- Kapitoly z diskrétní matematiky
- https://matematika.reseneulohy.cz
- https://stream.cuni.cz, nahrávka na YouTube (Diskrétní matematika Nešetřil)
- diskrétní matematika – protipól ke spojité matematice
- často konečné objekty
- důkazy matematickou indukcí

### Příklady

- 6. topinky – za 6 minut
	- 2 minuty opékat 1A, 2A
	- 2 minuty 1B, 3A
	- 2 minuty 2B, 3B
- 1. indukce – viz sešit 
	- lze indukovat tak, že dokážeme platnost tvrzení pro $n = 1$, $n = 2$ a následně pro $n + 2$

## Přednáška

- zkouška
	- teorie z přednášek – umět definovat, formulovat tvrzení, dokázat je
	- nemusíme si pamatovat důkazy z přednášek
	- je potřeba, abychom na zkoušce předvedli cokoliv, co funguje
- https://slama.dev/poznamky/diskretni-matematika/
- https://mj.ucw.cz/vyuka/dm/
- https://mj.ucw.cz/vyuka/2021/dm/
- https://iuuk.mff.cuni.cz/~rakdver/index.php?which=uceni&subject=dm

### Definice

* $a \backslash b$ (a dělí b)
	* $a \backslash b \equiv \exists c : b = a \cdot c$
* prvočíslo

$definice \rightarrow tvrzení \xrightarrow{důkaz} věta$

- lemma – pomocné tvrzení sloužící k dokázání větší věty
- definicí zavádíme pojem pomocí jednodušších pojmů
- axiomatický přístup – definice objektů pomocí jejich vlastností (axiomů)

### Důkazy

- důkaz sporem
	- budeme předpokládat, že tvrzení neplatí, následně dokážeme, že je nemožné, aby tomu tak bylo
	- příklad
		- **Tvrzení:** Prvočísel je nekonečně mnoho.
		- **Důkaz:** sporem: Nechť $p_1, p_2, \dots, p_n$
		- viz sešit
- důkaz indukcí
	- chceme: $\forall n \in \mathbb{N}: \phi(n)$
	- poznámka: do přirozených čísel na této přednášce řadíme nulu
	- uděláme: $\phi(0)$, indukční krok $\forall n(\phi(n) \Rightarrow \phi(n+1))$
	- příklad
		- **Tvrzení:** $2^0 + 2^1 + \dots + 2^n = 2^{n+1}-1$
		- **Dk:** indukcí podle n
			1) zákl. případ: $n=0$ ......... 1=1
			2) krok: IP: 

### Relace

- vztahy mezi dvojicemi objektů
- např. rovnost přirozených čísel
- "krabička" se dvěma vstupy (na pořadí záleží) → vrátí nám ano nebo ne
- můžeme vyjmenovat všechny dvojice, pro které nám krabička vrátí ano
- kartézský součin $X × Y := \{(x,y) | x \in X, y \in Y\}$
- Df: Relace mezi množinami X, Y je libovolná podmnožina X × Y.
- Relace na množině X ... mezi X, X.

- příklad – pro X = {1, 2, 3, 4, 5}
	- $(x,y) \in R$ zkrátíme na xRy
	- rovnost
		- R = {(1,1), (2,2), (3,3), (4,4), (5,5)}
		- diagonální relace – $\Delta_X := \{(x,x) | x \in X\}$
	- dělitelnost x \\ y
	- $x+y \leq 5$
	- $\emptyset$ prázdná relace
	- X × Y univerzální relace

- Df: pro relace $R \subseteq X × Y$ definujeme inverzní relaci $R^{-1} \subseteq Y × X$
	- $\forall x \in X, \forall  \in Y: yR^{-1}x \equiv xRy$
- Df: pro relace $R \subseteq X×Y$ a $S \subseteq Y×Z$ definujeme jejich složení $R \circ S \subseteq X×Z:$
	- $\forall x \in X, \forall z \in Z: x(R \circ S)z \equiv (\exists y \in Y: xRy \land ySz)$
- příklad
	- $R \subseteq X×Y, \Delta_Y$
	- $R\circ \Delta_Y = R$

### Funkce

- funkce jsou relace, které ke každému vstupu přiřazují pouze jeden výstup
- Df: Funkce (zobrazení) z X do Y je relace f mezi X, Y taková, že $\forall x \in X\  \exists! y \in Y: xfy$
- Značení: $f: X → Y$
	- pro $x \in X: f(x)=y \equiv xfy$
	- pro $A \subseteq X: f[A]:=\{f(a)|a \in A\}$
- příklady
	- $x \mapsto x$ **identita** $\Delta_X$
	- $sin: \mathbb{R} → [-1,1]$
		- lze zapsat větší množinu než definiční obor?
	- $sgn: \mathbb{R} → \{-1,0,+1\}$
		- $x \mapsto -1$ pro $x<0$
		- $x \mapsto 0$ pro $x=0$
		- $x \mapsto +1$ pro $x>0$
	- mohutnost množiny
		- $|\_|: 2^\mathbb{N} → \mathbb{N} \cup \{\infty\}$
	- $f(a,b) = a+b$
		- $f: \mathbb{R}×\mathbb{R} → \mathbb{R}$
- skládání funkcí
	- $f \circ g$
	- dva způsoby značení
	- $(f \circ g)(x)=g(f(x))$
- Df: Funkce $f:x→y$ je
	- prostá (injektivní) $\equiv \forall x_1, x_2 \in X: X \neq x_2 \Rightarrow f(x_1) \neq f(x_2)$
	- na Y (surjektivní, francouzská výslovnost) $\forall y \in Y : \exists x \in X : f(x)=y$
	- vzájemně jednoznačná (1–1, bijektivní) $\equiv \forall y \in Y : \exists! x \in X: f(x) = y$
- pro funkci $f$ je $f^{-1}$ funkce $\iff f$ je bijektivní
- pro $f$ prostou: $f^{-1}$ je funkce z Y' do X
	- přičemž Y' je množina všech obrazů, tedy všech $f[X]$
- Df: relace R na X je
	- reflexivní $\equiv \forall x \in X: xRx$
		- $\Delta_X \subseteq R$
	- symetrická $\equiv \forall x,y \in X: xRy \iff yRx$
		- $R = R^{-1}$
	- antisymetrická $\equiv \forall x,y \in X, x\neq y: (xRy \Rightarrow \neg yRx)$
		- pokud x a y jsou různé prvky a x je v relaci s y, tak není pravda, že y je v relaci s x
	- tranzitivní $\equiv \forall x,y,z \in X: xRy \land yRz \Rightarrow xRz$
		- $R \circ R \subseteq R$
	- Df: Relace R je ekvivalence $\equiv$ R je reflexivní & symetrická & tranzitivní
		- příklady
			- rovnost na reálných číslech
			- mod K na Z
				- $x \equiv y \iff K \backslash x-y$
			- geometrická shodnost
			- geometrická podobnost
		- pro R ekvivalenci na X
			- Df: ekvivalenční třída prvku $x \in X$: $R[x] := \{y\in X | xRy\}$
				- viz sešit

- Df: (částečné) **Uspořádání** na množině X je relace R na X, která je reflexivní, antisymetrická a tranzitivní
	- např. porovnávání reálných čísel
	- Df: (částečně) Uspořádaná množina (X,R): X je množina, R uspořádání na X
	- Značení $\leq$ (nebo různé varianty tohoto znaku)
	- Df: $x,y \in X$ jsou porovnatelné $\equiv xRy \lor yRx$
	- Df: Uspořádání je lineární (úplné) $\equiv$ každé 2 prvky jsou porovnatelné
	- částečné uspořádání – může (ale nemusí) mít neporovnatelné prvky
	- ostré uspořádání – každému uspořádání $\leq$ na X přiřadíme relaci $<$ na X: $a < b \equiv a \leq b \land a \neq b$ 
		- pozor – ostré uspořádání není speciálním případem uspořádání (protože není reflexivní)
		- vlastnosti ostrého uspořádání – ireflexivní, antisymetrické, tranzitivní
	- příklady
		- $(\mathbb{N}, \leq)$ lineární
		- $(\mathbb{Q}, \leq)$ lineární
		- $\Delta_X$
		- $(\mathbb{N}^+, \backslash)$
		- $(2^X, \subseteq)$ inkluze
		- lexikografické
			- abeceda: $(X, \leq)$
			- Df: $(X^2,\leq_{lex})$
			- $(a_1, a_2) \leq_{lex} (b_1, b_2) \equiv a_1 \lt b_1 \lor (a_1=b_1 \land a2\leq b_2)$
			- $(X^k, \leq_{lex})$
			- $(X^*, \leq_{lex})$
				- X* – konečné posloupnosti prvků z X
			- pokud je slovo krátké, doplníme ho mezerami ze začátku abecedy
- Df: relace bezprostředního předchůdce
	- $a \triangleleft b \equiv a \lt b \land \nexists c: a \lt c \land c \lt b$
	- Hasseův diagram – pro konečné ČUM (částečně uspořádané množiny) – viz sešit
- Df: pro ČUM $(X,\leq)$ je $x \in X$:
	- minimální $\equiv \nexists y\in X:y \lt x$
	- nejmenší $\equiv \forall y \in X: x \leq y$
	- maximální
	- největší
- Větička: Každá konečná neprázdná částečně uspořádaná množina $(X,\leq)$ má minimální prvek.
- Dk: zvolíme $x_1 \in X$ libovolně
	- Buď $x_1$ je minimální,
	- nebo $\exists x_2 < x_1$, s ním pokračuji
	- $x_1>x_2>x_3>\dots >x_t$
	- Pokud t > |x|, pak $\exists i,j; i\neq j: x_i = x_j$
	- to lze pomocí tranzitivity dovést ke sporu
- Df: $A \subseteq X$ pro ČUM $(X, \leq)$ je
	- řetězec $\equiv (A,\leq)$ je lineární UM
	- antiřetězec $\equiv \forall(a,b) \in A, a \neq b$ jsou neporovnatelné

### Kombinatorika

- Df: $[n] := \{1, \dots, n\}$
	- n-prvková množina od 1 do n
- \# $f: [n] → [m] = m^n$
- počet k-prvkových podmnožin – n-prvkové množiny
- kolik má n-prvková množina prázdných podmnožin? prázdná množina existuje pouze jedna
- základní vlastnosti kombinačních čísel
- symetrie kombinačních čísel – bijekce mezi podmnožinami a jejich doplňky do původní množiny
- součet kombinačních čísel v n-tém řádku je 2^n – je to potence množiny
- kombinační číslo rozložíme na součet počtu množin obsahující konkrétní prvek a množin, které tento prvek neobsahují → kombinační číslo se rovná součtu dvou čísel nad ním (v Pascalově trojúhelníku)
- binom – dvojčlen
- binomické koeficienty, binomická věta
	- jeden člen výsledného součtu – součin n věcí, z nichž každá bude x nebo y
		- z každé závorky vyberu x nebo y
		- výsledkem je člen $x^{n-k}y^k$
		- takových členů tam bude $n \choose k$
- když zvolíme x = 1, y = -1 a dosadíme do binomické věty, tak zjistíme, že sudých podmnožin je stejně jako lichých (kromě prázdné množiny, ta má jednu sudou a žádnou lichou)
- n kuliček do k přihrádek
	- kolik existuje způsobů, jak číslo n zapsat jako k sčítanců
	- kuličky nejsou rozlišitelné, přihrádky ano
	- máme stroj na plnění přihrádek, ten se nad nimi pohybuje a sype do nich kuličky
	- umí operace – pohni se o přihrádku doprava (P), přidej kuličku (K)
	- v programu je právě k-krát příkaz na pohyb a právě n-krát příkaz na přidání kuličky, musí končit p
	- tudíž (k-1)-krát příkaz na pohyb a n-krát příkaz na přidání kuličky
	- ${n+k-1}\choose n$ možností
- kluby (spolky), princip inkluze a exkluze
- šatnářka
	- bijekce z množiny klobouků do množiny pánů
	- $\pi(i)=i$ … pevný bod
	- velikost průniku je $(n-k)!$
	- nezáleží na výběru podmnožiny z indexové množiny, takže stačí vynásobit n nad k
- odhady faktoriálu
	- triviální: $2^{n-1} \leq n! \leq n^n$
	- $n^{\frac{n}{2}} \leq n! \leq (\frac{n+1}{2})^n$
	- důkaz AG nerovnosti
- odhad kombinačního čísla

### Grafy

- Df: Graf je (V, E), kde V je konečná neprázdná množina vrcholů a $E \subseteq {V \choose 2}$ je množina hran.
- značení
	- G = (V, E)
	- množina vrcholů … V(G)
	- množina hran … E(G)
- rozšíření grafů
	- orientované – hrany mají šipky
	- se smyčkami – jako u relací
	- multigrafy – dva vrcholy spojené více než jednou hranou
	- nekonečné grafy
- příklady
	- úplný graf $K_n$
		- $V(K_n):=[n]$
		- $E(K_n):={V(K_n)\choose 2}$
	- prázdný graf $E_n$
		- $V(E_n):=[n]$
		- $E(E_n) =\emptyset$
	- cesta $P_n$
		- $V(P_n):=\{0\dots n\}$
		- $E(P_n):=\{\{i,i+1\}|0\leq i \lt n\}$
		- délka cesty se měří v počtu hran
	- kružnice/cyklus $C_n$
		- $n\geq 3$
		- $V(C_n):=\{0\dots n–1\}$
		- $E(C_n):=\{\{i,i+1\mod n\}|0\leq i \lt n\}$
	- úplný bipartitní $K_{m,n}$
		- každý prvek nalevo je spojený s každým napravo
		- prvky na jedné straně mezi sebou nejsou spojeny
	- bipartitní graf
		- partity grafu – jednotlivé „strany“
		- Df: Graf (V, E) je bipartitní $\equiv \exists L,P\subseteq V$ t. ž.:
			- $L \cup P = V$
			- $L \cap P = \emptyset$
			- $\forall e \in E: |e \cap L| = 1\quad (\land\ |e \cap P| = 1)$
- izomorfismus grafů
	- existuje bijekce, která zachovává vlastnost být spojen hranou
	- v podstatě stačí přejmenovat vrcholy a dostaneme dva stejné grafy
	- značení $\cong$
	- $\cong$ je ekvivalence na libovolné množině grafů
		- neexistuje množina všech grafů (protože neexistuje množina všech množin)
- pokud vezmeme n vrcholů, kolik existuje grafů s touto množinou vrcholů?
	- \# grafů na n vrcholech
	- každá dvojice vrcholů buď je hranou, nebo ne
	- některé grafy jsou izomorfní, ale dokázali jsme, že se počet neizomorfních grafů blíží počtu všech grafů
- stupeň vrcholu v grafu – počet hran, kterých se účastní daný vrchol
- graf je k-regulární, pokud je stupeň všech vrcholů grafu roven k (z čehož vyplývá, že nemůže existovat více takových k)
- skóre grafu – posloupnost stupňů vrcholů (až na pořadí) → jakmile dvěma grafům vyjde jiné skóre, nemohou být izomorfní
- ale existují např. dva neizomorfní grafy se skórem 2,2,2,2,3,3
- nemůže existovat graf 3,3,3
- součet skóre je roven dvojnásobku počtu hran → součet skóre je vždy sudý
- počet vrcholů lichého stupně je sudý
- jednoprvková posloupnost je skóre grafu, když je to nula
- graf může mít u některých vrcholů nulu
- věta o skóre :)
- podgraf
- indukovaný podgraf – vyberu si vrcholy z původního grafu a do nového grafu zdědím všechny hrany mezi nimi
	- „podgraf indukovaný množinou vrcholů“
	- $G[A] := (A, E(G) \cap {A \choose 2})$
- cesta v grafu
	- v grafu existuje podgraf izomorfní s Pn
	- v grafu existuje určitá posloupnost
- kružnice v grafu
- souvislost grafu – pro každé dva vrcholy existuje cesta mezi nimi
- komponenty souvislosti
- relace dosažitelnosti – relace na vrcholech popisující existenci cesty
- důkaz tranzitivity dosažitelnosti
- sled (walk) – cesta s možným opakováním vrcholů i hran
- tah – hrany se neopakují, vrcholy mohou
- mezi vrcholy u,v vede sled $\iff$ mezi u,v vede cesta
- ze sledu lze udělat cestu vystřižením úseků mezi opakujícími se vrcholy
- komponenty souvislosti jsou podgrafy indukované ekvivalenčními třídami relace dosažitelnosti
- graf je souvislý $\iff$ # komponent souvislosti grafu = 1

#### Operace s grafy

- přidání vrcholu, přidání hrany, smazání hrany – vždy pouze úprava odpovídající množiny
- odebrání vrcholu – musím odebrat odpovídající hrany
	- výsledný graf je podgraf indukovaný množinou všech vrcholů bez toho odebíraného
		- $G-v=G[V\setminus\{v\}]$
- dělení hrany (pomocí nového vrcholu): G % e
- kontrakce hrany: G.e
- eulerovský tah obsahuje všechny vrcholy i hrany grafu
- tah může být uzavřený (končí, kde začal), nebo otevřený
- graf je eulerovský (má uzavřený eulerovský tah) $\iff$ je souvislý a každý jeho vrchol má sudý stupeň

#### Orientované grafy

- $(V,E): E \subseteq V^2 \setminus \{(x,x)|x\in V\}$
	- nepovolíme smyčky (v podstatě zakážeme diagonálu na relaci)
- vstupní stupeň, výstupní stupeň
- součet všech vstupních stupňů, součet všech výstupních stupňů a počet hran se rovnají
- dva druhy souvislosti
	- silná souvislost – existuje cesta z každého vrcholu do každého vrcholu
	- slabá souvislost – graf „drží pohromadě“, podkladový graf je souvislý (podkladový graf je neorientovaný graf založený na tom původním orientovaném)
	- silná souvislost $\implies$ slabá souvislost
	- pro vyvážené grafy platí silná souvislost právě tehdy, když platí slabá
- relace obousměrné dosažitelnosti
- komponenty silné souvislosti
- graf je vyvážený, pokud u každého vrcholu platí, že má stejný vstupní a výstupní stupeň
- vyvážený a slabě souvislý $\iff$ eulerovský $\iff$ vyvážený a silně souvislý
- indikátor $[\psi]$ je 0/1 podle platnosti výroku $\psi$
- popis grafů pomocí matic
	- matice sousednosti (A)
		- pro graf s n vrcholy má n řádků a n sloupců
		- jednoznačně určuje graf až na pojmenování vrcholů (tedy všechny izomorfní grafy)
		- matice sousednosti je symetrická s nulami na hlavní diagonále
		- druhá mocnina matice sousednosti nám určí, kolik je mezi dvěma vrcholy sledů délky 2
		- věta o k-té mocnině matice sousednosti + důkaz
- pro souvislý graf definujeme vzdálenost mezi dvěma vrcholy = počet hran v nejkratší cestě mezi dvěma vrcholy
	- vzdálenost bude vždy nezáporná
	- $d_G(u,v) = 0 \iff u=v$
	- platí trojúhelníková nerovnost $d_G(u,w) \leq d_G(u,w) + d_G(w,v)$
	- $d_G(v,u)=d_G(u,v)$
- tedy $d_G$ je metrika

#### Stromy

- strom $\equiv$ souvislý acyklický graf (nejsou v něm kružnice)
- les $\equiv$ acyklický graf (graf, jehož komponenty jsou stromy)
- list je vrchol stupně jedna
- nejméně listů (0) má strom o jednom vrcholu
- obecně stromy s nejméně listy jsou cesty
- lemma (o listu): každý strom s aspoň 2 vrcholy má aspoň 1 list + důkaz
- lemma: pro graf G s listem l platí, že G je strom $\iff G-l$ je strom
- důkaz Eulerovy formule (strom má o jeden vrchol víc než hran)
	- nejdřív musíme otrhat listy a potom je zpátky přidat – nestačí dokázat, že můžeme přidávat listy k grafu o jednom vrcholu a bude to platit stále
- věta o charakterizaci stromů – pro graf G jsou tato tvrzení ekvivalentní
	- G je souvislý a acyklický (strom)
	- mezi vrcholy $u, v$ existuje právě jedna cesta (jednoznačně souvislý)
	- G je souvislý a po smazání libovolné jedné hrany už nebude souvislý (minimální souvislý)
	- G je acyklický a po přidání libovolné jedné hrany vznikne cyklus (maximální acyklický)
	- G je souvislý a platí pro něj Eulerova formule
- kostra grafu – je podgraf, který obsahuje všechny vrcholy původního grafu a je to strom
- G má kostru $\iff$ G je souvislý

#### Rovinné grafy

- kreslení grafu, aby se hrany nekřížily
- definice křivky
	- $f:[0,1]→\mathbb R$
	- spojitá, prostá
	- = oblouk
- vrcholy = body v rovině, hrany = křivky, které se neprotínají a jejich společnými body jsou jejich společné vrcholy
- topologický graf je uspořádaná dvojice (graf, nakreslení)
- graf je rovinný, pokud má alespoň jedno rovinné nakreslení
- stěny nakreslení
	- části, na které nakreslení grafu rozděluje rovinu
	- stěnou je i vnější stěna (zbytek roviny)
	- hranice stěny – skládá se z hran
	- hranice stěny je nakreslení uzavřeného sledu
- je-li graf rovinný, všechny jeho podgrafy jsou také rovinné
- které grafy jsou rovinné
	- cesty
	- kružnice
	- stromy
	- $K_1, K_2, K_3, K_4$
- věta (Jordanova): každá uzavřená křivka v rovině dělí rovinu na dvě části
- příklad: $K_5$ není rovinný, podobně $K_{3,3}$
- kreslení na sféru
	- stereografická projekce
	- střílím polopřímku ze severního pólu, promítám na rovinu, na které leží jižní pól
	- spojitá bijekce mezi sférou bez severního pólu a rovinou
	- sféru můžeme libovolně pootočit
	- $\implies$vnější stěnu lze zvolit libovolně
- operace pro G rovinný
	- odebrání vrcholu či hrany je v pořádku
	- přidání vrcholu je v pořádku
	- přidání hrany může být problém
	- dělení hrany je v pořádku
	- kontrakce hrany je v pořádku (podle geometrické intuice)
- Kuratowského věta
	- G je nerovinný$\iff$G obsahuje podgraf izomorfní s dělením $K_5$ nebo $K_{3,3}$
- testování rovinnosti v $O(|V|+|E|)$
- Eulerova formule: Nechť G je souvislý graf nakreslený do roviny, $v:=|V(G)|, e:=|E(G)|, f:=$ \# stěn nakreslení, potom $v+f=e+2$.
- Dk: Zvolíme $v$ pevně, pak indukcí podle $e$.
	- základní příklad
		- G je strom, $e = v-1$
		- f = 1
		- chceme: $v+1=v-1+2 \space\checkmark$
	- $e -1→ e$
		- mějme graf G s $e$ hranami
		- nechť x je hrana na kružnici v G
		- $G' := G–x$
		- $v'=v$
		- $e'=e-1$
		- $f'=f-1$
		- z IP: $v' + f' = e'+2$
		- $v+f-1=e-1+2 \space \checkmark$
- Df: G je maximální rovinný, pokud mu nemůžeme bez ztráty rovinnosti přidat hranu
- je-li G maximální rovinný s aspoň 3 vrcholy, ve všech jeho nakresleních jsou všechny stěny trojúhelníky (říká se jim **rovinné triangulace**)
	- G je souvislý (u nesouvislých se komponenty dají spojit, což je spor s maximální souvislostí)
	- je-li hranicí stěny kružnice$\implies$je to $\Delta$ (kdyby to nebyl trojúhelník, dá se najít úhlopříčka, což je spor)
	- hranicí stěny není $C_n$
- počet hran pro triangulace
	- každá stěna přispěje třemi hranami
	- každá hrana patří ke dvěma stěnám
	- $3f=2e → f=\frac{2}{3}e$
	- $v+\frac{2}{3}e=e+2$
	- $v-2=\frac{1}{3}e$
	- $e=3v-6$
- věta: v každém rovinném grafu s aspoň 3 vrcholy je $|E|\leq 3|V|-6$
- dk: doplníme do G hrany, až získáme maximální rovinný G'
	- $v'=v,\ e'\geq e,\ e'=3v'-6,\ e\leq 3v-6$
- důsledky
	- průměrný stupeň vrcholu v rovinném grafu < 6
		- součet stupňů / v = 2e/v $\leq$ 6v-12 / v < 6
	- v každém rovinném grafu existuje vrchol stupně $\leq$ 5
- rovinný graf bez trojúhelníků
	- max. grafy mají stěny čtverec, pěticyklus, hvězda o pěti paprscích
	- podle eulerovy formule…

#### Barvení

- dualita grafu: rovinná mapa → rovinný graf
- Df: obarvení grafu G k barvami je funkce $c:V(G)\to \lbrace1,\dots,k\rbrace$ t. ž. $\forall \lbrace x,y\rbrace \in E(G): c(x) \neq c(y)$
- nemusím použít všechny barvy
- Df: barevnost (chromatické číslo) grafu G: $\chi(G):=\text{min } k$ t. ž. G má obarvení k barvami (tedy nejmenší počet barev, kterými lze graf obarvit)
- příklady
	- $\chi(E_n)=1$
	- $\chi(K_n)=n$
	- $\chi(P_n)=2$ pro $n\geq 1$
	- pro $n$ sudé $\chi(C_n)=2$, pro $n$ liché $\chi(C_n)=3$
- pozorování: $\chi(G)\leq 2 \iff G$ je bipartitní
- barvení stromu
	- strom rozdělíme do vrstev podle vzdálenosti od kořenu
	- $c(x)=(d(v,x) \mod 2)+1$
- tvrzení: každý strom je 2-obarvitelný
- dk: indukcí podle počtu vrcholů (základní případ pro 1 vrchol), postupně přidáváme (odebrané) listy, listu dáváme opačnou barvu než má vrchol, kam ho připojujeme, tedy $c(l)=3-c'(s)$
- pozorování: kdykoli $H\subseteq G$, pak $\chi(H)\leq \chi(G)$
- věta: graf má barevnost nejvýše dva $\iff$ neobsahuje lichou kružnici
	- tedy bipartitní grafy jsou ty, které neobsahují liché kružnice
- dk:
	- $\implies$ máme dokázáno obměnou (když má lichou kružnici, nejde obarvit dvěma barvami)
	- $\impliedby$ 
		- kdyby G byl nesouvislý: obarvíme po komponentách
		- jinak: nechť T je kostra grafu G, pak existuje obarvení kostry (dvěma barvami)
			- sporem: kdyby existovala hrana, které tohle obarvení přiřklo stejné barvy koncových vrcholů, pak v grafu existuje lichá kružnice
			- mezi stejnobarevnými vrcholy bude cesta sudé délky, protože mají stejnou barvu a jsou ve stromě
			- tedy spojením stejnobarevných vrcholů vznikne lichá kružnice
- odtrhávání vrcholů v rovinném grafu
- graf G je k-degenerovaný $\equiv \exists \leq$ lineární uspořádání na $V(G)$ t. ž. $\forall v \in V(G) |\lbrace u<v | \lbrace u,v \rbrace \in E(G) \rbrace| \leq k$
	- vrcholy lze uspořádat tak, že z každého vrcholu doleva vede nejvýše k hran
	- vrcholy skládám zprava doleva tak, jak je odtrhávám
- stromy 1-deg., rovinné 5-deg., rovinné bez trojúhelníků 3-deg.
- pro $\Delta := \text{max deg}(v)$: $\Delta\text{-degen.}$
- k-deg. → $\chi \leq k+1$
- takže pro rovinné grafy stačí 6 barev
- pojďme dokázat, že jich stačí 5
- věta (o 5 barvách): pro G rovinný je $\chi(G)\leq 5$
- dk \#1:  indukcí podle $|V|$
	- pro $|V|\leq 5$ triviální
	- $n-1\to n$
		- nechť $v$ je vrchol s minimálním stupněm (nejvýše pět)
		- G' := G–v, podle IP existuje 5-obarvení c' grafu G'
		- pokud na sousedech $v$ v obarvení c' jsou použity max. 4 barvy, tak tu pátou můžeme použít na vrchol $v$
		- co když má každý soused jinou barvu
			- A je podgraf indukovaný vrholy, do kterých existuje cesta ze souseda $a$ přes áčkové a céčkové barvy
			- pokud soused $c \notin A$
				- prohodíme barvy v A
				- tím pádem áčková barva se uvolní pro $v$
			- pokud soused $c \in A$
				- použiju stejný trik pro b a d
				- soused $b$ je obalený kružnicí mezi $a$ a $c$, takže nehrozí, že by byl spojený s $d$
		- tzv. Kempeho řetězce
- dk \#2:
	- máme vrchol stupně 5
	- musí existovat dva sousedi toho grafu, kteří nejsou spojeni hranou (jinak bychom dostali K5)
	- můžu vytvořit rovinný G'=G–v+{x,y} (přidání hrany)
	- můžu vytvořit rovinný G''=G'.{x,y} (kontrakce hrany)
	- G'' obarvíme indukcí → dostaneme obarvení c'' → c obarvení G–v (v němž se barvy x a y rovnají) → existuje volná barva pro v
