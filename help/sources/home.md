---
keywords: Experience Platform;thuis;populaire onderwerpen;bronschakelaars;bronschakelaar;bronnen;gegevensbronnen;gegevensbron;gegevensbronverbinding
solution: Experience Platform
title: Overzicht van bronconnectors
description: Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 0%

---

# Overzicht van bronconnectors

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

[!DNL Flow Service] wordt gebruikt om klantgegevens van diverse verschillende bronnen binnen Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waarmee u eenvoudig bronverbindingen met verschillende gegevensproviders kunt instellen. Deze bronverbindingen laten u toe om uw derdesystemen voor authentiek te verklaren, tijden voor ingestitielooppas te plaatsen, en gegevensinvoer te beheren.

Met Experience Platform, kunt u gegevens centraliseren u uit verschillende bronnen verzamelt en de inzichten gebruiken die uit het worden verkregen om meer te doen.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Adobe-gebouwde en partner-gebouwde bronnen {#adobe-and-partner-built-sources}

Sommige schakelaars in de de broncatalogus van het Experience Platform worden gebouwd en door Adobe gehandhaafd, terwijl anderen door partnerbedrijven worden gebouwd en worden gehandhaafd door te gebruiken [Bronnen-SDK](/help/sources/sources-sdk/overview.md). Een nota bij de bovenkant van de documentatiepagina voor elke partner-gebouwde schakelaarvraag uit als een bron door de partner wordt gecreeerd en gehandhaafd. Bijvoorbeeld de [Amazon S3-connector](/help/sources/connectors/cloud-storage/s3.md) wordt gemaakt door Adobe, terwijl de [RainFocus-connector](/help/sources/connectors/analytics/rainfocus.md) wordt gecreeerd en door het team RainFocus gehandhaafd.

Voor partner-authored en onderhouden schakelaars, betekent dit dat de kwesties met de schakelaar door het partnerteam zouden kunnen moeten worden opgelost (contactmethode die in de nota in de documentatiepagina wordt verstrekt). Neem voor problemen met door de Adobe ontworpen en onderhouden connectors contact op met uw Adobe of de klantenservice.

## Typen bronnen

Bronnen in Experience Platform worden gegroepeerd in de volgende categorieën:

### Adoben {#adobe-applications}

Met Experience Platform kunnen gegevens uit andere Adobe-toepassingen, zoals Adobe Analytics en Adobe Audience Manager, worden ingevoerd. Zie de volgende verwante documenten voor meer informatie:

- [Adobe Audience Manager-bronoverzicht](connectors/adobe-applications/audience-manager.md)
   - [Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Overzicht van Adobe Analytics Classifications Data source](connectors/adobe-applications/classifications.md)
   - [Een gegevensbronverbinding voor Adobe Analytics Classifications maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/classifications.md)
- [Overzicht van Adobe Analytics Report Suite-gegevensbron](connectors/adobe-applications/analytics.md)
   - [Een Adobe Analytics-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services-bronoverzicht](connectors/adobe-applications/campaign.md)
   - [Een Adobe Campaign Managed Cloud Services-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce-bronoverzicht](connectors/adobe-applications/commerce.md)
- [Overzicht van de bron voor gegevensverzameling voor Adoben](connectors/adobe-applications/data-collection.md)
   - [Een bronverbinding voor klantkenmerken maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] bronoverzicht](connectors/adobe-applications/marketo/marketo.md)
   - [Een [!DNL Marketo Engage] bronverbinding in de gebruikersinterface](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Een [!DNL Marketo Engage] bronverbinding en gegevensstroom voor gegevens met aangepaste activiteit](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Advertising {#advertising}

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een derde-advertentiesysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Google Adds](connectors/advertising/ads.md) [!BADGE Batch]{type=Informative}

### Analytics {#analytics}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een extern analyseplatform. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE Batch]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE Streaming]{type=Positive}

### Cloud Storage {#cloud-storage}

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen naar Platform zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema gebruikend het gebruikersinterface. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE Batch]{type=Informative}
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE Batch]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE Batch]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE Batch]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE Batch]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE Batch]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE Batch]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE Batch]{type=Informative}

