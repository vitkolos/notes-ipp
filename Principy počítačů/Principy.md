# Principy počítačů

- https://slama.dev/poznamky/principy-pocitacu/
- písemná zkouška, 10 otázek, každá za jeden bod, potřebujeme polovinu na úspěšné složení zkoušky, časový limit 4 hodiny, zkouší se s toho, co se probere na přednáškách, dostaneme ukázku (loňskou písemku)
- self-assessment úlohy – dostaneme ke každé přednášce sadu
	- za nějaké odevzdané úlohy můžeme dostat desetinu bodu ke zkoušce, až něco přes dva body budeme moci získat, týdenní deadliny
	- hodnocení úloh bude až dodatečně, pokud bychom ty body potřebovali
	- zadávání a odevzdávání úloh do MS Teams
- videozáznamy nám pošle
- důležité je pochopit, proč věci fungují tak, jak fungují – nemusíme se učit všechno nazpaměť, ale musíme umět termíny
- nemusíme se hlásit, když se na něco budeme chtít zeptat

## Počítač

- Harvardská architektura počítače
	- CPU – procesor, vykonává příkazy
	- kódová paměť (code memory) – uložení informací o příkazech
	- komunikační linka – umožňuje, aby procesor četl data z paměti
		- v základním počítači CPU nemusí zapisovat do kódové paměti, do ní se zapisuje nějak z venku
	- datová paměť (data memory) – CPU z ní čte a zapisuje do ní data
		- data se ukládají do proměnných
	- k procesoru jsou dále připojena vstupně-výstupní zařízení – I/O, periferie
- matematik Charles Babbage vymyslel koncept mechanického počítače – Analytical Engine (v roce 1837), byl plně programovatelný, Turing complete
	- jeho přítelkyně Ada Lovelace napsala manuál k tomuto počítači
		- vydala publikaci, kde vyslovila myšlenku kódování libovolných dat (textů a multimédií) pomocí čísel
- budeme se zabývat tím, jak v počítači reprezentovat čísla (všechna ostatní data na ně můžeme převést)
	- informace (data) → čísla → celá čísla → nezáporná celá čísla
- zaznamenáme libovolné číslo od nuly do milionu
	- nula je 0 V, miliion je 5 V, všechno ostatní mezi tím
	- problém je při vysílání, každý vodič má odpor
		- změna odporu při teplotě
		- kvůli vlastnostem vodičů vzniká elektromagnetický šum
		- analogový přenos
- posledním zjednodušením je přenášení čísel nula/jedna
	- této číslici budeme říkat bit (binary digit), b
	- stanovíme hranici napětí, všechny hodnoty nad ní budeme interpretovat jako jedničku, hodnoty pod ní jako nulu
	- digitální přenos – přenos číslic

![timing-diagram](přílohy/timing%20diagram.png)

- sériový digitální přenos
	- záleží na pořadí číslic – přijímající a vysílající se musí dohodnout
		- označíme si bit s nejnižší váhou – Least Significant bit (LSb)
		- bitu s nejvyšší váhou budeme říkat Most Significant bit (MSb)
		- stanovíme bit order – MSb-first nebo LSb-first
- mocniny dvojky
	- 16 = 2^4
	- 256 = 2^8
	- 1024 = 2^10
	- 4096 = 2^12
	- 65535 = 2^15
	- cca 10^6 = 2^?
	- cca 16 000 000 = 2^24
	- cca 4 200 000 000 = 2^32

![](přílohy/obvod.png)

![](přílohy/diferenciální%20přenos.png)

- diferenciální přenos
	- data 1 – data 2
	- \>0 = 1
	- \<0 = 0
- řešení problému se dvěma jedničkama / dlouhou jedničkou
	- pevná délka bitu
		- definuje se přenosová rychlost
			- v bitech za sekundu (bits per second, bps)
			- jednotka baud \[bód\] (symbol za sekundu) – obvykle budeme uvažovat x baud = x bps, ale jeden symbol může obsahovat více bitů

## 2. přednáška

- vodiče
	- klasický způsob přenosu (není diferenciální) – data a GND
	- diferenciální – data+, data–
- přijímač se na signál kouká přibližně v polovině bitů
	- přenosová rychlost zajišťuje intervaly čtení, je ale nutné zajistit začátek čtení (synchronizaci hodin, "tikání")
	- musíme si odlišit stav, kdy se nic nepřenáší, od začátku přenosu
