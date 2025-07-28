---
title: Vastleggen van wijzigingsgegevens inschakelen voor bronverbindingen in de API
description: Leer hoe u het vastleggen van wijzigingsgegevens inschakelt voor bronverbindingen in de API
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Vastleggen van wijzigingsgegevens inschakelen voor bronverbindingen in de API

Het vastleggen van gegevens in Adobe Experience Platform-bronnen wijzigen is een mogelijkheid waarmee u gegevenssynchronisatie in real time tussen uw bron- en doelsystemen kunt onderhouden.

Momenteel, steunt Experience Platform **stijgende gegevensexemplaar**, dat ervoor zorgt dat de pas gecreëerde of bijgewerkte verslagen in het bronsysteem periodiek aan de ingebedde datasets worden gekopieerd. Dit proces baseert zich op gebruik van de **timestamp kolom**, zoals `LastModified` om veranderingen te volgen en **slechts de onlangs opgenomen of bijgewerkte gegevens** te vangen. Deze methode houdt echter geen rekening met verwijderde records, wat in de loop der tijd tot inconsistenties in de gegevens kan leiden.

Bij het vastleggen van wijzigingsgegevens legt een bepaalde stroom alle wijzigingen vast en past deze toe, inclusief het invoegen, bijwerken en verwijderen. Op dezelfde manier blijven de datasets van Experience Platform volledig gesynchroniseerd met het bronsysteem.

U kunt het vangen van veranderingsgegevens voor de volgende bronnen gebruiken:

## [!DNL Amazon S3]

Zorg ervoor dat `_change_request_type` aanwezig is in het [!DNL Amazon S3] -bestand dat u wilt toevoegen aan Experience Platform. Daarnaast moet u ervoor zorgen dat de volgende geldige waarden in het bestand worden opgenomen:

* `u`: voor invoegen en bijwerken
* `d` : voor verwijderingen.

Als `_change_request_type` niet aanwezig is in uw bestand, wordt de standaardwaarde van `u` gebruikt.

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Amazon S3] bronverbinding:

* [ creeer a [!DNL Amazon S3]  basisverbinding ](../api/create/cloud-storage/s3.md).
* [ creeer een bronverbinding voor een wolkenopslag ](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Blob]

Zorg ervoor dat `_change_request_type` aanwezig is in het [!DNL Azure Blob] -bestand dat u wilt toevoegen aan Experience Platform. Daarnaast moet u ervoor zorgen dat de volgende geldige waarden in het bestand worden opgenomen:

* `u`: voor invoegen en bijwerken
* `d` : voor verwijderingen.

Als `_change_request_type` niet aanwezig is in uw bestand, wordt de standaardwaarde van `u` gebruikt.

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Azure Blob] bronverbinding:

* [ creeer a [!DNL Azure Blob]  basisverbinding ](../api/create/cloud-storage/blob.md).
* [ creeer een bronverbinding voor een wolkenopslag ](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Databricks]

U moet **voer van veranderingsgegevens** in uw [!DNL Azure Databricks] lijst toelaten om veranderingsgegevens te gebruiken vangen in uw bronverbinding.

Gebruik de volgende opdrachten om de optie voor het doorvoeren van gegevens wijzigen expliciet in te schakelen in [!DNL Azure Databricks]

**Nieuwe lijst**

Als u de gewijzigde gegevensinvoer wilt toepassen op een nieuwe tabel, moet u de tabeleigenschap `delta.enableChangeDataFeed` instellen op `TRUE` in de opdracht `CREATE TABLE` .

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Bestaande lijst**

Als u een gewijzigde gegevensfeed wilt toepassen op een bestaande tabel, moet u de tabeleigenschap `delta.enableChangeDataFeed` instellen op `TRUE` in de opdracht `ALTER TABLE` .

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Alle nieuwe lijsten**

Als u de gegevensfeed change wilt toepassen op alle nieuwe tabellen, moet u de standaardeigenschappen instellen op `TRUE` .

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