### Toestemming en voorkeuren {#consent}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een platform voor toestemming en voorkeurenbeheer van derden. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE Batch]{type=Informative}

### Customer Relationship Management (CRM) {#customer-relationship-management}

De systemen van CRM verstrekken gegevens die klantenverhoudingen kunnen helpen bouwen, die beurtelings, loyaliteit creëren en klantenbehoud drijven. Experience Platform biedt ondersteuning voor het opnemen van CRM-gegevens van [!DNL Microsoft Dynamics 365] en [!DNL Salesforce]. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE Batch]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE Batch]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE Batch]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE Batch]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE Batch]{type=Informative}

### Klant geslaagd {#customer-success}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor klantsucces van derden. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE Batch]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE Batch]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE Batch]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE Batch]{type=Informative}

### Database {#database}

Experience Platform verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE Batch]{type=Informative}
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE Batch]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE Batch]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE Batch]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE Batch]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE Batch]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE Batch]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE Batch]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE Batch]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE Batch]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE Batch]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE Batch]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE Batch]{type=Informative}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE Batch]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE Batch]{type=Informative}

### Gegevenspartner {#data-partner}

Experience Platform verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE Batch]{type=Informative}

### eCommerce {#ecommerce}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een eCommerce-systeem van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE Batch]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE Batch]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE Streaming]{type=Positive}

### Lokaal systeem {#local-system}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van uw lokale systeem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Lokale bestanden uploaden](connectors/local-system/local-file-upload.md)

### Marketing Automation {#marketing-automation}

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een derde marketingautomatiseringssysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Braze]](tutorials/ui/create/marketing-automation/braze.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE Batch]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE Batch]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE Batch]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### Betalingen {#payments}

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een betalingssysteem van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE Batch]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE Batch]{type=Informative}

### Streaming {#streaming}

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit streamingbronnen. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE Streaming]{type=Positive}

### Protocollen {#protocols}

Experience Platform verleent steun voor het opnemen van gegevens van een systeem van derdeprotocollen. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE Batch]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE Batch]{type=Informative}

## Toegangsbeheer voor bronnen bij gegevensinvoer

Machtigingen voor bronnen in gegevensinvoer kunnen binnen de Adobe Admin Console worden beheerd. U hebt toegang tot machtigingen via de **[!UICONTROL Permissions]** in een bepaald productprofiel. Van de **[!UICONTROL Edit Permissions]** kunt u de machtigingen voor bronnen openen via het dialoogvenster **[!UICONTROL data ingestion]** menu-item. De **[!UICONTROL View Sources]** toestemming verleent read-only toegang tot beschikbare bronnen in **[!UICONTROL Catalog]** tabblad en geverifieerde bronnen in het dialoogvenster **[!UICONTROL Browse]** terwijl de **[!UICONTROL Manage Sources]** met deze machtiging hebt u volledige toegang tot het lezen, maken, bewerken en uitschakelen van bronnen.

De volgende lijst schetst hoe UI zich gedraagt gebaseerd op verschillende combinaties van deze toestemmingen:

| Machtigingsniveau | Beschrijving |
| ---- | ----|
| **[!UICONTROL View Sources]** Aan | De read-only toegang van de subsidie tot bronnen in elk bron-type op het lusje van de Catalogus, evenals doorbladeren, Rekeningen, en lusjes Dataflow. |
| **[!UICONTROL Manage Sources]** Aan | Naast de in **[!UICONTROL View Sources]** verleent toegang tot **[!UICONTROL Connect Source]** optie in **[!UICONTROL Catalog]** en **[!UICONTROL Select Data]** optie in **[!UICONTROL Browse]**. **[!UICONTROL Manage Sources]** staat u ook toe om in of onbruikbaar te maken **[!UICONTROL DataFlows]** en bewerk de planning. |
| **[!UICONTROL View Sources]** Uit en **[!UICONTROL Manage Sources]** Uit | Alle toegang tot bronnen intrekken. |

