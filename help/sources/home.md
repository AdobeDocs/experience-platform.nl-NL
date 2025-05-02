---
keywords: Experience Platform;home;populaire onderwerpen;bronconnectors;bronaansluiting;bronnen;gegevensbronnen;gegevensbron;gegevensbronverbinding
solution: Experience Platform
title: Overzicht Source Connectors
description: Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 5637a12d5f9cc14b6cf3d88f018aa92de06ab739
workflow-type: tm+mt
source-wordcount: '1529'
ht-degree: 0%

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

## Geavanceerde bedrijfsbronnen {#advanced-enterprise-sources}

De volgende bronnen zijn beschikbaar aan [ Adobe Real-Time Customer Data Platform Ultimate ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) slechts klanten.

- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE  Streaming ]{type=Positive}
- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Azure Databricks]](connectors/databases/databricks.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE  Streaming ]{type=Positive}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE  Streaming ]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE  Streaming ]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE  Partij ]{type=Informative}

## Door Adobe gebouwde en door partners gebouwde bronnen {#adobe-and-partner-built-sources}

Sommige schakelaars in de Experience Platform broncatalogus worden gebouwd en door Adobe gehandhaafd, terwijl anderen door partnerbedrijven worden gebouwd en worden gehandhaafd door [ Bronnen SDK ](/help/sources/sources-sdk/overview.md) te gebruiken. Een nota bij de bovenkant van de documentatiepagina voor elke partner-gebouwde schakelaarvraag uit als een bron door de partner wordt gecreeerd en gehandhaafd. Bijvoorbeeld, wordt de [ schakelaar van Amazon S3 ](/help/sources/connectors/cloud-storage/s3.md) gecreeerd door Adobe, terwijl de [ schakelaar RainFocus ](/help/sources/connectors/analytics/rainfocus.md) door het team RainFocus wordt gecreeerd en gehandhaafd.

Voor partner-authored en onderhouden schakelaars, betekent dit dat de kwesties met de schakelaar door het partnerteam zouden kunnen moeten worden opgelost (contactmethode die in de nota in de documentatiepagina wordt verstrekt). Neem voor problemen met door Adobe ontworpen en onderhouden connectors contact op met uw Adobe-vertegenwoordiger of de klantenservice.

## Broncategorieën

Bronnen in Experience Platform zijn gegroepeerd in de volgende categorieën:

### Adobe-toepassingen {#adobe-applications}

Experience Platform staat toe dat gegevens worden ingevoerd van andere Adobe-toepassingen, zoals Adobe Analytics en Adobe Audience Manager. Zie de volgende verwante documenten voor meer informatie:

- [Adobe Audience Manager-bronoverzicht](connectors/adobe-applications/audience-manager.md)
   - [Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Overzicht van Adobe Analytics Classifications Data source](connectors/adobe-applications/classifications.md)
   - [Een gegevensbronverbinding voor Adobe Analytics Classifications maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/classifications.md)
- [Overzicht van Adobe Analytics Report Suite-gegevensbron](connectors/adobe-applications/analytics.md)
   - [Een Adobe Analytics-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services-bronoverzicht](connectors/adobe-applications/campaign.md)
   - [Een Adobe Campaign Managed Cloud Services-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce-bronoverzicht](connectors/adobe-applications/commerce.md)
