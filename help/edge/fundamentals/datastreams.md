---
title: Vorm uw DataStream voor het Web SDK van het Experience Platform
description: 'Leer hoe u de gegevensstromen configureert. '
keywords: configuratie;gegevensstreams;datastreamId;edge;datastream id;Environment Settings;edgeConfigId;identity;id sync ingeschakeld;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Dodes;url Doelen;Analytics Settings Blockreport suite id;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 012ebbadc7149747df1414360eca6451836d6bbc
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---


# Een gegevensstroom configureren

De configuratie voor Adobe Experience Platform Web SDK is verdeeld over twee plaatsen. De [configureren, opdracht](configuring-the-sdk.md) in SDK controleert dingen die op de cliënt, zoals moeten worden behandeld `edgeDomain`. De stromen van gegevens behandelen alle andere configuraties voor SDK. Wanneer een aanvraag naar het Adobe Experience Platform Edge-netwerk wordt verzonden, `edgeConfigId` wordt gebruikt om naar de serverzijconfiguratie te verwijzen. Hierdoor kunt u de configuratie bijwerken zonder dat u codewijzigingen hoeft aan te brengen op uw website.

Voor deze functie moet uw organisatie zijn ingericht. Neem contact op met uw Customer Success Manager (CSM) om de lijst van gewenste personen te starten.

## Een gegevensstroomconfiguratie maken

U kunt gegevensstromen in de UI van de Inzameling van Gegevens tot stand brengen en beheren door te selecteren **[!UICONTROL Datastreams]** in de linkernavigatie.

![gegevensstromen, gereedschapnavigatie](../images/datastreams/config.png)

>[!NOTE]
>
>Terwijl u toegang hebt tot [!UICONTROL Datastreams] , ongeacht of u de mogelijkheden voor tagbeheer van Platform gebruikt, hebt u ontwikkelaarmachtigingen nodig om gegevensstromen zelf te beheren. Zie de [gebruikersmachtigingen](../../tags/ui/administration/user-permissions.md) artikel in de tagdocumentatie voor meer informatie.

Een gegevensstroom maken door op **[!UICONTROL New Datastream]** in de rechterbovenhoek van het scherm. Nadat u een naam en een beschrijving hebt opgegeven, wordt u gevraagd om de standaardinstellingen voor elke omgeving. De beschikbare instellingen worden hieronder beschreven.

Bij het maken van een gegevensstroom worden automatisch drie omgevingen met identieke instellingen gemaakt. Deze drie omgevingen zijn *dev*, *stadium*, en *prod*. Ze komen overeen met de drie standaardomgevingen voor tags. Wanneer u een markeringsbibliotheek aan een ontwikkelomgeving bouwt, gebruikt de bibliotheek automatisch het dev milieu van uw configuratie. U kunt instellingen in afzonderlijke omgevingen naar wens bewerken.

