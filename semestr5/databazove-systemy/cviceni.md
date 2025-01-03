- konceptuální modelování
	- UML – primárně pro OOP
	- ER model – šitý na míru relačním databázím
- ze zákazníka chceme dostat
	- typy objektů
	- vztahy mezi objekty
		- arita – kolika objektů se týká daný vztah
		- kardinalita – např. kolik studentů si může zapsat jeden předmět (nejvýš jeden, aspoň jeden, několik, … ?)
	- atributy – co všechno potřebujeme o objektech a vztazích ukládat
		- kardinalita
- když si potřebuju vztah pamatovat vícekrát, převedu ho na entitu/třídu
- evidence HW/SW
	- počítače, OS, SW s verzemi
- řešení úlohy s dvojicemi kin, které mají stejné filmy
	- „všechny povolené dvojice kin“ – ((„dvojice kin a filmy z prvního“ U „dvojice kin a filmy z druhého“) – „dvojice kin a společné filmy“)

```
(cinemas<name→name1>[name1<name2]cinemas<name→name2>)[name1,name2]
- (
    ((program<name→name1>×cinemas<name→name2>)[name1,name2,title] ∪ (program<name→name2>×cinemas<name→name1>)[name1,name2,title])
    - (program<name→name1,title→title1>[name1<name2]program<name→name2>)(title1=title)[name1,name2,title]
)[name1,name2]
```

### Poznámky z poslední přednášky

- tabulky jsou uložené v souborech na disku, aby přežily vypnutí počítače
	- disky pracují s bloky, čtecí operace přečte blok
	- datové struktury musejí být zarovnané na bloky
	- sekvenční čtení je výrazně rychlejší než náhodné (to platí pro HDD)
	- časová složitost je primárně ovlivněna množstvím bloků, které musíme přečíst
	- jeden blok obsahuje nějaké řádky
	- někdy je problém s tím, že řádka může mít proměnnou šířku
- databáze má obvykle mezivrstvu
	- pracuje nad pamětí (bufferem), na disk se zapisuje nezávisle
	- aby to bylo rychlé
	- záznamy lze v souboru mít uloženy na hromadě (heap) nebo v nějakém pořadí (sorted file)
	- taky jsou v souborech typicky nějaké indexy
- cena operací – heap file vs. sorted file
- index
	- clustered × unclustered
		- unclustered index
			- bloky nemají správné řazení → musím ukazovat na jednotlivé záznamy
			- intervalové hledání trvá déle, musí se procházet různé bloky
		- clustered index
			- stačí ukazovat jen na začátky bloků
	- jak se ukládají indexy
		- $B^+$-stromy
			- ukládají data po blocích
			- jsou vyvažované
			- algoritmus vkládání a mazání je dělaný tak, aby bloky byly aspoň z poloviny zabrané
			- „plus“ znamená to, že jsou listy (obsahují data) pospojované, takže se dají efektivně dělat sekvenční dotazy
		- to se ale nehodí třeba pro binární hodnoty
			- k tomu se používají bitmapové indexy
			- vyrobí se několik bitmap – pro každou hodnotu výčtového typu bude jedna
- soubory
	- databáze typicky nedělá pro jednu tabulku jeden reálný soubor
	- vyrobí si jeden reálný soubor, v něm má spoustu logických souborů, ty si spravuje sama
- indexy
	- vyrábějí se automaticky pro primary a unique sloupce
	- dají se vyrábět i ručně
	- pokud dělám index nad více sloupečky, tak to bude efektivně index nad zřetězením sloupečků
- životní cyklus select query
	- parsování SQL a validace
	- kontrola existence plánu v shared poolu
	- pokud plán neexistuje, vygeneruje se co nejvíc plánů a spočítají se jejich ceny → vybere se nejlevnější plán
	- plán se vykoná
- plán
	- jsou různé metody přístupu k datům – každá trvá jinak dlouho
	- nejlepší plán lze vybrat podle toho, jaké metody používá (rule based), nebo podle toho, jak dlouho by mohl trvat (cost based)
	- můžeme dávat doporučení plánovači, ale bacha na premature optimization
