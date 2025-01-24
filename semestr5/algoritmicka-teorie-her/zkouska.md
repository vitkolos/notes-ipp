# Zkouška

## Normal-form games

- Definition: Normal-form game
	- hra v normální tvaru je trojice $(P,A,u)$
	- $P$ … konečná množina $n$ hráčů
	- $A=A_1\times\dots\times A_n$ je množina akčních profilů
		- $A_i$ … množina akcí $i$-tého hráče
	- $u=(u_1,\dots,u_n)$, kde $u_i:A\to\mathbb R$ je užitková funkce $i$-tého hráče
- Definition: Strategies
	- čistá (pure) strategie $s_i$ hráče $i$ je akce z $A_i$
		- profil čistých strategií je $n$-tice čistých strategií (akcí) – za každého z $n$ hráčů je tam jedna
	- smíšená (mixed) strategie $s_i$ hráče $i$ je pravděpodobnostní distribuce přes $A_i$
		- tedy $s_i(a_i)\in[0,1]$ a $\sum_{a_i\in A_i}s_i(a_i)=1$
		- profil smíšených strategií je $n$-tice smíšených strategií
	- každá čistá strategie je smíšená
- Definition: Expected payoff
	- ve hře $G=(P,A,u)$ je expected payoff (střední hodnota výplatní funkce) pro hráče $i$ z profilu smíšených strategií $s$ je $$u_i(s)=\sum_{a\in A} u_i(a)\cdot \underbrace{\prod_{j=1}^n s_j(a_j)}_{P(a)}$$
	- platí linearita střední hodnoty výplatní funkce $$u_i(s)=\sum_{a_i\in A_i} s_i(a_i)\cdot u_i(a_i;s_{-i})$$
- Example: Five basic games
	- vězňovo dilema
	- matching pennies
	- battle of sexes
	- game of chicken
	- bitva o duši Gothamu

## Nash equilibrium

- Definition: Best response
	- best response $i$-tého hráče na strategický profil $s_{-i}$ je smíšená strategie $s_i^*$ taková, že $$\forall s_i'\in S_i:u_i(s_i^*;s_{-i})\geq u_i(s_i';s_{-i})$$
	- kdyby hráč $i$ znal strategie ostatních, zvolil by si strategii $s_i^*$, protože maximalizuje jeho očekávanou výplatu, pokud ostatní hrají $s_{-i}$
- Definition: Nash equilibrium
	- mějme hru $G=(P,A,u)$ v normální tvaru s $n$ hráči
	- pak Nashovo ekvilibrium (NE) ve hře $G$ je strategický profil $(s_1,\dots,s_n)$ takový, že $s_i$ je best response hráče $i$ na $s_{-i}$ pro každé $i\in P$
	- tedy žádný hráč by neměnil svou strategii, kdyby znal strategie ostatních
