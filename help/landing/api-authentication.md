---
keywords: Experience Platform;thuis;populaire onderwerpen;Authenticeren;toegang
solution: Experience Platform
title: API's van Experience Platforms verifiëren en benaderen
topic: zelfstudie
type: Zelfstudie
description: 'Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen uit te voeren naar Experience Platform-API''s. '
translation-type: tm+mt
source-git-commit: ca5c8527b1b54856aa1e762a06ddbe404f30ec42
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---


# [!DNL Experience Platform] API&#39;s verifiëren en openen

Dit document biedt een stapsgewijze zelfstudie voor het verkrijgen van toegang tot een Adobe Experience Platform-ontwikkelaarsaccount om aanroepen uit te voeren naar [!DNL Experience Platform] API&#39;s.

## Verifiëren om API-aanroepen te maken

Om de veiligheid van uw toepassingen en gebruikers te handhaven, moeten alle verzoeken aan Adobe I/O APIs voor authentiek worden verklaard en worden gemachtigd gebruikend normen zoals de Tokens van het Web OAuth en JSON (JWT). JWT wordt dan gebruikt samen met cliënt-specifieke informatie om uw persoonlijk toegangstoken te produceren.

Deze zelfstudie behandelt de stappen van authentificatie door het creëren van een toegangstoken die in het volgende stroomschema wordt geschetst:
![](images/api-authentication/authentication-flowchart.png)

## Vereisten

Als u met succes aanroepen naar [!DNL Experience Platform] API&#39;s wilt uitvoeren, hebt u het volgende nodig:

* Een IMS-organisatie met toegang tot Adobe Experience Platform
* Een geregistreerde Adobe ID-account
* Een beheerder van de Admin Console om u als **ontwikkelaar** en **gebruiker** voor een product toe te voegen.

De volgende secties lopen door de stappen om een Adobe ID tot stand te brengen en een ontwikkelaar en een gebruiker voor een organisatie te worden.

### Een Adobe ID maken

Als u geen Adobe ID hebt, kunt u er een maken door de volgende stappen uit te voeren:

