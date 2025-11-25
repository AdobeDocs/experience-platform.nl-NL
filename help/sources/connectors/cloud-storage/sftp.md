---
title: Overzicht SFTP Source-connector
description: Leer hoe u een SFTP-server verbindt met Adobe Experience Platform via API's of de gebruikersinterface.
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
source-git-commit: 06db0d3023ebf26aa604880fb6b614e331b1b2ea
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# SFTP-aansluiting

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Lees dit document voor de vereiste stappen die u moet uitvoeren om uw [!DNL SFTP] -account met Experience Platform te kunnen verbinden.

>[!TIP]
>
>U moet de Interactieve Authentificatie van het Toetsenbord in de de serverconfiguratie van SFTP onbruikbaar maken alvorens te verbinden. Als u de instelling uitschakelt, kunnen wachtwoorden handmatig worden ingevoerd in plaats van via een service of programma.

## Vereisten {#prerequisites}

Lees deze sectie voor de vereiste stappen die u moet voltooien om de [!DNL SFTP] -bron met succes aan te sluiten op Experience Platform.

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

### Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

* Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
* De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
* De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
* De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
* Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [ RFC 2616, Sectie 2.2: BasisRegels ](https://www.ietf.org/rfc/rfc2616.txt) en [ RFC 3987 ](https://www.ietf.org/rfc/rfc3987.txt).
* De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

### Een Base64-gecodeerde OpenSSH-privésleutel instellen voor [!DNL SFTP]

De [!DNL SFTP] -bron ondersteunt verificatie met behulp van de [!DNL Base64] -gecodeerde OpenSSH-persoonlijke sleutel. Zie de onderstaande stappen voor informatie over het genereren van uw Base64-gecodeerde OpenSSH-persoonlijke sleutel en het verbinden van [!DNL SFTP] met Experience Platform.

>[!BEGINTABS]

>[!TAB  Vensters ]

### [!DNL Windows] gebruikers

Als u een [!DNL Windows] machine gebruikt, open omhoog het **2} menu van het Begin {en selecteer dan** Montages **.**

![ montages ](../../images/tutorials/create/sftp/settings.png)

Van het **menu van Montages** dat verschijnt, uitgezochte **Apps**.

![ apps ](../../images/tutorials/create/sftp/apps.png)

Daarna, uitgezochte **Facultatieve eigenschappen**.

![ facultatief-eigenschappen ](../../images/tutorials/create/sftp/optional-features.png)

Er wordt een lijst met optionele functies weergegeven. Als **Cliënt OpenSSH** reeds vooraf geïnstalleerd in uw machine is, dan zal het in de **Geïnstalleerde 3} lijst van eigenschappen** Facultatieve eigenschappen **worden omvat.**

![ open-ssh ](../../images/tutorials/create/sftp/open-ssh.png)

Als niet geïnstalleerd, selecteer **installeer** en open dan **[!DNL Powershell]** en stel het volgende bevel in werking om uw privé sleutel te produceren:

```shell
PS C:\Users\lucy> ssh-keygen -t rsa -m pem
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\lucy/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\lucy/.ssh/id_rsa.
Your public key has been saved in C:\Users\lucy/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:osJ6Lg0TqK8nekNQyZGMoYwfyxNc+Wh0hYBtBylXuGk lucy@LAPTOP-FUJT1JEC
The key's randomart image is:
+---[RSA 3072]----+
|.=.*+B.o.        |
|=.O.O +          |
|+o+= B           |
|+o +E .          |
|.o=o  . S        |
|+... . .         |
| *o .            |
|o.B.             |
|=O..             |
+----[SHA256]-----+
```

Voer vervolgens de volgende opdracht uit terwijl u het bestandspad van de persoonlijke sleutel opgeeft om uw persoonlijke sleutel te coderen in [!DNL Base64] :

```shell
C:\Users\lucy> [convert]::ToBase64String((Get-Content "C:\Users\lucy\.ssh\id_rsa" -AsByteStream)) > "C:\Users\lucy\.ssh\id_rsa_base64"
```

