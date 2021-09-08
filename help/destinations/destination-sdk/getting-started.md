---
description: Op deze pagina wordt beschreven hoe u de Adobe Experience Platform Destination SDK kunt verifiëren en gebruiken. Het omvat instructies op hoe te om de authentificatiegeloofsbrieven van de Adobe I/O, een zandbaknaam, en de toestemming van de bestemmings auteurstoegang te verkrijgen.
title: Aan de slag met de SDK van Doel
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# Aan de slag

## Overzicht {#overview}

Op deze pagina wordt beschreven hoe u de Adobe Experience Platform Destination SDK kunt verifiëren en gebruiken. Het omvat instructies op hoe te om de authentificatiegeloofsbrieven van de Adobe I/O, een zandbaknaam, en de toestemming van de bestemmings auteurstoegang te verkrijgen.

## Terminologie {#terminology}

Deze handleiding gebruikt Platform-specifieke concepten, zoals IMS-organisatie en sandboxen. Raadpleeg [Experience Platform glossary](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) voor definities van deze en andere termen.

## Verkrijg vereiste authentificatiegeloofsbrieven {#obtain-authentication-credentials}

De bestemming SDK gebruikt [Adobe I/O](https://www.adobe.io/) gateway voor authentificatie. Om API vraag aan de eindpunten van SDK van de Bestemming te maken, moet u bepaalde kopballen in uw API vraag verstrekken. Werk met het team van de Uitwisseling van de Adobe aan opstellingsauthentificatie voor u aan [de Console van de Ontwikkelaar ](http://console.adobe.io/) van de Adobe.

Om met succes vraag aan de eindpunten van SDK API van de Bestemming te maken, volg [Experience Platform authentificatiezelfstudie](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). Start de zelfstudie vanuit de stap &quot;[Genereer een API-sleutel, IMS Org-id en clientgeheim](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot;. Het team van de Uitwisseling van Adobe zal de vorige stappen voor u behandelen. Het voltooien van het authentificatieleerprogramma verstrekt de waarden voor elk van de vereiste kopballen in de vraag van SDK API van de Bestemming, zoals hieronder getoond:

* `x-api-key: {API_KEY}`, ook wel client-id genoemd
* `x-gw-ims-org-id: {IMS_ORG}`, ook bekend als organisatie-id
* `Authorization: Bearer {ACCESS_TOKEN}`. Het toegangstoken heeft een vervaltijd van 24 uren, die in milliseconden wordt uitgedrukt, zodat zult u het moeten verfrissen. Om het toegangstoken te verfrissen, herhaal de stappen die in het authentificatieleerprogramma worden geschetst.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {IMS_ORG}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Eigendom van bestemming en sandboxen {#destination-ownership}

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Verzoeken naar de SDK van de Bestemming vereisen kopballen die de naam van de zandbak specificeren de verrichting in plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Het team van de Uitwisseling van Adobe voorziet u van uw zandbaknaam, die u in vraag aan de eindpunten van SDK API van de Bestemming moet gebruiken.

## Rolgebaseerde toegangscontrole (RBAC) {#rbac}

Om de eindpunten van SDK API van de Bestemming te gebruiken die in [verwijzingsdocumentatie](./configuration-options.md) worden beschreven, hebt u **[!UICONTROL Destination Authoring]** toegangsbeheertoestemming nodig. Werk met het team van de Uitwisseling van de Adobe om deze toestemming te krijgen die aan u in [Adobe Admin Console](https://adminconsole.adobe.com/) wordt toegewezen.

![Machtiging voor ontwerpen van bestemming](./assets/destination-authoring-permission.png)

Lees voor meer informatie de volgende documenten van het Toegangsbeheer van het Experience Platform:

* [Rechten voor een productprofiel beheren](/help/access-control/ui/permissions.md)
* [Beschikbare machtigingen voor Experience Platform](/help/access-control/home.md#permissions)
* [Adobe Admin Console-documentatie](https://helpx.adobe.com/nl/enterprise/using/admin-console.html)

## Aanvullende overwegingen {#additional-considerations}

* Om het even welke veranderingen die u aan bestemmingsconfiguraties aanbrengt, of u creeert of een bestemmingsconfiguratie uitgeeft, moet door Adobe worden herzien en worden goedgekeurd. Uw veranderingen worden weerspiegeld in uw bestemmingen slechts nadat het overzicht wordt gedaan.
* Alleen de gebruikers die tot dezelfde organisatie behoren en toegang hebben tot de sandbox, kunnen de doelconfiguratie bewerken.

## Volgende stappen {#next-steps}

Door de stappen in dit artikel te volgen, hebt u authentificatiegeloofsbrieven aan Adobe I/O, een zandbaknaam, en de toestemming van de bestemmings authoring toegangscontrole verkregen. Vervolgens kunt u een bestemming instellen met de SDK van Doel. Lees [Gebruik de Doel SDK om uw bestemming](./configure-destination-instructions.md) voor volgende stappen te vormen.
