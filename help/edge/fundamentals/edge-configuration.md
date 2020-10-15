---
title: Edge-configuratie
seo-title: De configuratie van de rand voor het Web SDK van het Experience Platform
description: 'Leer hoe te om het Netwerk van de Rand van het Experience Platform te vormen. '
seo-description: 'Leer hoe te om het Netwerk van de Rand van het Experience Platform te vormen. '
keywords: configuration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: d069b3007265406367ca9de2b85540b2a070cf36
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---


# De rand configureren

De configuratie voor de Adobe Experience Platform [!DNL Web SDK] wordt gesplitst tussen twee plaatsen. Het [vormt bevel](configuring-the-sdk.md) in SDK controleert dingen die op de cliënt, zoals de `edgeDomain`. moeten worden behandeld. De randconfiguratie behandelt alle andere configuratie voor SDK. Wanneer een verzoek naar de Adobe Experience Platform wordt verzonden [!DNL Edge Network], `edgeConfigId` wordt het gebruikt om naar de server zijconfiguratie te verwijzen. Hierdoor kunt u de configuratie bijwerken zonder dat u codewijzigingen hoeft aan te brengen op uw website.

Voor deze functie moet uw organisatie zijn ingericht. Neem contact op met uw Certified Software Manager (CSM) om de lijst van gewenste personen te starten.

## Een Edge-configuratie-id maken

De de configuratie IDs van de rand kan in Adobe worden gecreeerd [!DNL Experience Platform Launch] gebruikend het hulpmiddel van de randconfiguratie. Met dit gereedschap kunt u zowel de randconfiguratie als omgevingen binnen die configuraties maken.

