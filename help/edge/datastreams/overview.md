---
title: Overzicht gegevensstromen
description: Sluit de integratie van uw client-side Experience Platform SDK aan op Adobe-producten en andere doelen.
keywords: configuratie;gegevensstreams;datastreamId;edge;datastream id;Environment Settings;edgeConfigId;identity;id sync ingeschakeld;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;clientcode;Eigenschapcontrole;Doel-id;Cookie-doelen;url-doelen;Analytics Settings Blockreport suite ID;Data Prep;Data Prep;Mapper XDM Mapper;Mapper on Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '1687'
ht-degree: 1%

---

# Overzicht gegevensstromen

Een gegevensstroom vertegenwoordigt de server-zijconfiguratie wanneer het uitvoeren van het Web van Adobe Experience Platform en Mobiele SDKs. Terwijl de [configureren, opdracht](../fundamentals/configuring-the-sdk.md) in SDK controleert dingen die op de cliënt (zoals moeten worden behandeld `edgeDomain`), worden in gegevensstreams alle andere configuraties voor de SDK afgehandeld. Wanneer een aanvraag naar het Adobe Experience Platform Edge-netwerk wordt verzonden, `edgeConfigId` wordt gebruikt om naar de gegevensstroom te verwijzen. Hierdoor kunt u de serverconfiguratie bijwerken zonder dat u codewijzigingen hoeft aan te brengen op uw website.

In dit document worden de stappen beschreven voor het configureren van een gegevensstroom in de gebruikersinterface voor gegevensverzameling.