- [Overzicht van Adobe-gegevensbron voor gegevensverzameling](connectors/adobe-applications/data-collection.md)
   - [Een bronverbinding voor klantkenmerken maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] bronoverzicht](connectors/adobe-applications/marketo/marketo.md)
   - [Creeer a [!DNL Marketo Engage]  bronverbinding in UI](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Creeer a  [!DNL Marketo Engage]  bronverbinding en dataflow voor de gegevens van de douaneactiviteit](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Advertising {#advertising}

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een derde-advertentiesysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [ Google Adds ](connectors/advertising/ads.md) [!BADGE  Partij ]{type=Informative}

### Analytics {#analytics}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een extern analyseplatform. Lees de volgende verwante documenten voor meer informatie:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE  Streaming ]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE  Streaming ]{type=Positive}

### Cloud Storage {#cloud-storage}

Opslagbronnen in de cloud kunnen uw eigen gegevens naar Experience Platform brengen zonder dat ze hoeven te worden gedownload, opgemaakt of geüpload. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema gebruikend het gebruikersinterface. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE  Partij ]{type=Informative}

### Toestemming en voorkeuren {#consent}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een platform voor toestemming en voorkeurenbeheer van derden. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE  Partij ]{type=Informative}

### Customer Relationship Management (CRM) {#customer-relationship-management}

De systemen van CRM verstrekken gegevens die klantenverhoudingen kunnen helpen bouwen, die beurtelings, loyaliteit creëren en klantenbehoud drijven. Experience Platform biedt ondersteuning voor het opnemen van CRM-gegevens van [!DNL Microsoft Dynamics 365] en [!DNL Salesforce] . Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE  Partij ]{type=Informative}

### Klant geslaagd {#customer-success}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor klantsucces van derden. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE  Partij ]{type=Informative}

### Database {#database}

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een database van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE  Partij ]{type=Informative}

### Gegevens- en identiteitspartners {#data-partner}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een data- en identiteitspartner. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE  Partij ]{type=Informative}

### eCommerce {#ecommerce}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een eCommerce-systeem van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE  Streaming ]{type=Positive}

### Lokaal systeem {#local-system}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van uw lokale systeem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Lokale bestanden uploaden](connectors/local-system/local-file-upload.md)

### Marketing Automation {#marketing-automation}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een derde marketingautomatiseringssysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Braze]](connectors/marketing-automation/braze.md) [!BADGE  Streaming ]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE  Streaming ]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE  Streaming ]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE  Partij ]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### Betalingen {#payments}

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een betalingssysteem van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Stripe]](connectors/payments/stripe.md) [!BADGE  Partij ]{type=Informative}

### Streaming {#streaming}

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit streamingbronnen. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE  Streaming ]{type=Positive}

### Protocollen {#protocols}

Experience Platform verleent steun voor het opnemen van gegevens van een systeem van derdeprotocollen. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE  Partij ]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE  Partij ]{type=Informative}

## Toegangsbeheer voor bronnen bij gegevensinvoer

Machtigingen voor bronnen in gegevensinvoer kunnen binnen de Adobe Admin Console worden beheerd. U hebt toegang tot machtigingen via het tabblad **[!UICONTROL Permissions]** in een bepaald productprofiel. Via het menu-item **[!UICONTROL data ingestion]** hebt u via het deelvenster **[!UICONTROL Edit Permissions]** toegang tot de machtigingen voor bronnen. De machtiging **[!UICONTROL View Sources]** verleent alleen-lezen toegang tot beschikbare bronnen op het tabblad **[!UICONTROL Catalog]** en voor authentiek verklaarde bronnen op het tabblad **[!UICONTROL Browse]** , terwijl met de machtiging **[!UICONTROL Manage Sources]** volledige toegang wordt verleend tot het lezen, maken, bewerken en uitschakelen van bronnen.

De volgende lijst schetst hoe UI zich gedraagt gebaseerd op verschillende combinaties van deze toestemmingen:

| Machtigingsniveau | Beschrijving |
| ---- | ----|
| **[!UICONTROL View Sources]** Aan | De read-only toegang van de subsidie tot bronnen in elk bron-type op het lusje van de Catalogus, evenals doorbladeren, Rekeningen, en lusjes Dataflow. |
| **[!UICONTROL Manage Sources]** Aan | Naast de functies die in **[!UICONTROL View Sources]** zijn opgenomen, verleent u toegang tot de optie **[!UICONTROL Connect Source]** in **[!UICONTROL Catalog]** en **[!UICONTROL Select Data]** in **[!UICONTROL Browse]** . Met **[!UICONTROL Manage Sources]** kunt u **[!UICONTROL DataFlows]** ook in- of uitschakelen en de schema&#39;s ervan bewerken. |
| **[!UICONTROL View Sources]** Uit en **[!UICONTROL Manage Sources]** Uit | Alle toegang tot bronnen intrekken. |

