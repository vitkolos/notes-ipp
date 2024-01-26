# Zkouška

## 1. Úvod

- historie robotiky
	- prehistorie
		- Leonardo Da Vinci
		- japonské mechanické panenky
		- Karel Čapek: R.U.R. (Rossumovi univerzální roboti)
	- manipulátory (ve 20. století)
		- manipulace s radioaktivním materiálem
		- počítačem řízená mechanická ruka
	- v druhé polovině 20. století
		- mobilní dálkově ovládaní roboti
		- mobilní autonomní roboti
- zákony robotiky
	- Robot nesmí ublížit člověku nebo svou nečinností dopustit, aby bylo člověku ublíženo.
    - Robot musí uposlechnout příkazů člověka, kromě případů, kdy jsou tyto příkazy v rozporu s prvním zákonem.
    - Robot musí chránit sám sebe před poškozením, kromě případů, kdy je tato ochrana v rozporu s prvním, nebo druhým zákonem.
- základní pojmy
	- robot je obvykle univerzální – je možné ho přeprogramovat
	- manipulátor – je určený k vykonávání jedné konkrétní práce

## 2. Kinematika a dynamika

- póza = poloha + orientace
	- ale občas se póza zaměňuje s polohou
	- typicky nás zajímá stav robota, tzn. poloha, orientace, stav nabití baterie, …
- dopředná úloha kinematiky – víme, o kolik jsme pohli manipulátorem, zajímá nás, kam se dostal
- zpětná úloha kinematiky – víme, kam se chceme dostat, zajímá nás, jak to uděláme
- kinematika = pohyb jednotlivých částí robota bez vztahu k silám
- obvykle nás zajímá ještě dynamika
- dopředná úloha kinematiky je vlastně násobení transformačních matic
- ve zpětné úloze kinematiky počítáme úhly pomocí původních a cílových souřadnic

### 2.1. Stupně volnosti, kinematický řetězec

- stupně volnosti
	- základní směry translace a rotace
	- stupeň volnosti = počet nezávislých proměnných v systému
	- 2D … 3 stupně volnosti ($x,y,\alpha$)
	- 3D … 6 stupňů volnosti (3 translace, 3 rotace)
		- někdy se jeden úhel nepočítá vůči rovině, ale vůči ose otáčení daného nástroje (např. šroubováku)
		- natočení
			- podle $x$ = roll, náklon
			- podle $y$ = pitch, sklon, zdvih, sklopení
			- podle $z$ = yaw, otočení, směr (to není úplně vhodné označení)
			- ![pitch axis, roll axis, yaw axis](https://upload.wikimedia.org/wikipedia/commons/1/16/Yaw_Axis.svg)
				- [Auawise derivative work: Jrvz - Yaw_Axis.svg, CC BY-SA 3.0](https://commons.wikimedia.org/w/index.php?curid=9441238)
- používáme pravotočivý systém (pravou rukou, prsty ukazují směrem $x$, zavřením dlaně je otočím k ose $y$, palec ukazuje směr osy $z$)
- kladný směr otáčení je proti směru hodinových ručiček

### 2.2. Pohyb a transformace

translace, rotace, sférický pohyb

## 3. Mechanika a mechatronika

senzory, aktuátory, nízkoúrovňové řízení

### 3.1. Metody pohybu, modely vozidel

### 3.2. Senzorické systémy

### 3.3. Pohonné systémy, řízení pohybu a rychlosti

### 3.4. Jednočipy, MCU, SoC

## 4. Software a algoritmy řízení robotů

### 4.1. Softwarové architektury, implementační metody

### 4.2. Kognitivní robotika, umělá inteligence

### 4.3. Lokalizace a mapování

Kalmanův filtr, metody Monte Carlo, pravděpodobnostní metody

### 4.4. Plánování, navigace

### 4.5. Pokročilá senzorika, zpracování obrazu

### 4.6. Multirobotické systémy
