---
keywords: Experience Platform;home;populaire onderwerpen;bronconnectors;bronaansluiting;bronnen;gegevensbronnen;gegevensbron;gegevensbronverbinding
solution: Experience Platform
title: Overzicht Source Connectors
description: Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 1%

---

# Overzicht van Source-connectors

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Experience Platform. De service biedt een gebruikersinterface en RESTful API waarmee u eenvoudig bronverbindingen met verschillende gegevensproviders kunt instellen. Deze bronverbindingen laten u toe om uw derdesystemen voor authentiek te verklaren, tijden voor ingestitielooppas te plaatsen, en gegevensinvoer te beheren.

Met Experience Platform kunt u gegevens die u uit verschillende bronnen verzamelt, centraliseren en de daaruit verkregen inzichten gebruiken om meer te doen.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

>[!BEGINSHADEBOX]

## Door Adobe gebouwde en door partners gebouwde bronnen {#adobe-and-partner-built-sources}

Sommige schakelaars in de Experience Platform broncatalogus worden gebouwd en door Adobe gehandhaafd, terwijl anderen door partnerbedrijven worden gebouwd en worden gehandhaafd door [&#x200B; Bronnen SDK &#x200B;](/help/sources/sources-sdk/overview.md) te gebruiken. Een nota bij de bovenkant van de documentatiepagina voor elke partner-gebouwde schakelaarvraag uit als een bron door de partner wordt gecreeerd en gehandhaafd. Bijvoorbeeld, wordt de [&#x200B; schakelaar van Amazon S3 &#x200B;](/help/sources/connectors/cloud-storage/s3.md) gecreeerd door Adobe, terwijl de [&#x200B; schakelaar RainFocus &#x200B;](/help/sources/connectors/analytics/rainfocus.md) door het team RainFocus wordt gecreeerd en gehandhaafd.

Voor partner-authored en onderhouden schakelaars, betekent dit dat de kwesties met de schakelaar door het partnerteam zouden kunnen moeten worden opgelost (contactmethode die in de nota in de documentatiepagina wordt verstrekt). Neem voor problemen met door Adobe ontworpen en onderhouden connectors contact op met uw Adobe-vertegenwoordiger of de klantenservice.

>[!ENDSHADEBOX]

## Broncatalogus

Lees de volgende secties voor een lijst van alle bronnen beschikbaar in de broncatalogus.

### Adobe-toepassingen {#adobe-applications}

Experience Platform staat toe dat gegevens worden ingevoerd van andere Adobe-toepassingen, zoals Adobe Analytics en Adobe Audience Manager. Lees de volgende verwante documenten voor meer informatie:

- [Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics-classificatiegegevens](connectors/adobe-applications/classifications.md)
   - [Een gegevensbronverbinding voor Adobe Analytics Classifications maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics Report Suite-gegevens](connectors/adobe-applications/analytics.md)
   - [Een Adobe Analytics-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Een Adobe Campaign Managed Cloud Services-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Adobe-gegevensverzameling](connectors/adobe-applications/data-collection.md)
   - [Een bronverbinding voor klantkenmerken maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Creeer a [!DNL Marketo Engage]  bronverbinding in UI](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Creeer a  [!DNL Marketo Engage]  bronverbinding en dataflow voor de gegevens van de douaneactiviteit](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Geavanceerde bedrijfsbronnen {#advanced-enterprise-sources}

De volgende bronnen zijn beschikbaar aan [&#x200B; Adobe Real-Time Customer Data Platform Ultimate &#x200B;](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) slechts klanten.

| Bron | Categorie | Type ontsteking | Wolk |
| --- | --- | --- | --- |
| [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) | Cloud-opslag | Streaming | Azure, AWS |
| [[!DNL Amazon Redshift]](connectors/databases/redshift.md) | Database | Batch | Azure, AWS |
| [[!DNL Azure Databricks]](connectors/databases/databricks.md) | Database | Batch | Azure |
| [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) | Cloud Storage | Streaming | Azure, AWS |
| [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) | Database | Batch | Azure |
| [[!DNL Google BigQuery]](connectors/databases/bigquery.md) | Database | Batch | Azure, AWS |
| [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) | Cloud Storage | Streaming | Azure |
| [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) | Database | Streaming | Azure, AWS |
| [[!DNL Snowflake]](connectors/databases/snowflake.md) | Database | Batch | Azure, AWS |

{style="table-layout:auto"}

### Advertising {#advertising}

U kunt de volgende bronnen gebruiken om advertentiegegevens in te voeren naar Experience Platform.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [&#x200B; Advertentie Google &#x200B;](connectors/advertising/ads.md) | Batch | Azure |

{style="table-layout:auto"}

### Analytics {#analytics}

U kunt de volgende bronnen gebruiken om analysegegevens in te voeren naar Experience Platform.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) | Batch | Azure |
| [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) | Streaming | Azure |
| [[!DNL RainFocus]](connectors/analytics/rainfocus.md) | Streaming | Azure |

{style="table-layout:auto"}

### Cloud Storage {#cloud-storage}

Opslagbronnen in de cloud kunnen uw eigen gegevens naar Experience Platform brengen zonder dat ze hoeven te worden gedownload, opgemaakt of geüpload. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema gebruikend het gebruikersinterface. Zie de volgende verwante documenten voor meer informatie:

U kunt de volgende bronnen gebruiken om gegevens over cloudopslag in Experience Platform op te nemen.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) | Batch | Azure |
| [[!DNL Azure Blob Storage]](connectors/cloud-storage/blob.md) | Batch | Azure |
| [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) | Batch | Azure, AWS |
| [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) | Batch | Azure |
| [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) | Batch | Azure |
| [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) | Batch | Azure, AWS |
| [[!DNL FTP]](connectors/cloud-storage/ftp.md) | Batch | Azure |
| [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) | Batch | Azure |
| [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) | Batch | Azure |
| [[!DNL SFTP]](connectors/cloud-storage/sftp.md) | Batch | Azure |

{style="table-layout:auto"}

### Toestemming en voorkeuren {#consent}

U kunt de volgende bronnen gebruiken om toestemmings- en voorkeursgegevens in te voeren voor Experience Platform.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Didomi]](../sources/connectors/consent-and-preferences/didomi.md) | Streaming | Azure |
| [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) | Batch | Azure |

{style="table-layout:auto"}

### Customer Relationship Management (CRM) {#customer-relationship-management}

De systemen van CRM verstrekken gegevens die klantenverhoudingen kunnen helpen bouwen, die beurtelings, loyaliteit creëren en klantenbehoud drijven. Experience Platform biedt ondersteuning voor het opnemen van CRM-gegevens van [!DNL Microsoft Dynamics 365] en [!DNL Salesforce] . Zie de volgende verwante documenten voor meer informatie:

U kunt de volgende bronnen gebruiken om CRM-gegevens in te voeren naar Experience Platform.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) | Batch | Azure |
| [[!DNL Salesforce]](connectors/crm/salesforce.md) | Batch | Azure, AWS |
| [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) | Batch | Azure |
| [[!DNL Veeva CRM]](connectors/crm/veeva.md) | Batch | Azure |

