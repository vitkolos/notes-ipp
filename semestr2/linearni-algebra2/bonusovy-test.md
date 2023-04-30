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
	- pro graf $G$ o $n$ vrcholech je $L_G\in\mathbb Z^{n\times n}$ Laplaceova matice taková, že $$(L_G)_{ij}= \begin{cases} \text{deg}(v_i) &\text{pokud } i=j \\ -1 &\text{pro }v_i,v_j\text{ sousední} \\ 0 &\text{jinak}\end{cases}$$
- polynom nad tělesem
- kořen polynomu a jeho násobnost
- algebraicky uzavřené těleso
- Vandermondova matice
- vlastní číslo a vlastní vektor lineárního zobrazení
- vlastní číslo a vlastní vektor matice
- charakteristický polynom
- algebraická násobnost vlastního čísla
- geometrická násobnost vlastního čísla
- podobné matice
- diagonalizovatelná matice
- Jordanův blok
- Jordanův normální tvar matice
- zobecněný vlastní vektor
- hermitovská matice
- unitární matice
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
