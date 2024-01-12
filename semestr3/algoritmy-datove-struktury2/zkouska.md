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
			- časová složitost $\Theta(S)$
				- pro každý znak se prochází nejvýše po jedné dopředné hraně
				- každá zpětná hrana vede aspoň o jeden stav doleva – tedy průchodů po zpětných hranách bude nejvýše tolik, po kolika dopředných hranách jsme prošli
		- KmpKonstrukce
			- nastavíme zpětnou hranu ze stavu 1 do stavu 0
			- provádíme jakoby KmpHledej, akorát jako seno použijeme jehlu bez prvního znaku
			- na základě výsledného stavu z každého kroku algoritmu nastavíme zpětnou hranu
			- časová složitost $\Theta(J)$
	- celkem čas $\Theta(J+S)$
- Algoritmus: Aho-Corasicková (více jehel v seně)
	- automat = trie
		- stavy = prefixy jehel
		- dopředné hrany = přidání jednoho znaku na konec ($\alpha\to\alpha x$)
		- konce jehel (označíme v trii)
		- zpětné hrany – vedou z $\alpha$ do nejdelšího vlastního suffixu $\alpha$, který je stavem (tohle obvykle v trii nebývá)
		- zkratkové hrany – vedou z $\alpha$ do nejbližšího stavu dosažitelného po zpětných hranách, kde končí jehla (použijeme při hlášení výskytů)
	- reprezentace automatu
		- stavy očíslujeme – kořen má číslo 0, ostatní vrcholy libovolná různá
		- pole Dopředu(stav, písmenko) – obsahuje další stav (podle dopředné hrany)
		- pole Slovo(stav) – končí v daném stavu slovo?
		- pole Zpět(stav) – číslo stavu, kam vede zpětná hrana (kromě kořene je vždy právě jedno)
		- pole Zkratka(stav) – číslo stavu, kam vede zkratková hrana
	- algoritmy/procedury
		- AcKrok
			- na vstupu aktuální stav a přečtený znak, na výstupu nový stav
			- projde dopředu po jedné hraně z aktuálního stavu nebo zkouší procházet po zpětných hranách, dokud nebude moct projít dopředu (přinejhorším vrátí kořen)
		- AcHledej
			- na vstupu seno a automat, postupně ohlašuje výskyty
			- spouští AcKrok pro každý znak sena
			- pokud je v daném stavu označen konec jehly, hlásí výskyt
			- prochází po zkratkových hranách a hlásí jednotlivé výskyty
			- složitost $\Theta(S+V)$, kde $S$ je délka sena a $V$ je počet výskytů
		- AcKonstrukce
			- nejdříve sestrojíme trii
			- zpětné hrany můžou vést křížem mezi větvemi stromu
			- proto je konstruujeme po hladinách (BFS, pomocí fronty)
			- pro vrchol $v$ a rodiče $r$ zkusíme k vrcholu Zpět(r) přidat písmeno na hraně $rv$, čímž dostaneme Zpět(v)
			- pokud pokud je Zpět(v) konec jehly, tak Zkratka(v) nastavíme na Zpět(v), jinak nastavíme Zkratka(v) na Zkratka(Zpět(v))
			- algoritmus jakoby hledá všechny jehly (jako u KMP)
			- složitost $\Theta(J)$, kde $J$ je součet délek jednotlivých jehel
	- celkem čas $\Theta(J+S+V)$
- Algoritmus: Rabin-Karp (okénkové hešování)
	- hledání jedné jehly
	- zahashuju si posloupnost $J$ znaků a porovnám s hashem jehly
	- hashovací funkce pro řetězec $x_1\dots x_J$
		- $h(x_1,\dots,x_J)=x_1P^{J-1}+x_2P^{J-2}+\dots+x_JP^0\mod M$
	- postupně přehashovávám pro každý takový úsek sena (hashování v lineárním čase, přehashování v konstantním)
		- $h(x_2,\dots,x_{J+1})=P\cdot h(x_1,\dots,x_j)-x_1 P^J+x_{J+1}\mod M$
	- pokud se hash posloupnosti znaků shoduje s hashem jehly, ověříme, zda je to opravdu jehla
	- průměrná časová složitost $\Theta(J+S+JV+{SJ\over M})$ pro rovnoměrnou hashovací funkci
		- jehlu hashujeme lineárně Hornerovým schématem
		- provádíme $S$ přepočítání hashovací funkce
		- nahlášení každého výskytu trvá $JV$ (ověřujeme, zda je to jehla)
		- pro dvě různé posloupnosti znaků se hashe shodují s pravděpodobností $1/M$ (viz věta o počtu kolizí) – takže průměrně $\Theta({SJ\over M})$ strávíme kontrolou falešně pozitivních výsledků
		- chceme $M\in\Omega(SJ)$, abychom minimalizovali vliv kolizí
	- naše polynomiální hashovací funkce není dokonale rovnoměrná (místo $1/M$ bude pravděpodobnost kolize $J/M$), ale podrobnější analýza nebude zkoušena
