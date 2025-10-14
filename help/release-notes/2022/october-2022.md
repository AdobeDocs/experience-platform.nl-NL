---
title: Aanvullende informatie van oktober 2022 voor Adobe Experience Platform
description: Aanvullende informatie van oktober 2022 voor Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 26%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 26 oktober 2022**

- [Door de klant beheerde sleutels](#cmk)
- [Dataverzameling](#data-collection)
- [Bestemmingen](#destinations)
- [Experience Data Model](#xdm)
- [Query-service](#query-service)

## Door de klant beheerde sleutels {#cmk}

Alle gegevens die op Adobe Experience Platform zijn opgeslagen, worden in rust gecodeerd met systeemtoetsen. Als u een toepassing gebruikt die op Experience Platform is gebouwd, kunt u nu ervoor kiezen om uw eigen coderingssleutels te gebruiken, zodat u meer controle hebt over de gegevensbeveiliging.

Zie het overzicht op [&#x200B; klant-geleide sleutels &#x200B;](../../landing/governance-privacy-security/customer-managed-keys/overview.md) voor details op de eigenschap.

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gevoelige gegevensverwerking voor gegevensstromen | Gegevensstromen maken nu gebruik van verschillende Experience Platform-technologieën om gevoelige gegevens op de juiste manier te verwerken, zoals wordt voorgeschreven door bijvoorbeeld de Health Insurance Portability and Accountability Act (HIPAA). Zie de sectie over [omgaan met gevoelige gegevens in datastreams](../../datastreams/overview.md#sensitive) voor meer informatie. |
| [!DNL Splunk] extensie voor het doorsturen van gebeurtenissen | U kunt gegevens aan [!DNL Splunk] nu verzenden gebruikend een [&#x200B; gebeurtenis die &#x200B;](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Splunk] extensieoverzicht](../../tags/extensions/server/splunk/overview.md) voor meer informatie. |
| [!DNL Zendesk] extensie voor het doorsturen van gebeurtenissen | U kunt gegevens aan [!DNL Zendesk] nu verzenden gebruikend een [&#x200B; gebeurtenis die &#x200B;](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Zendesk] extensieoverzicht](../../tags/extensions/server/zendesk/overview.md) voor meer informatie. |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| (Beta) Dataset exporteren | De [&#x200B; functie van de Uitvoer van de Dataset Beta &#x200B;](/help/destinations/ui/export-datasets.md) staat u toe om eerste generatiegegevens (zoals die in de [&#x200B; het productbeschrijving van Real-Time Customer Data Platform &#x200B;](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) worden bepaald) uit Adobe Experience Platform naar uw eigen externe klantensystemen, via het interface van bestemmingsgebruiker uit te voeren. Op deze manier kunt u gegevens uit Experience Platform ophalen met een workflow zonder code/lage code naar zes cloudopslagbestemmingen (vermeld in de onderstaande tabel) voor analytische en compatibiliteitsgevallen. |
| (Beta) Verbeterde exportmogelijkheden voor bestanden | U kunt nu profiteren van de verbeterde aanpassingsfunctionaliteit wanneer u bestanden exporteert vanuit Experience Platform: <br><ul><li>Aanvullende [&#x200B; dossier noemende opties &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Mogelijkheid om de kopballen van het douanedossier in uw uitgevoerde dossiers via de [&#x200B; verbeterde toewijzingsstap &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) te plaatsen.</li><li>[&#x200B; Mogelijkheid om het formatteren van uitgevoerde CSV gegevensdossiers &#x200B;](/help/destinations/ui/batch-destinations-file-formatting-options.md) aan te passen.</li></ul> <br> Deze functionaliteit wordt ondersteund door de zes nieuwe bètacloud-opslagkaarten in de onderstaande tabel. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte bestemmingen** {#new-or-updated-destinations}

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | De lijn is een populair communicatie platform dat mensen, de diensten en de informatie verbindt en van een praatjeapp tot een hub voor vermaak, sociale, en dagelijkse activiteiten is gegroeid. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 is een op cloud gebaseerd bedrijfstoepassingsplatform dat de Planning van het Middel van de Onderneming (ERP) en het Beheer van de Verhouding van de Klant (CRM) samen met productiviteitstoepassingen en AI hulpmiddelen combineert, om van begin tot eind vlottere en meer gecontroleerde verrichtingen, beter groeipotentieel en lagere kosten te brengen. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | Met de [!DNL (Beta) Adobe Commerce] -doelconnector kunt u een of meer Real-Time CDP-segmenten selecteren die u wilt activeren voor uw [!DNL Adobe Commerce] -account, zodat uw klanten een dynamische, gepersonaliseerde ervaring kunnen opdoen. Binnen [!DNL Adobe Commerce] kunt u die Real-Time CDP-segmenten selecteren om unieke aanbiedingen in het winkelwagentje aan te passen, zoals &#39;Koop 2 krijg 1 gratis&#39;. U kunt ook hoofdbanners weergeven en de productprijzen wijzigen via promotieaanbiedingen, die allemaal zijn aangepast aan Adobe Real-Time CDP-segmenten. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Maak een live uitgaande verbinding met [!DNL Azure Data Lake Storage Gen2] om periodiek gegevensbestanden van Adobe Experience Platform naar uw eigen opslaglocatie te exporteren. Deze nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die door Adobe Experience Platform is ingericht en u toegang biedt tot een veilige, op de cloud gebaseerde opslagfaciliteit voor het opslaan van bestanden om bestanden uit Experience Platform te exporteren. Deze nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Maak een live uitgaande verbinding met [!DNL Google Cloud Storage] om periodiek gegevensbestanden van Adobe Experience Platform naar uw eigen emmers te exporteren. Deze nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta-deelnemers zien nu twee [!DNL Amazon S3] doelkaarten naast elkaar in de doelcatalogus. De nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta-deelnemers zien nu twee [!DNL Azure Blob] doelkaarten naast elkaar in de doelcatalogus. De nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta-deelnemers zien nu twee [!DNL SFTP] doelkaarten naast elkaar in de doelcatalogus. De nieuwe bètabestemming biedt verbeterde functionaliteit voor het exporteren van bestanden en ondersteunt het exporteren van gegevenssets. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie**

| Documentatie | Beschrijving |
| ----------- | ----------- |
| [&#x200B; de guardrails van Doelen &#x200B;](../../destinations/guardrails.md) | Deze pagina bevat standaardgebruiks- en tarieflimieten voor activeringsgedrag. |

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gegevenstype | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Het veld `authorized` is bijgewerkt van een booleaans type naar een tekenreeks. `season` en `episode` zijn gewijzigd van gehele getallen in tekenreeksen. |
| Gegevenstype | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | De naam van `name` is gewijzigd in `friendlyName` en de naam van `ID` is gewijzigd in `name` . |
| Gegevenstype | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | De naam van `ID` is gewijzigd in `name` . |

{style="table-layout:auto"}

Voor meer informatie over XDM in Experience Platform, zie het [&#x200B; XDM overzicht van het Systeem &#x200B;](../../xdm/home.md).

## Query-service {#query-service}

Met de Query-service kunt u standaard SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake]. U kunt willekeurige datasets van [!DNL Data Lake] combineren en de queryresultaten vastleggen als nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bewaak query&#39;s via de gebruikersinterface van Experience Platform | Het tabblad Query Service [!UICONTROL Scheduled Queries] biedt een verbeterde zichtbaarheid voor de status van alle querytaken via de gebruikersinterface. Vanaf het tabblad [!UICONTROL Scheduled Queries] vindt u belangrijke informatie over de status van de query, waaronder foutberichten en codes voor het geval deze mislukken. U kunt ook op alarm door UI voor om het even welk van deze vragen intekenen die op hun status worden gebaseerd. Zie het [&#x200B; document van de Vragen van de Monitor &#x200B;](../../query-service/ui/monitor-queries.md) om meer over deze eigenschap te leren. |
| Vraag versnelde het melden van inzichten gegevensmodel | Als deel van Gegevens Distiller SKU, staat de vraag versnelde opslag u toe om de tijd en de verwerkingscapaciteit te verminderen die wordt vereist om kritieke inzichten van uw gegevens te bereiken. Met de opslag met versnelde query kunt u een aangepast gegevensmodel maken en/of uitbreiden op bestaande Adobe Real-Time Customer Data Platform-gegevensmodellen om uw rapporteringsinzichten en hun visualisaties te verbeteren. Zie de [&#x200B; vraag versnelde opslag die inzichten document &#x200B;](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md) rapporteert om meer over deze eigenschap te leren. |

{style="table-layout:auto"}

Voor meer informatie over de Diensten van de Vraag, verwijs naar het [&#x200B; overzicht van de Dienst van de Vraag &#x200B;](../../query-service/home.md).
Nieuwe functies in Adobe Experience Platform:

