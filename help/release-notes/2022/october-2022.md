---
title: Opmerkingen bij de release van Adobe Experience Platform, oktober 2022
description: Aanvullende informatie voor de versie van oktober 2022 voor Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 26 oktober 2022**

- [Door de klant beheerde sleutels](#cmk)
- [Gegevensverzameling](#data-collection)
- [Doelen](#destinations)
- [Experience Data Model](#xdm)
- [Query-service](#query-service)

## Door de klant beheerde sleutels {#cmk}

Alle gegevens die op Adobe Experience Platform zijn opgeslagen, worden in rust gecodeerd met systeemtoetsen. Als u een toepassing gebruikt die bovenop Platform wordt gebouwd, kunt u nu ervoor kiezen om uw eigen encryptiesleutels in plaats daarvan te gebruiken, die u grotere controle over uw gegevensveiligheid geven.

Zie het overzicht op [ klant-geleide sleutels ](../../landing/governance-privacy-security/customer-managed-keys/overview.md) voor details op de eigenschap.

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Adobe Experience Platform-Edge Network kunt sturen waar deze verrijkt, getransformeerd en gedistribueerd kan worden naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Gevoelige gegevensverwerking voor gegevensstromen | De gegevensstromen gebruiken nu verscheidene technologieën van het Platform om gevoelige gegevens zoals die door verordeningen zoals de Wet van de Portabiliteit en van de Verantwoording van de Ziekteverzekering (HIPAA) worden afgedwongen adequaat te behandelen. Zie de sectie over [ behandelend gevoelige gegevens in datstromen ](../../datastreams/overview.md#sensitive) voor meer informatie. |
| [!DNL Splunk] extensie voor het doorsturen van gebeurtenissen | U kunt gegevens aan [!DNL Splunk] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Splunk]  uitbreidingsoverzicht ](../../tags/extensions/server/splunk/overview.md) voor meer informatie. |
| [!DNL Zendesk] extensie voor het doorsturen van gebeurtenissen | U kunt gegevens aan [!DNL Zendesk] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Zendesk]  uitbreidingsoverzicht ](../../tags/extensions/server/zendesk/overview.md) voor meer informatie. |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| (Beta) Dataset exporteren | De [ functie van de Uitvoer van de Dataset Beta ](/help/destinations/ui/export-datasets.md) staat u toe om eerste generatiegegevens (zoals die in de [ het productbeschrijving van Real-time Customer Data Platform ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) worden bepaald) uit Adobe Experience Platform naar uw eigen externe klantensystemen, via het interface van bestemmingsgebruiker uit te voeren. Hierdoor kunt u gegevens uit het Experience Platform halen met een workflow zonder code/lage code naar zes cloudopslagbestemmingen (vermeld in de onderstaande tabel) voor analytische en compatibiliteitsgevallen. |
| (Beta) Verbeterde exportmogelijkheden voor bestanden | U kunt nu profiteren van de verbeterde aanpassingsfunctionaliteit wanneer u bestanden exporteert vanuit het Experience Platform: <br><ul><li>Aanvullende [ dossier noemende opties ](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Mogelijkheid om de kopballen van het douanedossier in uw uitgevoerde dossiers via de [ verbeterde toewijzingsstap ](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) te plaatsen.</li><li>[ Mogelijkheid om het formatteren van uitgevoerde CSV gegevensdossiers ](/help/destinations/ui/batch-destinations-file-formatting-options.md) aan te passen.</li></ul> <br> Deze functionaliteit wordt ondersteund door de zes nieuwe bètacloud-opslagkaarten in de onderstaande tabel. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte bestemmingen** {#new-or-updated-destinations}

| Doel | Beschrijving |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | De lijn is een populair communicatie platform dat mensen, de diensten en de informatie verbindt en van een praatjeapp tot een hub voor vermaak, sociale, en dagelijkse activiteiten is gegroeid. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 is een op cloud gebaseerd bedrijfstoepassingsplatform dat de Planning van het Middel van de Onderneming (ERP) en het Beheer van de Verhouding van de Klant (CRM) samen met productiviteitstoepassingen en AI hulpmiddelen combineert, om van begin tot eind vlottere en meer gecontroleerde verrichtingen, beter groeipotentieel en lagere kosten te brengen. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | Met de [!DNL (Beta) Adobe Commerce] -doelconnector kunt u een of meer Real-Time CDP-segmenten selecteren die u wilt activeren voor uw [!DNL Adobe Commerce] -account, zodat uw klanten een dynamische, gepersonaliseerde ervaring kunnen opdoen. Binnen [!DNL Adobe Commerce] kunt u die Real-Time CDP-segmenten selecteren om unieke aanbiedingen in het winkelwagentje aan te passen, zoals &#39;Koop 2 krijg 1 gratis&#39;. U kunt ook hoofdbanners weergeven en de productprijzen wijzigen via promotieaanbiedingen, die allemaal zijn aangepast aan Adobe Real-Time CDP-segmenten. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Maak een live uitgaande verbinding met [!DNL Azure Data Lake Storage Gen2] om periodiek gegevensbestanden van Adobe Experience Platform naar uw eigen opslaglocatie te exporteren. Deze nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die door Adobe Experience Platform is ingericht en u toegang biedt tot een veilige, op de cloud gebaseerde opslagfaciliteit voor het opslaan van bestanden om bestanden van het platform te exporteren. Deze nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Maak een live uitgaande verbinding met [!DNL Google Cloud Storage] om periodiek gegevensbestanden van Adobe Experience Platform naar uw eigen emmers te exporteren. Deze nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta-deelnemers zien nu twee [!DNL Amazon S3] doelkaarten naast elkaar in de doelcatalogus. De nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta-deelnemers zien nu twee [!DNL Azure Blob] doelkaarten naast elkaar in de doelcatalogus. De nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta-deelnemers zien nu twee [!DNL SFTP] doelkaarten naast elkaar in de doelcatalogus. De nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie**

| Documentatie | Beschrijving |
| ----------- | ----------- |
| [ de guardrails van Doelen ](../../destinations/guardrails.md) | Deze pagina bevat standaardgebruiks- en tarieflimieten voor activeringsgedrag. |

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gegevenstype | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Het veld `authorized` is bijgewerkt van een booleaans type naar een tekenreeks. `season` en `episode` zijn gewijzigd van gehele getallen in tekenreeksen. |
| Gegevenstype | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | De naam van `name` is gewijzigd in `friendlyName` en de naam van `ID` is gewijzigd in `name` . |
| Gegevenstype | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | De naam van `ID` is gewijzigd in `name` . |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Query-service {#query-service}

Met Query Service kunt u standaard-SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake] . U kunt zich bij om het even welke datasets van [!DNL Data Lake] aansluiten en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Wetenschap van Gegevens Workspace, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| De vragen van de monitor door Platform UI | Het tabblad Query Service [!UICONTROL Scheduled Queries] biedt een verbeterde zichtbaarheid voor de status van alle querytaken via de gebruikersinterface. Vanaf het tabblad [!UICONTROL Scheduled Queries] vindt u belangrijke informatie over de status van de query, waaronder foutberichten en codes voor het geval deze mislukken. U kunt ook op alarm door UI voor om het even welk van deze vragen intekenen die op hun status worden gebaseerd. Zie het [ document van de Vragen van de Monitor ](../../query-service/ui/monitor-queries.md) om meer over deze eigenschap te leren. |
| Vraag versnelde het melden van inzichten gegevensmodel | Als deel van Gegevens Distiller SKU, staat de vraag versnelde opslag u toe om de tijd en de verwerkingscapaciteit te verminderen die wordt vereist om kritieke inzichten van uw gegevens te bereiken. Met de opslag met versnelde query kunt u een aangepast gegevensmodel maken en/of uitbreiden op bestaande Adobe Real-time Customer Data Platform-gegevensmodellen om uw rapporteringsinzichten en hun visualisaties te verbeteren. Zie de [ vraag versnelde opslag die inzichten document ](../../query-service/data-distiller/customizable-insights/reporting-insights-data-model.md) rapporteert om meer over deze eigenschap te leren. |

{style="table-layout:auto"}

Voor meer informatie over de Diensten van de Vraag, verwijs naar het [ overzicht van de Dienst van de Vraag ](../../query-service/home.md).
Nieuwe functies in Adobe Experience Platform:

