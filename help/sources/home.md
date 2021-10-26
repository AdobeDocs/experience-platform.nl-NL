---
keywords: Experience Platform;thuis;populaire onderwerpen;bronschakelaars;bronschakelaar;bronnen;gegevensbronnen;gegevensbron;gegevensbronverbinding
solution: Experience Platform
title: Overzicht van bronconnectors
topic-legacy: overview
description: Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 030789af0a049b54d6e271410836c08456a83441
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 0%

---

# Overzicht van bronconnectors

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens uit diverse bronnen invoeren, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

[!DNL Flow Service] wordt gebruikt om klantgegevens van diverse verschillende bronnen binnen Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waarmee u eenvoudig bronverbindingen met verschillende gegevensproviders kunt instellen. Deze bronverbindingen laten u toe om uw derdesystemen voor authentiek te verklaren, tijden voor ingestitielooppas te plaatsen, en gegevensinvoer te beheren.

Met Experience Platform, kunt u gegevens centraliseren u uit verschillende bronnen verzamelt en de inzichten gebruiken die uit het worden verkregen om meer te doen.

## Typen bronnen

Bronnen in Experience Platform worden ingedeeld in de volgende categorieën:

### Adobe-toepassingen

Met Experience Platform kunnen gegevens van andere Adobe-toepassingen, zoals Adobe Analytics en Adobe Audience Manager, worden ingesloten. Zie de volgende verwante documenten voor meer informatie:

- [Overzicht Adobe Audience Manager-connector](connectors/adobe-applications/audience-manager.md)
- [Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Overzicht van Adobe Analytics Classifications Data Source Connection](connectors/adobe-applications/classifications.md)
- [Een gegevensbronverbinding voor Adobe Analytics Classifications maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/classifications.md)
- [Overzicht van Adobe Analytics Report Suite-gegevensbronverbinding](connectors/adobe-applications/analytics.md)
- [Een Adobe Analytics-bronverbinding maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/analytics.md)
- [Een bronverbinding voor klantkenmerken maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] connectoroverzicht](connectors/adobe-applications/marketo/marketo.md)
- [Een [!DNL Marketo Engage] bronverbinding in de gebruikersinterface](./tutorials/ui/create/adobe-applications/marketo.md)

### Reclame

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een derde-advertentiesysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) connector

### Cloud Storage

Met bronnen voor cloudopslag kunt u uw eigen gegevens in het Platform plaatsen zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema gebruikend het gebruikersinterface. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Azure Data Lake Storage Gen2] connector](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] connector](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] connector](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] connector](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] connector](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] connector](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] connector](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP] connector](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] connector](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] connector](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] connector](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] connector](connectors/cloud-storage/sftp.md)

### Customer Relationship Management (CRM)

De systemen van CRM verstrekken gegevens die klantenverhoudingen kunnen helpen bouwen, die beurtelings, loyaliteit creëren en klantenbehoud drijven. Experience Platform biedt ondersteuning voor het opnemen van CRM-gegevens van [!DNL Microsoft Dynamics 365] en [!DNL Salesforce]. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Microsoft Dynamics] connector](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] connector](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Klant geslaagd

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor klantsucces van derden. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Salesforce Service Cloud] connector](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] connector](connectors/customer-success/servicenow.md)

### Database

Experience Platform verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Amazon Redshift] connector](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] connector](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] connector](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] connector](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] connector](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] connector](connectors/databases/ats.md)
- [[!DNL Couchbase] connector](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] connector](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] connector](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] connector](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] connector](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB] connector](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server] connector](connectors/databases/sql-server.md)
- [[!DNL MySQL] connector](connectors/databases/mysql.md)
- [[!DNL Oracle] connector](connectors/databases/oracle.md)
- [[!DNL Phoenix] connector](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] connector](connectors/databases/postgres.md)
- [[!DNL Snowflake] connector](connectors/databases/snowflake.md)

### eCommerce

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een eCommerce-systeem van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Lokaal systeem

Experience Platform biedt ondersteuning voor het opnemen van gegevens van uw lokale systeem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Lokale bestanden uploaden](connectors/local-system/local-file-upload.md)

