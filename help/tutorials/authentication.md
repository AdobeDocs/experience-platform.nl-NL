---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: API's van Experience Platforms verifiëren en benaderen
topic: tutorial
translation-type: tm+mt
source-git-commit: 280456e68f54f49ce4a0134e226af89ad1f849a4
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---


# API&#39;s van Experience Platforms verifiëren en openen

Dit document verstrekt een geleidelijke zelfstudie voor het verkrijgen van toegang tot een rekening van de ontwikkelaar van het Adobe Experience Platform om vraag aan Experience Platform APIs te maken.

## Verifiëren om API-aanroepen te maken

Om de beveiliging van uw toepassingen en gebruikers te garanderen, moeten alle aanvragen voor Adobe I/O-API&#39;s worden geverifieerd en geautoriseerd aan de hand van standaarden zoals OAuth en JSON Web Tokens (JWT). JWT wordt dan gebruikt samen met cliënt-specifieke informatie om uw persoonlijk toegangstoken te produceren.

Deze zelfstudie behandelt de stappen van authentificatie door het creëren van een toegangstoken die in het volgende stroomschema wordt geschetst:
![](images/authentication/authentication-flowchart.png)

## Vereisten

Om met succes vraag aan Experience Platform APIs te maken, vereist u het volgende:

* Een IMS-organisatie met toegang tot Adobe Experience Platform
* Een geregistreerde Adobe ID-account
* Een beheerder van de Admin Console om u als **ontwikkelaar** en een **gebruiker** voor een product toe te voegen.

De volgende secties lopen door de stappen om een Adobe ID tot stand te brengen en een ontwikkelaar en een gebruiker voor een organisatie te worden.

### Een Adobe ID maken

Als u geen Adobe ID hebt, kunt u een van de volgende stappen maken:

1. Ga naar [Adobe Developer Console](https://console.adobe.io)
2. Klik op Een nieuw account **maken**
3. Voltooi het aanmeldingsproces

## Ontwikkelaar en gebruiker worden van Experience Platform voor een organisatie

Voordat u integraties maakt voor Adobe I/O, moet uw account ontwikkelaarsmachtigingen voor een product in een IMS-organisatie hebben. Gedetailleerde informatie over ontwikkelaarsaccounts in de Admin Console vindt u in het [ondersteuningsdocument](https://helpx.adobe.com/enterprise/using/manage-developers.html) voor ontwikkelaars.

**Toegang voor ontwikkelaars verkrijgen**

Neem contact op met een beheerder van een Admin Console in uw organisatie om u toe te voegen als ontwikkelaar voor een van de producten van uw organisatie met de [Admin Console](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

De beheerder moet u als ontwikkelaar toewijzen aan ten minste één productprofiel om door te gaan.

![](images/authentication/add-developer.png)

Als u eenmaal als ontwikkelaar bent toegewezen, hebt u toegangsrechten om integraties te maken voor [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Deze integraties vormen een pijplijn van externe apps en services naar de Adobe API.

**Toegang tot gebruikers verkrijgen**

Uw beheerder van de Admin Console moet u ook als gebruiker aan het product toevoegen.

![](images/authentication/assign-users.png)

Net als bij het toevoegen van een ontwikkelaar moet de beheerder u toewijzen aan ten minste één productprofiel om door te gaan.

![](images/authentication/assign-user-details.png)

## Toegangsgegevens genereren in Adobe Developer Console

>[!NOTE] Als u dit document volgt vanuit de [Privacy Service-ontwikkelaarsgids](../privacy-service/api/getting-started.md), kunt u nu terugkeren naar die handleiding om de toegangsreferenties te genereren die uniek zijn voor de Privacy Service.

Met Adobe Developer Console moet u de volgende drie toegangsreferenties genereren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Uw `{IMS_ORG}` en `{API_KEY}` moeten slechts eenmaal worden geproduceerd en kunnen in toekomstige Platform API vraag worden opnieuw gebruikt. Uw `{ACCESS_TOKEN}` is echter tijdelijk en moet elke 24 uur opnieuw worden gegenereerd.

De stappen worden hieronder in detail besproken.

### Eenmalige installatie

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Voer vervolgens de stappen uit die worden beschreven in de zelfstudie over het [maken van een leeg project](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de documentatie van de Adobe Developer Console.

Nadat u een nieuw project hebt gemaakt, klikt u op API **** toevoegen in het scherm _Projectoverzicht_ .

![](images/authentication/add-api-button.png)

Het scherm _Een API_ toevoegen wordt weergegeven. Klik op het productpictogram voor Adobe Experience Platform en selecteer vervolgens de **[!UICONTROL Experience Platform-API]** voordat u op **[!UICONTROL Volgende]** klikt.

![](images/authentication/add-platform-api.png)

Nadat u Experience Platform hebt geselecteerd als de API die aan het project moet worden toegevoegd, volgt u de stappen in de zelfstudie over het [toevoegen van een API aan een project met behulp van een serviceaccount (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (vanaf de stap API configureren) om het proces te voltooien.

Zodra API aan het project is toegevoegd, toont de het overzichtspagina _van het_ Project de volgende geloofsbrieven die in alle vraag aan Experience Platform APIs worden vereist:

* `{API_KEY}` (Client-id)
* `{IMS_ORG}` (Organisatie-id)

![](./images/authentication/api-key-ims-org.png)

### Verificatie voor elke sessie

De laatste vereiste referentie die u moet verzamelen, is uw `{ACCESS_TOKEN}`. In tegenstelling tot de waarden voor `{API_KEY}` en `{IMS_ORG}`, moet om de 24 uur een nieuw token worden gegenereerd om door te gaan met het gebruik van Platform-API&#39;s.

Als u een nieuwe token `{ACCESS_TOKEN}`wilt genereren, volgt u de stappen om een JWT-token [te](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) genereren in de handleiding voor de aanmeldgegevens van de Developer Console.

## Toegangsreferenties testen

Nadat u alle drie vereiste gegevens hebt verzameld, kunt u de volgende API-aanroep proberen te maken. Deze vraag zal van alle klassen van het Model van Gegevens van de Ervaring (XDM) binnen de container van de Registratie van het Schema een lijst maken: `global`

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

[Postman](https://www.getpostman.com/) is een populair hulpmiddel om met RESTful APIs te werken. In dit [artikel](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wordt beschreven hoe u een postman kunt instellen om automatisch JWT-verificatie uit te voeren en deze te gebruiken voor het gebruik van Adobe Experience Platform-API&#39;s.

## Volgende stappen

Door dit document te lezen, hebt u uw toegangsreferenties voor Platform-API&#39;s verzameld en getest. U kunt nu de voorbeeld-API-aanroepen volgen die in de hele [documentatie](../landing/documentation/overview.md)zijn opgegeven.

Naast de authentificatiewaarden u in dit leerprogramma hebt verzameld, vereisen vele Platform APIs ook geldig `{SANDBOX_NAME}` om als kopbal worden verstrekt. Zie het [sandboxoverzicht](../sandboxes/home.md) voor meer informatie.