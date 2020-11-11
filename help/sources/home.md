---
keywords: Experience Platform;home;popular topics;source connectors;source connector;sources;data sources;data source;data source connection
solution: Experience Platform
title: Overzicht van Adobe Experience Platform Source Connectors
topic: overview
description: Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.
translation-type: tm+mt
source-git-commit: d26eaf699a67a1bc7111f5f97da277368fcc4629
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# Overzicht van bronconnectors

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van [!DNL Platform] services. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen met verschillende gegevensproviders kunt instellen. Deze bronverbindingen laten u toe om uw derdesystemen voor authentiek te verklaren, tijden voor ingestitielooppas te plaatsen, en gegevensinvoer te beheren.

Met [!DNL Experience Platform], kunt u gegevens centraliseren u uit verschillende bronnen verzamelt en de inzichten gebruiken die uit het worden verkregen om meer te doen.

## Typen bronnen

De bronnen in [!DNL Experience Platform] worden gegroepeerd in de volgende categorieën:

### Adobe-toepassingen

[!DNL Experience Platform] staat toe dat gegevens van andere toepassingen van Adobe, met inbegrip van Adobe Analytics, Adobe Audience Manager, en [!DNL Experience Platform Launch]worden opgenomen. Zie de volgende verwante documenten voor meer informatie:

- [Overzicht Adobe Audience Manager-connector](connectors/adobe-applications/audience-manager.md)
- [Een Adobe Audience Manager-bronaansluiting maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Overzicht Adobe Analytics Classifications Data Connector](connectors/adobe-applications/classifications.md)
- [Een gegevensbronaansluiting voor Adobe Analytics Classifications maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/classifications.md)
- [Overzicht Adobe Analytics-gegevensconnector](connectors/adobe-applications/analytics.md)
- [Een Adobe Analytics-bronaansluiting maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/analytics.md)
- [Een bronconnector voor klantkenmerken in de gebruikersinterface maken](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Reclame

[!DNL Experience Platform] biedt ondersteuning voor het opnemen van gegevens uit een derde-advertentiesysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) connector

### Cloud Storage

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen [!DNL Platform] zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema gebruikend het gebruikersinterface. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Azure Data Lake Storage Gen2] connector](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] connector](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] connector](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] connector](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] connector](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] connector](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] connector](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP and SFTP] connector](connectors/cloud-storage/ftp-sftp.md)
- [[!DNL Google Cloud Storage] connector](connectors/cloud-storage/google-cloud-storage.md)

### Customer Relationship Management (CRM)

De systemen van CRM verstrekken gegevens die klantenverhoudingen kunnen helpen bouwen, die beurtelings, loyaliteit creëren en klantenbehoud drijven. [!DNL Experience Platform] verleent steun voor het opnemen van de gegevens van CRM van [!DNL Microsoft Dynamics 365] en [!DNL Salesforce]. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Microsoft Dynamics] connector](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] connector](connectors/crm/salesforce.md)

### Klant geslaagd

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een toepassing van het de succes van de derdeklant. Zie de volgende verwante documenten voor meer informatie:

- [[!DNL Salesforce Service Cloud] connector](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] connector](connectors/customer-success/servicenow.md)

### Database

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

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
- [[!DNL Microsoft SQL Server] connector](connectors/databases/sql-server.md)
- [[!DNL MySQL] connector](connectors/databases/mysql.md)
- [[!DNL Oracle] connector](connectors/databases/oracle.md)
- [[!DNL Phoenix] connector](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] connector](connectors/databases/postgres.md)

### eCommerce

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een derdeeCommerce systeem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Marketing Automation

[!DNL Experience Platform] biedt ondersteuning voor het opnemen van gegevens van een derde marketingautomatiseringssysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL HubSpot] connector](connectors/marketing-automation/hubspot.md)

### Betalingen

[!DNL Experience Platform] biedt ondersteuning voor het opnemen van gegevens uit een betalingssysteem van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL PayPal] connector](connectors/payments/paypal.md)

### Protocollen

[!DNL Experience Platform] verleent steun voor het opnemen van gegevens van een systeem van derdeprotocollen. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [[!DNL Generic OData] connector](connectors/protocols/odata.md)

## Toegangsbeheer voor bronnen bij gegevensinvoer

Machtigingen voor bronnen in gegevensinvoer kunnen binnen de Adobe Admin Console worden beheerd. U hebt toegang tot machtigingen via het tabblad **[!UICONTROL Machtigingen]** in een bepaald productprofiel. Via het deelvenster **[!UICONTROL Machtigingen]** bewerken hebt u toegang tot de machtigingen voor bronnen via de menuvermelding voor **[!UICONTROL gegevensinvoer]** . De toestemming van de Bronnen **[!UICONTROL van de]** Mening verleent read-only toegang tot beschikbare bronnen in het lusje van de **[!UICONTROL Catalogus]** en voor authentiek verklaarde bronnen op het **[!UICONTROL Browse]** lusje, terwijl de machtiging **[!UICONTROL Manage Bronnen]** volledige toegang verleent om te lezen, tot stand te brengen, uit te geven, en bronnen onbruikbaar te maken.

De volgende lijst schetst hoe UI zich gedraagt gebaseerd op verschillende combinaties van deze toestemmingen:

| Machtigingsniveau | Beschrijving |
| ---- | ----|
| **[!UICONTROL Bronnen]** weergeven op | De read-only toegang van de subsidie tot bronnen in elk bron-type op het lusje van de Catalogus, evenals doorbladeren, Rekeningen, en lusjes Dataflow. |
| **[!UICONTROL Bronnen]** beheren op | Naast de functies die zijn opgenomen in **[!UICONTROL Bronnen]** weergeven, verleent u toegang tot de optie **[!UICONTROL Bron]** verbinden in de **[!UICONTROL catalogus]** en **[!UICONTROL Gegevens]** selecteren in **[!UICONTROL Bladeren]**. **[!UICONTROL Beheer Bronnen]** staat u ook toe om **[!UICONTROL DataFlows]** toe te laten of onbruikbaar te maken en hun programma&#39;s uit te geven. |
| **[!UICONTROL Bronnen]** weergeven en bronnen **** beheren uitgeschakeld | Alle toegang tot bronnen intrekken. |

Voor meer informatie over de beschikbare toestemmingen die door de Admin Console, met inbegrip van die vier bronnen worden verleend, zie het overzicht [van de](../access-control/home.md)toegangscontrole.

## Voorwaarden en bepalingen {#terms-and-conditions}

Door een van de bronnen te gebruiken die als bèta (&quot;Beta&quot;) worden gelabeld, erkent u hierbij dat de bètaversie ***&quot;as is&quot; wordt geleverd zonder enige*** garantie.

Adobe is niet verplicht het bètaprogramma te onderhouden, te corrigeren, bij te werken, te wijzigen, te wijzigen of anderszins te ondersteunen. U wordt aangeraden voorzichtig te zijn en op geen enkele wijze te vertrouwen op de juiste werking of prestaties van dergelijke bèta en/of begeleidende materialen. De bètaversie wordt beschouwd als vertrouwelijke informatie van Adobe.

Elke &quot;feedback&quot; (informatie over de bètaversie, inclusief maar niet beperkt tot problemen of defecten die u tegenkomt bij het gebruik van de bètaversie, suggesties, verbeteringen en aanbevelingen) die u aan Adobe hebt gegeven, wordt toegewezen aan Adobe, inclusief alle rechten, titel en interesse in en voor dergelijke feedback.

Verzend Open Feedback of maak een Support Ticket om uw suggesties te delen of een bug te melden en een functieverbetering te zoeken.