Met de bovenstaande opdracht slaat u de [!DNL Base64] -gecodeerde persoonlijke sleutel op in het bestandspad dat u hebt toegewezen. Vervolgens kunt u die persoonlijke sleutel gebruiken om zich te verifiëren bij [!DNL SFTP] en verbinding te maken met Experience Platform.

>[!TAB  Mac ]

### [!DNL Mac] gebruikers

Als u a [!DNL Mac] gebruikt, open **Eind** en stel het volgende bevel in werking om de privé sleutel (in dit geval, zal de privé sleutel in `/Documents/id_rsa` worden bewaard) te produceren:

```shell
ssh-keygen -t rsa -m pem -f ~/Documents/id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/vrana/Documents/id_rsa.
Your public key has been saved in /Users/vrana/Documents/id_rsa.pub.
The key fingerprint is:
SHA256:s49PCaO4a0Ee8I7OOeSyhQAGc+pSUQnRii9+5S7pp1M vrana@vrana-macOS
The key's randomart image is:
+---[RSA 2048]----+
|o ==..           |
|.+..o            |
|oo.+             |
|=.. +            |
|oo = .  S        |
|+.+ +E . = .     |
|o*..*.. . o      |
|.o*=.+   +       |
|.oo=Oo  ..o      |
+----[SHA256]-----+
```

Voer vervolgens de volgende opdracht uit om de persoonlijke sleutel te coderen in [!DNL Base64] :

