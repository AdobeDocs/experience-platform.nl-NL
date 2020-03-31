---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Platform-API's verifiëren en openen
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

---


# Platform-API&#39;s verifiëren en openen

Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaaraccount om aanroepen uit te voeren naar Experience Platform-API&#39;s.

## Verifiëren om API-aanroepen te maken

Om de beveiliging van uw toepassingen en gebruikers te garanderen, moeten alle aanvragen voor Adobe I/O-API&#39;s worden geverifieerd en geautoriseerd aan de hand van standaarden zoals OAuth en JSON Web Tokens (JWT). JWT wordt dan gebruikt samen met cliënt specifieke informatie om uw persoonlijk toegangstoken te produceren.

Deze zelfstudie behandelt de stappen van authentificatie door het creëren van een toegangstoken die in het volgende stroomschema wordt geschetst:
![](images/authentication/authentication-flowchart.png)

## Vereisten

Om met succes vraag aan het Platform APIs van de Ervaring te maken, vereist u het volgende:

* Een IMS-organisatie met toegang tot het Adobe Experience Platform
* Een geregistreerd Adobe-id-account
* Een beheerder van de Console Admin om u als **ontwikkelaar** en een **gebruiker** voor een product toe te voegen.

In de volgende secties vindt u instructies voor het maken van een Adobe-id en het wordt een ontwikkelaar en gebruiker voor een organisatie.

### Een Adobe-id maken

Als u geen Adobe-id hebt, kunt u er een maken door de volgende stappen uit te voeren:

