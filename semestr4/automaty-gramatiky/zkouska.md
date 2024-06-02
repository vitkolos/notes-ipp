# Zkouška

## Úvod

- Definice: Deterministický konečný automat
	- deterministický konečný automat (DFA) je pětice $A=(Q,\Sigma,\delta,q_0,F)$
	- $Q$ … konečná množina stavů
	- $\Sigma$ … konečná neprázdná množina vstupních symbolů (abeceda)
	- $\delta:Q\times\Sigma\to Q$ … přechodová funkce
	- $q_0\in Q$ … počáteční stav
	- $F\subseteq Q$ … množina koncových (přijímajících) stavů
	- úmluva
		- pokud přechodová funkce není totální, doplníme ji pomocí stavu *fail* (do něj povedou přechody pro chybějící kombinace stavů a písmen, z něj povedou přechody pouze opět do *fail* pro každé písmeno)
		- pokud $F=\emptyset$ a je vyžadováno $F\neq\emptyset$, přidáme stav *final* (je incidentní jen s přechody, které vedou z *final* do *final* pro každé písmeno abecedy)
- Definice: Slovo, $\epsilon$, $\lambda$, $\Sigma^*$, $\Sigma^+$, jazyk
	- mějme neprázdnou množinu symbolů $\Sigma$
	- slovo je konečná (i prázdná) posloupnost symbolů $s\in\Sigma$
	- prázdné slovo se značí $\epsilon$ nebo $\lambda$
	- $\Sigma^*$ … množina všech slov v abecedě $\Sigma$
	- $\Sigma^+$ … množina všech neprázdných slov v abecedě $\Sigma$
	- jazyk $L\subseteq\Sigma^*$ je množina slov v abecedě $\Sigma$
- Definice: Operace zřetězení, mocnina, délka slova
	- nad slovy $\Sigma^*$ definujeme tyto operace:
		- zřetězení slov $u{.}v$ nebo $uv$
		- mocnina (počet opakování) $u^n$
		- délka slova $|u|$
		- počet výskytů $s\in\Sigma$ ve slově $u$ značíme $|u|_s$
- Definice: Rozšířená přechodová funkce
	- mějme přechodovou funkci $\delta:Q\times\Sigma\to Q$
	- rozšířenou přechodovou funkci $\delta^*:Q\times\Sigma^*\to Q$ (tranzitivní uzávěr $\delta$) definujeme induktivně:
		- $\delta^*(q,\epsilon)=q$
		- $\delta^*(q,wx)=\delta(\delta^*(q,w),x)$ pro $x\in\Sigma,\,w\in\Sigma^*$
	- idea: aplikujeme přechodovou funkci na celé slovo
- Definice: Jazyky rozpoznatelné konečnými automaty, regulární jazyky
	- jazykem rozpoznávaným (přijímaným) deterministickým konečným automatem $A=(Q,\Sigma,\delta,q_0,F)$ nazveme jazyk $L(A)=\set{w\mid w\in\Sigma^*\land\delta^*(q_0,w)\in F}$
	- slovo je přijímáno automatem $A\equiv w\in L(A)$
	- jazyk $L$ je rozpoznatelný konečným atuomatem $\equiv$ existuje konečný automat $A$ takový, že $L=L(A)$
	- třídu jazyků rozpoznatelných konečnými automaty označíme $\mathcal F$, nazveme regulární jazyky
- Věta: Iterační (pumping) lemma pro regulární jazyky
	- věta
		- nechť $L$ je regulární jazyk
		- $(\exists n\in\mathbb N)(\forall w\in L):|w|\geq n\implies w=xyz$
			- $y\neq\epsilon$
			- $|xy|\leq n$
			- $\forall k\geq 0:xy^kz\in L$
		- důkaz
			- mějme regulární jazyk $L$, pak existuje DFA $A$ s $n$ stavy, přičemž $L=L(A)$
			- vezměme libovolné slovo délky aspoň $n$
				- $a_1a_2\dots a_m=w\in L$
				- $m\geq n$
				- $a_i\in\Sigma$
			- definujme $p_i$ jako stav automatu, v němž budeme po $i$ písmenech toho slova
				- $\forall i:p_i=\delta^*(q_0,a_1a_2\dots a_i)$
				- zjevně $p_0=q_0$
			- máme $n+1$ $p_i$ a $n$ různých stavů automatu, takže mezi $p_i$ se nějaký stav opakuje, vezmeme první takový
				- $(\exists i,j)(0\leq i\lt j\leq n\land p_i=p_j)$
			- definujeme
				- $x=a_1\dots a_i$
				- $y=a_{i+1}\dots a_j$
				- $z=a_{j+1}\dots a_m$
			- tj. $w=xyz$, $y\neq\epsilon$, $|xy|\leq n$
