# Research platforme Distill Intelligence

| Autor | Nemanja Anđić |
| --- | --- |
| Datum izrade | 24.10.2026 |
| Datum izmjene | 1.11.2026 |
| Verzija | 2.0 |

Mapa cjelina (`docs/mapa-cjelina.md`) kaže **šta** Distill ima. Ovaj dokument objašnjava **kako** to radi: opcije, podešavanja, ograničenja, cijene, API i tragove arhitekture. Iz njega se kasnije pravi tehnička dokumentacija (#10) i analiza arhitekture (#11). Vezani issue: #8.

Verzija 2.0 obuhvata svih deset cjelina u aplikaciji (dio 3) i ispravlja nekoliko ranijih nalaza.

## Kako je rađen research

Distill je posmatran samo spolja, onako kako ga vidi svaki korisnik i posjetilac sajta:

- javni sajt, blog i pravni dokumenti
- javni opis API-ja (OpenAPI specifikacija), koji je Distill sam objavio
- javni registar firmi i direktorijumi startapa
- javni DNS zapisi i zaglavlja mejlova koje je Distill poslao na probni nalog
- probni nalog na `app.distillintelligence.com`, korišćen nešto više od sedmice kao običan korisnik

Kod aplikacije nije čitan i ništa nije testirano na silu, jer to zabranjuju Distillovi uslovi korišćenja (§2.1). U nalogu nisu mijenjani mejl ni lozinka, a plaćanje nije započeto.

**Pravila pisanja:**

- Svaka tvrdnja ima izvor. Naše tumačenje je označeno sa **(zaključak)**, a ono što nije potvrđeno sa „nije provjereno”.
- Nazivi iz aplikacije pišu se tačno kao na ekranu, na engleskom (npr. „Latest news”, „Notable”, „Block publishers”).
- Vrijeme se računa od dana registracije probnog naloga („dan registracije”, „drugi dan”, „osmi dan”). Sati su po vremenskoj zoni naloga.
- Slike ekrana su sačuvane van repoa, jer se na nekima vidi mejl naloga.

**Probni nalog.** Praćene su tri velike svjetske kompanije (Anthropic, NVIDIA, Spotify) i tri balkanske (NIS, Telekom Srbija, Crnogorski Telekom). Trećeg dana je dodata i Elektroprivreda Crne Gore (EPCG). Balkanske kompanije su u watchlist-i „Balkan”. Napravljena je i tema o telekomunikacijama na Balkanu („Telecommunications in the Balkans”), a upozorenja mejlom uključena su samo za NIS.

## Najvažniji nalazi

1. **Distill je firma jednog čovjeka, sa malo korisnika.** Osnivač i CEO je jedina osoba koja se javno pominje, nema investitora, a u registru firma ima 0 zaposlenih. (zaključak) Po rednim brojevima u adresama, svi ostali korisnici zajedno su za pet-šest dana napravili jednu watchlist-u, nijednu temu i tri izvještaja.
2. **API je javno opisan do detalja, a aplikacija radi po istim pravilima.** OpenAPI specifikacija ima 10 operacija i šeme svih podataka. Broj vijesti po strani, kategorije, filteri, statusi pri dodavanju kompanije i blokiranje medija isti su u aplikaciji i u API-ju.
3. **Balkan je slabo pokriven, i to zavisi od korisnika.** Bez kompanija dodatih iz probnog naloga, Distill je imao samo 5 crnogorskih i 3 srpske kompanije, gotovo sve IT agencije. NIS, Telekom Srbija, Crnogorski Telekom i EPCG ušli su u bazu tek kad su dodati. Konkurenti su im svjetske i nordijske firme, a ne regionalne.
4. **Veliki zatrpavaju male.** U feedu, dnevnom mejlu i sedmičnom sažetku vijesti o Anthropic-u i NVIDIA-i potiskuju balkanske. Crnogorski mediji se rijetko pojavljuju, a objave Crnogorskog Telekoma podrazumijevani filter Notable potpuno sakrije.
5. **Crnogorski jezik ne postoji u Distillu.** Među 59 jezika prikaza nema crnogorskog, a standard ISO 639-1, po kom API vodi jezike, nema kod za njega. Objave iste crnogorske kompanije označene su nekad „Translated from Serbian”, a nekad „Translated from Bosnian”.
6. **AI tekstovi nisu označeni kao AI i imaju greške.** Izvještaji Brief i Standard nad istim vijestima tvrde suprotno o prodaji NIS-a MOL-u. Teze su ponekad jednostrane, promotivni tekst se prikazuje kao novinarski, a članak se veže i za kompaniju koja je samo usput pomenuta. NIS je pogrešno označen kao privatna firma.
7. **Mejlovi idu preko Resend-a i Amazon SES-a (SAD), po rasporedu.** Dnevni pregled stiže u 6:00 po zoni korisnika, sedmični sažeci petkom u 6:01–6:02. Upozorenja nisu „instant”: prvih sedam dana nije stiglo nijedno, a osmog dana stigla su dva odjednom, noću, od kojih jedno o vijesti od prethodnog dana.
8. **Svaki klik na izvor ide preko Distilla** (`distillintelligence.com/link/...`), uz oznaku odakle je došao (`?source=email`, `?source=report`). Distill, dakle, bilježi šta korisnici otvaraju.
9. **Nijedan AI servis nije naveden**, ni na spisku servisa ni u politici privatnosti, iako je AI srž proizvoda. Uslovi korišćenja dozvoljavaju treniranje AI modela na anonimizovanim podacima korisnika.
10. **Nalog ima osnovne propuste.** Nema dvostepene prijave ni brisanja naloga, a promjena lozinke ne traži staru lozinku. Podrška je samo mejlom. Cijena u aplikaciji je u eurima, tačno 10 manja nego u dolarima na sajtu.

## 1. Kompanija

| | |
|---|---|
| **Pravno lice** | Distill Intelligence AB, org. broj 559511-9180, Artemisgatan 39, Stockholm, Švedska |
| **Registrovana** | krajem 2024, djelatnost „izdavanje ostalog softvera”, osnovni kapital 25.000 SEK |
| **Javno lansiranje** | 2025 (prvi blog post u proljeće), dva lansiranja na Product Hunt-u iste godine |
| **Osnivač i CEO** | Gustav Fridell. Prema stranici About: ranije GetAccept, Boston Consulting Group i Bullhound Capital. Lični sajt dodaje i Ericsson |
| **Tim** | The Hub navodi „1-10”, a registar 0 zaposlenih. Druga osoba se nigdje ne pominje |
| **Finansiranje** | „Bootstrapping”, investitori nisu pronađeni |
| **Finansije za 2025.** | prihod 89.000 SEK, neto dobit 40.000 SEK (allabolag.se) |
| **Imenovani klijenti** | nema. Logotipi na početnoj strani su samo primjer feeda |
| **Kontakt** | support@distillintelligence.com, X/Twitter @DistillHQ, LinkedIn |

Jedini nezavisni tekst o firmi je onaj na sajtu švedske trgovinske komore u UK, iz 2026. Ostalo su profili u direktorijumima (The Hub, AlternativeTo i Slashdot bez recenzija, Product Hunt).

## 2. Cijene, probni period i ograničenja

- **Pro:** za jednog korisnika, karticom. Na sajtu $79 mjesečno, ili $59 mjesečno uz godišnje plaćanje ($708).
- **Team:** cijena po veličini tima. Uključuje zajedničke watchlist-e i teme, upozorenja u Slack-u i Microsoft Teams-u, pomoć pri podešavanju i prioritetnu podršku. Plaća se karticom, fakturom ili bankovnim transferom.
- **Enterprise plan ne postoji.** Team je najbliži tome.
- **API:** cijena nije objavljena, a pristup se traži preko obrasca.

| | Sajt | Aplikacija (3.10) |
|---|---|---|
| Mjesečno plaćanje | $79 | €69 |
| Godišnje, po mjesecu | $59 | €49 |
| Godišnje ukupno | $708 | €588 |
| Ušteda godišnjeg plaćanja | oko 25% | piše „SAVE 28%”, a stvarno je 29% |

(zaključak) Cijene su postavljene ručno za svaku valutu, a ne preračunate po kursu. Valuta se vjerovatno bira prema zemlji korisnika.

**Probni period:**

- 14 dana, puni Pro, bez kartice ako se korisnik prijavi poslovnim mejlom.
- Brojač „Trial ends in N days” zaokružuje naviše: na dan registracije i sljedećeg dana piše „14 days”, drugog dana „13 days”, a sedmog dana uveče „7 days” (ostalo je 6 dana i oko 22 sata).
- Ko plati prije kraja probe ne gubi preostale dane: prva naplata je na dan kraja probe.
- Poslije probe se nalog pauzira, a liste i podešavanja ostaju. Brišu se samo na zahtjev.

**Ograničenja:** brojčana ograničenja nisu objavljena. U probi je limit 50 kompanija, a vidi se samo u prozoru „Add several at once”. Jedan blog post obećava „unlimited company monitoring” za $59.

**Otkazivanje i povraćaj:** Pro se otkazuje bilo kad i radi do kraja plaćenog perioda. Novac se po pravilu ne vraća. Pretplata se sama obnavlja, a online kupac mora otkazati najkasnije dan prije obnove. Kupac sa ugovorom (Order Form) otkazuje 30 dana prije, a cijena mu pri obnovi raste za CPI-U ili 5%, šta je veće. Cijene su u USD, bez poreza.

## 3. Cjeline u aplikaciji

Brojevi cjelina su isti kao u mapi cjelina. Za svaku cjelinu piše šta radi, koje opcije ima, šta je uočeno u radu i nalazi.

### 3.1 Feed vijesti (Latest news)

Latest news je glavni feed: vijesti svih praćenih kompanija na jednom mjestu.

**Kartice:**

- **Updates** („Company updates”): objave same kompanije (sajt, newsroom, blog, zvanični LinkedIn).
- **Articles** („Media articles”): tekstovi drugih medija. Isti tekst iz više medija spaja se u jednu karticu, uz oznaku `[medij] +N`.
- **Summary** („Weekly summary”): sedmični sažetak, petkom.

**Prikaz:** Headlines (samo naslovi), Summaries (naslov i sažetak od jedne do dvije rečenice) ili Summaries with images (uz sliku iz izvora).

**Filteri** se čuvaju dugmetom Save i ostaju dok se ne promijene. Ispod piše „These filters also apply to recaps and summaries”, pa filter mijenja i mejlove i sažetke.

| | Updates | Articles |
|---|---|---|
| Importance: All, Notable, Major | da, podrazumijevano Notable | da, podrazumijevano Notable |
| Kategorije (10) | da, podrazumijevano sve | ne |
| „Include stock price commentary” | ne | da, podrazumijevano isključeno |
| Outlets | ne | link ka Settings → News → Block publishers (3.9) |

Kategorije su: Finance, M&A, Product, Marketing, Expansion, Partnerships, People, Operations, Legal, Sustainability.

**Kartica vijesti:**

- Vijesti su grupisane po danima (Today, Yesterday, pa datumi).
- Updates imaju oznake kategorija i oznaku prevoda („Translated from Serbian”), a Articles ime medija i `+N`.
- Naslov se ne može kliknuti. Do originala se stiže samo preko ikonica izvora: „In” vodi baš na tu objavu na LinkedIn-u, a ikonica dokumenta na sajt kompanije.
- Važnost se ne prikazuje, iako postoji u podacima i koristi se za filter.
- Svi linkovi ka izvorima idu preko `distillintelligence.com/link/...`.

**Učitavanje:** prvo 20 vijesti, a zatim „Load more”, dan po dan. Feed ide bar skoro tri sedmice unazad. Gdje se završava nije provjereno.

**Dugme Edit** („Edit followed companies”) bira koje praćene kompanije ulaze u feed i nudi „All news” ili „Topic”, kao watchlist-a. Pretraga u njemu traži po cijeloj bazi, pa se odatle dodaju i nove kompanije. (zaključak) Latest news je podrazumijevana watchlist-a sa svim praćenim kompanijama.

**Šta je uočeno:**

- **Sedmični sažetak.** Prvog petka (dan poslije registracije) piše da će prvi biti spreman „on Friday”. Drugog petka piše „There wasn't enough news about your companies for a summary yet”. Istog jutra mejl za iste praćene kompanije ima 10 teza i 50 izvora (3.8).
- **Greška 500.** Sedmog dana uveče Latest news i stranice tema su oko pola sata vraćale „500: Internal Error”, u već otvorenoj kartici. Poslije punog osvježavanja stranice sve je radilo. (zaključak) Uzrok je ili kratak kvar na serveru, ili nova verzija aplikacije objavljena dok je kartica bila otvorena, što je poznata pojava kod SvelteKit aplikacija.

**Nalazi:**

- Balkanske kompanije se gube. Na prvoj strani Articles nema nijedne, ni sa filterom All. Tek poslije „Load more” pojavljuje se NIS, sa tekstom srpskog medija Mondo.
- Važnost se ne vidi, pa korisnik ne zna zašto je vijest prošla filter Notable.
- Aplikacija i mejl se ne slažu oko sedmičnog sažetka.
- Greška 500 nema objašnjenje, a javna stranica sa stanjem servisa nije poznata.

### 3.2 Praćenje kompanija

Provjereno detaljno na NIS-u, uz poređenje sa Anthropic-om, Microsoft-om, EPCG-om i dva Telekoma. Iste stranice su pregledane ponovo tri dana kasnije.

**Stranica kompanije** (`/company/{id}/{ime}`, npr. `/company/9073/nis`) ima pet kartica, svaka sa svojom adresom (`?tab=...`): Overview, Summary, Updates, Articles i Competitors. Gore desno su meni upozorenja i Unfollow, a kod kompanije koja se ne prati samo Follow. Spisak praćenih kompanija je u meniju lijevo, bez broja i bez limita.

**Meni upozorenja:** No email alerts, Alerts for all news, ili samo Company updates ili samo Media articles (pod naslovom grupe „Alerts only for”). Nova kompanija ima „No email alerts”.

**Overview:** opis i sajt, Headquarters, Type, Founded, Employees, Industries, te Products and services i Target customers po 5 stavki. Polje bez podatka se sakrije.

| | NIS | Anthropic | Microsoft | EPCG |
|---|---|---|---|---|
| Type | Private company (pogrešno) | Private company | Public company | Public company |
| Founded | 1949 | ne prikazuje se | ne prikazuje se | ne prikazuje se |
| Employees | 10,000+ | 500-6,500 | 200,000+ | 1,000-5,000 |
| Industries | Integrated Oil & Gas | Machine Learning & Artificial Intelligence (AI) Services | Software (Other), Cloud Computing Services | Electric Utilities (Other), Fossil Fuel Electric Utilities |

- Tipovi firme su Public company (akcije na berzi), Private company, Government agency, Nonprofit, Partnership i Educational.
- (zaključak) Nazivi industrija su iz klasifikacije TRBC.
- Pri prvom pregledu Headquarters je imao samo državu. Tri dana kasnije stoji i grad („Novi Sad, Serbia”, „Niksic, Montenegro”), a brojevi zaposlenih kod konkurenata su osvježeni. (zaključak) Podaci se povremeno dopunjuju.

**Summary:** 5 teza, uz svaku brojevi izvora, a ispod numerisan spisak Sources. Klik vodi na original (kod NIS-a na nis.rs, na srpskom).

- Kod NIS-a sažetak pokriva oko dvije i po godine, a završava se oko dvije i po sedmice prije pregleda. Kod Anthropic-a pokriva oko sedmicu dana. (zaključak) Period zavisi od količine vijesti.
- Sažetak se ne osvježava svaki dan: kod NIS-a ni tri dana kasnije nije bilo promjene.
- Kod Crnogorskog Telekoma piše „Not enough recent news for a summary yet”.

**Updates i Articles** rade kao u Latest news, samo za tu kompaniju. Kod NIS-a se odmah vide domaći i strani mediji (Mondo, Euronews +14, Hungarian Conservative), koji se u Latest news izgube.

**Competitors:** spisak sa opisom i oznakama (država, tip, godina osnivanja, broj zaposlenih). Filteri su Company type, Country, Employee count i Founded year, isti kao u API-ju. Pretraga traži samo među konkurentima te kompanije. Konkurent se ne može otvoriti ni zapratiti: klik na ime ne radi ništa.

| Kompanija | Konkurenti na spisku | Šta fali |
|---|---|---|
| NIS | TotalEnergies, Chevron, Equinor, Eni, Shell, QatarEnergy... i OMV | MOL, INA, Petrol, Lukoil |
| EPCG | Tibber, Vattenfall, EDF Energy, Octopus Energy, RWE... | EPS, HEP, Elektroprivreda BiH |
| Crnogorski Telekom | četiri Telia firme, SoftBank Corp., Telekom Srbija Group... | ostali regionalni operateri |
| Anthropic | OpenAI, Google DeepMind, Mistral AI, DeepSeek... | ništa bitno |

(zaključak) Konkurenti se biraju po sličnosti djelatnosti i veličini, i to samo iz kompanija koje su već u bazi, a ne po tržištu. Jedini regionalni konkurent Crnogorskog Telekoma, Telekom Srbija, ušao je u bazu tek kad je dodat iz probnog naloga.

**Tekstovi medija o balkanskim kompanijama** (Articles, filter All):

| Kompanija | Šta postoji |
|---|---|
| NIS | Mondo, Euronews +14 (prevod sa mađarskog), Hungarian Conservative, sve iz posljednje dvije sedmice |
| Telekom Srbija | Prijepolje info +1, Newsmax Balkans, Business Wire +4, sve iz posljednje dvije sedmice |
| Crnogorski Telekom | samo tri teksta (Vijesti i dva puta Telecompaper), najnoviji star oko dva i po mjeseca |
| EPCG | SeeNews, Serbia SEE Energy Mining News, Vijesti; više nego za Crnogorski Telekom |

Kod Crnogorskog Telekoma kartica Updates sa filterom Notable kaže „No updates from this company yet”. Sa filterom All objave postoje, sve samo sa LinkedIn-a, a nijedna sa sajta. Objava o kvartalnim rezultatima bila je u Distillu istog dana.

**Nalazi:**

- NIS je „Private company”, a kotiran je na Beogradskoj berzi (NIIS). Greška je ostala i poslije osvježavanja podataka.
- OpenAI je „Partnership”. SoftBank Corp. ima „500–880 employees”, a ima ih desetine hiljada. Telia Finland i Telia Lietuva imaju sjedište „SOLNA, Sweden”.
- Godina osnivanja fali i velikim firmama (Anthropic, Microsoft), a NIS je ima.
- „No updates from this company yet” zavarava kad objave postoje, a sakrio ih je filter.
- Sažetak vijesti je ponekad tekst sa obrasca („Before downloading the whitepaper, we would like to ask you to complete your profile...”) ili standardna rečenica medija („Read the original news at telegraf.rs”).
- U naslovima ostaje ime medija („... | Euronews”, „... - Telecompaper”).
- Ista vijest mijenja naslov, i to sa drugačijim smislom. Grupa o MOL-u i NIS-u prvo je imala naslov „... contract signed” (Euronews +14), a tri dana kasnije „... According to Mol, nothing unusual happened” (HVG +18).

### 3.3 Dodavanje kompanija

Postoje dva posla: zapratiti kompaniju koja je već u bazi, i dodati novu preko adrese sajta.

**Praćenje postojeće kompanije:** preko pretrage (Ctrl+K) i dugmeta Follow na stranici kompanije, preko Latest news → Edit, ili pri registraciji, sa ponuđene liste (nordijske i svjetske firme, bez balkanskih). Iz Company finder-a i kartice Competitors kompanija se ne može ni otvoriti ni zapratiti (3.2, 3.4). Watchlist-a → Edit dodaje kompaniju u watchlist-u, ali je ne zaprati (3.5).

**Nova kompanija:** Company finder → Add company. Prozor „Add company” ima polje Company website, izbor „Add to a watchlist (optional)” i napomenu „It's added to your followed companies once it's ready”. Dugme „Add several at once” prima jednu adresu po redu, uz napomenu „Add up to 50 companies during your trial”. Nova kompanija se dodaje i pri registraciji.

| Proba | Poruka u aplikaciji | Status u API-ju |
|---|---|---|
| nova kompanija (epcg.com), prvi put | nije zapisana | (zaključak) `queued` |
| ista adresa, odmah ponovo | „We are already in the process of adding that company” | `already_processing` |
| kompanija koja se već prati | „That company already exists and you are now following it” | `already_exists` |
| nepostojeći sajt | „Thanks! The company will be added shortly” | `invalid` ili `failed` se ne prikazuje |

**Obrada nove kompanije (EPCG):**

- EPCG se pojavio među praćenim kompanijama za manje od 1 h 40 min. Distill navodi do 24 sata.
- Dok traje obrada, stranica već postoji, uz poruku „Some data may be incomplete while the company is being added”. To odgovara stanju „processing” u API-ju.
- Za oko sat i po Distill je povukao objave bar dvije sedmice unazad. Profil je tada imao po 3 stavke umjesto 5.
- Konkurenti su mu Tibber, Vattenfall, EDF Energy, Octopus Energy i RWE.

**Nepostojeći sajt** je prihvaćen istom porukom kao pravi. Ni tri dana kasnije nije bio u spisku, a mejl o grešci nije stigao.

**Nalazi:**

- Aplikacija ne provjerava odmah da li sajt postoji. Nepostojeći sajt tiho odbaci, bez obavještenja.
- Koliko je kompanija od 50 već dodato ne piše nigdje. API prima do 100 adresa po zahtjevu.
- (zaključak) Aplikacija i API koriste isti red čekanja za obradu novih kompanija.
- Energetika je bolje pokrivena od telekomunikacija: o EPCG-u pišu regionalni portali na engleskom (SeeNews, Serbia SEE Energy Mining News) i Vijesti.
- Vijest o jubileju TE Pljevlja ima kategoriju „Legal”. (zaključak) Kategorije dodjeljuje AI i ponekad griješi.
- Regionalnih konkurenata EPCG-a nema, isti obrazac kao kod NIS-a.

### 3.4 Pretraga i Company finder

**Pretraga** (polje Search, prečica Ctrl+K) traži „companies, industries and more”:

- Rezultati su grupisani na Companies, Watchlists, Topics i Reports. Na primjer, „Balkan” daje watchlist-u, temu i dva izvještaja iz probnog naloga.
- Kompanije traži i po opisu: za „Microsoft” izlaze i firme čiji opis kaže „Microsoft-focused”. Isto radi parametar `query` u API-ju.
- Na dnu stoji „Can't find a company? Add it” (3.3).
- Da li traži i industrije po imenu nije provjereno.

**Company finder:**

- Filteri: Industry group, Industry, Company type, Country, Employee count, Founded year i Clear filters. Isti su kao parametri `GET /v1/companies`.
- Red ima logo, ime, opis i oznake (država, tip, godina osnivanja, broj zaposlenih).
- Kompanija iz spiska ne može da se otvori ni zapratiti. Ukupan broj rezultata se ne prikazuje, a na dnu piše „No more companies”.

**Balkanske kompanije u bazi** (filter Country):

| Država | Kompanije |
|---|---|
| Montenegro (7) | Crnogorski Telekom i Elektroprivreda Crne Gore (dodate iz probnog naloga), Bild, Amplitudo, Alicorn, Coinis, fleka |
| Serbia (5) | NIS i Telekom Srbija Group (dodate iz probnog naloga), ElevenEs, JCHX Mining Management, Vega IT |

Ostalih pet crnogorskih kompanija su manje IT i digitalne agencije. I ovdje NIS piše „Private company”.

**Nalazi:**

- Bez dodatih kompanija Distill je imao samo 5 crnogorskih i 3 srpske kompanije, a ne najveće firme zemlje.
- (zaključak) Balkanske kompanije ulaze u bazu uglavnom kad ih korisnik doda, a ne zato što ih Distill sam prati. To objašnjava i nordijsku listu pri registraciji i daleke konkurente.
- To se ne slaže sa sajtom („any company in the world”): Distill može dodati bilo koju kompaniju, ali je unaprijed ne prati.
- Iz Company finder-a se kompanija ne može otvoriti, pa korisnik mora ime posebno da ukuca u pretragu.

### 3.5 Watchlist-e

Watchlist-a je imenovana grupa kompanija sa svojim filterom, feedom i sažetkom. Nalazi se u meniju lijevo, pod Following → Watchlists, uz stavku „New watchlist +”.

**Pravljenje** (prozor „New watchlist”):

- Name i izbor „All news” ili „Topics”.
- Topics: „Pick up to three topics”, a svaka tema ima preciznost Broad matches, Close matches (podrazumijevano) ili Exact matches. Ispod piše: „Broad matches find more news, exact matches less but more relevant news.”
- „Search companies” traži po cijeloj bazi i po opisu.
- Prozor sam nudi praćene kompanije koje još nisu ni u jednoj watchlist-i.

**Stranica watchlist-e** ima kartice Updates, Articles, Summary i Companies, a gore desno meni „Email summaries” i dugme Edit. Kompanija se iz kartice Companies ne može otvoriti klikom.

**Filter:** isti kao u Latest news, ali svaka watchlist-a ima svoj. Kad je uključena tema, na dugmetu piše npr. „Notable updates · 1 topic”.

Proba sa temom „AI chips” (Anthropic, NVIDIA, Spotify; filter Notable):

| Preciznost | Rezultat |
|---|---|
| Broad matches | 20 vijesti i Load more; za taj dan bar 5 |
| Close matches | 20 vijesti i Load more; za taj dan 3, među njima i jedna o istraživanju Alchajmerove bolesti |
| Exact matches | ukupno 1 vijest, stara oko sedam mjeseci |

Sve vijesti su o NVIDIA-i. (zaključak) Tema se poredi po smislu, a ne po tačnim riječima, pa je Close labaviji nego što ime kaže. To se slaže sa javnim opisom API-ja („semantic topic matching”).

**Watchlist-a i praćenje su dvije odvojene stvari.** Netflix dodat u „Balkan” nije postao praćen i nije se pojavio u Latest news, ali su njegove vijesti o filmovima i serijama preplavile balkanski feed. Brisanje watchlist-e ne otprati njene kompanije. To odgovara API-ju, gdje watchlist-a ima svoj spisak kompanija.

**Izmjena i brisanje:** prozor „Edit watchlist” ima ista polja i dugmad Delete, Cancel i Save. Delete traži potvrdu u običnom prozoru browsera („Are you sure you want to delete the watchlist? This can't be undone.”). Dijeljenja watchlist-e nema, a Settings nema karticu Integrations, što se slaže sa „Team plan only”.

**Mejlovi:** meni „Email summaries” nudi No emails i Email summaries. Nova watchlist-a se sama štiklira u Settings → Emails. Da li „No emails” isključuje i pregled i sedmični sažetak nije provjereno.

**Prvi sedmični sažetak** stigao je drugog petka, u aplikaciji i mejlom u 6:01, sa istim tezama. Ima oznaku „Week ended …” i 9 teza sa 14 izvora: zahtjev NIS-a OFAC-u za novu licencu, politička vijest o ruskom gasu i sankcijama NIS-u, projekti NIS-a za lokalne zajednice i požar na Rusandi, neodržana skupština akcionara EPCG-a, sporazumi EPCG-a sa stranim partnerima, remont TE Pljevlja, uticaj CBAM-a i rast Crnogorskog Telekoma 22 kvartala zaredom.

**Nalazi:**

- Telekom Srbija se u sedmičnom sažetku ne pominje, iako je u watchlist-i.
- Teza o CBAM-u je sada tačno pripisana EPCG-u, a ne medijima kao u izvještaju (3.7).
- Ranije stigli sažetak za 30 dana (3.8) nije sačuvan u aplikaciji. Strelica za prethodni sažetak ne prikazuje ništa.
- Nigdje ne piše da je sažetak napisao AI.
- (zaključak) Latest news istovremeno nema sažetak, iako ima sve kompanije iz „Balkan”. Pravilo za „dovoljno vijesti” nije jasno.

### 3.6 Teme

Tema prati vijesti o nekoj oblasti preko ključnih riječi, a ne preko kompanija. U API-ju ima samo `id`, `name`, `created_by`, `created_at` i `keywords[]`. Nalazi se u meniju lijevo, pod Following → Topics.

**Pravljenje** (prozor „New topic”):

- Name, pa dugme „Generate keywords”: Distill od imena sam napravi spisak ključnih riječi. Create je neaktivno dok ključne riječi ne postoje.
- Prva ključna riječ je ime teme malim slovima i ne može se obrisati. „Add keyword” dodaje novi red.
- Za isto ime („Balkan”) Distill je dva puta dao malo drugačiji spisak. (zaključak) Ključne riječi pravi AI.

**Stranica teme** ima samo kartice Articles i Summary, jer tema nema kompanija čije bi objave pratila. To se slaže sa API-jem, gdje članci tema imaju prefiks `top_art_`. Uz vijest stoji logo medija, a ne kompanije.

**Filter:** Importance (All, Notable, Major) i link Outlets („Block outlets you don't want news from in settings”), koji vodi na Settings → News, gdje se opcija zove „Block publishers”. Ispod piše „These filters also apply to summaries.” Kategorija nema.

**Tema o telekomunikacijama na Balkanu:**

- Ključne riječi su na engleskom (balkan telecom market, mobile operators balkans...) i jedna na našem jeziku („telekomunikacije Balkan”). Da li je nju Distill generisao nije utvrđeno.
- Vijesti su iz Sjeverne Makedonije, Grčke i međunarodne (DE-CIX, veza Bliskog istoka i Evrope). Na prvoj strani nema crnogorskih ni srpskih medija.
- Sa filterom All ima i lokalnih tekstova (Vijesti +3 o grupi 4iG). Sažetak tog teksta počinje sa „G Group, owner of One...”, bez „4i”.

**Probna tema „Electricity prices in Montenegro”:**

- Ključne riječi su bile o balkanskoj politici, a nijedna o struji. Tema je pri generisanju imala ime „Balkan”, a ime je promijenjeno poslije. (zaključak) Ključne riječi se prave samo jednom, pa ime teme može da vara.
- Poslije 25 sati tema je imala jedan članak: Barron's o nestancima struje na Zapadnom Balkanu, iz ljeta 2024.
- (zaključak) Distill pri traženju uzima u obzir i značenje imena teme, jer riječ „struja” postoji samo u imenu.
- Istih dana Distill ima svježe tekstove o struji u Crnoj Gori kod kompanije EPCG, a tema ih nije našla. (zaključak) Članci tema i članci kompanija se čuvaju i traže odvojeno, što se slaže sa prefiksima `top_art_` i `comp_art_`.

**Samostalna tema i tema u watchlist-i** su dvije različite stvari sa istim imenom:

| | Samostalna tema | Tema u watchlist-i (3.5) |
|---|---|---|
| Sadržaj | ime i ključne riječi | do tri teme sa preciznošću |
| Kompanije | nema ih | sužava vijesti kompanija iz watchlist-e |
| U API-ju | `keywords[]` | `topics[]` sa `query` i `match_strictness` |

**Izmjena, brisanje i mejlovi:** „Edit topic” ima Name i Keywords, i dugmad Delete, Cancel i Save. Save ne daje nikakvu poruku, a Delete traži istu potvrdu browsera kao kod watchlist-e. Nova tema se sama štiklira u Settings → Emails. Upozorenja za teme ne postoje.

**Prvi sedmični sažetak** stigao je drugog petka, u aplikaciji i mejlom u 6:02. Ima 6 teza: RETN u Bugarskoj, Starlink u Sjevernoj Makedoniji, rezultati Mtel-a (Glas Srpske), državni data centar u Sjevernoj Makedoniji, DE-CIX i grčko tržište.

**Nalazi:**

- Prvi put se pojavljuje medij sa našeg jezičkog prostora (Glas Srpske). Crnogorskih medija i operatera nema.
- Naslov izvora „DE-CIX boosts boosts gateway offering” je nepopravljen ni poslije sedmicu dana.
- DE-CIX sa telekomunikacijama na Balkanu ima slabe veze.
- Nigdje ne piše da je sažetak napisao AI.

### 3.7 Izvještaji

Izvještaj je AI tekst nad vijestima, za izabrani period, sa izvorima i izvozom u PDF. Nalazi se u meniju lijevo, pod Resources („Create report” i „Reports”).

**Pravljenje** (stranica „Create report”):

| Polje | Opcije |
|---|---|
| Scope | All companies you follow (podrazumijevano), Selected companies, A watchlist, A topic |
| Date range | Last 24 hours, Last 7 days, Last 30 days, Last 3 months, Last 6 months, Last 12 months, Custom range |
| Report structure | Auto-generate (podrazumijevano) ili Custom sections |
| Report detail | Brief („A short summary of the key points”), Standard („A balanced overview”, podrazumijevano), Comprehensive („An in-depth analysis”) |

Create je neaktivno dok se ne izabere period. Polja za sopstvena uputstva ili za jezik nema.

**Stranica izvještaja** ima dugmad PDF i Edit i kartice:

- **Report:** sekcije sa oznakom teme, naslovom i tezama. Brojevi izvora uz teze mogu se kliknuti.
- **Sources:** spisak izvora sa imenom medija, datumom i naslovom. Linkovi idu preko `/link/...?source=report`.
- **About:** „Created on … with news from the 7 days ended … about the companies in Balkan”, uz oznake kompanija.

**PDF** ima logo Distilla i mejl korisnika u zaglavlju, ime izvještaja i „Page X of N” u podnožju, a izvore na kraju. Veličina strane se bira u Settings → Account.

**Izmjena:** može se promijeniti samo ime. „Start a new report with the same settings” pravi novi izvještaj, a postojeći se ne može osvježiti. Dijeljenja linkom nema, samo PDF.

**Tri izvještaja nad watchlist-om „Balkan”:**

| Nivo | Period | Kompanije | Obim |
|---|---|---|---|
| Brief | 12 mjeseci | NIS, Telekom Srbija, Crnogorski Telekom | 3 poglavlja, oko 40 izvora |
| Standard | 12 mjeseci | iste tri | 6 poglavlja, bar 63 izvora, PDF od 6 strana |
| Comprehensive | 7 dana | iste tri i EPCG | 5 sekcija, 15 izvora, PDF od 5 strana |

- Comprehensive je bio gotov za 20–30 sekundi. Mejl da je izvještaj gotov ne stiže.
- Broj izvora zavisi prije svega od perioda. (zaključak) Nivo detalja mijenja broj poglavlja i teza, a ne način pisanja: i „Comprehensive” je spisak kratkih teza.
- Izvještaj uzima kompanije koje su u watchlist-i u trenutku pravljenja i kasnije se ne mijenja.

**Provjera tačnosti:**

- **Brief i Standard tvrde suprotno o MOL-u i NIS-u.** Standard kaže da je ugovor potpisan, a Brief da u pregovorima nema značajnih promjena. Euronews potvrđuje da je ugovor potpisan. Isti period i iste kompanije, pa razlika nije u podacima, nego u tome kako ih je AI sažeo.
- **Teza o CBAM-u** kaže „Media reports highlighted that the CBAM significantly reduced the value of EPCG's first-quarter electricity sales”. Izvor kaže da je procjenu (oko €13 miliona) dao sam EPCG, i da je firma ostala profitabilna. (zaključak) Teza je tačna, ali jednostrana.
- **Teza o Crnogorskom Telekomu** je tačna, ali izvor je promotivni tekst na sajtu Vijesti (rubrika „Aktuelno iz Telekoma”, adresa se završava sa „-promo”), prikazan kao običan tekst medija. (zaključak) Distill ne razlikuje promotivni sadržaj od novinarskog.

**Nalazi:**

- Izvještaj nigdje ne kaže da ga je napisao AI i nema napomenu o mogućim greškama.
- Telekom Srbija je u probnom izvještaju samo oznaka u About, bez sekcije i izvora.
- Ista kompanija ima tri imena: „Crnogorski Telekom”, „Telekom” i „Telekom Crne Gore”.
- Od 15 izvora tri su crnogorska. Prije dodavanja EPCG-a ih gotovo nije bilo.
- Izvještaj koristi i objave koje feed sakrije filterom Notable. (zaključak) Izvještaj ne poštuje filter watchlist-e, a mejlovi ga poštuju (3.8).

### 3.8 Mejlovi i upozorenja

**Podešavanja** (Settings → Emails):

- Vremenska zona (npr. „(GMT+01:00) Warsaw”). Prati ljetnje i zimsko vrijeme.
- News recaps: No emails, Once a day ili Once a week, zajednički za sve. Kvačice za praćene kompanije, svaku watchlist-u i svaku temu.
- News summaries (sedmični sažeci), sa istim kvačicama.
- „Skip emails when there's no news”.
- Alerts postoje samo za kompanije („Turn them on from the company's page”).
- „Tips and getting-started emails”.

**Šta je stiglo:**

| Kada | Mejl | Pošiljalac |
|---|---|---|
| dan registracije | „Confirm your email to get started with Distill” | info@distillintelligence.com |
| dan registracije | „You're all set” („Your Distill account is ready”) | nije zapisano |
| od drugog dana, svaki dan u 6:00 | „Daily news recap” | news@distillintelligence.com |
| četvrti dan, u 6:01 | „3 ways to get more out of Distill” | info@distillintelligence.com |
| šesti dan, u 22:40 | „The last 30 days in Balkan” | news@distillintelligence.com |
| osmi dan, noću | „NIS news”, dva upozorenja odjednom | news@distillintelligence.com |
| osmi dan (drugi petak), 6:01–6:02 | tri sedmična sažetka | news@distillintelligence.com |

Mejl da je izvještaj gotov ne stiže. Za podršku je treća adresa, support@distillintelligence.com (3.10).

**Dnevni pregled:**

- „Here's the latest news from the past day across the companies, watchlists, and topics you follow.”
- Dijelovi idu redom: praćene kompanije, svaka watchlist-a, svaka tema. Tema bez vijesti dobija samo red na dnu („No news in …”).
- Svaka stavka je naslov kao link, ime medija i ponekad `+N more`, bez sažetka i važnosti. Objave kompanija i tekstovi medija su izmiješani.
- Podnožje ima „Email settings” (vodi pravo na podešavanja) i „Unsubscribe”.

Nalazi o dnevnom pregledu:

- **Veliki zatrpavaju male:** u jednom pregledu Anthropic ima oko 14 stavki, NVIDIA oko 11, a balkanske kompanije dvije.
- **Duplikati:** vijest o kompaniji koja je i praćena i u watchlist-i javlja se u oba dijela.
- **Članak se veže i za usput pomenutu kompaniju.** Pod Spotify-em su bili tekstovi o američkoj politici i o nordijskim bankama. U Distillovom sažetku jednog Spotify se pominje samo kao primjer, a u drugom uopšte ne. Takvi članci prolaze i filter Notable.
- **Greške u naslovima:** „DE-CIX boosts boosts gateway offering” i „We ll be out of business”. (zaključak) Naslove niko ne provjerava ručno.
- (zaključak) „Skip emails when there's no news” preskače mejl samo kad nema nijedne vijesti ni u jednom dijelu.

**Linkovi** imaju oblik `www.distillintelligence.com/link/a{broj}/{naslov}?source=email`. U adresi je originalni naslov (npr. na srpskom), a u mejlu prevod. Klik vodi na original bez oznaka za praćenje (npr. `utm_source`). (zaključak) Distill bilježi klik kod sebe, razlikuje kanal (mejl, izvještaj), ali ne i vrstu mejla.

**Sažetak za 30 dana („The last 30 days in Balkan”)** stigao je šestog dana, u srijedu u 22:40, samo za watchlist-u „Balkan”. Ima 9 teza sa 32 izvora: EPCG 4, NIS 2, Telekom Srbija 3 (rad u SAD uz paket od $29, EXPO 2027, ulaganja u AI) i jednu tezu „Other notable developments” sa 9 nepovezanih vijesti.

- To je AI tekst u stilu izvještaja, bez oznake da ga je napisao AI.
- Crnogorski Telekom ima samo pola rečenice, iz promotivnog teksta. Njegove LinkedIn objave nisu ušle, jer ih filter Notable sakrije. (zaključak) Mejl poštuje filter watchlist-e.
- Izvori su samo naslovi, bez imena medija i datuma. Naslovi lokalnih medija su ponekad nespretno prevedeni.
- **Provjera teze o Telekomu Srbija u SAD:** teza kaže da paket od $29 ima pozive, SMS i 5GB interneta, a naslov izvora pominje TV kanale. Original (Newsmax Balkans, vijest Tanjuga) kaže da paket ima i jedno i drugo. Teza je tačna, samo nepotpuna. (zaključak) AI čita i tekst članka, ne samo naslov.
- Šta pokreće ovaj mejl ne zna se. Nije stigao petkom ni uz jutarnje mejlove, a vrijeme se ne poklapa ni sa satom registracije ni sa radnjama u nalogu. (zaključak) Vjerovatno ga šalje poseban povremeni posao, da novi korisnik vidi sažetak prije prvog petka.

**Mejl sa savjetima** stigao je četvrtog dana poslije registracije, u 6:01. Nudi tri savjeta („Get the news by email”, „Filter your feed”, „Create PDF reports”), dugme „Open Distill” i „Questions? Just reply to this email.” Obećava „instant alerts” na stranici kompanije. (zaključak) Šalje ga isti jutarnji posao koji šalje preglede.

**Upozorenja (Alerts)** su bila uključena za NIS od dana registracije („Alerts for all news”):

- Prvih sedam dana nije stiglo nijedno, iako je NIS imao nove objave (npr. zahtjev OFAC-u za novu licencu).
- Osmog dana noću (3:47) stigla su dva odjednom, pod naslovom „NIS news”. Prvo je o vijesti od prethodnog dana (politička vijest o ruskom gasu i sankcijama NIS-u, izvor Pravda Serbia), a drugo o vijesti od istog dana (dobit grupe NIS za tri kvartala).
- Jedno upozorenje je jedna vijest: naslov, sažetak, ponekad slika i link.
- (zaključak) **Upozorenja nisu „instant”.** Liči na noćno slanje u paketu, a ne na slanje odmah po objavi.
- Zašto prvih sedam dana nije stiglo nijedno nije poznato. Prva su stigla iste noći kad su mijenjana podešavanja vijesti (3.9). Da li je to slučajnost ne može se utvrditi spolja.
- „Alerts for all news” šalje i vijesti u kojima se NIS samo pominje. Ime medija je napisano na dva pisma („Pravda Serbia” i „Pravda Србија”).

**Sedmični sažeci** su stigli drugog petka u 6:01–6:02, prije dnevnog pregleda (koji je tada stigao u 6:03): „Weekly news summary” (praćene kompanije), „Weekly summary for Balkan” i „Weekly summary for Telecommunications in the Balkans”. Sažeci za watchlist-u i temu imaju iste teze kao u aplikaciji.

- „Weekly news summary” ima 10 teza i 50 izvora, a Latest news u aplikaciji kaže da nema dovoljno vijesti. (zaključak) Sažetak u aplikaciji i u mejlu se ne prave istim putem, ili aplikacija ima grešku.
- Anthropic i NVIDIA imaju 9 od 10 teza i 44 od 50 izvora. Balkanske kompanije su samo u zadnjoj tezi, a Telekom Srbija se ne pominje.
- Microsoft je u sažetku, iako se ne prati. (zaključak) Članak je vezan za neku praćenu kompaniju.
- U naslovima izvora fali apostrof („Here s”, „Nvidia s”), a jedan naslov je odsječen i u adresi linka („...IPO V”). (zaključak) To su ponovljive greške u obradi teksta.

**Tehnički detalji mejlova:**

| Podatak | Vrijednost | Izvor |
|---|---|---|
| mailed-by | `send.distillintelligence.com` | zaglavlje mejla |
| signed-by | `distillintelligence.com` (DKIM) | zaglavlje mejla |
| security | Standard encryption (TLS) | zaglavlje mejla |
| MX zapis za `send.distillintelligence.com` | `10 feedback-smtp.us-east-1.amazonses.com` | javni DNS (dns.google) |

Poseban poddomen `send.` i MX zapis prema Amazon SES-u su način na koji Resend traži da se domen podesi. Mejlovi se, dakle, šalju preko Resend-a, odnosno Amazon SES-a u regionu us-east-1 (SAD).

### 3.9 Jezici i prevod

Jezici se biraju u Settings → News, koja ima dva dijela: Languages i Block publishers.

**Languages:**

- „News will be displayed in your selected languages”. Može se izabrati više jezika, a English je uvijek uključen.
- Ukupno 59 jezika. Sa našeg prostora su Serbian, Croatian, Bosnian, Slovenian i Macedonian, a od susjednih Albanian i Hungarian. Srpski je jedan, bez podjele na pisma.
- **Crnogorskog nema:** pretraga „Montenegrin” daje „No matches”.
- Izbor se čuva odmah po kvačici, bez dugmeta Save, i ostaje poslije osvježavanja stranice. Važi za cijeli nalog.

**Zašto nema crnogorskog.** API jezike vodi po standardu ISO 639-1 (dvoslovni kodovi `sr`, `hr`, `bs`). ISO 639-1 nema kod za crnogorski. Crnogorski ima samo troslovni kod `cnr`, u standardu ISO 639-3. (zaključak) Zato ga Distill ne prepoznaje, nego crnogorske tekstove vodi kao srpske ili bosanske.

**Oznaka prevoda** („Translated from [jezik]”) je samo tekst. Original se u aplikaciji ne vidi, osim kad se izabere njegov jezik. API za svaku vijest ima polje `original` (`title`, `snippet`, `language`).

| Kompanija | Oznaka na crnogorskim objavama |
|---|---|
| Elektroprivreda Crne Gore | uvijek „Translated from Serbian” |
| Crnogorski Telekom | nekad „Translated from Serbian”, a nekad „Translated from Bosnian” |

**Proba sa srpskim uz engleski:**

- Većina objava NIS-a, EPCG-a i Crnogorskog Telekoma prikazuje se u originalu, bez oznake prevoda.
- NIS je ekavicom, a EPCG i Crnogorski Telekom ijekavicom. Distill ne mijenja varijantu teksta, samo mu pogrešno dodijeli jezik.
- Meni, kategorije i datumi ostaju na engleskom. Dugme za prebacivanje jedne vijesti na engleski nije uočeno.

**Nalazi:**

- **Prevod se ponegdje sakrije.** Po jedna objava NIS-a i EPCG-a označena je kao prevod sa srpskog, a sa izabranim srpskim ostane na engleskom, bez oznake. Korisnik ne zna šta je original, a šta prevod.
- **Jezici se miješaju u istom feedu:** kod Crnogorskog Telekoma dvije objave su na crnogorskom, a dvije na engleskom (jedna jer je vođena kao bosanska).
- **Sažetke piše AI na oba jezika.** Sažetak oglasa za posao kaže „konkurencija je kratka” (misli se na kratak konkurs), a engleski „the competition is short”. U jednom sažetku na „srpskom” je hrvatska riječ „promicala”.
- Za izvještaje se jezik ne može izabrati, a mejlovi su bili samo na engleskom.
- Blog kaže „every language”, a izbor je ograničen na 59 jezika.

**Block publishers** („Hide articles from specific publishers in your feeds”):

- Prozor „Block publishers” ima pretragu medija. Svaka stavka ima logo, ime i domen.
- Proba: blokiran je Dagens industri (`di.se`). Njegov tekst je odmah nestao iz feeda, bez osvježavanja, a poslije odblokiranja se vratio.
- Na „Dagens industri” izlaze tri stavke sa istim imenom i različitim domenima (`di.se`, `dagensnaringsliv.se`, `energimarknaden.di.se`).
- Ista stvar ima tri imena: „Outlets” u filteru, „Block publishers” u podešavanjima i `blocked_domains` u API-ju.

Nalazi:

- Blokiranje radi odmah i može se potpuno vratiti. Važi samo za članke medija.
- (zaključak) Blokira se po domenu, a ne po mediju, pa korisnik mora sam naći sve domene jednog medija.
- Domen `dagensnaringsliv.se` nosi ime „Dagens Industri”. (zaključak) Imena medija u bazi nisu uvijek tačna.
- (zaključak) Spisak medija je veoma gust za Švedsku, što odgovara švedskoj firmi.
- Da li blokiranje važi i za mejlove nije provjereno.

### 3.10 Nalog i pretplata

U ovoj cjelini ništa nije mijenjano, plaćanje nije započeto, a stranica Stripe-a nije otvarana.

**Settings → Account:**

- Signed in as (mejl naloga).
- Document size za PDF: A4, US Letter ili US Legal.
- Credentials: promjena mejla i lozinke („Enter a new password”).

Nema: imena, slike, naziva firme, brisanja naloga, dvostepene prijave (2FA), spiska sesija, izvoza podataka ni dijela o plaćanju.

**Prelazak na plaćeni plan:** „Upgrade to continue” na dnu menija otvara `/activate` („Upgrade to Distill Pro”). Tu su prekidač Monthly / Yearly sa „SAVE 28%”, kartica „Distill Pro” sa oznakom koliko je dana probe ostalo i tok plaćanja: „Today: Keep your full access, no charge”, a na dan kraja probe „€69/month, billed monthly” ili „€49/month, billed €588 yearly”. Ispod je „Secured by Stripe • Cancel anytime”. Nudi se samo Pro.

**Podrška:** Support u meniju je samo mejl link (`mailto:support@distillintelligence.com`). Nema chata, obrasca ni čestih pitanja.

**Prijava i odjava:** Log out odjavljuje odmah, bez potvrde. Prijava ide preko „Sign in with Google”, „Sign in with Microsoft” ili mejla i lozinke. Prijave linkom na mejl i SSO-a nema. Adresa stranice za prijavu ima parametar `landing_page`.

**Nalazi:**

- (zaključak) Forma za promjenu lozinke traži samo novu lozinku, a ne i trenutnu. Ko dođe do otvorene sesije mogao bi promijeniti lozinku. Nije probano.
- Nema 2FA ni brisanja naloga, iako je firma iz EU. Brisanje se može tražiti samo preko podrške.
- Ušteda kod godišnjeg plaćanja je 29% (€588 umjesto €828), a piše 28%.
- (zaključak) Google, Microsoft i mejl sa lozinkom su načini prijave iz Supabase Auth, što se slaže sa spiskom servisa.
- (zaključak) Podrška samo mejlom odgovara firmi jednog čovjeka.
- (zaključak) `landing_page`, `?source=email` i `?source=report` pokazuju da Distill svuda mjeri odakle ljudi dolaze.

## 4. Company News API

Izvor: [OpenAPI specifikacija](https://api.distillintelligence.com/openapi.json) (OpenAPI 3.1, „Distill API” verzija 1.0). Stranica `/api` na sajtu pokazuje dvije operacije, blog o lansiranju pet, a specifikacija 10. Osnivač je specifikaciju 2026. prijavio u javni direktorijum APIs-guru.

- **Adresa:** `https://api.distillintelligence.com`, verzija u putanji (`/v1/`)
- **Prijava:** `Authorization: Bearer <ključ>`, za svaku operaciju
- **Primjeri koda:** TypeScript, cURL i Python. Zvanični SDK nije pronađen.

| Operacija | Šta radi |
|---|---|
| `GET /v1/companies` | pretraga i filtriranje kompanija |
| `POST /v1/companies` | dodavanje do 100 kompanija po adresi sajta, opciono u watchlist-u; odgovor 202 sa statusom po stavci (`queued`, `already_processing`, `already_exists`, `invalid`, `failed`) |
| `GET /v1/companies/{id ili domen}` | profil kompanije, ili 202 `{"status": "processing"}` dok se obrađuje |
| `GET /v1/companies/{id ili domen}/news` | vijesti kompanije |
| `GET /v1/watchlists`, `GET /v1/watchlists/{id}` | watchlist-e u organizaciji i podešavanja jedne |
| `GET /v1/watchlists/{id}/news` | vijesti watchlist-e |
| `GET /v1/topics`, `GET /v1/topics/{id}` | teme u organizaciji i ključne riječi jedne |
| `GET /v1/topics/{id}/news` | vijesti teme |

**Filteri vijesti:** `type` (update, article), `min_impact` (podrazumijevano `medium`, uz posebne `min_article_impact` i `min_update_impact`), `categories` (samo za updates), `blocked_domains` (samo za articles), `since`, `until`, `language` (ISO 639-1) i `include_stock_commentary_articles` (podrazumijevano `false`). Watchlist-a i tema bez parametara koriste sačuvana podešavanja.

**Paginacija:** vijesti preko kursora (`limit` od 1 do 100, podrazumijevano 20, `cursor`, `next_cursor`, `has_more`), a kompanije po stranama (`page`, `limit`).

**Greške:** 400, 401, 404, 429 i 500, u obliku `{"error": "...", "issues": ...}`. Broj dozvoljenih zahtjeva nije objavljen, ali odgovor 429 postoji. (zaključak) Polje `issues` liči na format biblioteke Zod (TypeScript).

**Model podataka iz šema:**

| Objekat | Polja |
|---|---|
| Company | `id`, `name`, `short_name`, `url`, `description`, `customers[]`, `offering[]`, `primary_industry`, `secondary_industry`, `company_type`, `founded_year`, `employee_count_min`, `employee_count_max`, `country_code`, `locality`, `region`, `postal_code` |
| Vijest | `id`, `type`, `name`, `domain`, `url`, `image_url`, `title`, `snippet`, `published_at`, `categories`, `impact`, `original` (`title`, `snippet`, `language`), `company` ili `topic`, `sources[]` |
| Watchlist | `id`, `name`, `created_by`, `created_at`, `companies[]`, `settings` (važnost za articles i updates, kategorije, komentari o akcijama, `topics[]` sa `query` i `match_strictness`) |
| Topic | `id`, `name`, `created_by`, `created_at`, `keywords[]` |

**Tragovi arhitekture:**

- ID-jevi imaju prefikse `comp_upd_`, `comp_art_` i `top_art_` (izvori `..._src_`). (zaključak) Objave kompanija, članci o kompanijama i članci tema čuvaju se odvojeno. To potvrđuje i proba sa temom (3.6).
- Nova kompanija ide u red čekanja (`queued`, `processing`, 202). (zaključak) Obrada radi u pozadini.
- Watchlist-e i teme se traže „across the organization”, sa poljem `created_by`. (zaključak) Podaci pripadaju organizaciji, a ne samo korisniku.
- Više tekstova o istoj priči spaja se u jedan zapis, sa svim izvorima u `sources[]`.

**Aplikacija i API rade po istim pravilima:**

| U aplikaciji | U API-ju |
|---|---|
| 20 vijesti, pa „Load more” | `limit=20`, `cursor` i `next_cursor` |
| Notable i Major | (zaključak) `min_impact=medium` i `high` |
| 10 kategorija, samo za Updates | `categories`, samo za updates |
| „Include stock price commentary”, isključeno | `include_stock_commentary_articles=false` |
| Block publishers, samo za Articles | `blocked_domains`, samo za articles |
| Languages i „Translated from …” | `language` i polje `original` |
| filteri u Company finder-u | `industry_group_ids`, `industry_ids`, `company_types`, `country_codes`, `min/max_employee_count`, `min/max_founded_year` |
| poruke pri dodavanju kompanije | `already_processing`, `already_exists` |
| „Some data may be incomplete while the company is being added” | 202 `processing` |
| tema u watchlist-i i samostalna tema | `topics[]` sa `match_strictness`, odnosno `keywords[]` |
| polja u Overview | `description`, `country_code`, `locality`, `company_type`, `founded_year`, `employee_count_min/max`, `primary/secondary_industry`, `offering`, `customers` |

## 5. Integracije

- **Mejl:** upozorenja po kompaniji, dnevni ili sedmični pregled i sedmični sažetak petkom (3.8).
- **Slack:** od kraja 2025, samo Team plan. Podešava se u Settings → Integrations, pa se uključuje po watchlist-i.
- **Microsoft Teams:** od 2026, samo Team plan. Prema uputstvu radi preko incoming webhook-a.
- **U probnom nalogu** nema kartice Integrations, pa Slack i Teams nisu dostupni, iako novija uputstva kažu da proba ima „access to all features”.
- **REST API** (dio 4) i **PDF** izvještaji (3.7).
- **Nisu pronađeni:** odlazni webhook-ovi, RSS kao izlaz, Zapier i gotova veza sa CRM-om.

## 6. Pravila korišćenja i privatnost

**Spisak servisa koje Distill koristi** ([subprocessors](https://www.distillintelligence.com/subprocessors), ažuriran 2025):

| Servis | Država | Namjena |
|---|---|---|
| Cal.com | SAD | zakazivanje sastanaka |
| Cloudflare | SAD | zaštita sajta (web application firewall) |
| GetAccept | Švedska | potpisivanje dokumenata |
| Hetzner | Njemačka | serveri i infrastruktura |
| Resend (Plus Five Five, Inc.) | SAD | slanje mejlova |
| Stripe | SAD | plaćanje |
| Supabase | SAD | baza podataka i prijava korisnika |
| Vercel | SAD | hosting sajta |

Na spisku nema nijednog AI servisa ni alata za analitiku. Region data centra nije naveden.

**Uslovi korišćenja** ([terms](https://www.distillintelligence.com/terms-of-service), ažurirani 2026):

- švedsko pravo; sporovi idu na medijaciju, pa na arbitražu u Stockholmu
- §2.1 zabranjuje reverse inženjering, sigurnosno testiranje i pravljenje konkurentskog proizvoda
- §1.6 dozvoljava Distillu da na podacima korisnika razvija i trenira AI modele, ali tek kad ih objedini i učini anonimnim
- AI rezultati mogu biti netačni; sadržaj nije finansijski ni pravni savjet
- SLA nema, a odgovornost je ograničena na iznos plaćen u posljednjih 12 mjeseci
- poslije raskida, na zahtjev, podaci se brišu za 60 dana

**Politika privatnosti** ([privacy](https://www.distillintelligence.com/privacy-policy)): region i rokovi čuvanja podataka nisu navedeni, a podaci se mogu prenositi u SAD. Aplikacija koristi samo neophodne kolačiće i local storage za podešavanja prikaza. Nema automatizovanog odlučivanja, a korisnik mora imati bar 18 godina.

**DPA** ([ugovor o obradi podataka](https://www.distillintelligence.com/data-processing-agreement)):

- Supabase je ključni servis za bazu i prijavu korisnika
- promjene na spisku servisa najavljuju se 10 radnih dana ranije
- o incidentu se javlja u roku od 72 sata
- poslije raskida podaci se brišu za 60 do 90 dana
- pominju se izvještaji SOC 2 Type II ili ISO 27001 na zahtjev. (zaključak) Nije jasno da li Distill ima sopstveni izvještaj ili misli na servise koje koristi.

**Nijedan AI servis** (OpenAI, Anthropic, Google...) nije naveden ni na jednom od ovih mjesta. (zaključak) Moguće je da nije prijavljen jer obrađuje samo javne vijesti, ili da modeli rade na Hetzner serverima. Ništa od toga nije potvrđeno.

## 7. Izvori podataka i obim

**Šta Distill kaže:**

- **Izvori:** newsroom-i i blogovi kompanija, RSS, Medium i Substack, zvanični LinkedIn, poslovni, stručni i lokalni mediji na više jezika.
- **Broj izvora:** na većini stranica „thousands of sources”, a na jednoj „100k+”.
- **Kompanije:** „any company in the world as long as they have a website”.
- **Jezici:** „every language”. Sve se prevodi na engleski.
- **Prikupljanje:** Distill kaže da sam rješava proxy-je, blokade IP adresa, CAPTCHA-e i promjene izgleda sajtova. Kako dolazi do LinkedIn objava nije objašnjeno.
- **Obrada:** vijesti se vezuju za kompaniju preko domena, a ne preko ključnih riječi. Kontekst (industrija, imena direktora) služi da se razlikuju firme sličnih imena.
- **Industrije:** 13 sektora i 153 industrije. (zaključak) Imena sektora se poklapaju sa klasifikacijom TRBC (LSEG).

**Šta se vidi u aplikaciji:**

- Za Crnogorski Telekom Distill prati samo LinkedIn, a ne sajt. Objave sa LinkedIn-a stižu istog dana.
- Za NIS ima vijesti oko dvije i po godine unazad, iako je tek dodat. Pretraga tema ide bar dvije godine unazad.
- Članak se veže i za kompaniju koja je samo pomenuta, a promotivni sadržaj se ne razlikuje od novinarskog.
- Medija iz Švedske i nordijskih zemalja ima mnogo, a crnogorskih malo.

**Procjene iz rednih brojeva u adresama** (zaključak; dobijeno samo čitanjem adresa sopstvenog naloga):

| Šta | Procjena |
|---|---|
| kompanije | oko 9.100 u bazi; za oko tri dana ušlo je oko 45 novih |
| watchlist-e | oko 340 od početka rada; za pet dana ostali korisnici su napravili jednu |
| teme | oko 80; za šest dana niko drugi nije napravio nijednu |
| izvještaji | oko 240; za četiri dana ostali korisnici su napravili tri |
| članci (oznaka `a{broj}` u linkovima) | oko 5,6 miliona, uz oko 10.000 dnevno; gruba procjena iz dva broja |

Brojevi su zaista redni: tri balkanske kompanije dodate jedna za drugom dobile su uzastopne ID-jeve (9071, 9072, 9073). (zaključak) Distill koristi mali broj ljudi, a baza kompanija raste uglavnom kad korisnici dodaju nove.

## 8. Tehnologija i infrastruktura

Samo javni izvori i ono što se vidi pri običnom korišćenju aplikacije.

| Trag | Šta pokazuje | Izvor | Pouzdanost |
|---|---|---|---|
| Putanje `/_app/immutable/` | frontend u SvelteKit-u | adrese fajlova na javnom sajtu | trag |
| Stranica „500: Internal Error” sa „Go back to the homepage” | podrazumijevana stranica greške u SvelteKit-u | aplikacija | trag |
| `/_vercel/image`, Vercel na spisku | sajt je na Vercel-u | sajt, spisak servisa | potvrđeno |
| Supabase | baza (PostgreSQL) i prijava korisnika | spisak servisa, DPA | potvrđeno |
| Prijava preko Google-a, Microsoft-a i mejla | (zaključak) Supabase Auth | stranica za prijavu | trag |
| Hetzner (Njemačka) | sopstveni serveri; (zaključak) vjerovatno za prikupljanje i obradu vijesti | spisak servisa | potvrđeno |
| Cloudflare | zaštita sajta | spisak servisa | potvrđeno |
| Resend → Amazon SES, us-east-1 | slanje mejlova | zaglavlje mejla, javni DNS | potvrđeno |
| Stripe, „Secured by Stripe” | plaćanje | spisak servisa, aplikacija | potvrđeno |
| `/link/...` sa `?source=email` i `?source=report` | bilježenje klikova, pa preusmjeravanje | aplikacija, mejl, PDF | potvrđeno |
| 202 i `queued`/`processing`; „Some data may be incomplete...” | obrada novih kompanija u pozadini, preko reda čekanja | OpenAPI, aplikacija | potvrđeno |
| Pregled u 6:00 po zoni korisnika, savjeti u 6:01, sažeci petkom u 6:01–6:02 | zakazani jutarnji poslovi | mejlovi | potvrđeno |
| Upozorenja noću, u paketu; sažetak za 30 dana u 22:40 | (zaključak) posebni poslovi, a ne slanje odmah | mejlovi | trag |
| Izvještaj gotov za 20–30 sekundi, kasnije se ne mijenja | (zaključak) pravi se na zahtjev i čuva kao snimak | aplikacija | trag |
| Uzastopni ID-jevi u adresama | (zaključak) redni brojevi u bazi, pored ID-jeva sa prefiksima u API-ju | aplikacija, mejl | trag |
| Brisanje traži ugrađenu potvrdu browsera | jednostavan frontend | aplikacija | potvrđeno |
| Product Hunt profil osnivača („Stack”) | Supabase, Svelte, Stripe | Product Hunt | trag |
| AI model ili servis | nepoznato | nigdje nije naveden | otvoreno |

Javni GitHub firme, oglasi za posao i tehnički blog ne postoje. Javne stranice o kompanijama na sajtu (`/news/{ime}`, `/competitors/{ime}`) izgledaju kao automatski pravljene stranice za Google pretragu.

## 9. Konkurencija i pozicioniranje

- **Distill se sam poredi sa** oko 35 alata, u tekstovima „X vs. Distill”:
  - praćenje konkurencije: Crayon, Klue, Owler, Contify, Kompyte
  - praćenje medija: Meltwater, Cision, Signal AI, Brandwatch
  - čitači vijesti: Feedly, Inoreader, Google Alerts
  - baze podataka o firmama: PitchBook, FactSet, LSEG Workspace, ZoomInfo
  - nadzor promjena na sajtovima: Visualping, Distill.io
- **Poruka:** jeftin alat koji korisnik sam podesi za dva minuta, bez održavanja. Prati sopstvene kanale kompanija, a ne samo agencijske vijesti, spaja duplikate i prevodi.
- **Cijene konkurenata** koje Distill navodi, bez izvora: Crayon i Klue 15–40 hiljada dolara godišnje, Feedly Market Intelligence od $1.600 mjesečno, Owler Pro $39 mjesečno.
- **Svoj API poredi sa** NewsAPI, Crunchbase, Diffbot, Event Registry, GDELT i Factiva.
- **Blog:** od ljeta 2026. izlazi tačno jedan tekst dnevno, uglavnom poređenja i vodiči. (zaključak) Sadržaj se pravi automatski, radi Google pretrage.
- **Razvoj proizvoda po blogu:** 2025. lansiranje, probni period, sedmični sažeci, blokiranje izvora, LinkedIn, teme u watchlist-i, prevod, filteri važnosti i Slack; 2026. Competitor Finder, izvještaji, Microsoft Teams, samostalne teme i API.
- **Pažnja na imena:** Distill.io (nadzor sajtova) i američka firma „Distill” su druge firme.

## 10. Kontradikcije i greške

| Nalaz | Izvor |
|---|---|
| Izvještaji Brief i Standard nad istim vijestima tvrde suprotno o prodaji udjela u NIS-u MOL-u. Euronews potvrđuje da je ugovor potpisan, pa je Brief pogriješio | izvještaji nivoa Brief i Standard nad watchlist-om „Balkan”, kartica Articles kod NIS-a |
| Teza o CBAM-u pripisuje procjenu medijima, a dao ju je EPCG; izostavlja iznos i protivtežu | probni izvještaj nivoa Comprehensive |
| Promotivni tekst („-promo”) prikazan kao običan tekst medija | izvještaj, dnevni pregled, sažetak za 30 dana |
| Sažetak vijesti je tekst sa obrasca („Before downloading the whitepaper...”) ili standardna rečenica medija („Read the original news at telegraf.rs”) | kartica Articles kod oba Telekoma |
| Profil NIS-a kaže „Private company”, a NIS je kotiran na Beogradskoj berzi (NIIS) | profil kompanije, [Beogradska berza](https://www.belex.rs/eng/trgovanje/vesti/hartija/NIIS/2010) |
| OpenAI je „Partnership”; SoftBank Corp. ima „500–880 employees”; Telia Finland i Telia Lietuva imaju sjedište „SOLNA, Sweden” | konkurenti Anthropic-a i Crnogorskog Telekoma |
| Ista grupa vijesti promijeni naslov sa drugačijim smislom („contract signed” → „nothing unusual happened”) | Articles kod NIS-a |
| Ponovljena riječ „DE-CIX boosts boosts gateway offering”, nepopravljena ni poslije sedmicu dana | dnevni pregled, sedmični sažetak teme |
| Izgubljeni apostrofi („We ll”, „Here s”, „Nvidia s”) i odsječen naslov („IPO V”) | dnevni pregled, sedmični sažetak |
| Ista kompanija ima tri imena: „Crnogorski Telekom”, „Telekom” i „Telekom Crne Gore” | probni izvještaj |
| Objave iste crnogorske kompanije označene nekad „Translated from Serbian”, a nekad „Translated from Bosnian” | Updates kod Crnogorskog Telekoma |
| Sa izabranim srpskim neke vijesti ostanu na engleskom, a oznaka prevoda nestane | Updates kod NIS-a i EPCG-a |
| Domen `dagensnaringsliv.se` nosi ime „Dagens Industri” | Block publishers |
| „No updates from this company yet”, a objave postoje i sakrio ih je filter | Updates kod Crnogorskog Telekoma |
| Ime teme i ključne riječi se ne slažu kad se ime promijeni | probna tema |
| Nepostojeći sajt prihvaćen porukom „The company will be added shortly”, a zatim tiho odbačen | Add company |
| Mejl i blog obećavaju „instant alerts”, a upozorenja su stigla tek osmog dana, dva odjednom, noću | mejl sa savjetima, blog |
| Latest news kaže da nema dovoljno vijesti za sažetak, a mejl za iste kompanije ima 10 teza | aplikacija, mejl „Weekly news summary” |
| Mejlovi poštuju filter Notable watchlist-e, a izvještaj ne | sažetak za 30 dana, probni izvještaj |
| „SAVE 28%”, a ušteda je 29% | stranica `/activate` |
| „Unlimited company monitoring”, a limit od 50 kompanija u probi | blog, aplikacija |
| „100k+” izvora na jednoj stranici, „thousands” na ostalim | sajt |
| „Every language” na blogu, a 59 jezika u aplikaciji | blog, Settings → News |
| Blog o izvještajima ne pominje period od 24 sata, a aplikacija ga nudi | blog, aplikacija |
| Slack i Teams su „Team plan only”, a novija uputstva kažu da proba ima „access to all features” | blog |
| Stranica o upozorenjima na jednom mjestu nudi Email, Slack i Teams, a na drugom samo Email i Slack | [business-news-alerts](https://www.distillintelligence.com/business-news-alerts) |
| Uslovi kažu da se podaci brišu za 60 dana, a DPA za 60 do 90 dana | terms, DPA |
| The Hub kaže „1-10” zaposlenih, a registar 0 | The Hub, allabolag.se |

## 11. Otvoreno

- **Upozorenja:** zašto prvih sedam dana nije stiglo nijedno, i da li sada stižu redovno.
- **Sažetak za 30 dana:** šta pokreće mejl „The last 30 days in Balkan”.
- **Sedmični sažetak u Latest news:** zašto ga aplikacija nema, a mejl ga ima, i koje je pravilo za „dovoljno vijesti”.
- **Prvi dnevni pregled:** zašto ga nije bilo prvog dana poslije registracije.
- **Kraj probe:** šta aplikacija prikazuje kad proba istekne i da li mejlovi prestaju.
- **Mejlovi:** da li Block publishers važi i za mejlove; kako mejlovi izgledaju sa izabranim srpskim; da li „No emails” na watchlist-i isključuje i pregled i sažetak.
- **Pretraga:** da li traži i industrije po imenu.
- **Feed:** koliko daleko unazad ide.
- **AI:** koji AI model ili servis Distill koristi.
- **Izvještaji:** kako se Brief i Standard razlikuju nad istim vijestima za 7 dana.
- **Klikovi iz aplikacije:** koju oznaku `source` dobijaju.
- **Dodavanje kompanije:** koja poruka se pojavi pri prvom dodavanju.
- **Namjerno nije otvarano:** stranica Stripe-a, registracija i promjena lozinke.

## Izvori

- Probni nalog na [app.distillintelligence.com](https://app.distillintelligence.com). Slike ekrana su sačuvane van repoa.
- [Distill Intelligence](https://www.distillintelligence.com/), [About](https://www.distillintelligence.com/about), [Pricing](https://www.distillintelligence.com/pricing), [Blog](https://www.distillintelligence.com/blog)
- [Company News API](https://www.distillintelligence.com/api), [OpenAPI specifikacija](https://api.distillintelligence.com/openapi.json), [najava API-ja](https://www.distillintelligence.com/blog/introducing-distill-company-news-api), [APIs-guru prijava](https://github.com/APIs-guru/openapi-directory/issues/3665)
- [Subprocessors](https://www.distillintelligence.com/subprocessors), [Terms of Service](https://www.distillintelligence.com/terms-of-service), [Privacy Policy](https://www.distillintelligence.com/privacy-policy), [Data Processing Agreement](https://www.distillintelligence.com/data-processing-agreement)
- [Slack integracija](https://www.distillintelligence.com/blog/distill-slack-company-news-alerts), [Microsoft Teams integracija](https://www.distillintelligence.com/blog/distill-microsoft-teams-company-news-alerts), [Teams preko webhook-a](https://www.distillintelligence.com/blog/how-to-route-market-and-competitor-intelligence-into-microsoft-teams), [Business news alerts](https://www.distillintelligence.com/business-news-alerts)
- [News scraping](https://www.distillintelligence.com/news-scraping), [Industries](https://www.distillintelligence.com/industries), [teme](https://www.distillintelligence.com/blog/introducing-topics), [izvještaji](https://www.distillintelligence.com/blog/introducing-custom-reports), [prevod sa svih jezika](https://www.distillintelligence.com/blog/articles-now-in-every-language), [unlimited company monitoring](https://www.distillintelligence.com/blog/semantic-business-monitoring-vs-visual-website-change-scrapers)
- [allabolag.se: Distill Intelligence AB](https://www.allabolag.se/foretag/distill-intelligence-ab/stockholm/datautveckling-systemutveckling-programutveckling/2KJ6TL8I5YDOJ), [The Hub](https://thehub.io/startups/distill-intelligence), [Švedska trgovinska komora u UK](https://www.scc.org.uk/resources/chamber-news/turning-a-world-of-info-into-business-decisions)
- [Product Hunt profil osnivača](https://www.producthunt.com/@gustavf), [lični sajt osnivača](https://gustavfridell.com/)
- [Google Public DNS](https://dns.google/resolve?name=send.distillintelligence.com&type=MX) za MX zapis `send.distillintelligence.com`
- [Beogradska berza: NIS (NIIS)](https://www.belex.rs/eng/trgovanje/vesti/hartija/NIIS/2010), [ISO 639-3: cnr](https://iso639-3.sil.org/code/cnr), [Wikipedia: TRBC](https://en.wikipedia.org/wiki/The_Refinitiv_Business_Classification)