- Věta: Počet kolizí u okénkového hešování
	- pro dokonale rovnoměrnou hashovací funkci $1/M$ pro $M$ okének
	- přesnější odhad nebude na zkoušce

## Toky v sítích

- Definice: Síť, tok, přebytek, velikost toku
	- síť je čtveřice
		- orientovaný graf $(V,E)$
			- BÚNO symetrický ($uv\in E\implies vu\in E$)
			- chybějící hrana má jakoby nulovou kapacitu
		- zdroj $z\in V$
		- spotřebič $s\in V,\,s\neq z$
		- kapacity $c:E\to\mathbb R_0^+$
	- tok je funkce $f:E\in\mathbb R_0^+$ taková, že
		- $\forall e\in E:f(e)\leq c(e)$
		- Kirchhoffův zákon
			- zákon zachování, tekutina se nám nikam neztrácí
			- $\forall v\in V\setminus\set{z,s}:f^\Delta(v)=0$
	- pro $v\in V$
		- přítok $f^+(v):=\sum_{uv\in E} f(uv)$
		- odtok $f^-(v):=\sum_{vw\in E}f(vw)$
		- přebytek $f^\Delta(v):=f^+(v)-f^-(v)$
	- velikost toku $|f|:=f^\Delta(s)$
- Definice: Řez, kapacita řezu
	- $E(A,B):=E\cap (A\times B)$
	- tedy $E(A,B)=\set{uv\in E\mid u\in A\land v\in B}$
	- řez je $E(A,B)$ pro $A\subseteq V,\;B=V\setminus A$
		- přičemž $z\in A,\;s\in B$
	- kapacita řezu $c(A,B):=\sum_{e\in E(A,B)} c(e)$
	- $f(A,B):=\sum_{e\in E(A,B)} f(e)$
	- $f^\Delta(A,B):=f(A,B)-f(B,A)$
- Věta: Velikost toku se dá měřit na každém řezu
	- lemma: pro každý řez $E(A,B)$ a každý tok $f$ platí $f^\Delta(A,B)=|f|$
	- důkaz
		- $\sum_{v\in B}f^\Delta(v)=f^\Delta(s)=|f|$
			- podle Kirchhoffova zákona
		- $\sum_{v\in B}f^\Delta(v)=f(A,B)-f(B,A)=f^\Delta(A,B)$
			- hrany zleva doprava přispívají kladně
			- hrany zprava doleva přispívají záporně
			- ostatní hrany nepřispívají
- Definice: Rezerva hrany, nasycená hrana
	- rezerva hrany $uv$
		- $r(uv):=c(uv)-f(uv)+f(vu)$
	- hrana je nasycená $\equiv$ má nulovou rezervu
	- hrana je nenasycená $\equiv$ má kladnou rezervu
- Algoritmus: Ford-Fulkerson (zlepšující cesty)
	- cesta je nenasycená $\equiv$ žádná její hrana není nasycená / všechny mají kladné rezervy
	- algoritmus
		- iterujeme, dokud existuje nenasycená cesta ze zdroje do stoku
		- spočítáme rezervu celé cesty (minimum přes rezervy hran cesty)
		- pro každou hranu upravíme tok – v protisměru odečteme co nejvíc, zbytek přičteme po směru
	- pro celočíselné kapacity vrátí celočíselný tok
	- racionální kapacity převedeme na celočíselné
	- pro iracionální kapacity se může rozbít
	- … (todo)
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
