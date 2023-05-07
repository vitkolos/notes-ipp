# Bonusový test

## Definice (37)

*definujte…*

- permutace
	- permutace na množině $\lbrace1,2,\dots,n\rbrace$ je bijektivní zobrazení $p:\lbrace1,2,\dots,n\rbrace\rightarrow \lbrace1,2,\dots,n\rbrace$
- znaménko permutace
	- znaménko permutace $p$ je $\text{sgn}(p)=(-1)^{\text{počet inverzí}\ p}$
	- permutace s kladným znaménkem jsou sudé, se záporným liché
	- v exponentu může být \# inverzí, \# transpozic, \# sudých cyklů, $n-$\# cyklů
- determinant
	- determinant matice $A\in\mathbb K^{n\times n}$ je dán výrazem $$\text{det }A=\sum_{p\in S_n}\text{sgn}(p)\prod_{i=1}^na_{i,p(i)}$$
- adjungovaná matice
	- $A^{ij}$ je podmatice získaná z $A$ odstraněním $i$-tého řádku a $j$-tého sloupce
	- pro $A\in\mathbb K^{n\times n}:(\text{adj }A)_{ji}=(-1)^{i+j}\cdot\text{det }A^{ij}$
	- tzn. faktory Laplaceova rozvoje podél i-tého řádku matice $A$ ukládáme do i-tého sloupce $\text{adj }A$
- Laplaceova matice
	- Laplaceova matice grafu $G$ na $V_G=\lbrace v_1,\dots,v_n\rbrace$ je $L_G\in\mathbb R^{n\times n}$ taková, že $$(L_G)_{ij}= \begin{cases} \text{deg}(v_i) &\text{pro } i=j \\ -1 &\text{jestliže }i\neq j\land (v_i,v_j)\in E_G \\ 0 &\text{jinak}\end{cases}$$
- polynom nad tělesem
	- polynom stupně $n$ v proměnné $x$ nad tělesem $\mathbb K$ je výraz $p(x)=a_nx^n+a_{n-1}x^{n-1}+\dots+a_2x^2+a_1x+a_0$, kde $a_n\neq 0$ a $a_n,\dots,a_0\in\mathbb K$
	- píšeme $p\in\mathbb K(x)$
- kořen polynomu a jeho násobnost
	- kořen polynomu $p\in\mathbb K(x)$ je $r\in\mathbb K$ takové, že $p(r)=0$
	- násobnost kořene $r$ z $p\in\mathbb K(x)$ je největší kladné celé číslo $k$ takové, že $(x-r)^k$ dělí $p$
- algebraicky uzavřené těleso
	- pokud každý polynom $p\in\mathbb K(x)$ stupně alespoň jedna má alespoň jeden kořen, pak je těleso $\mathbb K$ algebraicky uzavřené
- Vandermondova matice
	- značí se $V_{n+1}(x_0,\dots,x_n)$, přičemž prvky jsou určeny takto: $v_{ij}=x_{i-1}^{j-1}$ 
- vlastní číslo a vlastní vektor lineárního zobrazení
	- mějme vektorový prostor $V$ nad tělesem $\mathbb K$ a lineární zobrazení $f:V\to V$
	- vlastní číslo zobrazení $f$ je jakékoliv $\lambda\in\mathbb K$, pro které existuje vektor $u\in V\setminus 0$ takový, že $f(u)=\lambda u$
	- vlastní vektor odpovídající vlastnímu číslu $\lambda$ je libovolný vektor $u\in V$ takový, že $f(u)=\lambda u$
	- množina všech vlastních čísel matice je jejím spektrem
- vlastní číslo a vlastní vektor matice
	- mějme vektorový prostor $V$ nad tělesem $\mathbb K$ a matici $A\in\mathbb K^{n\times n}$
	- vlastní číslo matice $A$ je jakékoliv $\lambda\in\mathbb K$, pro které existuje vektor $x\in V\setminus 0$ takový, že $Ax=\lambda x$
	- vlastní vektor odpovídající vlastnímu číslu $\lambda$ je libovolný vektor $x\in V$ takový, že $Ax=\lambda x$
	- množina všech vlastních čísel matice je jejím spektrem
- charakteristický polynom
	- charakteristický polynom matice $A\in\mathbb K^{n\times n}$ je $p_A(t)=\text{det}(A-tI_n)$
