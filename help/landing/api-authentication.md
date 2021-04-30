---
keywords: Experience Platform;thuis;populaire onderwerpen;Authenticeren;toegang
solution: Experience Platform
title: API's van Experience Platforms verifiëren en benaderen
topic-legacy: tutorial
type: Tutorial
description: Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen uit te voeren naar Experience Platform-API's.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---


# API&#39;s van Experience Platforms verifiëren en openen

Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen uit te voeren naar Experience Platform-API&#39;s. Aan het eind van dit leerprogramma, zult u de volgende geloofsbrieven hebben geproduceerd die voor alle Platform API vraag worden vereist:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

Om de veiligheid van uw toepassingen en gebruikers te handhaven, moeten alle verzoeken aan Adobe I/O APIs voor authentiek worden verklaard en worden gemachtigd gebruikend normen zoals de Tokens van het Web OAuth en JSON (JWT). Een JWT wordt gebruikt samen met cliënt-specifieke informatie om uw persoonlijk toegangstoken te produceren.

In deze zelfstudie wordt uitgelegd hoe u de vereiste gegevens verzamelt om API-aanroepen van Platforms te verifiëren, zoals in het volgende stroomschema wordt beschreven:

![](./images/api-authentication/authentication-flowchart.png)

## Vereisten

Om met succes vraag aan Experience Platform APIs te maken, moet u het volgende hebben:

* Een IMS-organisatie met toegang tot Adobe Experience Platform.
* Een beheerder van de Admin Console die u als ontwikkelaar en gebruiker voor een productprofiel kan toevoegen.

U moet ook over een Adobe ID beschikken om deze zelfstudie te voltooien. Als u geen Adobe ID hebt, kunt u er een maken door de volgende stappen uit te voeren:

