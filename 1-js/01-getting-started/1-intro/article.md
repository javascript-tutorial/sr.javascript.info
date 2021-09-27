# Uvod u JavaScript

Hajde da vidimo šta je toliko posebno kod Javascript-a, šta možemo da postignemo sa njim, i koliko se druge tehnologije uklapaju sa njim.

## Šta je JavaScript?

*JavaScript* je prvobitno napravljen da bi "oživeo web stranice".

Kodovi u ovom jeziku se nazivaju *skripte*. One mogu biti upisane direktno u stranici HTML i pokrenute automatski nakon što se stranica učita. 

Skripte su obezbeđene i izvršene kao običan tekst. Nije im potrebna posebna priprema ili kompilacija za pokretanje.

U ovom pogledu, JavaScript se vrlo razlikuje od programskog jezika [Java](https://en.wikipedia.org/wiki/Java_(programming_language)).

```smart header="Why is it called <u>Java</u>Script?"
Kada je JavaScript stvoren, u početku je imao drugo ime: "LiveScript". Ali Java je bila veoma popularna u to vreme, pa je došlo do odluke da bi postavljanje LiveScript-a  na poziciju "mlađeg brata" Jave dosta pomoglo u napretku novog jezika.

Ali kako je napredovao, JavaScript je postao potpuno nezavisan jezik sa svim svojim specifikacijama zvanim [ECMAScript](http://en.wikipedia.org/wiki/ECMAScript), i sada nema nikakve povezanosti sa Javom.
```

Danas, JavaScript se ne pokreće samo u browseru, već i na serveru, ili zapravo na bilo kojoj napravi koja ima specijalan program [the JavaScript engine](https://en.wikipedia.org/wiki/JavaScript_engine).

Pregledač ima ugrađen engine ponekad nazvan "JavaScript virtual machine".

Različite mašine(engines) imaju različita "imena kodova". Na primer:

<<<<<<< HEAD
- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)) -- u Chromu i Operi.
- [SpiderMonkey](https://en.wikipedia.org/wiki/SpiderMonkey) -- u Firefox-u.
- ...Postoje druga imena kodova kao  "Chakra" za Internet Explorer, "ChakraCore" za Microsoft Edge, "Nitro" i "SquirrelFish" za Safari, i td.
=======
- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)) -- in Chrome and Opera.
- [SpiderMonkey](https://en.wikipedia.org/wiki/SpiderMonkey) -- in Firefox.
- ...There are other codenames like "Chakra" for IE, "JavaScriptCore", "Nitro" and "SquirrelFish" for Safari, etc.

The terms above are good to remember because they are used in developer articles on the internet. We'll use them too. For instance, if "a feature X is supported by V8", then it probably works in Chrome and Opera.
>>>>>>> b09e38c5573346c401a9f9f7410b4ff9be5f4115

Dobro je zapamtiti termine iznad zato što se koriste u programerskim člancima na internetu. Mi ćemo ih koristiti takođe. Na primer, ako je "funkcija X podržano od V8", onda verovatno funkcioniše u Chrome-u i Opera-i. 
```smart header="How do engines work?"

Engine(mašine) su komplikovane. Ali osnove su im lake.

1. Engine (embedded ako je pretraživač) čita ("parsira") skriptu.
2. Onda prebacuje ("kompajlira") skriptu u jezik mašine.
3. I onda kod radi, prilično brzo.

Engine omogućava optimizacije na svakom koraku u procesu. Čak posmatra kompajlovanu skriptu dok se izvršava, analizira podatke koji protiču kroz nju, i optimizira dalje kodove mašina zasnovane na tom znanju.
```


## Šta in-browser JavaScript može da radi?

Moderan JavaScript je "siguran" programski jezik. Ne dozvoljava pristupe niskog nivoa memoriji ili CPU-u, zato što je prvenstveno napravljen za pretraživače koji to ne zahtevaju.

JavaScript mogućnosti dosta zavise od njegovog okruženja. Na primer, [Node.js](https://wikipedia.org/wiki/Node.js) podržava funkcije koje dozvoljavaju JavaScript-u da čita/piše proizvoljne fajlove, pokreće mrežne zahteve, i td.

In-browser JavaScript može sve što je povezano sa manipulacijom vebstranice, interakcijom sa korisnikom i sa vebserverom.

Na primer, in-browser JavaScript može da:

- Dodaje novi HTML na stranicu, izmeni postojeći sadržaj, izmeni stilove.
- Reaguje na akcije korisnika, pokreće se na klik miša, pokrete kursora, pritisak dugmeta.
- Šalje zahteve putem mreža da bi upravljao serverima, daunlouduje i aplouduje fajlove (takozvani [AJAX](https://en.wikipedia.org/wiki/Ajax_(programming)) i [COMET](https://en.wikipedia.org/wiki/Comet_(programming)) tehnologije).
- Dobija i postavlja kukije, postavlja pitanja posetiocu, pokazuje poruke.
- Pamti informacije sa strane klijenta("local storage").

## Šta in-browser JavaScript ne može da radi?

JavaScript-ove mogućnosti u pretraživaču su ograničene zbog sigurnosti korisnika. Cilj je da se spreči da zla stranica pristupi privatnim podacima ili da nanese štetu korisnikovim podacima.

Primeri takvih restrikcija uključuju:

- JavaScript na vebstranici ne sme da čita/piše proizvoljne datoteke na hard disku,ne sme da ih kopira ili pokreće program. Nema direktan pristup OS funkcijama.

    Moderni pretraživači dozvoljavaju da radi sa datotekama, ali je pristup ograničen i samo omogućen ako korisnik radi određene akcije, na primer "spušta" fajl u prozor pretraživača ili ga selektuje putem `<input>` taga.

    Postoje načini za interakciju sa kamerom/mikrofonom, i ostalim uređajima, ali zahtevaju posebnu dozvolu korisnika. Tako da stranica na kojoj je omogućen JavaScript ne sme tajno da uključi Vebkameru, posmatra okolinu i šalje informacije na [NSA](https://en.wikipedia.org/wiki/National_Security_Agency).
- Različiti tabovi/prozori inače ne znaju jedni za druge. Ponekad znaju, na primer kada jedan prozor koristi JavaScript da bi otvorio drugi. Ali čak i u ovom slučaju, JavaScript sa jedne stranice nema pristup drugoj stranici ako dolaze sa različitih sajtova (sa različitog domejna, protokola ili porta).  

   Ovo se zove "Same Origin Policy" (politika istog porekla). Za rad sa njom, *obe stranice* moraju da pristanu na razmenu podataka, i da sadrže poseban JavaScript kod koji podržava tu politiku. Mi ćemo pokriti to u ovom tutorijalu. 
   
   Ovo ograničenje je, ponovo ponavljamo, zbog sigurnosti korisnika. Stranica sa `http://anysite.com` koju je korisnik otvorio ne sme da ima pristup drugom pretraživaču sa ovim URL-om  `http://gmail.com` i da ukrade informacije odatle. 
- JavaScript može lako da komunicira preko interneta do servera odakle trenutno stranica dolazi. Ali njegova mugućnost da prima podatke sa drugih sajtova/domejnova je oštećena. Ako je moguće, zahtevaće posebno odobrenje (izraženo u HTTP zaglavljima) Još jednom, to je sigurnosno ograničenje. 
![](limitations.svg)

takva ograničenja ne postoje ako je JavaScript korišćen van pretraživača, na pr. na sreveru. Moderni pretraživči takodje dozvoljavaju plagin ekstenzije koji služe za izdavanje dozvole.

## Šta čini JavaScript jedinstvenim?

Postoje najmanje tri bitne stvari o JavaScriptu: 
```compare
+ Potpuna integracija sa HTML/CSS.
+ Jednostavne stvari koje se prosto izvršavaju.
+ Podrška od svih većih pretraživača i dozvola po default-u.
```
JavaScript je jedina brauzer tehnologija koja kombinuje ove tri stavke. 

To je ono što čini JavaScript jedinstvenim. Zato je on najrasprostranjenija alatka za stvaranje pretraživačkog interfejsa. 

Ovim rečeno, JavaScript omogućuje kreiranje servera, mobilnih aplikacija, i td. 

## Jezici "preko" JavaScript-a

JavaScript sintaksa ne ispunjava svačije potrebe. Različiti ljudi zahtevaju različite stvari. 

To je očekivano, zato što projekti i zahtevi tih projekata su drugačiji za sve.

Zato se skoro mnoštvo drugih jezika pojavilo, koji su konvertovani u JavaScript pre nego što se pokrenu u pretraživaču.

Moderne alatke stvaraju konvertovanje veoma brzim i lakim, zapravo dozvoljavaju programerima da kreiraju kod u drugom jeziku auto-konvertujući njegovu suštinu.

Primeri takvih jezika:

- [CoffeeScript](http://coffeescript.org/) je "sintetički šećer" za JavaScript. Upoznaje nas sa kraćom sintaksom, dozvoljavajući nam da pišemo čistije i preciznije kodove. Inače *Rubi* developeri ga vole.
- [TypeScript](http://www.typescriptlang.org/) je koncentrisan na dodavanje "strogog pisanje podataka" da bi pojednostavilo razvijanje i podršku kompleksnih sistema. Razvijen je od strane Microsoft-a.
- [Flow](http://flow.org/) takođe dodaje pisanje podataka, ali na drugi način. Razvijen od Fejsbuk-a.
- [Dart](https://www.dartlang.org/) je samostalan jezik koja ima svoju mašinu koja radi u non-brauzer okruženjima(kao što su mobilne aplikacije), ali takođe može biti konvertovan u JavaScript. Razvijen od Google-a.
- [Brython](https://brython.info/) je Python konvertovan u JavaScript koji omogućava pisanje aplikacija na čistom Python jeziku bez JavaScript-a.
- [Kotlin](https://kotlinlang.org/docs/reference/js-overview.html) je moderan, sažet i siguran programski jezik koji cilja na pretraživač ili Node. 

Ima ih više. Naravno, čak iako smo se navikli na neki od konvertovanih jezika, trebali bismo da poznajemo JavaScript da bismo stvarno razumeli šta činimo.

## Rezime

- JavaScript je prvobitno stvoren kao jezik samo za pretraživače, ali se sada koristi i u mnogim drugim okruženjima.
- Danas, JavaScript ima jedinstvenu poziciju kao najprihvaćeniji pretraživački jezik potpuno integrisan u HTML/CSS.
- Postoje mnogi jezici koji su "pretočeni" u JavaScript i daju razne mogućnosti. Preporučujemo da ih istražite, barem nakon usavršavanja JavaScript-a.
