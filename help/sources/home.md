---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van Adobe Experience Platform Source Connectors
topic: overview
translation-type: tm+mt
source-git-commit: eadf285ef5fd373eec54e6680b5f253b0b16dcf9
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---


# Overzicht van bronconnectors

Met het Adobe Experience Platform kunnen gegevens uit externe bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Het Platform van de ervaring verstrekt RESTful API en een interactieve UI die u bronverbindingen aan diverse gegevensleveranciers met gemak laat plaatsen. Deze bronverbindingen laten u toe om uw derdesystemen voor authentiek te verklaren, tijden voor ingestitielooppas te plaatsen, en gegevensinvoer te beheren.

Met het Platform van de Ervaring, kunt u gegevens centraliseren u uit verschillende bronnen verzamelt en de inzichten gebruikt die uit het worden verkregen om meer te doen.

## Typen bronnen

De bronnen in het Platform van de Ervaring worden gegroepeerd in de volgende categorieën:

### Adobe-toepassingen

Met het Experience Platform kunnen gegevens uit andere Adobe-toepassingen worden ingevoerd, zoals Adobe Analytics, Adobe Audience Manager en Experience Platform Launch. Zie de volgende verwante documenten voor meer informatie:

- [Overzicht van de Adobe Audience Manager-connector](connectors/adobe-applications/audience-manager.md)
- [Een Adobe Audience Manager-bronaansluiting maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Overzicht gegevensconnector Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Een Adobe Analytics-bronconnector maken in de gebruikersinterface](./tutorials/ui/create/adobe-applications/analytics.md)
- [Een bronconnector voor klantkenmerken in de gebruikersinterface maken](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Reclame

Het Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een derde advertentiesysteem. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Google Ads-connector](connectors/advertising/ads.md)

### Cloud Storage

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen naar Platform zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema gebruikend het gebruikersinterface. Zie de volgende verwante documenten voor meer informatie:

- [Azure Data Lake Storage Gen2-connector](connectors/cloud-storage/adls-gen2.md)
- [Azure Blob- en Amazon S3-connector](connectors/cloud-storage/blob-s3.md)
- [FTP- en SFTP-aansluiting](connectors/cloud-storage/ftp-sftp.md)
- [Google Cloud Storage-connector](connectors/cloud-storage/google-cloud-storage.md)

### Customer Relationship Management (CRM)

De systemen van CRM verstrekken gegevens die klantenverhoudingen kunnen helpen bouwen, die beurtelings, loyaliteit creëren en klantenbehoud drijven. Het Platform van de ervaring verleent steun voor het opnemen van de gegevens van CRM van de Dynamica 365 van Microsoft en Salesforce. Zie de volgende verwante documenten voor meer informatie:

- [Microsoft Dynamics-connector](connectors/crm/ms-dynamics.md)
- [Salesforce-aansluiting](connectors/crm/salesforce.md)

### Klant geslaagd

Het Platform van de ervaring verleent steun voor het opnemen van gegevens van een derde toepassing van het klantensucces. Zie de volgende verwante documenten voor meer informatie:

- [Salesforce Service Cloud-aansluiting](connectors/customer-success/salesforce-service-cloud.md)
- [ServiceNow-connector](connectors/customer-success/servicenow.md)

### Database

Het Platform van de ervaring verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Amazon Redshift-connector](connectors/databases/redshift.md)
- [Apache Hive op Azure HDInsights-connector](connectors/databases/hive.md)
- [Apache Spark op Azure HDInsights-connector](connectors/databases/spark.md)
- [Azure Data Explorer-connector](connectors/databases/data-explorer.md)
- [Azure Synapse Analytics-connector](connectors/databases/synapse-analytics.md)
- [Azure Table Storage-connector](connectors/databases/ats.md)
- [Google BigQuery-connector](connectors/databases/bigquery.md)
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

Het Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een betalingssysteem van derden. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [PayPal-connector](connectors/payments/paypal.md)

### Protocollen

Het Platform van de ervaring verleent steun voor het opnemen van gegevens van een systeem van derdeprotocollen. Zie de volgende verwante documenten voor meer informatie over specifieke bronschakelaars:

- [Generic OData-connector](connectors/protocols/odata.md)

## Toegangsbeheer voor bronnen bij gegevensinvoer

Rechten voor bronnen bij gegevensinvoer kunnen worden beheerd in de Adobe Admin Console. U hebt toegang tot machtigingen via het tabblad *Machtigingen* in een bepaald productprofiel. Via het deelvenster **Machtigingen** bewerken hebt u toegang tot de machtigingen voor bronnen via de menuvermelding voor *gegevensinvoer* . De toestemming van de Bronnen **van de** Mening verleent read-only toegang tot beschikbare bronnen in het lusje van de *Catalogus* en voor authentiek verklaarde bronnen op het *Browse* lusje, terwijl de machtiging **Manage Bronnen** volledige toegang verleent om te lezen, tot stand te brengen, uit te geven, en bronnen onbruikbaar te maken.

De volgende lijst schetst hoe UI zich gedraagt gebaseerd op verschillende combinaties van deze toestemmingen:

| Machtigingsniveau | Beschrijving |
| ---- | ----|
| **Bronnen** weergeven op | Alleen-lezen toegang verlenen tot bronnen in elk brontype op het tabblad *Catalogus* en op de tabbladen *Bladeren*, *Accounts* en *DataFlow* . |
| **Bronnen** beheren op | Naast de functies die zijn opgenomen in **Bronnen** weergeven, verleent u toegang tot de optie *Bron* verbinden in de *catalogus* en *Gegevens* selecteren in *Bladeren*. **Beheer Bronnen** staat u ook toe om *DataFlows* toe te laten of onbruikbaar te maken en hun programma&#39;s uit te geven. |
| **Bronnen** weergeven en bronnen **** beheren uitgeschakeld | Alle toegang tot bronnen intrekken. |

Voor meer informatie over de beschikbare toestemmingen die door de Console Admin, met inbegrip van die vier bronnen worden verleend, zie het overzicht [van de](../access-control/home.md)toegangscontrole.