- algebraická násobnost vlastního čísla
	- odpovídá násobnosti daného vlastního čísla jako kořene charakteristického polynomu
- geometrická násobnost vlastního čísla
	- geometrická násobnost vlastního čísla je dimenze podprostoru jeho vlastních vektorů
- podobné matice
	- matice $A,B\in\mathbb K^{n\times n}$ jsou si podobné, pokud existuje regulární matice $R$ taková, že $A=R^{-1}BR$
- diagonalizovatelná matice
	- matice podobná diagonální matici je diagonalizovatelná
- Jordanův blok
	- Jordanův blok je čtvercová matice, která má na hlavní diagonále dané vlastní číslo, na diagonále nad ní má jedničky a všude jinde má nuly
- Jordanův normální tvar matice
	- matice v Jordanově normálním tvaru má na diagonále Jordanovy bloky (a všude jinde nuly)
- zobecněný vlastní vektor
	- zobecněný vlastní vektor matice $A$ k vlastnímu číslu $\lambda$ je libovolný vektor $x$ splňující $(A-\lambda I)^ix=0$ pro nějaké $i\in\mathbb N$
	- lze je řadit do řetězců $x_k,\dots,x_2,x_1,0$, kde $(A-\lambda I)x_i=x_{i-1}$
- hermitovská matice
	- hermitovská transpozice komplexní matice $A\in\mathbb C^{m\times n}$ je matice $A^H\in\mathbb C^{n\times m}$, kde $(A^H)_{ij}=\overline{a_{ji}}$
	- matice $A$ je hermitovská, pokud $A=A^H$
- unitární matice
	- matice $A$ je unitární, pokud $A^{-1}=A^H$
- skalární součin pro vektorové prostory nad komplexními čísly
- norma spojená se skalárním součinem
- kolmé vektory
- ortonormální báze
- Fourierovy koeficienty
- kolmá projekce
- izometrie
- ortogonální doplněk
- Gramova matice
- pozitivně definitní matice
- Choleského rozklad
- bilineární forma
- kvadratická forma
- matice bilineární formy vzhledem k bázi
- analytické vyjádření formy
- signatura formy

## Věty a důkazy (30)

*vyslovte a dokažte… / uveďte a dokažte…*

- věta o linearitě determinantu
- věta o determinantu součinu dvou matic
- věta o Laplaceově rozvoji determinantu
- Cramerovo pravidlo (řešení systémů s determinanty)
- věta o adjungované matici
- věta o počtu koster grafu
- malá Fermatova věta
- věta o Vandermondově matici
- správnost Lagrangeovy interpolace
- věta o podprostoru vlastních vektorů
- věta o lineární nezávislosti vlastních vektorů
- věta o kořenech charakteristického polynomu
- Cayley-Hamiltonova věta
- nezbytná a postačující podmínka, kdy je matice diagonalizovatelná
- věta o diagonalizaci speciálních komplexních matic
- Cauchy-Schwarzova nerovnost
- trojúhelníková nerovnost
- věta o Fourierových koeficientech
- správnost Gram-Schmidtovy ortonormalizace (včetně lemmatu, pokud jej potřebujete)
- věta o izometrii a normě
- věta o izometrii a vlastnostech její matice
- věta o ortogonálním doplňku
- věta o skalárním součinu dvou vektorů a Gramově matici
- věta o třech ekvivalentních podmínkách pro pozitivně definitní matice
- věta o rekurentní podmínce pro pozitivně definitní matice
- věta o pozitivně definitních maticích a determinantech
- správnost algoritmu pro výpočet Choleského rozkladu
- věta o diagonalizovatelnosti matic forem
- Sylvesterův zákon setrvačnosti — o diagonalizaci kvadratických forem
- věta o počtu přímek svírajících stejný úhel

## Přehledy (14)

*přehledově sepište, co víte o… (uveďte definice, tvrzení, věty, příklady a souvislosti – důkazy nejsou vyžadovány)*

- výpočet determinantů
- determinanty a jejich geometrický význam
- počet koster grafu
- polynomy
- vlastní čísla a vlastní vektory
- charakteristický polynom a jeho koeficienty
- podobné matice a diagonalizace
- speciální komplexní matice
- skalární součin a související norma
- ortogonalita a kolmá projekce
- ortonormální báze
- ortogonální doplněk
- pozitivně definitní matice
- bilineární a kvadratické formy a jejich matice