### Marketing Automation

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een derde marketingautomatiseringssysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL HubSpot] connector](connectors/marketing-automation/hubspot.md)
- [[!DNL MailChimp Campaign]](./tutorials/api/create/marketing-automation/mailchimp-campaign.md)
- [[!DNL MailChimp Members]](./tutorials/api/create/marketing-automation/mailchimp-members.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Betalingen

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een betalingssysteem van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL PayPal] connector](connectors/payments/paypal.md)

### Streaming

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit streamingbronnen. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protocollen

Experience Platform verleent steun voor het opnemen van gegevens van een systeem van derdeprotocollen. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Genereic REST API]](connectors/protocols/generic-rest.md)

## Toegangsbeheer voor bronnen bij gegevensinvoer

Machtigingen voor bronnen in gegevensinvoer kunnen binnen de Adobe Admin Console worden beheerd. U hebt toegang tot machtigingen via de **[!UICONTROL Permissions]** in een bepaald productprofiel. Van de **[!UICONTROL Edit Permissions]** kunt u toegang krijgen tot de machtigingen voor bronnen via het dialoogvenster **[!UICONTROL data ingestion]** menu-item. De **[!UICONTROL View Sources]** toestemming verleent read-only toegang tot beschikbare bronnen in **[!UICONTROL Catalog]** tabblad en geverifieerde bronnen in het dialoogvenster **[!UICONTROL Browse]** terwijl de **[!UICONTROL Manage Sources]** met deze machtiging hebt u volledige toegang tot het lezen, maken, bewerken en uitschakelen van bronnen.

De volgende lijst schetst hoe UI zich gedraagt gebaseerd op verschillende combinaties van deze toestemmingen:

| Machtigingsniveau | Beschrijving |
| ---- | ----|
| **[!UICONTROL View Sources]** Aan | De read-only toegang van de subsidie tot bronnen in elk bron-type op het lusje van de Catalogus, evenals doorbladeren, Rekeningen, en lusjes Dataflow. |
| **[!UICONTROL Manage Sources]** Aan | Naast de in **[!UICONTROL View Sources]** verleent toegang tot **[!UICONTROL Connect Source]** optie in **[!UICONTROL Catalog]** en **[!UICONTROL Select Data]** optie in **[!UICONTROL Browse]**. **[!UICONTROL Manage Sources]** staat u ook toe om in of onbruikbaar te maken **[!UICONTROL DataFlows]** en bewerk hun schema&#39;s. |
| **[!UICONTROL View Sources]** Uit en **[!UICONTROL Manage Sources]** Uit | Alle toegang tot bronnen intrekken. |

Voor meer informatie over de beschikbare toestemmingen die door de Admin Console, met inbegrip van die vier bronnen worden verleend, zie [toegangsbeheeroverzicht](../access-control/home.md).

## Voorwaarden en bepalingen {#terms-and-conditions}

Door een van de bronnen met het label bèta (&quot;Beta&quot;) te gebruiken, bevestigt u hierbij dat de bèta wordt geleverd ***&quot;zoals is&quot; zonder enige garantie***.

Adobe is niet verplicht het bètaprogramma te onderhouden, te corrigeren, bij te werken, te wijzigen, te wijzigen of anderszins te ondersteunen. U wordt aangeraden voorzichtig te zijn en op geen enkele wijze te vertrouwen op de juiste werking of prestaties van dergelijke bèta en/of begeleidende materialen. De bètaversie wordt beschouwd als vertrouwelijke informatie van Adobe.

Elke &quot;feedback&quot; (informatie over de bètaversie, inclusief maar niet beperkt tot problemen of defecten die u tegenkomt bij het gebruik van de bètaversie, suggesties, verbeteringen en aanbevelingen) die u aan Adobe hebt gegeven, wordt toegewezen aan Adobe, inclusief alle rechten, titel en interesse in en voor dergelijke feedback.

Verzend Open Feedback of maak een Support Ticket om uw suggesties te delen of een bug te melden en een functieverbetering te zoeken.