{style="table-layout:auto"}

### Klant geslaagd {#customer-success}

U kunt de volgende bronnen gebruiken om succesgegevens van klanten aan Experience Platform toe te voegen.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) | Batch | Azure |
| [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) | Batch | Azure |
| [[!DNL Zendesk]](connectors/customer-success/zendesk.md) | Batch | Azure |

{style="table-layout:auto"}

### Database {#database}

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een database van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

U kunt de volgende bronnen gebruiken om gegevens van uw database in te voeren naar Experience Platform.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) | Batch | Azure |
| [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) | Batch | Azure |
| [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) | Batch | Azure |
| [[!DNL Azure Table Storage]](connectors/databases/ats.md) | Batch | Azure |
| [[!DNL GreenPlum]](connectors/databases/greenplum.md) | Batch | Azure |
| [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) | Batch | Azure |
| [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) | Batch | Azure |
| [[!DNL MariaDB]](connectors/databases/mariadb.md) | Batch | Azure |
| [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) | Batch | Azure |
| [[!DNL MySQL]](connectors/databases/mysql.md) | Batch | Azure, AWS |
| [[!DNL Oracle]](connectors/databases/oracle.md) | Batch | Azure, AWS |
| [[!DNL PostgreSQL]](connectors/databases/postgres.md) | Batch | Azure, AWS |
| [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) | Batch | Azure |

{style="table-layout:auto"}

### Gegevens- en identiteitspartners {#data-partner}

U kunt de volgende bronnen gebruiken om gegevens en identiteitspartnergegevens in te voeren aan Experience Platform.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) | Batch | Azure |
| [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) | Batch | Azure |
| [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) | Batch | Azure |
| [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) | Batch | Azure |
| [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) | Batch | Azure |
| [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) | Batch | Azure |

