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
- https://kam.mff.cuni.cz/~perm/programovani/NMIN201/objektovy_navrh/
- úlohy na dynamické programování
	1. opíjení u piva, vína, tvrdého
		- n drinků
		- hned po vínu není tvrdý
		- hned po tvrdém není víno ani tvrdý
	1. T, F, ^, v, !
		- vstup: konstantní bool. výraz
		- výstup: počet možných uzávorkování, aby to byla pravda
	2. mosty
	3. pokleslá podposloupnost
	4. salámy
	5. loupežníci
	6. editační vzdálenost
	7. čínský mobil
- podposloupnost
	- rekurzivní:
	- nevíme, který prvek bude poslední → zkusíme všechny
	- nevíme, který prvek bude před ním → zkusíme všechny
	- délka nejdelší podposloupnosti končící v daném místě je X → uložíme do cache
	- pokleslá podposloupnost = dvě nejdelší podposloupnosti za sebou
	- takže spočítáme cache nejdelší podposloupnosti začínající v daném místě