---
title: Aanvullende informatie over Adobe Experience Platform
description: De release van juli 2023 bevat opmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 819c4e8b4ab24d364cf6d26d3ce38d0bc372e603
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 26 juli 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Catalogusservice](#catalog-service)
- [Gegevensverzameling](#data-collection)
- [Doelen](#data-prep)
- [Query-service](#query-service)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie van gegevens en de gegevensverbinding in Adobe Experience Platform. Terwijl alle gegevens die in Experience Platform worden opgenomen in het meer van Gegevens als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.

| Functie | Beschrijving |
| --- | --- |
| Beheer gegevenssets | De datasets UI biedt nu een inzamelingen van gealigneerde acties aan om uw datasets beter te beheren. Het geavanceerde gegevenssetbeheer verbetert uw werkefficiency door de verwezenlijking en het toewijzen van omslagen en markeringen aan uw datasets die voor het filtreren en betere ontdekkingsbaarheid toestaat. Zie de documentatie voor meer informatie over [inline-handelingen](../../catalog/datasets/user-guide.md#inline-actions), hoe [zoek- en filtergegevenssets](../../catalog/datasets/user-guide.md#search-and-filter), en [gegevenssets verplaatsen naar mappen](../../catalog/datasets/user-guide.md#move-to-folders). |

{style="table-layout:auto"}

Raadpleeg voor meer informatie over Catalog Service de [Overzicht van Catalog Service](../../catalog/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Tags en doorsturen van gebeurtenissen | Controleregboeken voor gegevensverzameling | U kunt nu zien wanneer een actie is uitgevoerd en wie deze actie heeft uitgevoerd op Tags en Gebeurtenis doorsturen. Dit vergemakkelijkt het oplossen van problemen met producten, behoorlijk bestuur, en interne controleactiviteiten. Deze controlegegevens worden weergegeven via in-context schuifmenu&#39;s die ook snelle acties en updates van de middelstatus bevatten. Deze gegevens zijn in de volgende schermen zichtbaar in de gebruikersinterface Tags en Event Forwarding:<br><ul><li>[Overzicht van eigenschappen](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[Regels](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[Gegevenselementen](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[Extensies](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[Bibliotheekrevisie](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[Bibliotheek laatst samenstellen en gepubliceerd](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| Gegevensstromen | [Geo Lookup](../../datastreams/configure.md#advanced-options) | U kunt geolocatie en netwerkzoekopdracht voor gegevensstreams nu configureren om informatie zoals: <ul><li>Land</li><li>Postcode</li><li>Staat/provincie</li><li>DMA</li><li>Plaats</li><li>Breedtegraad </li><li>Lengtegraad</li><li>Vervoerder</li><li>Domein</li><li>ISP</li></ul> U bent ervoor verantwoordelijk dat u alle benodigde machtigingen, toestemmingen, toestemmingen, toestemmingen en toestemming hebt verkregen die vereist zijn krachtens de toepasselijke wet- en regelgeving voor het verzamelen, verwerken en verzenden van persoonlijke gegevens, inclusief nauwkeurige geolocatiegegevens. <br> Uw IP selectie van de adresverwarring beïnvloedt niet het niveau van geolocatieinformatie die van het IP adres zal worden afgeleid en naar uw gevormde oplossingen van Adobe verzonden. Geolocation lookups moeten worden beperkt of afzonderlijk worden uitgeschakeld. <br> Zie de [datastreams documentatie](../../datastreams/configure.md#advanced-options) voor meer informatie . |

{style="table-layout:auto"}

Lees voor meer informatie over gegevensverzameling de [overzicht van gegevensverzamelingen](../../tags/home.md).
<!-- 
## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions | You can now use the following functions when mapping objects in Data Prep: <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md#hierarchies---objects). |

{style="table-layout:auto"}

For more information on Data Prep, please read the [Data Prep overview](../../data-prep/home.md). -->

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte doelen** {#new-updated-destinations}

| Bestemming | Nieuw of Bijgewerkt | Beschrijving |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Onboarding]](../../destinations/catalog/advertising/liveramp-onboarding.md) | Nieuw | Identiteiten aan boord van Adobe Experience Platform tot [!DNL LiveRamp Connect] zodat u gebruikers kunt richten op mobiel, open Web, sociaal en [!DNL CTV] platformen, gebruiken [!DNL Ramp ID] id. |
| [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Nieuw | Een live uitgaande verbinding maken met [!DNL Azure Data Lake Storage Gen2] om periodiek gegevensbestanden van Adobe Experience Platform naar uw eigen opslaglocatie te exporteren. Deze nieuwe bestemming biedt verbeterde functies voor het exporteren van bestanden en ondersteunt [!BADGE Beta]{type=Informative} |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Nieuw | [!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die door Adobe Experience Platform is ingericht, zodat u toegang hebt tot een veilige, op de cloud gebaseerde opslagvoorziening voor bestanden om bestanden uit het Platform te exporteren. Deze nieuwe bestemming biedt verbeterde functies voor het exporteren van bestanden en ondersteunt [!BADGE Beta]{type=Informative} |
| [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Nieuw | Een live uitgaande verbinding maken met [!DNL Google Cloud Storage] om gegevensbestanden van Adobe Experience Platform regelmatig naar uw eigen emmers te exporteren. Deze nieuwe bestemming biedt verbeterde functies voor het exporteren van bestanden en ondersteunt [!BADGE Beta]{type=Informative} |
| [[!DNL Amazon S3] update](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Bijgewerkt | Met deze update biedt de bestemming uitgebreide functies voor het exporteren van bestanden en biedt deze functie ondersteuning voor [!BADGE Beta]{type=Informative} |
| [[!DNL Azure Blob] update](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Bijgewerkt | Met deze update biedt de bestemming uitgebreide functies voor het exporteren van bestanden en biedt deze functie ondersteuning voor [!BADGE Beta]{type=Informative} |
| [[!DNL SFTP] update](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Bijgewerkt | Met deze update biedt de bestemming uitgebreide functies voor het exporteren van bestanden en biedt deze functie ondersteuning voor [!BADGE Beta]{type=Informative} |
| [[!DNL Adobe Campaign Managed Services] verbinding](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Bijgewerkt | De [!DNL Adobe Campaign Managed Services] integratie met Adobe Experience Platform ondersteunt nu verschillende soorten publiekssynchronisatie. Gebruik het besturingselement Synchronisatietype selecteren om te bepalen of u soorten publiek wilt exporteren naar Adobe Campaign of naar soorten publiek en hun profielkenmerken. <br> ![Nieuwe selector voor synchronisatietype selecteren is gemarkeerd.](/help/release-notes/2023/assets/acms-destination-export-type.png "Nieuwe selector voor synchronisatietype selecteren is gemarkeerd."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

De update en de algemene beschikbaarheidsversie van de zes hierboven vermelde bestemmingen van de wolkenopslag verstrekken de volgende functionaliteit:

- Extra [naamgevingsopties voor bestanden](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
- Mogelijkheid om aangepaste bestandsheaders in uw geëxporteerde bestanden in te stellen via de [verbeterde toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
- De mogelijkheid om de [opmaak van geëxporteerde CSV-gegevensbestanden](/help/destinations/ui/batch-destinations-file-formatting-options.md).
- [!BADGE Beta]{type=Informative}[Ondersteuning voor gegevensexport](/help/destinations/ui/export-datasets.md).


**Oplossingen en verbeteringen** {#destinations-fixes-and-enhancements}

- We hebben een probleem opgelost met de Salesforce-bestemming (API) van de Salesforce-Marketing Cloud, waarbij in de toewijzingsstap niet alle beschikbare doelkenmerken werden geretourneerd van Salesforce. Er is nu een [bovengrens van 2000 doelkenmerken](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md#mapping-considerations-example) vanuit Salesforce die kan worden weergegeven.
- We hebben een probleem opgelost met de bestemming Microsoft Dynamics 365. De bestemming steunt nu regionaal verpletteren van gegevens via [Gebiedselector](/help/destinations/catalog/crm/microsoft-dynamics-365.md#authenticate), zodat kunt u uw gegevensexport leiden afhankelijk van welk gebied uw bedrijf binnen het ecosysteem van Microsoft provisioned is. ![Selector nieuw gebied gemarkeerd.](/help/release-notes/2023/assets/region-parameter-microsoft-dynamics-365.png "Selector nieuw gebied gemarkeerd."){width="100" zoomable="yes"}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL te gebruiken om gegevens in het gegevenspeer van Adobe Experience Platform te vragen. U kunt zich bij om het even welke datasets van gegevens aansluiten meer en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Uitgebreide functie voor Query-editor | De verbeterde knevel van de Redacteur van de Vraag verstrekt betere toegankelijkheid en multi-theming steun. Met de verbeterde editor-instellingen kunt u donkere of lichte thema&#39;s inschakelen. Zie de [documentatie](../../query-service/ui/user-guide.md#enhanced-editor-toggle) voor meer informatie . |
| Aliasnaam voor berekende statistieken | U kunt nu een aliasnaam opgeven om de resultaten van uw gegevens in uw berekende statistieken in SQL-query&#39;s beschrijvend te gebruiken. Zie de documentatie voor informatie over dit en andere updates aan het bevel van de STATISTIEKEN van de COMPUTE. Zie de [documentatie](../../query-service/essential-concepts/dataset-statistics.md#alias-name) voor meer informatie . |

{style="table-layout:auto"}

Raadpleeg voor meer informatie over Query Service de [Overzicht van Query Service](../../query-service/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] die betrekking heeft op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) die het publiek bereiken. U kunt publiek door segmentdefinities of andere bronnen van uw tot stand brengen [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn door elke Adobe-oplossing.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Poort publiek | De portal Publiek biedt een nieuwe browserervaring voor toegang tot, het maken en beheren van soorten publiek in Adobe Experience Platform. Binnen het Portaal van het Publiek, kunt u Platform-geproduceerd en uiterlijk geproduceerd publiek bekijken; uw het werkefficiency verbeteren door het filtreren, omslagen, en markeringen, creeer Platform-geproduceerd publiek; en de invoer extern geproduceerd publiek door Csv- dossiers. Voor meer informatie over de Poort van het Publiek, gelieve te lezen [Handleiding voor segmentatieservice](../../segmentation/ui/overview.md). |
| Samenstelling publiek | De Samenstelling van het publiek verstrekt een makkelijk te gebruiken werkruimte om publiek te bouwen en uit te geven, gebruikend blokken die worden gebruikt om verschillende acties te vertegenwoordigen. Lees voor meer informatie over Audience Composition de [Handleiding voor compositie van publiek](../../segmentation/ui/audience-composition.md). |

Voor meer informatie over [!DNL Segmentation Service], lees de [Overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | U kunt nu de opdracht [[!DNL SAP Commerce] bron](../../sources/connectors/ecommerce/sap-commerce.md) om factureringsgegevens voor abonnementen van uw [!DNL SAP Commerce] aan Experience Platform. |
| Ondersteuning voor [!DNL Phoenix] | U kunt nu de opdracht [[!DNL Phoenix] bron](../../sources/connectors/databases/phoenix.md) om gegevens van uw [!DNL Phoenix] database naar Experience Platform. |
| Verificatieupdates voor [!DNL Salesforce] en [!DNL Salesforce Service Cloud] | U kunt nu de API-versie van uw [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) en [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) bron wanneer het voor authentiek verklaren van een nieuwe rekening met het Experience Platform UI of [!DNL Flow Service] API. |

{style="table-layout:auto"}

Lees voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