{style="table-layout:auto"}

### e-handel {#ecommerce}

U kunt de volgende bronnen gebruiken om e-commercegegevens in te voeren naar Experience Platform.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) | Batch | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify.md) | Batch | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) | Streaming | Azure |

{style="table-layout:auto"}

### Lokaal systeem {#local-system}

U kunt de volgende bronnen gebruiken om gegevens van uw lokale systeem aan Experience Platform in te voeren.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [&#x200B; Lokale dossier uploadt &#x200B;](connectors/local-system/local-file-upload.md) | Batch | Azure |

{style="table-layout:auto"}

### Loyalty {#loyalty}

U kunt de volgende bronnen gebruiken om gegevensloyaliteit aan Experience Platform in te voeren.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Capillary Streaming Events]](connectors/loyalty/capillary.md) | Streaming | Azure |

{style="table-layout:auto"}

### Marketing Automation {#marketing-automation}

U kunt de volgende bronnen gebruiken om gegevens over marketingautomatisering in te voeren naar Experience Platform.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Braze]](connectors/marketing-automation/braze.md) | Streaming | Azure |
| [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) | Streaming | Azure |
| [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) | Streaming | Azure |
| [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) | Batch | Azure |
| [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) | Batch | Azure |
| [[!DNL Oracle Eloqua]  (V2) &#x200B;](connectors/marketing-automation/eloqua.md) | Batch | Azure |
| [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) | Batch | Azure |
| [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) | Batch | Azure |
| [[!DNL Relay Connector]](tutorials/ui/create/marketing-automation/relay-connector.md) | Streaming | Azure |
| [[!DNL Salesforce Marketing Cloud]  (V2) &#x200B;](connectors/marketing-automation/sfmc.md) | Batch | Azure |

{style="table-layout:auto"}

### Betalingen {#payments}

U kunt de volgende bronnen gebruiken om betalingsgegevens in te voeren naar Experience Platform.

| Bron | Type ontsteking | Wolk |
| --- | --- | --- |
| [[!DNL Square]](connectors/payments/square.md) | Batch | Azure |
| [[!DNL Stripe]](connectors/payments/stripe.md) | Batch | Azure |

{style="table-layout:auto"}

### Streaming {#streaming}

U kunt de volgende bronnen gebruiken om gegevens te streamen naar Experience Platform.

| Bron | Type ontsteking | Ondersteuning voor cloud |
| --- | --- | --- |
| [[!DNL HTTP API]](connectors/streaming/http.md) | Streaming | Azure, AWS |

{style="table-layout:auto"}

### Protocollen {#protocols}

U kunt de volgende bronnen gebruiken om protocolgegevens in te voeren naar Experience Platform.

| Bron | Type ontsteking | Ondersteuning voor cloud |
| --- | --- | --- |
| [[!DNL Generic OData]](connectors/protocols/odata.md) | Batch | Azure |
| [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) | Batch | Azure |

{style="table-layout:auto"}

## Toegangsbeheer voor bronnen bij gegevensinvoer

Machtigingen voor bronnen in gegevensinvoer kunnen binnen de Adobe Admin Console worden beheerd. U hebt toegang tot machtigingen via het tabblad **[!UICONTROL Permissions]** in een bepaald productprofiel. Via het menu-item **[!UICONTROL Edit Permissions]** hebt u via het deelvenster **[!UICONTROL data ingestion]** toegang tot de machtigingen voor bronnen. De machtiging **[!UICONTROL View Sources]** verleent alleen-lezen toegang tot beschikbare bronnen op het tabblad **[!UICONTROL Catalog]** en voor authentiek verklaarde bronnen op het tabblad **[!UICONTROL Browse]** , terwijl met de machtiging **[!UICONTROL Manage Sources]** volledige toegang wordt verleend tot het lezen, maken, bewerken en uitschakelen van bronnen.

De volgende lijst schetst hoe UI zich gedraagt gebaseerd op verschillende combinaties van deze toestemmingen:

| Machtigingsniveau | Beschrijving |
| ---- | ----|
| **[!UICONTROL View Sources]** Aan | De read-only toegang van de subsidie tot bronnen in elk bron-type op het lusje van de Catalogus, evenals doorbladeren, Rekeningen, en lusjes Dataflow. |
| **[!UICONTROL Manage Sources]** Aan | Naast de functies die in **[!UICONTROL View Sources]** zijn opgenomen, verleent u toegang tot de optie **[!UICONTROL Connect Source]** in **[!UICONTROL Catalog]** en **[!UICONTROL Select Data]** in **[!UICONTROL Browse]** . Met **[!UICONTROL Manage Sources]** kunt u **[!UICONTROL DataFlows]** ook in- of uitschakelen en de schema&#39;s ervan bewerken. |
| **[!UICONTROL View Sources]** Uit en **[!UICONTROL Manage Sources]** Uit | Alle toegang tot bronnen intrekken. |

Voor meer informatie over de beschikbare toestemmingen die door de Toestemmingen van Adobe worden verleend, lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](../access-control/home.md).

### Toegangsbeheer op basis van kenmerken

Met toegangsbeheer op basis van kenmerken in Adobe Experience Platform kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van kenmerken.

Met op attribuut-gebaseerde toegangsbeheer, kunt u toewijzingsconfiguraties op gebieden toepassen die u toestemmingen hebt. Bovendien kunt u geen gegevens aan een dataset opnemen als u geen toegang tot alle gebieden in de dataset hebt.

#### Ondersteuning voor op kenmerken gebaseerde toegangscontrole in bronnen

>[!TIP]
>
>Op attributen-gebaseerde toegangsbeheer werkt als volgt: **rollen** worden gecreeerd om de types van gebruikers te categoriseren die met uw instantie van Experience Platform in wisselwerking staan. **de Etiketten** worden toegepast op **rollen** om de toegang van die bepaalde rol aan te wijzen. **de Etiketten** worden ook toegepast op middelen zoals schemagebieden en segmenten. Opdat een gebruiker toegang tot bepaalde schemagebieden en segmenten heeft, moeten zij aan *een rol met het zelfde etiket worden toegevoegd dat aan het gevraagde middel* wordt toegewezen. Voor meer informatie, lees de [&#x200B; op attributen-gebaseerde gids van begin tot eind van de toegangscontrole &#x200B;](../access-control/abac/end-to-end-guide.md).

- Pas etiketten op schemagebieden toe om toegang tot specifieke schemagebieden in uw organisatie te bepalen. Zodra de toegang tot specifieke schemagebieden wordt gevestigd, zullen de gebruikers slechts afbeeldingen voor de gebieden kunnen tot stand brengen die zij toegang hebben tot.
- Gebruikers zonder de juiste rollen kunnen geen dataflows met toewijzingen maken of bijwerken die ontoegankelijke schemavelden bevatten. Bovendien kunnen onbevoegde gebruikers bestaande gegevensstromen met ontoegankelijke schemavelden niet bijwerken, verwijderen, inschakelen of uitschakelen.
- Bovendien, moet een dataflow precies zelfde schema identiteitskaart en versie in zijn afbeelding, doeldataset, en doelverbinding hebben. Dit geldt voor zowel standaard XDM-schema&#39;s als relationele schema&#39;s.

>[!NOTE]
>
>Relationele schema&#39;s hebben aanvullende vereisten, waaronder velden voor primaire sleutel en versie-id. Voor meer informatie, zie het [&#x200B; relationele schemaoverzicht &#x200B;](../xdm/schema/relational.md).

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, lees het [&#x200B; op attributen-gebaseerde toegangsbeheeroverzicht &#x200B;](../access-control/abac/overview.md).

## Voorwaarden en bepalingen {#terms-and-conditions}

Door om het even welke bronnen te gebruiken die als bèta (&quot;Beta&quot;) worden geëtiketteerd, bevestigt u hierbij dat Beta ***&quot;zoals is&quot;zonder enige garantie van welke aard*** wordt verstrekt.

Adobe is niet verplicht de Beta te onderhouden, te corrigeren, bij te werken, te wijzigen, te wijzigen of anderszins te ondersteunen. U wordt aangeraden informatief te zijn en op geen enkele wijze te vertrouwen op de juiste werking of prestaties van dergelijke Beta en/of begeleidende materialen. De Beta wordt beschouwd als vertrouwelijke informatie van Adobe.

Alle &quot;Feedback&quot; (informatie over de Beta, inclusief maar niet beperkt tot problemen of defecten die u tegenkomt bij het gebruik van de Beta, suggesties, verbeteringen en aanbevelingen) die u aan Adobe verstrekt, worden hierbij aan Adobe toegewezen, inclusief alle rechten, titel en interesse in en voor dergelijke feedback.

Verzend Open Feedback of maak een Support Ticket om uw suggesties te delen of een bug te melden en een functieverbetering te zoeken.
