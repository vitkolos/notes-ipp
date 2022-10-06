# Úvodní hodina

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

![timing-diagram](přílohy/timing-diagram.png)

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

![](přílohy/Pasted%20image%2020221006151451.png)

![](přílohy/Pasted%20image%2020221006151438.png)

- diferenciální přenos
	- data 1 – data 2
	- >0 = 1
	- <0 = 0
- řešení problému se dvěma jedničkama / dlouhou jedničkou
	- pevná délka bitu
		- definuje se přenosová rychlost
			- v bitech za sekundu (bits per second, bps)
			- jednotka baud (symbol za sekundu) – obvykle budeme uvažovat x baud = x bps, ale jeden symbol může obsahovat více bitů
			- 