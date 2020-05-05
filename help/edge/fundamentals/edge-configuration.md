---
title: Edge-configuratie
seo-title: Edge-configuratie voor de Web SDK van het Experience Platform
description: 'Leer hoe te om het Netwerk van de Rand van het Platform van de Ervaring te vormen. '
seo-description: 'Leer hoe te om het Netwerk van de Rand van het Platform van de Ervaring te vormen. '
translation-type: tm+mt
source-git-commit: efbc080117754cee01f21c9f9ec409204648e757

---


# (bèta) Edge Configuration

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De configuratie voor het Adobe Experience Platform Web SDK is gesplitst naar twee locaties. Het [vormt bevel](configuring-the-sdk.md) in SDK controleert dingen die op de cliënt, zoals de `edgeDomain`. moeten worden behandeld. De randconfiguratie behandelt alle andere configuratie voor SDK. Wanneer een verzoek naar het Adobe Experience Platform Edge Network wordt verzonden, `edgeConfigId` wordt het gebruikt om naar de serverconfiguratie te verwijzen. Zo kunt u de configuratie bijwerken zonder dat u codewijzigingen op uw website hoeft aan te brengen.

## Een Edge-configuratie-id maken

De de configuratie IDs van de rand kan in Lancering worden gecreeerd gebruikend het hulpmiddel van de randconfiguratie. Met dit gereedschap kunt u zowel de randconfiguratie als omgevingen binnen die configuraties maken.

![Edge Configuration Tool navigation](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>Het gereedschap voor randconfiguratie is beschikbaar voor klanten met een whitelist, ongeacht of ze Launch gebruiken als tagbeheer. Bovendien vereisen gebruikers ontwikkelmachtigingen in Launch. Zie het artikel [Gebruikersmachtigingen](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html) in de documentatie bij Starten voor meer informatie.

U kunt een randconfiguratie tot stand brengen door op **[UICONTROL Nieuwe Configuratie]** van de Rand in het hoogste juiste gebied van het scherm te klikken. Nadat u een naam en een beschrijving hebt opgegeven, wordt u gevraagd om de standaardinstellingen voor elke omgeving.

### Standaardinstellingen voor omgeving

Deze standaardinstellingen worden gebruikt om de eerste drie omgevingen met identieke instellingen te maken. Deze drie omgevingen zijn dev, stage en prod. Ze komen overeen met de drie standaardomgevingen in Launch. Wanneer u een bibliotheek van de Lancering aan een ontwikkelomgeving bouwt, gebruikt de bibliotheek automatisch het dev milieu van uw configuratie. U kunt instellingen in afzonderlijke omgevingen naar wens bewerken.

De id die in de SDK als de id wordt gebruikt, `edgeConfigId` is een samengestelde id die de configuratie en de omgeving opgeeft. Als er geen omgeving is, wordt de productieomgeving gebruikt.

### Omgevingsinstellingen

Hieronder vindt u een van de instellingen die beschikbaar zijn voor een omgeving. De meeste secties kunnen worden in- of uitgeschakeld. Als deze optie is uitgeschakeld, worden de instellingen opgeslagen maar niet actief.

#### [!UICONTROL Identity]

Het identiteitsgedeelte is het enige gedeelte dat altijd ingeschakeld is. Er zijn twee beschikbare instellingen: ID Syncs Enabled en ID Sync Container ID.

![Het gedeelte Identiteit van de configuratie-interface](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID Sync Enabled]

Bepaalt of de SDK identiteitssyncs uitvoert met partners van derden.

##### [!UICONTROL ID Sync Container ID]

De syncs van identiteitskaart kunnen in containers worden gegroepeerd om verschillende syncs van identiteitskaart toe te laten om op verschillende tijden worden in werking gesteld. Dit controleert welke container van de syncs van identiteitskaart voor een bepaalde configuratieidentiteitskaart in werking wordt gesteld

#### Adobe Experience Platform

Met de hier vermelde instellingen kunt u gegevens naar het Adobe Experience Platform verzenden. Schakel deze sectie alleen in als u het Adobe Experience Platform hebt aangeschaft.

![Instellingenblok van Adobe Experience Platform](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

Sandboxen zijn locaties in het Adobe Experience Platform waarmee klanten hun gegevens en implementaties van elkaar kunnen isoleren. Meer informatie over hoe ze werken vindt u in de documentatie bij [Sandboxen](../../sandboxes/home.md).

##### [!UICONTROL Streaming Inlet]

Een streaminginlaat is een HTTP-bron in het Adobe Experience Platform. Deze worden onder het [!UICONTROL Sources] tabblad in het Adobe Experience Platform gemaakt als een HTTP-API.

##### [!UICONTROL Event Dataset]

De configuraties van de rand steunen verzendend gegevens naar datasets die een schema van klasse hebben [!UICONTROL Experience Event].

#### Adobe-doel

Als u Adobe Target wilt configureren, moet u een clientcode opgeven. De andere velden zijn optioneel.

![Adobe Target-instellingenblok](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>De organisatie die is gekoppeld aan de clientcode, moet overeenkomen met de organisatie waar de configuratie-id is gemaakt.

##### [!UICONTROL Client Code]

De unieke id voor een doelaccount. Als u dit wilt zoeken, navigeert u naar [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementation] > [!UICONTROL edit settings] naast de [!UICONTROL download] knop voor [!UICONTROL at.js] of [!UICONTROL mbox.js]

##### [!UICONTROL Property Token]

Het doel staat klanten toe om toestemmingen door het gebruik van eigenschappen te controleren. De details kunnen in de sectie van de Toestemmingen [van de](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) Onderneming van de Documentatie van het Doel worden gevonden.

Het eigenschapstoken vindt u in [!UICONTROL Adobe Target] > [!UICONTROL setup] > Eigenschappen [UICONTROL]

##### [!UICONTROL Target Environment ID]

[Met de omgevingen](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) in Adobe Target kunt u uw implementatie in alle ontwikkelingsfasen beheren. Deze instelling geeft aan welke omgeving u voor elke omgeving wilt gebruiken.

Adobe raadt u aan dit anders in te stellen voor elk van uw `dev`-, `stage`- en `prod` randconfiguratieomgevingen om de zaken eenvoudig te houden. Als u echter al een definitie hebt [!UICONTROL Adobe Target environments] opgegeven, kunt u deze gebruiken.

#### Adobe Audience Manager

U kunt deze sectie alleen inschakelen als u gegevens naar Adobe Audience Manager hebt verzonden. De andere instellingen zijn optioneel, maar worden aangemoedigd.

![Instellingenblok Adobe Audience Manage](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie Destinations Enabled]

Staat SDK toe om segmentinformatie via de Doelen [van het](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) Koekje van de Manager van het Publiek te delen.

##### [!UICONTROL URL Destinations Enabled]

Staat SDK toe om segmentinformatie via Doelen [URL](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)te delen. Deze worden gevormd in de Manager van het Publiek.

#### Adobe Analytics

Hiermee bepaalt u of gegevens naar Adobe Analytics worden verzonden. De extra details zijn in het Overzicht [van](../solution-specific/analytics/analytics-overview.md)Analytics.

![Adobe Analytics Settings Block](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Report Suite ID]

De rapportsuite vindt u in de sectie Adobe Analytics Admin onder [!UICONTROL Admin > ReportSuites]. Als de veelvoudige rapportreeksen worden gespecificeerd, dan worden de gegevens gekopieerd aan elke rapportreeks.