- Věta: Neregularita $L_{01}=\set{0^n1^n\mid n\geq 0}$
	- předpokládejme regularitu $L_{01}$
	- vezměme $m$ z pumping lemmatu
	- zvolme $w=0^m1^m$
	- rozdělme $w=xyz$ dle pumping lemmatu
		- $|xy|\leq n$ je na začátku $w$, takže obsahuje jen nuly
		- $y\neq\epsilon$
	- z pumping lemmatu $xz\in L_{01}$, což je spor, protože $xz$ obsahuje méně nul než jedniček
- Algoritmus: Hledání dosažitelných stavů
	- definice: dosažitelný stav
		- mějme DFA $A=(Q,\Sigma,\delta,q_0,F)$
		- stav $q\in Q$ je dosažitelný, existuje-li $w\in\Sigma^*$ takové, že $\delta^*(q_0,w)=q$
	- dosažitelné stavy hledáme iterativně
		- začneme s $M_0=\set{q_0}$
		- $M_{i+1}=M_i\cup\set{q\in Q:(\exists p\in M_i)(\exists x\in\Sigma)(\delta(p,x)=q)}$
		- opakujeme dokud $M_{i+1}\neq M_i$
	- korektnost
		- každé $M_i$ obsahuje pouze dosažitelné stavy
	- úplnost
		- pro dosažitelný stav $q$ mějme nejkratší takové $w$, že $\delta^*(q_0,w)=q$
			- $|w|=n$
			- $w=x_1\dots x_n$
		- zjevně $\delta^*(q_0,x_1\dots x_i)\in M_i$
		- tedy $q=\delta^*(q_0,w)\in M_n$

## Redukovaný DFA

- Definice: Kongruence
	- mějme konečnou abecedu $\Sigma$ a relaci ekvivalence $\sim$ na $\Sigma^*$
	- $\sim$ je pravá kongruence $\equiv(\forall u,v,w\in\Sigma^*):u\sim v\implies uw\sim vw$
	- $\sim$ je konečného indexu $\equiv$ rozklad $\Sigma^*/\sim$ má konečný počet tříd
	- třídu kongruence $\sim$ obsahující slovo $u$ značíme $[u]_\sim$ nebo $[u]$
	- příklady
		- relace „končí stejným písmenem“ je pravá kongruence
		- relace „mají stejný počet znaků“ není konečného indexu
- Věta: Myhill-Nerodova věta
	- věta
		- nechť $L$ je jazyk nad konečnou abecedou $\Sigma$
		- potom následující trzení jsou ekvivalentní:
			- $L$ je rozpoznatelný konečným automatem
			- existuje pravá kongruence $\sim$ konečného indexu nad $\Sigma^*$ tak, že $L$ je sjednocením jistých tříd rozkladu $\Sigma^*/\sim$
	- důkaz $\implies$
		- definujeme $u\sim v\equiv\delta^*(q_0,u)=\delta^*(q_0,v)$
		- je to ekvivalence, je to pravá kongruence
		- má konečný index (protože automat má konečně mnoho stavů)
		- $L=\set{w\in\Sigma^*:\delta^*(q_0,w)\in F}$
		- $=\bigcup_{q\in F}\set{w\in\Sigma^*:\delta^*(q_0,w)=q}$
		- $=\bigcup_{q\in F}[w\in\Sigma^*:\delta^*(q_0,w)=q]$
		- tedy $L$ je sjednocením tříd, které odpovídají přijímajícím stavům automatu
	- důkaz $\impliedby$
		- abeceda automatu bude $\Sigma$
		- za stavy $Q$ položíme třídy rozkladů $\Sigma^*/\sim$
		- počáteční stav $q_0:=[\epsilon]$
		- koncové stavy budou třídy, jejichž sjednocením je $L$
		- přechodová funkce $\delta([u],x):=[ux]$
			- je korektní z definice pravé kongruence
		- zjevně $L(A)=L$
	- použití k důkazu neregularity
		- ukážeme pro pumpovatelný jazyk slov ve tvaru $a^+b^ic^i$ nebo $b^ic^j$
		- pro regulární $L$ musí existovat pravá kongruence konečného indexu $m$
		- mějme množinu řetězců $S=\set{ab,abb,abbb,\dots,ab^{m+1}}$
		- $|S|=m+1$, tedy nutně existují dvě slova $i\neq j$, která padnou do stejné třídy
			- $ab^i\sim ab^j$
			- tedy $ab^ic^i\sim ab^jc^i$
			- ale $ab^ic^i\in L$ a $ab^jc^i\notin L$, což je spor, takže jazyk není regulární
