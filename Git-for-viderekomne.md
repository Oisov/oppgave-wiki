
<p align="center">
<img border="0" alt="git alt logo"
src="https://github.com/Oisov/oppgave-wiki/blob/master/images/git-viderekomne/git-internal-logo" 
height="200">
</p>


# Git for viderekomne

## Introduksjon

Når du leser dette avsnittet antar vi at du allerede kan bruke Git, og at du har
opprettet pull requests før. Dersom dette er ukjent anbefaler vi at du leser
[[Komme-i-gang-med-Git]], som forklarer alle disse tingene.

Her skal vi se hvordan vi kan bruke Git fra terminalen, og hvordan vi løser noen
vanlige problemer som kan dukke opp.

## Din identitet

Den første tingen du må gjøre etter du har installert Git er å sette
brukernavnet og e-postadressen din. Dette er viktig fordi hver *commit* bruker
denne informasjonen som en digital signatur.

[[/images/git-viderekomne/git-username.png|Hva som skjer når du ikke setter brukernavn]]

Å sette brukernavn og e-post kan gjøres slik:

    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com

Du trenger bare å gjøre dette en gang når vi bruker `--global`, fordi dette gjør
at Git alltid bruker denne informasjonen, uavhengig av hvilket prosjekt du
arbeider med. Dersom du ønsker å bruke et annet navn eller e-postadresse for et
spesifikt prosjekt kan du gjøre det ved å kjøre kommandoen ovenfor uten
`--global` når du er i mappen til prosjektet.

Mange av de grafiske verkøyene for å bruke Git hjelper deg med å sette
identiteten din første gang du starter programmet.

## SSH

Å skrive inn passord og brukernavn hver gang du skal pushe endringer til GitHub
kan bli slitsomt i lengden. Ved å bruke SSH kan du slippe unna ved å gi
datamaskinen din tilgang til å bruke GitHub-profilen din.

Når du setter opp SSH vil du generere en SSH-nøkkel og legge denne til i
`ssh-agent` og på GitHub-kontoen din. Når du legger nøkkelen til i `ssh-agent`
forsikrer vi oss om at nøkkelen har litt ekstra sikkerhet gjennom et passord.

### Generere SHH-nøkler

Før du genererer nye nøkler kan du sjekke om det ligger noen eksisterende i
systemet. Dette steget er strengt tatt ikke nødvendig, men om du ønsker kan du
kjøre

    ls -al ~/.ssh

i terminalen. Om det ligger noen nøkler der fra før vil de ende på `.pub`.
Sannsynligvis ligger det ingen der fra før. Dersom det gjør det kan du hoppe
videre til neste steg.

1. Åpne terminalen (for eksempel Git Bash)

2. Lim inn teksten under, men legg inn din egen e-postadresse (som du bruker på
  GitHub).

        ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

  Dette genererer en ny SSH-nøkkel, og bruker e-postadressen som vannmerke.

        Generating public/private rsa key pair.

3. Når du blir spurt om å "Enter a file in which to save the key" trykk Enter.
   Da bruker du standardplasseringen.

        Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]

4. Nå får du opp valg om å skrive inn et passord. Du kommer til å måtte skrive
inn dette passordet hver gang du skal pushe endringer til GitHub. Det er mulig å
la det være tomt om du vil. For enkelhets skyld kan du bruke et kort og enkelt
passord her.

        Enter passphrase (empty for no passphrase): [Type a passphrase]
        Enter same passphrase again: [Type passphrase again]!

### Legge til de genererte nøklene til `ssh-agent`

1. Start `ssh-agent` i terminalen.

          eval "$(ssh-agent -s)"
        Agent pid 59566

2. Legg til din private SSH-nøkkel til `ssh-agent`. Dersom du har generert en
   nøkkel med et annet navn, eller dersom du legger til en eksistererende nøkkel
   med et annet navn, erstatt `id_rsa` i kommandoen ovenfor med navnet på din
   private nøkkel.

        ssh-add ~/.ssh/id_rsa

