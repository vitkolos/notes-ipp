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
	- robot – obvykle je univerzální, je možné ho přeprogramovat
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
			- ![pitch axis, roll axis, yaw axis](https://upload.wikimedia.org/wikipedia/commons/c/c1/Yaw_Axis_Corrected.svg)
				- [Auawise derivative work: Jrvz - Yaw_Axis.svg, CC BY-SA 3.0](https://commons.wikimedia.org/w/index.php?curid=9441238)
	- používáme pravotočivý systém (pravou rukou, prsty ukazují směrem $x$, zavřením dlaně je otočím k ose $y$, palec ukazuje směr osy $z$)
	- kladný směr otáčení je proti směru hodinových ručiček
- manipulátory
	- slouží k manipulaci objektu v prostoru – požadujeme aspoň 6 stupňů volnosti ve 3D
	- stav jednoho kloubu popisuje jedna proměnná (joint variable $q_i$)
		- může být vícesložková
	- stavový vektor (joints state) $q=[q_1,q_2,\dots,q_n]$
		- $n$ stupňů volnosti
- pracovní prostor (working space) – kartézský součin všech proměnných
- lokální vs. globální souřadný systém (local × global coordinate system – LCS, GCS)
	- lokální systém je někdy výhodnější – pokud se něco změní u jednoho kloubu, stačí to softwarově změnit pouze u něj
	- typicky nás zajímají globální souřadnice
- typy kloubů
	- otočný (revolute) – 1 stupeň volnosti
	- prismatický = píst (prismatic) – 1 stupeň volnosti
	- šroub (helical) – 1 stupeň volnosti
	- cylindrical – 2 stupně volnosti
	- spherical – 3 stupně volnosti (pohyb kolem dvou os + otáčení)
	- planar – 3 stupně volnosti (posun ve dvou osách + otáčení)
- obvykle se používají prismatický a otočný
- různé z těchto kloubů se dají najít i v lidském těle
- poloha … stavový vektor o tolika složkách, kolik jich potřebujeme
- rotace
	- $P$ … poloha
	- $R$ … rotační matice
	- $P'=R\cdot P$
	- $R_{x,\phi}=\begin{bmatrix}1&0&0\\0&\cos\phi&-\sin\phi\\0&\sin\phi&\cos\phi\end{bmatrix}$
		- rotace podle osy $x$
	- používáme písmenka fí $\phi$, psí $\psi$, xí $\xi$
- rotace a translace
	- $P'=R\cdot P+T$
	- místo $T$ (translation) se někdy píše $D$ jako displacement
- jak to kombinovat?
	- $P'=R_2\cdot(R\cdot P+T)+T_2$
- homogenní souřadnice ve 2D
	- bod vyjádřím jako $p=(x,y,w)^T$
	- kde $w$ je projekce do nějaké roviny
	- budeme pracovat s $w=1$
	- rotace v rovině vypadá stejně jako rotace podle osy $z$ v prostoru (takže u třetí souřadnice bude identita)
	- translaci $p'=p+\mathcal D_p$ uděláme pomocí násobení matic
	- $(x',y',w')^T=\begin{pmatrix}1&0&d_x\\0&1&d_y\\0&0&1\end{pmatrix}\cdot\begin{pmatrix}x\\ y\\ w\end{pmatrix}$
- dopředná kinematika ve 3D
	- $P=f(q)$
	- $q=[q_1,q_2,\dots,q_6]$
	- $P=[x,y,z,\alpha,\beta,\gamma]$
- složení systému
	- obecné
		- každý kloub je reprezentován svou geometrickou transformací
		- přechod mezi lokálními souřadnicovými systémy
		- může být těžké vytvořit celkovou zkombinovanou transformační matici
	- Denavit-Hartenberg
		- pokud jsou systémy šikovně navrženy
		- funguje ve 3D
		- fiktivní pohyby spojující dva systémy – rotate (podle osy $z$), move (po ose $z$), move (po ose $x$), rotate (podle osy $x$)
		- v libovolně dlouhé sekvenci
- Denavit-Hartenberg (DH) systém
	- systém je složen z rotačních a posuvných kloubů, mezi klouby jsou spoje
	- vztah mezi $LCS_{i-1}$ a $LCS_i$ je složená trasformace
		- natočení osy $x_{i-1}$ kolem osy $z_{i-1}$ o úhel $\vartheta_i$
		- posunutí osy $x_{i-1}$ ve směru osy $z_{i-1}$ o vzdálenost $d_i$
		- posunutí počátku $LCS_{i-1}$ podél osy $x_i$ o vzdálenost $a_i$
		- natočení osy $z_{i-1}$ kolem osy $x_i$ o úhel $\alpha_i$
	- DH parametry $\vartheta_i,d_i,a_i,\alpha_i$
		- $\vartheta_i$ … úhel mezi osami $x$ kolem $z_{i-1}$
		- $d_i$ … vzdálenost mezi osami $x$
		- $a_i$ … vzdálenost mezi osami $z$
		- $\alpha_i$ … úhel mezi osami $z$ kolem $x_i$
	- osy $z$ jsou dány tím, jak to kdo vyrobil
	- osu $x$ si zvolím tak, aby byla kolmá na $z_i$ a $z_{i-1}$
	- $\vartheta_i$ a $d_i$ jsou (můžou být) proměnné, zbytek jsou konstanty
	- konstrukce D-H řetězce
		- očíslování kloubů $0$ až $n$ ($0$ je první, pevný)
		- očíslování článků $1$ až $n$ (článek $i$ spojuje klouby $i-1$ a $i$)
		- používáme ortonormální pravotočivý souřadný systém
		- osa $z_{i-1}$ je osou pohybu kloubu $i$ (kloub kolem ní rotuje nebo se jejím směrem posouvá)
		- $x_i$ je osa přechodu mezi $z_{i-1}$ a $z_i$ (posunu nebo rotace)
			- nechť je kolmá na $z_{i-1}$ a $z_i$
			- když jsou $z$ rovnoběžné nebo totožné, tak ji nechám rovnoběžnou s $x_{i-1}$
			- když jsou $z$ mimoběžné, tak ať kladný směr vede ze $z_{i-1}$ do $z_i$ ($x_i$ je ve společné normále)
			- když jsou $z$ různoběžné, ať je kladný směr takový, aby se z $z_{i-1}$ do $z_i$ rotovalo kladným směrem
		- osa $y_i$ je doplněna tak, aby vyhovovala pravotočivému systému
		- počátek $LCS_i$ je umístěn do průsečíku $z_{i-1}$ a $z_i$ nebo do průsečíku jejich společné normály a $z_i$ (pokud se neprotínají)
	- někdy je potřeba přeznačit osy – v takové situaci bude jeden řádek tabulky bez proměnné
- inverzní kinematika
	- jak mají být klouby natočeny, aby byl konec manipulátoru v daném bodě?
	- pro RRR manipulátor ve 3D – natočíme první R vhodným směrem a pak máme úlohu ve 2D
	- RR ve 2D je úloha o úhlech v trojúhelníku, jehož tři strany známe
	- Stewart platform – umožňuje libovolné naklonění roviny
	- řešení obecné úlohy inverzní kinematiky
		- vektorová metoda
		- numerické metody – např. aproximační, optimalizační (heuristické, gradientové)
		- složitost obvykle závisí na konkrétní kinematické soustavě

## 3. Mechanika a mechatronika

### Modely vozidel

- holonomní / neholonomní vozidla
	- Heinrich Hertz – stupně volnosti
		- vozidlo je holonomní, pokud se počet lokálních stupňů volnosti rovná počtu globálních stupňů volnosti
	- pokud je počet lokálních stupňů volnosti větší než počet globálních stupňů volnosti, máme přezadaný systém – v reálném světě se některá kola smýkají
	- vlak … holonomní (v 1D prostoru jezdí dopředu a dozadu)
	- auto … neholonomní (v 2D prostoru jezdí dopředu a dozadu, otáčí kola, ale nemůže jet do boku)
- pokud chceme najít výslednou polohu, integrujeme přes čas
- Ackermannovo řízení
	- neholonomní
	- natáčím jednu soupravu (jako u auta)
	- v zatáčce je potřeba, aby vnitřní kolo bylo natočeno jinak než vnější kolo (tzn. nelze natáčet přímo osu, na které jsou kola – v takovém případě se kola smýkají)
	- zatáčí se posouváním tyče rovnoběžné s přední osou, ta je ke kolům připojena tyčemi, jejichž prodloužení se protínají uprostřed zadní osy („delta“?)
	- v praxi se používá složitější konstrukce
- differential steering (diferenciální řízení?)
	- neholonomní
	- zatáčím rozdílem rychlosti levého a pravého kola (jako u tanku)
	- použití v praxi
		- obecnou trajektorii nahradím sérií úseček nebo oblouků
		- musím rozumně určit $\Delta t$ – ne moc malé, abych pořád nepočítal, ale ne moc velké, abych dostal rozumné výsledky (situace: obě kola ujely stejně, ale nejdřív jedno stálo a druhé se točilo a pak naopak)
		- musím změřit vzdálenost
- omnidirectional steering
	- holonomní
	- kola mohou jet libovolným směrem
	- příklady
		- swerve/crab drive – lze otáčet kolem o 360 stupňů
		- omniwheel – kolo má po obvodu válečky, které mohou volně prokluzovat ve směru kolmém na směr otáčení kola
		- mecanum wheel – velmi podobné jako omniwheel, ale válečky jsou otočeny o 45 stupňů; když točím kolem, tak výsledný pohyb směřuje šikmo (rovněž pod úhlem 45 stupňů)
		- Killough / Ilon wheels
		- syncrodrive – není úplně omnidirectional, všechny kola jsou natočeny stejným směrem
	- špatná prostupnost terénem
	- jednoduchá mechanická konstrukce pro omniwheels a mecanum wheels

### Elektromotory

- typy elektrických motorů
	- DC (stejnosměrný)
		- brushed (kartáčový)
		- brushless (bezkartáčový)
	- AC (střídavý)
		- synchronní
		- asynchronní (indukční)
	- piezoelektrický, ultrasonický, …
	- (pneumatický, hydraulický, …)
- hlavní princip stejnosměrných motorů
	- elektro-mechanické zařízení
	- magnetické pole + elektrický proud → síla
		- podle Flemingova pravidla levé ruky
- DC brushed
	- v nejjednodušší formě: stator, rotor (armatura), kartáče (uhlíky), komutátor
	- typy
		- s permanentním magnetem
		- vinutý (wound) stator
			- shunt (paralelní) vinutí (= derivační motor)
			- sériové vinutí (= motor se sériovým buzením)
			- paralelní i sériové vinutí (= kompaundní motor)
	- problém – když jsou kartáčky zarovnané s mezerou mezi póly
		- nulový točivý moment
		- zkrat
	- řešení – širší mezera? víc pólů
	- kontrola rychlosti
		- regulace napětí
			- fixní voltáž + rychlé vypínání/zapínání → PWM
		- regulace frekvence – pro střídavý proud
		- PWM = pulse-width modulation (pulsně-šířková modulace)
	- kontrola směru otáčení pomocí H-můstku (H-bridge) – určuje směr toku proudu
- DC brushless
	- stator z cívek, rotor z permanentního magnetu
	- nebo SRM – switched reluctance motor (rotor je vyroben z magneticky slabého materiálu)
	- externí komutace – přepínání cívek (je potřeba znát pozici hřídele – pomocí Hallových senzorů nebo BEMF)
	- výhody
		- méně opotřebovávaných částí – větší spolehlivost
		- lehčí rotor, lepší dynamika
		- může operovat ve vysokých otáčkách
		- méně hluku a EMI (electromagnetic interference) než u kartáčových
	- problémy
		- stabilita při vysoké rychlosti
		- kolísavost točivého momentu
	- vlastnostmi jsou lepší než brushed (asi?)
- krokové motory
	- stator z cívek, rotor z magnetu
	- zubatá konstrukce
	- jednopólové nebo dvojpólové zapojení
	- krokování
		- 1f full – rotor je natočený k aktivní cívce
		- 2f full – rotor je natočený ke dvěma aktivním cívkám
		- half – střídají se stavy, kdy je aktivní jedna nebo dvě cívky, takže se motor otáčí po polovinách kroků
		- mikrostepping – cívky nejsou binární, ale po nějakých krocích se jim mění proud
	- výhody
		- vhodné pro precizní pozicování
		- levná kontrola, jednoduchá konstrukce
		- k řízení nepotřebuje zpětnou vazbu = je možná open-loop kontrola
	- problémy
		- nízká efektivita
		- nízký moment ve vysokých rychlostech
		- špatná dynamika
- brushless DC vs. stepper
	- oba jsou bezkartáčové
	- typicky (ne vždy)
		- BLDC má jen pár pólů (maximálně 8), stepper jich má víc
		- BLDC closed-loop (k řízení používá zpětnou vazbu), stepper open-loop
		- BLDC pro vyšší otáčky, stepper pro nižší
		- BLDC pro rotaci, stepper pro pozici
- servo motor
	- je to vlastně motor + nějaká další elektronika zajišťující zjištění pozice osy a nějaké řízení (tzv. zpětná vazba)
	- neurčujeme rychlost (otáčky), ale natočení hřídele
	- RC servo
		- otáčí se podle délky pulzů
		- má omezení – nemůže se otáčet kolem dokola (obvykle kvůli potenciometru)
		- obsahuje převodovku
		- pulzní signál má dlouhé mezery – aby se dalo ovládat více servomotorů
	- na principu servomotoru funguje třeba naklápění světel v autě
	- je možné mít i víceotáčková serva
	- RC „digitální servo“ – dva typy
		- jedno podobné jako analogové (jen elektronika uvnitř používá digitální signál, tudíž může mít hladší chod než analogové – lze ho bez problémů vyměnit s analogovým)
		- druhé komunikuje digitálně s ovladačem, je programovatelné
	- „hacknuté“ servo
		- místo potenciometru použijeme pevný odpor – řekneme servu, že je v půlce
			- někdy je potřeba doladit, aby se servo opravdu netočilo (kvůli nepřesnostem při výrobě odporů apod.)
		- takže když mu řekneme, kam se má otočit, ono se tam bude točit (ale nikdy tam nedojde)
		- tudíž místo natočení udáváme rychlost
			- PWM (pulsně-šířková modulace) ovládá směr a rychlost
				- 1.5 ms → servo se netočí
				- míň nebo víc → servo se točí (jedním nebo druhým směrem)
		- u digitálních serv to nelze (rozhodně ne u druhého typu, u prvního typu někdy)

### Senzory

- lidské smysly – není jich jen pět (dále rovnováha, zrychlení, bolest, tlak, čas, teplota, …)
- někdy mě zajímá jen detekce (je tam překážka?), jindy měření hodnoty (jak je daleko?)
- senzory
	- lokální – taktilní (např. nárazník, měření elektrického signálu)
	- bezdotykové – měříme vzdálenost, světlo apod.
	- virtuální – měříme „vlastnosti robota“, např. proud, který jde do motoru, z toho zjistíme, že narazil na překážku → nepotřebujeme koncové senzory
- pokročilé – radar, lidar, kamera, hloubková kamera, IMU, …
- aktivní × pasivní měření
- oblíbené senzory v robotice
	- taktilní – mikrospínače, koncové spínače, „nárazníky“
	- elektrické – měření spotřeby proudu motorem, měření indukovaným proudem
	- směrové akustické, optické – měření detekcí odraženého paprsku (detekce překážek, mapování prostředí)
	- liniové senzory – směrové měření multiplexované v čase
	- kamery – zpracování obrazu
	- MEMS (micro-electromechanical systems) – používají mikroskopické jevy
	- virtuální – nepřímé měření, používají důsledky akcí k jejich detekci (např. virtuální nárazník)
- měření pomocí odrazu signálu
	- metody
		- direct TOF (time of flight)
			- měřím čas, jak dlouho signál letí
			- je potřeba přesně měřit čas
			- pomocí světla se malé vzdálenosti měří těžko – lepší je zvuk
		- pulsed TOF
			- přenáším pulzy
			- měřím poměr signálu, který se vrátil před a po události
		- phase-shift
			- počítám vzdálenost z fázového posunu
	- typy signálu – infračervené záření, laser, radar, ultrazvuk
	- signál se musí odrazit, jinak nic nezměřím
	- měření je aktivní
		- jsem závislý na prostředí, ve kterém měřím
		- může tam být interference s jiným senzorem stejného typu
		- je to detekovatelné nepřítelem (ve vojenském prostředí)
- měření pomocí přerušení signálu
	- pomocí brány – dvě části na sebe „svítí“, pokud signál nedoletí, tak mezi nimi něco je
	- lze detekovat odražení signálu nebo absenci odražení…
	- typicky se hodí informace o intenzitě signálu
	- někdy takhle fungují kolečka na myších (fungovaly tak kuličkové myši)
- ultrazvuk
	- přímé měření času letu signálu je možné
	- typicky měří v rozsahu 1 cm – 10 m
	- používá se neslyšitelné spektrum (vhodné jsou hodnoty kolem 40 kHz, aby to neslyšela ani zvířata)
	- měří to do kuželu, dokonce i trochu do stran a dozadu
- infračervené senzory
	- krátký dosah
	- svítí tam infra LED
	- odraz se detekuje pomocí fotorezistoru
	- PSD (infrared position sensitive detector) – měří vzdálenost až v jednotkách metrů, problém s osvětlením (horší měření venku apod.)
- laser & lidar
	- 1D, 2D, 3D
	- až 20 km
	- dnes se používají i solid-state lidary, mají víc jednotek, takže není potřeba, aby se lidar otáčel
- MEMS – micro-electromechanical systems
	- používají mikroskopické jevy
	- akcelerometry
	- gyroskopy
	- senzory tlaku
	- displeje, pumpy, motory
- odometrie
	- měření ujeté vzdálenosti
	- možnosti
		- pomocí otáček kol – ale kola můžou prokluzovat
		- pomocí otáček motoru – pozor na převodovku a na chvíle, kdy motor zabírá, ale kola se neotáčí
		- pozorováním prostředí
	- počítání
		- mechanické
		- jazýčkový spínač (reed switch)
		- induktivní a kapacitní (detekce magnetickým polem)
		- resolver, synchro (vinutí kolem motoru – generuje proud)
		- optický snímač (třeba u počítačových myší)
		- Hallův jev
		- Dopplerův jev (frekvenční posun)
		- snímání povrchu
	- enkodéry
		- relativní – říkají nám změnu měření od předchozího stavu, neříkají nám úhel
			- rate – senzor sleduje změnu mezi dvěma hodnotami (sleduje černobílý terč), frekvence změn indikuje rychlost, počet změn indikuje úhel rotace; nelze zjistit směr rotace
			- quadrature – dva senzory, snímají i směr, více možností
				- dvě stopy posunuté o půl kroku, senzory vedle sebe
				- jedna stopa, senzory posunuté o půl kroku
		- absolutní
			- binární – více senzorů v různých stopách, každý úhel odpovídá jinému binárnímu číslu, problém nastává v situaci, kdy mám nepřesné senzory
			- Grayův kód – v každém kroku se mění jeden bit
				- lze snadno sestavit (vezmu nulu, přidám sekvenci, vezmu jedničku, přidám sekvenci pozpátku)
				- je potřeba aspoň 9 stop pro 1° přesnost
			- single-track Gray code
				- černobílé proužky na terči nejsou stejně široké, ale jsou poskládané tak, aby při vhodném rozmístění senzorů na kružnici (nikoliv na poloměru) dávaly Grayův kód
				- N. B. Spedding ukázal pětisenzorový jednostopý kód
				- Hiltgen a Paterson ukázali 9senzorový kód (pro 360 pozic)
	- reálné enkodéry
		- na staré počítačové myši – ozubené kolečko přerušuje optický signál
		- Austria Microsystems AS5035 – magnetický, ale používá quadrature výstup
		- twist & push rotační enkodér – kovové ozubené kolečko, tři kontakty se ho dotýkají, jeden trvale, další dva vzájemně posunuté → kvadraturní signál
	- Hallův jev
		- proud protéká polovodičem, když je to v magnetickém poli, tak se proud vychyluje
		- používá se v ABS v autě
	- Dopplerův jev
		- pohybující se vysílač a přijímač, měří se fázový posun odraženého signálu
		- je jednodušší měřit rázovou frekvenci

### Regulace a řízení

- v ideálním světě se motor otáčí podle zadané rychlosti
	- tzv. open loop systém – kontroler zadá motoru rychlost, ten se otáčí (a tam to končí)
		- regulátor (controller) → aktuátor → proces
- u reálného motoru do hry vstupuje spousta jevů – je potřeba tomu přizpůsobovat vstup
	- problémy: mechanické ztráty, nelineární chování, vlivy prostředí…
	- např. servo je lineární jen v určitém frekvenčním rozsahu
- typicky použijeme nějakou zpětnou vazbu a podle toho budeme měnit vstup
	- closed loop systém – senzor snímá stav procesu a podle toho ovlivňuje řízení
		- regulátor → aktuátor → proces → senzor → regulátor → …
- možné řešení problému s nelinearitou serva – triviálně bez feedbacku
	- experimentálně zjistím, jaká je skutečná maximální hodnota (v lineárním rozsahu), pak to natvrdo zapíšu do kódu
- řešení s feedbackem
	- řízení motoru nastavím na rozdíl mezi reálnou a požadovanou hodnotou (rozdíl = chyba)
	- ten rozdíl násobím ještě nějakou ladicí konstantou
	- dostáváme proporční regulátor (P)
- druhý pokus
	- budu upravovat řízení podle chyby (rozdílu mezi reálnou a požadovanou hodnotou)
	- = integral controller
	- nevýhody
		- oscilace
		- pomalý nájezd
		- přestřelení
	- chtěl bych nepřestřelit
		- čím víc se blížíme k cílové hodnotě, tím víc snižujeme přidávání výkonu
		- budu derivovat
		- PD regulátor (proportional + derivative controller)
- třetí pokus
	- budu přímo počítat řízení
	- ladicí konstanta bude jiná u minulých chyb než u aktuální chyby
	- proportional + integral controller
- PID controller
	- e = req_speed - cur_speed
	- sum_e = += e
	- control = P\*e + I\*sum_e - D\*(cur_speed - last_speed)
	- parametry P, I, D jsou platné pro jeden typ procesu
	- P – základní zpětnovazebné řízení
	- I – zajišťuje nenulový výstup pro nulovou chybu
	- D – zabraňuje přestřelení
	- vliv parametrů
		- P – nastavuje citlivost na chybu
		- I – zrychluje dosáhnutí setpointu (tedy aby vstup odpovídal realitě)
		- D – zpomaluje a tlumí
- ladění parametrů
	- manuálně
	- ze zkušenosti
	- pomocí magie
	- pomocí vědy
		- Ziegler-Nichols
		- Cohen-Coon
		- Tyreus-Luyben
		- Chien-Hrones-Reswick Autotuning
	- výsledky vědeckého bádání se hodí použít – pak to obykle stačí jen trochu doladit
- rychlé manuální ladění
	- I=0, D=0
	- zvyšuju P, dokud to nezačne oscilovat
	- nastavím P na polovinu
	- ↑ tohle obvykle stačí, pokud ne, tak začnu ladit další složky
		- obvykle se ladí I
		- D se používá pro tlumení nebo vyhlazení šumu
	- zvyšuju I, dokud se mi nelíbí doba trvání procesu (abych ale nenarušil stabilitu)
	- u hlučného procesu zvyšuju D (aby ale odpověď byla pořád dost rychlá)
- pozorování: když to má být rychlé, tak to obvykle přestřelí (může být potřeba snížit I a P)
- Ziegler-Nichols
	- velkou roli hraje čas mezi změnou a zaznamenáním změny (= „perioda“?)
	- je potřeba najít Pc a Tc
		- Pc … kritické P, kdy to začíná oscilovat s nulovými I, D
		- Tc … perioda
- pozorování: je lepší používat jednodušší přístup – někdy stačí P, PI nebo PD
- implementační problémy
	- nedokonalé informace (měření, rozlišení enkodéru, filtrování dat)
	- rozsah proměnných
	- aritmetika (když bude akumulovaná chyba moc velká, tak může být problém s přičítáním/odčítáním)
- u boebotů nedává smysl měnit rychlost motorů vícekrát než 20× za sekundu
- implementace v reálném světě
	- mechanická – páčka, pružina, hmotnost
	- elektrická (analogová) – zesilovač, kondendzátor, odpor
	- digitální – výpočet v mikrokontrolerech FPGA, PLC, …

## 4. Software a algoritmy řízení robotů

### Implementace řídicích systémů

- v přírodě
	- zaměřeny na přežití – diverzita, nepředvídatelnost, nestabilita
	- lokálně omezené – omezené vnímání i znalost
	- omezeny na konkrétní situaci v konkrétním čase
- starší průmyslová robotika – roboti se nepřizpůsobují okolním podmínkám (takže to vlastně nebyli roboti, ale spíše mechanická zařízení)
- robot control = sensing (načtení informací z okolí) → processing (zpracování informací) → executing (vykonání reakcí na podněty)
- konečný stavový automat (finite state machine)
	- chybí tam výstup – chování robota
- implementace FSM
	- definuju stavy jako výčtový typ
	- nastavím počáteční stav
	- implementuju přechod mezi stavy (třeba pomocí switche)
	- pozor na časování
- složitější implementace – pomocí tabulky stavů a vychodnocovacích funkcí
- Petriho síť
	- orientovaný bipartitní graf
	- vrcholy … přechody a místa
	- graf je vhodný na znázornění nezávislých událostí a synchronizace
- Grafcet
	- GRAphe Fonctionnel de Commande Etapes/Transitions
	- založen na binárních Petriho sítích
	- je vhodný pro asynchronní paralelní spouštění
- Sequential Function Chart
- Node-RED
	- low-code programování pro událostmi řízené aplikace
- implementace na střední úrovni – middleware
	- propojuje moduly na nízké úrovni, které ovládají hardware, s high level algoritmy a rozhodovacími procesy
	- např. ROS (potřebuje operační systém, na kterém by mohl běžet; poskytuje spoustu užitečných nástrojů a balíčků)
- implementace průmyslového řízení – podle technických norem
- architektury vyšší úrovně řízení
	- deliberative control
		- nejdřív se posbírají všechny indicie
		- rozhodne se, co se má dělat
		- a pak se to vykoná
		- problém – dynamické prostředí
	- SPA architektura
		- sense, plan, act
		- podobné jako předchozí
	- reaktivní řízení
		- nepřemýšlej – konej
		- tenhle princip používáme u boebotů
		- takhle funguje spousta rostlin a živočichů (mají přirozené reflexy)
		- těsný vztah mezi senzory a aktuátory
		- typicky se takové systémy popisují systémem pravidel – když se něco stane, tak něco udělej
		- minimální vnitřní stav
		- v čisté formě nemá reaktivní systém žádnou paměť, nepamatujeme si globální stav
		- pořád se používá
	- subsumption architecture
		- Rodney Brooks, firma iRobot
		- několik úrovní kontroly – vyšší úrovně řeší problémy, které nižší nezvládnou vyřešit
		- vyšší úrovně přepisujou vstupy a výstupy nižších úrovní
	- hybridní řízení
		- mysli a konej
		- reaktivita v reálném čase
		- racionální rozhodování
		- interakce obou komponent
			- reactive – okamžité potřeby
			- deliberative – dlouhodobé potřeby
		- můžou být v konfliktu – používá se třetí úroveň, která to koordinuje
		- tři úrovně – plánovací (jak splnit misi), sekvenční (jak vykonat plán), reaktivní (vyhýbání překážkám)
	- behaviour control
		- mysli tak, jak se chováš
		- sada distribuovaných a interagujících modulů
		- je to sada jednotlivých „chování“ (behaviours)
		- behaviours ovlivňují chování robota
		- decentralizované řízení
		- jako behaviours se dají použít i neuronové sítě apod.
		- adaptabilní způsob řízení
- použití
	- reaktivní – v prostředích, které vyžadují okamžitou odpověď, rychle se mění
	- deliberative – v optimalizačně hladových úkolách, v doménách založených na strategii, při hledání a plánování
	- hybridní – vnitřní model je potřeba, ale nejsou vysoké realtime nároky, realtime odpověď je nezávislá na vysoceúrovňovém plánování
	- behaviour-based – významné dynamické změny, rychlá odpověď a přizpůsobitelnost je nezbytná + schopnost vyvarovat se chybám, které robot učinil dříve, a plánování dopředu

### Reprezentace prostředí

- dělení podle způsobu vytvoření mapy
	- manuální – trvá to dlouho, není přesná
	- (částečně) automatické
- podle času vytvoření – offline (předem), online (v průběhu činnosti)
- fixní/adaptivní mapa
- metrické/topologické mapy – topologické reprezentují svět jako objekty a vztahy mezi nimi
- podle úrovně abstrakce – senzorická (popis objektů podle senzorů), geometrická (popis objektů podle jejich rozměrů, hmotností apod.), topologická (objekty a jejich atributy), symbolická („tohle je židle“)
- metrické mapy mají referenční souřadnicový systém
	- objekt je charakterizován tím, jaké místo na mapě zabírá
	- příklady: turistické mapy, někdy městské mapy (ale např. všechny ulice jsou zobrazeny stejně široké)
- topologické mapy
	- neuvádějí obvykle informaci o pozici, ale pouze informace o vztazích mezi objekty
- v robotice se často používají oba přístupy, které se kombinují
- bereme v úvahu rozměry robota – nasnímané překážky tedy „rozšíříme“, aby do nich robot nenarazil (pak to může vypadat, že se chová zvláštně)
- při delším pohybu robota někdy vznikají v mapách chyby – řeší se to „uzavřením“ mapy (loop closure), které vychází z toho, že zdi na sebe navazují
- senzorická mapa
	- spojení vstupů ze senzorů
	- typickým příkladem je occupancy grid
		- pravidelná nebo nepravidelná
		- zachycuje volný prostor, překážky a neznámý prostor
	- obvykle jen částečná, ne globální
- geometrická mapa
	- objekty se skládají z geometrických primitiv (křivek, přímek, hranolů, válců, koulí)
	- problém – automatické vytvoření geometrické mapy
- topologická mapa
	- zobecněná geometrická mapa do obecného grafu
	- typické příklady
		- vrcholy … objekty, hrany … vztahy mezi nimi
		- vrcholy … objekty a vztahy mezi nimi, hrany … přiřazení objektů a vztahů
- symbolická mapa
	- pro přímou komunikaci člověk – robot
- occupancy grid / mřížka obsazenosti
	- přímý přístup
		- měření ze senzorů
		- těžké na vytváření a údržbu
	- pravděpodobnostní přístup
		-  vede na bayesovské metody
	- plausibility approach (věrohodnostní přístup)
		- zachycuje více různých možností – různé úrovně jistoty
	- fuzzy přístup
		- s daty se špatně pracuje
		- „je hotel blízko pláže?“ – co je to blízko?
	- neuronové sítě, genetické algoritmy
		- problém s trénováním a neočekávanými událostmi
- roboto-centrická senzorika
	- senzory se hýbou s robotem
	- musíme data přepočítávat

### Lokalizace

- cíle lokalizace
	- abychom zjistili robotovu pozici a orientaci
		- vzhledem k mapě
		- v daném prostředí
	- někdy chceme získat pozici a orientaci jednotlivých částí robota
	- pozice + orientace = „póza robota“
- problém transformace souřadnic mezi globálním a lokálním systémem
- dělení lokalizace
	- absolutní (globální) / relativní (lokální) – relativní se typicky vztahuje k nějaké poloze v minulosti
	- pasivní / aktivní – při aktivním přístupu se při lokalizaci můžu pohybovat (např. jsem v dlouhé chodbě, nevím, ve které, tak zkusím popojet)
	- ve statickém / dynamickém prostředí
- absolutní lokalizace
	- nebere v úvahu předchozí pozici
	- obvykle technicky nebo výpočetně složitější
	- řeší situaci, kdy nemáme informaci o předchozí pozici
		- wake-up problem (robota jsme zapnuli)
		- kidnap problem (poloha robota se změnila, ale robot to neví)
	- používáme vlastnosti prostředí – landmarks (aktivní vs. pasivní)
		- aktivní – vysílají informaci, ze které lze něco zjistit
	- GPS (Navstar), Glonass, Compass (BeiDou), Galileo
- relativní lokalizace
	- měříme změnu od minule
	- problém – akumulace chyby
	- používá se odometrie a inerciální navigace
	- dead reckoning – tradiční námořní navigační postupy (směr + rychlost + čas)
	- odometrie – měření rotací kol
- pasivní lokalizace – nemůžu ovlivňovat řízení robota
- aktivní lokalizace – když je to potřeba, řízení robota může být ovlivněno
- lokalizace ve statickém prostřední – robot je jediný objekt, který se hýbe
- lokalizace v dynamickém prostřední – mění se podmínky (osvětlení, umístění objektů, podoba prostředí)
- typicky se setkáváme s problémy při reálné lokalizaci
- řešení reálných problémů s lokalizací
	- přesnější měření – „model based“, nejistotu eliminuju
		- nějakou náhodu použiju – ale pouze jako techniku řešení příliš těžkých problémů při plánování (třeba k výběru vhodné trajektorie)
	- nespoléhám se na to, že znám přesnou pozici robota – pravděpodobnostní lokalizace
		- pozice robota je náhodná proměnná
		- i data ze senzorů jsou náhodné proměnné
		- používají se principy teorie pravděpodobnosti
		- Markovovský řetězec – historie pohybu neovlivňuje budoucnost pohybu
		- odhad pózy robota je funkce $\text{Bel}:l\to\set{0,1}$
			- kde $\text{Bel}$ … belief, $l$ … pozice
		- nesnažíme se odstranit nejistotu
		- hodnoty z minulých měření kombinujeme s aktuálním měřením
		- reprezentace odhadů
			- nepotřebujeme spojitost, takže máme jistou granularitu → diskrétní reprezentace
				- pravděpodobnostní mřížka – rozdělení prostoru na stejně velké buňky
				- topologický graf – vrcholy = možné pozice, hrany = možné přechody
					- $\text{Bel}(l)$ odpovídá pravděpodobnosti, že je robot ve vrcholu $l$
				- Monte Carlo lokalizace
					- sledujeme množinu bodů, které mají nějakou pravděpodobnost (váhy)
					- součet vah = 1
					- algoritmus
						- predikční krok – pohnu se všemi vzorky (pokud vím, že robotovi prokluzují kolečka, tak pohnu každým vzorkem trochu jinak)
						- korekční krok – změním váhu vzorků na základě měření
						- převzorkování – upravím množinu vzorků tak, že losuju ze vzorků, přičemž vyšší váha odpovídá vyšší pravděpodobnosti vybrání (ostatní zahodím); taky bývá vhodné nějaké vzorky přidávat nebo někdy dává smysl všechny vzorky zahodit a začít znova
					- nejlepších výsledků se dosahuje se senzory, které nejsou moc nepřesné, ale ani moc přesné
					- MCL (Monte Carlo lokalizace) může kombinovat informace z více senzorů
					- pozorování
						- MCL je imunní vůči chybám v odometrii
						- MCL je imunní vůči nepřesnosti GPS
			- reprezentace odhadů ve spojitém prostoru
				- bylo by těžké získat obecnou reprezentaci
				- Kalmanův filtr
					- odhad založen na Gaussově křivce
					- nemožné sledovat více hypotéz
					- příliš striktní předpoklady – měření musejí mít normální rozdělení
	- další metody lokalizace – fuzzy logika, intervalová algebra, holistická lokalizace a navigace
	- žádná lokalizace
		- předprogramované automaty
		- reaktivní systémy
		- evoluční algoritmy
- SLAM – simultánní lokalizace a mapování
- když známe vzdálenosti od landmarků
	- vzdálenost od dvou landmarků nám dává dvě symetrická řešení, jedno z nich typicky můžeme zahodit, protože nedává smysl
- když známe úhly k landmarkům
	- dva landmarky nám dají jeden (obvodový) úhel → máme kružnici (pokud známe pozici landmarků na mapě)
	- když máme třetí landmark, máme tři úhly (tři trojúhelníky) a dostaneme bod

### Plánování, navigace

- zadání: najdi cestu ze startu do cíle nebo řekni, že cesta neexistuje
- bereme v úvahu, jestli je cesta vůbec proveditelná, vyhýbáme se překážkám na cestě
- zajímá nás složitost algoritmu, případně jestli najde optimální cestu
- zajímá nás úplnost algoritmu
- algoritmy
	- grafové
	- mřížkové / metody s potenciálovým polem
- algoritmus nezáleží na typu mapy – lze přecházet mezi typy algoritmů
- dělení algoritmů podle nalezeného řešení
	- přesné (exaktní)
	- aproximace
	- pravděpodobnostní řešení
- bug algoritmy
	- žádný globální model
		- žádná mapa ani známé překážky
		- nevíme, jestli se dá vůbec dostat do cíle
	- známe pozici cíle vzhledem k pozici startu
	- máme senzory (omezené)
	- předpoklady
		- 2D statické prostředí
		- konečné parametry (tyhle všechny věci musí být konečné, aby byl algoritmus úplný)
			- lokální počet překážek
			- obvod překážky
			- tloušťka překážky
			- počet překážek, které protíná přímka
		- překážky se nedotýkají, jinak je můžeme sloučit do jedné překážky
	- Bug0
		- běž k cíli, dokud nenarazíš na překážku
		- pokud narazíš na překážku, obcházej ji, dokud nemůžeš jít zase rovně k cíli
			- je jedno, jestli budeme všechny překážky obcházet zleva nebo se budeme rozhodovat náhodně
		- robot nemá paměť, překážka ve tvaru C ho zacyklí
	- Bug1
		- řešením by bylo obcházet překážku tak dlouho, dokud nebudu blíž cíli než v místě, kde jsem do ní narazil
		- tady už potřebujeme paměť
		- hledáme místo na obvodu překážky, které je nejblíž k cíli (?)
		- je Bug1 úplný?
			- lemma 1-1: brouk se nevrací k překážce, kterou opustil
			- důkaz
				- $H_i$ … hit point, $L_i$ … leave point
				- brouk se pohybuje od startu přes H1, L1, H2, L2, …, Hn, Ln do cíle
				- pokud se díváme na vzdálenosti brouka od cíle v hitpointech a leavepointech, tak se postupně zmenšují
			- lemma 1-2: brouk potká konečný počet překážek
			- důkaz: v kruhu se středem v cíli a s poloměrem odpovídajícím vzdálenosti startu a cíle je konečný počet překážek, cesty mezi Li a Hi jsou uvnitř kruhu
	- Bug2
		- máme úsečku ze startu do cíle
		- obcházíme tak dlouho, dokud tu úsečku nepotkáme znova
		- pokud se obcházením dostaneme na místo, kde už jsme byli, na dané křižovatce se příště musíme rozhodnout jinak
	- Bug2 je hladový
	- area of sight improvement
		- brouk obchází překážky kratší trasou
		- tangent bug
- shrnutí brouků
	- minimální globální informace
	- jednoduchá strategie – pohybuj se směrem k cíli, pohybuj se kolem překážky
	- Bug0 neúplný
	- Bug1 úplný, bezpečný, spolehlivý
	- Bug2 úplný, někdy lepší a někdy horší než Bug1
	- tangent bug úplný
- nejkratší cesta
	- Dijkstra
	- A* – Dijkstra s heuristikou
	- D* – řeší přeplánování, když najde překážku na trase
	- náhodné stromy – randomizovaný průzkum oblasti, iterativní vylepšování modelu, rychle najde nějaké řešení, může brát v úvahu neholonomii
	- potential field planning
		- pustíme vodu z robota
		- cíl je prohlubeň
		- překážky jsou vyvýšené
- další úloha – bez překážek, obejít dané body
- používají se spliny, hermitovské křivky

### Multirobotické systémy

- motivace
	- úkol je příliš komplexní pro jednoho robota
	- úkol je distribuovaný
	- několik specializovaných robotů se vyrábí snáz než jeden silný
	- paralelismus umožňuje rychlejší splnění úkolu
	- lepší robustnost skrz redundanci
- aplikace
	- sklady
	- modelování chování v reálném světě
	- virtuální roje
- centralizovaná architektura
	- jeden point-of-failure
	- velká komunikační zátěž
- hierarchie
	- rozděl a panuj
	- dobré škálování
	- problémy při selhání na vysoké úrovni
- decentralizovaná kontrola
	- roboti se rozhodují podle svých lokálních znalostí
	- problém při změně cílů/plánů
- hybridní řízení
	- lokální řízení společně s multirobotnímm řízením
- příklady
	- The Nerd Herd – roj 20 robotů
	- SwarmBots

### Satelitní lokalizace

- základní myšlenka
	- měření vzdálenosti od dvou satelitů → kružnice
	- přidání třetího satelitu → dva body
- jednoduchá myšlenka – time of flight + trilaterace (určení polohy podle vzdáleností)
- historie
	- Wernher von Braun
	- Sputnik
	- USA
		- Transit – námořnictvo, 5/7 satelitů, problémy s časem a pomalou lokalizací
		- Timation – námořnictvo, 27 satelitů, přesné hodiny, problémy s rušením
		- 621B – letectvo, konečně 3D lokalizace, pseudorandom noise kvůli odolnosti rušení, vyžadoval nepřetržité spojení se zemí
		- kooperace několik laboratoří → vznik Navstar GPS
- Navstar GPS
	- původně pouze armádní
	- záměrné snížení přesnosti na 100 metrů (pomocí Select Availability)
		- vypnuto po sestřelení civilního letadla Sovětským svazem kvůli chybě v navigaci
	- v květnu 2000 použití GPS pro civilní účely zpřesněno na 5–10 metrů
	- kódový multiplex (CDMA)
	- konstelace
		- 6 orbitů po čtyřech slotech
		- původně 24 slotů, nyní 27
		- aspoň 4 satelity v každém orbitu
			- aspoň 4 viditelné na každém místě na Zemi
	- diferenciální GPS – umožňuje zpřesnění naměřených hodnot z GPS pomocí známých souřadnic pozemních stanic
- další globální systémy
	- CNSS / Compass / Beidou II (Čína)
	- Galileo (Evropa)
	- Glonass (Rusko)
- doplňkové – EGNOS, GAGAN, MSAS, WASS
- regionální – Beidou (Čína), DORIS (Francie), IRNSS (Indie), QZSS (Japonsko)
- lokalizace uvnitř (indoor) – pomocí Wi-Fi nebo Bluetooth