- Definice: Automatový homomorfismus
	- nechť $A_1,A_2$ jsou DFA
	- řekneme, že zobrazení $h:Q_1\to Q_2$ je automatovým homomorfismem, jestliže:
		- $h(q_{0_1})=q_{0_2}$
		- $h(\delta_1(q,x))=\delta_2(h(q),x)$
		- $q\in F_1\iff h(q)\in F_2$
	- homomorfismus prostý a na (tzn. bijekci) nazýváme isomorfismus
- Věta: Ekvivalence automatů
	- definice: dva konečné automaty $A,B$ nad stjenou abecedou $\Sigma$ jsou ekvivalentní, jestliže rozpoznávají stejný jazyk, tj. $L(A)=L(B)$
	- věta: existuje-li homomorfismus konečných automatů $A_1$ do $A_2$, pak jsou $A_1$ a $A_2$ ekvivalentní
	- důkaz
		- zjevně $\forall w\in\Sigma^*:h(\delta^*_1(q,w))=\delta^*_2(h(q),w)$
		- dále projdeme sérií ekvivalentních výroků
			- $w\in L(A_1)$
			- $\delta_1^*(q_{0_1},w)\in F_1$
			- $h(\delta_1^*(q_{0_1},w))\in F_2$
			- $\delta_2^*(h(q_{0_1}),w)\in F_2$
			- $\delta_2^*(q_{0_2},w)\in F_2$
			- $w\in L(A_2)$
- Definice: Ekvivalence stavů
	- říkáme, že stavy $p,q\in Q$ konečného automatu $A$ jsou ekvivalentní, pokud $\forall w\in\Sigma^*:\delta^*(p,w)\in F\iff\delta^*(q,w)\in F$
	- nejsou-li dva stavy ekvivalentní, říkáme, že jsou rozlišitelné
- Algoritmus: Hledání rozlišitelných stavů v DFA
	- základ: pokud $p\in F$ a $q\notin F$, pak je dvojice $\set{p,q}$ rozlišitelná
	- indukce
		- nechť $p,q\in Q,\, a\in\Sigma$ a o dvojici stavů $\set{\delta(p,a),\delta(q,a)}$ víme, že jsou rozlišitelné, pak i $\set{p,q}$ jsou rozlišitelné
		- opakujeme, dokud existuje nějaká nová trojice $p,q,a$
	- korektnost
		- uvažujme špatné páry stavů, které jsou rozlišitelné, ale algoritmus je nerozlišil
		- vezměme z nich pár $\set{p,q}$ rozlišitelný nejkratším slovem $w=a_1\dots a_n$
		- stavy $r=\delta(p,a_1)$ a $s=\delta(q,a_1)$ jsou rozlišitelné kratším slovem $a_2\dots a_n$, takže pár není mezi špatnými
		- tedy v příštím kroku algoritmus rozliší i $p,q$
	- složitost
		- čas výpočtu je polynomiální vzhledem k počtu stavů
		- v jednom kole uvažujeme všechny páry, tj. $O(n^2)$
		- kol je maximálně $O(n^2)$, protože v každém rozlišíme aspoň jeden pár
		- dohromady $O(n^4)$, ale lze zrychlit na $O(n^2)$ pamatováním závislostí mezi stavy
