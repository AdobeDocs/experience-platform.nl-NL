---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
source-git-commit: d046c17a7b376f5c2e2f25c38fac0916ed2dba73
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 26 oktober 2022**

Nieuwe functies in Adobe Experience Platform:

- [Door de klant beheerde sleutels](#cmk)

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensverzameling](#data-collection)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Query-service](#query-service)
- [Bronnen](#sources)

## Door de klant beheerde sleutels {#cmk}

Alle gegevens die op Adobe Experience Platform zijn opgeslagen, worden in rust gecodeerd met systeemtoetsen. Als u een toepassing gebruikt die bovenop Platform wordt gebouwd, kunt u nu ervoor kiezen om uw eigen encryptiesleutels in plaats daarvan te gebruiken, die u grotere controle over uw gegevensveiligheid geven.

Zie het overzicht op [door de klant beheerde sleutels](../../landing/governance-privacy-security/customer-managed-keys.md) voor meer informatie over de functie.

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gevoelige gegevensverwerking voor gegevensstromen | De gegevensstromen gebruiken nu verscheidene technologieën van de Platform om gevoelige gegevens zoals die door verordeningen zoals de Wet van de Portabiliteit en van de Verantwoording van de Ziekteverzekering (HIPAA) worden afgedwongen adequaat te behandelen. Zie de sectie over [verwerking van gevoelige gegevens in gegevensstreams](../../edge/datastreams/overview.md#sensitive) voor meer informatie . |
| [!DNL Splunk] extensie voor het doorsturen van gebeurtenissen | U kunt nu gegevens verzenden naar [!DNL Splunk] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Splunk] extensieoverzicht](../../tags/extensions/web/splunk/overview.md) voor meer informatie . |
| [!DNL Zendesk] extensie voor het doorsturen van gebeurtenissen | U kunt nu gegevens verzenden naar [!DNL Zendesk] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Zendesk] extensieoverzicht](../../tags/extensions/web/zendesk/overview.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| (bèta) Gegevensset exporteren | De [Dataset exporteert bètafunctionaliteit](/help/destinations/ui/export-datasets.md) kunt u gegevens van de eerste generatie exporteren (zoals gedefinieerd in het dialoogvenster [Real-time Customer Data Platform-productbeschrijving](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) van Adobe Experience Platform naar uw eigen systemen voor externe klanten, via de gebruikersinterface voor bestemmingen. Hierdoor kunt u gegevens uit het Experience Platform halen met een workflow zonder code/lage code naar zes cloudopslagbestemmingen (vermeld in de onderstaande tabel) voor analytische en compatibiliteitsgevallen. |
| (bèta) Verbeterde mogelijkheden voor het exporteren van bestanden | U kunt nu profiteren van de verbeterde aanpassingsfunctionaliteit wanneer u bestanden exporteert vanuit het Experience Platform: <br><ul><li>Extra [naamgevingsopties voor bestanden](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Mogelijkheid om aangepaste bestandsheaders in uw geëxporteerde bestanden in te stellen via de [verbeterde toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Mogelijkheid om de opmaak van geëxporteerde CSV-gegevensbestanden aan te passen](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Deze functionaliteit wordt ondersteund door de zes nieuwe bètacloud-opslagkaarten die in de onderstaande tabel worden vermeld. |

{style=&quot;table-layout:auto&quot;}

**Nieuwe of bijgewerkte doelen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | De lijn is een populair communicatie platform dat mensen, de diensten en de informatie verbindt en van een praatjeapp tot een hub voor vermaak, sociale, en dagelijkse activiteiten is gegroeid. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 is een op cloud gebaseerd bedrijfstoepassingsplatform dat de Planning van het Middel van de Onderneming (ERP) en het Beheer van de Verhouding van de Klant (CRM) samen met productiviteitstoepassingen en AI hulpmiddelen combineert, om van begin tot eind vlottere en meer gecontroleerde verrichtingen, beter groeipotentieel en lagere kosten te brengen. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | De [!DNL (Beta) Adobe Commerce] met de doelconnector kunt u een of meer Real-Time CDP-segmenten selecteren die u voor uw [!DNL Adobe Commerce] -account voor een dynamische, op maat gesneden ervaring voor kopers. Within [!DNL Adobe Commerce], kunt u die Real-Time CDP-segmenten selecteren om unieke aanbiedingen in de winkelwagen aan te passen, zoals &#39;Koop 2 krijg 1 gratis&#39;. U kunt ook hoofdbanners weergeven en de productprijzen wijzigen via promotieaanbiedingen, die allemaal zijn aangepast aan Adobe Real-Time CDP-segmenten. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Een live uitgaande verbinding maken met [!DNL Azure Data Lake Storage Gen2] om periodiek gegevensbestanden van Adobe Experience Platform naar uw eigen opslaglocatie te exporteren. Deze nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Azure Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die door Adobe Experience Platform is ingericht, zodat u toegang hebt tot een veilige, op de cloud gebaseerde opslagvoorziening voor bestanden om bestanden uit het Platform te exporteren. Deze nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Een live uitgaande verbinding maken met [!DNL Google Cloud Storage] om gegevensbestanden van Adobe Experience Platform regelmatig naar uw eigen emmers te exporteren. Deze nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Bètadeelnemers zien nu twee [!DNL Amazon S3] doelkaarten naast elkaar in de doelcatalogus. De nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Bètadeelnemers zien nu twee [!DNL Azure Blob] doelkaarten naast elkaar in de doelcatalogus. De nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Bètadeelnemers zien nu twee [!DNL SFTP] doelkaarten naast elkaar in de doelcatalogus. De nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |

{style=&quot;table-layout:auto&quot;}

**Nieuwe of bijgewerkte documentatie**

| Documentatie | Beschrijving |
| ----------- | ----------- |
| [Doelgeleidingen](../../destinations/guardrails.md) | Deze pagina bevat standaardgebruiks- en tarieflimieten voor activeringsgedrag. |

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gegevenstype | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | De `authorized` van een booleaanse tekst naar een tekenreeks. `season` en `episode` zijn gewijzigd van gehele getallen in tekenreeksen. |
| Gegevenstype | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` is hernoemd naar `friendlyName`, en `ID` is hernoemd naar `name`. |
| Gegevenstype | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` is hernoemd naar `name`. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL Data Lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL Data Lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| De vragen van de monitor door Platform UI | De Query-service [!UICONTROL Scheduled Queries] biedt een verbeterde zichtbaarheid voor de status van alle querytaken via de gebruikersinterface. U kunt belangrijke informatie over de status van uw vraaglooppas nu vinden, met inbegrip van foutenmeldingen en codes indien zij ontbreken, van [!UICONTROL Scheduled Queries] tab. U kunt ook op alarm door UI voor om het even welk van deze vragen intekenen die op hun status worden gebaseerd. Zie de [Document met query&#39;s controleren](../../query-service/monitor-queries.md) voor meer informatie over deze functie. |
| Vraag versnelde het melden van inzichten gegevensmodel | Als deel van Gegevens Distiller SKU, staat de vraag versnelde opslag u toe om de tijd en de verwerkingscapaciteit te verminderen die wordt vereist om kritieke inzichten van uw gegevens te bereiken. Met de opslag met versnelde query kunt u een aangepast gegevensmodel maken en/of uitbreiden op bestaande Adobe Real-time Customer Data Platform-gegevensmodellen om uw rapporteringsinzichten en hun visualisaties te verbeteren. Zie de [document met query-versnelde gegevens voor winkelrapporten](../../query-service/query-accelerated-store/reporting-insights-data-model.md) voor meer informatie over deze functie. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de Diensten van de Vraag, verwijs naar [Overzicht van Query Service](../../query-service/home.md).
Nieuwe functies in Adobe Experience Platform:

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- | 
| Beta-beschikbaarheid van Adobe Workfront-bron | Gebruik de [Adobe Workfront-bron](../../sources/connectors/adobe-applications/workfront.md) om uw gegevens van Workfront aan Experience Platform te brengen en gebruiksgevallen uit te voeren zoals het combineren van uw werkverslagen met derdengegevens, het toepassen van historische en tijdreeksanalyses op het werkverslagen, en het vragen van het werkgegevens gebruikend standaardSQL. Lees voor meer informatie de handleiding op [een Workfront-bronverbinding maken in de gebruikersinterface](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Beta beschikbaarheid van Oracle Service Cloud-bron | Gebruik de Cloud-bron van de service Oracle om gegevens van uw Oracle Service Cloud-account in te voeren naar Experience Platform. Voor meer informatie leest u de documentatie op het tabblad [Cloud-bron voor oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
