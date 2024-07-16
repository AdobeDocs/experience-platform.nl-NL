---
description: Op deze pagina wordt beschreven hoe u Adobe Experience Platform Destination SDK kunt verifiëren en gebruiken. Het omvat instructies op hoe te om de authentificatiegeloofsbrieven van de Adobe I/O, een zandbaknaam, en de toestemming van de bestemmings auteurstoegang te verkrijgen.
title: Aan de slag met Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Aan de slag

## Overzicht {#overview}

Op deze pagina wordt beschreven hoe u Adobe Experience Platform Destination SDK kunt verifiëren en gebruiken. Het omvat instructies op hoe te om de authentificatiegeloofsbrieven van de Adobe I/O, een zandbaknaam, en de toestemming van de bestemmings auteurstoegang te verkrijgen.

## Terminologie {#terminology}

Deze gids gebruikt Platform-specifieke concepten, zoals organisatie en zandbakken. Raadpleeg de [ verklarende woordenlijst van het Experience Platform ](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) voor definities van deze en andere termijnen.

## Verkrijg vereiste authentificatiegeloofsbrieven {#obtain-authentication-credentials}

Destination SDK gebruikt de [ Adobe I/O ](https://www.adobe.io/) gateway voor authentificatie. Om API vraag aan Destination SDK eindpunten te maken, moet u bepaalde kopballen in uw API vraag verstrekken. Het werk met het team van de Adobe Exchange aan opstellingsauthentificatie voor u aan [ Adobe Developer Console ](https://developer.adobe.com/console).

Om vraag aan Destination SDK API eindpunten met succes te maken, volg het [ de authentificatieleerprogramma van het Experience Platform ](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). Begin het leerprogramma van &quot;[ produceert een API sleutel, organisatie identiteitskaart, en cliënt geheim ](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot;stap. Het team van de Adobe Exchange zal de vorige stappen voor u behandelen. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in Destination SDK API-aanroepen, zoals hieronder wordt getoond:

* `x-api-key: {API_KEY}`, ook wel client-id genoemd
* `x-gw-ims-org-id: {ORG_ID}`, ook bekend als organisatie-id
* `Authorization: Bearer {ACCESS_TOKEN}`. Het toegangstoken heeft een vervaltijd van 24 uren, die in milliseconden wordt uitgedrukt, zodat zult u het moeten verfrissen. Om het toegangstoken te verfrissen, herhaal de stappen die in het authentificatieleerprogramma worden geschetst.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Eigendom van bestemming en sandboxen {#destination-ownership}

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Verzoeken om Destination SDK vereisen kopballen die de naam van de zandbak specificeren de verrichting in plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Het team van de Adobe Exchange voorziet u van uw zandbaknaam, die u in vraag aan de Destination SDK API eindpunten moet gebruiken.

## Rolgebaseerde toegangscontrole (RBAC) {#rbac}

Om de Destination SDK API eindpunten te gebruiken die in de [ verwijzingsdocumentatie ](functionality/configuration-options.md) worden beschreven, hebt u de **[!UICONTROL Destination Authoring]** toegangsbeheertoestemming nodig. Het werk met het team van de Adobe Exchange om deze toestemming te krijgen die aan u in [ wordt toegewezen Adobe Admin Console ](https://adminconsole.adobe.com/).

![ Authoring toestemming van de Bestemming ](./assets/destination-authoring-permission.png)

Lees voor meer informatie de volgende documenten van het Toegangsbeheer van het Experience Platform:

* [Rechten voor een productprofiel beheren](/help/access-control/ui/permissions.md)
* [Beschikbare machtigingen voor Experience Platform](/help/access-control/home.md#permissions)
* [ documentatie van Adobe Admin Console ](https://helpx.adobe.com/nl/enterprise/using/admin-console.html)

## Aanvullende overwegingen {#additional-considerations}

* Voor geproduceerde/openbare bestemmingen, om het even welke veranderingen die u aan bestemmingsconfiguraties aanbrengt, of u creeert of een bestemmingsconfiguratie uitgeeft, moet door Adobe worden herzien en worden goedgekeurd. Uw veranderingen worden weerspiegeld in uw bestemmingen slechts nadat het overzicht wordt gedaan. Dit geldt niet voor particuliere bestemmingen die alleen voor u beschikbaar zijn.
* Alleen de gebruikers die tot dezelfde organisatie behoren en toegang hebben tot de sandbox, kunnen de doelconfiguratie bewerken.

## Volgende stappen {#next-steps}

Door de stappen in dit artikel te volgen, hebt u authentificatiegeloofsbrieven aan Adobe I/O, een zandbaknaam, en de toestemming van de bestemmings authoring toegangscontrole verkregen. Vervolgens kunt u een bestemming instellen met behulp van Destination SDK.

* Lees de volgende configuratiegidsen, afhankelijk van uw bestemmingstype:

   * [Gebruik Destination SDK om een streamingbestemming te configureren](guides/configure-destination-instructions.md)
   * [Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren](guides/configure-file-based-destination-instructions.md)

* Voor alle verrichtingen, verwijs naar de [ Authoring API documentatie van de Bestemming ](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Gebruik de [ Authoring API van de Bestemming de inzameling van Postman ](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) om uw bestemming te vormen gebruikend de Destination SDK API eindpunten. Om met Postman begonnen te worden, zie de [ stappen voor het invoeren van milieu&#39;s en inzamelingen ](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) en a [ videogids voor het creëren van het milieu van Postman ](https://video.tv.adobe.com/v/28832).
