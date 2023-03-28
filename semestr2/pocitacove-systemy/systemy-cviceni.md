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