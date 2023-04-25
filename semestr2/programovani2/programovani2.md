# Programování 2

- permutace – je jich 14, aby se indexy vešly do číselného typu (vejde se to longu)
	- 25. permutace je 21345
		- protože 24 je permutací se stejným prvním číslem (permutuješ poslední čtyřčíslí)
	- 49. je 23145?
		- ne, je 31., protože 24+6=30, permutace nemůže začínat 22xxx
- pexeso
	- alespoň 16 párů kartiček (naklikat ručně nebo generovat automaticky – při generování jich může být i míň)
	- může tam být jakýkoliv obsah
	- hra hráče proti počítači
	- počítač by si neměl pamatovat všechno, ale měl by si pamatovat něco
- zápočťák
	- [https://ksvi.mff.cuni.cz/~holan/MSVS_GitLab.pdf](https://ksvi.mff.cuni.cz/~holan/MSVS_GitLab.pdf)  
	- zápočťák 2000 řádků (něco přes 1000 funkčního kódu)  
	- náročnost u MJ jako 4, 5  
	- v červenci a srpnu tady Pergel pro nikoho není  
	- do konce semestru vybrat téma  
	- do prázdnin přijít s alfa verzí  
	- má to být v C#, leda by byl dobrý důvod
	- k mým návrhům (diff, akordy) – obě varianty jsou použitelné
- https://kam.mff.cuni.cz/~perm/programovani/NMIN201/objektovy_navrh/
- úlohy na dynamické programování
	1. opíjení u piva, vína, tvrdého
		- n drinků
		- hned po vínu není tvrdý
		- hned po tvrdém není víno ani tvrdý
	2. T, F, ^, v, !
		- vstup: konstantní bool. výraz (bez závorek – skládá se ze znaků výše)
		- výstup: počet možných uzávorkování, aby to byla pravda
		- u konjunkce spolu vynásobím, kolika způsoby lze splnit levý výraz a kolika způsoby lze splnit pravý výraz
		- kvůli disjunkci si musím evidovat i kolika způsoby lze výraz nesplnit
		- rekurze podle posledního operátoru
	1. mosty
		- nesmějí se křížit
		- maximální počet mostů
		- nahoře čísla 1 až n
		- dole permutace 1 až n
		- spojujeme stejná čísla – hledáme co největší počet nekřížících se spojení
		- nápověda: některý most bude poslední
	1. pokleslá podposloupnost
	2. salámy
		- vstup je počet požadovaných centimetrů (n) a cena salámů o délkách 1 až n
		- výstup je nejlevnější kombinace
	3. loupežníci
	4. editační vzdálenost
		- skaly → laska (odeberu ly, přidám la)
		- některá operace bude poslední
		- voláme rekurzivně lps(začátek1,začátek2,délka1,délka2)
		- tabulka, kde jsou řádky podle znaků jednoho stringu a sloupce podle znaků druhého stringu
	1. čínský mobil
- podposloupnost
	- rekurzivní:
	- nevíme, který prvek bude poslední → zkusíme všechny
	- nevíme, který prvek bude před ním → zkusíme všechny
	- délka nejdelší podposloupnosti končící v daném místě je X → uložíme do cache
	- pokleslá podposloupnost = dvě nejdelší podposloupnosti za sebou
	- takže spočítáme cache nejdelší podposloupnosti začínající v daném místě