1. Ga naar [Adobe Developer Console](https://console.adobe.io).
2. Selecteer **[!UICONTROL Create a new account]**.
3. Voltooi het aanmeldingsproces.

## Verbeter ontwikkelaar en gebruikerstoegang voor Experience Platform

Voordat u integratie kunt maken in de Adobe Developer Console, moet uw account ontwikkelings- en gebruikersmachtigingen hebben voor een productprofiel voor een Experience Platform in Adobe Admin Console.

### Toegang voor ontwikkelaars verkrijgen

Neem contact op met een [!DNL Admin Console]-beheerder in uw organisatie om u als ontwikkelaar toe te voegen aan een productprofiel van een Experience Platform met de [[!DNL Admin Console]](https://adminconsole.adobe.com/). Zie de [!DNL Admin Console] documentatie voor specifieke instructies over hoe te [de toegang van de ontwikkelaar voor productprofielen ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html) beheren.

Als u eenmaal als ontwikkelaar bent toegewezen, kunt u beginnen met het maken van integratie in [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Deze integratie vormt een pijplijn van externe apps en services naar Adobe-API&#39;s.

### Toegang tot gebruikers verkrijgen

Uw [!DNL Admin Console] beheerder moet u als gebruiker aan het zelfde productprofiel ook toevoegen. Zie de handleiding over [het beheren van gebruikersgroepen in [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) voor meer informatie.

## Een API-sleutel, IMS Org ID en een clientgeheim {#api-ims-secret} genereren

>[!NOTE]
>
>Als u dit document van [Privacy Service ontwikkelaarsgids](../privacy-service/api/getting-started.md) volgt, kunt u nu aan die gids terugkeren om de toegangsgeloofsbrieven te produceren uniek aan [!DNL Privacy Service].

Nadat u ontwikkelaar en gebruiker toegang tot Platform door [!DNL Admin Console] hebt gekregen, is de volgende stap uw `{IMS_ORG}` en `{API_KEY}` geloofsbrieven in de Console van de Ontwikkelaar van de Adobe te produceren. Deze geloofsbrieven moeten slechts eenmaal worden geproduceerd en kunnen in toekomstige Platform API vraag worden opnieuw gebruikt.

### Experience Platform toevoegen aan een project

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Volg vervolgens de stappen die worden beschreven in de zelfstudie over het maken van een leeg project](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de documentatie van de Adobe Developer Console.[

Nadat u een nieuw project hebt gemaakt, selecteert u **[!UICONTROL Add API]** op het scherm **[!UICONTROL Project Overview]**.

![](./images/api-authentication/add-api.png)

Het **[!UICONTROL Add an API]** scherm verschijnt. Selecteer het productpictogram voor Adobe Experience Platform en kies **[!UICONTROL Experience Platform API]** voordat u **[!UICONTROL Next]** selecteert.

![](./images/api-authentication/platform-api.png)

Van hier, volg de stappen die in de zelfstudie op [worden geschetst toevoegend API aan een project gebruikend een de dienstrekening (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (beginnend van de &quot;Configure API&quot;stap) om het proces te beëindigen.

>[!IMPORTANT]
>
>Tijdens een bepaalde stap tijdens het hierboven gekoppelde proces worden in uw browser automatisch een persoonlijke sleutel en een bijbehorend openbaar certificaat gedownload. Deze persoonlijke sleutel wordt op uw computer opgeslagen, aangezien deze in een latere stap in deze zelfstudie is vereist.

### Referenties verzamelen

Zodra API aan het project is toegevoegd, **[!UICONTROL Experience Platform API]** de pagina voor het project toont de volgende geloofsbrieven die in alle vraag aan Experience Platform APIs worden vereist:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{IMS_ORG}` ([!UICONTROL Organization ID])

![](././images/api-authentication/api-key-ims-org.png)

Naast de bovengenoemde geloofsbrieven, hebt u ook geproduceerde **[!UICONTROL Client Secret]** voor een toekomstige stap nodig. Selecteer **[!UICONTROL Retrieve client secret]** om de waarde weer te geven en kopieer deze vervolgens voor later gebruik.

![](././images/api-authentication/client-secret.png)

## Een JSON-webtoken (JWT) {#jwt} genereren

De volgende stap bestaat uit het genereren van een JSON Web Token (JWT) op basis van uw accountgegevens. Deze waarde wordt gebruikt om uw `{ACCESS_TOKEN}` referentie voor gebruik in Platform API vraag te produceren, die om de 24 uur opnieuw moet worden geproduceerd.

Selecteer **[!UICONTROL Service Account (JWT)]** in de linkernavigatie, dan uitgezocht **[!UICONTROL Generate JWT]**.

![](././images/api-authentication/generate-jwt.png)

Plak in het tekstvak onder **[!UICONTROL Generate custom JWT]** de inhoud van de persoonlijke sleutel die u eerder hebt gegenereerd toen u de Platform-API aan uw serviceaccount toevoegde. Selecteer vervolgens **[!UICONTROL Generate Token]**.

![](././images/api-authentication/paste-key.png)

De pagina wordt bijgewerkt om de gegenereerde JWT weer te geven, samen met een voorbeeld-URL-opdracht waarmee u een toegangstoken kunt genereren. In deze zelfstudie selecteert u **[!UICONTROL Copy]** naast **[!UICONTROL Generated JWT]** om het token naar het klembord te kopiëren.

![](././images/api-authentication/copy-jwt.png)

## Een toegangstoken genereren

Zodra u een JWT hebt geproduceerd, kunt u het in een API vraag gebruiken om uw `{ACCESS_TOKEN}` te produceren. In tegenstelling tot de waarden voor `{API_KEY}` en `{IMS_ORG}`, moet om de 24 uur een nieuw token worden gegenereerd om verder te gaan met het gebruik van Platform-API&#39;s.

**Verzoek**

Met het volgende verzoek wordt een nieuwe `{ACCESS_TOKEN}` gegenereerd op basis van de referenties die in de payload zijn opgegeven. Dit eindpunt keurt slechts vormgegevens als zijn lading goed, en daarom moet het een `Content-Type` kopbal van `multipart/form-data` worden gegeven.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `{API_KEY}` | De `{API_KEY}` ([!UICONTROL Client ID]) die u in een [vorige stap](#api-ims-secret) terughaalde. |
| `{SECRET}` | Het clientgeheim dat u hebt opgehaald in een [vorige stap](#api-ims-secret). |
| `{JWT}` | De JWT die u in een [vorige stap](#jwt) hebt gegenereerd. |

>[!NOTE]
>
>U kunt dezelfde API-sleutel, clientgeheim en JWT gebruiken om een nieuw toegangstoken voor elke sessie te genereren. Hierdoor kunt u het genereren van toegangstoken in uw toepassingen automatiseren.

**Antwoord**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `token_type` | Het type token dat wordt geretourneerd. Voor toegangstokens, is deze waarde altijd `bearer`. |
| `access_token` | De gegenereerde `{ACCESS_TOKEN}`. Deze waarde, die met het woord `Bearer` vooraf wordt bepaald, wordt vereist als `Authentication` kopbal voor alle Platform API vraag. |
| `expires_in` | Het aantal milliseconden dat resteert tot het toegangstoken verloopt. Zodra deze waarde 0 bereikt, moet een nieuw toegangstoken worden geproduceerd om Platform APIs te blijven gebruiken. |

## Toegangsreferenties testen

Nadat u alle drie vereiste gegevens hebt verzameld, kunt u de volgende API-aanroep proberen te maken. Deze vraag maakt een lijst van alle standaard [!DNL Experience Data Model] (XDM) klassen beschikbaar aan uw organisatie.

**Verzoek**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwoord**

Als uw reactie vergelijkbaar is met de hieronder weergegeven reactie, zijn uw gegevens geldig en werken ze. (Deze reactie is afgebroken voor de ruimte.)

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

## Gebruik Postman om API-aanroepen te verifiëren en te testen

[](https://www.postman.com/) Postmanis is een populair hulpmiddel dat ontwikkelaars toestaat om RESTful APIs te onderzoeken en te testen. In deze [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wordt beschreven hoe u Postman kunt instellen om automatisch JWT-verificatie uit te voeren en deze te gebruiken om Platform-API&#39;s te gebruiken.

## Volgende stappen

Door dit document te lezen, hebt u uw toegangsreferenties voor Platform-API&#39;s verzameld en getest. U kunt nu de voorbeeldAPI vraag volgen die door [documentatie](../landing/documentation/overview.md) wordt verstrekt.

Naast de authentificatiewaarden u in dit leerprogramma hebt verzameld, vereisen veel Platform APIs ook een geldige `{SANDBOX_NAME}` om als kopbal worden verstrekt. Zie het [overzicht van sandboxen](../sandboxes/home.md) voor meer informatie.