![Edge Configuration Tool navigation](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>Het gereedschap voor randconfiguratie is beschikbaar voor klanten op de lijst van gewenste personen, ongeacht of ze [!DNL Experience Platform Launch] als tagbeheer gebruiken. Bovendien vereisen gebruikers ontwikkelmachtigingen in [!DNL Experience Platform Launch]. Zie het artikel [Gebruikersmachtigingen](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html) in de [!DNL Experience Platform Launch] documentatie voor meer informatie.

U kunt een randconfiguratie tot stand brengen door op **[!UICONTROL Nieuwe Configuratie]** van de Rand in het hoogste juiste gebied van het scherm te klikken. Nadat u een naam en een beschrijving hebt opgegeven, wordt u gevraagd om de standaardinstellingen voor elke omgeving.

### Standaardomgevingen

Deze standaardinstellingen worden gebruikt om de eerste drie omgevingen met identieke instellingen te maken. Deze drie omgevingen zijn *dev*, *stage* en *prod*. Ze komen overeen met de drie standaardomgevingen in [!DNL Experience Platform Launch]. Wanneer u een [!DNL Experience Platform Launch] bibliotheek aan een ontwikkelomgeving bouwt, gebruikt de bibliotheek automatisch het dev milieu van uw configuratie. U kunt instellingen in afzonderlijke omgevingen naar wens bewerken.

De id die in de SDK als de id wordt gebruikt, `edgeConfigId` is een samengestelde id die de configuratie en de omgeving opgeeft. Als er geen omgeving is, wordt de productieomgeving gebruikt.

### Omgevingsinstellingen

Hieronder vindt u een van de instellingen die beschikbaar zijn voor een omgeving. De meeste secties kunnen worden in- of uitgeschakeld. Als deze optie is uitgeschakeld, worden de instellingen opgeslagen maar niet actief.

#### [!UICONTROL Identiteit]

Het identiteitsgedeelte is het enige gedeelte dat altijd ingeschakeld is. Er zijn twee beschikbare instellingen: &quot;[!UICONTROL ID Syncs Enabled]&quot; en &quot;[!UICONTROL ID Sync Container ID]&quot;.

![Het gedeelte Identiteit van de configuratie-interface](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID-synchronisatie ingeschakeld]

Bepaalt of de SDK identiteitssyncs uitvoert met partners van derden.

##### [!UICONTROL ID Container-id synchroniseren]

De syncs van identiteitskaart kunnen in containers worden gegroepeerd om verschillende syncs van identiteitskaart toe te laten om op verschillende tijden worden in werking gesteld. Dit controleert welke container van de syncs van identiteitskaart voor een bepaalde configuratieidentiteitskaart in werking wordt gesteld

#### Adobe Experience Platform

Met de hier vermelde instellingen kunt u gegevens naar de Adobe Experience Platform verzenden. Schakel deze sectie alleen in als u de Adobe Experience Platform hebt aangeschaft.

![Adobe Experience Platform-instellingenblok](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

Sandboxen zijn locaties in de Adobe Experience Platform die klanten in staat stellen hun gegevens en implementaties van elkaar te isoleren. Raadpleeg de documentatie bij [Sandboxen voor meer informatie over hoe ze werken](../../sandboxes/home.md).

##### [!UICONTROL Streaming-ingang]

Een streaminginlaat is een HTTP-bron in de Adobe Experience Platform. Deze worden gemaakt onder het tabblad &quot;[!UICONTROL Bronnen]&quot; in de Adobe Experience Platform als een HTTP-API.

##### [!UICONTROL Gebeurtenisgegevens]

De configuraties van de rand steunen verzendend gegevens naar datasets die een schema van de Gebeurtenis [!UICONTROL van de]Ervaring van de klasse hebben.

#### Adobe Target

Als u Adobe Target wilt configureren, moet u een clientcode opgeven. De andere velden zijn optioneel.

![Adobe Target-instellingenblok](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>De organisatie die is gekoppeld aan de clientcode, moet overeenkomen met de organisatie waar de configuratie-id is gemaakt.

##### [!UICONTROL Clientcode]

De unieke id voor een doelaccount. Als u dit wilt zoeken, navigeert u naar [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementatie] > Instellingen  bewerken naast de knop [!UICONTROL Downloaden]  [!UICONTROL voor ofwelat.jsofmbox.js]

##### [!UICONTROL Eigenschapstoken]

[!DNL Target] staat klanten toe om toestemmingen door het gebruik van eigenschappen te controleren. Details vindt u in de sectie [Enterprise Permissions](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) van de [!DNL Target] documentatie.

De eigenschap token vindt u in [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Eigenschappen]

##### [!UICONTROL Id doelomgeving]

[Met omgevingen](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) in Adobe Target kunt u uw implementatie in alle ontwikkelingsstadia beheren. Deze instelling geeft aan welke omgeving u voor elke omgeving wilt gebruiken.

Adobe raadt u aan dit anders in te stellen voor elk van uw `dev`-, `stage`- en `prod` randconfiguratieomgevingen om de zaken eenvoudig te houden. Als u echter al Adobe Target-omgevingen hebt gedefinieerd, kunt u deze gebruiken.

#### Adobe Audience Manager

U kunt deze sectie alleen inschakelen als u gegevens naar Adobe Audience Manager wilt verzenden. De andere instellingen zijn optioneel, maar worden aangemoedigd.

![Adobe Publiek beheren, instellingenblok](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie-doelen ingeschakeld]

Staat SDK toe om segmentinformatie via de Doelen [van het](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) Koekje van te delen [!DNL Audience Manager].

##### [!UICONTROL URL-doelen ingeschakeld]

Staat SDK toe om segmentinformatie via Doelen [URL](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)te delen. Deze worden gevormd in [!DNL Audience Manager].

#### Adobe Analytics

Bepaalt of gegevens naar Adobe Analytics worden verzonden. De extra details zijn in het Overzicht [van](../data-collection/adobe-analytics/analytics-overview.md)Analytics.

![Adobe Analytics Settings Block](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Rapportsuite-id]

De rapportsuite vindt u in de sectie Adobe Analytics Admin onder [!UICONTROL Beheer > ReportSuites]. Als de veelvoudige rapportreeksen worden gespecificeerd, dan worden de gegevens gekopieerd aan elke rapportreeks.
