# REA: reverse inženjering Distilla

| Autor | Nemanja Anđić |
| --- | --- |
| Datum izrade | 1.11.2026 |
| Datum izmjene | 15.11.2026 |
| Verzija | 1.1 |

## Uvod

Ovaj dokument opisuje kako je alat REA korišćen za analizu platforme Distill Intelligence i šta je tom analizom pronađeno. Pokriva alat i pravila rada, instalaciju, probu na sopstvenom sajtu, primjenu na Distill, nalaze, kratak opis arhitekture u četiri dijela i ono što ostaje nepoznato. Cijela arhitektura Distilla, sa dijagramima, opisana je u tehničkoj dokumentaciji ([`tehnicka-dokumentacija.pdf`](tehnicka-dokumentacija.pdf)).

Analiza je rađena samo posmatranjem sopstvene sesije, u granicama Distillovih uslova korišćenja. Svaki nalaz nosi oznaku:

- **POSMATRANO:** vidi se u snimku ili na stranici.
- **(zaključak):** tumačenje zasnovano na dokazima.
- **NEPOZNATO:** ne može se utvrditi spolja.

## Šta je REA

REA („Reverse Engineer Anything”) je MCP server i alat za komandnu liniju koji AI agentu, ovdje Claude Code-u, daje alate za reverse inženjering. Otvorenog je koda, pod licencom MIT. Zvanični izvori su samo `github.com/morluto/rea`, `rea.tools` i npm paket `rea-agents`.

REA analizira programe, JavaScript i Electron aplikacije, Android, sajtove, snimljeni mrežni saobraćaj (HAR), baze i drugo. Svaki nalaz vraća sa dokazom i razdvaja ono što je posmatrano od onoga što je zaključeno.

Za web aplikaciju kao što je Distill važne su tri sposobnosti:

| Sposobnost | Alat | Šta radi |
| --- | --- | --- |
| Posmatranje stranice | `inspect_web_page` | Pasivno se prikači na već otvoren Chrome i zapiše stanje stranice: skripte, skladište, service worker i mrežu. Ne klikće, ne navigira i ne izvršava kod. |
| Snimljeni saobraćaj | `inspect_web_network_capture`, `inspect_analysis_view` | Čita HAR fajl i izvlači domene, API pozive, zaglavlja i oblik odgovora. |
| Analiza JavaScript-a | `analyze_javascript_application` | Čita JavaScript aplikacije bez pokretanja. Na Distillu nije korišćena (vidi Obim rada i pravila). |

## Obim rada i pravila

Granicu postavljaju dva dokumenta:

- **Uslovi korišćenja Distilla, §2.1:** zabranjuju reverse inženjering, dekompilaciju, otkrivanje algoritama i sigurnosno testiranje servisa. Nalog je probni nalog na lično ime, pa ovi uslovi važe.
- **REA DISCLAIMER:** REA ne pomaže u zaobilaženju zaštite, prijave i kontrole pristupa, ni u kopiranju tuđeg koda. Za dozvole i poštovanje uslova korišćenja odgovoran je korisnik.

Zato je rad ograničen na pasivno posmatranje sopstvene sesije:

| Rađeno | Nije rađeno |
| --- | --- |
| Normalno korišćenje aplikacije kao prijavljen korisnik | Analiza, dekompilacija ili rekonstrukcija njihovog JavaScript koda |
| HAR snimak saobraćaja sopstvene sesije (tri stranice) | Ponavljanje zahtjeva ka njihovom API-ju ili Supabase-u |
| Pasivni pregled otvorene stranice alatom REA | Probanje zaštite, prijave ili ograničenja |
| Imena kolačića u DevTools-u, bez vrijednosti | Bilo kakav automatizovan saobraćaj ka Distillu |
| Javni izvori: sajt, OpenAPI, spisak servisa, DNS, zaglavlja mejlova | |

## Instalacija

- REA je instaliran komandom `npx --yes rea-agents@latest setup`, uz izbor Claude Code-a i skill-a `reverse-engineer-anything`. Instalirana je verzija `rea-agents` 6.8.0.
- Alati za analizu programa (Hopper, Ghidra, IDA) nisu instalirani, jer za web ne trebaju.
- Provjera: `claude mcp list` prikazuje `rea` kao povezan.
- Preduslov je Node 22.23.4 ili noviji. Na računaru je Node 24.22.1.
- Uz instalaciju je napravljena rezervna kopija podešavanja Claude Code-a (`.claude.json.rea.backup`).

## Proba na sopstvenom sajtu

Prije Distilla, cio postupak je isproban na sopstvenom sajtu za izvještaje, gdje nema nikakvih ograničenja.

