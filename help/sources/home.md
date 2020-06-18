---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van Adobe Experience Platform Source Connectors
topic: overview
translation-type: tm+mt
source-git-commit: a9ce046d6ee8622e23f31edbbf777b045109c13b
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---


# Overzicht van bronconnectors

Adobe Experience Platform staat gegevens toe om van externe bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen met verschillende gegevensproviders kunt instellen. Deze bronverbindingen laten u toe om uw derdesystemen voor authentiek te verklaren, tijden voor ingestitielooppas te plaatsen, en gegevensinvoer te beheren.

Met Experience Platform, kunt u gegevens centraliseren u uit verschillende bronnen verzamelt en de inzichten gebruiken die uit het worden verkregen om meer te doen.

## Typen bronnen

Bronnen in Experience Platform worden gegroepeerd in de volgende categorieën:

### Adobe-toepassingen

Met Experience Platform kunnen gegevens uit andere Adobe-toepassingen worden ingevoerd, zoals Adobe Analytics, Adobe Audience Manager en Experience Platform Launch. Zie de volgende verwante documenten voor meer informatie:

- [Overzicht van de Adobe Audience Manager-aansluiting](connectors/adobe-applications/audience-manager.md)
- [Creeer een Adobe Audience Manager bronschakelaar in UI](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Overzicht van de Adobe Analytics-gegevensconnector](connectors/adobe-applications/analytics.md)
- [Een Adobe Analytics-bronaansluiting maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/analytics.md)
- [Een bronconnector voor klantkenmerken in de gebruikersinterface maken](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Reclame

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een derde-advertentiesysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Google AdWords-connector](connectors/advertising/ads.md)

### Cloud Storage

Met bronnen voor cloudopslag kunt u uw eigen gegevens in het Platform plaatsen zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema gebruikend het gebruikersinterface. Zie de volgende verwante documenten voor meer informatie:

- [Azure Data Lake Storage Gen2-connector](connectors/cloud-storage/adls-gen2.md)
- [Azure Blob- en Amazon S3-connector](connectors/cloud-storage/blob-s3.md)
- [Amazon Kinesis-connector](connectors/cloud-storage/kinesis.md)
- [Apache HDFS-aansluiting](connectors/cloud-storage/hdfs.md)
- [Azure Event Hubs-connector](connectors/cloud-storage/eventhub.md)
- [Azure File Storage-aansluiting](connectors/cloud-storage/azure-file-storage.md)
- [FTP- en SFTP-aansluiting](connectors/cloud-storage/ftp-sftp.md)
- [Google Cloud Storage-connector](connectors/cloud-storage/google-cloud-storage.md)

### Customer Relationship Management (CRM)

De systemen van CRM verstrekken gegevens die klantenverhoudingen kunnen helpen bouwen, die beurtelings, loyaliteit creëren en klantenbehoud drijven. Experience Platform verleent steun voor het opnemen van de gegevens van CRM van de Dynamica 365 van Microsoft en Salesforce. Zie de volgende verwante documenten voor meer informatie:

- [Microsoft Dynamics-connector](connectors/crm/ms-dynamics.md)
- [Salesforce-aansluiting](connectors/crm/salesforce.md)

### Klant geslaagd

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor klantsucces van derden. Zie de volgende verwante documenten voor meer informatie:

- [Salesforce Service Cloud-aansluiting](connectors/customer-success/salesforce-service-cloud.md)
- [ServiceNow-connector](connectors/customer-success/servicenow.md)

### Database

Experience Platform verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Amazon Redshift-connector](connectors/databases/redshift.md)
- [Apache Hive op Azure HDInsights-connector](connectors/databases/hive.md)
- [Apache Spark op Azure HDInsights-connector](connectors/databases/spark.md)
- [Azure Data Explorer-connector](connectors/databases/data-explorer.md)
- [Azure Synapse Analytics-connector](connectors/databases/synapse-analytics.md)
- [Azure Table Storage-connector](connectors/databases/ats.md)
- [Koppelaansluiting](connectors/databases/couchbase.md)
- [Google BigQuery-connector](connectors/databases/bigquery.md)
- [GreenPlum-connector](connectors/databases/greenplum.md)
- [HP Vertica-connector](connectors/databases/hp-vertica.md)
- [IBM DB2-connector](connectors/databases/ibm-db2.md)
- [MariaDB-connector](connectors/databases/mariadb.md)
- [Microsoft SQL Server-aansluiting](connectors/databases/sql-server.md)
- [MySQL-connector](connectors/databases/mysql.md)
- [Oracle-connector](connectors/databases/oracle.md)
- [Phoenix-aansluiting](connectors/databases/phoenix.md)
- [PostgreSQL-connector](connectors/databases/postgres.md)

