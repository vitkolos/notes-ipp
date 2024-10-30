- cvičení
	- s Koupilem budeme řešit zápočtové programy
	- všechno ostatní s Bednárkem
	- když něco děláme na cvičení, tak je fajn to vyplňovat v repozitáři – pak nám to může pomoct, kdybychom měli problém se zápočtovým programem apod.
		- občas se něco bude navíc odevzdávat do recodexu
	- docházka nebude
	- cvičení bude většinu semestru předbíhat přednášku
- zápočtové testy
	- 8. 1. 2025 12:20 v učebnách SU1 a SU2
	- první týden zkouškového období – opravný termín
	- když domácí úkol vyřeším včas, tak dostanu zpětnou vazbu
	- do SU1 můžeme většinou přijít volně, Rotunda je konfigurovaná stejně
	- můžeme si vybrat mezi Linuxem a Windows
		- ve Windows je Visual Studio
	- měli bychom se naučit používat debugger
- zápočtové programy
	- polovina listopadu – návrh tématu
		- návrhy psát do Mattermostu jako Direct Messages pro dva příjemce @pavel.koupil a @bednarek
	- 20. 12. podrobné zadání
		- zadání psát jako markdown do project/docs
		- implementace do project/src
			- musíme to pravidelně commitovat tam
		- použití knihoven je potřeba uvést v zadání
	- 14. 2. technologické demo
		- obsahuje knihovny a komponenty, které chceme použít
		- aby to někdo jiný byl schopný jednoduše rozchodit
		- bude obsahovat krátký návod, co je potřeba postahovat + make/cmake skript
	- 23. 5. finální verze
		- osobní předvedení zápočťáku nebude
		- musíme to udělat tak, aby se zápočťák dal z repozitáře použít
	- témata
		- hry obvykle nejsou moc zajímavé
		- matematické věci jsou fajn (jako knihovny)
		- nejsou důležité algoritmy, spíš ukázat, že umíme programovat v C++ (rozhraní, datové struktury apod.)
	- typické problémy
		- interní součásti programu nejsou dostatečně oddělené
- pokud chci v C++ implementovat funkci volatelnou z C, tak se to řeší pomocí `extern "C"`
- můžeme používat překladače ve Visual Studiu
	- v nastavení projektu budeme potřebovat nastavit C++ Language Standard
		- default je C++14
		- časem asi budeme chtít používat věci z C++17 a C++20
- ve VS Code
	- dá se nainstalovat microsoftí překladač nebo gcc nebo clang ve verzi pro windows
- na Windows bychom měli programy psát tak, aby fungovaly i na Linuxu
	- na grafické rozhraní knihovna Qt
- default g++ pro překlad je před C++11, takže je tam potřeba dát přepínač pro C++20
- budou po nás chtít překlad bez warningů
	- většinou se dají odstranit – lepším programování nebo obratem, který přesvědčí překladač
	- např. můžu zrušit jména nepoužitých parametrů funkce
- je dobré z programů vracet nulu
	- v prostředí Windows se návratové hodnoty prakticky nepoužívají
	- v recodexu vracet nulu vždycky – i když je tam nějaký problém
		- vyhodnotilo by se to jako naše chyba
- v C++ spíš nepoužívat `#include <stdio.h>`, ale raději `#include <cstdio>`
- printf je nebezpečné, nekontroluje shodu parametrů
- argv
	- je to pointer na pointer na char
	- akorát ten char není jeden, ale je to nulou ukončený řetězec charů
	- správně by tam mělo být const char**, ale rozhraní mainu je tak staré, že tehdy const neexistovalo
	- díky argc víme, kolik těch řetězců program dostal
	- dvě různé konvence určování délky polí – koncová nula nebo proměnná s délkou
	- další konvence – pointer na místo za koncem pole
		- kdyby se jmenoval arge
			- arge - argv = délka pole
			- když je to rozdíl pointerů, není to pouhé odečtení, ale také vydělení velikostí položky pole
- vector
	- iterátory
	- umožňuje provést i implicitní konverzi
	- `std::vector<std::string> arg(argv, argv + argc);`
	- `argv` a `argv+argc` jsou iterátory
	- `std::string` má konverzní konstruktor, z typu `char*` vznikne `std::string`
	- `std::vector<std::string>` je kontejner stringů
	- pozor, porovnávání céčkových stringů (char*) je porovnávání pointerů
- stringy
	- když jsou velké, tak se alokují dynamicky
	- jsou mutable

```cpp
#include<vector>
#include<string>

#include <cstdio>

int main(int argc, char** argv) {
	std::vector<std::string> arg(argv, argv + argc);
	
	for (int i = 0; i < argc; ++i) {
		// tohle nebude fungovat, protože arg[i] neopovídá typu %s
		std::printf("%d: %s\n", i, arg[i]);
	}
	
	return 0;
}
```
- std::string … trojice pointerů, první ukazuje na začátek stringu, druhý vlastně na jeho koncovou nulu a třetí na konec bloku, který je pro string vyhrazen
- aliasy typů pomocí `using`, používá se předpona `t_`
	- `using t_arg = std::vector<std::string>;`
- `for (auto&& x : parg)`
	- parg je kontejner
	- auto se píše s dvojitým &&
	- kdyby tam ty reference nebyly, tak bychom ten string kopírovali

---

- zpracování CSV souboru
- třída `std::ifstream` … vstupní souborový stream
	- `ctd::cout` je typu `std::ofstream`
	- `fstream` umí vstup i výstupu, ale ovládá se komplikovaněji
	- existuje taky `strstream`, který pracuje s proměnnou typu string