### Legg til SSH-nøkkelen til GitHub-kontoen din

1. Den enkleste måten å kopiere nøkkelen til utklippstavlen direkte fra
kommandolinjen. Hvordan dette gjøres varierer hårfint basert på plattformen du
bruker

| *Linux*                     | *Mac*                        | *Windows*                  |
| -------------               | -------------                | ---                        |
| `xclip < ~/.ssh/id_rsa.pub` | `pbcopy < ~/.ssh/id_rsa.pub` | `clip < ~/.ssh/id_rsa.pub` |

På Linux må du sannsynligvis installere `xclip` manuelt, for eksempel med `sudo
apt-get install xclip` om du sitter på en Ubuntu-basert distro.

**Tips:** Dersom dette ikke fungerer kan du navigere deg til den hemmelige
`.shh` mappen, åpne mappen i din favoritt-editor, og så kopiere teksten til
utklippstavlen.

2. Øverst på GitHub-nettsiden finner du profilbildet ditt, trykker på det og
velger "*Settings*".

  [[/images/git-viderekomne/userbar-account-settings.png|Authentication keys]]

3. I sidemenyen på brukeren din velger du **SSH and GPG keys**.

  [[/images/git-viderekomne/settings-sidebar-ssh-keys.png|Authentication keys]]

4. Klikk **New SSH key** eller **Add SSH key**.

  [[/images/git-viderekomne/ssh-add-key.png|SSH Key button]]

5. I "*Title*"-feltet skriver du et beskrivende navn for den nye nøkkelen. Hvis
du bruker din personlige Mac kan du for eksempel kalle den "Min MacBook Air".

6. Lim inn nøkkelen din inn i "*Key*"-feltet.

  [[/images/git-viderekomne/ssh-key-paste.png|The Add key button]]

7. Klikk **Add SSH key**

  [[/images/git-viderekomne/ssh-add-key.png|Sudo mode dialog]]

8. Nå dukker det kanskje opp en meldingsboks som ber deg bekrefte
GitHub-passordet ditt.

  [[/images/git-viderekomne/sudo-mode-popup.png|Sudo mode dialog]]

# Grunnleggende Git fra terminalen

