

# Den gode oppgaven

Når du skriver en oppgave som skal legges ut på oppgavesidene må du følge denne
malen. Slik blir utformingen på oppgavene mest mulig lik. 
Leser du [[stilguiden for kode og tekst|Stilguide-for-kode-og-tekst]] 
ser du hvordan vi ønsker at markdown-koden skal skrives.

Rammen for oppgaven er en YAML-header, altså informasjon _om_ oppgaven,
oppgaveteksten med figurer, og en lærerveiledning som forklarer _hvordan_ en
klasse kan jobbe med oppgaven.

Når du har skrevet ferdig en oppgave med riktig formatering kan du sende den inn
til oppgaverepoet på Github. Se [[Hvordan bruke GitHub|Komme-i-gang-med-Git]].

## YAML-header

For å markere YAML-headeren bruker vi `---` før og etter. I YAML-headeren skal
følgende være med:

- [ ] Tittel på oppgavene.

- [ ] Navn på den som har skrevet oppgaven, eventuelt hvem som skrev den
  originalt.

- [ ] Anbefalt nivå (introduksjon-begynner-erfaren-ekspert).

- [ ] Språk
  ([ISO 639-1](https://no.wikipedia.org/wiki/Liste_over_ISO_639-1-koder)).

Et eksempel på YAML-header blir da

```
---
title: Astrokatt
level: 1
author: 'Geir Arne Hjelle'
language: nb
---
```

Hvis du ønsker å dele oppgaven med en annen lisens enn det som er standard (CC
BY-SA 4.0), så må du skrive `lisens: 'lisenstype'`, der _lisenstype_ er den
lisensen du ønsker å dele med, i YAML-headeren.

## Oppgaveteksten

Det er vanlig med en introduksjon som forklarer hva formålet med oppgaven er. I
denne passer det å skrive hva som skal programmeres og litt historie dersom
målet er å reprodusere et kjent spill. Ta gjerne med et bilde som viser hvordan
det vil se ut til slutt. Husk å skrive en bildetekst for brukere som ikke ser
bildet.

```
# Introduksjon {.intro}

Katten vår har så lyst å være en astronaut, la oss se om vi kan hjelpe ham?
Underveis vil vi lære hvordan vi flytter figurer rundt på skjermen, og hvordan
katter blir påvirket av gravitasjonskreftene fra jorden.

![Bilde av en katt i verdensrommet](astrokatt.png)
```

Merk at bildet `astrokatt.png` ligger i samme mappe som oppgaveteksten.

### Stegene

En god oppgave bygges i steg, slik at vi gjør en del om gangen. Det gjør det
enklere å holde styr på hvor langt brukeren har kommet i progammeringen, og gir
en mulighet for å sjekke om alt så langt er forstått.

Hvert steg skal inneholde en sjekkliste med ting som skal gjøres i rekkefølge.
De kan gjerne ha følge av forklarende tekst, spørsmål og lignende.

```
# Steg 1: Dette er starten på noe stort {.activity}

Her legger vi grunnlaget for det vi skal programmere.

- [ ] Start et nytt prosjekt i Scratch.

- [ ] Legg inn en ny figur.

Du kan prøve å flytte den nye figuren rundt på skjermen.
```

I tillegg til selve oppgaveteksten kan du legge til utfordringer `{.challenge}`,
tips `{.protip}` eller ting å prøve ut `{.try}`. Til slutt i hvert steg bør du
ha med en test av det som er gjort så langt, merket med `{.flag}`.

### Nivå

Det er viktig at vi informerer om hvilket nivå oppgaven er på. Det gir en idé
til både den som skal gjøre oppgaven og eventuell lærer/veileder om oppgaven
egner seg for den enkelte. Her finner du beskrivelsen som er lagt til grunn for
nivåinndelingen vår.

- `level: 1` **introduksjonsoppgave**: Alle uten programmeringskunnskap burde ha
  mulighet til å følge oppgaven. Oppgaven burde være selvstendig, slik at man
  ikke trenger å sjekke opp andre ressurser for tilleggsinformasjon. Oppgaven
  kan gjerne ha kodeblokker som det ikke er meningen at eleven skal forstå, men
  som viser hva som er mulig i programmeringsspråket. Kodeblokker kan gjerne
  være fullstendige, slik at kopier og lim inn er tilstrekkelig for å komme seg
  gjennom oppgaven.

- `level: 2` **nybegynner**: Det antas at eleven kan bruke editoren og vet
  hvordan koden kjøres. Bygg opp meget enkle utfordringer med nesten identiske
  eksempler, slik at eleven ikke setter seg fast, samt at man unngår passiv
  kopiering og lim inn.

- `level: 3` **erfaren**: Eleven kan lage program og kjøre dem. Eleven kan løse
  enkle problemer på egen hånd. Hjelp eleven å løse middels vanskelige problemer
  med lignende eksempler. Link gjerne til eksterne ressurser som API i
  `## Utfordring {.challenge}`, slik at eleven blir flink til å utforske.

- `level: 4` **ekspert**: Eleven kan løse middels vanskelige problemer på egen
  hånd. Hjelp eleven til å løse vanskelige problemer ved å foreslå søkeord og
  linke til offisielle API-ressurser. Ikke gi kode som løser oppgaven uten
  redigering.

### Oppmuntringer og tips

Det er mange plasser det går an å kjøre seg fast når man programmerer. Selv om
du kan det du holder på med vil en nybegynner ha behov for mange vink i riktig
retning. Tenk gjennom hvilket nivå oppgaven skal være for! Er det en
ekspertoppgave kan du kanskje droppe noen av tipsene og kodeeksemplene, mens i
en nybegynneroppgave må du skrive nesten all koden slik at brukeren kan
sammenligne sin egen kode med noe som helt sikkert fungerer.

## Lærerveiledning

I tillegg til oppgavene ønsker vi å ha lærerveiledninger til hver enkelt. Denne
kan inneholde mer informasjon om hva som må gjøres på forhånd, anbefalt
aldersnivå og så videre. Dersom du har gjort deg erfaringer med hvor brukerne
møter motstand i oppgaven, så kan du skrive hvordan du løste det.

Dessuten ønsker vi å informere om eventuelle kompetansemål i læreplanene som kan
oppfylles ved hjelp av hver enkelt oppgave. Det skrives i lærerveiledningen. Se
[[Hvordan skrive en lærerveiledning]] for mer informasjon.