>[!NOTE]
>
>Uw organisatie moet voor deze eigenschap worden voorzien om tot het in UI toegang te hebben. Vul het volgende in [formulier](https://adobe.ly/websdkaccess) om de nodige toegang te vragen. Om gegevensstromen te beheren, moet uw gebruikersrekening aan een productprofiel voor markeringen in worden toegevoegd [!DNL Adobe Experience Platform].

## Toegang krijgen tot [!UICONTROL Datastreams] werkruimte

U kunt gegevensstromen in de UI van de Inzameling van Gegevens tot stand brengen en beheren door te selecteren **[!UICONTROL Datastreams]** in de linkernavigatie.

![Het lusje van gegevensstromen in de UI van de Inzameling van Gegevens](../images/datastreams/overview/datastreams-tab.png)

De [!UICONTROL Datastreams] wordt een lijst weergegeven met bestaande gegevensstromen, inclusief de vriendelijke naam, id en datum die als laatste is gewijzigd. Selecteer de naam van een gegevensstroom die u wilt [zijn details bekijken en de diensten vormen](#view-details).

Selecteer het pictogram Meer (**...**) voor een bepaalde gegevensstroom om meer opties weer te geven. Selecteren **[!UICONTROL Edit]** om de [basisconfiguratie](#configure) voor de gegevensstroom, of selecteer **[!UICONTROL Delete]** om de gegevensstroom te verwijderen.

![Opties om bestaande gegevensstroom te bewerken of te verwijderen](../images/datastreams/overview/edit-datastream.png)

## Een nieuwe gegevensstroom maken {#create}

Als u een gegevensstroom wilt maken, selecteert u **[!UICONTROL New Datastream]**.

![Nieuwe gegevensstroom selecteren](../images/datastreams/overview/new-datastream-button.png)

De workflow voor het maken van de gegevensstroom wordt weergegeven, te beginnen bij de configuratiestap. Van hier, moet u een naam en een facultatieve beschrijving voor de gegevensstroom verstrekken.

Als u deze gegevensstroom voor gebruik in Experience Platform vormt en SDK van het Web van het Platform gebruikt, moet u ook selecteren [op gebeurtenissen gebaseerd XDM-schema (Experience Data Model)](../../xdm/classes/experienceevent.md) om de gegevens te vertegenwoordigen u bij het opnemen bent.

![Basisconfiguratie voor een gegevensstroom](../images/datastreams/overview/configure.png)

Selecteren **[!UICONTROL Advanced Options]** om extra controles te openbaren om de gegevensstroom te vormen.

![Geavanceerde configuratieopties](../images/datastreams/overview/advanced-options.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Geo Location] | Hiermee bepaalt u of GPS-opzoekingen worden uitgevoerd op basis van het IP-adres van de gebruiker. De standaardinstelling **[!UICONTROL None]** schakelt GPS-opzoekingen uit terwijl de **[!UICONTROL City]** Met deze instelling krijgt u GPS-coördinaten met twee decimalen. |
| [!UICONTROL First Party ID Cookie] | Als deze instelling is ingeschakeld, geeft het Edge Network de opdracht naar een opgegeven cookie te verwijzen wanneer u een [apparaat-id van eerste partij](../identity/first-party-device-ids.md)in plaats van deze waarde op te zoeken in het identiteitsoverzicht.<br><br>Als u deze instelling inschakelt, moet u de naam opgeven van het cookie waarop de id moet worden opgeslagen. |
| [!UICONTROL Third Party ID Sync] | De syncs van identiteitskaart kunnen in containers worden gegroepeerd om verschillende syncs van identiteitskaart toe te laten om op verschillende tijden worden in werking gesteld. Als deze instelling is ingeschakeld, kunt u opgeven welke container met id-syncs wordt uitgevoerd voor deze gegevensstroom. |
| [!UICONTROL Access Type] | Definieert het verificatietype dat de [!DNL Edge Network] Accepteert voor de gegevensstroom. <ul><li>**[!UICONTROL Mixed Authentication]**: Wanneer deze optie wordt geselecteerd, keurt het Netwerk van de Rand zowel voor authentiek verklaarde als unauthenticated verzoeken goed. Selecteer deze optie als u de SDK van het Web wilt gebruiken of [Mobile SDK](https://aep-sdks.gitbook.io/docs/), samen met de [Server-API](../../server-api/overview.md). </li><li>**[!UICONTROL Authenticated Only]**: Wanneer deze optie wordt geselecteerd, keurt het Netwerk van de Rand slechts voor authentiek verklaarde verzoeken goed. Selecteer deze optie als u alleen de Server-API wilt gebruiken en niet-geverifieerde aanvragen door de [!DNL Edge Network]. </li></ul> |

Als u vanaf hier uw gegevensstroom configureert voor Experience Platform, volgt u de zelfstudie [Gegevensvoorvoegsel voor gegevensverzameling](./data-prep.md) om uw gegevens aan een Platform gebeurtenisschema toe te wijzen alvorens aan deze gids terug te keren. Anders selecteert u **[!UICONTROL Save]** en ga verder met de volgende sectie.

## Gegevens gegevensstroom weergeven {#view-details}

Nadat u een nieuwe gegevensstroom hebt geconfigureerd of een bestaande gegevensstroom hebt geselecteerd, wordt de detailpagina voor die gegevensstroom weergegeven. Hier vindt u meer informatie over de gegevensstroom, inclusief de bijbehorende id.

![De pagina Details van een gemaakte gegevensstroom](../images/datastreams/overview/view-details.png)

Vanuit het scherm met gegevensstroomdetails kunt u [toevoegen, services](#add-services) om functies in te schakelen van de Adobe Experience Cloud-producten waartoe u toegang hebt. U kunt de gegevensstroom ook uitgeven [basisconfiguratie](#create), werkt de [toewijzingsregels](./data-prep.md), [de gegevensstroom kopiëren](#copy), of deze volledig verwijderen.

## Services toevoegen aan een gegevensstroom {#add-services}

Selecteer op de detailpagina van een gegevensstroom de optie **[!UICONTROL Add Service]** om de beschikbare services voor die gegevensstroom toe te voegen.

![Selecteer Service toevoegen om door te gaan](../images/datastreams/overview/add-service.png)

Voor het volgende scherm, gebruik dropdown menu om de dienst te selecteren voor deze gegevensstroom te vormen. Alleen de services waartoe u toegang hebt, worden in deze lijst weergegeven.

![Selecteer een service in de lijst](../images/datastreams/overview/service-selection.png)

Selecteer de gewenste service, vul de configuratieopties in die worden weergegeven en selecteer **[!UICONTROL Save]** om de dienst aan de datastream toe te voegen. Alle toegevoegde diensten verschijnen in de detailmening voor de gegevensstroom.

![Services die aan een gegevensstroom zijn toegevoegd](../images/datastreams/overview/services-added.png)

In de onderstaande subsecties worden de configuratieopties voor elke service beschreven.

>[!NOTE]
>
>Elke de dienstconfiguratie bevat **[!UICONTROL Enabled]** schakelt die automatisch wordt geactiveerd wanneer de service wordt geselecteerd. Als u de geselecteerde service voor deze gegevensstroom wilt uitschakelen, selecteert u de optie **[!UICONTROL Enabled]** weer schakelen.

### Adobe Analytics-instellingen {#analytics}

Deze service bepaalt of en hoe gegevens naar Adobe Analytics worden verzonden. Meer informatie vindt u in de handleiding op [gegevens verzenden naar Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics-instellingen blokkeren](../images/datastreams/overview/analytics-config.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Report Suite ID] | **(Vereist)** De id van de Analytics-rapportsuite waarnaar u gegevens wilt verzenden. Deze id is te vinden in de gebruikersinterface van Adobe Analytics onder [!UICONTROL Admin] > [!UICONTROL ReportSuites]. Als de veelvoudige rapportreeksen worden gespecificeerd, dan worden de gegevens gekopieerd aan elke rapportreeks. |

### Adobe Audience Manager-instellingen {#audience-manager}

Deze service bepaalt of en hoe gegevens naar Adobe Audience Manager worden verzonden. Alles wat nodig is om gegevens naar de Audience Manager te verzenden, moet deze sectie inschakelen. De andere instellingen zijn optioneel, maar worden aangemoedigd.

![Adobe Publiek beheren, instellingenblok](../images/datastreams/overview/audience-manager-config.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Cookie Destinations Enabled] | Staat SDK toe om segmentinformatie via te delen [koekjesbestemmingen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) van [!DNL Audience Manager]. |
| [!UICONTROL URL Destinations Enabled] | Staat SDK toe om segmentinformatie via te delen [URL-doelen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) van [!DNL Audience Manager]. |

### Adobe Experience Platform-instellingen {#aep}

>[!IMPORTANT]
>
>Wanneer het toelaten van een gegevensstroom voor Platform, neem nota van de zandbak van het Platform die u momenteel gebruikt, zoals getoond in het hoogste lint van UI van de Inzameling van Gegevens.
>
>![Geselecteerde sandbox](../images/datastreams/overview/platform-sandbox.png)
>
>Sandboxen zijn virtuele partities in Adobe Experience Platform waarmee u uw gegevens en implementaties kunt isoleren van die in uw organisatie. Wanneer een gegevensstroom is gemaakt, kan de sandbox niet meer worden gewijzigd. Zie voor meer informatie over de rol van sandboxen in Experience Platform de klasse [sandboxdocumentatie](../../sandboxes/home.md).

Deze service bepaalt of en hoe gegevens naar Adobe Experience Platform worden verzonden.

![Adobe Experience Platform-instellingenblok](../images/datastreams/overview/platform-config.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Event Dataset] | **(Vereist)** Selecteer de dataset van het Platform dat de gegevens van de klantengebeurtenis zullen worden gestroomd aan. Dit schema moet de [XDM ExperienceEvent, klasse](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Profile Dataset] | Selecteer de dataset van het Platform dat de gegevens van de klantenattributen zullen worden verzonden naar. Dit schema moet de [Afzonderlijke XDM-profielklasse](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Selecteer dit checkbox om Offer decisioning voor een implementatie van SDK van het Web van het Platform toe te laten. Zie de handleiding op [het gebruiken van Offer decisioning met het Web SDK van het Platform](../personalization/offer-decisioning/offer-decisioning-overview.md) voor meer details over de implementatie. Raadpleeg voor meer informatie over de mogelijkheden van Offer decisioning de [Adobe Journey Optimizer-documentatie](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=nl). |
| [!UICONTROL Edge Segmentation] | Schakel dit selectievakje in om in te schakelen [randsegmentatie](../../segmentation/ui/edge-segmentation.md) voor deze gegevensstroom. Wanneer de SDK gegevens via een voor edge-segmentatie ingeschakelde gegevensstroom verzendt, worden bijgewerkte segmentlidmaatschappen voor het profiel in kwestie teruggestuurd in de reactie.<br><br>Deze optie kan in combinatie met [!UICONTROL Personalization Destinations] for [gebruiksgevallen voor personalisatie op de volgende pagina](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Personalization Destinations] | Indien gebruikt in combinatie met [!UICONTROL Edge Segmentation] Schakel deze optie in om de datastream verbinding te laten maken met personaliseringsengines zoals Adobe Target. Raadpleeg de documentatie bij bestemmingen voor specifieke stappen over [het vormen verpersoonlijkingsbestemmingen](../../destinations/ui/configure-personalization-destinations.md). |

### Adobe Target-instellingen {#target}

Deze service bepaalt of en hoe gegevens naar Adobe Target worden verzonden.

![Adobe Target-instellingenblok](../images/datastreams/overview/target-config.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Property Token] | [!DNL Target] staat klanten toe om toestemmingen door het gebruik van eigenschappen te controleren. Zie de handleiding voor meer informatie over eigenschappen [configureren van bedrijfsmachtigingen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) in de [!DNL Target] documentatie.<br><br>Het eigenschapstoken vindt u in de gebruikersinterface van Adobe Target onder [!UICONTROL Setup] > [!UICONTROL Properties]. |
| [!UICONTROL Target Environment ID] | [Milieu in Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) helpen u bij het beheren van uw implementatie in alle ontwikkelingsstadia. Deze instelling geeft aan welke omgeving u wilt gebruiken voor deze gegevensstroom.<br><br>U kunt dit het beste voor elk van uw `dev`, `stage`, en `prod` gegevensstroomomgevingen om dingen eenvoudig te houden. Als u echter al Adobe Target-omgevingen hebt gedefinieerd, kunt u deze gebruiken. |
| [!UICONTROL Target Third Party ID namespace] | De naamruimte voor de identiteit van de `mbox3rdPartyId` wilt gebruiken voor deze gegevensstroom. Zie de handleiding op [uitvoeren `mbox3rdPartyId` met de Web SDK](../personalization/adobe-target/using-mbox-3rdpartyid.md) voor meer informatie . |

### [!UICONTROL Event Forwarding] instellingen

Deze service bepaalt of en hoe gegevens worden verzonden naar [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md).

![Het door:sturen van de gebeurtenis sectie van de configuratie UI](../images/datastreams/overview/event-forwarding-config.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Launch Property] | **(Vereist)** De gebeurtenis die bezit door:sturen dat u gegevens naar wilt verzenden. |
| [!UICONTROL Launch Environment] | **(Vereist)** De omgeving binnen de geselecteerde eigenschap waarnaar u gegevens wilt verzenden. |

>[!NOTE]
>
>U kunt **[!UICONTROL Manually enter IDs]** om in de bezit en omgevingsnamen in plaats van het gebruiken van dropdown menu&#39;s te typen.

## Een gegevensstroom kopiëren {#copy}

U kunt een kopie van een bestaande gegevensstroom maken en de details ervan desgewenst wijzigen.

>[!NOTE]
>
>Gegevensstromen kunnen alleen worden gekopieerd binnen dezelfde [sandbox](../../sandboxes/home.md). Met andere woorden, u kunt geen gegevensstroom van één zandbak aan een andere kopiëren.

Vanaf de hoofdpagina in het dialoogvenster [!UICONTROL Datastreams] werkruimte, selecteert u de ellips (**....**) voor de gegevensstroom in kwestie, dan selecteren **[!UICONTROL Copy]**.

![Afbeelding die de [!UICONTROL Copy] optie die wordt geselecteerd in de lijstweergave van de gegevensstroom](../images/datastreams/overview/copy-datastream-list.png)

U kunt ook **[!UICONTROL Copy Datastream]** in de detailweergave van een bepaalde gegevensstroom.

![Afbeelding die de [!UICONTROL Copy] optie die wordt geselecteerd uit de datastream detailweergave](../images/datastreams/overview/copy-datastream-details.png)

Er wordt een bevestigingsdialoogvenster weergegeven waarin u wordt gevraagd een unieke naam op te geven voor de nieuwe gegevensstroom die moet worden gemaakt, en waarin u informatie kunt vinden over de configuratieopties waarover u de gegevens wilt kopiëren. Indien gereed, selecteert u **[!UICONTROL Copy]**.

![Afbeelding van het bevestigingsvenster voor het kopiëren van een gegevensstroom](../images/datastreams/overview/copy-datastream-confirm.png)

De hoofdpagina van de [!UICONTROL Datastreams] wordt de werkruimte opnieuw weergegeven met de nieuwe gegevensstroom.

## Volgende stappen

Deze gids behandelde hoe te om gegevensstromen in de Inzameling van Gegevens UI te beheren. Voor meer informatie over om SDK van het Web na vestiging een gegevensstroom te installeren en te vormen, verwijs naar [E2E-handleiding voor gegevensverzameling](../../rtcdp-connections/e2e.md#install).
