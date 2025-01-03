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
