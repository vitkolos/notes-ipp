# Algoritmická teorie her: cvičení

- cvičení nebude úplně pravidelně
	- bude oznámeno, když cviko odpadne
- https://kam.mff.cuni.cz/~cizek/ath2425/ath.html
- dotazy na/po cviku nebo mailem
- zápočet
	- 4 sady domácích úkolů, v každé 3–4 příklady
	- celkem 36 bodů, z nich potřebujeme 18 na zápočet
	- zápočtový test byl zrušen
	- všichni musejí na zkoušku, ale zkoušející bude přihlížet k vyššímu počtu bodů z příkladů
	- odevzdávání přes Sovu
	- deadline vždycky za 2 týdny
	- čím dřív odevzdáme, tím je větší šance, že dostaneme zpětnou vazbu včas a budeme si moct řešení opravit

## Lineární programování

- soustava $n$ lineárních nerovnic (podmínek) $p_1,\dots,p_n$ o $m$ neznámých
	- podmínka $p_i:a_{i1}x_1+a_{i2}x_2+\dots+a_{im}x_m\leq b_i$
	- řešení … $x=(x_1,\dots,x_m)\in\mathbb R^m$
	- maximalizujeme účelovou funkci $c_1x_1+c_2x_2+\dots+c_mx_m$
- u řešení lineárních rovnic – lineární rovnice reprezentují nadroviny, hledáme jejich průniky
- lineární nerovnice reprezentují poloroviny, určují nějaký mnohostěn (nemusí být omezený)
	- účelová funkce roste ve směru vektoru $c$
	- nadrovina kolmá na $c$ určuje řešení se stejnou hodnotou účelové funkce
	- „zametáme“ nadrovinou, najdeme optimální řešení $x^*$
	- pozorování: aspoň jedno optimální řešení se nachází ve vrcholu mnohostěnu
- co se může stát
	- lineární program nemá řešení – průnik (mnohostěn) je prázdný
	- má řešení, ale není omezené
	- má maximální řešení
- simplexová metoda
	- začne v nějakém vrcholu, pak cestuje po hraně dokud nedojde do dalšího vrcholu
	- podle pivotovacího pravidla si vybírá další směr
	- simplexová metoda může běžet až exponenciálně
		- ale průměrně je velmi rychlá
		- jsou i polynomiální způsoby řešení
- kanonická forma (tvar) … viz handout
- existuje také ILP, celočíselné lineární programování
	- řešení se nacházejí na celočíselné mřížce uvnitř mnohostěnu
	- tento problém je NP těžký
