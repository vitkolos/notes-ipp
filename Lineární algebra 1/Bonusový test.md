# Bonusový test

## Definice (38)

*definujte…*

- rozšířená matice soustavy
	- soustava m lineárních rovnic o n neznámých … Ax = b
	- rozšířená matice soustavy … $(A|b) \in \mathbb{R}^{m×(n+1)}$
	- matice soustavy … $A \in \mathbb{R}^{m×n}$
	- vektor pravých stran … $b \in \mathbb{R}^m$
	- vektor neznámých … $x = (x_1,\dots,x_n)^T$
	- vektor $x \in \mathbb{R}^n$ je řešení soustavy Ax = b, pokud splňuje všechny její rovnice
	- soustavy Ax = 0 se nazývají homogenní a vždy umožňují x = 0
- elementární řádkové operace
	- definujeme základní dvě elementární řádkové úpravy
		- vynásobení i-tého řádku nenulovým $t \in R \setminus \{0\}$
		- přičtení j-tého řádku k i-tému řádku
	- z těch lze odvodit další dvě úpravy
		- přičtení t-násobku ($t \in R$) j-tého řádku k i-tému řádku
		- záměna dvou řádků
	- provedení jedné elementární úpravy značíme $A\sim A'$
	- provedení posloupnosti úprav značíme $A\sim\sim A'$
- odstupňovaný tvar matice
	- matice je v řádkově odstupňovaném tvaru (REF = row echelon form), pokud jsou nenulové řádky seřazeny podle počtu počátečních nul a nulové řádky jsou pod nenulovými
	- první nenulový prvek nenulového řádku se nazývá pivot, pod pivotem jsou v REF všechny prvky nulové
- napište pseudokód pro Gaussovu eliminaci
	- // input: matice A
	- // output: matice A v REF
	- foreach i do určete j(i)
		- // j(i) = sloupec s pivotem daného řádku, $j(i) = min\{j: a_{i,j}\neq 0\}$
		- // prázdný řádek má j(i) = $\infty$
	- seřaďte řádky A podle j(i)
	- forever
		- if $\exists i: j(i) = j(i+1) \lt \infty$ then
			- // i-tý a (i+1)-ní řádky jsou nenulové a mají stejně počátečních nul
			- přičtěte $–a_{i+1,j(i)}/a_{i,j(i)}$-násobek i-tého řádku
			- // nyní je prvek ve sloupci j(i) řádku i+1 nulový
			- aktualizujte j(i + 1) a zařaďte (i + 1)-tý řádek na místo
		- else
			- // všechny nenulové řádky mají různý počet počátečních nul
			- return A
	- // konečnost: v každé iteraci roste celkový počet počátečních nul
- volné a bázické proměnné
	- pro soustavu $A'x = b'$ s A' v REF jsou proměnné odpovídající sloupcům s pivoty bázické, ostatní jsou volné
- hodnost matice
	- hodnost matice A, značená jako rank(A), je počet pivotů v libovolné A' v REF takové, že $A\sim\sim A'$
- jednotková matice
	- pro $n \in \mathbb{N}$ je jednotková matice $I_n \in \mathbb{R}^{n×n}$ definovaná tak, že $(I_n)_{i,j} = 1 \iff i=j$, ostatní prvky jsou nulové 
- transponovaná matice
	- transponovaná matice k matici $A \in \mathbb{R}^{m×n}$ je matice $A^T \in \mathbb R^{n×m}$ splňující $(A^T)_{i,j}=a_{j,i}$
- symetrická matice
	- čtvercová matice A je symetrická, pokud $A^T =A$, tedy $a_{i,j}=a_{j,i}$
- maticový součin
- inverzní matice
- regulární matice
- definujte binární operaci
- definujte komutativní a asociativní binární operace
- neutrální prvek
- inverzní prvek
- grupa
- permutace
- transpozice
- inverze v permutaci
- znaménko permutace
- těleso
- charakteristika tělesa
- vektorový prostor
- podprostor vektorového prostoru
- lineární kombinace
- lineární obal (podprostor generovaný množinou)
- řádkový a sloupcový prostor matice
- jádro matice
- lineárně nezávislé vektory
- báze vektorového prostoru
- dimenze vektorového prostoru
- vektor souřadnic
- lineární zobrazení
- matice lineárního zobrazení
- matice přechodu
- izomorfismus vektorových prostorů
- afinní prostor a jeho dimenze

## Věty a důkazy (15)

*vyslovte a dokažte… / uveďte a dokažte…*

- vztah mezi elementárními řádkovými operacemi a soustavami rovnic
- věta o jednoznačnosti volných a bázických proměnných
- Frobeniova věta
- věta o vztahu mezi řešeními Ax = b a Ax = 0
- věta popistující všechna řešení Ax = b
- věta o ekvivalentních definicích regulárních matic
- věta o znaménku složené permutace
- věta charakterizující, kdy $\mathbb{Z}_n$ je těleso
- malá Fermatova věta
- věta o průniku vektorových prostorů
- věta o ekvivalentních definicích lineárního obalu
- Steinitzova věta o výměně (včetně lemmatu, pokud jej potřebujete)
- věta o jedinečnosti lineárního zobrazení
- věta o charakterizaci izomorfismu mezi vektorovými prostory
- věta o vektorových prostorech souvisejících s maticí A

## Přehledy (13)

*přehledově sepište, co víte o…*

*uveďte definice, tvrzení, věty, příklady a souvislosti – důkazy nejsou vyžadovány*

- elementární řádkové operace a Gaussova eliminaci
- řešení homogenních a nehomogenních soustav lineárních rovnic
- maticové operace
- regulární a singulární matice
- binární operace a jejich vlastnosti
- (obecné) grupy
- permutační grupy
- tělesa
- vektorové prostory a jejich podprostory
- vektorové prostory určené maticí A
- lineární závislost
- báze vektorových prostorů
- lineární zobrazení a jejich matice
