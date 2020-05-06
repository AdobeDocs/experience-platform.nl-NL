---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Platform-API's verifiëren en openen
topic: tutorial
translation-type: tm+mt
source-git-commit: e1ba476fffc164b78decd7168192714993c791bc
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---


# Platform-API&#39;s verifiëren en openen

Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaaraccount om aanroepen uit te voeren naar Experience Platform-API&#39;s.

## Verifiëren om API-aanroepen te maken

Om de beveiliging van uw toepassingen en gebruikers te garanderen, moeten alle aanvragen voor Adobe I/O-API&#39;s worden geverifieerd en geautoriseerd aan de hand van standaarden zoals OAuth en JSON Web Tokens (JWT). JWT wordt dan gebruikt samen met cliënt-specifieke informatie om uw persoonlijk toegangstoken te produceren.

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

1. Ga naar [Adobe Developer Console](https://console.adobe.io)
2. Klik op Een nieuw account **maken**
3. Voltooi het aanmeldingsproces

## Word een ontwikkelaar en gebruiker voor het Platform van de Ervaring voor een organisatie

Voordat u integraties maakt voor Adobe I/O, moet uw account ontwikkelaarsmachtigingen voor een product in een IMS-organisatie hebben. Gedetailleerde informatie over ontwikkelaarsaccounts in de beheerconsole vindt u in het [ondersteuningsdocument](https://helpx.adobe.com/enterprise/using/manage-developers.html) voor ontwikkelaars.

**Toegang voor ontwikkelaars verkrijgen**

Neem contact op met een beheerder van de beheerconsole in uw organisatie om u via de [beheerconsole](https://adminconsole.adobe.com/)toe te voegen als ontwikkelaar voor een van de producten van uw organisatie.

![](images/authentication/assign-developer.png)

De beheerder moet u als ontwikkelaar toewijzen aan ten minste één productprofiel om door te gaan.

![](images/authentication/add-developer.png)

Als u eenmaal als ontwikkelaar bent toegewezen, hebt u toegangsrechten om integraties te maken voor [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Deze integraties vormen een pijplijn van externe apps en services naar de Adobe API.

**Toegang tot gebruikers verkrijgen**

De beheerder van de beheerconsole moet u ook als gebruiker aan het product toevoegen.

![](images/authentication/assign-users.png)

Net als bij het toevoegen van een ontwikkelaar moet de beheerder u toewijzen aan ten minste één productprofiel om door te gaan.

![](images/authentication/assign-user-details.png)


## Toegangsgegevens genereren in Adobe Developer Console

Met Adobe Developer Console moet u de volgende drie toegangsreferenties genereren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Uw `{IMS_ORG}` en `{API_KEY}` hoeven slechts eenmaal te worden gegenereerd en kunnen in toekomstige API-aanroepen van het platform opnieuw worden gebruikt. Uw `{ACCESS_TOKEN}` is echter tijdelijk en moet elke 24 uur opnieuw worden gegenereerd.

De stappen worden hieronder in detail besproken.

### Eenmalige installatie

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe-id. Voer vervolgens de stappen uit die worden beschreven in de zelfstudie over het [maken van een leeg project](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de documentatie van de Adobe Developer Console.

Nadat u een nieuw project hebt gemaakt, klikt u op API **** toevoegen in het scherm _Projectoverzicht_ .

![](images/authentication/add-api-button.png)

Het scherm _Een API_ toevoegen wordt weergegeven. Klik op het productpictogram voor Adobe Experience Platform en selecteer **[!UICONTROL Experience Platform API]** voordat u op **[!UICONTROL Volgende]** klikt.

![](images/authentication/add-platform-api.png)

Zodra u het Platform van de Ervaring als API hebt geselecteerd die aan het project moet worden toegevoegd, volg de stappen die in het leerprogramma worden geschetst over het [toevoegen van API aan een project gebruikend een de dienstrekening (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (die van &quot;vormen API&quot;stap) beginnen om het proces te voltooien.

Zodra API aan het project is toegevoegd, toont de het overzichtspagina _van het_ Project de volgende geloofsbrieven die in alle vraag aan het Platform APIs van de Ervaring worden vereist:

* `{API_KEY}` (Client-id)
* `{IMS_ORG}` (Organisatie-id)

![](./images/authentication/api-key-ims-org.png)

### Verificatie voor elke sessie

De laatste vereiste referentie die u moet verzamelen, is uw `{ACCESS_TOKEN}`. In tegenstelling tot de waarden voor `{API_KEY}` en `{IMS_ORG}`, moet om de 24 uur een nieuw token worden gegenereerd om door te gaan met het gebruik van platform-API&#39;s.

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

Als uw reactie vergelijkbaar is met de hieronder weergegeven reactie, zijn uw gegevens geldig en werken ze. (Deze reactie is afgebroken voor de ruimte.)

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

## Volgende stappen

Door dit document te lezen, hebt u uw toegangsreferenties voor platform-API&#39;s verzameld en getest. U kunt nu de voorbeeld-API-aanroepen volgen die in de hele [documentatie](../landing/documentation/overview.md)zijn opgegeven.

Naast de authentificatiewaarden u in dit leerprogramma hebt verzameld, vereisen vele Platform APIs ook geldig `{SANDBOX_NAME}` om als kopbal worden verstrekt. Zie het [sandboxoverzicht](../sandboxes/home.md) voor meer informatie.