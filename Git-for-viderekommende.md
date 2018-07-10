

# Git for viderekomne

## Introduksjon

Når du leser dette avsnittet her så antar jeg at du allerede kan bruke Git, og
at du har opprettet pull requests før. Dersom dette er ukjent så anbefaler jeg
deg å lese [[Hvordan-bruke-GitHub]], som forklarer alle disse tingene.

I denne artikkelen skal vi se hvordan vi kan bruke git fra terminalen, samt
hvordan løse noen vanlige problemer som kan dukke opp.

## Din identitet

Den første tingen du må gjøre etter du har installert Git er å sette
brukernavnet og e-postadressen din. Dette er viktig fordi hver *commit* bruker
denne informasjonen som en digital signatur.

[[/images/git-viderekommende/git-username.png|Hva som skjer når du ikke setter brukernavn]]

Å sette brukernavn og e-post kan gjøres slik:

    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com

Du trenger bare å gjøre dette en gang når vi bruker `--global` fordi da vil Git
alltid bruke denne informasjonen, uavhengig av hvilket prosjekt du arbeider med.
Dersom du ønsker å bruke et annet navn eller e-postadresse for ett spesifikt
prosjekt kan du gjøre dette ved å kjøre kommandoen ovenfor uten `--global` når
du er i mappen til prosjektet.

Mange av de grafiske verkøyene for å bruke Git hjelper deg med å sette
identiteten din første gang du starter programmet.

## SSH

Det å skrive inn passord og brukernavn hver gang du skal pushe endringer til
GitHub kan bli slitsomt i lengden. Ved å bruke SSH kan du slippe dette ved å
tillate at din datamaskin kan bruke din GitHub profil.

Når du setter opp SSH så vil du generere en SSH nøkkel og legge denne til i
`ssh-agent` og på din GitHub konto. Ved å legge til nøkkelen både til
`ssh-agent` forsikrer oss at nøkkelen din har litt ekstra sikkerhet igjennom en
passord.

### Generere SHH nøkkler

Før du genererer nye nøkkler kan du sjekke om det ligger noen eksisterende i
systemet. Dette steget er strengt talt ikke nødvendig, men om du ønsker kan du
kjøre

    ls -al ~/.ssh

i terminalen. Nøkklene vil da ende på `.pub` om det ligger noen der fra før,
sannsynligvis gjør det ikke det. Dersom det gjør det kan du hoppe videre til
neste steg.

1. Åpne Terminalen (f.eks Git Bash)

2. Lim inn teksten under, hvor du setter inn din egen GitHub e-postaddresse.

        ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

  Dette genererer en ny SSH-nøkkel, og bruker e-postaddressen som vannmerke.

        Generating public/private rsa key pair.

3. Når du blir spurt om å "Enter a file in which to save the key" trykk Enter.
   Da bruker man standardplasseringen.

        Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]

4. Nå får du opp valget å skrive inn ett passord. Merk at hver gang du skal
   pushe endringer til GitHub skriver du inn dette passordet, du kan også la
   dette feltet være tomt om du vil. Selv bruker jeg et kort og enkelt passord
   her.

        Enter passphrase (empty for no passphrase): [Type a passphrase]
        Enter same passphrase again: [Type passphrase again]!

### Legge til de genererte nøkklene til `ssh-agent`

1. Start `ssh-agent` i terminalen.

          eval "$(ssh-agent -s)"
        Agent pid 59566

