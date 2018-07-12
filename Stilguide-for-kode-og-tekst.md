
<a href="https://xkcd.com/1513/">
<img border="0" alt="Tegneserie fra XKCD om konvensjoner og koding" src="https://github.com/Oisov/oppgave-wiki/blob/master/images/konvensjoner/xkcd.png">
</a>


# Stilguide for kode og tekst

## Hvorfor en stilguide?

Det er lettere å jobbe med kode (og tekst) som ser lik ut over hele prosjektet.
Dette er noe de fleste er enige om. Med en stilguide skriver vi dette ned, så vi
kan gjøre det samme alle sammen.

Vi kan også ta hensyn til at vi alle bruker forskjellige verktøy. For eksempel
er det mange som kjører verktøy i terminaler. Disse er typisk 80 tegn brede. Det
er derfor svært vanlig å bruke linjeskift (som vi setter inn med Enter) for å
holde linjebredden nede. Dette gjør det mer behagelig å redigere tekst i mange
editorer, og lettere å sammenlikne filer.

Stilguiden er lite streng. Du trenger ikke finkjemme stilguiden før du foreslår
noe. Om noe er viktig å få med seg, får du tilbakemelding på det når du legger
inn _pull request_.

## Hvorfor akkurat disse konvensjonene?

Konvensjonen under kan virke noe snodig til å begynne med, men det ligger en god
tanke bak. Hensikten bak disse konvensjonen er å gjøre koden enklere å lese
over; ved å dele inn teksten i naturlige blokker, samt gi koden litt mer
pusterom.


# Formatering av Markdown-filer

- Bruk `-` for punktlister.

- Bruk `- [ ]` for lister av sjekkpunkter.

- Bruk `1.`, `2.`, ... for lister av tall.

- Ha en tom linje mellom hvert punkt i en liste

- Ha én tom linje før og etter overskrifter.

- Unntaket er hovedoverskrifter (#) som bør ha _to_ tomme linjer før og en etter.

- Én tom linje på slutten av filen.

  Foretrukket:

  ```markdown
  _Her er slutten på forrige avsnitt._


  # Formatering av Markdown-filer

  ## Underoverskrift

  - Bruk `-` for punktlister

  - [ ] Første sjekkpunkt

  - [ ] Andre sjekkpunkt

  ```

  Ikke foretrukket:

  ```markdown
  _Her er slutten på forrige avsnitt._

  # Formatering av Markdown-filer
  ## Underoverskrift
  - Bruk `-` for punktlister
  ```

- Bryt avsnitt på 80 tegn.

  Foretrukket:

  ```markdown
  Stilguiden er lite streng. Du trenger ikke finkjemme stilguiden før du foreslår
  noe. Om noe er viktig å få med seg, får du tilbakemelding på det når du legger
  inn _pull request_.
  ```

  Ikke foretrukket:

  ```markdown
  Stilguiden er lite streng. Du trenger ikke finkjemme stilguiden før du foreslår noe. Om noe er viktig å få med seg, får du tilbakemelding på det når du legger inn _pull request_.
  ```

  - Automatisk brytning av linjer i Emacs: `M-q` eller `M-x auto-fill-mode`

  - Automatisk brytning av linjer i Atom: `C-S-q` med
    [Autoflow](https://github.com/atom/autoflow) (innebygget)

  - Automatisk brytning av linjer i Vim: `gqq`

## Tekstfiler generelt

Dette er typisk ting du kan sette opp teksteditoren din til å gjøre for deg.

- Bruk **mellomrom** til inntrykk heller enn tab

- Bruk **to mellomrom** for hvert nivå innrykk

- Avslutt filen med en tom linje

- Unngå mellomrom til høyre for teksten eller på tomme linjer
