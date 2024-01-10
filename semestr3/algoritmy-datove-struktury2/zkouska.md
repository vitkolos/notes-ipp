# Zkouška

## Vyhledávání v textu

- Definice: Terminologie okolo řetězců (podslova, prefixy, suffixy)
	- slovo $\alpha$ … konečná posloupnost znaků z abecedy $\Sigma$
	- prázdný řetězec $\varepsilon$
	- $i$-tý znak $\alpha[i]$ (počítáme od nuly)
	- podřetězec/podslovo $\alpha[i:j]$ (od i-tého znaku do (j-1). znaku včetně)
	- prefix $\alpha[:j]=\alpha[0:j]$
	- suffix $\alpha[i:]=\alpha[i:|\alpha|]$
	- $\alpha[:]=\alpha$
- Algoritmus: Knuth-Morris-Pratt (jedna jehla v seně)
	- udržujeme si informaci o tom, jakým nejdelším prefixem jehly končí zatím přečtená část sena
	- tento prefix postupně zvětšujeme – pokud nejde zvětšit, pomocí zpětné funkce získáme menší prefix jehly a zkusíme zvětšit ten
	- pro získání zpětné funkce stačí postavit vyhledávací automat nad jehlou
		- vrcholy (stavy) = prefixy jehly (od prázdného prefixu $\varepsilon$ k celé jehle)
		- dopředné hrany … spojují prefixy zleva doprava
		- zpětné hrany … odpovídají zpětné funkci (např. z `barba` vede zpětná hrana do `ba`)
	- algoritmus rozdělíme na tři
		- KmpKrok
			- spouštíme pro nově přečtený znak a aktuální stav, vrátí nám nový stav
			- algoritmus projde po zpětných hranách (postupně zkouší kratší a kratší prefixy), dokud nedojde do stavu 0 ($\varepsilon$) nebo nenajde prefix, který pokračuje tím přečteným znakem
			- pokud ten prefix najde, tak stav zvýší o jedna
			- implementační detail: za poslední znak jehly musíme připojit fiktivní znak (takový, který se v seně nevyskytuje)
		- KmpHledej
			- spouštíme pro seno a automat nad jehlou, postupně jsou hlášeny jednotlivé výskyty
			- iterujeme přes všechny znaky sena a spouštíme KmpKrok
			- pokud se stav rovná délce jehly, ohlásíme výskyt
			- složitost
				- pro každý znak se prochází nejvýše po jedné dopředné hraně
				- každá zpětná hrana vede aspoň o jeden stav doleva – tedy průchodů po zpětných hranách bude nejvýše tolik, po kolika dopředných hranách jsme prošli
				- časová složitost $\Theta(S)$
		- KmpKonstrukce
			- nastavíme zpětnou hranu ze stavu 1 do stavu 0
			- provádíme jakoby KmpHledej, akorát jako seno použijeme jehlu bez prvního znaku
			- na základě výsledného stavu z každého kroku algoritmu nastavíme zpětnou hranu
			- časová složitost $\Theta(J)$
	- celkem čas $\Theta(J+S)$
- Algoritmus: Aho-Corasicková (více jehel v seně)
- Algoritmus: Rabin-Karp (okénkové hešování)
- Věta: Počet kolizí u okénkového hešování

## Toky v sítích

- Definice: Síť, tok, přebytek, velikost toku
- Definice: Řez, kapacita řezu
- Věta: Velikost toku se dá měřit na každém řezu
- Definice: Rezerva hrany, nasycená hrana
- Algoritmus: Ford-Fulkerson (zlepšující cesty)
- Definice: Minimální řez je stejně velký jako maximální tok
- Definice: Průtok (čistý tok)
- Příklad: Celočíselná síť má celočíselný maximální tok
- Algoritmus: Největší párování v bipartitním grafu
- Definice: Blokující tok, vrstevnatá síť
- Algoritmus: Dinicův algoritmus (zlepšující toky)
- Definice: Vlna, převedení přebytku po hraně
- Algoritmus: Goldbergův algoritmus (výšky a přebytky)
- Algoritmus: Goldbergův algoritmus s výběrem nejvyššího vrcholu

## Algebraické algoritmy

- Věta: Reprezentace polynomu grafem
- Definice: Primitivní n-tá odmocnina z jedničky
- Věta: Rychlá Fourierova transformace a její inverze
- Věta: Násobení polynomů pomocí Fourierovy transformace

## Paralelní algoritmy

- Definice: Hradlová síť
- Algoritmus: Sčítání přirozených čísel hradlovou sítí
- Algoritmus: Násobení přirozených čísel hradlovou sítí
- Definice: Komparátorová síť
- Algoritmus: Bitonické třídění komparátorovou sítí

## Geometrické algoritmy

- Algoritmus: Konvexní obal
- Algoritmus: Průsečíky úseček
- Definice: Voroného diagram
- Algoritmus: Lokalizace bodu v mnohoúhelníkové síti
- Algoritmus: Semipersistentní binární vyhledávací strom

## Převody problémů

- Definice: Rozhodovací problém
- Příklad: Bipartitní párování jako rozhodovací problém, kódování vstupu
- Definice: Převod mezi problémy
- Věta: Vlastnosti převoditelnosti (reflexivita, tranzitivita apod.)
- Definice: Problémy: klika, nezávislá množina, SAT, 3-SAT, 3,3-SAT, 3D-párování
- Algoritmus: Převod klika ↔ nezávislá množina
- Algoritmus: Převod SAT → 3-SAT → 3,3-SAT
- Algoritmus: Převod 3-SAT → nezávislá množina
- Algoritmus: Převod nezávislá množina → SAT
- Algoritmus: Převod 3,3-SAT → 3D-párování

## NP-úplnost

- Definice: Třídy složitosti P a NP
- Definice: NP-těžké a NP-úplné problémy
- Věta: Pokud A→B a B∈P, pak A∈P
- Věta: Pokud A→B, B∈NP a A je NP-úplný, pak B je NP-úplný
- Věta: Cookova věta: SAT je NP-úplný (náznak důkazu)
- Algoritmus: Převod obvodového SATu na SAT
- Příklad: Klasické NP-úplné problémy

## Jak zvládnout těžký problém

- Algoritmus: Nezávislá množina ve stromu
- Algoritmus: Barvení intervalového grafu
- Algoritmus: Pseudopolynomiální algoritmus pro problém batohu
- Definice: Aproximační algoritmus
- Algoritmus: 2-aproximace obchodního cestujícího v metrickém prostoru
- Věta: Neaproximovatelnost obchodního cestujícího bez trojúhelníkové nerovnosti
- Definice: Polynomiální aproximační schéma (PTAS)
- Definice: Plně polynomiální aproximační schéma (FPTAS)
- Algoritmus: FPTAS pro problém batohu