### Marketing Automation

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een derde marketingautomatiseringssysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [HubSpot-connector](connectors/marketing-automation/hubspot.md)

### Betalingen

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een betalingssysteem van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [PayPal-connector](connectors/payments/paypal.md)

### Protocollen

Experience Platform verleent steun voor het opnemen van gegevens van een systeem van derdeprotocollen. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Generic OData-connector](connectors/protocols/odata.md)

## Toegangsbeheer voor bronnen bij gegevensinvoer

Machtigingen voor bronnen in gegevensinvoer kunnen worden beheerd in de Adobe-Admin Console. U hebt toegang tot machtigingen via het tabblad *Machtigingen* in een bepaald productprofiel. Via het deelvenster **Machtigingen** bewerken hebt u toegang tot de machtigingen voor bronnen via de menuvermelding voor *gegevensinvoer* . De toestemming van de Bronnen **van de** Mening verleent read-only toegang tot beschikbare bronnen in het lusje van de *Catalogus* en voor authentiek verklaarde bronnen op het *Browse* lusje, terwijl de machtiging **Manage Bronnen** volledige toegang verleent om te lezen, tot stand te brengen, uit te geven, en bronnen onbruikbaar te maken.

De volgende lijst schetst hoe UI zich gedraagt gebaseerd op verschillende combinaties van deze toestemmingen:

| Machtigingsniveau | Beschrijving |
| ---- | ----|
| **Bronnen** weergeven op | Alleen-lezen toegang verlenen tot bronnen in elk brontype op het tabblad *Catalogus* en op de tabbladen *Bladeren*, *Accounts* en *DataFlow* . |
| **Bronnen** beheren op | Naast de functies die zijn opgenomen in **Bronnen** weergeven, verleent u toegang tot de optie *Bron* verbinden in de *catalogus* en *Gegevens* selecteren in *Bladeren*. **Beheer Bronnen** staat u ook toe om *DataFlows* toe te laten of onbruikbaar te maken en hun programma&#39;s uit te geven. |
| **Bronnen** weergeven en bronnen **** beheren uitgeschakeld | Alle toegang tot bronnen intrekken. |

Voor meer informatie over de beschikbare toestemmingen die door de Admin Console, met inbegrip van die vier bronnen worden verleend, zie het overzicht [van de](../access-control/home.md)toegangscontrole.

## Voorwaarden en bepalingen {#terms-and-conditions}

Door een van de bronnen te gebruiken die als bèta (&quot;Beta&quot;) worden gelabeld, erkent u hierbij dat de bètaversie ***&quot;as is&quot; wordt geleverd zonder enige*** garantie.

Adobe is niet verplicht het bètaprogramma te onderhouden, te corrigeren, bij te werken, te wijzigen, te wijzigen of anderszins te ondersteunen. U wordt aangeraden voorzichtig te zijn en op geen enkele wijze te vertrouwen op de juiste werking of prestaties van dergelijke bèta en/of begeleidende materialen. De bètaversie wordt beschouwd als vertrouwelijke informatie van Adobe.

Alle &quot;Feedback&quot; (informatie over de bètaversie, inclusief maar niet beperkt tot problemen of fouten die u tegenkomt bij het gebruik van de bètaversie, suggesties, verbeteringen en aanbevelingen) die u aan Adobe hebt gegeven, worden hierbij aan Adobe toegewezen, inclusief alle rechten, titels en interesse in en voor dergelijke feedback.

Verzend Open Feedback of maak een Support Ticket om uw suggesties te delen of een bug te melden en een functieverbetering te zoeken.