1. Ga naar [Adobe I/O-console](https://console.adobe.io)
2. Klik op Een nieuw account **maken**
3. Voltooi het aanmeldingsproces


### Word een ontwikkelaar en gebruiker voor het Platform van de Ervaring voor een organisatie

Voordat u integraties maakt voor Adobe I/O, moet uw account ontwikkelaarsmachtigingen voor een product in een IMS-organisatie hebben. Gedetailleerde informatie over ontwikkelaarsaccounts in de beheerconsole vindt u in het [ondersteuningsdocument](https://helpx.adobe.com/enterprise/using/manage-developers.html) voor ontwikkelaars.

**Toegang voor ontwikkelaars verkrijgen**

Neem contact op met een beheerder van de beheerconsole in uw organisatie om u via de [beheerconsole](https://adminconsole.adobe.com/)toe te voegen als ontwikkelaar voor een van de producten van uw organisatie.

![](images/authentication/assign-developer.png)

De beheerder moet u als ontwikkelaar toewijzen aan ten minste één productprofiel om door te gaan.

![](images/authentication/add-developer.png)

Als u eenmaal als ontwikkelaar bent toegewezen, hebt u toegangsrechten om integraties te maken voor [Adobe I/O](https://console.adobe.io/). Deze integraties vormen een pijplijn van externe apps en services naar de Adobe API.

**Toegang tot gebruikers verkrijgen**

De beheerder van de beheerconsole moet u ook als gebruiker aan het product toevoegen.

![](images/authentication/assign-users.png)

Net als bij het toevoegen van een ontwikkelaar moet de beheerder u toewijzen aan ten minste één productprofiel om door te gaan.

![](images/authentication/assign-user-details.png)


## Eenmalige installatie

De volgende stappen hoeven slechts eenmaal te worden uitgevoerd:

* Aanmelden bij Adobe I/O-console
* Integratie maken
* Toegangswaarden voor Omlaag kopiëren

Zodra u uw integratie en toegangswaarden hebt, zult u hen voor authentificatie in de toekomst kunnen opnieuw gebruiken. Elke stap wordt hieronder in detail behandeld.

### Aanmelden bij Adobe I/O-console

Ga naar [Adobe I/O-console](https://console.adobe.io/) en meld u aan met uw Adobe-id.

Nadat u zich hebt aangemeld, klikt u op het tabblad **Integraties** boven aan het scherm. Een integratie is een de dienstrekening die voor de geselecteerde IMS Organisatie wordt gecreeerd. U mag alleen oproepen naar de IMS-organisatie waarin de integratie is gemaakt.

>[!NOTE]
>Als uw account aan meerdere organisaties is gekoppeld, kunt u in het keuzemenu rechtsboven in het scherm gemakkelijk tussen de organisaties schakelen.

### Integratie maken

Klik op de pagina **Integraties** op **Nieuwe integratie** om het proces te starten. Het proces bestaat uit drie stappen:
* Type integratie kiezen
* Kies welke Adobe-service u wilt integreren
* Integratiedetails, openbare sleutel en productprofiel toevoegen

![](images/authentication/integrations.png)

#### Type integratie kiezen

In het volgende scherm wordt u gevraagd of u toegang wilt krijgen tot een API of gebeurtenissen in real-time wilt ontvangen. Selecteer **Toegang tot API** en **ga dan verder**.

![](images/authentication/create-new-integration.png)

#### Kies welke Adobe-service u wilt integreren

Als uw account aan meerdere IMS-organisaties is gekoppeld, kunt u tussen deze organisaties schakelen via het keuzemenu rechtsboven. Selecteer **Workshop** en **Experience Platform API** onder **Adobe Experience Platform** voor toegang tot de API&#39;s.

![](images/authentication/integration-select-service.png)

Klik op **Doorgaan** om naar de volgende sectie te gaan.

#### Integratiedetails, openbare sleutel en productprofiel toevoegen

In het volgende scherm wordt u gevraagd uw integratiegegevens in te vullen, uw openbare-sleutelcertificaat in te voeren en een productprofiel te selecteren.

![](images/authentication/integration-details.png)

Voer eerst uw integratiegegevens in. Selecteer vervolgens een productprofiel. De profielen van het product verlenen korrelige toegang tot een groep eigenschappen die tot de dienst behoren die u in vorige stappen selecteerde.

Voor de certificaatsectie moet u een certificaat genereren:

**Voor Mac OS- en Linux-platforms:**

Open de opdrachtregel en voer de volgende opdracht uit:

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**Voor Windows-platforms:**

1. Een open client downloaden om openbare certificaten te genereren (bijvoorbeeld de [OpenSl-vensterclient](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip))

1. Extraheer de map en kopieer deze naar C:/libs/ locatie.

1. Opdrachtregelprompt openen en de volgende opdrachten uitvoeren:

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

U krijgt een antwoord dat lijkt op het volgende: u wordt gevraagd om informatie over uzelf in te voeren:

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

Nadat u de gegevens hebt ingevoerd, worden twee bestanden gegenereerd: `certificate_pub.crt` en `private.key`.

>[!NOTE]
>`certificate_pub.crt` verloopt over 365 dagen. U kunt de periode langer maken door de waarde van `days` in het `openssl` bevel hierboven te veranderen, maar het roteren van geloofsbrieven periodiek is een goede veiligheidspraktijk.

Het `private.key` zal worden gebruikt om onze JWT in de recentere sectie te produceren.

De sleutel `certificate_pub.crt` wordt gebruikt om een API-sleutel te maken. Ga terug naar de Adobe I/O-console en klik op **Selecteer een bestand** om uw `certificate_pub.crt` bestand te uploaden.

Klik op Integratie **** maken om het proces te voltooien.

### Toegangswaarden naar beneden kopiëren

Nadat u de integratie hebt gemaakt, kunt u de details ervan bekijken. Klik op **Clientgeheim** ophalen en uw scherm ziet er ongeveer als volgt uit:

![](images/authentication/access-values.png)

Kopieer de waarden voor `{API KEY}`, `{IMS ORG}` namelijk de organisatie-id, en `{CLIENT SECRET}` zoals deze in de volgende stap worden gebruikt.

## Verificatie voor elke sessie

De laatste stap bestaat uit het genereren van uw API-aanroepen `{ACCESS_TOKEN}` die u wilt gebruiken voor verificatie. Het toegangstoken moet worden opgenomen in de machtigingheader van elke API-aanroep naar het Adobe Experience Platform. Toegangstokens verlopen na 24 uur, waarna nieuwe tokens moeten worden gegenereerd om de API&#39;s te kunnen blijven gebruiken.

### JWT maken

Navigeer in de detailpagina van uw integratie in de Adobe I/O-console naar het **tabblad JWT** :

![](images/authentication/generate-jwt.png)

Op de pagina wordt u gevraagd de pagina in te voeren die `private.key` u in de vorige sectie hebt gemaakt. Open de opdrachtregel om de inhoud van het `private.key` bestand weer te geven:

```shell
cat private.key
```

Uw uitvoer ziet er ongeveer als volgt uit:

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

Kopieer de volledige uitvoer en plak deze in het tekstveld en klik vervolgens op **JWT** genereren. Kopieer de gegenereerde JWT-code naar beneden voor de volgende stap.

![](images/authentication/generated-jwt.png)

### Toegangstoken genereren

U kunt een toegangstoken door een cURL bevel produceren. Als u geen cURL hebt geïnstalleerd, kunt u het installeren gebruikend `npm install curl`. Meer informatie over cURL [vindt u hier](https://curl.haxx.se/)

Nadat cURL is geïnstalleerd, moet u de velden in de volgende opdracht vervangen door uw eigen opdracht `{API_KEY}`, `{CLIENT_SECRET}`en `{JWT_TOKEN}`:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

Als dit lukt, ziet de uitvoer er ongeveer als volgt uit:

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

Uw toegangstoken is de waarde onder de `access_token` sleutel. Deze toegangstoken `expires_in` 86399947 milliseconden (24 uren). Daarna, zult u een nieuw toegangstoken moeten produceren door de zelfde stappen hierboven te volgen.

U kunt nu API-aanvragen indienen in het Adobe Experience Platform.

### Toegangscode testen

Om te testen of uw toegangstoken geldig is, kunt u proberen om de volgende API vraag te maken. Deze vraag zal van alle klassen binnen de `global` container een lijst maken:

>[!NOTE]
>`{API_KEY}` en `{IMS_ORG}` raadpleeg de waarden die u hierboven hebt gegenereerd.

**Verzoek**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


Als uw reactie vergelijkbaar is met de hieronder weergegeven reactie, `access_token` is uw reactie geldig en werkt u. (Deze reactie is afgebroken voor de ruimte.)

**Antwoord**

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Postman gebruiken voor JWT-verificatie en API-aanroepen

[Postman](https://www.getpostman.com/) is een populair hulpmiddel om met RESTful APIs te werken. In dit [standaardbericht](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wordt beschreven hoe u een postman kunt instellen om automatisch JWT-verificatie uit te voeren en deze te gebruiken voor het gebruik van Adobe Experience Platform-API&#39;s.