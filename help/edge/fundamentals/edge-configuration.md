---
title: Edge-configuratie
seo-title: De configuratie van de rand voor het Web SDK van het Experience Platform
description: 'Leer hoe te om het Netwerk van de Rand van het Experience Platform te vormen. '
seo-description: 'Leer hoe te om het Netwerk van de Rand van het Experience Platform te vormen. '
keywords: configuration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: 94b3faf3157f4e1f4e46b6055914a04883dc44fa
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# De rand configureren

De configuratie voor Adobe Experience Platform Web SDK is verdeeld over twee plaatsen. [configure bevel](configuring-the-sdk.md) in SDK controleert dingen die op de cliënt, zoals `edgeDomain` moeten worden behandeld. De randconfiguratie behandelt alle andere configuratie voor SDK. Wanneer een verzoek naar het Adobe Experience Platform Edge Network wordt verzonden, wordt `edgeConfigId` gebruikt om naar de configuratie aan de serverzijde te verwijzen. Hierdoor kunt u de configuratie bijwerken zonder dat u codewijzigingen hoeft aan te brengen op uw website.

Voor deze functie moet uw organisatie zijn ingericht. Neem contact op met uw Customer Success Manager (CSM) om de lijst van gewenste personen te starten.

## Een Edge-configuratie maken

U kunt Edge-configuraties maken in Adobe [!DNL Experience Platform Launch] met het gereedschap voor randconfiguratie.