1. Ga naar [Adobe Developer Console](https://console.adobe.io)
2. Selecteer **[!UICONTROL een nieuw account maken]**
3. Voltooi het aanmeldingsproces

## Ontwikkelaar en gebruiker worden voor [!DNL Experience Platform] voor een organisatie

Voordat u integraties op Adobe I/O maakt, moet uw account beschikken over ontwikkelaarsmachtigingen voor een product in een IMS-organisatie. Gedetailleerde informatie over ontwikkelaarsaccounts in de Admin Console vindt u in het [ondersteuningsdocument](https://helpx.adobe.com/enterprise/using/manage-developers.html) voor het beheer van ontwikkelaars.

**Toegang voor ontwikkelaars verkrijgen**

Neem contact op met een [!DNL Admin Console]-beheerder in uw organisatie om u toe te voegen als ontwikkelaar voor een van de producten van uw organisatie met de [[!DNL Admin Console]](https://adminconsole.adobe.com/).

![](images/api-authentication/assign-developer.png)

De beheerder moet u als ontwikkelaar toewijzen aan ten minste één productprofiel om door te gaan.

![](images/api-authentication/add-developer.png)

Zodra u als ontwikkelaar wordt toegewezen, zult u toegangsvoorrechten hebben om tot integratie op [Adobe I/O](https://www.adobe.com/go/devs_console_ui) te leiden. Deze integratie vormt een pijplijn van externe apps en services naar de Adobe-API.

**Toegang tot gebruikers verkrijgen**

Uw [!DNL Admin Console] beheerder moet u aan het product als gebruiker ook toevoegen.

![](images/api-authentication/assign-users.png)

Net als bij het toevoegen van een ontwikkelaar moet de beheerder u toewijzen aan ten minste één productprofiel om door te gaan.

![](images/api-authentication/assign-user-details.png)

## Toegangsgegevens genereren in Adobe Developer Console

>[!NOTE]
>
>Als u dit document van [Privacy Service ontwikkelaarsgids](../privacy-service/api/getting-started.md) volgt, kunt u nu aan die gids terugkeren om de toegangsgeloofsbrieven te produceren uniek aan [!DNL Privacy Service].

Gebruikend de Console van de Ontwikkelaar van Adobe, moet u de volgende drie toegangsgeloofsbrieven produceren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Uw `{IMS_ORG}` en `{API_KEY}` moeten slechts eenmaal worden geproduceerd en kunnen in toekomstige [!DNL Platform] API vraag opnieuw worden gebruikt. Uw `{ACCESS_TOKEN}` is echter tijdelijk en moet elke 24 uur opnieuw worden gegenereerd.

De stappen worden hieronder in detail besproken.

### Eenmalige installatie

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Volg vervolgens de stappen die worden beschreven in de zelfstudie over het maken van een leeg project](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de documentatie van de Adobe Developer Console.[

Zodra u een nieuw project hebt gecreeerd, uitgezocht **[!UICONTROL voeg API]** op **Overzicht van het Project** scherm toe.

![](images/api-authentication/add-api-button.png)

Het scherm **Add een API** verschijnt. Selecteer het productpictogram voor Adobe Experience Platform en kies **[!UICONTROL Experience Platform-API]** voordat u **[!UICONTROL Volgende]** selecteert.

![](images/api-authentication/add-platform-api.png)

Nadat u [!DNL Experience Platform] hebt geselecteerd als de API die aan het project moet worden toegevoegd, volgt u de stappen in de zelfstudie over [het toevoegen van een API aan een project met behulp van een serviceaccount (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (te beginnen bij de stap &quot;API configureren&quot;) om het proces te voltooien.

Zodra API aan het project is toegevoegd, **Project overzicht** de pagina toont de volgende geloofsbrieven die in alle vraag aan [!DNL Experience Platform] APIs worden vereist:

* `{API_KEY}` (Client-id)
* `{IMS_ORG}` (Organisatie-id)

![](./images/api-authentication/api-key-ims-org.png)

### Verificatie voor elke sessie

De laatste vereiste referentie die u moet verzamelen, is uw `{ACCESS_TOKEN}`. In tegenstelling tot de waarden voor `{API_KEY}` en `{IMS_ORG}`, moet om de 24 uur een nieuw token worden gegenereerd om te kunnen doorgaan met het gebruik van [!DNL Platform] API&#39;s.

Als u een nieuwe `{ACCESS_TOKEN}` wilt genereren, voert u de stappen uit om een JWT-token te genereren in de handleiding voor aanmeldgegevens van de ontwikkelaarsconsole.[](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md)

## Toegangsreferenties testen

Nadat u alle drie vereiste gegevens hebt verzameld, kunt u de volgende API-aanroep proberen te maken. Deze vraag zal van alle [!DNL Experience Data Model] (XDM) klassen binnen de container `global` van de Registratie van het Schema een lijst maken:

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

[](https://www.postman.com/) Postmanis is een populair hulpmiddel om met RESTful APIs te werken. In deze [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wordt beschreven hoe u een postman kunt instellen om automatisch JWT-verificatie uit te voeren en deze te gebruiken om Adobe Experience Platform API&#39;s te gebruiken.

## Volgende stappen

Door dit document te lezen, hebt u uw toegangsreferenties voor [!DNL Platform] API&#39;s verzameld en getest. U kunt nu de voorbeelden volgen die in [gids aan de slag voor Platform APIs](api-guide.md) worden verstrekt. Deze handleiding bevat koppelingen naar de API-hulplijnen voor elke service van het Platform en bevat aanvullende informatie. op fouten, Postman en JSON.

Naast de verificatiewaarden die u in deze zelfstudie hebt verzameld, vereisen veel [!DNL Platform] API&#39;s ook dat een geldige `{SANDBOX_NAME}` als koptekst wordt opgegeven. Zie het [overzicht van sandboxen](../sandboxes/home.md) voor meer informatie.