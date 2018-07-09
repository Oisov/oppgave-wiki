

# Git for viderekommende

## Introduksjon 

Når du leser dette avsnittet her så antar jeg at du allerede kan bruke Git, og 
at du har opprettet pull requests før. Dersom dette er ukjent så anbefaler jeg 
deg å lese hvordan-komme-i-gang-med-github, som forklarer alle disse tingene.

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