Voor meer informatie over de beschikbare toestemmingen die door de Toestemmingen van Adobe worden verleend, lees het [ overzicht van de toegangscontrole ](../access-control/home.md).

### Toegangsbeheer op basis van kenmerken

Met toegangsbeheer op basis van kenmerken in Adobe Experience Platform kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van kenmerken.

Met op attribuut-gebaseerde toegangsbeheer, kunt u toewijzingsconfiguraties op gebieden toepassen die u toestemmingen hebt. Bovendien kunt u geen gegevens aan een dataset opnemen als u geen toegang tot alle gebieden in de dataset hebt.

#### Ondersteuning voor op kenmerken gebaseerde toegangscontrole in bronnen

>[!TIP]
>
>Op attributen-gebaseerde toegangsbeheer werkt als volgt: **rollen** worden gecreeerd om de types van gebruikers te categoriseren die met uw instantie van Experience Platform in wisselwerking staan. **de Etiketten** worden toegepast op **rollen** om de toegang van die bepaalde rol aan te wijzen. **de Etiketten** worden ook toegepast op middelen zoals schemagebieden en segmenten. Opdat een gebruiker toegang tot bepaalde schemagebieden en segmenten heeft, moeten zij aan *een rol met het zelfde etiket worden toegevoegd dat aan het gevraagde middel* wordt toegewezen. Voor meer informatie, lees de [ op attributen-gebaseerde gids van begin tot eind van de toegangscontrole ](../access-control/abac/end-to-end-guide.md).

- Pas etiketten op schemagebieden toe om toegang tot specifieke schemagebieden in uw organisatie te bepalen. Zodra de toegang tot specifieke schemagebieden wordt gevestigd, zullen de gebruikers slechts afbeeldingen voor de gebieden kunnen tot stand brengen die zij toegang hebben tot.
- Gebruikers zonder de juiste rollen kunnen geen dataflows met toewijzingen maken of bijwerken die ontoegankelijke schemavelden bevatten. Bovendien kunnen onbevoegde gebruikers bestaande gegevensstromen met ontoegankelijke schemavelden niet bijwerken, verwijderen, inschakelen of uitschakelen.
- Bovendien, moet een dataflow precies zelfde schema identiteitskaart en versie in zijn afbeelding, doeldataset, en doelverbinding hebben.

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, lees het [ op attributen-gebaseerde toegangsbeheeroverzicht ](../access-control/abac/overview.md).

## Voorwaarden en bepalingen {#terms-and-conditions}

Door om het even welke bronnen te gebruiken die als bèta (&quot;Beta&quot;) worden geëtiketteerd, bevestigt u hierbij dat Beta ***&quot;zoals is&quot;zonder enige garantie van welke aard*** wordt verstrekt.

Adobe is niet verplicht de Beta te onderhouden, te corrigeren, bij te werken, te wijzigen, te wijzigen of anderszins te ondersteunen. U wordt aangeraden informatief te zijn en op geen enkele wijze te vertrouwen op de juiste werking of prestaties van dergelijke Beta en/of begeleidende materialen. De Beta wordt beschouwd als vertrouwelijke informatie van Adobe.

Alle &quot;Feedback&quot; (informatie over de Beta, inclusief maar niet beperkt tot problemen of defecten die u tegenkomt bij het gebruik van de Beta, suggesties, verbeteringen en aanbevelingen) die u aan Adobe verstrekt, worden hierbij aan Adobe toegewezen, inclusief alle rechten, titel en interesse in en voor dergelijke feedback.

Verzend Open Feedback of maak een Support Ticket om uw suggesties te delen of een bug te melden en een functieverbetering te zoeken.