Voor meer informatie over de beschikbare toestemmingen die door de Toestemmingen van de Adobe worden verleend, lees [toegangsbeheeroverzicht](../access-control/home.md).

### Toegangsbeheer op basis van kenmerken

Met toegangsbeheer op basis van kenmerken in Adobe Experience Platform kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van kenmerken.

Met op attribuut-gebaseerde toegangsbeheer, kunt u toewijzingsconfiguraties op gebieden toepassen die u toestemmingen hebt. Bovendien kunt u geen gegevens aan een dataset opnemen als u geen toegang tot alle gebieden in de dataset hebt.

#### Ondersteuning voor op kenmerken gebaseerd toegangsbeheer in bronnen

>[!TIP]
>
>Toegangsbeheer op basis van kenmerken werkt als volgt: **rollen** worden gecreeerd om de types van gebruikers te categoriseren die met uw instantie van het Platform in wisselwerking staan. **Labels** worden toegepast op **rollen** de toegang tot die bepaalde rol aan te wijzen. **Labels** worden ook toegepast op bronnen zoals schemavelden en segmenten. Als u wilt dat een gebruiker toegang heeft tot bepaalde schemavelden en segmenten, moet u deze toevoegen aan *een rol met het zelfde etiket dat aan het gevraagde middel wordt toegewezen*. Lees voor meer informatie de [attribuut-based toegangsbeheergids van begin tot eind](../access-control/abac/end-to-end-guide.md).

- Pas etiketten op schemagebieden toe om toegang tot specifieke schemagebieden in uw organisatie te bepalen. Zodra de toegang tot specifieke schemagebieden wordt gevestigd, zullen de gebruikers slechts afbeeldingen voor de gebieden kunnen tot stand brengen die zij toegang hebben tot.
- Gebruikers zonder de juiste rollen kunnen geen dataflows met toewijzingen maken of bijwerken die ontoegankelijke schemavelden bevatten. Bovendien kunnen onbevoegde gebruikers bestaande gegevensstromen met ontoegankelijke schemavelden niet bijwerken, verwijderen, inschakelen of uitschakelen.
- Bovendien, moet een dataflow precies zelfde schema identiteitskaart en versie in zijn afbeelding, doeldataset, en doelverbinding hebben.

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, lees [op attributen-gebaseerd toegangsbeheeroverzicht](../access-control/abac/overview.md).

## Voorwaarden en bepalingen {#terms-and-conditions}

Door een van de bronnen met het label bèta (&quot;Beta&quot;) te gebruiken, bevestigt u hierbij dat de bèta wordt geleverd ***&quot;zoals is&quot; zonder enige garantie***.

Adobe is niet verplicht het bètaprogramma te onderhouden, te corrigeren, bij te werken, te wijzigen, te wijzigen of anderszins te ondersteunen. U wordt geadviseerd om Informatief te gebruiken en op geen enkele wijze te vertrouwen op de correcte werking of prestaties van dergelijke bèta en/of begeleidende materialen. De bètaversie wordt beschouwd als vertrouwelijke informatie over Adobe.

Elke &quot;feedback&quot; (informatie over de bètaversie, inclusief maar niet beperkt tot problemen of defecten die u tegenkomt bij het gebruik van de bètaversie, suggesties, verbeteringen en aanbevelingen) die u aan de Adobe verstrekt, wordt toegewezen aan de Adobe, inclusief alle rechten, titel en interesse in en voor dergelijke feedback.

Verzend Open Feedback of maak een Support Ticket om uw suggesties te delen of een bug te melden en een functieverbetering te zoeken.
