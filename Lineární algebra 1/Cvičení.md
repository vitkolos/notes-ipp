# Lineární algebra: cvičení

- http://elif.cz/LA_2223_2.html
- elif@kam.mff.cuni.cz
- zápočet
	- písemky + aktivita
		- na začátku každého cvičení písemka na 5–10 minut, za každou lze získat 10 bodů (celkem 110)
		- za aktivitu v hodině lze získat dohromady 10 bodů
		- celkem alespoň 60 ze 120 bodů
	- domácí úkoly
		- alespoň 60 ze 120 bodů
		- na webu
		- ideálně jako jeden soubor
		- když pošleme dřív, tak nám může dát možnost si to opravit
		- deadline je začátek následujícího cvičení
	- když budeme mít víc než 80 bodů, tak bude na konci semestru možnost to nějak vyřešit

- popis přímky v rovině
	- obecná rovnice
		- ax + by + c = 0
		- $(a,b) \neq (0,0)$
		- (a, b) je normálový vektor
	- parametrický popis
		- $(a,b)+t\cdot (u,v)=(x,y), t \in \mathbb{R}$
		- $(u,v) \neq (0,0)$
- popis roviny v prostoru ($\mathbb{R^3}$)
	- $ax+by+cz+d=0$
		- $(a,b,c)\neq (0,0,0)$
	- $(x,y,z)=(a,b,c)+s\cdot (u_1,u_2,u_3)+t\cdot (v_1, v_2,v_3), s, t \in R$
		- $(u_1,u_2,u_3)\neq (0,0,0)$
		- $(v_1,v_2,v_3)\neq (0,0,0)$
		- jeden vektor se nesmí rovnat k-násobku druhého
	- převod z parametrického popisu na obecnou rovnici se provádí nalezením vektoru kolmého (normálového) k oběma známým vektorům
	- převod z obecné rovnice na parametrický popis se provádí nalezením libovolného bodu v rovině a dále nalezením dvou libovolných (různých) vektorů kolmých na normálový vektor
- přímka v prostoru
	- parametricky pomocí jednoho nenulového vektoru
	- rovnicový popis (jako průnik dvou rovin) – neobjeví se teďka na písemce
		- každá rovina obecnou rovnicí
		- normálové vektory rovin nesmějí být nulové, jeden nesmí být k-násobkem druhého
- kolmost vektorů – jejich skalární součin je nulový

- 1.2 najděte rovnicové vyjádření roviny popsané bodem (3,2,1) a směrovými vektory (1,1,1) a (2,-1,0)
	- je potřeba najít normálový vektor
- 1.3 najděte parametrický popis roviny $2x_1 + 3x_2 + x_3 = 4$
	- existuje více řešení

### Gaussova eliminační metoda

matice soustavy vs. rozšířená matice soustavy (s pravými stranami rovnic)
elementární úpravy
odstupňovaný tvar (REF)

- pokud je matice v REF (o m řádcích a n sloupcích)
	- pak existsuje řádek r, kde první až r-tý řádek jsou nenulové, řádky r + 1 až m jsou nulové
	- pro $p_i=min\{j:a_{ij} \pm 0\}$ platí p1 < p2 < ... < pr
	- pozice (1,p1) ... (r,pr) nazýváme pivoty
	- hodnost matice rank(A) je počet nenulových řádků REF(A)
- redukovaný odstupňovaný tvar (RREF)
	- REF a navíc $a_{1p_1} = a_{rp_r} = 1$
	- $\forall i \in \{1 ... r\}: a_{1p_i} = a_{2p_i} = a_{(i-1)p_1} = 0$
- počítání viz sešit
- na příští písemce pouze analytika (bez Gaussovky)
- doma spočítat úkol, dále 2c a připravit se na písemku