- debug režim
	- překladač se nesnaží optimalizovat kód
	- ve standardních knihovnách jsou testy, jestli je používáme správně
- starší vrstva standardních knihoven nevypouštějí výjimky
	- řeší se to pomocí návratových hodnot, příznaků a jinými způsoby
	- pokud se `ifstream` nepovede otevřít, nastaví se chybový příznak
		- metoda `fail()` vrací true, pokud se poslední volání rozbilo
		- metoda `good()` vrací true, pokud je objekt v pořádku
- příznak `eof` se nastaví až po tom, co se pokusíme přečíst data za koncem souboru
	- takže po každém čtení kontrolujeme fail, pokud to zfailovalo a nastavil se příznak eof, je to v pohodě – jsme na konci souboru
- neinicializovaná proměnná typu std::string obsahuje prázdný řetězec
- pozor, pokud něco zfailuje, tak std::getline v proměnné nechá původní hodnotu
- měli bychom kontrolovat chyby při čtení ze souboru i při zápisu do souboru
- chceme, aby `csv_file` byla nějaká sofistikovanější datová struktura (struktura nebo třída), která bude odděleně obsahovat hlavičku a tělo souboru
- stačí mi vytvořit lokální proměnnou `csv_file csv;`, nic víc nepotřebuju, protože životnost proměnné se kryje s funkcí main
- celý soubor se nám vleze do paměti
- můžeme ignorovat všechny úplně prázdné řádky
- chceme testovat, jestli je vstup korektní (třeba že na konci řádku nejsou ukončené uvozovky)
- zajímavé věci, které můžeme použít
	- ve stringu append (string je mutabilní)
	- kdybychom si chtěli něco signalizovat výjimkama, používá se třída `std::runtime_error`, nepoužívá se `new`
	- `std::sort` k třídění
	- `std::pair` se umí řadit lexikograficky
	- na číslování sloupečků je fajn použít `size_t`
		- typ `int` budeme používat málokdy – většinou řešíme nějaké pozice, indexování do pole
	- `std::emplace_back` na přidání dvojice na konec kontejneru dvojic
	- `std::iota`
	- lambda funkce

---

- časté chyby a poznámky
	- před `constexpr` by se v hlavičkovém souboru mělo napsat `inline`
	- `constexpr` je informace pro překladač, `const` je informace pro vývojáře
	- je potřeba psát u parametrů funkcí `const`, pokud nemodifikují své parametry
		- jednak tím děsíme programátory
		- jednak se taková funkce nedá volat s rvalue parametrem
			- např. takovou funkci, která bere `std::string&` (nikoliv const) nemůžeme zavolat se zřetězením stringů
	- používat `using` konstrukci
		- nedávat tam dekorace (const, &), aby bylo vidět, jak se parametr předává
		- ale můžeme tam dát `*`
	- kontejnery se inicializují prázdné
		- takže stačí `std::string out;`
		- nemusíme psát `std::string out = "";`
		- funguje taky `std::string out();` nebo `std::string out{};`
			- může to takhle být lepší, je to explicitnější
	- chceme-li procpat výsledek operace přes návratovou hodnotu, můžeme použít typ `optional<T>`
		- `optional<string> x;` je automaticky inicializovaná jako neplatná
		- existuje operátor `!x`, který nám řekne, že je nevalidní
			- kdybychom to chtěli otočit, tak použijeme dvojitý vykřičník
		- k hodnotě se přistupuje pomocí `*x` nebo `x->`
	- používat referentítka (&)
		- jinak se hodnota parametru kopíruje
		- všechno dává smysl předávat jako const reference kromě čísel a hvězdičkových pointerů
	- bez referentítka nedává smysl použít const
	- je fajn dělat si referenční lokální proměnné – např. ukázat na prvek pole
	- nepoužívat typedef, má jinou syntaxi
- vyhodnocování výrazů
	- funkce A (aditivní) žere posloupnost M (multiplikativní) oddělených plusy nebo minusy
	- M dělá to samé, akorát žere T, mezi nimiž jsou hvězdičky (nebo lomítka?)
	- T (term) žere čísla a závorky
		- pozor, v repu chybí eat po počáteční kulaté závorce
	- next je implementovaný jako peek – neposouvá ukazovátko
	- eat může být jako get
	- next/eat může přeskakovat mezery
	- můžeme mít enum pro operátory
- poznámky
	- kdybych chtěl používat istream, aby to podporovalo ifstream i istringstream
		- nevystačím si s hodnotou
		- potřebuju referenci nebo pointer
	- reference a pointery technicky fungujou stejně, jen se jinak používají
	- když chceme do pointeru přiřadit referenci, použijeme `&`
		- `s_ = &p;`
		- je zvyk předávat streamy do funkcí jako reference (ne pointery), aby se pak lépe používaly se zapisovacími a vypisovacími operátory
			- předávání hodnotou nedává smysl, jelikož má stream nějaký vnitřní stav
	- speciální syntaxe pro konstruktor
		- `parser(istream & p) : s_(p) {}`
		- takhle můžu mít referenci `s_`
		- překladač vždycky zajistí volání konstruktoru na těch položkách
	- ale neočekává se, že když funkci/objektu předám referenci, tak si ji někam schová a bude ji používat dál
	- takže parametr konstruktoru bude typu pointer
		- tak upozorníme na to, že si objekt ukazatel nechá
	- pokud bychom chtěli vytovřit objekt parseru a jen na něm zavolat parse, tak by bylo hezčí, kdybychom místo toho měli statickou metodu parse, která by si uvnitř vytvořila instanci parseru
		- není důvod, aby byl objekt parseru vidět – není v něm nic zajímavého
