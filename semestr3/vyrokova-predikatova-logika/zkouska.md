# Zkouška

## Pojmy

- Model ve výrokové logice, pravdivostní funkce výroku
	- model jazyka je určité pravdivostní ohodnocení proměnných
	- pravdivostní funkce výroku přiřazuje konkrétnímu ohodnocení proměnných nulu nebo jedničku, definuje se induktivně pomocí binárních funkcí
- Sémantické pojmy (pravdivost, lživost, nezávislost, splnitelnost) v logice, vzhledem k teorii
	- pravdivý výrok platí v každém modelu (jazyka/teorie)
		- je pravdivý v logice = platí v logice = je tautologie
		- je pravdivý v T = platí v T = je důsledek T
	- lživý (sporný) výrok neplatí v žádném modelu
	- nezávislý výrok platí v nějakém modelu a neplatí v jiném modelu
	- splnitelný výrok platí v nějakém modelu (tedy není lživý, je pravdivý nebo nezávislý)
- Ekvivalence výroků resp. výrokových teorií, T-ekvivalence
	- výroky/teorie jsou ekvivalentní, když se rovnají jejich množiny modelů
	- výroky/teorie jsou T-ekvivalentní, když se rovnají jejich množiny modelů vzhledem k teorii T
		- $\varphi\sim_T\psi\equiv M_\mathbb P(T,\varphi)=M_\mathbb P(T,\psi)$
		- kde $M_\mathbb P(T,\varphi)\equiv M_\mathbb P(T\cup\set{\varphi})$, což odpovídá $M_\mathbb P(T)\cap M_\mathbb P(\varphi)$
- Sémantické pojmy o teorii (sporná, bezesporná, kompletní, splnitelná)
	- teorie je sporná, jestliže… (ekvivalentně)
		- v ní platí spor
		- nemá žádný model
		- v ní platí všechny výroky
	- teorie je bezesporná (splnitelná), pokud není sporná, tj. má nějaký model
	- teorie je kompletní, jestliže není sporná a každý výrok je v ní pravdivý nebo lživý (tj. nemá žádné nezávislé výroky), ekvivalentně, pokud má právě jeden model
- Extenze teorie (jednoduchá, konzervativní), odpovídající sémantická kritéria
- Tablo z teorie, tablo důkaz
- Kanonický model
- Kongruence struktury, faktorstruktura, axiomy rovnosti
- CNF a DNF, Hornův tvar. Množinová reprezentace CNF formule, splňující ohodnocení
- Rezoluční pravidlo, unifikace, nejobecnější unifikace
- Rezoluční důkaz a zamítnutí, rezoluční strom
- Vysvětlete rozdíl mezi rezolučním důkazem, lineárním důkazem, a LI-důkazem
- Signatura a jazyk predikátové logiky, struktura daného jazyka
- Atomická formule, formule, sentence, otevřené formule
- Instance formule, substituovatelnost, varianta formule
- Pravdivostní hodnota formule ve struktuře při ohodnocení, platnost formule ve struktuře
- Kompletní teorie v predikátové logice, elementární ekvivalence
- Podstruktura, generovaná podstruktura, expanze a redukt struktury
- Definovatelnost ve struktuře
- Extenze o definice
- Prenexní normální forma, Skolemova varianta
- Izomorfismus struktur, izomorfní spektrum, ω-kategorická teorie
- Axiomatizovatelnost, konečná axiomatizovatelnost, otevřená axiomatizovatelnost
- Rekurzivní axiomatizace, rekurzivní axiomatizovatelnost, rekurzivně spočetná kompletace
- Rozhodnutelná a částečně rozhodnutelná teorie

## Lehké otázky

- Množinu modelů nad konečným jazykem lze axiomatizovat výrokem v CNF, výrokem v DNF
- 2-SAT, Algoritmus implikačního grafu, jeho korektnost
- Horn-SAT, Algoritmus jednotkové propagace, jeho korektnost
- Algoritmus DPLL pro řešení SAT
- Věta o konstantách
- Vlastnosti extenze o definice
- Vztah definovatelných množin a automorfismů
- Tablo metoda v jazyce s rovností
- Věta o kompaktnosti a její aplikace
- Věta o korektnosti rezoluce ve výrokové logice
- Věta o korektnosti rezoluce v predikátové logice
- Souvislost stromu dosazení a splnitelnosti CNF formule
- Nestandardní model přirozených čísel
- Kompletní jednoduché extenze DeLO*
- Existence spočetného algebraicky uzavřeného tělesa
- Tělesa charakteristiky 0 nejsou konečně axiomatizovatelná
- Kritérium otevřené axiomatizovatelnosti
- Rekurzivně axiomatizovaná teorie je částečně rozhodnutelná, kompletní je rozhodnutelná
- Teorie konečné struktury v konečném jazyce s rovností je rozhodnutelná
- Gödelovy věty o neúplnosti a jejich důsledky (bez důkazů)

## Těžké otázky

- Věta o korektnosti tablo metody ve výrokové logice
- Věta o korektnosti tablo metody v predikátové logice
- Věta o úplnosti tablo metody ve výrokové logice
- Věta o úplnosti tablo metody v predikátové logice
- Věta o konečnosti sporu, důsledky o konečnosti a systematičnosti důkazů
- Věta o úplnosti rezoluce ve výrokové logice
- Věta o úplnosti LI-rezoluce pro výrokové Hornovy formule
- Věta o úplnosti rezoluce v predikátové logice (Lifting lemma stačí vyslovit)
- Skolemova věta
- Herbrandova věta
- Löwenheim-Skolemova věta včetně varianty s rovností, jejich důsledky
- Vztah izomorfismu a elementární ekvivalence
- ω-kategorické kritérium kompletnosti
- Neaxiomatizovatelnost konečných modelů
- Věta o konečné axiomatizovatelnosti
- Rekurzivně axiomatizovaná teorie s rekurzivně spočetnou kompletací je rozhodnutelná
- Nerozhodnutelnost predikátové logiky