- **idle stav** – nic nepřenášíme
- floating stav / stav s vysokou impedancí / Hi-Z = stav, kdy je obvod rozpojený, ale vodič indukuje náhodnou hodnotu
- 3-stavová logika – funguje na lince, kde umíme rozlišit floating stav, nulu a jedničku
	- floating stav bychom mohli požadovat za idle stav
- my ale chceme fungovat na 2-stavové logice (lince)
	- můžeme definovat idle stav jako nulu
	- začátek přenosu označíme pomocí start condition – rising edge (rostoucí hrana)
	- definujeme si, že na začátku přenosu bude start bit (nebo nějaký určitý počet start bitů)
	- potom začíná přenos užitečných bitů (datových bitů / data bits)
		- data bits se do obrázku značí podobně jako diferenciální přenos, ale znamenají něco jiného (jde o obecné značení bitů, jaké je možné posílat)
- může se stát, že se nám vysílání a příjem bitů posune
	- proto definujeme maximální délku přenosu – max X → const X (definujeme konstatní maximální délku)
	- N bitů celkem rozdělíme po X bitech
		- N/X = Y přenosů
	- výrobci se shodli, že se přenos bude uskutečňovat po 8 bitech
		- 8 bitů = 1 byte (B)
		- 8 bitů = 1 octet (existuje několik málo zařízení, která mají jinou velikost bytu, proto je obecně správnější používat označení octet)
- po X bitech (obvykle osmi, ale může být i více bytů) – stop condition (falling edge, klesající hrana), stop bity, idle stav, start condition, start bity, ...
- takhle navržená linka přenáší 20 % času technická data (8 data bits, 1 start bit, 1 stop bit) – 20% overhead
- přenosová rychlost bps (bits per second) – počítají se data bits
- synchronizaci je možné řešit i pomocí hodinového signálu (clock) – linka vysílající střídavě nuly a jedničky, jednička značí čas čtení (zajišťuje synchronizaci přijímače a vysílače)
	- vodiče
		- data, GND, clock
		- diferenciální – data1, data2, clock, GND, (clock1, clock2) (?)
	- přenosová rychlost by mohla být definovaná rychlostí tikání hodinového signálu
	- hodinový signál může generovat vysílající – určité nevýhody
	- hodinový signál může generovat centrální oscilátor
	- cyklus (cycle/takt) hodinového signálu definuje přenosovou rychlost
	- lépe se detekují hrany signálu – můžeme si definovat, že rostoucí hrany hodinového signálu definují momenty čtení
	- abychom zrychlili přenos, můžeme používat obě hrany hodinového signálu (rostoucí i klesající) – označení DDR (double data rate)
- co když je hodinový vodič kratší než datový vodič?
	- můžeme se vykašlat na hodiny a synchronizovat se jiným způsobem – vždy jen v určitých (delších) intervalech
	- mohli bychom se synchronizovat pomocí hran, ale museli bychom mít jistotu, že se v datech dostatečně často střídají jedničky a nuly – to ale nemusí vždy platit
	- na každých osm bitů bychom mohli poslat 10 bitů
	- ke každé kombinaci osmi bitů bychom mohli namapovat kombinaci 10 bitů, které jsou dostatečně "hezké" – dostatečně často se tam střídají jedničky a nuly
	- přijímač i vysílač má mapovací tabulku
	- tento způsob synchronizace se nazývá clock recovery, používá se např. v USB
		- vodiče v USB: 5 V, GND (tyto dva slouží k napájení připojeného zařízení), data+, data– (tyto dva zajišťují přenos dat)
		- zbylé dva způsoby synchronizace přenosu používají linky I²C (pomocí hodinového signálu) a RS-252 (pomocí start a stop bitů)
- linky simplex a duplex
	- přenos jedním směrem – simplex
	- přenos oběma směry – duplex
		- half-duplex – strany se musejí domlouvat, kdo zrovna posílá
		- full-duplex – nezávisle data přenášíme oběma směry → řešení pomocí dvou zcela nezávislých simplexních linek
			- např. RS-232
				- Rx – přijímající vodič (receiver)
				- Tx – vysílající vodič (transmitter)
				- dále se definují out-of-band signály
					- přenášejí se tam informace nezávisle
					- obvykle přenášejí konstatní nulu nebo jedničku – signál platí/neplatí
- běžné kódování – 0 = nepravda, 1 = pravda
	- power-out signál
		- někdy dává smysl to definovat obráceně – 0 = platí, 1 = neplatí → inverzní logika
			- obvyklá značení inverzní logiky na signálu SIG: SIG (s čárou nad textem), \#SIG, /SIG, !SIG, SIG (bílé písmo na černém pozadí)