- **Pasivni pregled:** REA se prikačio na Chrome sa portom za debug i zapisao stranicu: oko 50 elemenata, bez skripti, prazno skladište i bez mrežnih zahtjeva poslije prikačivanja.
- **HAR:** REA je pročitao snimak i našao jedan zahtjev (odgovor 304, `Server: SimpleHTTP/0.6 Python/3.14.9`, bez bezbjednosnih zaglavlja).

Pouke za Distill:

- HAR snimati sa uključenim „Disable cache”, da se dobiju puni odgovori (200) sa svim zaglavljima, a ne 304.
- Pasivni pregled vidi stanje tek od trenutka prikačivanja, pa za mrežu treba HAR.
- REA strogo provjerava HAR: Chrome je zapisao IPv6 adresu `[::1]` u obliku koji standard ne prihvata, pa je REA radio nad ispravljenom kopijom.

## Primjena na Distill

1. Chrome je pokrenut sa portom za debug (9222) i posebnim profilom, odvojenim od svakodnevnog browsera, a u Distill je urađena obična prijava.
2. HAR snimak je napravljen sa uključenim „Preserve log” i „Disable cache”, na tri stranice: Latest news, stranica NIS-a i jedan izvještaj. Izvoz je „sanitized”, pa Chrome sam izbacuje kolačiće i zaglavlja za prijavu. Ukupno 216 zahtjeva za oko dva minuta.
3. REA je pokrenut u Claude Code-u, uz pisana pravila: bez analize JavaScript-a, bez zahtjeva ka Distillu, bez navigacije i bez ispisa tokena, kolačića i mejlova.
   - HAR: `inspect_web_network_capture` i pregledi `summary` i `api-surface`.
   - Stranica: `inspect_web_page`, pasivno, bez izvornog koda skripti.
   - Zaglavlja i imena polja: lokalna skripta nad kopijom HAR-a, bez mreže.
4. Imena kolačića (bez vrijednosti) pročitana su ručno u DevTools-u, jer ih „sanitized” HAR ne sadrži.
5. Čišćenje: odjava iz Distilla u posebnom profilu i zatvaranje tog Chrome-a. HAR je čuvan samo lokalno, van repoa.

**Zaštita podataka.** Prva verzija fajla sa nalazima je, uprkos pravilima, sadržala nizove nalik tokenu i mejl adresu. Ručna provjera (pretraga „eyJ” i „@”) ih je otkrila prije dijeljenja. Claude Code ih je zatim sakrio i ponovo provjerio fajl: 0 tokena, 0 mejlova. Oznaka Supabase projekta iz imena kolačića se namjerno ne navodi.

## Nalazi

| # | Nalaz | Oznaka |
| --- | --- | --- |
| 1 | Web aplikacija je SvelteKit sa renderovanjem na serveru, a hostuje se na Vercel-u. | POSMATRANO |
| 2 | Ispred aplikacije nema Cloudflare-a, iako je Cloudflare na Distillovom spisku servisa kao WAF. Gdje se Cloudflare koristi, nije poznato. | POSMATRANO / NEPOZNATO |
| 3 | U snimku browser ne zove ni Supabase ni javni API. Podaci stižu od SvelteKit servera kao `__data.json`, sa brojevima kao ID-jevima. Javni API (ID-jevi `comp_art_…`) je poseban ulaz za programe. | POSMATRANO / (zaključak) |
| 4 | Prijava ide preko Supabase Auth: kolačić `sb-…-auth-token`, HttpOnly, Secure, SameSite=Lax. | POSMATRANO |
| 5 | Analitika je OpenPanel na njihovom domenu `dstl.in` i pri identifikaciji dobija i mejl korisnika. Postoji i sopstveno brojanje pregleda kompanija (`/a7s/company-page-view`). | POSMATRANO / (zaključak) za ime |
| 6 | U snimku nema Google Analytics-a, PostHog-a, Sentry-ja, Intercom-a ni drugih skripti trećih strana; sve skripte su sa njihovog domena. | POSMATRANO |
| 7 | Ikonice izvora dolaze sa Google-ovog servisa, a slike članaka direktno sa sajtova izdavača, pa i oni vide šta korisnik gleda. | POSMATRANO / (zaključak) |
| 8 | Podaci otkrivaju funkcije koje se u probnom nalogu ne vide: zakazani izvještaji, API ključevi, timovi, Slack i Teams, praćenje industrija. | POSMATRANO (imena polja) |
| 9 | Aplikacija redovno provjerava da li postoji nova verzija (`/_app/version.json`). To je jedno moguće objašnjenje povremene greške 500 koja nestane kad se stranica osvježi. | POSMATRANO / (zaključak) |
| 10 | Zaglavlja: HSTS i CSP samo sa `frame-ancestors`; nema X-Content-Type-Options, Referrer-Policy ni Permissions-Policy. Nema source map-a ni service worker-a. | POSMATRANO |

