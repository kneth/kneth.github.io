---
title: "Open Source for Ledere"
date: 1999-04-18T09:56:57+02:00
categories: [essay]
tags: [open source, free software, dansk]
draft: false
---

## Tjen penge på Open Source

### Notes in English

* Co-authors: [Peter Toft](https://www.linkedin.com/in/petertoftdk/) and [Hanne Munkholm](https://www.linkedin.com/in/hanne-munkholm/)
* Published at sslug.dk
* Original license: [http://www.opencontent.org/opl.shtml](https://web.archive.org/web/19991009175004/http://www.opencontent.org/opl.shtml)

### Formål

Vi vil i denne artikel argumentere for at [Open Source](https://web.archive.org/web/19991009175004/http://www.opensource.org/) Software er bedre end det mere traditionelle lukkede software. Det vil blive beskrevet hvorfor Linux-verdenens måde at udvikle software på har store fordele - dels med hensyn til stabilitet og sikkerhed, men også med hensyn til den strategiske risiko, som en moderne erhvervsleder altid må tage, når der købes software.

Artiklen er kraftigt inspireret af Open Source bevægelsen og Eric S. Raymonds artikler og foredrag. Eric S. Raymond er en (nu meget kendt) systemprogrammør fra USA, der har studeret og dokumenteret mange af de stærke ting, som kendetegner udviklingen af det meget udbredte Linux styresystem. 

### Indledning til Open Source

I de første måneder af 1998 opstod et nyt begreb blandt Internet-brugere: Open Source. Eric S. Raymond skrev et par opsigtsvækkende artikler omkring udvikling af software, og netop disse artikler fik Netscape til at åbne dørene til Netscape Communicator. I starten af 1998 fik hele verden adgang til kildeteksten (selve programkoden) til Netscape Communicator, og programmet fik en Open Source kompatibel licens. Det gjorde det muligt at tilføje til eller ændre i programmet, i modsætning til de gængse binære programmer, som ikke kan ændres. Disse vil vi kalde "closed source" programmer i det følgende.

Open Source er i virkeligheden et simpelt begreb, som anvendes på licensbetingelserne til software. I sin enkelhed betyder Open Source at alle mennesker, uanset hudfarve, religion, politisk overbevisning eller geografisk placering, kommerciel eller privat bruger, skal have adgang til kildeteksten til softwaren. Endvidere medfølger retten til at ændre kildeteksten.

Men Open Source er mere end blot adgang til kildeteksten. Ofte følger de programmer, som har en Open Source licens, en række fælles mønstre. Et af mønstrene er, at udviklingssprojekterne ofte bruger Internettet som det vigtigste medium, dvs. at e-post og WWW er vigtige elementer hvor udviklerne kommunikerer. Et andet fælles mønster er den udviklingsmodel, som man benytter i projekterne (ofte uden bevidst at tænke over den).

Flere af de store firmaer anerkender nu Open Source og anvender det som udviklingsmodel: SUN, Silicon Graphics og Netscape.

Der findes en mange tusinde mere eller mindre kendte Open Source projekter.  De allermest kendte er

* **Linux** - Med en vækst på 212% i 1998 og ca. 20 millioner brugere er Linux det styresystem, der virker mest lovende af alle. Linux er i dag det mest anvendte styresystem til web, news og ftp-servere med en markeds andel på 25%-33%
* **Apache** - Webserveren Apache kan downloades gratis fra Internettet og er af en meget høj kvalitet. Netop den høje kvalitet har betydet, at Apache har en markedsandel på omkring 50%.
* **Samba** - [Samba](https://web.archive.org/web/19991009175004/http://www.samba.org/) er blandt mange ting et stykke software, som kan fungere som filserver for et Microsoft Windows 95 netværk. Programmet betyder at en edb-afdeling kan benytte UNIX-baserede servere, imens slutbrugerne bruger Windows og de mange applikationer, som findes til Windows 95. Mange firmaer anvender i dag Samba uden at klienterne aner det.
* **Perl** - Programmeringssproget [Perl](https://web.archive.org/web/19991009175004/http://www.perl.org/) benyttes af rigtig mange mennesker. Omkring 95 % af alle CGI-scripts (interaktive hjemmesider) er skrevet i Perl.
* **Netscape Communicator** - Netscape Communicator var det første store kommercielle produkt der gik over til Open Source. Man regner med at ca. 50 % af alle verdens browsere er fra Netscape.

### Linux Development Model

Udviklingsprojekter som har en grad af Open Source over sig benytter ofte en udviklingsmodel, som hos Eric S. Raymond går under betegnelsen Linux Development Model (LDM).

I et traditionelt udviklingsprojekt arbejder N programmører sammen. Omkostningerne for ethvert projekt måles i mandemåneder, dvs. hvor mange måneder en programmør vil være om at udvikle det ønskede programmel. Hypotesen bag den målestok er, at sættes der dobbelt så mange programmører på projektet, vil det tage den halve tid. Men virkeligheden er en anden! Udviklingsomkostningerne sprænger næsten altid budgetterne.

Det kan let forklares, at det ikke er muligt at sætte udviklingstiden vilkårligt ned ved at ansætte flere programmører. Frederick P. Brooks, jr. giver forklaringen i _The Mythical Man-month_ [Addison-Wesley, 1995]. Når man har N programmører er der N(N-1)/2 snitflader mellem programmørerne. Det vil sige, at hvis man fordobler antallet af programmører, vil antallet af snitflader firdobles. Med andre ord vil produktiviteten ædes op af kommunikation og konflikter mellem programmørerne. Derfor ser man ofte projekter med små hold af programmører, som arbejder med velafgrænsede opgaver og integration mellem delprogrammer.

LDM er anderledes. I Open Source projekter findes der typisk en kerne af programmører (N personer), som leder projektet. Men der findes M personer, f.eks. 10.000 personer, som downloader programmet. Disse personer (beta-testerne) finder fejl og sender typisk rettelserne til den lille kerne af N personer, der leder projektet. Men antallet af snitflader er kun M, idet beta-testerne ikke kommunikerer med hinanden. Eftersom M typisk er mange gange større end N, ser vi at kompleksiteten vokser lineært med antallet af beta-testere, men kompleksiteten for et traditionelt ledet projekt vokser med kvadratet.

For at konkludere uden brug af matematik: LDM har de to store fordele at arbejdet per person udnyttes virkelig godt, og at alle de personer, der arbejder som beta-testere og retter i koden, ikke skal betales af firmaet. I den traditionelle beta-test af programmer uden kildetekst, er belastningen af de betalte programmører, som modtager fejlrapporter stor - for de skal selv genskabe samme fejl, finde fejlen i koden og rette den. Oftest er dette en ineffektiv arbejdsgang. Som software producent opnår man med LDM en mere effektiv arbejdsgang, og et bedre testet og mere stabilt program, hvor det er meget svært at skjule sikkerhedshuller, da alle kan læse med i kildeteksten.

Det er dog ikke altid, at man som software producent kan bruge Open Source konceptet. Laver man f.eks. produkter som alene sælges på grund af en nyudviklet hemmelig metode, så kan producenten ikke bevare den hemmelighed i Open Source programmel, da alle har adgang til kildeteksten. Men de fleste computerbrugere bruger alene software, hvor programmets værdi ret beset skyldes programmets stabilitet - og kun i ringe grad hemmeligheder. Som computerbruger vil man som oftest langt hellere have et stabilt program, man kan stole på - fremfor et par ekstra "features", som får programmet til at gå ned fra tid til anden. Med hensyn til stabilitet, og oftest også ydelse, er Open Source og LDM en overlegen udviklingsmetode.

### Reduktion af omkostninger

I en virksomhed, som ikke lever af at udvikle software, sker der ofte en hel del softwareudvikling alligevel. Mange forbinder software udvikling med færdige software produkter man kan købe, men sandheden er snarere, at mindst 90 % af alle edb-folk arbejder med intern udvikling eller drift. Dette er overraskende, men det betyder at langt de fleste firmaer udvikler software for at bruge den, ikke for at sælge den. Disse firmaer har oftest større fordel af at have stabile og effektive programmer, hvor programmernes kildetekst er offentlig kendt, fremfor at skulle stole på at et "closed source"-firma ikke har fejl i deres program.

Som eksempel vil vi nævne Cisco. Cisco fremstiller diverse netværkskomponenter, f.eks. routere. Eftersom Cisco er en international virksomhed, har virksomheden kontorer rundt om i verdenen. På et tidspunkt ønskede ledelsen, at alle Ciscos ansatte kunne udskrive på en vilkårlig printer et andet sted i verden. Ciscos edb-afdeling påbegyndte projektet, og valgte efter nogen tid at lade projektet være Open Source, så andre virksomheder i dag kan bruge systemet, og bidrage til dets udvikling. Det betyder, at Cisco ikke blev nær så afhængige af den lille gruppe ansatte, der har udviklet systemet. De finder måske et andet job en dag, og var det et lukket system, var der ikke længere nogen, der var kvalificerede til at vedligeholde softwaren. Ved at lave deres printerstyringsprojekt til et Open Source projekt opnåede Cisco risikospredning, men de har også opnået at udviklingsomkostningerne bliver delt imellem flere virksomheder. Da Cisco's forretningsområde ikke er printerstyring, vil de ikke miste markedsandele, hvis deres konkurrenter bruger det samme program. Typisk vil et sådant program, blive anvendt af alle mulige andre virksomheder som strukturmæssigt minder om Cisco, og altså ikke fremstiller det samme som Cisco - og Cisco har reelt fået et system, som ikke koster ret meget, men bidrager til den interne værdi i firmaet.

Open Source Software (OSS) kan typisk fås gratis eller for et symbolsk beløb svarende til en manuals pris, hvilket også betyder en kraftig reduktion af omkostningerne. Skal man installere både Microsoft Windows NT og Microsoft Office på en PC løber det let op i mere end 5.000 kr. Naturligvis koster uddannelsen af medarbejderne det samme for både Open Source og kommercielle produkter. Hardware er typisk billigere, hvis man kun kører Open Source Software, idet Open Source Software typisk er mindre ressourcekrævende. Dette er navnlig sandt, når vi taler om servere. En Linux webserver kan køre fint på en i486 maskine med kun 16 MB RAM.

### Reduktion af risiko

Et oplagt problem med closed source software er, at leverandøren går konkurs eller vælger at stoppe vedligeholdelsen af et produkt. En konkurs vil betyde, at du sidder med et edb-system, som du ikke kan få rettet fejl i eller tilføjet nye funktioner til.

I mange tilfælde vil et stop af vedligeholdelsen af et program være endog meget kritisk for en virksomhed. Et måske noget letkøbt eksempel kunne være et lagerstyringssystem, som ikke er år 2000 klar. Eller blot, at det har et maximalt antal varegrupper, som firmaet nu overskrider. Fatale problemer, som man møder alt for ofte.

Benyttes Open Source Software har du adgang til selve kildesteksten. Derved kan du ansætte en programmør til at gøre dit lagerstyringssystem klar til år 2000. Brugen af Open Source Software er derfor en reduktion af din risiko.

Reduktion af risiko gælder også software udviklet internt i et firma, hvor man selv har kildeteksten. Hvor mange har ikke oplevet at et eller andet ikke længere kunne bruges, fordi "ham der havde forstand på det" er rejst. Software skal vedligeholdes, og det tager tid og kræfter at sætte sig ind i et projekt, selvom man har kildeteksten. Hvis et projekt er Open Source, vil der altid være nogen et eller andet sted, som har forstand på det, og de kan lære hinanden op. Således kommer et godt Open Source projekt aldrig til at samle støv i skuffen. Modsat så vil et dårligt Open Source projekt aldrig få stor støtte og aldrig få luft under vingerne - ligesom et tilsvarende kommercielt produkt nok ville være svært at sælge.

Som bruger af Open Source software har man den sikkerhed, at når først et program er startet som Open Source, så kan man ikke stoppe udviklingen - programmet vil fortsætte som Open Source. Man kan ikke købe sig tilbage til et lukket udviklingsmodel. Som eksempel er Linux kernen copyrightet af mange hundrede folk under en Open Source licens.

### Aktiv IT-strategi

Ikke-softwarefirmaer, der udveksler information med hinanden, har den fælles interesse, at dokumenterne er læsbare, når de når frem. Virksomhederne er som sådan ikke interesserede i anvende det samme program, hvor de måske har forskellige behov. Virksomhederne er blot interesserede i at dokumenter følger en åben standard, så modtageren kan læse det. Dette er modtridende med den kommercielle software producents interesser, som ønsker at alle bruger deres software.

Hvis en virksomhed vælger Open Source Software, vælger virksomheden samtidig sin egen skæbne. Det lyder måske prætentiøst, men i virkeligheden er det meget simpelt. Sagen er, at ved at vælge lukket (kommerciel) software, vælger du ikke din egen IT-strategi. Din IT-strategi bliver kraftigt bundet til din leverandørs forretningsstrategi.

Et velkendt eksempel er da Microsoft kom med Office97 pakken. Mange firmaer havde installeret Word95 til tekstbehandling, men med Word97 blev det almindelige filformat ændret, og dermed kunne man ikke længere i Word95 læse de filer, som Word97 brugere genererede. Resultatet blev, at langt de fleste Office95 installationer blev erstattet af Office97. Hvem blev vinderen af dette? Synes du, som erhvervsleder, at I reelt fik mere, end hvad I havde? For lige at være retfærdig, så frigav Microsoft ganske vist filtre (programændringer af Word95), så man kunne læse Word97 tekstbehandlingsfiler fra Word95, men det blev aldrig rigtig godt.

Et andet grelt eksempel er fra den gang, da IBM og Microsoft indgik et meget integreret samarbejde omkring OS/2. Alle var vilde - de ville bruge OS/2. Danmark var dengang et WordPerfect-land - der blev solgt WP-bøger og kurser. WordPerfect Corp. satsede stærkt på OS/2 og f.eks. banker og mange financielle virksomheder skiftede selv på server-siden. Men hvad skete der? Microsoft skiftede forretningsstategi - på det tidspunkt kom Windows 3.0, og pludselig kunne alle WordPerfect-brugerne se deres erfaring gå tabt: WordPerfect kom ikke lige så hurtigt til Windows systemerne, som Word gjorde.

Et endnu værre eksempel ville være hvis leverandøren enten gik konkurs eller ikke længere ønskede at vedligeholde en bestemt programpakke. Eller at leverandøren ikke ønsker at bibeholde en - for dig - missionskritisk funktion.

Men hvis du har kildeteksten, dvs. benytter Open Source Software, kan du (evt. sammen med andre) fortsætte med at videreudvikle og vedligeholde programmet. Mange virksomheder har ikke resourcer til at rette en fejl i f.eks. Linux, men kan i den situation købe sig til en rettelse af et konsulentfirma. Det vil være kostbart, men endnu mere kostbart, hvis ikke fejlen blev rettet.

Elektronisk Dokument Udveksling (EDI), er et eksempel på en standard hvor åbenhed er en nødvendighed. Skal forskellige økonomisystemer kunne kommunikere med hinanden, må de forskellige producenter have fri adgang til standarderne. For brugerne af økonomisystemerne, har det den yderligere fordel, at de har mulighed for, at skifte til et andet system, når dette bliver nødvendigt for virksomheden.

Nu vil nogen sikkert mene, at deres virksomhed ikke er specielt IT-tung, og derfor er de ikke så sårbare overfor leverandørens luner. Dette er desværre nok ikke rigtigt; alle virksomheder er sårbare overfor deres leverandørers luner - og IT er hurtigt blevet en integreret del af alle moderne virksomheder. Det er vigtigt at huske på, at IT-verdenen er en verden, hvor udviklingen går meget stærkt, og netop derfor kan en leverandør skifte strategi med meget kort varsel.

### Support

Ofte hører man indvendinger om at der ingen support er på Open Source Software. Hvor ringer man hen når systemet ikke virker som det skal?

For nogle år siden var der noget om snakken. Men i dag kan man sagtens betale sig til fuld support på Open Source software. De firmaer, der tilbyder support, ejer ikke softwaren - den er frit tilgængelig for alle. Men de har fuld adgang til kildeteksten, og kan derfor lige så godt løse kundens problemer, som hvis det var et kommercielt produkt de ydede support på. Måske endda bedre og hurtigere - måske er der andre, der allerede har løst problemet. Internettet bugner i dag af support information på Open Source Software. Support-leverandøren skal bare sørge for at løsningen kommer hurtigt ud til kunden. Og det er muligt for support-leverandøren at ansætte folk, som allerede kender til systemet, i stedet for at det tager evigheder at lære nye folk op.

### Penge og Open Source

Selvom størstedelen af dagens software udvikling foregår internt, er der alligevel en del virksomheder, der lever af at udvikle software og sælge det. Disse virksomheder behøver ikke at fortvivle fordi Open Source og gratis software vinder frem. Der er masser af måder at tjene penge på - men producenten skal forstå de ændrede vilkår for at kunne indse disse muligheder og udnytte dem optimalt.

Man kan godt tjene penge på at sælge Open Source software, selvom folk i princippet kunne få det gratis. Hvis man pakker det på en pæn måde, gør det nemt at installere, og laver en manual, er der mange, der vælger at betale for at få disse goder. Man kan yde support på nogle Open Source programmer, og det vil mange virksomheder gerne betale for. Træning og uddannelse i Open Source software er der bestemt mange penge at hente indenfor.

Der er også mulighed for at lave hardware og software kombinationer, hvor softwaren er Open Source og pengene tjenes på hardwaren. Det har en del fordele for producenten. Antallet af personer, som hjælper med softwareudviklingen (og ikke skal lønnes) vil være anseeligt hvis programmet er interessant, og der vi automatisk være mange, som sørger for en yderligere udbredelse af produktet - helt uden reklamekroner i ryggen. Modsat vil det være en vurdering, om man har forretningshemmeligheder i klemme i software-delen. Oftest er det dog stabilitet, som er i højsædet, og her kan fordelene ved Open Source ofte opveje ulemperne.

At afsætte udviklere til at arbejde på et Open Source projekt kan umiddelbart virke som en ren udgift. Men hvis dette danner grundlag for at virksomhedens closed source programmer kan overleve, eller vinde frem, er der pludselig en vis økonomisk fornuft i det. Den grundlæggende software kan være Open Source, tilgængelig for alle og klippestabil. Den mere specialiserede software kan forblive lukket. Netscape frigav deres browser som Open Source for at bevare grundlaget for deres server software.

### Epilog

Vi er af den mening, at jo mere kritisk et program er for din virksomhed, jo vigtigere er, at du selv bestemmer programmets skæbne. Det vil sige, at software, der er kritisk for firmaers drift bør være Open Source Software.

Hvem skal bestemme fremtiden, dig eller din leverandør?

### Relevante links for at læse videre

* Open Source - [http://www.opensource.dk/mirror](https://web.archive.org/web/19991009175004/http://www.opensource.dk/mirror)
* Eric S. Raymond - [http://www.tuxedo.org/~esr](https://web.archive.org/web/19991009175004/http://www.tuxedo.org/~esr/)
* The Cathedral and the Bazaar - [http://www.tuxedo.org/~esr/writings/cathedral-bazaar](https://web.archive.org/web/19991009175004/http://www.tuxedo.org/~esr/writings/cathedral-bazaar)
* Homesteading the Noosphere - [http://www.tuxedo.org/~esr/writings/homesteading](https://web.archive.org/web/19991009175004/http://www.tuxedo.org/~esr/writings/homesteading)
* Open Source artikel på dansk - [http://www.sslug.dk/artikler/OpenSource.html](https://web.archive.org/web/19991009175004/http://www.sslug.dk/artikler/OpenSource.html)

### Vi takker

* 15. marts 1999: Katja Blankensteiner - en større revision af teksten.
* 17. marts 1999: Torben Fjerdingstad - et par gode sproglige rettelser.
* 18. marts 1999: Hans Schou - et par rigtig sunde tilføjelser.
* 23. marts 1999: Hans Chr. Andersen - mere objektiv holdning i teksten.
