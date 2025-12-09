---
title: Vastleggen van wijzigingsgegevens inschakelen voor bronverbindingen in de API
description: Leer hoe u het vastleggen van wijzigingsgegevens inschakelt voor bronverbindingen in de API
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Vastleggen van wijzigingsgegevens inschakelen voor bronverbindingen in de API

Met de functie voor het vastleggen van wijzigingsgegevens in Adobe Experience Platform-bronnen zorgt u ervoor dat uw bron- en doelsystemen vrijwel realtime gesynchroniseerd blijven.

Experience Platform steunt momenteel **stijgende gegevensexemplaar**, dat periodiek nieuw gecreeerde of bijgewerkte verslagen van het bronsysteem aan de ingebedde datasets overbrengt. Deze methode baseert zich op de kolom van a **timestamp** om veranderingen te volgen, maar het ontdekt geen schrappingen, die tot gegevensinconsistenties in tijd kunnen leiden.

Als u daarentegen de gegevensopname wijzigt, worden de gegevens vastgelegd en worden invoegingen, updates en verwijderingen in bijna real-time toegepast. Deze uitvoerige verandering het volgen zorgt ervoor dat de datasets volledig gericht op het bronsysteem blijven en verstrekt een volledige veranderingsgeschiedenis, voorbij welke stijgende exemplaar steunt. Nochtans, schrapt verrichtingen vereisen speciale overweging aangezien zij alle toepassingen beïnvloeden die de doeldatasets gebruiken.