- Algoritmus: Testování ekvivalence regulárních jazyků
	- testujeme ekvivalenci regulárních jazyků $L,M$
	- najdeme DFA $A_L,A_M$ takové, že
		- $L(A_L)=L$
		- $L(A_M)=M$
		- $Q_L\cap Q_M=\emptyset$
	- vytvoříme DFA sjednocením stavů a přechodů $(Q_L\cup Q_M,\Sigma,\delta_L\cup \delta_M,q_{0_L},F_L\cup F_M)$
		- není důležité, zda jako počáteční stav zvolíme $q_{0_L}$ nebo $q_{0_M}$
	- použijeme algoritmus hledání rozlišitelných stavů
	- jazyky jsou ekvivalentní $\iff$ počáteční stavy $q_{0_L},q_{0_M}$ jsou ekvivalentní
- Definice: Redukovaný DFA, redukt (viz i 2.6)
	- deterministický konečný automat je redukovaný, pokud
		- nemá nedosažitelné stavy
		- žádné dva stavy nejsou ekvivalentní
		- $\delta$ je totální
	- konečný automat $A$ je reduktem automatu $B$, pokud
		- $A$ je redukovaný
		- $A$ a $B$ jsou ekvivalentní
	- lemma: každé dva ekvivalentní redukované automaty jsou izomorfní
	- lemma: pro každý DFA, který přijímá aspoň jedno slovo, existuje redukovaný DFA, který je s ním ekvivalentní
	- důsledek: všechny redukty jednoho DFA jsou izomorfní
- Algoritmus: Nalezení reduktu DFA
	- eliminujeme nedosažitelné stavy
	- najdeme rozklad zbylých stavů na třídy ekvivalence
	- stavy nového automatu budou jednotlivé třídy
	- zkonstruujeme přechodovou funkci mezi třídami
	- počáteční stav nového automatu bude odpovídat třídě s počátečním stavem původního automatu
	- množinou přijímajících stavů budou třídy odpovídající přijímajícím stavům původního automatu
	- poznámka: pro nedeterministické konečné automaty tento algoritmus nefunguje

## Nedeterministické $\epsilon$NFA

- Definice: Nedeterministický konečný automat s $\epsilon$ přechody ($\epsilon$NFA)
- Definice: $\epsilon$-uzávěr
- Definice: $\delta^*$ pro $\epsilon$NFA
- Definice: Jazyk přijímaný $\epsilon$NFA
- Definice: Konfigurace DFA, $\epsilon$NFA
- Definice: Výpočetní strom, graf $\epsilon$NFA
- Věta: Podmnožinová konstrukce (s $\epsilon$-přechody)
- Algoritmus: Podmnožinová konstrukce (s $\epsilon$-přechody)
- Věta: Převod NFA na DFA
- Věta: Uzavřenost na množinové operace
- Definice: Řetězcové operace nad jazyky
- Věta: Uzavřenost regulárních jazyků na řetězcové operace

## Regulární výrazy

- Definice: Regulární výrazy, hodnota regulárního výrazu
- Věta: Varianta Kleeneho věty
- Definice: Substituce jazyků
- Definice: Homomorfismus jazyků, inverzní homomorfismus
- Věta: Uzavřenost na homomorfismus
- Definice: Inverzní homomorfismus
- Věta: Rozhodovací problémy pro regulární jazyky

## Gramatiky

- Definice: Formální (generativní) gramatika
- Definice: Klasifikace gramatik podle tvaru přepisovacích pravidel
- Definice: Derivace $\Rightarrow^*$
- Definice: Jazyk generovaný gramatikou $G$
- Věta: $L\in RE\implies L\in\mathcal L_3$
- Věta: $\epsilon$-NFA pro gramatiku typu 3 rozpoznávající stejný jazyk
- Definice: Levé (a pravé) lineární gramatiky
- Definice: Lineární gramatika, jazyk
- Definice: Derivační strom
- Definice: Strom dává slovo (yield)
- Definice: Levá a pravá derivace
- Věta: Ekvivalence tvrzení o derivacích
- Definice: Ekvivalence gramatik

## Chomského normální forma, CFG