Voor meer informatie, lees de [[!DNL Azure Databricks]  gids bij het toelaten van de voer van veranderingsgegevens ](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed).

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Azure Databricks] bronverbinding:

* [ creeer a [!DNL Azure Databricks]  basisverbinding ](../api/create/databases/databricks.md).
* [ creeer een bronverbinding voor een gegevensbestand ](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Data Landing Zone]

U moet **voer van veranderingsgegevens** in uw [!DNL Data Landing Zone] lijst toelaten om veranderingsgegevens te gebruiken vangen in uw bronverbinding.

Gebruik de volgende opdrachten om de optie voor het doorvoeren van gegevens wijzigen expliciet in te schakelen in [!DNL Data Landing Zone] .

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Data Landing Zone] bronverbinding:

* [ creeer a [!DNL Data Landing Zone]  basisverbinding ](../api/create/cloud-storage/data-landing-zone.md).
* [ creeer een bronverbinding voor een wolkenopslag ](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Google BigQuery]

Om veranderingsgegevens te gebruiken vangen in uw [!DNL Google BigQuery] bronverbinding. Navigeer naar de pagina [!DNL Google BigQuery] in de [!DNL Google Cloud] console en stel `enable_change_history` in op `TRUE` . Met deze eigenschap wordt de wijzigingshistorie voor uw gegevenstabel ingeschakeld.

Voor meer informatie, lees de gids over [ de taalverklaringen van de gegevensdefinitie in  [!DNL GoogleSQL] ](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Google BigQuery] bronverbinding:

* [ creeer a [!DNL Google BigQuery]  basisverbinding ](../api/create/databases/bigquery.md).
* [ creeer een bronverbinding voor een gegevensbestand ](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Google Cloud Storage]

Zorg ervoor dat `_change_request_type` aanwezig is in het [!DNL Google Cloud Storage] -bestand dat u wilt toevoegen aan Experience Platform. Daarnaast moet u ervoor zorgen dat de volgende geldige waarden in het bestand worden opgenomen:

* `u`: voor invoegen en bijwerken
* `d` : voor verwijderingen.

Als `_change_request_type` niet aanwezig is in uw bestand, wordt de standaardwaarde van `u` gebruikt.

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Google Cloud Storage] bronverbinding:

* [ creeer a [!DNL Google Cloud Storage]  basisverbinding ](../api/create/cloud-storage/google.md).
* [ creeer een bronverbinding voor een wolkenopslag ](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL SFTP]

Zorg ervoor dat `_change_request_type` aanwezig is in het [!DNL SFTP] -bestand dat u wilt toevoegen aan Experience Platform. Daarnaast moet u ervoor zorgen dat de volgende geldige waarden in het bestand worden opgenomen:

* `u`: voor invoegen en bijwerken
* `d` : voor verwijderingen.

Als `_change_request_type` niet aanwezig is in uw bestand, wordt de standaardwaarde van `u` gebruikt.

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL SFTP] bronverbinding:

* [ creeer a [!DNL SFTP]  basisverbinding ](../api/create/cloud-storage/sftp.md).
* [ creeer een bronverbinding voor een wolkenopslag ](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL Snowflake]

U moet **verandering het volgen** in uw [!DNL Snowflake] lijsten toelaten om veranderingsgegevens te gebruiken vangen in uw bronverbindingen.

Schakel in [!DNL Snowflake] de optie Wijzigingen bijhouden in met de waarden `ALTER TABLE` en `CHANGE_TRACKING` op `TRUE` .

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Voor meer informatie, lees de [[!DNL Snowflake]  gids bij het gebruiken van de veranderingsclausule ](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Snowflake] bronverbinding:

* [ creeer a [!DNL Snowflake]  basisverbinding ](../api/create/databases/snowflake.md).
* [ creeer een bronverbinding voor een gegevensbestand ](../api/collect/database-nosql.md#create-a-source-connection).

