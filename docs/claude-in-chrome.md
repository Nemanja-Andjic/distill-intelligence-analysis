# Claude in Chrome: instalacija i povezivanje sa Claude Code-om

Kratko uputstvo za issue #7. Claude in Chrome je dodatak za Chrome koji Claude Code-u omogućava da otvara stranice, klikće, čita ih i čita greške u konzoli.

## Upozorenja

- Dodatak radi u pravom Chrome-u, sa svim prijavama korisnika. Šta god korisnik može na sajtu na koji je prijavljen, može i Claude.
- Ne koristiti ga na banci, menadžeru lozinki, mejlu, u podešavanjima i tajnama na GitHub-u i na Cloudflare-u.
- Od Distilla se otvara samo javni sajt. Aplikacija i API se ne otvaraju preko Claude-a, jer Distillovi uslovi korišćenja (§2.1) zabranjuju reverse inženjering i sigurnosno testiranje.
- Dozvole se daju sajt po sajt, kad Claude pita. Stranica može imati skrivena uputstva za AI (*prompt injection*), pa ga treba slati samo na poznate sajtove.
- GIF i slika ekrana snime sve što se vidi, i podatke naloga. Pregledati ih prije objave.

## Šta treba

- Plan Pro, Max, Team ili Enterprise; Claude Code prijavljen claude.ai nalogom, ne API ključem.
- Google Chrome ili Microsoft Edge (radi i u drugim pregledačima zasnovanim na Chromium-u).
- Ekstenzija Claude in Chrome, verzija 1.0.36 ili novija.
- Ne radi u WSL-u.

## Instalacija

1. Instalirati ekstenziju sa [Chrome Web Store-a](https://chromewebstore.google.com/detail/claude/fcoeoabgfenejglbffodgkkbkcdhcgfn) (**Add to Chrome** → **Add extension**).
2. Prijaviti se u ekstenziji istim claude.ai nalogom i istom organizacijom kao u Claude Code-u (`/status`, red **Organization**).
3. U VS Code panelu ukucati `/chrome` i provjeriti stanje veze. Prekidač **Enabled by default** može ostati isključen.
4. Ako veza ne proradi odmah, zatvoriti sve prozore Chrome-a i otvoriti ga ponovo. Chrome tek tada pročita fajl za vezu (*native messaging host*).

Zadatak za pregledač počinje sa `@browser`:

```
@browser otvori code.claude.com/docs, klikni na polje za pretragu, ukucaj "hooks" i reci mi koji se rezultati pojave
```

Iz terminala se Claude Code sa pregledačem pokreće ovako:

```
claude --chrome
```

## Proba za #7

```
@browser otvori https://www.distillintelligence.com i opiši šta vidiš: glavne dijelove naslovne stranice i šta Distill nudi. Ostani samo na toj stranici: ne klikći Log in ni Sign up, ne otvaraj aplikaciju i ništa ne popunjavaj.
```

## Česti problemi

| Šta se vidi | Šta uraditi |
|---|---|
| „Not detected” u `/chrome` | U `chrome://extensions` provjeriti da je ekstenzija uključena. |
| „Browser extension is not connected” | Isti nalog i organizacija u ekstenziji i Claude Code-u; restart Chrome-a i VS Code-a; `/chrome` → **Reconnect extension**. |
| Alati prestanu da rade poslije pauze | `/chrome` → **Reconnect extension**. |
| „EADDRINUSE” na Windowsu | Zatvoriti ostale Claude Code sesije i restartovati. |

## Izvori

- [Use Claude Code with Chrome](https://code.claude.com/docs/en/chrome)
- [Use Claude Code in VS Code: Automate browser tasks with Chrome](https://code.claude.com/docs/en/vs-code#automate-browser-tasks-with-chrome)