- hodiny reálného času – RTC
	- chceme, aby nám zařízení poslalo tři informace – den, měsíc a rok
		- třeba 9 bitů na den, 5 bitů na měsíc, 7 bitů na rok
	- musíme si definovat, jak bude která informace dlouhá
	- komunikační protokol/formát
	- jeden logický blok dat = packet (tento packet by měl 21 bitů)
	- musíme se dohodnout na MSb-first / LSb-first
	- délka packetu nemusí být pevná, délka packetu může být definovaná uvnitř packetu
- řadič (controller) – zařízení, které zajišťuje ovládání linky (procesor → linka → řadič → linka → myš)
	- uvnitř je registr daného zařízení – data register
	- komunikace s řadičem z programu – musím mu říct, jak má interpretovat změny na datovém vodiči, který jde z myši
		- pomocí pyserial → serial → Serial
		- nastavení řadiče (config register)
		- status register – ukládá informaci, v jakém stavu je datový registr (např. 0 = no change, 1 = new byte in data register)
			- operace přečtení data registru zaznamená do status registru nulu
	- funkce, které komunikují se zařízeními, mají často nějaký timeout, aby čekání na data nebylo nekonečné

## 3. přednáška

- řadič řeší komunikaci programu s myší a překlad ze sedmibitových na osmibitové bajty
- sériovou myš také potřebujeme nějak napájet
	- běžně v USB konektoru jsou 4 piny, z toho dvoje data, zem a napájení
	- kvůli kompatibilitě se sériová myš připojovala pomocí RS-232 linky
	- RS-232 nemá napájecí konektor, ale pouze out of band signály
	- sériová myš je tedy napájená pomocí out of band signálů RTS a DTR nastavených na hodnotu 1
	- v řadiči je control register (modem control register) – pro každý out of band signál je tam jeden bit, který má hodnotu 0 (false) nebo 1 (true)
	- jak resetovat myš? stačí nastavit signály RTS a DTR na nulu → myš se po chvíli vypne → můžeme myš opět zapnout
	- (nemusíme si pamatovat, že to jsou zrovna RTS a DTR)
- po zapnutí myš pošle inicializační packet (init packet) – není přesně definován
	- po zapnutí myši tedy čekáme na X (třeba 1024) bajtů
	- čekáme pomocí funkce .read(n), tato funkce je ale blokující
	- ideální by byla neblokující funkce
	- řešením je nastavení timeoutu
- potřebujeme být schopni stisknout klávesu na klávesnici a začít dělat něco jiného
	- input() – blokující funkce
	- keyboard.is_pressed('\<key\>') → True/False – neblokující funkce
- přijímání dat z myši
	- bity jsou zprava doleva seřazeny 0–7 (podle zápisu čísla ve dvojkové soustavě)
	- myš posílá 7 bitů, takže MSb je pro ni bit č. 7
	- stisknutí levého tlačítka → packet 96 0 0 0
		- 96 = 64 + 32 = 2^6 + 2^5 → 01 10 00 00 (01 LR YY XX)
- co dělat s informací 738201600
	- šestnáctková/hexadecimální/hexa/hex soustava
	- značení čísla v šestnáctkové soustavě: $23, 23h, 0x23, $23_{16}$, $23_{hex}$
	- značení čísla v desítkové soustavě: $23_{10}, 23_{dec}$
	- pro uložení jedné číslice v šestnáctkové soustavě využijeme 4 bity
	- 1 bajt zaberou dvě šestnáctkové číslice
	- nuly na začátku čísla = leading zeros
	- $738201600_{10} =$ $2C001000 → 2C 00 10 00 → nenulové bity jsou pouze na některých místech
		- bity 29, 27, 26 a 12 jsou jedna
- čísla zadané v Pythonu v desítkové soustavě se ukládají ve dvojkové soustavě
- proměnou lze uložit v šestnáctkové soustavě, Python ji opět uloží ve dvojkové soustavě → není rozdíl mezi 35 a 0x23
- funkce print(a) vezme dvojkovou proměnnou a převede ji na string
- znaky stringu jsou uloženy pomocí osmibitových čísel
- funkce hex(a) vrací zápis čísla v šestnáctkové soustavě
- funkce format(a, '04X') doplní číslo o leading zeros na 4 číslice
- modifikovaný kód
	- packet 60 00 00 00 → první byte 01 10 00 00