![Edge Configuration Tool navigation](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>Het hulpprogramma voor randconfiguratie is beschikbaar voor klanten op de lijst van gewenste personen, ongeacht of ze [!DNL Experience Platform Launch] als tagbeheer gebruiken. Bovendien, vereisen de gebruikers ontwikkeltoestemmingen in [!DNL Experience Platform Launch]. Zie het [User Permissions](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html) artikel in [!DNL Experience Platform Launch] documentatie voor meer details.

Creeer een randconfiguratie door op **[!UICONTROL Nieuwe Configuratie van de Rand]** in het hoogste juiste gebied van het scherm te klikken. Nadat u een naam en een beschrijving hebt opgegeven, wordt u gevraagd om de standaardinstellingen voor elke omgeving. De beschikbare instellingen worden hieronder beschreven.

Wanneer u een randconfiguratie maakt, worden er automatisch drie omgevingen met identieke instellingen gemaakt. Deze drie omgevingen zijn *dev*, *stage* en *prod*. Ze komen overeen met de drie standaardomgevingen in [!DNL Experience Platform Launch]. Wanneer u een [!DNL Experience Platform Launch] bibliotheek aan een ontwikkelomgeving bouwt, gebruikt de bibliotheek automatisch het dev milieu van uw configuratie. U kunt instellingen in afzonderlijke omgevingen naar wens bewerken.

De id die in de SDK als `edgeConfigId` wordt gebruikt, is een samengestelde id die de configuratie en de omgeving opgeeft (bijvoorbeeld `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Als er geen omgeving aanwezig is in de samengestelde id (bijvoorbeeld `stage` in het vorige voorbeeld), wordt de productieomgeving gebruikt.

Hieronder vindt u de beschikbare instellingen voor elke configuratieomgeving. De meeste secties kunnen worden in- of uitgeschakeld. Als deze optie is uitgeschakeld, worden de instellingen opgeslagen maar niet actief.

##  IdentitySettings

Het identiteitsgedeelte is het enige gedeelte dat altijd ingeschakeld is. Er zijn twee beschikbare instellingen: &quot;[!UICONTROL ID Syncs Enabled]&quot; en &quot;[!UICONTROL ID Sync Container ID]&quot;.

![Het gedeelte Identiteit van de configuratie-interface](../../assets/edge_configuration_identity.png)

### [!UICONTROL ID-synchronisatie ingeschakeld]

Bepaalt of de SDK identiteitssyncs uitvoert met partners van derden.

### [!UICONTROL ID Container-id synchroniseren]

De syncs van identiteitskaart kunnen in containers worden gegroepeerd om verschillende syncs van identiteitskaart toe te laten om op verschillende tijden worden in werking gesteld. Dit controleert welke container van de syncs van identiteitskaart voor een bepaalde configuratieidentiteitskaart in werking wordt gesteld

## Adobe Experience Platform-instellingen

Met de hier vermelde instellingen kunt u gegevens naar Adobe Experience Platform verzenden. Schakel deze sectie alleen in als u de Adobe Experience Platform hebt aangeschaft.

![Adobe Experience Platform-instellingenblok](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

Sandboxen zijn locaties in Adobe Experience Platform waarmee klanten hun gegevens en implementaties van elkaar kunnen isoleren. Zie de [Sandboxdocumentatie](../../sandboxes/home.md) voor meer informatie over hoe ze werken.

### [!UICONTROL Streaming-ingang]

Een streaminginlaat is een HTTP-bron in Adobe Experience Platform. Deze worden gecreeerd onder &quot;[!UICONTROL Bronnen]&quot;lusje in Adobe Experience Platform als HTTP API.

### [!UICONTROL Gebeurtenisgegevens]

Edge-configuraties ondersteunen het verzenden van gegevens naar gegevenssets met een schema van klasse [!UICONTROL Experience Event].

## Adobe Target-instellingen

Als u Adobe Target wilt configureren, moet u een clientcode opgeven. De andere velden zijn optioneel.

![Adobe Target-instellingenblok](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>De organisatie die is gekoppeld aan de clientcode, moet overeenkomen met de organisatie waar de configuratie-id is gemaakt.

### [!UICONTROL Clientcode]

De unieke id voor een doelaccount. Als u dit wilt zoeken, navigeert u naar [!UICONTROL Adobe Target] > [!UICONTROL Setup] [!UICONTROL Implementation] > [!UICONTROL Instellingen bewerken] naast de [!UICONTROL download]-knop voor [!UICONTROL at.js] of &lt;a1 2/>mbox.js][!UICONTROL 

### [!UICONTROL Eigenschapstoken]

[!DNL Target] staat klanten toe om toestemmingen door het gebruik van eigenschappen te controleren. Details vindt u in het gedeelte [Enterprise Permissions](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) van de [!DNL Target]-documentatie.

Het eigenschapstoken vindt u in [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Eigenschappen]

### [!UICONTROL Id doelomgeving]

[Met ](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) omgevingen in Adobe Target kunt u uw implementatie in alle ontwikkelingsfasen beheren. Deze instelling geeft aan welke omgeving u voor elke omgeving wilt gebruiken.

Adobe raadt u aan dit anders in te stellen voor elk van uw `dev`-, `stage`- en `prod`-randconfiguratieomgevingen om de zaken eenvoudig te houden. Als u echter al Adobe Target-omgevingen hebt gedefinieerd, kunt u deze gebruiken.

## Adobe Audience Manager-instellingen

U kunt deze sectie alleen inschakelen als u gegevens naar Adobe Audience Manager wilt verzenden. De andere instellingen zijn optioneel, maar worden aangemoedigd.

![Adobe Publiek beheren, instellingenblok](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie-doelen ingeschakeld]

Staat SDK toe om segmentinformatie via [Cookie Doelen](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) van [!DNL Audience Manager] te delen.

### [!UICONTROL URL-doelen ingeschakeld]

Staat SDK toe om segmentinformatie via [URL Doelen](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) te delen. Deze worden gevormd in [!DNL Audience Manager].

## Adobe Analytics-instellingen

Bepaalt of gegevens naar Adobe Analytics worden verzonden. De extra details zijn in [Overzicht Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics Settings Block](../../assets/edge_configuration_aa.png)

### [!UICONTROL Rapportsuite-id]

De rapportsuite vindt u in de sectie Adobe Analytics Admin onder [!UICONTROL Admin > ReportSuites]. Als de veelvoudige rapportreeksen worden gespecificeerd, dan worden de gegevens gekopieerd aan elke rapportreeks.
