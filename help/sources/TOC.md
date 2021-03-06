---
audience: user
user-guide-title: Help bij Adobe Experience Platform Source Connectors
breadcrumb-title: Handleiding voor bronaansluitingen
user-guide-description: Verzamel gegevens uit diverse bronnen of structuren, label en verbeter reeds opgenomen gegevens.
feature: Sources
source-git-commit: 6f7611b120046fffc1b7c15bd657d699f4b4a588
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 5%

---


# Bronnen {#sources}

- [Overzicht van bronnen](home.md)
- Beschikbare bronconnectors {#connectors}
   - Adobe-toepassingen {#adobe-applications}
      - [Bron voor analytische classificaties](connectors/adobe-applications/classifications.md)
      - [Analysebron](connectors/adobe-applications/analytics.md)
      - [Bron Audience Manager](connectors/adobe-applications/audience-manager.md)
      - [Kenmerkbron van klant](connectors/adobe-applications/customer-attributes.md)
      - [Bron gegevensverzameling](connectors/adobe-applications/data-collection.md)
      - Veldtoewijzingen {#mapping}
         - [Toewijzingen van analytische velden](connectors/adobe-applications/mapping/analytics.md)
         - [Veldtoewijzingen Audience Manager](connectors/adobe-applications/mapping/audience-manager.md)
         - [Toewijzingen doelveld](connectors/adobe-applications/mapping/target.md)
         - [Marketo Engage-veldtoewijzingen](connectors/adobe-applications/mapping/marketo.md)
         - [Microsoft Dynamics-veldtoewijzingen](connectors/adobe-applications/mapping/dynamics.md)
         - [Toewijzingen in Salesforce-veld](connectors/adobe-applications/mapping/salesforce.md)
      - Marketo {#marketo}
         - [Marketo Engage-aansluiting](connectors/adobe-applications/marketo/marketo.md)
         - [Marketo Engage-verificatiegids](connectors/adobe-applications/marketo/marketo-auth.md)
         - [B2B-naamruimten en -schema&#39;s](connectors/adobe-applications/marketo/marketo-namespaces.md)
   - Reclame {#advertising}
      - [Google AdWords-connector](connectors/advertising/ads.md)
   - Analytics {#analytics}
      - [Mixpanel-aansluiting](connectors/analytics/mixpanel.md)
   - Cloud-opslag {#cloud-storage}
      - [Amazon Kinesis-connector](connectors/cloud-storage/kinesis.md)
      - [Amazon S3-connector](connectors/cloud-storage/s3.md)
      - [Apache HDFS-aansluiting](connectors/cloud-storage/hdfs.md)
      - [Azure Data Lake Storage Gen2-connector](connectors/cloud-storage/adls-gen2.md)
      - [Azure Blob-connector](connectors/cloud-storage/blob.md)
      - [Azure Event Hubs-connector](connectors/cloud-storage/eventhub.md)
      - [Azure File Storage-aansluiting](connectors/cloud-storage/azure-file-storage.md)
      - [Gegevenslandingszone](connectors/cloud-storage/data-landing-zone.md)
      - [FTP-aansluiting](connectors/cloud-storage/ftp.md)
      - [Google Cloud Storage-connector](connectors/cloud-storage/google-cloud-storage.md)
      - [Google PubSub](connectors/cloud-storage/google-pubsub.md)
      - [Oracle Object Storage](connectors/cloud-storage/oracle-object-storage.md)
      - [SFTP-aansluiting](connectors/cloud-storage/sftp.md)
      - [Amazon S3- en Azure Blob-connector](connectors/cloud-storage/blob-s3.md)
   - Toestemming en voorkeuren {#consent}
      - [OneTrust-integratie](connectors/consent-and-preferences/onetrust.md)
   - CRM {#crm}
      - [Microsoft Dynamics-connector](connectors/crm/ms-dynamics.md)
      - [Salesforce-aansluiting](connectors/crm/salesforce.md)
      - [Veeva CRM-connector](connectors/crm/veeva.md)
      - [Zoho CRM-aansluiting](connectors/crm/zoho.md)
   - Klantsucces {#customer-success}
      - [Salesforce Service Cloud-aansluiting](connectors/customer-success/salesforce-service-cloud.md)
      - [ServiceNow-connector](connectors/customer-success/servicenow.md)
      - [Zendesk-connector](connectors/customer-success/zendesk.md)
   - Databases {#databases}
      - [Amazon Redshift-connector](connectors/databases/redshift.md)
      - [Apache Hive op Azure HDInsights-connector](connectors/databases/hive.md)
      - [Apache Spark op Azure HDInsights-connector](connectors/databases/spark.md)
      - [Azure Data Explorer-connector](connectors/databases/data-explorer.md)
      - [azure synapse Analytics-connector](connectors/databases/synapse-analytics.md)
      - [Azure Table Storage-connector](connectors/databases/ats.md)
      - [Koppelaansluiting](connectors/databases/couchbase.md)
      - [Google BigQuery-connector](connectors/databases/bigquery.md)
      - [GreenPlum-connector](connectors/databases/greenplum.md)
      - [HP Vertica-connector](connectors/databases/hp-vertica.md)
      - [IBM DB2-connector](connectors/databases/ibm-db2.md)
      - [MariaDB-connector](connectors/databases/mariadb.md)
      - [Microsoft SQL Server-connector](connectors/databases/sql-server.md)
      - [MySQL-connector](connectors/databases/mysql.md)
      - [Oracle-aansluiting](connectors/databases/oracle.md)
      - [Phoenix-aansluiting](connectors/databases/phoenix.md)
      - [PostgreSQL-connector](connectors/databases/postgres.md)
      - [Snowflake-aansluiting](connectors/databases/snowflake.md)
   - eCommerce {#ecommerce}
      - [Shopify-connector](connectors/ecommerce/shopify.md)
   - Lokaal systeem {#local-system}
      - [Aansluiting voor lokale bestandsupload](connectors/local-system/local-file-upload.md)
   - Marketing automatiseren {#marketing-automation}
      - [HubSpot-connector](connectors/marketing-automation/hubspot.md)
      - [Mailchimp-connector](connectors/marketing-automation/mailchimp.md)
      - [Oracle Eloqua-aansluiting](connectors/marketing-automation/oracle-eloqua.md)
      - [Salesforce-Marketing Cloud](connectors/marketing-automation/salesforce-marketing-cloud.md)
   - Betalingen {#payments}
      - [PayPal-connector](connectors/payments/paypal.md)
      - [Vierkante connector](connectors/payments/square.md)
   - Protocollen {#protocols}
      - [Generic OData-connector](connectors/protocols/odata.md)
      - [Algemene REST API-aansluiting](connectors/protocols/generic-rest.md)
   - Streaming {#streaming}
      - [HTTP API-connector](connectors/streaming/http.md)
- API-zelfstudies {#api-tutorials}
   - Een basisverbinding maken {#create}
      - Reclame {#advertising}
         - [Google AdWords](tutorials/api/create/advertising/ads.md)
      - Analyse {#analytics}
         - [Mixpanel](tutorials/api/create/analytics/mixpanel.md)
      - Cloud-opslag {#cloud-storage}
         - [Amazon Kinesis](tutorials/api/create/cloud-storage/kinesis.md)
         - [Amazon S3](tutorials/api/create/cloud-storage/s3.md)
         - [Apache HDFS](tutorials/api/create/cloud-storage/hdfs.md)
         - [Azure Blob](tutorials/api/create/cloud-storage/blob.md)
         - [Azure Data Lake Storage Gen2](tutorials/api/create/cloud-storage/adls-gen2.md)
         - [Azure Event Hubs](tutorials/api/create/cloud-storage/eventhub.md)
         - [Azure-bestandsopslag](tutorials/api/create/cloud-storage/azure-file-storage.md)
         - [Gegevenslandingszone](tutorials/api/create/cloud-storage/data-landing-zone.md)
         - [FTP](tutorials/api/create/cloud-storage/ftp.md)
         - [Google Cloud Storage](tutorials/api/create/cloud-storage/google.md)
         - [Google PubSub](tutorials/api/create/cloud-storage/google-pubsub.md)
         - [Oracle Object Storage](tutorials/api/create/cloud-storage/oracle-object-storage.md)
         - [SFTP](tutorials/api/create/cloud-storage/sftp.md)
      - Toestemming en voorkeuren {#consent}
         - [OneTrust-integratie](tutorials/api/create/consent-and-preferences/onetrust.md)
      - CRM {#crm}
         - [Microsoft Dynamics](tutorials/api/create/crm/ms-dynamics.md)
         - [Salesforce](tutorials/api/create/crm/salesforce.md)
         - [Veeva CRM](tutorials/api/create/crm/veeva.md)
         - [Zoho CRM](tutorials/api/create/crm/zoho.md)
      - Klantsucces {#customer-success}
         - [Salesforce Service Cloud](tutorials/api/create/customer-success/salesforce-service-cloud.md)
         - [ServiceNow](tutorials/api/create/customer-success/servicenow.md)
         - [Zendesk](tutorials/api/create/customer-success/zendesk.md)
      - Databases {#databases}
         - [Amazon Redshift](tutorials/api/create/databases/redshift.md)
         - [Apache Hive op Azure HDInsights](tutorials/api/create/databases/hive.md)
         - [Apache Spark op Azure HDInsights](tutorials/api/create/databases/spark.md)
         - [Azure Data Explorer](tutorials/api/create/databases/data-explorer.md)
         - [azure synapse Analytics](tutorials/api/create/databases/synapse-analytics.md)
         - [Azure Table Storage](tutorials/api/create/databases/ats.md)
         - [Couchbase](tutorials/api/create/databases/couchbase.md)
         - [Google BigQuery](tutorials/api/create/databases/bigquery.md)
         - [GreenPlum](tutorials/api/create/databases/greenplum.md)
         - [HP Vertica](tutorials/api/create/databases/hp-vertica.md)
         - [IBM DB2](tutorials/api/create/databases/ibm-db2.md)
         - [MariaDB](tutorials/api/create/databases/mariadb.md)
         - [MySQL](tutorials/api/create/databases/mysql.md)
         - [Oracle](tutorials/api/create/databases/oracle.md)
         - [Phoenix](tutorials/api/create/databases/phoenix.md)
         - [PostgreSQL](tutorials/api/create/databases/postgres.md)
         - [Snowflake](tutorials/api/create/databases/snowflake.md)
         - [SQL Server](tutorials/api/create/databases/sql-server.md)
      - eCommerce {#ecommerce}
         - [Schopify](tutorials/api/create/ecommerce/shopify.md)
      - Marketing automatiseren {#marketing-automation}
         - [HubSpot](tutorials/api/create/marketing-automation/hubspot.md)
         - [MailChimp-campagne](tutorials/api/create/marketing-automation/mailchimp-campaign.md)
         - [MailChimp-leden](tutorials/api/create/marketing-automation/mailchimp-members.md)
         - [Oracle Eloqua](tutorials/api/create/marketing-automation/oracle-eloqua.md)
         - [Salesforce-Marketing Cloud](tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
      - Betalingen {#payments}
         - [PayPal](tutorials/api/create/payments/paypal.md)
         - [Vierkant](tutorials/api/create/payments/square.md)
      - Protocollen {#protocols}
         - [Generic OData](tutorials/api/create/protocols/odata.md)
         - [Algemene REST-API](tutorials/api/create/protocols/generic-rest.md)
      - Streaming {#streaming}
         - [HTTP-API](tutorials/api/create/streaming/http.md)
   - Gegevens verkennen {#explore}
      - [Reclamegegevens verkennen](tutorials/api/explore/advertising.md)
      - [Gegevens over cloudopslag verkennen](tutorials/api/explore/cloud-storage.md)
      - [CRM-gegevens verkennen](tutorials/api/explore/crm.md)
      - [Ontdek de succesgegevens van klanten](tutorials/api/explore/customer-success.md)
      - [Databasegegevens verkennen](tutorials/api/explore/database-nosql.md)
      - [Gegevens over eCommerce verkennen](tutorials/api/explore/ecommerce.md)
      - [Gegevens over marketingautomatisering verkennen](tutorials/api/explore/marketing-automation.md)
      - [Betalingsgegevens verkennen](tutorials/api/explore/payments.md)
      - [protocolgegevens verkennen](tutorials/api/explore/protocols.md)
      - [Gegevenstabellen verkennen](tutorials/api/explore/tabular.md)
   - Gegevens verzamelen {#collect}
      - [Reclamegegevens verzamelen](tutorials/api/collect/advertising.md)
      - [Gegevens over cloudopslag verzamelen](tutorials/api/collect/cloud-storage.md)
      - [CRM-gegevens verzamelen](tutorials/api/collect/crm.md)
      - [Gegevens over succes van klanten verzamelen](tutorials/api/collect/customer-success.md)
      - [Databasegegevens verzamelen](tutorials/api/collect/database-nosql.md)
      - [Gegevens over eCommerce verzamelen](tutorials/api/collect/ecommerce.md)
      - [Gegevens over marketingautomatisering verzamelen](tutorials/api/collect/marketing-automation.md)
      - [Betalingsgegevens verzamelen](tutorials/api/collect/payments.md)
      - [protocolgegevens verzamelen](tutorials/api/collect/protocols.md)
      - [Streaming gegevens verzamelen](tutorials/api/collect/streaming.md)
   - [Dataflows bewaken](tutorials/api/monitor.md)
   - [Accounts bijwerken](tutorials/api/update.md)
   - [Gegevensstromen bijwerken](tutorials/api/update-dataflows.md)
   - [Accounts verwijderen](tutorials/api/delete.md)
   - [Gegevensstromen verwijderen](tutorials/api/delete-dataflows.md)
- UI-zelfstudies {#ui-tutorials}
   - Een bronverbinding maken {#create}
      - Adobe-toepassingen {#adobe-applications}
         - [Adobe Analytics (rapportsuite-gegevens)](tutorials/ui/create/adobe-applications/analytics.md)
         - [Adobe Analytics (classificatiegegevens)](tutorials/ui/create/adobe-applications/classifications.md)
         - [Adobe Audience Manager](tutorials/ui/create/adobe-applications/audience-manager.md)
         - [Adobe Campaign Managed Services](tutorials/ui/create/adobe-applications/campaign.md)
         - [Klantkenmerken](tutorials/ui/create/adobe-applications/customer-attributes.md)
         - [Marketo Engage](tutorials/ui/create/adobe-applications/marketo.md)
      - Reclame {#advertising}
         - [Google AdWords](tutorials/ui/create/advertising/ads.md)
      - Analyse {#analytics}
         - [Mixpanel](tutorials/ui/create/analytics/mixpanel.md)
      - Cloud-opslag {#cloud-storage}
         - [Amazon Kinesis](tutorials/ui/create/cloud-storage/kinesis.md)
         - [Amazon S3](tutorials/ui/create/cloud-storage/s3.md)
         - [Apache HDFS](tutorials/ui/create/cloud-storage/hdfs.md)
         - [Azure Data Lake Storage Gen2](tutorials/ui/create/cloud-storage/adls-gen2.md)
         - [Azure Blob](tutorials/ui/create/cloud-storage/blob.md)
         - [Azure Event Hubs](tutorials/ui/create/cloud-storage/eventhub.md)
         - [Azure-bestandsopslag](tutorials/ui/create/cloud-storage/azure-file-storage.md)
         - [Gegevenslandingszone](tutorials/ui/create/cloud-storage/data-landing-zone.md)
         - [FTP](tutorials/ui/create/cloud-storage/ftp.md)
         - [Google Cloud Storage](tutorials/ui/create/cloud-storage/google-cloud-storage.md)
         - [Google PubSub](tutorials/ui/create/cloud-storage/google-pubsub.md)
         - [Oracle Object Storage](tutorials/ui/create/cloud-storage/oracle-object-storage.md)
         - [SFTP](tutorials/ui/create/cloud-storage/sftp.md)
         - [Amazon S3 en Blob](tutorials/ui/create/cloud-storage/blob-s3.md)
      - Toestemming en voorkeuren {#consent}
         - [OneTrust-integratie](tutorials/ui/create/consent-and-preferences/onetrust.md)
      - CRM {#crm}
         - [Microsoft Dynamics](tutorials/ui/create/crm/dynamics.md)
         - [Salesforce](tutorials/ui/create/crm/salesforce.md)
         - [Veeva CRM](tutorials/ui/create/crm/veeva.md)
         - [Zoho CRM](tutorials/ui/create/crm/zoho.md)
      - Klant geslaagd {#customer-success}
         - [Salesforce Service Cloud](tutorials/ui/create/customer-success/salesforce-service-cloud.md)
         - [ServiceNow](tutorials/ui/create/customer-success/servicenow.md)
         - [Zendesk](tutorials/ui/create/customer-success/zendesk.md)
      - Databases {#databases}
         - [Amazon Redshift](tutorials/ui/create/databases/redshift.md)
         - [Apache Hive op Azure HDInsights](tutorials/ui/create/databases/hive.md)
         - [Apache Spark op Azure HDInsights](tutorials/ui/create/databases/spark.md)
         - [Azure Data Explorer](tutorials/ui/create/databases/data-explorer.md)
         - [azure synapse Analytics](tutorials/ui/create/databases/synapse-analytics.md)
         - [Azure Table Storage](tutorials/ui/create/databases/ats.md)
         - [Couchbase](tutorials/ui/create/databases/couchbase.md)
         - [Google Big Query](tutorials/ui/create/databases/bigquery.md)
         - [GreenPlum](tutorials/ui/create/databases/greenplum.md)
         - [HP Vertica](tutorials/ui/create/databases/hp-vertica.md)
         - [IBM DB2](tutorials/ui/create/databases/ibm-db2.md)
         - [MariaDB](tutorials/ui/create/databases/mariadb.md)
         - [Microsoft SQL Server](tutorials/ui/create/databases/sql-server.md)
         - [MySQL](tutorials/ui/create/databases/mysql.md)
         - [Oracle](tutorials/ui/create/databases/oracle.md)
         - [Phoenix](tutorials/ui/create/databases/phoenix.md)
         - [PostgreSQL](tutorials/ui/create/databases/postgres.md)
         - [Snowflake](tutorials/ui/create/databases/snowflake.md)
      - eCommerce {#ecommerce}
         - [Schopify](tutorials/ui/create/ecommerce/shopify.md)
      - Lokaal systeem {#local-system}
         - [Lokale bestanden uploaden](tutorials/ui/create/local-system/local-file-upload.md)
      - Marketing automatiseren {#marketing-automation}
         - [HubSpot](tutorials/ui/create/marketing-automation/hubspot.md)
         - [Mailchimp-campagnes](tutorials/ui/create/marketing-automation/mailchimp-campaigns.md)
         - [Mailchimp-leden](tutorials/ui/create/marketing-automation/mailchimp-members.md)
         - [Oracle Eloqua](tutorials/ui/create/marketing-automation/oracle-eloqua.md)
         - [Salesforce-Marketing Cloud](tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
      - Betalingen {#payments}
         - [PayPal](tutorials/ui/create/payments/paypal.md)
         - [Vierkant](tutorials/ui/create/payments/square.md)
      - Protocollen {#protocols}
         - [Generic OData](tutorials/ui/create/protocols/odata.md)
      - Streaming {#streaming}
         - [HTTP-API](tutorials/ui/create/streaming/http.md)
   - Een gegevensstroom configureren {#dataflow}
      - [Gegevensstroom advertentieverbinding](tutorials/ui/dataflow/advertising.md)
      - [Gegevensstroom analytische verbinding](tutorials/ui/dataflow/analytics.md)
      - [Batch-gegevens voor cloudopslagverbinding](tutorials/ui/dataflow/batch/cloud-storage.md)
      - [Gegevens over streaming cloudopslagverbinding](tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
      - [Verbindingsgegevens voor goedkeuring en voorkeuren](tutorials/ui/dataflow/consent-and-preferences.md)
      - [Gegevens CRM-verbinding](tutorials/ui/dataflow/crm.md)
      - [Gegevensstroom voor succesverbinding van klant](tutorials/ui/dataflow/customer-success.md)
      - [Gegevensstroom databaseverbinding](tutorials/ui/dataflow/databases.md)
      - [Gegevensstroom ecommerce-verbinding](tutorials/ui/dataflow/ecommerce.md)
      - [Verbinding voor marketingautomatisering](tutorials/ui/dataflow/marketing-automation.md)
      - [Gegevensstroom betalingsverbinding](tutorials/ui/dataflow/payments.md)
      - [Dataflow van protocolverbinding](tutorials/ui/dataflow/protocols.md)
   - [Inkomende gegevens activeren om klantprofielen te vullen](tutorials/ui/profile.md)
   - [Batchgegevens controleren](tutorials/ui/monitor.md)
   - [Streaming gegevens bijhouden](tutorials/ui/monitor-streaming.md)
   - [Accounts bijwerken](tutorials/ui/update.md)
   - [Gegevensstromen bijwerken](tutorials/ui/update-dataflows.md)
   - [Accounts verwijderen](tutorials/ui/delete-accounts.md)
   - [Gegevensstromen verwijderen](tutorials/ui/delete.md)
   - [Abonneren op waarschuwingen voor bronnen](tutorials/ui/alerts.md)
- Bronnen-SDK {#sdk}
   - [Overzicht](sources-sdk/overview.md)
   - [Configuratieopties](sources-sdk/config/config.md)
   - [Verificatiespecificatie configureren](sources-sdk/config/authspec.md)
   - [Bronspecificatie configureren](sources-sdk/config/sourcespec.md)
   - [Uitgebreide specificatie configureren](sources-sdk/config/explorespec.md)
   - [Overzicht SDK API van bronnen](sources-sdk/api/api-overview.md)
   - [Aan de slag](sources-sdk/api/getting-started.md)
   - [Een verbindingsspecificatie maken](sources-sdk/api/create.md)
   - [Een verbindingsspecificatie bijwerken](sources-sdk/api/update-connection-specs.md)
   - [Een stroomspecificatie bijwerken](sources-sdk/api/update-flow-specs.md)
   - [Uw bron verzenden](sources-sdk/api/submit.md)
   - [Uw bron documenteren in Adobe Experience Platform](sources-sdk/documentation/doc-overview.md)
   - [Gebruik de het Webinterface van GitHub om een pagina van de brondocumentatie tot stand te brengen](sources-sdk/documentation/github.md)
   - [Een teksteditor in uw lokale omgeving gebruiken om een documentatiepagina voor bronnen te maken](sources-sdk/documentation/text-editor.md)
   - [Zelfbediening API-sjabloon voor documentatie](sources-sdk/documentation/template.md)
   - [Zelfbediening UI-sjabloon voor documentatie](sources-sdk/documentation/ui-template.md)
- [Meldingen voor stroomuitvoering](notifications.md)
- [IP adres lijst van gewenste personen](ip-address-allow-list.md)
- [Veelgestelde vragen](./troubleshooting.md)
- [API-referentie](https://www.adobe.io/experience-platform-apis/references/flow-service/)
- [Opmerkingen bij de release Platform](https://www.adobe.com/go/platform-release-notes-en)