- Theorem: Nash’s Theorem
	- Nashova věta: každá hra v normálním tvaru má Nashovo ekvilibrium
	- $X\subseteq\mathbb R^d$ je kompaktní, pokud je uzavřená a omezená
	- $Y\subseteq\mathbb R^d$ je konvexní, pokud $\forall\alpha\in [0,1]:\alpha x+(1-\alpha)y\in Y$
	- pro $n$ afinně nezávislých bodů $x_1,\dots,x_n\in\mathbb R^d$ definujeme $(n-1)$-simplex $\Delta_n$ na $x_1,\dots,x_n$ jako množinu konvexních kombinací bodů $x_1,\dots,x_n$
		- každý simplex je kompaktní konvexní množina v $\mathbb R^d$
	- lemma: pokud $K_1,\dots,K_n$ jsou kompaktní množiny a $\forall i:K_i\subseteq\mathbb R^{d_i}$, pak $K_1\times\dots\times K_n$ je kompaktní množina v $\mathbb R^{d_1+\dots+d_n}$
	- Brouwerova věta o pevném bodu: pokud $K\subseteq\mathbb R^d$ je neprázdná kompaktní konvexní množina a $f:K\to K$ je spojité zobrazení, pak existuje pevný bod $x_0\in K$ pro $f$, tedy $f(x_0)=x_0$
	- důkaz Nashovy věty
		- nechť $K=S_1\times\dots\times S_n$ je množina všech smíšených strategií
			- $S_i$ … množina smíšených strategií hráče $i$
			- každá množina $S_i$ je simplex, takže je kompaktní a konvexní
			- proto i $K$ je kompaktní
			- pro libovolné $s,s'\in K$ a $\alpha\in[0,1]$ je $\alpha s+(1-\alpha)s'$ také smíšený strategický profil v $K$, tedy $K$ je konvexní
		- pro hráče $i\in S$ a akci $a_i\in A$ definujeme zobrazení $\varphi_{i,a_i}:K\to\mathbb R$ tak, že $\varphi_{i,a_i}(s)=\max\set{0,u_i(a_i;s_{-i})-u_i(s)}$
			- tato funkce vyjadřuje, o kolik by si hráč polepšil, kdyby místo $s_i$ hrál akci $a_i$ (pokud by si nepolepšil, je nulová)
			- z definice $u_i$ je toto zobrazení spojité
		- pro $s\in K$ definujeme nový „vylepšený“ strategický profil $s'\in K$ tak, že přidáme pravděpodobnost akcím, které jsou lepšími odpověďmi na $s_{-i}$
			- $s'_i(a_i)=\frac{s_i(a_i)+\varphi_{i,a_i}(s)}{\sum_{b_i\in A_i}(s_i(b_i)+\varphi_{i,b_i}(s))}=\frac{s_i(a_i)+\varphi_{i,a_i}(s)}{1+\sum_{b_i\in A_i}\varphi_{i,b_i}(s)}$
			- ve jmenovateli je normalizační konstanta
		- pak definujeme $f:K\to K$ tak, že nastavíme $f(s)=s'$
			- $f$ je spojitá, protože $\varphi$ jsou spojité
			- podle Brouwerovy věty má $f$ pevný bod
		- pokud je $s\in K$ Nashovo ekvilibrium, pak všechny $\varphi$ jsou nulové a $f(s)=s$, tedy $s$ je pevný bod funkce $f$
		- pokud je $s\in K$ pevným bodem funkce $f$…
			- zvolíme libovolného hráče $i\in P$
			- v supportu $s_i$ existuje akce $a_i'\in A_i$ taková, že $u_i(a'_i;s_{-i})\leq u_i(s)$
				- jinak by platilo $u_i(s)\lt\sum_{a_i}s_i(a_i)u_i(a_i;s_{-i})$, což je spor s linearitou střední hodnoty výplatní funkce
				- support $s_i$ … akce $\in A_i$, které $s_i$ nemapuje na nulu
			- pro tuto akci $a_i'$ nutně platí $\varphi_{i,a_i'}=0$ (díky té nerovnosti)
			- tak získáme $s'_i(a'_i)=\frac{s_i(a'_i)}{1+\sum_{b_i\in A_i}\varphi_{i,b_i}(s)}$
			- $s$ je pevný bod, proto $s_i'(a_i')=s_i(a_i')$, tedy ve jmenovateli musí být jednička a suma bude nulová
			- proto $u_i(s)\geq u_i(b_i;s_{-i})$ pro každé $b_i\in A_i$
			- z toho vyplývá, že pro libovolnou smíšenou strategii $s_i''\in S_i$ platí $$u_i(s_i'';s_{-i})=\sum_{b_i\in A_i} s_i''(b_i)u_i(b_i;s_{-i})\leq\sum_{b_i\in A_i} s''_i(b_i)u_i(s)=u_i(s)$$
				- levá rovnost z linearity, nerovnost z nerovnosti výše, pravá rovnost z jednotkového součtu pravděpodobností
			- tedy $s_i$ je best response hráče $i$ na $s_{-i}$ a $s$ je smíšené Nashovo ekvilibrium hry $G$
- Definition: Pareto optimality
	- strategický profil $s$ v $G$ Pareto dominuje $s'$, píšeme $s'\prec s$, pokud…
		- $\forall i\in P:u_i(s)\geq u_i(s')$
		- $\exists j\in P:u_j(s)\gt u_j(s')$
	- $\prec$ je částečná uspořádání množiny $S$ všech strategických profilů hry $G$
	- za nejlepší výsledky $G$ se považují maxima $S$ podle $\prec$
	- strategický profil $s\in S$ je Pareto optimální, pokud neexistuje jiný profil, který ho dominuje
		- ve hrách nulového součtu jsou všechny strategické profily Pareto optimální
		- ne všechna Nashova ekvilibria jsou Pareto optimální (viz vězňovo dilema)

## Zero-sum games

- Definition: Zero-sum game and its representation
	- $G=(P,A=A_1\times A_2,u)$
	- $\forall a\in A:u_1(a)+u_2(a)=0$
	- pokud $|A_1|=m$ a $|A_2|=n$, pak můžeme $G$ reprezentovat pomocí výplatní matice $M\in\mathbb R^{m\times n}$, kde $M_{ij}=u_1(i,j)=-u_2(i,j)$
	- pro strategický profil $(s_1,s_2)$ uvažujeme vektory smíšených strategií $x,y$ takové, že $x_i=s_1(i)$ a podobně $y_i=s_2(j)$
	- pak platí $u_1(s)=x^TMy=-u_2(s)$
- Definition: Worst-case optimal strategies
	- best response druhého hráče je vektor $y\in S_2$, který minimalizuje $x^TMy$
	- best response prvního hráče je vektor $x\in S_1$, který maximalizuje $x^TMy$
	- $\beta(x)=\min_{y\in S_2}x^TMy$ je nejlepší očekávaný payoff druhého hráče proti $x$
	- $\alpha(y)=\max_{x\in S_1} x^TMy$ je nejlepší očekávaný payoff prvního hráče proti $y$
	- strategický profil $(x,y)$ je NE, právě když $\beta(x)=x^TMy=\alpha(y)$
	- pokud první hráč předpokládá, že druhý hráč vždy zvolí best response na každou jeho strategii, a snaží se maximalizovat payoff za tohoto předpokladu, zvolí strategii $\overline x\in S_1$ 
		- pro tuto „worst-case optimal strategy“ platí $\beta(\overline x)=\max_{x\in S_1}\beta(x)$
	- podobně worst-case optimal strategy je taková strategie $\overline y\in S_2$, že $\alpha(\overline y)=\min_{y\in S_2}\alpha(y)$
- Theorem: Worst-case optimal strategies and NE
	- lemma
		1. $(\forall x\in S_1)(\forall y\in S_2):\beta(x)\leq x^TMy\leq\alpha(y)$
		2. pokud je strategický profil $(x^*,y^*)$ Nashovým ekvilibriem, pak jsou obě strategie worst-case optimální
		3. libovolné strategie $x^*\in S_1$ a $y^*\in S_2$ splňující $\beta(x^*)=\alpha(y^*)$ tvoří Nashovo ekvilibrium $(x^*,y^*)$
	- důkaz
		1. přímo z definice $\beta,\alpha$ (jedno definujeme jako minimum, druhé jako maximum)
		2. z (1) vyplývá $\forall x\in S_1:\beta(x)\leq\alpha(y^*)$
			- $(x^*,y^*)$ je NE, proto $\beta(x^*)=\alpha(y^*)$
			- tedy $\forall x\in S_1:\beta(x)\leq \beta(x^*)$
			- proto $x^*$ je worst-case optimální pro prvního hráče, podobně $y^*$ pro druhého hráče
		3. pokud $\beta(x^*)=\alpha(y^*)$, pak (1) implikuje $\beta(x^*)=(x^*)^TMy^*=\alpha(y^*)$
- Theorem: The Duality Theorem
- Theorem: The Minimax Theorem

## Bimatrix games

- Definition: Bimatrix game, nondegenerate bimatrix game
- Theorem: Best response condition
- Algorithm: Support enumeration
- Definition: Best response polyhedra, best response polytope
- Theorem: NE and Best response polyhedra/polytope
- Algorithm: Vertex enumeration
- Algorithm: Lemke–Howson algorithm
- Theorem: Computational complexity of NASH

## Other notions of equilibria

- Definition: $\varepsilon$-Nash equilibrium
- Theorem: Algorithmic aspects of $\varepsilon$-Nash equilibria
- Definition: Correlated equilibrium (CE)
- Theorem: Properties of correlated equilibria

## Regret minimization

- Definition: Regret minimization model
- Definition: External regret
- Theorem: External regret as a suitable metric
- Algorithm: Greedy algorithm
- Algorithm: Randomized greedy algorithm
- Algorithm: Polynomial weights algorithm
- Algorithm: No-regret dynamics

## Applications of regret minimization

- Theorem: Modern proof of the Minimax Theorem
- Definition: Coarse correlated equilibrium (CCE)
- Theorem: Converging to CCE
- Definition: Internal and swap regret
- Algorithm: No-swap-regret dynamics
- Theorem: Reduction from external regret to swap regret
- Theorem: Converging to CE

## Games in extensive form

- Definition: Extensive game, (im)perfect-information game
- Definition: Strategies in extensive games
- Definition: Games of perfect recall, Kuhn’s theorem
- Definition: Sequence form
- Theorem: Using the sequence form to find NE

## Mechanism design

- Definition: Single item auction
- Definition: Dominant strategy, social surplus, awesome auction
- Theorem: Vickrey’s auction is awesome
- Definition: Single parameter environment
- Example: Some single parameter environments
- Theorem: Myerson’s lemma

## Applications of mechanism design

- Definition: Social surplus, Bayesian model
- Theorem: Maximizing expected revenue
- Theorem: Vickrey with reserve price is optimal
- Theorem: The Bulow–Klemperer theorem
- Definition: Knapsack auction
- Theorem: 2-approximation for knapsack auctions
- Definition: Multi-parameter mechanism design
- Theorem: VCG mechanism
- Theorem: Revelation principle
