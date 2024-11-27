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
- během následujících dvou týdnů navrhovat témata zápočťáku
- rozdělit projekt parseru do více „modulů“ (postaru)
	- viz expr_evaluator_modules
	- je praktické mít v hlavičkovém souboru definovaný alias pro číselný typ
	- i soukromé věci se musí psát do hlavičkového souboru
		- jsou potřeba datové položky, aby bylo jasné, jak ty instance mají být velké
		- soukromé metody by tam potřeba nebyly
	- chceme udržet pořádek v globálních identifikátorech, ale nevystavovat obsah třídy ven
	- můžeme mít namespace parser a v něm jenom funkci parse a ten alias – to je kompletní obsah hlavičkového souboru (viz expr_parser_namespaces)
	- obecně se nedoporučuje mít v namespacu stejnojmennou třídu
	- aby funkce parse mohla přistupovat k privátním členům té třídy, tak se použije friend deklarace
		- friend deklarace umožňují napsat i implementaci funkce
	- aby bylo jasné, že některé věci jsou implementační detaily a že ho nemají zajímat, tak se používají vnořené namespacy s názvem `impl` nebo `detail`
- strom výrazu
	- je fajn mít enum na operace
	- existuje `std::variant`, ale to se tady moc nehodí
	- nechceme tam mít hvězdičkové pointery, místo nich použijeme `std::unique_ptr`
- OOP
	- v C++ je „abstraktní třída“ trochu něco jiného než abstraktní třída, ale ten pojem se používá i pro abstraktní třídy
	- v abstraktní třídě typicky nebývají žádná data
	- virtuální funkci označím jako `virtual`
	- `virtual val_t eval(val_t x) const = 0;`
		- const, protože eval nemá modifikovat node
		- 0, protože tělo bude až v potomcích (tzv. čistě virtuální metoda)
	- `virtual void print(std::ostream& out) const = 0;`
	- dědičnost
		- `class PlusNode : public AbstractNode {`
		- public píšu, protože chci, aby byla dědičnost veřejná, aby byl viditelný vztah mezi potomkem a předkem
		- virtuální metody můžu předefinovat v privátní sekci
		- `virtual val_t eval(val_t x) const override {`
			- to virtual tam být nemusí, ale je to vhodné
			- to override nám kontroluje, jestli existuje virtuální metoda na předkovi
		- virtuální metody se overridují v privátní sekci – je to dobrý zvyk
		- potřebujeme `using owner_ptr_t = std::unique_ptr<AbstractNode>;`
			- budeme mít privátní `owner_ptr_t left_, right_;`
			- tenhle pointer reprezentuje vlastnictví, proto je tam owner
		- potřebujeme veřejný konstruktor, abychom nemuseli za každého uživatele přidávat frienda
	- předávání pointerů do funkce
		- hvězdičkové hodnotou
		- chytré pomocí rvalue reference `&&`
	- konstruktory je vhodné psát tak, aby bylo všechno v dvojtečkové sekci a tělo bylo prázdné
		- `PlusNode(owner_ptr_t&& left, owner_ptr_t&& right) : left_(std::move(left)), right_(std::move(right)) {}`
	- existuje konstrukce `using namespace std;`
		- to nesmíme napsat do hlavičkového souboru, protože by to ten namespace vysypalo všem
		- pak bychom v headeru měli hlavičky s prefixem std:: a v cpp souboru bez něj, což by vypadalo divně
		- ale můžu to napsat do těla funkce, to je někdy užitečné
			- dokonce lze specificky napsat `using std::make_unique;`
		- ale třeba v impl namespacu už by to šlo vybalit
		- kdybychom to vybalili v namespacu parser, tak to povede k tomu, že bude existovat parser::move, parser::endl apod.
- alternativní úloha
	- `y=1+2*x; x=y+1;` se obvykle řeší pomocí nějaké mezikódu (bytecode)
	- první výraz
		- `CONST 1`
		- `CONST 2`
		- `LD x`
		- `MUL`
		- `ADD`
		- `ST y`
		- `LD y`
		- `CONST 1`
		- `ADD`
		- `ST x`
	- když tam přidáme na začátek návěští a na konec goto, tak tam může být smyčka
		- `GOTO -10`
	- tohle se objeví na zkoušce
	- pozor na načítání ze souboru – často jsou s tím větší problémy než s implementací logiky
	- úkol
		- načíst vstup
		- reprezentovat ho jako posloupnost kroků (ne textově)
			- 1, 2, x, \*, +
		- `virtual void exec(double x, stack& s) const = 0;`
			- double x … pro jednu proměnnou x
			- stack … odkaz na zásobník
				- může to být instance knihovní třídy std::stack nebo std::vector
				- je to vector chytrých pointerů na instrukce
			- to by nestačilo na goto, ale zatím nám to nevadí
		- funkce
			- push_back
			- chci přesunout chytré pointery z jednoho kontejneru do druhého
				- to můžu udělat ručně
				- poznámka: lvalue se pozná tak, že opakovaným použitím výrazu se dostanu k tomu stejnému objektu
				- ale dá se to udělat pomocí std::move z hlavičkového souboru `<algorithm>`
					- ale dělá se to natřikrát
					- pomocí size změříme zdrojový kontejner
					- přidáme prázdný prostor na konec cílového kontejneru (pomocí insert, třetí verze – kam, kolik, jakých hodnot)
						- `result.insert(result.end(), right.size(), nullptr);`
							- tohle nefunguje :)
					- `std::move(right.begin(), right.end(), result.end()-right.size());`
				- může se stát, že se nám invalidují iterátory
					- takže iterátory je potřeba používat čerstvé
					- kdykoliv něco přidává do kontejneru, tak můžeme do té doby vytvořené iterátory považovat za nevalidní – nedává smysl, abychom si je pamatovali
