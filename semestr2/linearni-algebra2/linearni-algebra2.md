# Lineární algebra 2

- skalární součin vektorů
	- definujeme jako maticový součin řádkového a sloupcového vektoru
	- odpovídá součinu velikostí vektorů a kosinu úhlu, který svírají
	- vektory jsou kolmé, právě když je jejich skalární součin roven nule
	- eukleidovská norma vektoru = zobecnění Pythagorovy věty pro n-složkový vektor … $||x||=\sqrt{x^Tx}=\sqrt{\sum_{i=0}^n x_i^2}$
	- vlastnosti skalárního součinu
	- skalární součin nad $\mathbb R$ je zobrazení, splňuje čtyři vlastnosti
	- omezujeme se na reálná čísla, protože je umíme porovnávat
		- kvůli vlastnosti $\langle x,x\rangle\geq 0$
	- ze symetrie a linearity v první složce vyplývá linearita v druhé složce
	- pokud je alespoň jedním činitelem nulový vektor, vyjde nula
- komplexní skalární součin
	- trochu jiné vlastnosti – jedna z nich obsahuje komplexně sdružené číslo
- …
- norma (indukovaná skalárním součinem) a kolmost
- existují různé skalární součiny – my většinou používáme ten standardní
- Pythagorova věta
	- pokud $x,y\in V$ jsou kolmé, tak platí
	- $||x+y||^2=||x||^2+||y||^2$
	- důkaz
- Cauchyho-Schwarzova nerovnost
	- důkaz reálného případu
- trojúhelníková nerovnost
- norma obecně
- p-norma
	- ne všechny normy jsou indukované skalárním součinem
	- typicky se používá $p$ rovno $1,2,\infty$
	- funguje to pro $p\geq 1$
- jednotková koule
- ortogonální a ortonormální systém
	- ortogonální – systém na sebe kolmých vektorů
	- ortonormální – ortogonální systém, kde norma všech vektorů je jedna
	- ortogonální systém lze zortonormalizovat, pokud tam není nulový vektor, a to tak, že všechny vektory vydělím normou
	- kanonická báze v prostoru $\mathbb R^n$ je ortonormální
- je-li systém ortonormální, pak je lineárně nezávislý (důkaz „trikem“, použiju skalární součin lineární kombinace všech vektorů systému s libovolným vektorem systému)
- Fourierovy koeficienty, Fourierův rozvoj – vyjádření vektoru vůči ortonormální bázi prostoru
- Gramova-Schmidtova ortogonalizace – ortonormální bázi sestrojím postupným nakolmováním vektorů (od vektoru $x_k$ odečtu projekci do lineárního obalu vektorů $x_1,\dots,x_n$)
- každý konečně generovaný prostor se skalárním součinem má ortonormální bázi (platí pro prostory s konečnou dimenzí)
- tvrzení o skalárním součinu vyplývajícím z báze
- libovolný skalární součin je standardní skalární součin vůči určité bázi (pro ten standardní je bází kanonická báze)
	- podobně to platí pro normu indukovanou skalárním součinem
- ortogonální doplněk množiny – všechny vektory doplňku jsou kolmé na všechny vektory množiny
- vlastnosti ortogonálního doplňku podprostoru