---
keywords: Experience Platform;thuis;populaire onderwerpen;Authenticeren;toegang
solution: Experience Platform
title: API's van Experience Platforms verifiëren en benaderen
topic-legacy: tutorial
type: Tutorial
description: Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen uit te voeren naar Experience Platform-API's.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 1%

---


# Experience Platform-API&#39;s verifiëren en openen

Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen uit te voeren naar Experience Platform-API&#39;s. Aan het eind van dit leerprogramma, zult u de volgende geloofsbrieven hebben geproduceerd die voor alle Platform API vraag worden vereist:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

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

Contact opnemen met [!DNL Admin Console] beheerder in uw organisatie om u als ontwikkelaar aan een het productprofiel van het Experience Platform toe te voegen gebruikend [[!DNL Admin Console]](https://adminconsole.adobe.com/). Zie de [!DNL Admin Console] documentatie voor specifieke instructies over hoe te [toegang voor ontwikkelaars beheren voor productprofielen](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Als u eenmaal als ontwikkelaar bent toegewezen, kunt u beginnen met het maken van integratie in [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Deze integratie vormt een pijplijn van externe apps en services naar Adobe-API&#39;s.

### Toegang tot gebruikers verkrijgen

Uw [!DNL Admin Console] beheerder moet u ook als gebruiker toevoegen aan hetzelfde productprofiel. Zie de handleiding op [gebruikersgroepen beheren in [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) voor meer informatie .

## Een API-sleutel, IMS Org ID en een clientgeheim genereren {#api-ims-secret}

>[!NOTE]
>
>Als u dit document volgt vanuit de [Handleiding Privacy Service-API](../privacy-service/api/getting-started.md), kunt u nu terugkeren naar die gids om de toegangsgeloofsbrieven te produceren uniek aan [!DNL Privacy Service].

Nadat u ontwikkelaars en gebruikers toegang tot Platform hebt gegeven door [!DNL Admin Console]De volgende stap bestaat uit het genereren van uw `{ORG_ID}` en `{API_KEY}` referenties in Adobe Developer Console. Deze geloofsbrieven moeten slechts eenmaal worden geproduceerd en kunnen in toekomstige Platform API vraag worden opnieuw gebruikt.

### Experience Platform toevoegen aan een project

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Voer vervolgens de stappen uit die in de zelfstudie worden beschreven [een leeg project maken](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de Adobe Developer Console-documentatie.

Als u een nieuw project hebt gemaakt, selecteert u **[!UICONTROL Add API]** op de **[!UICONTROL Project Overview]** scherm.

![](./images/api-authentication/add-api.png)

De **[!UICONTROL Add an API]** wordt weergegeven. Selecteer het productpictogram voor Adobe Experience Platform en kies **[!UICONTROL Experience Platform API]** voordat u selecteert **[!UICONTROL Next]**.

![](./images/api-authentication/platform-api.png)

Volg vanaf hier de stappen die in de zelfstudie worden beschreven [toevoegen van API aan een project gebruikend een de dienstrekening (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (vanaf de stap &quot;API configureren&quot;) om het proces te voltooien.

>[!IMPORTANT]
>
>Tijdens een bepaalde stap tijdens het hierboven gekoppelde proces worden in uw browser automatisch een persoonlijke sleutel en een bijbehorend openbaar certificaat gedownload. Deze persoonlijke sleutel wordt op uw computer opgeslagen, aangezien deze in een latere stap in deze zelfstudie is vereist.

### Referenties verzamelen

Zodra API aan het project is toegevoegd, **[!UICONTROL Experience Platform API]** De pagina voor het project toont de volgende geloofsbrieven die in alle vraag aan Experience Platform APIs worden vereist:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{ORG_ID}` ([!UICONTROL Organization ID])

![](././images/api-authentication/api-key-ims-org.png)

Naast de bovenstaande referenties hebt u ook de gegenereerde **[!UICONTROL Client Secret]** voor een toekomstige stap. Selecteren **[!UICONTROL Retrieve client secret]** om de waarde weer te geven en deze vervolgens voor later gebruik te kopiëren.

![](././images/api-authentication/client-secret.png)

## Een JSON-webtoken (JWT) genereren {#jwt}

De volgende stap bestaat uit het genereren van een JSON Web Token (JWT) op basis van uw accountgegevens. Deze waarde wordt gebruikt om uw `{ACCESS_TOKEN}` referentie voor gebruik in Platform API vraag, die om de 24 uur opnieuw moet worden geproduceerd.

>[!IMPORTANT]
>
>In deze zelfstudie wordt in de onderstaande stappen beschreven hoe u een JWT kunt genereren in de Developer Console. Deze generatiemethode mag echter alleen voor test- en evaluatiedoeleinden worden gebruikt.
>
>Voor normaal gebruik moet de JWT automatisch worden gegenereerd. Voor meer informatie over hoe te om JWTs programmatically te produceren, zie [servicerekeningautorisatiehandleiding](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) op Adobe Developer.

Selecteren **[!UICONTROL Service Account (JWT)]** in de linkernavigatie selecteert u vervolgens **[!UICONTROL Generate JWT]**.

![](././images/api-authentication/generate-jwt.png)

In het tekstvak onder **[!UICONTROL Generate custom JWT]** plakken, plakt u de inhoud van de persoonlijke sleutel die u eerder hebt gegenereerd toen u de Platform-API aan uw serviceaccount toevoegde. Selecteer vervolgens **[!UICONTROL Generate Token]**.

![](././images/api-authentication/paste-key.png)

De pagina wordt bijgewerkt om de gegenereerde JWT weer te geven, samen met een voorbeeld-URL-opdracht waarmee u een toegangstoken kunt genereren. In deze zelfstudie selecteert u **[!UICONTROL Copy]** naast **[!UICONTROL Generated JWT]** om het token naar het klembord te kopiëren.

![](././images/api-authentication/copy-jwt.png)

## Een toegangstoken genereren

Nadat u een JWT hebt gegenereerd, kunt u deze gebruiken in een API-aanroep om uw `{ACCESS_TOKEN}`. In tegenstelling tot de waarden voor `{API_KEY}` en `{ORG_ID}`moet om de 24 uur een nieuw token worden gegenereerd om Platform API&#39;s te kunnen blijven gebruiken.

**Verzoek**

Met de volgende aanvraag wordt een nieuwe `{ACCESS_TOKEN}` op basis van de gegevens die in de payload zijn opgegeven. Dit eindpunt keurt vormgegevens slechts als zijn lading goed, en daarom moet het worden gegeven `Content-Type` header van `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `{API_KEY}` | De `{API_KEY}` ([!UICONTROL Client ID]) die u hebt opgehaald in een [vorige stap](#api-ims-secret). |
| `{SECRET}` | Het clientgeheim dat u hebt opgehaald in een [vorige stap](#api-ims-secret). |
| `{JWT}` | De JWT die u in een [vorige stap](#jwt). |

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
| `token_type` | Het type token dat wordt geretourneerd. Deze waarde is altijd voor toegangstokens `bearer`. |
| `access_token` | De gegenereerde `{ACCESS_TOKEN}`. Deze waarde, voorafgegaan door het woord `Bearer`is vereist als de `Authentication` header voor alle Platform API-aanroepen. |
| `expires_in` | Het aantal milliseconden dat resteert tot het toegangstoken verloopt. Zodra deze waarde 0 bereikt, moet een nieuw toegangstoken worden geproduceerd om Platform APIs te blijven gebruiken. |

## Toegangsreferenties testen

Nadat u alle drie vereiste gegevens hebt verzameld, kunt u de volgende API-aanroep proberen te maken. Deze vraag maakt een lijst van alle norm [!DNL Experience Data Model] (XDM) klassen beschikbaar aan uw organisatie.

**Verzoek**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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

## Postman gebruiken om API-aanroepen te verifiëren en te testen

[Postman](https://www.postman.com/) is een populair hulpmiddel dat ontwikkelaars toestaat om RESTful APIs te onderzoeken en te testen. Dit [Normale post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) beschrijft hoe u Postman kunt instellen om automatisch JWT-verificatie uit te voeren en deze te gebruiken om Platform-API&#39;s te gebruiken.

## Volgende stappen

Door dit document te lezen, hebt u uw toegangsreferenties voor Platform-API&#39;s verzameld en getest. U kunt nu de voorbeeld-API-aanroepen volgen die via de [documentatie](../landing/documentation/overview.md).

Naast de authentificatiewaarden u in dit leerprogramma hebt verzameld, vereisen vele Platform APIs ook een geldig `{SANDBOX_NAME}` te verstrekken als koptekst. Zie de [sandboxen, overzicht](../sandboxes/home.md) voor meer informatie .