- proč má první byte v 6. bitu jedničku?
	- abychom ho poznali od ostatních tří bytů a nedošlo ke špatné synchronizaci snímání komunikace myši
- bitové operace – obvykle dva argumenty (binární operace)
	- n-bitová operace (např. osmibitová – podle délky každého ze dvou vstupů a délky výstupu)
	- 8-bit operace – na vstupu dvě osmibitová čísla, na výstupu jedno osmibitové číslo
	- operace vždy vezme dva bity na stejné pozici, nějakým mechanismem je zkombinuje a výsledek uloží do bitu na téže pozici
	- operace or: 1010 | 1100 = 1110
		- můžeme kombinovat hodnotu a příkaz – jednička v příkazu znamená natvrdo nastavit výsledek na jedna, nula v příkazu znamená zkopírovat hodnotu do výsledku
		- nastavení bitu (na jedna) se označuje jako set
	- operace and: 1010 & 1100 = 1000
		- když je příkaz nula → nastav natvrdo nulu
		- když je příkaz jedna → zachovej hodnotu
		- vymazání bitu – clear (to 0)
	- bitová negace not ~
		- ~ 1010 = 0101
		- v Pythonu funguje jinak
	- operace xor (eor)
		- exkluzivní or
		- 1010 ^ 1100 = 0110
		- selektivní flip (not)
			- když je jednička, převrať hodnotu
			- když je nula, zkopíruj hodnotu
- jak zjistit, jestli je levé tlačítko stisknuté
	- použijeme bitovou masku
	- na ?? L? ?? ?? použijeme masku 00 10 00 00 a operaci and
	- dostaneme buď 00 00 00 00 → tlačítko není stisknuté, nebo 00 10 00 00 → tlačítko je stisknuté
	- B1 (byte 1) & 0x20 = 0x20 → levé tlačítko je stisknuté
- pohyb myši
	- kvůli přesnosti chceme použít 8 bitů, v jednom bytu je ale jenom 6 volných míst (máme 7bitový byte a bit č. 6 určuje pořadí bytu)
	- informaci tedy rozdělíme 1. a 2. bytu
		- B1 & 0x03
		- B2 & 0x3F
		- chceme ze dvou čísel 000000XX a 00XXXXXX dostat XXXXXXXX
			- použijeme magii a převedeme 000000XX → XX000000
			- XX000000 | 00XXXXXX = XXXXXXXX

## 4. přednáška

- potřebujeme magickou operaci, která nám umožní posunout bity
	- = bitové posuny (bitwise shifts)
	- posun doleva (shift left) – SHL (<<)
		- a << x → b
		- a – hodnota, se kterou chceme pracovat (n-bitové číslo)
		- b – výsledek operace (n-bitové číslo)
		- x – o kolik bitů se má posunout (celé číslo)
		- **posun k MSb!**
		- příklad
			- 4-bit 1101 (vlevo MSb, vpravo LSb)
			- SHL 1 → výsledek: 1010
				- o jedničku úplně vlevo jsme přišli, vpravo přibyla nula
			- SHL 3 → výsledek: 1000
			- SHL n → výsledek: 0000
	- posun doprava (shift right) – SHR (>>)
		- a >> x → b
		- funguje podobně jako SHL, akorát opačně
		- posun k LSb
	- rotace doleva (rotate left) – ROL
		- 1101 ROL 3 → 1110 (vysunuté bity nerušíme, ale ve stejném pořadí zasuneme z druhé strany)
		- výsledkem ROL n je identita
	- rotace doprava – ROR
		- 1101 ROR 2 → 0111
	- rotace Python nepodporuje

## 5. přednáška