## Arhitektura u četiri dijela

Nalazi su složeni u četiri dijela po C4 modelu. Dijagrami su u tehničkoj dokumentaciji ([`tehnicka-dokumentacija.pdf`](tehnicka-dokumentacija.pdf)), a ovdje je kratak opis svakog dijela.

### Kontekst

Distill je jedna kutija: koriste ga ljudi preko browsera i programi preko API-ja, vijesti uzima iz kanala kompanija i medija, a oslanja se na iznajmljene servise. Za dva servisa nije potvrđeno mjesto ili ime: Cloudflare i AI servis.

### Kontejneri

Kroz istu bazu (Supabase) prolaze tri toka: korisnik dobija stranice od web aplikacije na Vercel-u, obrada vijesti puni bazu, a zakazani poslovi iz nje šalju mejlove preko Resend-a. API je poseban ulaz za programe, uz Bearer ključ.

### Model podataka

Prava šema baze nije javna, pa je model izveden iz javnog OpenAPI-ja i imena polja koja aplikacija dobija. Organizacija posjeduje watchliste, teme i izvještaje, a vijesti pripadaju kompanijama i temama. Tri vrste vijesti imaju svoje oznake ID-ja: `comp_upd_`, `comp_art_` i `top_art_`.

### Učitavanje stranice

Prijava daje kolačić sesije, a svaku stranicu browser traži od SvelteKit servera. Koraci sa Supabase-om nisu u snimku, nego su zaključak. Analitika i brojanje pregleda kompanija idu odvojeno, a provjera nove verzije se ponavlja dok je stranica otvorena.

## Šta ostaje nepoznato i zašto

- AI model, algoritmi (ocjena važnosti, spajanje vijesti, sažimanje) i šema baze rade na serveru. Browser dobija samo gotove rezultate, pa ih ne otkriva ni HAR ni pregled stranice. **NEPOZNATO**
- Dublja analiza web aplikacije, koja nije rađena zbog §2.1, ne bi dala te odgovore, jer se oni u kodu koji stiže u browser ne nalaze. Za njih bi trebao pristup serveru ili podaci od samog Distilla. **(zaključak)**
- Gdje se koristi Cloudflare i na kom serveru radi analitika ostaje otvoreno. To se može provjeriti javnim DNS zapisima.

## Iskustva sa alatom

- **Prednosti:** REA se drži pravila (radi pasivno, ne izvršava kod), svaki nalaz ima dokaz i jasno razdvaja posmatrano, zaključeno i nepoznato. Pregled `api-surface` brzo daje spisak poziva aplikacije.
- **Stroga provjera HAR-a:** i na Distillu je Chrome-ov HAR odbijen (šest zapisa sa vremenom malo ispod nule, greška zaokruživanja). REA je radio nad ispravljenom kopijom, a original je ostao netaknut.
- **„Sanitized” HAR je bezbjedniji, ali skriva kolačiće.** Imena kolačića zato treba pročitati u DevTools-u, bez vrijednosti.
- **Pregledi ne prikazuju zaglavlja i tijela odgovora.** Za to je korišćena lokalna skripta koja ispisuje samo imena polja.
- **Izlaz agenta treba uvijek ručno provjeriti** na tokene i mejlove prije dijeljenja, bez obzira na pravila u zadatku.

## Zaključak

REA je samo pasivnim posmatranjem sopstvene sesije potvrdio od čega je Distillova web aplikacija sastavljena: SvelteKit na Vercel-u, prijava i baza na Supabase-u, analitika OpenPanel, a javni API je poseban ulaz za programe. Ono što Distill čini vrijednim, AI model i algoritmi obrade vijesti, radi na serveru i spolja se ne vidi, ni ovim ni bilo kojim drugim alatom. Alat je pouzdan za ovakav posao, ali njegov izlaz uvijek treba provjeriti na lične podatke prije dijeljenja.

## Izvori

- [REA na GitHub-u](https://github.com/morluto/rea): README, DISCLAIMER i vodiči `browser-observation`, `web-network-captures`, `javascript-application-workflows` i `installation`.
- [Distill: uslovi korišćenja](https://www.distillintelligence.com/terms-of-service) (§2.1).
- [Distill: spisak servisa](https://www.distillintelligence.com/subprocessors).
- [Distill: javni OpenAPI](https://api.distillintelligence.com/openapi.json).
- Snimak sopstvene sesije i nalazi REA. HAR se ne dijeli, jer sadrži lične podatke.