- `std::numeric_limits<T>`
	- `lowest` … vrací minimum
	- `min` … pro desetinná čísla vrací „epsilon“ (nejmenší kladnou hodnotu), jinak také minimum
	- `max` … vrací maximum
- `std::is_integral_v<T>` … je typ celočíselný?
- `std::plus` a podobné objekty
	- mají definovaný volací operátor

```cpp
template<typename OP>
class binary : public abstop {
	public:
		binary(.... l, .... r) : left(std::move(l)), right(std::move(r)) {}
		virtual int eval() const override {
			return f(left->eval(), right->eval())
		}

	private:
		..... left, right, OP f;
}
```

- taky by tam mohlo být třeba `return OP()(left->eval(), right->eval());`
	- nebo by první závorky mohly být složené
- jak udělat genericky i typ, co vrací eval?
	- můžu to přidat jako další šablonovaný parametr
	- ale pak to musíme mít i v abstraktní třídě
- z šablon vyplývají některé zvláštnosti
- parametr šablony může být typ nebo číselná konstanta
- jak to udělat, abychom nemuseli mít `int` v typech uvedený dvakrát (jednou pro eval, jednou v rámci plus)?

```cpp
// chceme použít
binary<plus<int>>
// uvnitř bude
using my_type = typename OP::result_type; // nefunguje v C++20
// nebo
// chceme použít
binary<int, plus>
// to se dělá takhle
template<typename my_type, template<typename> typename GOP>
class binary : public abstrop<my_type> {
	using OP = GOP<my_type>;
}
```

- naše mainy mají vracet nulu, jinak s tím recodex bude mít problém

---

- napíšeme si vlastní kontejner
- v C++ standardní knihovně není podpora pro matice
- je dobré ty řádky udělat tak, aby se daly iterovat třeba pomocí dvojtečkového for cyklu
	- třeba `a.rows()` by mohla vracet řádky matice
		- `.cols()` sloupce
	- budeme potřebovat iterátory
- matice by měla být šablona
	- ale zatím asi psát bez šablon
- lze implementovat pomocí vektoru vektorů
	- je to silnější než to, co potřebujeme – umožňuje „jagged array“
	- museli bychom to hlídat, aby se nám to nerozuteklo
	- plus to bude žrát hodně paměti – každý vektor má overhead
	- taky ty řádky budeme mít rozházené po paměti
- lze implementovat pomocí jednoho vektoru
	- potřebujeme znát rozměry matice
	- begin a end pro rows mají vracet řádkový iterátor (`row_iterator`)
		- vector má metodu data(), která vrací raw pointer na začátek
		- nebo můžeme držet pointer na celou matici a index řádku
	- co musí implementovat iterator kromě begin a end
		- ++ … posune iterátor
		- != … porovnávání iterátorů
		- \* … vrací konkrétní prvek

```cpp
class row_iterator {
	public:
		row_iterator &operator ++() {
			// něco
			return *this;
		}
		// tohle je prefixový ++
		// kdybychom chtěli postfixový, bylo by to s jedním intovým parametrem
		// (žádný intový argument se nepředává)
		// a musíme vracet hodnotou
		row_iterator operator ++(int) {
			row_iterator tmp = *this;
			++*this;
			return tmp;
		}
		row_ref operator *() const { /* ... */ }
		// trikové řešení: do iterátoru zavřu row_ref
		// obvykle se z operátoru hvězdičky vrací T&
		
}
bool operator !=(const row_iterator& a, const row_iterator& b) { /* ... */ }
// můžeme implementovat spaceship operator
```

- iterátory pro prvky řádku už můžou být přímo C pointery
	- C pointery mají vlastnosti iterátorů
- co potřebujeme
	- z funkce rows vrátíme objekt `rows_t`
	- `*((*(a.rows().begin())).begin())` … takhle se dostanu k levému hornímu prvku matice