```shell
base64 ~/Documents/id_rsa > ~/Documents/id_rsa_base64
 
 
# Print Content of base64 encoded file
cat ~/Documents/id_rsa_base64
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUJGd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFRRUF0cWFYczlXOUF1ZmtWazUwSXpwNXNLTDlOMU9VYklaYXVxbVM0Q0ZaenI1NjNxUGFuN244CmFxZWdvQTlCZnVnWDJsTVpGSFl5elEzbnp6NXdXMkdZa1hkdjFjakd0elVyNyt1NnBUeWRneGxrOGRXZWZsSzBpUlpYWW4KVFRwS0E5c2xXaHhjTXg3R2x5ejdGeDhWSzI3MmdNSzNqY1d1Q0VIU3lLSFR5SFFwekw0MEVKbGZJY1RGR1h1dW1LQjI5SwpEakhwT1grSDdGcG5Gd1pabTA4Uzc2UHJveTVaMndFalcyd1lYcTlyUDFhL0E4ejFoM1ZLdllzcG53c2tCcHFQSkQ1V3haCjczZ3M2OG9sVllIdnhWajNjS3ZsRlFqQlVFNWRNUnB2M0I5QWZ0SWlrYmNJeUNDaXV3UnJmbHk5eVNPQ2VlSEc0Z2tUcGwKL3V4YXNOT0h1d0FBQThqNnF6R1YrcXN4bFFBQUFBZHpjMmd0Y25OaEFBQUJBUUMycHBlejFiMEM1K1JXVG5Rak9ubXdvdgowM1U1UnNobHE2cVpMZ0lWbk92bnJlbzlxZnVmeHFwNkNnRDBGKzZCZmFVeGtVZGpMTkRlZlBQbkJiWVppUmQyL1Z5TWEzCk5TdnY2N3FsUEoyREdXVHgxWjUrVXJTSkZsZGlkTk9rb0QyeVZhSEZ3ekhzYVhMUHNYSHhVcmJ2YUF3cmVOeGE0SVFkTEkKb2RQSWRDbk12alFRbVY4aHhNVVplNjZZb0hiMG9PTWVrNWY0ZnNXbWNYQmxtYlR4THZvK3VqTGxuYkFTTmJiQmhlcjJzLwpWcjhEelBXSGRVcTlpeW1mQ3lRR21vOGtQbGJGbnZlQ3pyeWlWVmdlL0ZXUGR3cStVVkNNRlFUbDB4R20vY0gwQiswaUtSCnR3aklJS0s3Qkd0K1hMM0pJNEo1NGNiaUNST21YKzdGcXcwNGU3QUFBQUF3RUFBUUFBQVFBcGs0WllzMENSRnNRTk9WS0sKYWxjazlCVDdzUlRLRjFNenhrSGVydmpJYk9kL0lvRXpkcHlVa28rbm41RmpGK1hHRnNCUXZnOFdTaUlJTk1oU3BNYWI1agpvWXlka2gvd0ovWElOaDlZaE5QVXlURi9NNkFnMkNYd21KS2RxN1VKWjZyNjloV3V0VVN6U05QbkVYWTZLc29GeVUwTEFvCko0OHJMT1pMZldtMHFhWDBLNUgzNmJPaHFXSWJwMDNoZk94eno5M0MrSDM5MFJkRkp4bzJVZ0FVY3UvdHREb0REVldBdmEKVkVyMWEzak9LenVHbThrK21WeXpPZERjVFY4ckZIT0pwRnRBU3l6Q24yVld1MjV0TWtrcGRPRjNKcVdMZHdOY3loeG1URApXZGVDNWh4V0Fiano0WDZ5WXpHcFcwTmptVkFoWUVVZGNBSVlXWWM3OGEvQkFBQUFnRm8wakl4aGhwZkJ6QjF6b09FMDJBClpjTC9hcUNuYysrdmJ1a2V0aFg5Zzhlb0xQMTQyeUgzdlpLczl3c1RtbVVsZ0prZURaN2hUcklwOGY2eEwzdDRlMXByY1kKb2ZLd0gwckNGOTFyaldPbGZOUmxEempoR1NTTEVMczZoNlNzMEdBQXE2Z0ZQTVF2dTB4TDlQUTlGQ21YZVVKazJpRm1MWgpEWWJGc0NyVUxEQUFBQWdRRGF0a1pMamJaSTBFM0ZuY2dTOVF5Y3lVWmtkZ1dVNjBQcG9ud3BMQXdUdHRpOG1EQXE5cHYwClEvUlk1WE9UeGF3VXNHa0tYMjNtV1BYR0grdUlBSzhrelVVM2dGM1dRWGVkTWw4NHVCVFZCTEtUdStvVVAvZmIvMEE0dE0KSE9BSythbXZPMkZuYzFiSmVwd05USTE2cjZXWk9sZWV2ZklJQVpXcEgxVVpIdkVRQUFBSUVBMWNwcStDNUVXSFJwbnVPZQpiNHE4T0tKTlJhSUxIRUN6U0twWlFpZDFhRmJYWlVKUXpIQU85YzhINVZMcjBNUjFkcW1ORkNja2ZsZzI2Y3BEUEl3TjBYCm5HMFBxcmhKbXp0U3ZQZ3NGdkNPallncXF6U0RYUjkxd1JQTEN5cU8zcGMyM2kzZnp2WkhtMGhIdWdoNVJqV0loUlFZVkwKZUpDWHRqM08vY3p1SWdzQUFBQVJkbkpoYm1GQWRuSmhibUV0YldGalQxTUJBZz09Ci0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

Nadat de door [!DNL Base64] gecodeerde persoonlijke sleutel is opgeslagen in de opgegeven map, moet u de inhoud van het bestand met de openbare sleutel toevoegen aan een nieuwe regel in de door de host geautoriseerde toetsen van [!DNL SFTP] . Voer de volgende opdracht uit op de opdrachtregel:

```shell
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

Om te bevestigen of uw openbare sleutel behoorlijk werd toegevoegd, kunt u het volgende op de bevellijn lopen:

```shell
more ~/.ssh/authorized_keys
```

>[!ENDTABS]

### Vereiste referenties verzamelen {#credentials}

