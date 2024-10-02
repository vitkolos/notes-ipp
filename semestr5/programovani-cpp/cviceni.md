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
		// tohle nebude fungovat, protože argv[i] neopovídá typu %s
		std::printf("%d: %s\n", i, argv[i]);
	}
	
	return 0;
}
```
