# Systémy

## Cviko

- cvičení nebude moc navazovat na přednášku
- cílem cvičení je naučit nás myslet low-level a naučit nás programovat
- na přednášce se navazuje na principy
- informace jsou na webu
- 6 cvičení – 6 domácích úkolů odevzdávaných do recodexu
	- plus závěrečná úloha v SISu
- měli bychom zvládnout tu úlohu naprogramovat během cvičení
- nestačí testy v recodexu – kód musí nějak vypadat
- nesmíme porušovat pravidla – je možné, že přijdeme o zápočet
- týdenní deadline, pak ruční kontrola a případné poznámky, kód musíme upravit (ideálně během týdne / do dalšího cvičení)
- splněno máme až v okamžiku, kdy je náš kód přijat
- nesmíme opisovat – kód píšeme sami, o problému se můžeme bavit
- komunikace přes Mattermost
- budeme programovat v C

## Poznámky

- k úkolu ze systémů – nemusí nás trápit oscilace, musíme udělat jednotný kód pro všechna tři tlačítka (přístup C nebo C++)

```C
// předávání funkcí v C
struct Button;
typedef void(*action-f)(Button &b);
void increment(Button &b) { counter++; }
struct Button { int pin; bool down; action-f down; }
struct Button buttons[3];
button[0].down = &increment;

// třídy v C++
// virtuální funkce + virtuální destruktor
// když k nějaké virtuální metodě dám =0, tak mi to znemožní vytvořit samotnou třídu – u každého syna musím danou metodu přepsat
// nepoužívat operátor new
// chci mít pole tlačítek
Button *buttons[3];
// uděláme si globální proměnné pro jednotlivé typy (tři tlačítka) a pak jejich ukazatele uložíme do pole
// všechen kód na detekci změny nebo autorepeatu bude ve funkci loop

// můžeme si vybrat, který přístup se nám líbí víc
```

- digitalRead používat úsporně (jako u millis)
- hodnota digitalRead může oscilovat (je potřeba to softwarově opravit, na začátku na to kašleme)
- ReCodEx má problém s voláním funkcí v globálním scopu
	- u tříd dělá problém volání funkcí v konstruktoru a při přímé inicializaci vlastností objektu (stylem `int t = millis();`)
- když chci rozsvítit desetinnou tečku, vyANDuju aktuální rozsvícení s 0x7F
- je potřeba pohnout s latchem pomocí digitalWrite (postupně LOW, HIGH)
- data se posílají pomocí `shiftOut(data_pin, clock_pin, bitOrder, value)`
- všechny tři piny (data, clock, latch) je potřeba nastavit na output
- používá se MSBFIRST bitOrder
- dají se používat dvě metody latchování
	- jedna varianta – latch high, nastavení registrů, latch low
	- druhá varianta – nastavení registrů, latch low, latch high
		- v setupu nastavím latch na high
- uděláme si funkci na zobrazení jedné pozice (jako hodnotu k zobrazení předávat bajt, ne zobrazované číslo)

## Závěrečný úkol

- hází se kostkama – jsou fixně dané, takže je můžu dát do pole
- dva režimy – normální a konfigurační (nezáleží na tom, který bude aktivní při spuštění)
- házecí animaci máme vymyslet sami (nějakou pěknou)
- je na nás, jestli to bude d04 nebo d_4 nebo d4_
- když jsem v jednom režimu, tak zmáčknutí tlačítka jiného režimu to jenom přepne, nic dalšího nedělá (akce se provádí až při dalším stisknutí daného tlačítka)
- odevzdat zdroják (ino) do recodexu (neprovádějí se testy)
- Yaghob si to stáhne a pustí u sebe na Arduinu
- měřit čas pomocí `micros`
- házet každou kostkou samostatně! (když se háže více kostkami)
- najít si libovolnou hashovací funkci z internetu, do řešení uvést url
- můžeme použít `rand` a seedovat to pomocí `micros`

## 6. úloha

- zaměřuje se na pointery
- na null pointer se používá `nullptr`
- operátor `&` vrací adresu proměnné
- operátor `*` dělá dvě různé věci („inicializuje“ pointer = je to vlastně typ, získává hodnotu na dané adrese)
- pointerová aritmetika
- `buf[i]` $\iff$ `*(buf + i)`
- když sáhneme mimo pole, tak je to náš problém (nikde se to nekontroluje)
- dá se použít rozdíl indexů v poli (odečtu dva pointery), vrací `diffptr_t` (velký jako `size_t`, ale znaménkový)
- řetězce se chovají jako pole charů, které končí `\0`
- `const char str[] = "Ahoj";` vytvoří jenom jednu věc (pole), ukázka v prezentaci (s pointerem) vytvoří dvě věci (pole a pointer)
- za normálních okolností radši použít `str[]`, ale záleží na tom, jaké máme úmysly
- `size_t` je typ související s velikostí paměti
- pasti
	- neinicializovaný pointer `int *p;` – může ukazovat kamkoliv do paměti
	- sahání mimo pole
	- řetězec v bufferu pevné délky – typická bezpečnostní díra; nezapomínat na koncovou nulu
- úkol
	- jezdící nápis
	- máme použít připravený zdroják, je tam i pole na písmenka
	- na začátek okýnka použít pointer, mít tam nějakou pointerovou aritmetiku (nepoužívat indexy)
	- na displeji můžeme indexovat `p[0]` až `p[3]`
	- volat funkci `getMessage()`
		- dokud zpráva scrolluje, tak nevolám getMessage
		- takže pokud během scrollování přijde několik zpráv, tak se zobrazí až ta poslední a ty mezi tím se zahodí – to je korektní chování
	- nemusíme ošetřovat situaci, kdy nám getMessage vrátí několikrát to samé
	- mezery jsou v příkladu v recodexu špatně
	- na začátku zobrazím čtyři mezery, po 300 ms zobrazím tři mezery a první znak…
	- poslední stav = poslední znak a tři mezery
	- pozor na řetězec o jednom znaku
	- nedělat kopii řetězce (nechceme žádnou alokaci) – tzn. neobalovat řetězec mezerami
	- ošetřit prázdný řetězec (je zakončený `\0`)
	- nevolat getMessage v konstruktoru, ale až v setupu
