# Zkouška

## Písemná část

- písemná část zkoušky
	1. upřesnění zadání, pokud je potřeba
	2. postřehy
	3. algoritmy
		- nevadí, když nevymyslíme nejoptimálnější
		- svou volbu musíme zdůvodnit
	4. datové struktury (reprezentace dat)
	5. dekompozice programu (objektový návrh)
	6. závěr/shrnutí (diskuze)

## Ústní část

- [algoritmizace](../algoritmy-datove-struktury1/zkouska.md)
	- složitost algoritmu, složitost úlohy/problému
	- fronta, zásobník, BFS, DFS
	- halda
	- rekurze
	- základní grafové algoritmy
		- hledání nejkratších cest a minimálních koster (Dijkstra, Kruskal, Bellman-Ford, Jarník, Borůvka)
		- topologické uspořádání
		- způsoby reprezentace grafu
	- stromové datové struktury a algoritmy na nich
		- BVS
		- AVL-strom
		- A-B-strom
	- třídicí algoritmy, vnější třídění
	- strom hry, minimax, alfa-beta prořezávání
	- memoizace a dynamické programování a typické problémy takto řešené (závorkování násobení matic, celočíselný problém batohu)
- [programování](#výpisky-z-programování)
	- OOP
		- princip/idea
		- dědičnost
		- zapouzdření
		- virtuální metody, abstraktní metody a třídy
	- dekompozice
		- funkční
		- objektová (SOLID a spol.)
		- modulární
	- diskrétní simulace
	- programování řízené událostmi
	- C# generické funkce a třídy
	- C# delegáty

## Výpisky z programování

- specifika C#, objektově orientované programování
	- C# je staticky typovaný, je překládaný (ne interpretovaný)
	- objekt = data + funkce (metody)
	- dělíme problém na podproblémy, izolujeme části kódu, ukrýváme vnitřek (= zapouzdření)
	- objekty jsou instance třídy
	- statické metody a atributy příslušejí přímo třídě
	- statické třídy neumožňují vytvoření instance
	- modifikátory přístupu (umožňují snazší zapouzdření)
		- public – přístupné všem
		- private – přístupné jen metodám dané třídy (default)
		- protected – přístupné této třídě a potomkům
	- konstruktory
		- klíčová slova this, base
	- přetěžování metod/operátorů
	- předávání proměnné referencí
		- modifikátory ref, out, in (liší se)
	- properties – vlastnosti (get, set)
	- child class se definuje pomocí dvojtečky (`class child:parent`)
	- virtuální metody
		- zděděné metody v synovských třídách můžeme přepisovat, pokud použijeme v rodiči virtual a v synovi override
			- alternativní (horší) přístup s klíčovým slovem new (schová rodičovskou metodu)
		- virtuální metody jsou reprezentovány odkazy z VMT (virtual method table, tabulka virtuálních metod)
		- VMT přísluší celé třídě (vytváří ji překladač)
		- každý objekt má ukazatel na svou VMT (tudíž syn přetypovaný na otce může podle VMT poznat, že je syn) – umisťuje ho tam konstruktor
		- přepisování metod je potřeba kvůli tomu, že synovské třídy často inicializujeme s typem rodiče (abychom ke všem objektům různých synovských tříd mohli přistupovat jednotně) = polymorfismus
	- abstraktní třída – vše je automaticky virtuální (nelze přímo vytvořit její instanci)
	- abstraktní metoda – pouze hlavička funkce, musí být obsažena v abstraktní třídě, nelze ji volat (musí se přepsat)
	- modifikátor sealed – u třídy zakazuje dědění, u metody zakazuje override
	- interface – vypadá jako abstraktní třída (bez těl funkcí), zachází se s ním podobně
	- delegáty
		- chceme předat funkci jako parametr (= zacházet s ní jako s proměnnou)
		- nejdříve musíme definovat datový typ reprezentující danou funkci – pomocí klíčového slova delegate
			- `public delegate int compare(object a, object b);`
		- pak můžeme uložit odkaz na funkci (metodu) do proměnné s tímto typem
		- odkazy na funkce lze řetězit pomocí operátoru sčítání (odčítání naopak odebírá ze seznamu)
		- klíčové slovo delegate se rovněž používá při definici anonymních funkcí (existují rovněž lambda funkce – u nich je jiný přístup k typování)
	- namespace
- další prvky C#
	- struktury jsou v C# hodnotové typy (na rozdíl od objektů – ty se předávají referencí)
	- pole – pevný počet prvků
	- obecný seznam – ArrayList ze System.Collections
	- typovaný seznam – `List<type>` (tzv. generická třída)
	- logické operátory – pro částečné i úplné vyhodnocení
	- try, catch, finally, throw
	- paralelní procesy – vlákna, asynchronní volání
- diskrétní simulace
	- simulujeme mnoho procesů a to, jak se ovlivňují
	- nemusíme sledovat celý průběh procesu, zajímají nás jenom důležité chvíle (např. začátek a konec) – tzv. události
	- simulační jádro – provádí obsluhu událostí, aktivně je „vykonává“
	- kalendář událostí – přehled událostí s časem, kdy mají nastat
	- simulační jádro si typicky bere první událost z kalendáře (tedy tu naplánovanou na nejdřívější čas)
	- jádro také může události do kalendáře přidávat nebo je rušit
	- kalendář je obvykle schopen měřit čas (tedy určit čas simulace)
	- simulace končí, jakmile po obsluze události zůstane kalendář prázdný
	- každý proces je v nějakém stavu, typické stavy jsou
		- běží (aktivní) – právě se obsluhuje jeho událost
		- naplánovaný – čeká v kalendáři událostí
		- čeká (pasivní) – čeká, až ho někdo vzbudí
		- ukončený – doběhl a nebude mít další události
	- pokud simulační jádro běží paralelně ve více vláknech, plynou z toho problémy paralelizace – race condition, deadlock
	- možná implementace
		- kalendář událostí = cyklický spoják
		- plánujeme procesy (o jakou událost jde si pamatuje proces)
		- pokud proces závisí na jiném procesu, tak se jím nechá aktivovat po jeho skončení (= pasivní čekání; aktivně čekající proces by se neustále ptal, jestli může pokračovat, což by zatěžovalo procesor)
- programování řízené událostmi = program reaguje na události (obvykle uživatelské nebo simulované – při diskrétní simulaci), zpracovává je a transformuje, předává mezi úrovněmi
- objektový návrh
	- lze ho pojmout jako návrh hlaviček tříd a metod a definice atributů
	- snažíme se problém rozdělit na co nejmenší smysluplné součásti
	- UML diagram – krabičky představují třídy, spojnicemi se značí relace (případně komunikace)
	- data flow diagram – orientovaný graf, vrcholy představují operace, grany jsou popsány putujícími daty
- SOLID
	- single reponsibility – každá entita zodpovídá za jednu věc
	- open-closed – entity jsou otevřené rozšíření, ale uzavřené změnám
		- můžeme odvodit novou třídu s více daty a funkcemi, ale rozhraní stávající třídy se nebude měnit
	- Liskov substitution – místo rodiče lze použít potomka
		- s objektem synovské třídy lze zacházet jako s objektem rodičovské třídy (Tygra lze použít, jako by to byla Kočka)
	- interface segregation – více specifických rozhraní (pro různé klienty) je lepších než jedno univerzální
	- dependency inversion – závislost by měla být na abstraktním, ne na konkrétním (implementace se mění často, kdežto abstrakce je trvalejší)
- další pravidla
	- Deméteřin zákon – funkce by neměla volat jiné funkce, které jsou od ní „příliš daleko“ (měly by být přibližně na její úrovni; porušení zhoršuje udržovatelnost kódu a zapouzdření)
	- DRY – neopakuj se
	- high cohesion, low coupling – související věci by měly být v programu u sebe, ale měl by být provázané jen zlehka (přes interface)
- grafové algoritmy
	- reprezentace grafu
		- matice sousednosti – řádky i sloupce odpovídají vrcholům, jednička odpovídá hraně, nula nehraně
		- matice incidence – řádky indexovány vrcholy, sloupce hranami, jednička určuje, že vrchol náleží hraně
		- seznam vrcholů a u každého seznam přilehlých hran