2. Legg til din private SSH-nøkkel til `ssh-agent`. Dersom du har generert en
   nøkkel med et annet navn, eller dersom du legger til en eksistererende nøkkel
   med et annet navn, erstatt `id_rsa** i kommandoen ovenfor med navnet på din
   private nøkkel.

        ssh-add ~/.ssh/id_rsa

### Add the SSH key to your GitHub account.

1. Den enkleste måten å kopiere nøkkelen til utklippstavlen direkte fra
   kommandolinjen. Hvordan dette gjøres varierer hårint basert på platformen du
   bruker

| *Linux*                     | *Mac*                        | *Windows*                  |
| -------------               | -------------                | ---                        |
| `xclip < ~/.ssh/id_rsa.pub` | `pbcopy < ~/.ssh/id_rsa.pub` | `clip < ~/.ssh/id_rsa.pub` |

På Linux må du sannsynligvis installere `xclip` manuelt f.eks `sudo apt-get
install xclip` om du sitter på en Ubuntu basert distro.

**tips** Dersom dette ikke fungerer, kan du navigere deg til den hemmelige
`.shh` mappen, åpne mappen i din favoritt editor, også kopiere teksten til
utklippstavlen.


2. Øverst oppe på enhver GitHub side, trykk på profilbildet ditt, og velg
   "*Settings*".

  [[/images/git-viderekommende/userbar-account-settings.png|Authentication keys]]

3. På din bruker sin sidemeny, velg **SSH and GPG keys**.

  [[/images/git-viderekommende/settings-sidebar-ssh-keys.png|Authentication keys]]

4. Klikk **New SSH key** eller **Add SSH key**.

  [[/images/git-viderekommende/ssh-add-key.png|SSH Key button]]

5. I "*Title*" feltet, legg inn en beskrivende navn for den nye nøkkelen. For
   eksempel, dersom du bruker din personlige Mac, så kan du for eksempel kalle
   den "Min MacBook Air".

6. Lim inn nøkkelen din inn i "*Key*" feltet.

  [[/images/git-viderekommende/ssh-key-paste.png|The Add key button]]

7. Klikk **Add SSH key**

  [[/images/git-viderekommende/ssh-add-key.png|Sudo mode dialog]]

8. Nå dukker det kanskje opp en meldingsboks, som ber deg bekrefte GitHub
   passordet ditt.

  [[/images/git-viderekommende/sudo-mode-popup.png|Sudo mode dialog]]

# Grunnleggende git fra terminalen

La oss igjen se på [[oppsumeringen av hvordan git fungerer|Komme-i-gang-med-Git#oppsummering]], 
men denne gangen vil vi notere hvordan
hvert steg kan gjøres direkte fra terminalen. Vi deler det i to steg:

## Hvordan sette opp Git første gang.

1. Hver bruker som ønsker å bidra lager en _fork_, sin egen kopi av _repo_-et.

2. Brukeren lagrer (kalt _clone_ på engelsk) sin _fork_ lokalt på sin
   datamaskin.

        git clone git@github.com:BRUKERNAVN/oppgaver.git

    Her bruker jeg SSH lenken og ikke HTTP lenken fra GitHub, dette gjør at jeg
    kan bruke passordet knyttet til SSH-nøkkelen min, i stedet for brukernavn og
    passord når jeg ønsker å pushe endringer til _fork_en.

    Deretter legger vi inn Kodeklubbens repo som upstream (tenk på det som
    foreldre).

        git remote add upstream git@github.com:kodeklubben/oppgaver.git

    Dette er nødvendig slik at vi senere kan enkelt holde vår _fork_ oppdatert
    med Kodeklubbens repo.

## Daglig bruk

1. En bruker lager en _branch_ i sin egen _fork_, og bytter til den.

        git checkout -b NAVN_PÅ_NY_BRANCH

   Alternativt om du ønsker å bytt til en eksisterende branch skriver du

        git checkout NAVN_PÅ_EKSISTERENDE_BRANCH

2. Brukeren gjør endringer i en eller flere filer, eller legger til noe helt
   nytt.Ønsker du å sjekke hvilke endringer som er gjort, og eventuelt hvilke
   filer som er staget, kan du skrive

        git status

3. Brukeren kan _commit_-e endringer gjort i en _branch_,

  Før du er klar til å _commit_e endringene må du legge dem til i _commit_en.
  For eksempel

        git add NY_FIL.md

  Her er det mye forskjellig en kan gjøre f.eks kan en bruke `git add .` for å
  legge til alle filer. Mens `git add *.md` for eksempel legger til alle `.md`
  filer. Når du har staget de riktige filene skriver du

        git commit -m "MELDING"

    En god melding forklarer i en kort setning hvilke endringer som er gjort.

4. Når du er ferdig med å _commit_-e kan du _push_-e endringene til Internett for
   å gjøre den klar for deling med resten.

        git push -u <remote> <branch>

   Hvor `remote` som regel er `origin` om du ikke har gjort noen vesentlige
   endringer, mens `branch` er grenen du har commitet til.

5. Brukeren legger inn en _pull request_ (ofte forkortet PR) og ber om at
   endringene hun har gjort lokalt blir _merge_-t med _repo_-et.

Bildet under illustrerer arbeidsflyten i Git mellom din datamaskin, og din
_fork_.

[[/images/git-viderekommende/git_workflow_detailed.png|Detaljert arbeidsflyt]]

Selv om vi ikke har pratet om det kan det nevnes at dersom du ønsker å _unstage_
en fil, kan du bruke `git checkout FILNAVN` for å gjøre dette.

## Hvordan holde forken oppdatert

Som forklart i stegene for å sett opp git for første gang så må vi først passe
på at Kodeklubben repo ligger inne som `remote`

    git remote add upstream git@github.com:kodeklubben/oppgaver.git

**Merk:** det er i utgangspunktet ingenting spesielt med navnet *upstream** og vi
kunne for eksempel og kalt det for *kodeklubben* eller lignende. Konvensjonen er
dog å kalle repo'et du har laget en _fork_ fra for *upstream*.

Nå kan vi hente inn endringene som eventuelt er gjort på Kodeklubbens repo, men
som enda ikke ligger i vårt

    git fetch upstream

Etter vi har hentet inn endringene kan vi flette sammen vår lokale mappe med
endringene som er gjort på Kodeklubbens repo

    git merge upstream/master

Tilslutt kan vi dytte disse endringene opp på vår _fork_ på nettet

    git push

[[/images/git-viderekommende/git.png|Viser eksempel på git i praksis]]


# Noen tips og triks

**Endringer på master branch:** Anta at du har begynt å endre en fil før du har
byttet til riktig gren. Dette er heldigvis relativt enkelt å fikse. Først må du
bruke `add` for å legge til endringene dine til _staging area_. Tenk på dette
området som en pose som du fyller med filene dine. Deretter bruker vi

    git stash

for å lukke denne posen med filer å ta den med oss. Deretter bytter vi til
riktig branch

    git checkout branch_name

Før vi kan slippe ut inneholdet i posen på den nye grenen.

    git stash pop

Du kan i utgangspunktet ha så mange poser eller staging areas _stashed_ som du
vil. Ved å bruke `pop` så slipper du ut den siste du tok inn.

**Branch i Branch:** Husk og *alltid bytte til master før du oppretter nye
branches**! Det kan ofte gå raskt i svingene og du kan ende opp med branches
inni branches. Dette skaper ofte mye hodebry. Det beste er nok bare å lagre
endringene du har gjort utenfor prosjektet. Så sletter du branchen via

    git branch -d branch_name

Så passer du på at du faktisk er på _master branch_

    git checkout master

Før vi oppretter den nye branchen

    git checkout -b branch_name

Deretter kan vi lime inn endringene vi hadde lagret utenfor prosjektet. Selvsagt
kan dette også gjøres direkte fra git med å bruke en kombinasjon av `git rebase`
og `git push -f`, men favner videre enn hva denne guiden sikter på.
