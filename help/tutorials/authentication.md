---
keywords: Experience Platform;home;popular topics;Authenticate;access
solution: Experience Platform
title: API's van Experience Platforms verifiëren en benaderen
topic: tutorial
description: 'Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen uit te voeren naar Experience Platform-API''s. '
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---


# API&#39; [!DNL Experience Platform] s verifiëren en openen

Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen naar API&#39; [!DNL Experience Platform] s uit te voeren.

## Verifiëren om API-aanroepen te maken

Om de veiligheid van uw toepassingen en gebruikers te handhaven, moeten alle verzoeken aan Adobe I/O APIs voor authentiek worden verklaard en worden gemachtigd gebruikend normen zoals OAuth en JSON Webtokens (JWT). JWT wordt dan gebruikt samen met cliënt-specifieke informatie om uw persoonlijk toegangstoken te produceren.

Deze zelfstudie behandelt de stappen van authentificatie door het creëren van een toegangstoken die in het volgende stroomschema wordt geschetst:
![](images/authentication/authentication-flowchart.png)

## Vereisten

Als u aanroepen naar API&#39; [!DNL Experience Platform] s wilt uitvoeren, hebt u het volgende nodig:

* Een IMS-organisatie met toegang tot Adobe Experience Platform
* Een geregistreerde Adobe ID-account
* Een beheerder van de Admin Console om u als **ontwikkelaar** en een **gebruiker** voor een product toe te voegen.

De volgende secties lopen door de stappen om een Adobe ID tot stand te brengen en een ontwikkelaar en een gebruiker voor een organisatie te worden.

### Een Adobe ID maken

Als u geen Adobe ID hebt, kunt u er een maken door de volgende stappen uit te voeren:

1. Ga naar [Adobe Developer Console](https://console.adobe.io)
2. Klik op Een nieuw account **[!UICONTROL maken]**
3. Voltooi het aanmeldingsproces

## Ontwikkelaar en gebruiker worden voor [!DNL Experience Platform] een organisatie

Voordat u integratie op Adobe I/O maakt, moet uw account beschikken over ontwikkelaarsmachtigingen voor een product in een IMS-organisatie. Gedetailleerde informatie over ontwikkelaarsaccounts in de Admin Console vindt u in het [ondersteuningsdocument](https://helpx.adobe.com/enterprise/using/manage-developers.html) voor ontwikkelaars.

**Toegang voor ontwikkelaars verkrijgen**

Neem contact op met een [!DNL Admin Console] beheerder in uw organisatie om u toe te voegen als ontwikkelaar voor een van de producten van uw organisatie met de [[!DNL-Admin Console]](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

De beheerder moet u als ontwikkelaar toewijzen aan ten minste één productprofiel om door te gaan.

![](images/authentication/add-developer.png)

Als u eenmaal als ontwikkelaar bent toegewezen, hebt u toegangsrechten om integraties te maken voor [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Deze integratie vormt een pijplijn van externe apps en services naar de Adobe-API.

**Toegang tot gebruikers verkrijgen**

Uw [!DNL Admin Console] beheerder moet u ook als gebruiker aan het product toevoegen.

![](images/authentication/assign-users.png)

Net als bij het toevoegen van een ontwikkelaar moet de beheerder u toewijzen aan ten minste één productprofiel om door te gaan.

![](images/authentication/assign-user-details.png)

## Toegangsgegevens genereren in Adobe Developer Console

>[!NOTE]
>
>Als u dit document volgt vanuit de [Privacy Service-ontwikkelaarsgids](../privacy-service/api/getting-started.md), kunt u nu terugkeren naar die handleiding om de toegangsreferenties te genereren die uniek zijn voor [!DNL Privacy Service].

Gebruikend de Console van de Ontwikkelaar van Adobe, moet u de volgende drie toegangsgeloofsbrieven produceren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Uw `{IMS_ORG}` en `{API_KEY}` hoeven slechts eenmaal te worden gegenereerd en kunnen in toekomstige [!DNL Platform] API-aanroepen opnieuw worden gebruikt. Uw `{ACCESS_TOKEN}` is echter tijdelijk en moet elke 24 uur opnieuw worden gegenereerd.

De stappen worden hieronder in detail besproken.

### Eenmalige installatie

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Voer vervolgens de stappen uit die worden beschreven in de zelfstudie over het [maken van een leeg project](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de documentatie van de Adobe Developer Console.

Nadat u een nieuw project hebt gemaakt, klikt u op API **** toevoegen in het scherm _Projectoverzicht_ .

![](images/authentication/add-api-button.png)

Het scherm _Een API_ toevoegen wordt weergegeven. Klik op het productpictogram voor Adobe Experience Platform en selecteer vervolgens de **[!UICONTROL Experience Platform-API]** voordat u op **[!UICONTROL Volgende]** klikt.

![](images/authentication/add-platform-api.png)

Nadat u hebt geselecteerd [!DNL Experience Platform] als de API die aan het project moet worden toegevoegd, volgt u de stappen in de zelfstudie over het [toevoegen van een API aan een project met een serviceaccount (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (vanaf de stap API configureren) om het proces te voltooien.

Zodra API aan het project is toegevoegd, toont de het overzichtspagina _van het_ [!DNL Experience Platform] Project de volgende geloofsbrieven die in alle vraag aan APIs worden vereist:

* `{API_KEY}` (Client-id)
* `{IMS_ORG}` (Organisatie-id)

![](./images/authentication/api-key-ims-org.png)

### Verificatie voor elke sessie

De laatste vereiste referentie die u moet verzamelen, is uw `{ACCESS_TOKEN}`. In tegenstelling tot de waarden voor `{API_KEY}` en `{IMS_ORG}`, moet om de 24 uur een nieuw token worden gegenereerd om API&#39; [!DNL Platform] s te kunnen blijven gebruiken.

Als u een nieuwe token `{ACCESS_TOKEN}`wilt genereren, volgt u de stappen om een JWT-token [te](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) genereren in de handleiding voor de aanmeldgegevens van de Developer Console.

## Toegangsreferenties testen

Nadat u alle drie vereiste gegevens hebt verzameld, kunt u de volgende API-aanroep proberen te maken. Deze vraag zal van alle [!DNL Experience Data Model] (XDM) klassen binnen de container van de Registratie van het Schema een lijst maken `global` :

**API-indeling**

```http
GET /global/classes
```

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

## Postman gebruiken voor JWT-verificatie en API-aanroepen

[Postman](https://www.getpostman.com/) is een populair hulpmiddel om met RESTful APIs te werken. In dit [artikel](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wordt beschreven hoe u een postman kunt instellen om automatisch JWT-verificatie uit te voeren en deze te gebruiken voor het gebruik van Adobe Experience Platform API&#39;s.

## Volgende stappen

Door dit document te lezen, hebt u uw toegangsreferenties voor API&#39; [!DNL Platform] s verzameld en getest. U kunt nu de voorbeeld-API-aanroepen volgen die in de hele [documentatie](../landing/documentation/overview.md)zijn opgegeven.

Naast de verificatiewaarden die u hebt verzameld in deze zelfstudie, vereisen veel [!DNL Platform] API&#39;s ook dat een geldige id als koptekst `{SANDBOX_NAME}` wordt opgegeven. Zie het [sandboxoverzicht](../sandboxes/home.md) voor meer informatie.