Igjen ser vi på [[oppsumeringen av hvordan Git
fungerer|Komme-i-gang-med-Git#oppsummering]], men denne gangen skal vi se
hvordan hvert steg kan gjøres direkte fra terminalen. Vi deler det i to steg:

## Hvordan sette opp Git første gang.

1. Hver bruker som ønsker å bidra lager en _fork_, sin egen kopi av _repo_-et.

2. Brukeren lagrer (kalt _clone_ på engelsk) sin _fork_ lokalt på sin
   datamaskin.

        git clone git@github.com:BRUKERNAVN/oppgaver.git

    Her bruker vi SSH-lenken og ikke HTTP-lenken fra GitHub. Da kan vi bruke
    passordet knyttet til SSH-nøkkelen i stedet for brukernavn og passord når vi
    vil pushe endringer til _fork_-en.

    Så legger vi inn Kodeklubbens _repo_ som `upstream`. Dette kan du tenke på
    som en forelder til vår egen _fork_.

        git remote add upstream git@github.com:kodeklubben/oppgaver.git

    Dette er nødvendig slik at det er enkelt å holde vår egen _fork_ oppdatert
    med Kodeklubbens _repo_ senere.

## Daglig bruk

1. En bruker lager en _branch_ i sin egen _fork_, og bytter til den.

        git checkout -b NAVN_PÅ_NY_BRANCH

   Alternativt om du ønsker å bytte til en eksisterende _branch_ skriver du

        git checkout NAVN_PÅ_EKSISTERENDE_BRANCH

2. Brukeren gjør endringer i en eller flere filer, eller legger til noe helt
   nytt. Ønsker du å sjekke hvilke endringer som er gjort, og eventuelt hvilke
   filer som er _staget_, kan du skrive

        git status

3. Brukeren kan _commit_-e endringer gjort i en _branch_,

  Før du er klar til å _commit_-e endringene må du legge dem til i _commit_-en.
  For eksempel

        git add NY_FIL.md

  Her er det mye forskjellig du kan gjøre. Du kan bruke `git add .` for å legge
  til alle filer. Koden `git add *.md` vil legge til alle `.md`-filer. Når du
  har _staget_ de riktige filene skriver du

        git commit -m "MELDING"

    En god melding forklarer i en kort setning hvilke endringer som er gjort.

4. Når du er ferdig med å _commit_-e kan du _push_-e endringene til Internett
for å gjøre den klar for deling med resten.

        git push -u <remote> <branch>

   Hvor `remote` som regel er `origin` om du ikke har gjort noen vesentlige
   endringer, mens `branch` er grenen du har _commit_-et til.

5. Brukeren legger inn en _pull request_ (ofte forkortet PR) og ber om at
   endringene hun har gjort lokalt blir _merge_-t med _repo_-et.

Bildet under illustrerer arbeidsflyten i Git mellom din datamaskin, og din
_fork_.

[[/images/git-viderekomne/git_workflow_detailed.png|Detaljert arbeidsflyt]]

Det er også mulig å _unstage_ en fil ved å bruke `git checkout FILNAVN`.

## Hvordan holde forken oppdatert

Som forklart i stegene for å sette opp Git for første gang, så må vi først passe
på at Kodeklubbens repo ligger inne som `remote` med

    git remote add upstream git@github.com:kodeklubben/oppgaver.git

**Merk:** Det er i utgangspunktet ingenting spesielt med navnet *upstream*, og
vi kunne for eksempel ha brukt *kodeklubben* eller noe lignende i stedet.
Konvensjonen er dog å kalle _repo_-et du har laget en _fork_ fra for
*upstream*.

Nå kan vi hente inn endringene som eventuelt er gjort på Kodeklubbens _repo_,
men som enda ikke ligger i _repo_-et vårt:

    git fetch upstream

Etter vi har hentet inn endringene kan vi flette sammen vår lokale mappe med
endringene som er gjort på Kodeklubbens _repo_

    git merge upstream/master

Til slutt kan vi dytte disse endringene opp på vår _fork_ på nettet

    git push

[[/images/git-viderekomne/git.png|Viser eksempel på git i praksis]]


# Noen tips og triks

**Endringer på master branch:** Anta at du har begynt å endre en fil før du har
byttet til riktig gren. Dette er heldigvis relativt enkelt å fikse. Først må du
bruke `add` for å legge til endringene dine til _staging area_. Tenk på dette
området som en pose som du fyller med filene dine. Deretter bruker vi

    git stash

for å lukke denne posen med filer slik at vi kan ta den med oss. Deretter bytter
vi til riktig _branch_

    git checkout branch_name

Før vi kan slippe ut inneholdet i posen på den nye _branch_-en.

    git stash pop

Du kan i utgangspunktet ha så mange poser eller staging areas _stashed_ som du
vil. Ved å bruke `pop` så slipper du ut den siste du tok inn.

**Branch i Branch:** Husk å *alltid bytte til master før du oppretter nye
branches*! Det kan ofte gå raskt i svingene og du kan ende opp med branches
inni branches. Dette skaper ofte mye hodebry. Da er det enkleste om du bare lagrer endringene du har gjort utenfor prosjektet, og så slette branchen med

    git branch -d branch_name

Pass på at du faktisk er på _master branch_

    git checkout master

før du oppretter den nye branchen

    git checkout -b branch_name

Til slutt kan du lime inn endringene du lagret utenfor prosjektet.

Dette kan løses direkte med Git ved å bruke en kombinasjon av `git rebase` og
`git push -f`, men det er mer avansert enn nivået denne guiden sikter på.
