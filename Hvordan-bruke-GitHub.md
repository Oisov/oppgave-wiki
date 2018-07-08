
[[/images/git/github-logo.png|Github sin logo]]


# Hvordan bruke GitHub?

For å laste opp oppgaver til [kidsakoder.no](http://oppgaver.kidsakoder.no)
bruker vi GitHub, ofte bare kalt Git. Dette er programvare som gir flere brukere
muligheten til å jobbe i et prosjekt samtidig, laste opp hver sine deler, og så
sette alt sammen til ett felles prosjekt.

Vi kan bruke ordtaket "jo flere kokker jo mer søl" når vi jobber med en side som
Kodeklubbens nettside. Tenk på nettsiden som en stor kake som mange flittige
kokker jobber sammen om å lage. Dersom du begynner å endre direkte på kaken kan
det hende du endrer noe de andre kokkene var veldig fornøyde med, eller kanskje
du ved et uhell brukte et kilo pepper i stedet for en teskje. For å hindre disse
uhellene bruker vi _versjonskontroll_.

Helt enkelt fungerer det slik at du lager en kopi av prosjektet på Internett, og
så en lokal kopi på datamaskinen din. Så deler du prosjektet opp i flere stykker
du kan jobbe på individuelt. Du gjør forbedringene på en liten bit først, og så
kan du be en administrator i Kodeklubben om å bytte ut den tilsvarende biten i
det opprinnelige prosjektet med den du har forbedret. Det kan hende du får
beskjed om å gjøre noen mindre endringer, men så vil en del av Kodeklubbens
prosjekt være forbedret med dine endringer.

## Oppsummering

Dette er ideen bak Git, og i praksis fungerer det slik: Det er en felles samling
av filer som nettsiden bygges opp av (her:
[github.com/kodeklubben](https://github.com/kodeklubben/oppgaver)). Dette kalles
et _repo_, kort for _repository_.

1. Hver bruker som ønsker å bidra lager en _fork_, sin egen kopi av _repo_-et.

2. Brukeren lagrer (kalt _clone_ på engelsk) sin _fork_ lokalt på sin
   datamaskin.

2. En bruker lager en _branch_ i sin egen _fork_, og bytter til den.

4. Brukeren gjør endringer i en eller flere filer, eller legger til noe helt nytt.

3. Brukeren kan _commit_-e endringer gjort i en _branch_,

6. Når du er ferdig med å _commit_-e kan du _push_-e endringene til Internett for
   å gjøre den klar for deling med resten.

6. Brukeren legger inn en _pull request_ (ofte forkortet PR) og ber om at
   endringene hun har gjort lokalt blir _merge_-t med _repo_-et.

  [[/images/git/git_workflow.png|Oversikt over arbeidsflyt med Git]]

8. Alle kan se og kommentere på _PR_-en, før en administrator kan _merge_ filene.

9. Endringene som brukeren gjorde i sin _branch_ er nå en del av _repo_-et.

## Komme i gang med Git

- [ ] Du må ha en bruker på [github.com](www.github.com).

- [ ] Last ned [Git](https://git-scm.com/downloads) til datamaskinen din.

- [ ] Du trenger en [skrivebordsklient av Git](https://desktop.github.com/).

- [ ] Du trenger en editor å jobbe i, for eksempel [Atom](https://atom.io/) (for
      en grunndigere innføring se [[introduksjon til Atom]]).

Gå til [Kodeklubbens GitHub](https://github.com/kodeklubben/oppgaver), og klikk
`fork` oppe i høyre hjørne. Da får du laget din egen kopi som du finner igjen på
din egen github-side.

[[/images/git/create_fork.png|Skjermdump som viser hvor fork-knappen er]]

Åpne GitHub Desktop og logg inn. Klikk `clone repository` og velg oppgave-repoet
du kopierte fra Kodeklubben. Da laster du ned en kopi av denne til datamaskinen
din. Det er denne vi skal jobbe i videre. Merk deg hvor denne blir lagret!

[[/images/git/clone_repository.png|Skjermdump som viser hvordan clone repository ser ut]]

## Arbeidsflyt

Her beskriver vi arbeidsflyten i Git.

### Lage en branch

For hver ting du vil gjøre i Git er det ryddig å lage en ny _branch_. Dette er
en uavhengig del av din egen _fork_ du kan jobbe i. Endringer du gjør her
påvirker ikke andre _branch_-es du har laget, og heller ikke
`master`-_branch_-en din før du er klar for at den skal gjøre det. Den bør ha et
beskrivende navn på stikkordsform, for eksempel navnet på oppgaven du skal
skrive. Slik blir det enklere for deg å holde styr på endringene du gjør, og det
er enklere for den som skal se over og _merge_ å kontrollere at ting er gjort
riktig.

Du kan trykke `ctrl + shift + N` for å lage en ny _branch_. Hvis du foretrekker
klikk og skriv kan du finne `Branch` i menylinjen øverst og velge `New
branch...`. Skriv inn navnet og klikk `Create branch`. Pass på at nye
_branch_-er lages ut fra `master`, slik at du alltid tar utgangspunkt i det som
faktisk er den oppdaterte versjonen i _repo_-et.

Nå er du klar til å opprette eller endre filer. Åpne tekstbehandlingsprogrammet
du vil jobbe i, for eksempel [Atom](guide_bruk_atom.md). Der kan du legge til
`oppgaver`-mappa, som er den lokale kopien av _fork_-en din, som et prosjekt. Da
har du alle mappene og filene du vil jobbe med lett tilgjengelig.

### Lage en ny oppgave

Oppgavene er sortert etter kodespråk. For eksempel ligger Scratch-oppgaven
"Astrokatt" i

```
oppgaver/src/scratch/astrokatt
```

sammen med alle tilhørende filer og alternative språk oppgaven er tilgjengelig
på. For å skrive helt nye oppgaver lager du en ny mappe. Den skal ha samme navn
som filen du skriver oppgaven i, noe kort og beskrivende. Pass på å ikke bruke
mellomrom, men du kan markere orddeling med understrek.

Husk å lagre filene dine! Det er alltid kjedelig å miste arbeid du har gjort
fordi du glemte å lagre. Før du kan gå videre på neste steg må alle filene du
vil sende fra _branch_-en din være lagret.

### Push og pull request

Når du har lagret en ny fil i en _branch_ vil du _commit_-e den slik at den
legges til lokalt, og _push_-e for å sende den til _fork_-en din. Det gjør du i
GitHub Desktop.

Til venstre har du en oversikt over alle filene som er endret i _branch_-en du
jobber i. Nederst er en boks der du kan skrive et sammendrag av hva du har
gjort, for eksempel `Laget ny oppgave om en katt i verdensrommet`. Om du ønsker
å skrive litt mer kan du gjøre det i boksen under. Trykk `Commit to [navn på
branch]` og vent til det er gjort.

Så trykker du `ctrl + P` for å _push_-e. Hvis du foretrekker å klikke kan du
finne `Branch`i menylinjen og velge `Push` eller bare trykke `Publish branch`
øverst i midten på skjermen. Nå blir det sendt til din _fork_ på nettet, og
sammenlignet med det originale _repo_-et.

Gå til [Kodeklubbens GitHub](https://github.com/kodeklubben/oppgaver). Der ser
du at det har kommet opp en ny linje om at du har noe å legge til denne
versjonen. Til høyre er det en grønn knapp med `Create pull request`. Trykk på
denne. Du blir sendt videre til en PR der teksten du skrev for _commit_-en din
er lagt inn allerede. Denne kan du endre eller la stå som den er. Rull deg ned
til du finner en grønn knapp med `Create pull request` igjen og trykk på den.

Du har sendt en PR til _repo_-et! Nå er det bare å vente til en administrator
kommenterer eller godkjenner. Om du ikke har slått det av får du e-postvarsel,
så du trenger ikke følge med selv.

