# Zkouška

## Relační algebra

- operace
	- množinové $R\cup S,\;R\cap S,\;R\setminus S,\; R\times S$
	- selekce $R(\text{cond})$
	- projekce $R[\text{attr1},\text{attr2}]$
	- spojení $R[\text{cond}]S$
	- přirozené spojení $R*S$
	- přejmenování $R\braket{\text{attr1}\to\text{x1},\text{attr2}\to\text{x2}}$
	- dělení $R\div S$
- přirozené spojení
- dělení

## Normální formy a funkční závislosti

- normální formy
	- 1NF
	- 2NF
	- 3NF
	- BCNF
- funkční závislosti
	- rozepsání na elementární závislosti
	- redukce redundantních atributů
	- odstranění redundantních závislostí
	- nalezení klíčů
	- zachování závislostí při dělení podle normálních forem

## Transakce

- uspořádatelnost rozvrhu
- konfliktní uspořádatelnost
- pohledová uspořádatelnost
- zamykací protokol
- 2PL
- S2PL

## Teorie

### Multimédia

- Popište naivní způsob, jak rozšířit Tabulku pro potřeby hledání v obrázcích. Jaké jsou možnosti a omezení tohoto přístupu?
- Definujte klasický podobnostní model pro dva obrázky, vysvětlete z jakých funkcí se skládá. Na „toy example” ukažte princip hledání v DB, kde je 5 obrázků.
- Definujte moderní podobnostní model pro text a obrázek, vysvětlete z jakých funkcí se skládá. Na „toy example” ukažte princip hledání v DB, kde je 5 obrázků.
- Popište Bayesovský model pro hledání za pomocí zpětné vazby. Popište všechny kroky jedné iterace.

### Moderní DB systémy

- Popište limity relačního modelu pro Big Data, které jsou popsány v přednášce.
- Key-value – popište model, jaké podporuje základní funkce, názvosloví tabulek atp. v Riak, na jaké úkoly je model vhodný a na jaké ne.
- Column-family – popište model, jaké podporuje základní funkce, názvosloví tabulek atp. v Cassandra, na jaké úkoly je model vhodný a na jaké ne.
- Document DB – popište model, jaké podporuje základní funkce, názvosloví tabulek atp. v MongoDB, na jaké úkoly je model vhodný a na jaké ne.
- Graph DB – popište model, jaké podporuje základní funkce, na jaké úkoly je model vhodný a na jaké ne.

### Datové struktury a optimalizace

- Nad jakými sloupci je vhodné vytvořit index založený na B+-stromu / bitmapách? Uveďte příklad.
- Popište změny v rychlosti databázových operací nad tabulkou po vytvoření (no)clusterovaného indexu nad nějakým sloupcem.
- Popište hlavní rozdíly mezi clusterovaným a neclusterovaným indexem.
- Popište (ne)výhody použití tříděného souboru oproti souboru netříděnému (heap-file) z hlediska rychlosti DB operací pro ukládání záznamů tabulky.