U moet waarden opgeven voor de volgende referenties om uw [!DNL SFTP] -server te verbinden met Experience Platform.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Geef de juiste waarden op voor de volgende referenties om de [!DNL SFTP] -server te verifiëren met behulp van basisverificatie.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP-adres dat aan de [!DNL SFTP] -server is gekoppeld. |
| `port` | De [!DNL SFTP] serverpoort waarmee u verbinding maakt. Als deze waarde niet wordt opgegeven, wordt deze standaard ingesteld op `22` . |
| `username` | De gebruikersnaam met toegang tot de [!DNL SFTP] -server. |
| `password` | Het wachtwoord voor uw [!DNL SFTP] -server. |
| `maxConcurrentConnections` | Met deze parameter kunt u een maximumlimiet opgeven voor het aantal gelijktijdige verbindingen dat Experience Platform maakt wanneer verbinding wordt gemaakt met uw SFTP-server. U moet deze waarde instellen op een waarde die kleiner is dan de limiet die door SFTP is ingesteld. **Nota**: Wanneer dit het plaatsen voor een bestaande rekening van SFTP wordt toegelaten, zal het slechts toekomstige dataflows en niet bestaande dataflows beïnvloeden. |
| `folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. [!DNL SFTP] -bron, kunt u het mappad opgeven waarmee u gebruikerstoegang tot de submap van uw keuze kunt opgeven. |
| `disableChunking` | Tijdens gegevensinvoer kan de bron van [!DNL SFTP] eerst de lengte van het bestand ophalen, het bestand in meerdere delen verdelen en deze vervolgens parallel lezen. U kunt deze waarde in- of uitschakelen om op te geven of de [!DNL SFTP] -server de lengte van bestanden kan ophalen of gegevens kan lezen vanaf een specifieke verschuiving. |
| `connectionSpec.id` | (Alleen API) De verbindingsspecificatie retourneert de verbindingseigenschappen van een bron, inclusief verificatiespecificaties voor het maken van de basis- en bronverbindingen. De verbindingsspecificatie-id voor [!DNL SFTP] is: `b7bf2577-4520-42c9-bae9-cad01560f7bc` . |

>[!TAB  SSH openbare zeer belangrijke authentificatie ]

Geef de juiste waarden op voor de volgende referenties om uw [!DNL SFTP] -server te verifiëren met behulp van SSH-verificatie met openbare sleutels.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP-adres dat aan de [!DNL SFTP] -server is gekoppeld. |
| `port` | De [!DNL SFTP] serverpoort waarmee u verbinding maakt. Als deze waarde niet wordt opgegeven, wordt deze standaard ingesteld op `22` . |
| `username` | De gebruikersnaam met toegang tot de [!DNL SFTP] -server. |
| `password` | Het wachtwoord voor uw [!DNL SFTP] -server. |
| `privateKeyContent` | De Base64-gecodeerde inhoud van de privé sleutel van SSH. De ondersteunde OpenSSH-sleuteltypen zijn `ed25519` , `RSA` en `DSA` . |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |
| `maxConcurrentConnections` | Met deze parameter kunt u een maximumlimiet opgeven voor het aantal gelijktijdige verbindingen dat Experience Platform maakt wanneer verbinding wordt gemaakt met uw SFTP-server. U moet deze waarde instellen op een waarde die kleiner is dan de limiet die door SFTP is ingesteld. **Nota**: Wanneer dit het plaatsen voor een bestaande rekening van SFTP wordt toegelaten, zal het slechts toekomstige dataflows en niet bestaande dataflows beïnvloeden. |
| `folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. [!DNL SFTP] -bron, kunt u het mappad opgeven waarmee u gebruikerstoegang tot de submap van uw keuze kunt opgeven. |
| `disableChunking` | Tijdens gegevensinvoer kan de bron van [!DNL SFTP] eerst de lengte van het bestand ophalen, het bestand in meerdere delen verdelen en deze vervolgens parallel lezen. U kunt deze waarde in- of uitschakelen om op te geven of de [!DNL SFTP] -server de lengte van bestanden kan ophalen of gegevens kan lezen vanaf een specifieke verschuiving. |
| `connectionSpec.id` | (Alleen API) De verbindingsspecificatie retourneert de verbindingseigenschappen van een bron, inclusief verificatiespecificaties voor het maken van de basis- en bronverbindingen. De verbindingsspecificatie-id voor [!DNL SFTP] is: `b7bf2577-4520-42c9-bae9-cad01560f7bc` . |

>[!ENDTABS]

## SFTP verbinden met Experience Platform

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen een SFTP-server en Experience Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

* [Een SFTP-basisverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/sftp.md)
* [De gegevensstructuur en inhoud van een cloudopslagbron verkennen met behulp van de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
* [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### UI gebruiken

* [Een SFTP-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/sftp.md)
* [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