- potřebujeme rozlišit posun myši nahoru a doleva → záporná čísla ve formě jedniček a nul
	- bezznaménková čísla (unsigned)
	- znaménková čísla (singed)
		- signed magnitude – 1 bit určuje znaménko, ostatní bity hodnotu čísla
			- z hlediska kompatibility je výhodné umístit znaménkový bit na místo MSb, přičemž 1 určuje záporné číslo, 0 kladné
			- při počítání pouze s nezápornými čísly ztrácíme polovinu rozsahu, takže se v takovém případě může hodit použít bezznaménková čísla
		- každý procesor podporuje operace pro bezznaménková čísla
			- můžeme libovolně přecházet mezi interpretací čísla jako znaménkového a bezznaménkového
			- nefunguje nám bezznaménkové porovnání na porovnávání záporných čísel (ani sčítání apod.)
		- jedničkový doplněk (ones' complement)
			- kladná čísla jsou zaznamenaná stejně jako unsigned
			- záporná jsou zaznamenaná znegovaně
		- jak udělat z kladného čísla záporné?
			- u signed magnitude pomocí operace XOR
			- u jedničkového doplňku negací
		- problém s nulou
			- máme dvě nuly – kladnou a zápornou
			- u jedničkového doplňku můžeme negovat a přičíst jedničku → dostaneme zpátky nulu
		- dvojkový doplněk (two's complement)
			- kladná čísla jako unsigned
			- záporná čísla jsou negace absolutní hodnoty plus 1
			- rozsah –128 až 127
			- nefunguje porovnání mezi kladnými a zápornými čísly – procesor musí podporovat znaménkové porovnání
			- MSb určuje znaménko
			- nejběžněji používaná implementace záporných čísel
- Python ke každému číslu ukládá počet platných bitů, ukládá je jako znaménková čísla
	- jejich rozsah je prakticky neomezený
	- při posunech (<< a >>) nikdy nepřijdu o číslice – Python si čísla před operací zvětší odpovídajícím způsobem
	- funkce bit_length() vrací bitovou délku čísla (bez znaménkového bitu)
	- knihovna numpy nám umožní vyrábět proměnné pevně daných typů (uint8, uint16, int8, …)
		- čísla intX jsou znaménková, takže tam mj. funguje porovnání
	- funkce type(x) nám vrátí typ čísla
- převod 8-bit čísla na 4-bit
	- operace truncation, přebytečné bity se zahodí – v podstatě $x \mod 2^n$
	- u čísel blízko nuly funguje dobře, u vzdálenějších čísel získáváme modulo
- převod 4-bit čísla na 8-bit
	- bezznaménkové rozšíření (zero extension) – na začátek se přidají čtyři nuly, nefunguje pro znaménková čísla
	- znaménkové rozšíření (signed extension) – rozkopíruje znaménkovou číslici do nových bitů, nefunguje pro bezznaménková čísla
	- v Pythonu se bezznaménkové rozšíření používá jenom při převodu mezi dvěma bezznaménkovými čísly, jinak se používá znaménkové rozšíření

## 6. přednáška

- Harvardská architektura – CPU čte z kódové paměti, čte z datové paměti a zapisuje do datové paměti
	- datové paměti můžeme říkat operační paměť (operating memory)
	- periferie komunikují s CPU jednosměrně nebo oběma směry (monitor posílá informace o rozlišení, klávesnice přijímá informace o rozsvícení diod)
- zařízení
	- master – řídí přenos (řídící – řídí komunikaci)
	- slave – poslouchá (řízený)
	- při komunikaci procesoru s pamětí je procesor master, paměť je slave
	- když data proudí směrem master → slave, tak jde o zápis, opačným směrem je to čtení
	- typický procesor funguje jenom jako master – abychom toto pravidlo neporušili, používáme řadič
		- řadič je potřeba u myši, u klávesnice tato potřeba obvykle není, protože se chová jako slave (uvnitř má vlastní registr)
- komunikační linka point-to-point – z procesoru by muselo vést mnoho vstupů/výstupů
- chceme komunikační linku, která umožňuje více vstupů/výstupů – multidrop/bus/sběrnice (linka se sběrnicovou topologií)
- nákres – z CPU vedou dvě sběrnice, na jedné jsou připojené paměti, na druhé perfiferie (myš za řadičem), CPU je master, všechno ostatní slave
- adresa (address) zařízení na sběrnici (typicky 0 až n)
	- v příkazu v programu pro procesor budou dvě informace – chci komunikovat se zařízením X na sběrnici Y
	- adresy zařízení musí být unikátní v rámci jedné sběrnice
	- rozsah adres (address space)
	- máme X bitový adresový prostor → platné adresy jsou $0$ až $2^x-1$
	- někdy i master musí mít vlastní adresu?
- zařízení je připojené na sběrnici
	- má Rx a Tx – může přijímat i vysílat data
	- je tam víc zařízení, zkusíme se obejít bez floating stavu
	- k lince připojíme 5 voltů přes rezistor s velkým odporem (pull-up rezistor, kdyby tam byla nula voltů, tak by to bylo pull-down rezistor)
	- když není žádné zařízení připojené k lince, tak je stav linky 1 (protože je tam těch pět voltů za rezistorem)
	- zařízení je připojené, ale nedělá nic → nepřipojí se ke sběrnici´→ stav linky je 1
	- zařízení je připojené a vysílá jedničku → nepřipojí se ke sběrnici → stav linky je 1
	- zařízení je připojené a vysílá nulu → připojí se (na malém rezistoru v zařízení na Tx je 0 V) → stav linky je 0

| D1 | D2 | bus |
|---|---|---|
| x | x | 1 |
| x | 1 | 1 |
| x | 0 | 0 |
| 1 | 1 | 1 |
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 0 | 0 | 0 |

- spodní čtyři řádky implementují AND
- $I^2C$ – Inter Integrated Circuit
	- vodič SDA – sériová data
	- vodič SCL – sériové hodiny
	- oba vodiče posílají digitální signál
	- oba vodiče jsou připojené na pull-up rezistor
	- napájecí napětí se označuje jako $V_{DD}$ nebo $V_{CC}$
	- pod 30 % $V_{DD}$ se považuje za nulu, nad 70 % za jedničku
	- multimaster – různá zařízení můžou být master
		- existují i singlemaster sběrnice – např. USB
	- musíme rozeznat idle stav od přenosu
		- SCL tiká jenom během přenosu, generuje ho master
		- dvě jedničky (na SDA i SCL) znamenají idle stav
		- na lince existují nepovolené stavy – např. změna stavu na SDA při jedničce na SCL – toho využijeme jako START a STOP condition
			- START condition = sestupná hrana na SDA při jedničce na SCL
			- STOP condition = vzestupná hrana na SDA při jedničce na SCL
	- sběrnice má 9-bitové byty: 8 data bit + 1 control bit
		- kontrolní bit (acknowledgement/potvrzovací/ACK bit)
			- (acknowledgement = ACK × negative acknowledgement = NACK/NAK)
		- první byte vždycky posílá master, slave ho potvrzuje kontrolním bitem
		- další byty posílá vysílající a přijímající potvrzuje (pokud přijímající přestane potvrzovat, vyhodnotí se to jako NAK)

|  | B1 | a1 | B2 | a2 | B3 | a3 |  |
|---|---|---|---|---|---|---|---|
| write | M | S | M | S | M | S | NAK |
| read | M | S | S | M | S | M | NAK |

- MSb-first komunikace
- série bytů tvoří packet, ten se dělí na overhead ($I^2C$ control) a payload (device specific – požadovaná data)
- $I^2C$ sestává ze slave address (7-bit) a bitu určujícího směr přenosu $R/\bar W$
	- read = 1, write = 0
	- devátý control bit má obrácenou logiku – 0 = ACK, 1 = NAK (typicky pokud tam slave není)
- když slave nestíhá, tak může v hodinovém signálu generovat nulu → master ví, že nemůže posílat další data – tomu se říká clock stretching / hold clock low

### Ambient Light Sensor (ALS)

- ve smartphonu určuje intenzitu okolního světla a podle toho se určuje intenzita podsvícení
- v datasheetu najdeme informace o fungování
- zařízení má čtyři piny – VDD (napájení), GND (zem), SDA (data), SCL (hodiny)
- v zařízení bude senzor a logika
- součástí logiky je counter register – zajišťuje počítání intenzity světla
- měření v intervalech (na začátku měření se counter vynuluje)
- příkazy start integration a stop integration
	- command register (cmd reg)
- při extrémních hodnotách lze softwarově prodloužit/zkrátit dobu měření, abychom vůbec něco naměřili (to zajišťuje procesor zařízení)
- counter register = ADC register (analog digital converter)
	- existuje také DAC (digital analog converter) – opačný proces, z digitálního signálu se generuje např. analogová intenzita světla
	- v ALS má 2 byty – z toho 15 datových bitů a jeden valid bit
- připojení na sběrnici zajišťuje bus interface – skrze něj máme jako programátoři přístup k registrům
	- write-only register (W/O)
	- read-only register (R/O)
	- read-write register (R/W) – v ALS nenajdeme
	- v případě ALS bude „zápis“ znamenat zápis do W/O cmd registru a „čtení“ bude znamenat čtení z R/O counter registru
	- adresa zařízení na sběrnici je pevně daná výrobcem – hardwired/zadrátovaná, v tomto případě je to $29 – na jednu sběrnici tedy nemůžu připojit dvě stejná zařízení, protože by měla stejnou adresu
- u vícebytových čísel se rozlišuje LSB (byte s LSb) a MSB (byte s MSb)
- kromě bit order se určuje byte order
