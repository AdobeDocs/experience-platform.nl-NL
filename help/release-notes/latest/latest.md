---
title: Opmerkingen bij de release van Adobe Experience Platform, juli 2024
description: De release van juli 2024 bevat opmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c38f6845a4819b648abacea2c36a576dac61f38f
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 30 juli 2024**

Nieuwe functies in Adobe Experience Platform:

- [!BADGE Beperkte beschikbaarheid]{type=Informative}[ Federated Audience Composition ](#federated-audience-composition)

Updates van bestaande functies en documentatie in Experience Platform:

- [Geavanceerd levenscyclusbeheer van gegevens](#advanced-data-lifecycle-management)
- [Gegevensverzameling](#data-collection)
- [Gegevensbeheer](#data-governance)
- [Doelen](#destinations)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)
- [Uniforme tags](#unified-tags)

## Federale compositie publiek {#federated-audience-composition}

De Federated Audience Composition staat ondernemingen toe om gegevens voor betere toepassing over diverse gebruiksgevallen samen te stellen. Met deze nieuwe benadering, als Adobe Real-time Customer Data Platform en/of gebruiker van Adobe Journey Optimizer, kunt u datasets van uw bestaand gegevenspakhuis direct federeren om het publiek en de attributen van Adobe Experience Platform tot stand te brengen en te verrijken allen in één systeem.

Voor meer informatie, lees de [ Federated documentatie van de Samenstelling van de Publiek ](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/home).

## Geavanceerd levenscyclusbeheer van gegevens {#advanced-data-lifecycle-management}

Experience Platform biedt een reeks mogelijkheden voor gegevenshygiëne waarmee u uw opgeslagen gegevens kunt beheren via programmatische verwijderingen van consumentengegevens en gegevenssets. Met de werkruimte van de Levenscyclus van Gegevens in UI of door vraag aan de API van de Hygiëne van Gegevens, kunt u uw gegevensopslag effectief beheren. Gebruik deze mogelijkheden om ervoor te zorgen dat de informatie zoals verwacht wordt gebruikt, wordt bijgewerkt wanneer onjuiste gegevens het bevestigen vereisen, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

**Nieuwe documentatie**

| Nieuwe documentatie | Beschrijving |
| --- | --- |
| [!DNL Data Hygiene API] reference | Met de API voor gegevenshygiëne kunt u uw gegevensopslag in Experience Platform op effectieve wijze beheren. Met deze mogelijkheden, kunt u ervoor zorgen dat de informatie wordt gebruikt zoals verwacht, wanneer onjuist bijgewerkt, en geschrapt wanneer het organisatorische beleid het noodzakelijk acht.<br><br> leest het [ API verwijzingsdocument van de Hygiëne van Gegevens ](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/) voor gedetailleerde informatie over hoe te om API te gebruiken. Met de API voor gegevenshygiëne kunt u vervaldatums van gegevenssets plannen, opgeslagen persoonlijke gegevens van klanten programmatically corrigeren of verwijderen en uw quota voor gegevenshygiëne controleren. Het API verwijzingsdocument omvat de beschikbare eindpunten, verzoekparameters, en antwoordformaten om u te helpen uw opgeslagen klantengegevens efficiënt beheren.</br></br> |

Voor meer informatie, leest het [ geavanceerde overzicht van het beheer van de gegevenslevenscyclus ](../../hygiene/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Edge Network van het Experience Platform kunt verzenden waar het kan worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte eigenschappen**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Web SDK | Propositieinteracties automatisch bijhouden | U kunt nu de eigenschap `autoTrackPropositionInteractionsEnabled` in Web SDK gebruiken om te bepalen of Web SDK automatisch propositieinteracties moet verzamelen. Raadpleeg de documentatie bij [`autoTrackPropositionInteractionsEnabled`](../../web-sdk/commands/configure/autotrackpropositioninteractionsenabled.md) voor meer informatie. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie**

| Nieuwe of bijgewerkte documentatie | Beschrijving |
| --- | --- |
| Nieuwe API-eindpunten gedocumenteerd voor de Reactor-API | De het pakketgebruiksautorisatieeindpunten van de uitbreiding kunnen nu in de [ Reactor API verwijzingsdocumentatie ](https://developer.adobe.com/experience-platform-apis/references/reactor/) worden gevonden. Extensieeigenaars kunnen met deze eindpunten pakketmachtigingen voor een extensiepakket toevoegen, verwijderen en ophalen. |
| Document met eindpunten voor machtigingen voor het gebruik van nieuwe extensiepakketten | Een overzicht van hoe de eigenaars van het uitbreidingspakket andere bedrijven kunnen machtigen om hun privé versies van de pakketten in Reactor API te gebruiken kan in de [ documentatie van het het pakketgebruik van de Uitbreiding eindpunten ](/help/tags/api/endpoints/extension-package-usage-authorizations.md) worden gevonden. |
| Nieuwe hulplijn voor persoonlijke extensies delen | De de vergunningsverwezenlijking, goedkeuring, en schrappingsprocedures van het uitbreidingspakket van Reactor API worden geschetst in [ het Delen van privé uitbreidingen ](/help/tags/api/guides/extension-packages.md) documentatie. |

{style="table-layout:auto"}

Voor meer informatie, lees het [ overzicht van de gegevensinzameling ](../../collection/home.md).

## Gegevensbeheer {#data-governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen Experience Platform op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

**Nieuwe eigenschap**

| Functie | Beschrijving |
| --- | --- |
| mTLS Service API | De [ mTLS dienst API ](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/overview) wordt ontworpen om veiligheid voor gegevensuitwisseling te verbeteren. Gebruik deze API om de openbare certificaten veilig op te halen die door Adobe voor de toepassingen van uw organisatie worden uitgegeven. Deze certificaten zorgen ervoor dat alle communicatie wordt geverifieerd en gecodeerd en kunnen worden gebruikt om de authenticiteit van certificaten extern te controleren. Lees de [ openbare gids van het certificaateindpunt ](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/public-certificate-endpoint) om te leren hoe te openbare certificaten voor de toepassingen van de Adobe van uw organisatie veilig terugwinnen. |

{style="table-layout:auto"}

Voor meer informatie, lees het [ overzicht van het gegevensbeheer ](../../data-governance/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Doel | Beschrijving |
| ----------- | ----------- |
| [ (Beta) Merkury Enterprise Connections ](/help/destinations/catalog/data-partners/merkury-enterprise-connections.md) | Gebruik de bestemming [!DNL Merkury Enterprise Connections] om een publiek veilig aan [!DNL Merkury] te leveren. [!DNL Merkury] biedt marketers eenvoudig overeenkomsten en levering van op personen gebaseerde soorten publiek met maximaal 80 eersteklas tv-/CTV-, uitgever- en advertentietechnische verbindingen van [!DNL Merkury] . [!DNL Merkury] wordt aangedreven door een uitgebreide identiteitsgrafiek van 268+ miljoen mensen voor volwassenen in de VS. |
| [ (Beta) Merkury Enterprise Identity ](/help/destinations/catalog/data-partners/merkury-enterprise-identity.md) | Gebruik de bestemming [!DNL Merkury Enterprise Identity] om nauwkeurigere, uitvoerige, en inzichtelijkere consumentenprofielen te bouwen. Met verbeterde profielgegevens kunnen marketers betere inzichten, segmenten en modellen tot stand brengen, wat resulteert in een nauwkeuriger gerichte benadering en voorspellende modellering. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Bewaking op het niveau van de doelgroep | De controle van uw gegevensstromen, die door publiek worden gegroepeerd, was eerder beschikbaar voor partij (op dossier-gebaseerde) slechts bestemmingen. Vanaf deze release is bewaking op publieksniveau ook beschikbaar voor de [ (Beta) Google Customer Match + DV360 streaming destination ](/help/destinations/catalog/advertising/google-customer-match-dv360.md) . Lees meer over [ publiek-vlakke controle ](/help/dataflows/ui/monitor-destinations.md#segment-level-view) en contacteer uw vertegenwoordiger van de Adobe als u zich bij het bètaprogramma wilt aansluiten om de Klant van Google te gebruiken Gelijke + bestemming DV360. |
| Ondersteuning voor verrijkingskenmerken in publiekmetagegevensmacro&#39;s voor Destination SDK | U kunt tot verrijkingsattributen in [ Destination SDK publieksmeta-gegevensmalplaatjes ](../../destinations/destination-sdk/functionality/audience-metadata-management.md) door specifieke macro&#39;s nu toegang hebben. De attributen van de verrijking zijn beschikbaar slechts voor [ douane uploadt publiek ](../../destinations/destination-sdk/functionality/destination-configuration/schema-configuration.md#external-audiences). Zie de [ gids van de de activering van het partijpubliek ](../../destinations/ui/activate-batch-profile-destinations.md#select-enrichment-attributes) om te zien hoe de selectie van de verrijkingsattributen werkt. Zie het publieksmalplaatje [ macros lijst ](../../destinations/destination-sdk/functionality/audience-metadata-management.md#macros) voor meer details. |

{style="table-layout:auto"}

Voor meer informatie, lees het [ overzicht van bestemmingen ](../../destinations/home.md).

## Segmenteringsservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) segmenteren naar het publiek. U kunt een publiek maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze soorten publiek worden centraal geconfigureerd en onderhouden op [!DNL Platform] en zijn gemakkelijk toegankelijk voor elke Adobe.

**Nieuwe documentatie**

| Nieuwe documentatie | Beschrijving |
| ----------------- | ----------- | 
| [ Portaal van het Publiek ](../../segmentation/ui/audience-portal.md) | Leer hoe u Poort publiek kunt gebruiken, waarmee u het publiek in Adobe Experience Platform in een gecentraliseerde hub kunt weergeven, beheren en maken. |

{style="table-layout:auto"}

## Bronnen

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

Gebruik bronnen in Experience Platform om gegevens van een Adobe of een gegevensbron van derden in te voeren.

**Bijgewerkte documentatie**

| Bijgewerkte documentatie | Beschrijving |
| --- | --- |
| Uitgebreide verificatiegids voor [[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md) | Lees de uitgebreide authentificatiegids voor [!DNL Snowflake] leren hoe te om uw [ rekeningsherkenningsteken ](../../sources/connectors/databases/snowflake.md#retrieve-your-account-identifier) en [ privé sleutel ](../../sources/connectors/databases/snowflake.md#retrieve-your-private-key) voor authentificatie terug te winnen. Bovendien, gebruik de uitgebreide authentificatiegids voor stappen op hoe te [ uw pakhuis en rolconfiguraties ](../../sources/connectors/databases/snowflake.md#verify-configurations) verifiëren. |

{style="table-layout:auto"}

Voor meer informatie, lees het [ overzicht van bronnen ](../../sources/home.md).

## Uniforme tags

Met Unified Tags kunt u uw bedrijfsobjecten in Adobe Experience Platform indelen en beheren. Met de Verenigde Markeringen API, kunt u zowel omslagen als markeringen tot stand brengen om de voorwerpen van het Platform zoals publiek of datasets beter te organiseren.

**Nieuwe documentatie**

| Nieuwe documentatie | Beschrijving |
| ----------------- | ----------- |
| [ Verenigde Tags API gids ](../../administrative-tags/api/overview.md) | Lees de Unified Tags API-handleiding om te leren hoe u mappen en tags kunt maken om uw zakelijke objecten te sorteren. |
| [ Verenigde Tags API verwijzing ](https://developer.adobe.com/experience-platform-apis/references/unified-tags/) | Gebruik de Verenigde Tags API verwijzing om de Verenigde tags-eindpunten op interactieve wijze uit te proberen. |

{style="table-layout:auto"}

Voor meer informatie, lees het [ Verenigde overzicht van Markeringen ](../../administrative-tags/overview.md).
