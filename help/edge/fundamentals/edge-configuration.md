---
title: Edge-configuratie
seo-title: De configuratie van de rand voor het Web SDK van het Experience Platform
description: 'Leer hoe te om het Netwerk van de Rand van het Experience Platform te vormen. '
seo-description: 'Leer hoe te om het Netwerk van de Rand van het Experience Platform te vormen. '
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 1%

---


# De rand configureren

De configuratie voor het Adobe Experience Platform [!DNL Web SDK] wordt gesplitst tussen twee plaatsen. Het [vormt bevel](configuring-the-sdk.md) in SDK controleert dingen die op de cliënt, zoals de `edgeDomain`. moeten worden behandeld. De randconfiguratie behandelt alle andere configuratie voor SDK. Wanneer een verzoek naar het Adobe Experience Platform wordt verzonden [!DNL Edge Network], `edgeConfigId` wordt gebruikt om naar de server zijconfiguratie te verwijzen. Hierdoor kunt u de configuratie bijwerken zonder dat u codewijzigingen hoeft aan te brengen op uw website.

## Een Edge-configuratie-id maken

Edge-configuratie-id&#39;s kunnen in Adobe worden gemaakt [!DNL Launch] met het gereedschap voor randconfiguratie. Met dit gereedschap kunt u zowel de randconfiguratie als omgevingen binnen die configuraties maken.

![Edge Configuration Tool navigation](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>
>
>Het gereedschap voor randconfiguratie is beschikbaar voor klanten op de lijst van gewenste personen, ongeacht of ze [!DNL Launch] als tagbeheer gebruiken. Bovendien vereisen gebruikers ontwikkelmachtigingen in [!DNL Launch]. Zie het artikel [Gebruikersmachtigingen](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html) in de [!DNL Launch] documentatie voor meer informatie.

U kunt een randconfiguratie tot stand brengen door op **[!UICONTROL Nieuwe Configuratie]** van de Rand in het hoogste juiste gebied van het scherm te klikken. Nadat u een naam en een beschrijving hebt opgegeven, wordt u gevraagd om de standaardinstellingen voor elke omgeving.

### Standaardinstellingen voor omgeving

Deze standaardinstellingen worden gebruikt om de eerste drie omgevingen met identieke instellingen te maken. Deze drie omgevingen zijn *dev*, *stage* en *prod*. Ze komen overeen met de drie standaardomgevingen in [!DNL Launch]. Wanneer u een [!DNL Launch] bibliotheek aan een ontwikkelomgeving bouwt, gebruikt de bibliotheek automatisch het dev milieu van uw configuratie. U kunt instellingen in afzonderlijke omgevingen naar wens bewerken.

De id die in de SDK als de id wordt gebruikt, `edgeConfigId` is een samengestelde id die de configuratie en de omgeving opgeeft. Als er geen omgeving is, wordt de productieomgeving gebruikt.

### Omgevingsinstellingen

Hieronder vindt u een van de instellingen die beschikbaar zijn voor een omgeving. De meeste secties kunnen worden in- of uitgeschakeld. Als deze optie is uitgeschakeld, worden de instellingen opgeslagen maar niet actief.

#### [!UICONTROL Identiteit]

Het identiteitsgedeelte is het enige gedeelte dat altijd ingeschakeld is. Er zijn twee beschikbare instellingen: [!UICONTROL ID Syncs Enabled] en [!UICONTROL ID Sync Container ID].

![Het gedeelte Identiteit van de configuratie-interface](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID-synchronisatie ingeschakeld]

Bepaalt of de SDK identiteitssyncs uitvoert met partners van derden.

##### [!UICONTROL ID Container-id synchroniseren]

De syncs van identiteitskaart kunnen in containers worden gegroepeerd om verschillende syncs van identiteitskaart toe te laten om op verschillende tijden worden in werking gesteld. Dit controleert welke container van de syncs van identiteitskaart voor een bepaalde configuratieidentiteitskaart in werking wordt gesteld

#### Adobe Experience Platform

Met de hier vermelde instellingen kunt u gegevens naar het Adobe Experience Platform verzenden. Schakel deze sectie alleen in als u het Adobe Experience Platform hebt aangeschaft.

![Adobe Experience Platform-instellingenblok](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

Sandboxen zijn locaties in het Adobe Experience Platform waarmee klanten hun gegevens en implementaties van elkaar kunnen isoleren. Raadpleeg de documentatie bij [Sandboxen voor meer informatie over hoe ze werken](../../sandboxes/home.md).

##### [!UICONTROL Streaming-ingang]

Een streaminginlaat is een HTTP-bron in het Adobe Experience Platform. Deze worden gecreeerd onder het [!UICONTROL Bronlusje] in het Adobe Experience Platform als HTTP API.

##### [!UICONTROL Gebeurtenisgegevens]

De configuraties van de rand steunen verzendend gegevens naar datasets die een schema van de Gebeurtenis [!UICONTROL van de]Ervaring van de klasse hebben.

#### Adobe Target

Als u Adobe Target wilt configureren, moet u een clientcode opgeven. De andere velden zijn optioneel.

![Adobe Target-instellingenblok](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>
>
>De organisatie die is gekoppeld aan de clientcode, moet overeenkomen met de organisatie waar de configuratie-id is gemaakt.

##### [!UICONTROL Clientcode]

De unieke id voor een doelaccount. Als u dit wilt zoeken, navigeert u naar [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementatie] > Instellingen  bewerken naast de knop [!UICONTROL Downloaden]  [!UICONTROL voor ofwelat.jsofmbox.js]

##### [!UICONTROL Eigenschapstoken]

[!DNL Target] staat klanten toe om toestemmingen door het gebruik van eigenschappen te controleren. Details vindt u in de sectie [Enterprise Permissions](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) van de [!DNL Target] documentatie.

De eigenschap token vindt u in [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Eigenschappen]

##### [!UICONTROL Target Environment ID]

[Met omgevingen](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) in Adobe Target kunt u uw implementatie in alle ontwikkelingsstadia beheren. Deze instelling geeft aan welke omgeving u voor elke omgeving wilt gebruiken.

Adobe raadt u aan dit anders in te stellen voor elk van uw `dev`-, `stage`- en `prod` randconfiguratieomgevingen om de zaken eenvoudig te houden. Als u echter al [!UICONTROL Adobe Target-omgevingen] hebt gedefinieerd, kunt u deze gebruiken.

#### Adobe Audience Manager

Alles wat nodig is om gegevens naar de Adobe Audience Manager te verzenden, moet deze sectie inschakelen. De andere instellingen zijn optioneel, maar worden aangemoedigd.

![Instellingenblok Adobe Audience Manage](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie-doelen ingeschakeld]

Staat SDK toe om segmentinformatie via de Doelen [van het](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) Koekje van te delen [!DNL Audience Manager].

##### [!UICONTROL URL-doelen ingeschakeld]

Staat SDK toe om segmentinformatie via Doelen [URL](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)te delen. Deze worden gevormd in [!DNL Audience Manager].

#### Adobe Analytics

Hiermee bepaalt u of gegevens naar Adobe Analytics worden verzonden. Meer informatie vindt u in het overzicht [van](../solution-specific/analytics/analytics-overview.md)Analytics.

![Adobe Analytics Settings Block](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Rapportsuite-id]

De rapportsuite vindt u in de sectie Adobe Analytics Admin onder [!UICONTROL Admin > ReportSuites]. Als de veelvoudige rapportreeksen worden gespecificeerd, dan worden de gegevens gekopieerd aan elke rapportreeks.