- Definice: Zbytečný, užitečný, generující, dosažitelný symbol
- Definice: Nulovatelný neterminál
- Algoritmus: Převod CFG do Chomského normálního tvaru
- Definice: Jednotkové pravidlo, jednotkový pár
- Věta: Gramatika v normálním tvaru, redukovaná
- Definice: Chomského normální tvar
- Věta: Chomského normální tvar bezkontextové gramatiky
- Věta: Lemma o vkládání (pumping) pro bezkontextové jazyky
- Algoritmus: CYK algoritmus, v čase $O(n^3)$
- Věta: CYK
- Definice: Jednoznačnost a víceznačnost CFG

## Zásobníkové automaty

- Definice: Zásobníkový automat (PDA)
- Definice: Přechodový diagram pro zásobníkový automat
- Definice: Konfigurace zásobníkového automatu
- Definice: $\vdash$, $\vdash^*$ posloupnosti konfigurací
- Definice: Jazyk přijímaný koncovým stavem, prázdným zásobníkem
- Věta: L(CFG), L(PDA), N(PDA)
- Algoritmus: Konstrukce PDA z CFG
- Definice: Deterministický zásobníkový automat (DPDA)
- Věta: Zařazení $L_{DPDA}$ mezi $L_{PDA}$ a regulární jazyky
- Definice: Bezprefixové jazyky
- Věta: $L\in N(P_{DPDA})$, právě když $L$ bezprefixový a $L\in L(P'_{DPDA})$

## Uzávěrové vlastnosti

- Věta: CFL uzavřené na sjednocení, konkatenaci, iteraci, reverzi, naopak neuzavřené na průnik
- Věta: CFL i DCFL jsou uzavřené na průnik s regulárním jazykem
- Věta: CFL jsou uzavřené na substituci a homomorfismus
- Věta: CFL jsou uzavřené na inverzní homomorfismus
- Věta: Odečtení regulárního jazyka
- Věta: CFL nejsou uzavřené na doplněk ani rozdíl

## Turingův stroj

- Definice: Turingův stroj
- Definice: Konfigurace Turingova stroje
- Definice: Krok Turingova stroje
- Definice: TM přijímá jazyk, rekurzivně spočetný jazyk
- Definice: Přechodový diagram pro TM
- Definice: Vícepáskový Turingův stroj
- Věta: Vícepáskový Turingův stroj
- Definice: Nedeterministický TM
- Věta: Nedeterministický TM
- Věta: TM s jednosměrnou páskou

## LBA, diagonální jazyk

- Definice: Separovaná gramatika
- Definice: Monotónní (nevypouštějící) gramatika
- Definice: Lineárně omezený automat (LBA)
- Věta: Každý kontextový jazyk lze přijímat pomocí LBA
- Věta: LBA přijímají pouze kontextové jazyky
- Věta: Rekurzivně spočetné jsou $\mathcal L_0$
- Věta: Každý jazyk typu 0 je rekurzivně spočetný
- Definice: TM zastaví
- Definice: Rekurzivní jazyky
- Definice: Diagonální jazyk
- Definice: Univerzální jazyk
- Věta: Existence univerzálního Turingova stroje
- Věta: Postova věta
- Věta: Nerozhodnutelnost univerzálního jazyka

## Nerozhodnutelné problémy

- Definice: Rozhodnutelný problém
- Definice: Redukce problému
- Věta: Redukce problému
- Věta: Problém zastavení není rozhodnutelný

## Časová složitost

- Definice: Časová složitost
- Definice: (Asymptotická) horní hranice $O(g(n))$
- Definice: Třída časové složitosti
- Definice: Notace malé $o$
- Definice: Doba běhu nedeterministického TM
- Věta: Převod mezi časovou složitostí pro deterministický a nedeterministický TM
- Definice: Třída $P$
- Věta: $CFL\subseteq P$
- Definice: Verifikátor
- Definice: Třída $NP$
- Definice: Polynomiálně vyčíslitelná funkce, převoditelný jazyk, polynomiální redukce
- Definice: SAT, 3SAT
- Definice: NP úplnost
- Věta: Cook-Levinova věta
- Věta: 3SAT je NP-úplný

## co-NP, prostorová složitost

- Definice: co-NP
- Věta: Problém tautologičnosti je co-NP
- Definice: Prostorová složitost
- Definice: Třídy prostorové složitosti
- Věta: Savitchova věta
- Definice: PSPACE
- Věta: Prostorové a časové třídy
