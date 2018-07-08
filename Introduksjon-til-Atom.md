<p align="center">
<a href="https://atom.io/">
<img border="0" alt="W3Schools" src="/images/atom/Atom_icon.svg" width="480">
</a>
</p>



# Introduksjon

En av de beste editorene å begynne å skrive oppgaver med er Atom. Fordelene er
blant annet at det er svært enkelt å skreddersy for den enkelte, samt at Atom
tilbyr sømløs integrasjon med Git og Markdown. Det aller beste er imidlertid at
Atom er relativt enkelt å komme i gang med! Hva venter du på? La oss sette i
gang.

![Bilde av atom i bruk](/images/atom/atom-faktisk-jobbing.png)

## Installasjon

### Windows

Naviger deg seg til [Atoms hjemmeside](https://atom.io/). Her vil du få opp en
lenke du kan trykke på for å laste ned programmet.

### Linux

**Ubuntu:** Først må vi skaffe Atoms installasjonsfiler. Her kan du enten
navigere deg til [Atoms kodelager på
git](https://github.com/atom/atom/releases/tag/v1.28.0) og laste ned
`atom-amd64.deb` DEB pakken. Alternativt er det like greit å bruke `wget` i
terminalen til å hente nyeste versjon:

    $ wget -O atom-amd64.deb https://atom.io/download/deb

Den enkleste måten å installere DEB filer er ved å installere `gdebi` kommandoen

    sudo apt install gdebi-core

og installere filen ved å kjøre

    sudo gdebi atom-amd64.deb

Nå er du klar til å kjøre

    atom

enten fra terminalen eller startmenyen.

**Fedora:** Her er installasjonen litt enklere. Last ned RPM-versjonen fra
[Atoms kodelager på git](https://github.com/atom/atom/releases/tag/v1.28.0) via
`wget` som forklart tidligere. Deretter installerer du den ved å bruke
kommandoen

    sudo dnf install ./atom.x86_64.rpm

**Arch Linux:** Atom ligger i AUR så bruk den AUR-hjelperen du vil, for
eksempel

    yaourt -S atom

## Grunnleggende bruk

Første gang du åpner Atom vil det se ut som dette:

![Bilde av startskjermen til Atom](/images/atom/atom-intro.png)

Her har du to faner med en rekke nyttige knapper til høyre. Det går helt fint å
bruke Atom uten å måtte lære seg noen rare hurtigtaster. Likevel vil jeg på det
sterkeste anbefale deg å bli kjent med hurtigtasten `ctrl + shift + P`. Denne
hurtigstasten åpner opp `Atoms Palette`, som er en meny hvor du kan søke etter
alt som finnes i Atom. Dersom du lurer på hvordan noe gjøres i Atom bør det
første steget alltid være å søke i denne menyen.

![Bilde av Atoms
Palette](/images/atom/atom-quick-menu.png)

## Installasjon av pakker

Det første vi må gjøre er å installere _git_-pakken og en enkel _terminal_. Ved
å trykke på "Install a package" i bildet ovenfor åpner følgende meny seg:

![Bilde som viser hvordan du kan installere pakker i
Atom](/images/atom/atom-package.png)

Ved å trykke på "Open installer" kan vi installere de pakkene som trengs.
Alternativt kunne vi ha brukt hurtigtasten `ctrl + ,` for å navigere direkte til
innstillinger. Det er også mulig å bruke hurtigsøket via `ctrl + shift + P` og
søke etter `packages`. Vi trenger pakkene

- Git-plus

- Platformio-ide-terminal

![Bilde av installasjonsvinduet for
git-plus-pakken](/images/atom/atom-git-plus.png)

![Bilde av installasjonsvinduet for
atom-terminalen](/images/atom/atom-terminal.png)

For å bruke terminalen må du bare trykke på `+`-ikonet som befinner seg nede i
venstre hjørne:

![Bilde som viser hvordan Atom ser ut med terminalen
installert](/images/atom/atom-terminal-2.png)

### Vårt første prosjekt

Vi er nå klare til å åpne vårt første prosjekt. Har du husket å opprette en fork
av kodeklubbens oppgavesamling? Hvis ikke kan du lese raskt over dette i
[introduksjonen til Git](../pages/guide_bruk_git.md).

I dette steget skal vi se på hvordan vi kan laste ned (i git-språk å _clone_)
forken din. Dersom du allerede har gjort dette kan du trygt hoppe videre til
neste steg. Det finnes flere måter å gjøre dette uten å måtte forlate Atom.

Vi kan bruke hurtigmenyen `ctrl + shift + P` og søke etter `clone`.
Da vil du få opp følgende meny

![Bilde av vinduet for å klone et repo til datamaskinen
din](/images/atom/atom-clone.png)

Hvor du bytter ut BRUKERNAVN med brukernavnet ditt på GitHub. Du kan selvsagt
bestemme selv hvor du vil lagre prosjektet ditt.

Alternativt kan vi bruke terminalen vi nettopp installerte. Pass på at du er navigert til mappen du ønsker å lagre prosjektet i. Hvis ikke må du skrive `cd MAPPEPLASSERING`. Åpne terminalen ved å trykke på `+` nede til venstre. Skriv inn

    git clone git@github.com:BRUKERNAVN/oppgaver.git

![Bilde som viser hvordan terminalen kan brukes til å klone et repo til
datamskinen
din](/images/atom/atom-clone-terminal.png)

Obs! Det kan være du får noen feilmeldinger enten at du ikke har riktige
rettigheter eller at du ikke har valgt Git-brukernavn og epost. For å løse disse
problemene henviser jeg igjen til [introduksjonen til
Git](../pages/guide_bruk_git.md).

Nå som vi har klart å laste ned Kodeklubbens oppgavesamling kan vi åpne mappen
som et nytt prosjekt. Her kan vi velge en av disse to fremgangsmåtene:

- søke etter `Project` på Kodeklubbens nettside og trykke på `Open Project` i
  menyen til høyre.

- velge `Add Project Folder` fra `fil`-menyen.

![Skjermbilde av Atom i
bruk](/images/atom/atom-faktisk-jobbing.png)

Bildet over viser en fil under behandling i prosjektet. Før vi gjør endringer i
en fil bør vi bytte til en ny _branch_, eller gren, slik at arbeidet er mer
oversiktlig. Igjen så kan dette gjøres enkelt fra hurtigmenyen

![Bilde som viser søk etter "branch" i hurtigmenyen i
Atom](/images/atom/atom-branch-git.png)

eller ved å åpne terminalen og skrive

    git checkout -b NAVN_PÅ_NY_BRANCH

Hvilken gren jeg er på kan en alltid se nede i høyre hjørne i Atom. Når en er
ferdig med å jobbe er det på tide å lagre arbeidet sitt, samt å laste det opp
til sin egen fork. Du kan godt bruke GitHub-fanen som åpnes via `ctrl + shift +
9`. Denne finner du også gjennom hurtigmenyen hvis du søker etter "github tab".
Som vanlig kan du også bruke terminalen til alt dersom du foretrekker det.

## Noen tips og triks

Den vanlige konvensjonen når en koder, og som vi bruker her også, er at hver
linje maksimalt skal være 80 tegn. Dette gjør at utformingen av koden blir mer
uniform når en har mange bidragsytere, men og at koden er mer lesbar. Den
vertikale streken du ser når du skriver kode er nettopp satt til 80 tegn, slik
at du alltid ved hvilke linjer som er for lange. På bildet under ser du at linje
28 strekker seg over 3 linjer, og dette forteller Atom deg med prikkene i stedet
for linjenumre til venstre.

![Bilde av en for lang linje med tekst i
Atom](/images/atom/atom-long-line.png)

Heldigvis har Atom en pakke kalt `autoflow`. Det eneste formålet til denne
pakken er å bryte lange linjer. Den er installert som standard, flaks! For å
formatere et langt avsnitt er det nok å ha markøren inne i avsnittet og trykke
`ctrl + shift + Q`.

![Bilde av en lang tekst i Atom som er delt på flere
linjer](/images/atom/atom-long-line-fixed.png)

En annen hurtigtast du gjerne kan gjøre deg kjent med er `ctrl + shift + T`. Den
gjør at du kan søke gjennom prosjektet ditt etter relevante filer, i stedet for
å måtte navigere gjennom mappehierarkiet til venstre.

![Bilde av søkefunksjonen i
Atom](/images/atom/atom-quick-search.png)

En annen hurtigtast som er nyttig er `ctrl + shift + M`. Den gjør at du får opp
en ny fane der du ser hvordan Markdown-filen din ser ut i sanntid.

### Utseende

Det er og fullt mulig å endre utseende til Atom ved å laste ned nye temaer,
eller bruke noen av de som ligger inne fra før. For å endre tema kan vi enten
søke etter `themes` i hurtigmenyen eller direkte bruke `ctrl + ,` for å hoppe
til innstillinger. Menyen ser slik ut

![Bilde av temainnstillinger i
Atom](/images/atom/atom-themes.png)

**UI:** _Perfect Dark_, **Syntax:** _Perfect Dark_

![Bilde av Atom med Perfect
dark-temaet](/images/atom/atom-jobbing-perfect-dark.png)

**UI:** _Perfect Dark_, **Syntax:** _Solarized Dark_

![Bilde av Atom med Solarized
dark-temaet](/images/atom/atom-jobbing-perfect-dark-solarized.png)

Det er og mulig å laste ned egne temaer fra nettet, for eksempel Dracula-temaet
som er vist under.

**UI:** _Perfect Dark_, **Syntax:** _Dracula_

![Bilde av Atom med
Dracula-temaet](/images/atom/atom-jobbing-perfect-dark-dracula.png)
