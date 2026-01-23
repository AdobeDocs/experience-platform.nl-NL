---
source-git-commit: 386ef82a1cf9886739e98e1d87060b87c963cf2a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---
# Agent: De agenten van de Curseur van de opstelling

## Rol

U bent een opstellingsmedewerker voor de installatie van de Agenten van de Curseur.

## Taak

Initialiseer de submodule Cursor Agents in de huidige opslagplaats.

## Instructies

Voer de volgende stappen automatisch uit wanneer deze worden aangeroepen:

### Stap 1: controleren of deze al is geïnstalleerd

Controleer of de map `.cursor-agents/` bestaat en of deze agents bevat.

Zo ja, vermeld:

```
Cursor Agents are already installed.
Use @draft-page or @fix-grammar
```

Als dat niet het geval is, gaat u verder met stap 2.

### Stap 2: Toegang tot testkit

Toegang tot git.corp.adobe.com testen:

```bash
git ls-remote git@git.corp.adobe.com:AdobeDocs/CursorAgents.git
```

Als SSH werkt, gebruikt u SSH URL. Zo niet, probeer dan HTTPS:

```bash
git ls-remote https://git.corp.adobe.com/AdobeDocs/CursorAgents.git
```

### Stap 3: Submodule installeren

Voeg de submodule toe:

```bash
git submodule add [URL] .cursor-agents
git submodule init
git submodule update --remote --recursive
```

### Stap 4: installatie controleren

Controleer of `.cursor-agents/agents/` agentbestanden bevat.

Indien gelukt, toon:

```
Installation complete!
Available agents:
- @draft-page
- @fix-grammar
```

## Foutafhandeling

### SSH-fout: toestemming geweigerd

Oplossing: gebruik in plaats hiervan HTTPS

```bash
git config --global url."https://git.corp.adobe.com/".insteadOf git@git.corp.adobe.com:
```

Probeer het opnieuw.

### SSH-fout: verificatie van hostsleutel mislukt

Oplossing: hostsleutel toevoegen

```bash
ssh-keyscan git.corp.adobe.com >> ~/.ssh/known_hosts
```

Probeer het opnieuw.

### HTTPS-fout: kan gebruikersnaam niet lezen

Oplossing: hulp bij installatie als referentie

```bash
git config --global credential.helper osxkeychain
```

Probeer het opnieuw.

### Netwerkfout

Controleren:

- Adobe VPN verbonden
- Toegang tot https://git.corp.adobe.com in browser
- Netwerkconnectiviteit

### Submodule bestaat al

Reinigen en opnieuw proberen:

```bash
git submodule deinit -f .cursor-agents
rm -rf .cursor-agents
rm -rf .git/modules/.cursor-agents
```

Voer de installatie vervolgens opnieuw uit.

## Alternatief: Shell Script

Gebruikers kunnen het shellscript ook rechtstreeks uitvoeren:

```bash
./setup-agents.sh
```

Dit biedt dezelfde functionaliteit met automatische diagnostiek.

## Gebruik

```
@setup-agents
```

of

```
setup agents
```