De gegevens van de verandering vangen in Experience Platform vereist **[Data Mirror](../../../xdm/data-mirror/overview.md)** met [ relationele schema&#39;s ](../../../xdm/schema/relational.md). U kunt wijzigingsgegevens op twee manieren naar Data Mirror verzenden:

* **[Handmatige verandering het volgen](#file-based-sources)**: Omvat a `_change_request_type` kolom in uw dataset voor bronnen die niet natically veranderingsgegevens produceren vangen verslagen
* **[de Inheemse vangst van veranderingsgegevens voert](#database-sources)** uit: De verslagen van de vangst van veranderingsgegevens van het gebruik direct uit uw bronsysteem worden uitgevoerd

Beide benaderingen vereisen Data Mirror met relationele schema&#39;s om verhoudingen te bewaren en uniciteit af te dwingen.

## Data Mirror met relationele schema&#39;s

>[!AVAILABILITY]
>
>Data Mirror en relationele schema&#39;s zijn beschikbaar aan Adobe Journey Optimizer **Geordende campagnes** vergunninghouders. Zij zijn ook beschikbaar als a **beperkte versie** voor de gebruikers van Customer Journey Analytics, afhankelijk van uw vergunning en eigenschapenactivering. Neem contact op met uw Adobe-vertegenwoordiger voor toegang.

>[!NOTE]
>
>**Geordende campagnegebruikers**: Gebruik de mogelijkheden van Data Mirror die in dit document worden beschreven om met klantengegevens te werken die referentiële integriteit handhaven. Zelfs als uw bron geen opmaak voor het vastleggen van wijzigingsgegevens gebruikt, biedt Data Mirror ondersteuning voor relationele functies, zoals primaire toetsenbordhandhaving, upserts op recordniveau en schema-relaties. Deze eigenschappen verzekeren verenigbare en betrouwbare gegevensmodellering over verbonden datasets.

Data Mirror gebruikt relationele schema&#39;s om het vastleggen van wijzigingsgegevens uit te breiden en geavanceerde mogelijkheden voor databasesynchronisatie in te schakelen. Voor een overzicht van Data Mirror, zie [ overzicht van Data Mirror ](../../../xdm/data-mirror/overview.md).

Relationele schema&#39;s breiden Experience Platform uit om primaire zeer belangrijke uniciteit af te dwingen, rij-vlakke veranderingen te volgen, en schema-vlakke verhoudingen te bepalen. Met veranderingsgegevens vangen, passen zij tussenvoegsels toe, updates, en schrapt direct in het gegevensmeer, die de behoefte aan Extraheren, Transformeren, Lading (ETL) of handverzoening verminderen.

Zie [ Overzicht Relationele schema&#39;s ](../../../xdm/schema/relational.md) voor meer informatie.

### Relationele schemavereisten voor het vangen van veranderingsgegevens

Voordat u een relationeel schema gebruikt met het vastleggen van wijzigingsgegevens, configureert u de volgende id&#39;s:

* Elke record op unieke wijze identificeren met een primaire sleutel.
* Pas opeenvolgende updates toe met behulp van een versie-id.
* Voeg een tijdstempel-id toe aan tijdreeksschema&#39;s.

### Bediening van kolommen {#control-column-handling}

Gebruik de kolom `_change_request_type` om op te geven hoe elke rij moet worden verwerkt:

* `u` — upsert (standaardwaarde als de kolom ontbreekt)
* `d` — delete

Deze kolom wordt alleen geëvalueerd tijdens inname en wordt niet opgeslagen of toegewezen aan XDM-velden.

### Workflow {#workflow}

Om veranderingsgegevens toe te laten vangen met een relationeel schema:

1. Maak een relationeel schema.
2. Voeg de vereiste beschrijvingen toe:
   * [Descriptor primaire sleutel](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [Versiebeschrijving](../../../xdm/api/descriptors.md#version-descriptor)
   * [ de beschrijver van de tijdstempel ](../../../xdm/api/descriptors.md#timestamp-descriptor) (tijd-reeksen slechts)
3. Creeer een dataset van het schema en laat veranderingsgegevens toe vangen.
4. Alleen voor op een bestand gebaseerde invoer: voeg de kolom `_change_request_type` toe aan uw bronbestanden als u expliciet verwijderingsbewerkingen moet opgeven. CDC-exportconfiguraties verwerken dit automatisch voor databasebronnen.
5. Voltooi de instelling van de bronverbinding om opname in te schakelen.

>[!NOTE]
>
>De kolom `_change_request_type` is alleen vereist voor bestandsgebaseerde bronnen (Amazon S3, Azure Blob, Google Cloud Storage, SFTP) wanneer u wijzigingsgedrag op rijniveau expliciet wilt bepalen. Voor databasebronnen met native CDC-mogelijkheden worden wijzigingsbewerkingen automatisch afgehandeld via CDC-exportconfiguraties. Op bestand gebaseerde invoer gaat standaard uit van upserbewerkingen. U hoeft deze kolom alleen toe te voegen als u verwijderbewerkingen wilt opgeven in het uploaden van bestanden.

>[!IMPORTANT]
>
>**de schrapping van Gegevens planning wordt vereist**. Alle toepassingen die relationele schema&#39;s gebruiken moeten schrappingsimplicaties begrijpen alvorens veranderingsgegevens uit te voeren vangen. Plan voor hoe schrappingen verwante datasets, nalevingsvereisten, en stroomafwaartse processen zullen beïnvloeden. Zie [ overwegingen van de gegevenshygiëne ](../../../hygiene/ui/record-delete.md#relational-record-delete) voor begeleiding.

## Wijzigingsgegevens opgeven voor op bestanden gebaseerde bronnen {#file-based-sources}

>[!IMPORTANT]
>
>Voor het vastleggen van wijzigingsgegevens op basis van bestanden is Data Mirror met relationele schema&#39;s vereist. Alvorens de dossier volgende formatterende stappen hieronder te volgen, zorg ervoor u het [ de opstellingswerkschema van Data Mirror ](#workflow) eerder in dit document beschreven hebt voltooid. In de onderstaande stappen wordt beschreven hoe u uw gegevensbestanden kunt opmaken met informatie over het bijhouden van wijzigingen die door Data Mirror wordt verwerkt.

Voor bestandsgebaseerde bronnen ([!DNL Amazon S3] , [!DNL Azure Blob] , [!DNL Google Cloud Storage] en [!DNL SFTP] ) neemt u een `_change_request_type` -kolom op in uw bestanden.

Gebruik de `_change_request_type` waarden die in de [ worden bepaald kolom behandelende ](#control-column-handling) sectie hierboven.

>[!IMPORTANT]
>
>Voor **dossier-gebaseerde slechts bronnen**, kunnen bepaalde toepassingen een `_change_request_type` kolom met of `u` (upsert) of `d` (schrapping) vereisen om verandering volgende mogelijkheden te bevestigen. Bijvoorbeeld, vereist de Adobe Journey Optimizer **Geordende campagnes** eigenschap deze kolom om de &quot;Geordende campagneknevel&quot;toe te laten en datasetselectie voor het richten toe te staan. Toepassingsspecifieke validatievereisten kunnen variëren.

Voer de onderstaande bronspecifieke stappen uit.

### Opslagbronnen voor cloud {#cloud-storage-sources}

Schakel het vastleggen van wijzigingsgegevens voor bronnen voor cloudopslag als volgt in:

1. Maak een basisverbinding voor uw bron:

   | Bron | Basisverbindingshulplijn |
   |---|---|
   | [!DNL Amazon S3] | [ creeer a [!DNL Amazon S3]  basisverbinding ](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [ creeer a [!DNL Azure Blob]  basisverbinding ](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [ creeer a [!DNL Google Cloud Storage]  basisverbinding ](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [ creeer a [!DNL SFTP]  basisverbinding ](../api/create/cloud-storage/sftp.md) |

2. [ creeer een bronverbinding voor een wolkenopslag ](../api/collect/cloud-storage.md#create-a-source-connection).

Alle bronnen van de wolkenopslag gebruiken het zelfde `_change_request_type` kolomformaat dat in de [ op dossier-gebaseerde bronnen ](#file-based-sources) hierboven wordt beschreven sectie.

## Databasebronnen {#database-sources}

### [!DNL Azure Databricks]

Om veranderingsgegevens te gebruiken vangt met [!DNL Azure Databricks], moet u **voer van veranderingsgegevens** in uw bronlijsten toelaten en Data Mirror met relationele schema&#39;s in Experience Platform vormen.

Gebruik de volgende opdrachten om de invoer van wijzigingsgegevens in uw tabellen in te schakelen:

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

### [!DNL Data Landing Zone]

Om veranderingsgegevens te gebruiken vangt met [!DNL Data Landing Zone], moet u **voer van veranderingsgegevens** in uw bronlijsten toelaten en Data Mirror met relationele schema&#39;s in Experience Platform vormen.

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Data Landing Zone] bronverbinding:

* [ creeer a [!DNL Data Landing Zone]  basisverbinding ](../api/create/cloud-storage/data-landing-zone.md).
* [ creeer een bronverbinding voor een wolkenopslag ](../api/collect/cloud-storage.md#create-a-source-connection).

### [!DNL Google BigQuery]

Als u wijzigingsgegevens wilt vastleggen met [!DNL Google BigQuery] , moet u de wijzigingshistorie in uw brontabellen inschakelen en Data Mirror configureren met relationele schema&#39;s in Experience Platform.

Als u wijzigingsgeschiedenis wilt inschakelen in uw [!DNL Google BigQuery] bronverbinding, navigeert u naar de [!DNL Google BigQuery] -pagina in de [!DNL Google Cloud] -console en stelt u `enable_change_history` in op `TRUE` . Met deze eigenschap wordt de wijzigingshistorie voor uw gegevenstabel ingeschakeld.

Voor meer informatie, lees de gids over [ de taalverklaringen van de gegevensdefinitie in  [!DNL GoogleSQL] ](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Google BigQuery] bronverbinding:

* [ creeer a [!DNL Google BigQuery]  basisverbinding ](../api/create/databases/bigquery.md).
* [ creeer een bronverbinding voor een gegevensbestand ](../api/collect/database-nosql.md#create-a-source-connection).

### [!DNL Snowflake]

Om veranderingsgegevens te gebruiken vangen met [!DNL Snowflake], moet u **verandering het volgen** in uw bronlijsten toelaten en Data Mirror met relationele schema&#39;s in Experience Platform vormen.

Schakel in [!DNL Snowflake] de optie Wijzigingen bijhouden in met de waarden `ALTER TABLE` en `CHANGE_TRACKING` op `TRUE` .

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Voor meer informatie, lees de [[!DNL Snowflake]  gids bij het gebruiken van de veranderingsclausule ](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Lees de volgende documentatie voor stappen over het inschakelen van het vastleggen van wijzigingsgegevens voor uw [!DNL Snowflake] bronverbinding:

* [ creeer a [!DNL Snowflake]  basisverbinding ](../api/create/databases/snowflake.md).
* [ creeer een bronverbinding voor een gegevensbestand ](../api/collect/database-nosql.md#create-a-source-connection).
