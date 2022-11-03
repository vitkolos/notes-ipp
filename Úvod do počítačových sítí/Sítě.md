# Úvod do počítačových sítí: síťová část

Libor Forst, SISAL MFF UK
<https://www.ksi.mff.cuni.cz/teaching/nswi141-web/pages/>

- po splnění úkolu můžeme přijít na zkoušku (ale přihlásit se můžeme dopředu)
- domácí úkol se odevzdává do ReCodExu, potřebujeme dva body
- u zkoušky budeme mít vygenerovaný test (40 uzavřených otázek, jedna správná odpověď)
- literatura není potřeba
- <https://www.warriorsofthe.net>

---

- obecné atributy komunikace
- porovnání komunikací
- přenos zprávy

- souhrn 1
	- ...
	- jak se projevilo to, že vznik sítí iniciovala armáda?
		- nijak, data proudí nezabezpečeně
	- jaká je definice LAN?
		- žádná; lokální sítě LAN bývají většinou privátní
	- VPN – geografické rozšíření privátní sítě
- adresování počítačů
	- na fyzické vrstvě se nepoužívají adresy
	- na linkové vrstvě se používají fyzické, MAC adresy
- adresování služeb
	- v URI není protokol, ale schéma (které je někdy totožné s názvem protokolu)

- souhrn 1
	- o přidělování IP adres rozhoduje správa sítě
	- router zajišťuje směrování požadavků a odpovědí
- kryptografie
	- symetrické šifrování
		- pro zašifrování a dešifrování se používá stejný klíč
		- rychlé, vhodné na velká data
		- neřeší problém přenosu klíče
	- asymetrické šifrování
		- veřejný a tajný klíč
		- netřeba přenášet tajný klíč, veřejný klíč naopak netřeba tajit
		- pomalé algoritmy
		- problém autenticity veřejného klíče – je potřeba ověřit, že daný veřejný klíč opravdu patří danému člověku
	- hashovací funkce
		- vytvoření otisku dat
		- není možné data z hashe zpětně odvodit
		- nalezení dat se shodným hashem je obtížné
		- kryptografické hashovací funkce mají dodatečné bezpečnostní mechanismy
	- šifrování dat v praxi
		- data se šifrují symetricky pomocí náhodného klíče
		- symetrický klíč se šifruje asymetricky
	- elektronický podpis
		- hash dat se zašifruje tajným klíčem odesilatele
		- příjemce hash dešifruje pomocí veřejného klíče odesílatele a porovná ho s vlastnoručně spočítaným hashem
	- Diffie-Hellmanův algoritmus – výměnou informací veřejným kanálem lze získat sdílenou tajnou informaci
	- autenticita veřejných klíčů
		- lze ověřit z více nezávislých zdrojů
		- klíč mi ověří někdo, jehož klíč mám ověřený
		- veřejně uznávaná certifikační autorita
	- certifikát
		- klíč doplněný o identifikaci vlastníka a podepsaný vydavatelem
		- řetěz certifikačních autorit – alespoň nejvýše postavené autoritě bych měl věřit
	- SSL, TLS – mezivrstva mezi transportní a aplikační vrstvou umožňující autentikaci a šifrování
	- aplikační vrstva TCP/IP
		- spojuje funkce OSI 5, 6 a 7 – pravidla komunikace mezi klientem a serverem, stav dialogu, interpretaci dat
		- na aplikační vrstvě definuje formát zpráv, průběh dialogu atd.
	- DNS
		- překlad jmen na adresy a naopak
		- protokol nad UDP (obvykle) i TCP (větší dotazy)
		- nameservery
		- jednotkou dat je záznam – SOA (info o doméně), NS (nameserver), A (IPv4 adresa počítače), AAAA (IPv6 adresa počítače), PTR (doménové jméno počítače), CNAME (kanonické jméno počítače – k aliasu), MX (poštovní server)
	- servery DNS
		- typy – primární (záznamy o doméně), sekundární (kopie dat o doméně), caching-only (jen nevyřešené dotazy)
		- každá doména musí mít alespoň jeden nameserver
		- aktualizaci zónové databáze vyvolává sekundární server, je ale možné z primárního serveru signalizovat její potřebu
	- vyřizování DNS dotazu
		- klient se zeptá lokálního nameserveru, ten se následně ptá několika serverů, každému posílá celou doménu a dostává dílčí odpovědi odkazující na další nameserver (NS) nebo na konkrétní počítač (A)
		- klient pokládá rekurzivní dotaz, lokální nameserver pokládá nerekurzivní dotazy
		- součástí doménového jména může být tečka (nelze sekat domény podle teček)
	- zabezpečení DNS spočívá v tom, že si klient volí náhodný zdrojový port, náhodné ID a že je těžké dostat se ke komunikaci nameserverů
	- možné napadnutí DNS – cache-poisoning (server útočníka se označí za nameserver pro doménu vyššího řádu)
	- zabezpečení DNS = DNSSEC – informace o doménách jsou podepsané
	- diagnostika DNS – nslookup, dig
- e-mail
	- open relay servery umožňují komukoliv odesílat poštu
- souhrn
	- problémy FTP – nešifrovaný přenos, přenos probíhá přes pomocné spojení, aktivní spojení je rizikem
	- MTA vs. MX
- POP vs. IMAP