De id die in de SDK wordt gebruikt als de `edgeConfigId` is een samengestelde identiteitskaart die de configuratie en het milieu specificeert (bijvoorbeeld `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Als er geen omgeving aanwezig is in de samengestelde id (bijvoorbeeld `stage` in het vorige voorbeeld) wordt de productieomgeving gebruikt.

Hieronder vindt u de beschikbare instellingen voor elke configuratieomgeving. De meeste secties kunnen worden in- of uitgeschakeld. Als deze optie is uitgeschakeld, worden de instellingen opgeslagen maar niet actief.

## [!UICONTROL Third Party ID] instellingen

De sectie met de id van derden is de enige sectie die altijd is ingeschakeld. Er zijn twee beschikbare instellingen: &quot;[!UICONTROL Third Party ID Sync Enabled]&quot; en &quot;[!UICONTROL Third Party ID Sync Container ID]&quot;.

![Het gedeelte Identiteit van de configuratie-interface](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Third Party ID Sync Enabled]

Bepaalt of de SDK identiteitssyncs uitvoert met partners van derden.

### [!UICONTROL Third Party ID Sync Container ID]

De syncs van identiteitskaart kunnen in containers worden gegroepeerd om verschillende syncs van identiteitskaart toe te laten om op verschillende tijden worden in werking gesteld. Dit controleert welke container van de syncs van identiteitskaart voor een bepaalde configuratieidentiteitskaart in werking wordt gesteld

## Adobe Experience Platform-instellingen

Met de hier vermelde instellingen kunt u gegevens naar Adobe Experience Platform verzenden. Schakel deze sectie alleen in als u de Adobe Experience Platform hebt aangeschaft.

![Adobe Experience Platform-instellingenblok](../images/datastreams/platform-config.png)

| Veld | Beschrijving |
| --- | --- |
| [!UICONTROL Sandbox] | **(Vereist)** Selecteer de sandbox met Platforms waarnaar u gegevens wilt verzenden. Sandboxen zijn virtuele partities in Adobe Experience Platform waarmee u uw gegevens en implementaties kunt isoleren van die in uw organisatie.<br><br>Wanneer een gegevensstroom is gemaakt, kan de sandbox niet meer worden gewijzigd. De [!UICONTROL Sandbox] selectieveld is daarom niet beschikbaar bij het bewerken van een bestaande gegevensstroom.<br><br>Zie voor meer informatie over de rol van sandboxen in Experience Platform de klasse [sandboxdocumentatie](../../sandboxes/home.md). |
| [!UICONTROL Event Dataset] | **(Vereist)** Selecteer de dataset van het Platform dat de gegevens van de klantengebeurtenis zullen worden gestroomd aan. Dit schema moet de [XDM ExperienceEvent, klasse](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Profile Dataset] | Selecteer de dataset van het Platform dat de gegevens van de klantenattributen zullen worden verzonden naar. Dit schema moet de [Afzonderlijke XDM-profielklasse](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Selecteer dit checkbox om Offer decisioning voor een implementatie van SDK van het Web van het Platform toe te laten. Zie de handleiding op [het gebruiken van Offer decisioning met het Web SDK van het Platform](../personalization/offer-decisioning/offer-decisioning-overview.md) voor meer details over de implementatie. Raadpleeg voor meer informatie over de mogelijkheden van Offer decisioning de [Adobe Journey Optimizer-documentatie](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=nl). |
| [!UICONTROL Edge Segmentation] | Schakel dit selectievakje in om in te schakelen [randsegmentatie](../../segmentation/ui/edge-segmentation.md) voor deze gegevensstroom. Wanneer het Web SDK van het Platform gegevens door een rand-segmentation-Toegelaten gegevensstroom verzendt, worden om het even welke bijgewerkte segmentlidmaatschap voor het profiel in kwestie teruggestuurd in de reactie.<br><br>Deze optie kan in combinatie met [!UICONTROL Personalization Destinations] for [gebruiksgevallen voor personalisatie op de volgende pagina](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Personalization Destinations] | Indien gebruikt in combinatie met [!UICONTROL Edge Segmentation] Schakel deze optie in om de datastream verbinding te laten maken met personaliseringsengines zoals Adobe Target. Raadpleeg de documentatie bij bestemmingen voor specifieke stappen over [het vormen verpersoonlijkingsbestemmingen](../../destinations/ui/configure-personalization-destinations.md). |

## Adobe Target-instellingen

Als u Adobe Target wilt configureren, moet u een clientcode opgeven. De andere velden zijn optioneel.

![Adobe Target-instellingenblok](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>De organisatie die is gekoppeld aan de clientcode, moet overeenkomen met de organisatie waar de configuratie-id is gemaakt.

### [!UICONTROL Client Code]

De unieke id voor een doelaccount. Als u dit wilt zoeken, navigeert u naar [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementation] > [!UICONTROL edit settings] naast de [!UICONTROL download] knop voor een van beide [!UICONTROL at.js] of [!UICONTROL mbox.js]

### [!UICONTROL Property Token]

[!DNL Target] staat klanten toe om toestemmingen door het gebruik van eigenschappen te controleren. Details vindt u in het gedeelte [Bedrijfsmachtigingen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) van de [!DNL Target] documentatie.

Het eigenschapstoken vindt u in [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

### [!UICONTROL Target Environment ID]

[Omgevingen](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) in Adobe Target helpt u uw implementatie in alle ontwikkelingsstadia te beheren. Deze instelling geeft aan welke omgeving u voor elke omgeving wilt gebruiken.

Adobe raadt u aan dit voor elk van uw `dev`, `stage`, en `prod` gegevensstroomomgevingen om dingen eenvoudig te houden. Als u echter al Adobe Target-omgevingen hebt gedefinieerd, kunt u deze gebruiken.

## Adobe Audience Manager-instellingen

U kunt deze sectie alleen inschakelen als u gegevens naar Adobe Audience Manager wilt verzenden. De andere instellingen zijn optioneel, maar worden aangemoedigd.

![Adobe Publiek beheren, instellingenblok](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Cookie Destinations Enabled]

Staat SDK toe om segmentinformatie via te delen [Cookie-doelen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) van [!DNL Audience Manager].

### [!UICONTROL URL Destinations Enabled]

Staat SDK toe om segmentinformatie via te delen [URL-doelen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Deze zijn geconfigureerd in [!DNL Audience Manager].

## Adobe Analytics-instellingen

Bepaalt of gegevens naar Adobe Analytics worden verzonden. Meer informatie vindt u in het gedeelte [Overzicht van analysemogelijkheden](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics-instellingen blokkeren](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL Report Suite ID]

De rapportsuite vindt u in de sectie Adobe Analytics Admin onder [!UICONTROL Admin > ReportSuites]. Als de veelvoudige rapportreeksen worden gespecificeerd, dan worden de gegevens gekopieerd aan elke rapportreeks.
