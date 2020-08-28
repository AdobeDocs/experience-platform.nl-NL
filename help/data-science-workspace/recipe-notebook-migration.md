---
keywords: Experience Platform;Data Science Workspace;popular topics;Recipe migration guides;Notebook migration guide
solution: Experience Platform
title: Hulplijnen voor recept- en laptopmigratie
topic: Tutorial
description: In de volgende handleidingen worden de stappen en informatie beschreven die nodig zijn voor het migreren van bestaande recepten en laptops in de Data Science Workspace.
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '3330'
ht-degree: 0%

---


# Hulplijnen voor recept- en laptopmigratie

>[!NOTE]
>
>Laptops en recepten die gebruikmaken van [!DNL Python]R blijven ongewijzigd. De migratie geldt alleen voor PySpark/[!DNL Spark] (2.3) recepten en notebooks.

In de volgende handleidingen worden de stappen en informatie beschreven die nodig zijn voor het migreren van bestaande recepten en laptops.

- [Hulplijnen voor migratie ontvang](#recipe-migration)
- [Laptopmigratiehulplijnen](#notebook-migration)

## Hulplijnen voor migratie ontvang {#recipe-migration}

Recente wijzigingen [!DNL Data Science Workspace] vereisen dat bestaande recepten [!DNL Spark] en PySpark worden bijgewerkt. Gebruik de volgende workflows om u te helpen bij de overgang van uw recepten.

- [Gids voor parkmigratie](#spark-migration-guide)
   - [Wijzigen hoe u gegevenssets leest en schrijft](#read-write-recipe-spark)
   - [Download het voorbeeldrecept](#download-sample-spark)
   - [Het dockingbestand toevoegen](#add-dockerfile-spark)
   - [Afhankelijkheden controleren](#change-dependencies-spark)
   - [Dockerscripts voorbereiden](#prepare-docker-spark)
   - [recept maken met docker](#create-recipe-spark)
- [PySpark-migratiegids](#pyspark-migration-guide)
   - [Wijzigen hoe u gegevenssets leest en schrijft](#pyspark-read-write)
   - [Download het voorbeeldrecept](#pyspark-download-sample)
   - [Het dockingbestand toevoegen](#pyspark-add-dockerfile)
   - [Dockerscripts voorbereiden](#pyspark-prepare-docker)
   - [recept maken met docker](#pyspark-create-recipe)

## [!DNL Spark] migratiegids {#spark-migration-guide}

Het recept artefact dat door de bouwstijlstappen wordt geproduceerd is nu een beeld van de Docker dat uw .jar binair dossier bevat. Daarnaast is de syntaxis die wordt gebruikt voor het lezen en schrijven van gegevenssets met de [!DNL Platform] SDK gewijzigd en moet u de recept-code wijzigen.

De volgende video is ontworpen om meer inzicht te krijgen in de wijzigingen die vereist zijn voor [!DNL Spark] recepten:

>[!VIDEO](https://video.tv.adobe.com/v/33243)

### Gegevenssets lezen en schrijven ([!DNL Spark]) {#read-write-recipe-spark}

Alvorens u het beeld van de Docker bouwt, herzie de voorbeelden voor het lezen van en het schrijven van datasets in [!DNL Platform] SDK, die in de hieronder secties wordt verstrekt. Als u bestaande recepten converteert, moet uw [!DNL Platform] SDK-code worden bijgewerkt.

#### Een gegevensset lezen

Deze sectie schetst de veranderingen die voor het lezen van een dataset nodig zijn en gebruikt het [helper.range](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/helper/Helper.scala) voorbeeld, dat door Adobe wordt verstrekt.

**Oude manier om een dataset te lezen**

```scala
 var df = sparkSession.read.format("com.adobe.platform.dataset")
    .option(DataSetOptions.orgId, orgId)
    .option(DataSetOptions.serviceToken, serviceToken)
    .option(DataSetOptions.userToken, userToken)
    .option(DataSetOptions.serviceApiKey, apiKey)
    .load(dataSetId)
```

**Nieuwe manier om een dataset te lezen**

Met de updates van [!DNL Spark] recepten moet een aantal waarden worden toegevoegd en gewijzigd. Ten eerste wordt `DataSetOptions` het niet meer gebruikt. Vervangen `DataSetOptions` door `QSOption`. Daarnaast zijn nieuwe `option` parameters vereist. Zowel `QSOption.mode` als `QSOption.datasetId` zijn nodig. Tot slot `orgId` en `serviceApiKey` moeten we het veranderen in `imsOrg` en `apiKey`. Bekijk het volgende voorbeeld voor een vergelijking bij het lezen van datasets:

```scala
import com.adobe.platform.query.QSOption
var df = sparkSession.read.format("com.adobe.platform.query")
  .option(QSOption.userToken", {userToken})
  .option(QSOption.serviceToken, {serviceToken})
  .option(QSOption.imsOrg, {orgId})
  .option(QSOption.apiKey, {apiKey})
  .option(QSOption.mode, "interactive")
  .option(QSOption.datasetId, {dataSetId})
  .load()
```

>[!TIP]
>
> De interactieve wijzetijden uit als de vragen langer dan 10 minuten lopen. Als u meer dan een paar gigabytes aan gegevens opneemt, adviseert men dat u op &quot;partij&quot;wijze overschakelt. De batterijmodus duurt langer om te starten, maar kan grotere gegevenssets verwerken.

#### Schrijven naar een gegevensset

Deze sectie schetst de veranderingen nodig voor het schrijven van een dataset door het [ScoringDataSaver.range](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/ScoringDataSaver.scala) voorbeeld te gebruiken, die door Adobe wordt verstrekt.

**Oude manier om een dataset te schrijven**

```scala
df.write.format("com.adobe.platform.dataset")
    .option(DataSetOptions.orgId, orgId)
    .option(DataSetOptions.serviceToken, serviceToken)
    .option(DataSetOptions.userToken, userToken)
    .option(DataSetOptions.serviceApiKey, apiKey)
    .save(scoringResultsDataSetId)
```

**Nieuwe manier om een dataset te schrijven**

Met de updates van [!DNL Spark] recepten moet een aantal waarden worden toegevoegd en gewijzigd. Ten eerste wordt `DataSetOptions` het niet meer gebruikt. Vervangen `DataSetOptions` door `QSOption`. Daarnaast zijn nieuwe `option` parameters vereist. `QSOption.datasetId` is vereist en vervangt de noodzaak om de `{dataSetId}` insteekmodule te laden `.save()`. Tot slot `orgId` en `serviceApiKey` moeten we het veranderen in `imsOrg` en `apiKey`. Bekijk het volgende voorbeeld voor een vergelijking bij het schrijven van datasets:

```scala
import com.adobe.platform.query.QSOption
df.write.format("com.adobe.platform.query")
  .option(QSOption.userToken", {userToken})
  .option(QSOption.serviceToken, {serviceToken})
  .option(QSOption.imsOrg, {orgId})
  .option(QSOption.apiKey, {apiKey})
  .option(QSOption.datasetId, {dataSetId})
  .save()
```

### Bronbestanden op basis van Docker-pakket ([!DNL Spark]) {#package-docker-spark}

Begin door naar de directory te navigeren waar uw recept zich bevindt.

In de volgende secties wordt gebruikgemaakt van het nieuwe Scala Retail Sales-recept dat u kunt vinden in de [Data Science Workspace public Github-opslagplaats](https://github.com/adobe/experience-platform-dsw-reference).

### Download het voorbeeldrecept ([!DNL Spark]) {#download-sample-spark}

Het voorbeeldrecept bevat bestanden die naar het bestaande recept moeten worden gekopieerd. Als u de openbare Github wilt klonen die alle voorbeeldrecepten bevat, voert u het volgende in de terminal in:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Het Scala-recept bevindt zich in de volgende directory `experience-platform-dsw-reference/recipes/scala/retail`.

### Dockerfile toevoegen ([!DNL Spark]) {#add-dockerfile-spark}

Er is een nieuw bestand nodig in de map Recept om de op docker gebaseerde workflow te kunnen gebruiken. Kopieer en plak het Dockerbestand vanuit de map recipes in `experience-platform-dsw-reference/recipes/scala/Dockerfile`de map. U kunt desgewenst ook de onderstaande code kopiëren en plakken in een nieuw bestand met de naam `Dockerfile`.

>[!IMPORTANT]
>
> Het hieronder weergegeven voorbeeldjar-bestand `ml-retail-sample-spark-*-jar-with-dependencies.jar` moet worden vervangen door de naam van het jar-bestand van uw recept.

```scala
FROM adobe/acp-dsw-ml-runtime-spark:0.0.1

COPY target/ml-retail-sample-spark-*-jar-with-dependencies.jar /application.jar
```

### Afhankelijkheden wijzigen ([!DNL Spark]) {#change-dependencies-spark}

Als u een bestaand recept gebruikt, worden de veranderingen vereist in het pom.xml- dossier voor gebiedsdelen. Verander model-creatie-sdk gebiedsdeelversie in 2.0.0. Werk vervolgens de [!DNL Spark] versie in het pombestand bij naar versie 2.4.3 en de Scala-versie naar versie 2.11.12.

```json
<groupId>com.adobe.platform.ml</groupId>
<artifactId>authoring-sdk_2.11</artifactId>
<version>2.0.0</version>
<classifier>jar-with-dependencies</classifier>
```

### De Docker-scripts voorbereiden ([!DNL Spark]) {#prepare-docker-spark}

[!DNL Spark] recepten gebruiken niet langer binaire artefacten en moeten een Docker-afbeelding maken. Als u dit nog niet hebt gedaan, [downloadt en installeert u Docker](https://www.docker.com/products/docker-desktop).

In het meegeleverde Scala-voorbeeldrecept kunt u de scripts vinden `login.sh` en `build.sh` vinden op `experience-platform-dsw-reference/recipes/scala/` . Kopieer en plak deze bestanden in uw bestaande recept.

De mapstructuur moet er nu hetzelfde uitzien als in het volgende voorbeeld (nieuw toegevoegde bestanden worden gemarkeerd):

![mapstructuur](./images/migration/scala-folder.png)

De volgende stap bestaat uit het volgen van de bronbestanden van het [pakket in een zelfstudie over het recept](./models-recipes/package-source-files-recipe.md) . Deze zelfstudie bevat een sectie waarin de bouw van een dockerafbeelding voor een Scala-recept (Spark) wordt beschreven. Zodra volledig, wordt u voorzien van het beeld van de Dokker in een Azure Registratie van de Container samen met het overeenkomstige beeld URL.

### Een recept maken ([!DNL Spark]) {#create-recipe-spark}

Als u een recept wilt maken, moet u eerst de zelfstudie over bronbestanden [in het](./models-recipes/package-source-files-recipe.md) pakket voltooien en de URL van de dockerafbeelding gereed hebben. U kunt een recept maken met de gebruikersinterface of API.

Als u uw recept wilt maken met de gebruikersinterface, volgt u de zelfstudie voor het verpakken van een recept (UI) [voor het](./models-recipes/import-packaged-recipe-ui.md) importeren van Scala.

Als u uw recept wilt maken met de API, volgt u de zelfstudie [voor het verpakte recept (API)](./models-recipes/import-packaged-recipe-api.md) voor Scala.

## PySpark-migratiegids {#pyspark-migration-guide}

Het recept artefact dat door de bouwstijlstappen wordt geproduceerd is nu een beeld van de Docker dat uw binair dossier .egg bevat. Daarnaast is de syntaxis die wordt gebruikt voor het lezen en schrijven van gegevenssets met de [!DNL Platform] SDK gewijzigd en moet u de recept-code wijzigen.

De volgende video wordt ontworpen om in het begrijpen van de veranderingen verder te helpen die voor PySpark recepten worden vereist:

>[!VIDEO](https://video.tv.adobe.com/v/33048?learn=on&quality=12)

### Gegevenssets lezen en schrijven (PySpark) {#pyspark-read-write}

Alvorens u het beeld van de Docker bouwt, herzie de voorbeelden voor het lezen van en het schrijven van datasets in [!DNL Platform] SDK, die in de hieronder secties wordt verstrekt. Als u bestaande recepten converteert, moet uw [!DNL Platform] SDK-code worden bijgewerkt.

#### Een gegevensset lezen

Deze sectie schetst de veranderingen nodig voor het lezen van een dataset door het [helper.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/pyspark/pysparkretailapp/helper.py) voorbeeld te gebruiken, die door Adobe wordt verstrekt.

**Oude manier om een dataset te lezen**

```python
dataset_options = get_dataset_options(spark.sparkContext)
pd = spark.read.format("com.adobe.platform.dataset") 
  .option(dataset_options.serviceToken(), service_token) 
  .option(dataset_options.userToken(), user_token) 
  .option(dataset_options.orgId(), org_id) 
  .option(dataset_options.serviceApiKey(), api_key)
  .load(dataset_id)
```

**Nieuwe manier om een dataset te lezen**

Met de updates van [!DNL Spark] recepten moet een aantal waarden worden toegevoegd en gewijzigd. Ten eerste wordt `DataSetOptions` het niet meer gebruikt. Vervangen `DataSetOptions` door `qs_option`. Daarnaast zijn nieuwe `option` parameters vereist. Zowel `qs_option.mode` als `qs_option.datasetId` zijn nodig. Tot slot `orgId` en `serviceApiKey` moeten we het veranderen in `imsOrg` en `apiKey`. Bekijk het volgende voorbeeld voor een vergelijking bij het lezen van datasets:

```python
qs_option = spark_context._jvm.com.adobe.platform.query.QSOption
pd = sparkSession.read.format("com.adobe.platform.query") 
  .option(qs_option.userToken, {userToken}) 
  .option(qs_option.serviceToken, {serviceToken}) 
  .option(qs_option.imsOrg, {orgId}) 
  .option(qs_option.apiKey, {apiKey}) 
  .option(qs_option.mode, "interactive") 
  .option(qs_option.datasetId, {dataSetId}) 
  .load()
```

>[!TIP]
>
> De interactieve wijzetijden uit als de vragen langer dan 10 minuten lopen. Als u meer dan een paar gigabytes aan gegevens opneemt, adviseert men dat u op &quot;partij&quot;wijze overschakelt. De batterijmodus duurt langer om te starten, maar kan grotere gegevenssets verwerken.

#### Schrijven naar een gegevensset

Deze sectie schetst de veranderingen nodig voor het schrijven van een dataset door het [data_saver.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/pyspark/pysparkretailapp/data_saver.py) voorbeeld te gebruiken, die door Adobe wordt verstrekt.

**Oude manier om een dataset te schrijven**

```python
df.write.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, orgId)
  .option(DataSetOptions.serviceToken, serviceToken)
  .option(DataSetOptions.userToken, userToken)
  .option(DataSetOptions.serviceApiKey, apiKey)
  .save(scoringResultsDataSetId)
```

**Nieuwe manier om een dataset te schrijven**

Met de updates aan PySpark recepten, moet een aantal waarden worden toegevoegd en worden veranderd. Ten eerste wordt `DataSetOptions` het niet meer gebruikt. Vervangen `DataSetOptions` door `qs_option`. Daarnaast zijn nieuwe `option` parameters vereist.  `qs_option.datasetId` is vereist en vervangt de noodzaak om de `{dataSetId}` in te laden `.save()` . Tot slot `orgId` en `serviceApiKey` moeten we het veranderen in `imsOrg` en `apiKey`. Bekijk het volgende voorbeeld voor een vergelijking bij het lezen van datasets:

```python
qs_option = spark_context._jvm.com.adobe.platform.query.QSOption
scored_df.write.format("com.adobe.platform.query") 
  .option(qs_option.userToken, {userToken}) 
  .option(qs_option.serviceToken, {serviceToken}) 
  .option(qs_option.imsOrg, {orgId}) 
  .option(qs_option.apiKey, {apiKey}) 
  .option(qs_option.datasetId, {dataSetId}) 
  .save()
```

### Op docker gebaseerde bronbestanden in pakketten (PySpark) {#pyspark-package-docker}

Begin door naar de directory te navigeren waar uw recept zich bevindt.

In dit voorbeeld wordt het nieuwe PySpark Retail Sales-recept gebruikt en is het te vinden in de [Data Science Workspace public Github-opslagplaats](https://github.com/adobe/experience-platform-dsw-reference).

### Download het voorbeeldrecept (PySpark) {#pyspark-download-sample}

Het voorbeeldrecept bevat bestanden die naar het bestaande recept moeten worden gekopieerd. Om het publiek te klonen [!DNL Github] dat alle steekproefrecepten bevat, ga het volgende in terminal in.

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Het PySpark-recept bevindt zich in de volgende directory `experience-platform-dsw-reference/recipes/pyspark`.

### Dockerfile toevoegen (PySpark) {#pyspark-add-dockerfile}

Er is een nieuw bestand nodig in de map Recept om de op docker gebaseerde workflow te kunnen gebruiken. Kopieer en plak het Dockerbestand vanuit de map recipes in `experience-platform-dsw-reference/recipes/pyspark/Dockerfile`de map. U kunt desgewenst ook de onderstaande code kopiëren en plakken en een nieuw bestand maken met de naam `Dockerfile`.

>[!IMPORTANT]
>
> Het onderstaande voorbeeld-eibestand `pysparkretailapp-*.egg` moet worden vervangen door de naam van het eibestand van uw recept.

```scala
FROM adobe/acp-dsw-ml-runtime-pyspark:0.0.1
RUN mkdir /recipe

COPY . /recipe

RUN cd /recipe && \
    ${PYTHON} setup.py clean install && \
    rm -rf /recipe

RUN cp /databricks/conda/envs/${DEFAULT_DATABRICKS_ROOT_CONDA_ENV}/lib/python3.6/site-packages/pysparkretailapp-*.egg /application.egg
```

### De Docker-scripts voorbereiden (PySpark) {#pyspark-prepare-docker}

PySpark-recepten gebruiken niet langer Binaire artefacten en vereisen in plaats daarvan het maken van een Docker-afbeelding. Download en installeer [Docker](https://www.docker.com/products/docker-desktop)als u dat nog niet hebt gedaan.

In het meegeleverde PySpark-voorbeeldrecept kunt u de scripts vinden `login.sh` en `build.sh` vinden op `experience-platform-dsw-reference/recipes/pyspark` . Kopieer en plak deze bestanden in uw bestaande recept.

De mapstructuur moet er nu hetzelfde uitzien als in het volgende voorbeeld (nieuw toegevoegde bestanden worden gemarkeerd):

![mapstructuur](./images/migration/folder.png)

Uw recept is nu klaar om te worden gebouwd met een Docker-afbeelding. De volgende stap bestaat uit het volgen van de bronbestanden van het [pakket in een zelfstudie over het recept](./models-recipes/package-source-files-recipe.md) . Deze zelfstudie bevat een sectie met een overzicht van het maken van een dockerafbeelding voor een PySpark-recept (Spark 2.4). Zodra volledig, wordt u voorzien van het beeld van de Dokker in een Azure Registratie van de Container samen met het overeenkomstige beeld URL.

### Een recept maken (PySpark) {#pyspark-create-recipe}

Als u een recept wilt maken, moet u eerst de zelfstudie over bronbestanden [in het](./models-recipes/package-source-files-recipe.md) pakket voltooien en de URL van de dockerafbeelding gereed hebben. U kunt een recept maken met de gebruikersinterface of API.

Om uw recept te bouwen gebruikend UI, volg de [invoer een verpakte recept (UI)](./models-recipes/import-packaged-recipe-ui.md) zelfstudie voor PySpark.

Als u het recept wilt maken met de API, volgt u de zelfstudie [voor verpakte recept (API)](./models-recipes/import-packaged-recipe-api.md) voor PySpark.

## Laptopmigratiehulplijnen {#notebook-migration}

Recente wijzigingen in [!DNL JupyterLab] laptops vereisen dat u uw bestaande PySpark- en [!DNL Spark] 2.3-laptops bijwerkt naar 2.4. Met deze wijziging [!DNL JupyterLab Launcher] is deze versie bijgewerkt met nieuwe startlaptops. Voor een stapsgewijze handleiding voor het omzetten van uw laptops selecteert u een van de volgende hulplijnen:

- [PySpark 2.3 tot 2.4-migratiegids](#pyspark-notebook-migration)
- [Spark 2.3 aan Vonk 2.4 (Scala) migratiegids](#spark-notebook-migration)

De volgende video is ontworpen om meer inzicht te krijgen in de wijzigingen die vereist zijn voor [!DNL JupyterLab Notebooks]:

>[!VIDEO](https://video.tv.adobe.com/v/33444?quality=12&learn=on)

## PySpark 2.3 tot 2.4 laptopmigratiehandleiding {#pyspark-notebook-migration}

Met de introductie van PySpark 2.4 aan [!DNL JupyterLab Notebooks], gebruiken de nieuwe [!DNL Python] laptops met PySpark 2.4 nu de [!DNL Python] 3 kernel in plaats van PySpark 3 kernel. Dit betekent bestaande code die op PySpark 2.3 loopt niet in PySpark 2.4 wordt gesteund.

>[!IMPORTANT]
>
>PySpark 2.3 is afgekeurd en ingesteld om in een volgende versie te worden verwijderd. Alle bestaande voorbeelden worden geplaatst om met PySpark 2.4 voorbeelden worden vervangen.

Volg de onderstaande voorbeelden om uw bestaande PySpark 3 ([!DNL Spark] 2.3)-laptops om te zetten in [!DNL Spark] 2.4:

### Kernel

PySpark 3 ([!DNL Spark] 2.4) notebooks gebruiken de Python 3 Kernel in plaats van de afgekeurde PySpark kernel die in PySpark 3 (Spark 2.3 - afgekeurd) notebooks wordt gebruikt.

Als u de kernel in de [!DNL JupyterLab] gebruikersinterface wilt bevestigen of wijzigen, selecteert u de kernelknop in de rechterbovennavigatiebalk van uw laptop. Als u een van de vooraf gedefinieerde laptops voor startprogramma&#39;s gebruikt, wordt de kernel vooraf geselecteerd. In het onderstaande voorbeeld wordt de startfunctie van de PySpark 3 ([!DNL Spark] 2.4)- *aggregatielaptop* gebruikt.

![controlekernel](./images/migration/pyspark-migration/check-kernel.png)

Als u het vervolgkeuzemenu selecteert, wordt een lijst met beschikbare kernels geopend.

![kernel selecteren](./images/migration/pyspark-migration/kernel-click.png)

![kerneldropdown](./images/migration/pyspark-migration/select-kernel.png)

Selecteer voor PySpark 3 ([!DNL Spark] 2.4)-laptops de Python 3-kernel en klik op de knop **Selecteren** om dit te bevestigen.

![kernel bevestigen](./images/migration/pyspark-migration/confirm-kernel.png)

## sparkSession initialiseren

Alle [!DNL Spark] 2.4 laptops vereisen dat u de zitting met de nieuwe boilerplate code initialiseert.

<table>
  <th>Laptop</th>
  <th>PySpark 3 ([!DNL Spark] 2.3 - afgekeurd)</th>
  <th>PySpark 3 ([!DNL Spark] 2.4)</th>
  <tr>
  <th>Kernel</th>
  <td align="center">PySpark 3</td>
  <td align="center">Python 3</td>
  </tr>
  <tr>
  <th>Code</th>
  <td>
  <pre class="JSON language-JSON hljs">
  [!DNL spark]
</pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
van pyspark.sql import SparkSessionspark = SparkSession.builder.getOrCreate()
</pre>
  </td>
  </tr>
</table>

De volgende beelden benadrukken de verschillen in configuratie voor PySpark 2.3 en PySpark 2.4. In dit voorbeeld worden de *aggregatie* -startlaptops gebruikt die in [!DNL JupyterLab Launcher].

**Voorbeeld van configuratie voor 2.3 (afgekeurd)**

![config 1](./images/migration/pyspark-migration/2.3-config.png)![config 2](./images/migration/pyspark-migration/2.3-config-import.png)

**Voorbeeld van configuratie voor 2.4**

![config 3](./images/migration/pyspark-migration/2.4-config.png)

## Tovermagie %dataset gebruiken {#magic}

Met de introductie van [!DNL Spark] 2.4 wordt `%dataset` aangepaste magie geleverd voor gebruik in nieuwe PySpark 3 ([!DNL Spark] 2.4) notebooks ([!DNL Python] 3 kernel).

**Gebruik**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Beschrijving**

Een aangepaste opdracht voor het [!DNL Data Science Workspace] schrijven of lezen van een gegevensset van een [!DNL Python] laptop ([!DNL Python] 3 kernel).

- **{action}**: Het type van actie op de dataset uit te voeren. Er zijn twee handelingen beschikbaar: &quot;read&quot; of &quot;write&quot;.
- **—datasetId {id}**: Gebruikt om identiteitskaart van de dataset te leveren om te lezen of te schrijven. Dit is een verplicht argument.
- **—dataFrame {df}**: Het dataframe van de pandas. Dit is een verplicht argument.
   - Wanneer de handeling &quot;read&quot; is, is {df} de variabele waar de resultaten van de bewerking voor het lezen van de gegevensset beschikbaar zijn.
   - Wanneer de actie &quot;schrijven&quot;is, wordt dit dataframe {df} geschreven aan de dataset.
- **—modus (optioneel)**: Toegestane parameters zijn &quot;batch&quot; en &quot;interactief&quot;. De modus is standaard ingesteld op &quot;interactief&quot;. Het wordt aanbevolen de modus &quot;batch&quot; te gebruiken bij het lezen van grote hoeveelheden gegevens.

**Voorbeelden**

- **Voorbeeld** lezen: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **Voorbeeld** schrijven: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

## Laden in een dataframe in LocalContext

Met de introductie van [!DNL Spark] 2.4 wordt [`%dataset`](#magic) aangepaste magie geleverd. In het volgende voorbeeld worden de belangrijkste verschillen voor het laden van dataframe in PySpark ([!DNL Spark] 2.3) en PySpark ([!DNL Spark] 2.4) notebooks gemarkeerd:

**Gebruikend PySpark 3 ([!DNL Spark]2.3 - afgekeurd) - PySpark 3 Kernel**

```python
dataset_options = sc._jvm.com.adobe.platform.dataset.DataSetOptions
pd0 = spark.read.format("com.adobe.platform.dataset")
  .option(dataset_options.orgId(), "310C6D375BA5248F0A494212@AdobeOrg")
  .load("5e68141134492718af974844")
```

**Werken met PySpark 3 ([!DNL Spark]2.4) - Python 3 Kernel**

```python
%dataset read --datasetId 5e68141134492718af974844 --dataFrame pd0
```

| Element | Beschrijving |
| ------- | ----------- |
| pd0 | Naam van dataframe van pandas dat moet worden gebruikt of gemaakt. |
| [%dataset](#magic) | Aangepaste magie voor gegevenstoegang in [!DNL Python] 3 kernel. |

De volgende beelden benadrukken de belangrijkste verschillen in ladingsgegevens voor PySpark 2.3 en PySpark 2.4. In dit voorbeeld worden de *aggregatie* -startlaptops gebruikt die in [!DNL JupyterLab Launcher].

**Gegevens laden in PySpark 2.3 (Luminagegegevensset) - afgekeurd**

![Laden 1](./images/migration/pyspark-migration/2.3-load.png)

**Gegevens laden in PySpark 2.4 (Luminagegegevensset)**

Met PySpark 3 (Vonk 2.4) `sc = spark.sparkContext` wordt bepaald in lading.

![Laden 1](./images/migration/pyspark-migration/2.4-load.png)

**Gegevens laden[!DNL Experience Cloud Platform]in PySpark 2.3 - afgekeurd**

![Laden 2](./images/migration/pyspark-migration/2.3-load-alt.png)

**Gegevens laden[!DNL Experience Cloud Platform]in PySpark 2.4**

Met PySpark 3 ([!DNL Spark] 2.4) hoeven de `org_id` en `dataset_id` niet langer te worden gedefinieerd. Bovendien `df = spark.read.format` is deze vervangen door een aangepaste magie [`%dataset`](#magic) om het lezen en schrijven van datasets te vereenvoudigen.

![Laden 2](./images/migration/pyspark-migration/2.4-load-alt.png)

| Element | beschrijving |
| ------- | ----------- |
| [%dataset](#magic) | Aangepaste magie voor gegevenstoegang in [!DNL Python] 3 kernel. |

>[!TIP]
>
>—mode kan aan `interactive` of worden geplaatst `batch`. De standaardwaarde voor —mode is `interactive`. Het wordt aanbevolen de `batch` modus te gebruiken wanneer u grote hoeveelheden gegevens leest.

## Een lokaal dataframe maken

Met PySpark 3 ([!DNL Spark] 2.4) wordt `%%` sparkmagic niet meer ondersteund. De volgende bewerkingen kunnen niet meer worden gebruikt:

- `%%help`
- `%%info`
- `%%cleanup`
- `%%delete`
- `%%configure`
- `%%local`

In de volgende tabel worden de wijzigingen beschreven die nodig zijn om `%%sql` query&#39;s in sparkmagic om te zetten:

<table>
  <th>Laptop</th>
  <th>PySpark 3 ([!DNL Spark] 2.3 - afgekeurd)</th>
  <th>PySpark 3 ([!DNL Spark] 2.4)</th>
  <tr>
  <th>Kernel</th>
  <td align="center">PySpark 3</td>
  <td align="center">[!DNL Python] 3</td>
  </tr>
  <tr>
  <th>Code</th>
      <td>
         <pre class="JSON language-JSON hljs">%%sql -o dfselect * van sparkdf
</pre>
         <pre class="JSON language-JSON hljs"> %%sql -o df -n limitselect * van sparkdf
</pre>
         <pre class="JSON language-JSON hljs">%%sql -o df -qselect * van sparkdf
</pre>
         <pre class="JSON language-JSON hljs"> %%sql -o df -r fractionselect * van sparkdf
</pre>
      </td>
      <td>
         <pre class="JSON language-JSON hljs">
df = spark.sql('' SELECT * FROM sparkdf'')
</pre>
         <pre class="JSON language-JSON hljs">
df = spark.sql('' SELECT * FROM sparkdf LIMIT limit'')
</pre>
         <pre class="JSON language-JSON hljs">
df = spark.sql('' SELECT * FROM sparkdf LIMIT limit'')
</pre>
         <pre class="JSON language-JSON hljs">
sample_df = df.sample(breuk)
</pre>
      </td>
   </tr>
</table>

>[!TIP]
>
>U kunt ook een optioneel zaadmonster opgeven, zoals een booleaan met Vervanging, een dubbele fractie of een lang zaadmonster.

De volgende beelden benadrukken de belangrijkste verschillen voor het creëren van een lokaal dataframe in PySpark 2.3 en PySpark 2.4. In dit voorbeeld worden de *aggregatie* -startlaptops gebruikt die in [!DNL JupyterLab Launcher].

**Lokaal dataframe PySpark 2.3 maken - afgekeurd**

![dataframe 1](./images/migration/pyspark-migration/2.3-dataframe.png)

**Lokaal dataframe PySpark 2.4 maken**

Met PySpark 3 ([!DNL Spark] 2.4) wordt `%%sql` Sparkmagic niet meer ondersteund en is vervangen door:

![dataframe 2](./images/migration/pyspark-migration/2.4-dataframe.png)

## Schrijven naar een gegevensset

Met de introductie van [!DNL Spark] 2.4 wordt [`%dataset`](#magic) aangepaste magie geleverd die het schrijven van datasets schoner maakt. Om aan een dataset te schrijven, gebruik het volgende 2.4 voorbeeld: [!DNL Spark]

**Gebruikend PySpark 3 ([!DNL Spark]2.3 - afgekeurd) - PySpark 3 Kernel**

```python
userToken = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.USER_TOKEN")
serviceToken = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.SERVICE_TOKEN")
serviceApiKey = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.SERVICE_API_KEY")

dataset_options = sc._jvm.com.adobe.platform.dataset.DataSetOptions

pd0.write.format("com.adobe.platform.dataset")
  .option(dataset_options.orgId(), "310C6D375BA5248F0A494212@AdobeOrg")
  .option(dataset_options.userToken(), userToken)
  .option(dataset_options.serviceToken(), serviceToken)
  .option(dataset_options.serviceApiKey(), serviceApiKey)
  .save("5e68141134492718af974844")
```

**PySpark 3 gebruiken ([!DNL Spark]2.4) -[!DNL Python]3 Kernel**

```python
%dataset write --datasetId 5e68141134492718af974844 --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

| Element | beschrijving |
| ------- | ----------- |
| pd0 | Naam van dataframe van pandas dat moet worden gebruikt of gemaakt. |
| [%dataset](#magic) | Aangepaste magie voor gegevenstoegang in [!DNL Python] 3 kernel. |

>[!TIP]
>
>—mode kan aan `interactive` of worden geplaatst `batch`. De standaardwaarde voor —mode is `interactive`. Het wordt aanbevolen de `batch` modus te gebruiken wanneer u grote hoeveelheden gegevens leest.

De volgende beelden benadrukken de belangrijkste verschillen voor het schrijven van gegevens terug naar [!DNL Platform] in PySpark 2.3 en PySpark 2.4. In dit voorbeeld worden de *aggregatie* -startlaptops gebruikt die in [!DNL JupyterLab Launcher].

**Gegevens terugschrijven naar[!DNL Platform]PySpark 2.3 - afgekeurd**

![dataframe 1](./images/migration/pyspark-migration/2.3-write.png)![dataframe 1](./images/migration/pyspark-migration/2.3-write-2.png)![dataframe 1](./images/migration/pyspark-migration/2.3-write-3.png)

**Gegevens terugschrijven naar[!DNL Platform]PySpark 2.4**

Met PySpark 3 ([!DNL Spark] 2.4) verwijdert de `%dataset` douanemagie de behoefte om waarden zoals `userToken`, `serviceToken`, `serviceApiKey`, en `.option`te bepalen. Bovendien hoeft `orgId` niet langer te worden gedefinieerd.

![dataframe 2](./images/migration/pyspark-migration/2.4-write.png)![dataframe 2](./images/migration/pyspark-migration/2.4-write-2.png)

## [!DNL Spark] 2.3 tot [!DNL Spark] 2.4 (Scala) handleiding voor migratie van laptops {#spark-notebook-migration}

Met de introductie van [!DNL Spark] 2,4 naar [!DNL JupyterLab Notebooks], gebruiken bestaande [!DNL Spark] ([!DNL Spark] 2,3) notebooks nu de Scala kernel in plaats van de [!DNL Spark] kernel. Dit betekent dat bestaande code die wordt uitgevoerd op [!DNL Spark] ([!DNL Spark] 2.3) niet wordt ondersteund in Scala ([!DNL Spark] 2.4). Bovendien moeten alle nieuwe [!DNL Spark] laptops gebruikmaken van Scala ([!DNL Spark] 2.4) in de [!DNL JupyterLab Launcher].

>[!IMPORTANT]
>
>[!DNL Spark] ([!DNL Spark] 2.3) is afgekeurd en is ingesteld om in een volgende versie te worden verwijderd. Alle bestaande voorbeelden worden vervangen door Scala-voorbeelden ([!DNL Spark] 2.4).

Volg de onderstaande voorbeelden om uw bestaande [!DNL Spark] ([!DNL Spark] 2.3) laptops om te zetten in Scala ([!DNL Spark] 2.4):

## Kernel

Scala-laptops (Spark 2.4) gebruiken de Scala Kernel in plaats van de afgekeurde [!DNL Spark] kernel die wordt gebruikt in laptops [!DNL Spark] ([!DNL Spark] 2.3 - afgekeurd).

Als u de kernel in de [!DNL JupyterLab] gebruikersinterface wilt bevestigen of wijzigen, selecteert u de kernelknop in de rechterbovennavigatiebalk van uw laptop. Het pop-upvenster *Selecteren van* ernel wordt weergegeven. Als u een van de vooraf gedefinieerde laptops voor startprogramma&#39;s gebruikt, wordt de kernel vooraf geselecteerd. In het onderstaande voorbeeld wordt de Scala *Clustering* -laptop in gebruikt [!DNL JupyterLab Launcher].

![controlekernel](./images/migration/spark-scala/scala-kernel.png)

Als u het vervolgkeuzemenu selecteert, wordt een lijst met beschikbare kernels geopend.

![kerneldropdown](./images/migration/spark-scala/select-dropdown.png)

![kernel selecteren](./images/migration/spark-scala/dropdown.png)

Voor Scala-laptops (Spark 2.4) selecteert u de Scala-kernel en klikt u op de knop **Selecteren** .

![kernel bevestigen](./images/migration/spark-scala/select.png)

## SparkSession initialiseren {#initialize-sparksession-scala}

Alle Scala-laptops ([!DNL Spark] 2.4) vereisen dat u de sessie initialiseert met de volgende bouwsteencode:

<table>
  <th>Laptop</th>
  <th>Vonk ([!DNL Spark] 2.3 - afgekeurd)</th>
  <th>Scala ([!DNL Spark] 2.4)</th>
  <tr>
  <th>Kernel</th>
  <td align="center">[!DNL Spark]</td>
  <td align="center">Scala</td>
  </tr>
  <tr>
  <th>code</th>
  <td align="center">
  geen code vereist
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
import org.apache.spark.sql.{ SparkSession} val spark = SparkSession.builder() .master("local") .getOrCreate()
</pre>
  </td>
  </tr>
</table>

De afbeelding Scala ([!DNL Spark] 2.4) hieronder markeert het belangrijkste verschil in het initialiseren van sparkSession met de [!DNL Spark] 2.3 [!DNL Spark] -kernel en [!DNL Spark] 2.4 Scala-kernel. In dit voorbeeld worden de *Clustering* -startlaptops gebruikt die in [!DNL JupyterLab Launcher].

**[!DNL Spark]([!DNL Spark]2.3 - afgekeurd)**

[!DNL Spark] ([!DNL Spark] 2.3 - afgekeurd) gebruikt de [!DNL Spark] kernel en daarom was u niet verplicht om te definiëren [!DNL Spark].

**Scala ([!DNL Spark]2.4)**

Als u [!DNL Spark] 2.4 gebruikt met de Scala-kernel, moet u definiëren `val spark` en importeren `SparkSesson` om te lezen of te schrijven:

![vonken importeren en definiëren](./images/migration/spark-scala/start-session.png)

## Query-gegevens

Met Scala ([!DNL Spark] 2.4) wordt `%%` sparkmagic niet meer ondersteund. De volgende bewerkingen kunnen niet meer worden gebruikt:

- `%%help`
- `%%info`
- `%%cleanup`
- `%%delete`
- `%%configure`
- `%%local`

In de volgende tabel worden de wijzigingen beschreven die nodig zijn om `%%sql` query&#39;s in sparkmagic om te zetten:

<table>
  <th>Laptop</th>
  <th>[!DNL Spark] ([!DNL Spark] 2.3 - afgekeurd)</th>
  <th>Scala ([!DNL Spark] 2.4)</th>
  <tr>
  <th>Kernel</th>
  <td align="center">[!DNL Spark]</td>
  <td align="center">Scala</td>
  </tr>
  <tr>
  <th>code</th>
    <td>
       <pre class="JSON language-JSON hljs">
%%sql -o dfselect * van sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o df -n limitselect * van sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o df -qselect * van sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o df -r fractionselect * van sparkdf
</pre>
      </td>
      <td>
         <pre class="JSON language-JSON hljs">
val df = spark.sql('' SELECT * FROM sparkdf'')
</pre>
         <pre class="JSON language-JSON hljs">
val df = spark.sql('' SELECT * FROM sparkdf LIMIT limit'')
</pre>
         <pre class="JSON language-JSON hljs">
val df = spark.sql('' SELECT * FROM sparkdf LIMIT limit'')
</pre>
         <pre class="JSON language-JSON hljs">
val sample_df = df.sample(fraction) </pre>
      </td>
   </tr>
</table>

De afbeelding Scala ([!DNL Spark] 2.4) hieronder benadrukt de belangrijkste verschillen in het maken van vragen met de [!DNL Spark] 2.3 [!DNL Spark] kernel en Spark 2.4 Scala kernel. In dit voorbeeld worden de *Clustering* -startlaptops gebruikt die in [!DNL JupyterLab Launcher].

**[!DNL Spark]([!DNL Spark]2.3 - afgekeurd)**

De [!DNL Spark] ([!DNL Spark] 2,3 - afgekeurd) laptop gebruikt de [!DNL Spark] kernel. De [!DNL Spark] kernel ondersteunt en gebruikt `%%sql` sparkmagic.

![](./images/migration/spark-scala/sql-2.3.png)

**Scala ([!DNL Spark]2.4)**

De Scala-kernel ondersteunt geen `%%sql` magie meer. Bestaande magische code moet worden omgezet.

![vonken importeren en definiëren](./images/migration/spark-scala/sql-2.4.png)

## Een gegevensset lezen {#notebook-read-dataset-spark}

In [!DNL Spark] 2.3 moest u variabelen definiëren voor `option` waarden die worden gebruikt om gegevens te lezen of de onbewerkte waarden in de codecel te gebruiken. In Scala, kunt u gebruiken `sys.env("PYDASDK_IMS_USER_TOKEN")` om een waarde te verklaren en terug te keren, elimineert dit de behoefte om variabelen zoals `var userToken`te bepalen. In het Scala (Vonk 2.4) voorbeeld hieronder, `sys.env` wordt gebruikt om alle vereiste waarden te bepalen en terug te keren nodig voor het lezen van een dataset.

**Gebruikt[!DNL Spark]([!DNL Spark]2.3 - afgekeurd) -[!DNL Spark]Kernel**

```scala
import com.adobe.platform.dataset.DataSetOptions
var df1 = spark.read.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, "310C6D375BA5248F0A494212@AdobeOrg")
  .option(DataSetOptions.batchId, "dbe154d3-197a-4e6c-80f8-9b7025eea2b9")
  .load("5e68141134492718af974844")
```

**Scala ([!DNL Spark]2.4) gebruiken - Scala Kernel**

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
  .option("ims-org", sys.env("IMS_ORG_ID"))
  .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
  .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()
```

| element | beschrijving |
| ------- | ----------- |
| df1 | Een variabele die het dataframe van Pandas vertegenwoordigt dat wordt gebruikt om gegevens te lezen en te schrijven. |
| user-token | Uw gebruikerstoken die automatisch wordt opgehaald gebruikend `sys.env("PYDASDK_IMS_USER_TOKEN")`. |
| service-token | Uw servicetoken dat automatisch wordt opgehaald met `sys.env("PYDASDK_IMS_SERVICE_TOKEN")`. |
| ims-org | Uw ims-org-id die automatisch wordt opgehaald met `sys.env("IMS_ORG_ID")`. |
| api-toets | De api-sleutel die automatisch wordt opgehaald met `sys.env("PYDASDK_IMS_CLIENT_ID")`. |

In de onderstaande afbeeldingen worden de belangrijkste verschillen in het laden van gegevens met de [!DNL Spark] 2.3 en [!DNL Spark] 2.4 benadrukt. In dit voorbeeld worden de *Clustering* -startlaptops gebruikt die in [!DNL JupyterLab Launcher].

**[!DNL Spark]([!DNL Spark]2.3 - afgekeurd)**

De [!DNL Spark] ([!DNL Spark] 2,3 - afgekeurd) laptop gebruikt de [!DNL Spark] kernel. De volgende twee cellen tonen een voorbeeld van het laden van de gegevensset met een opgegeven id voor de gegevensset in het datumbereik (2019-3-21, 2019-3-29).

![vonk 2.3 laden](./images/migration/spark-scala/load-2.3.png)

**Scala ([!DNL Spark]2.4)**

De Scala-laptop ([!DNL Spark] 2.4) gebruikt de Scala-kernel die bij de installatie meer waarden vereist, zoals gemarkeerd in de eerste codecel. Daarnaast `var mdata` moeten er meer `option` waarden worden ingevuld. In dit notitieboek, is de eerder vermelde code voor het [initialiseren van SparkSession](#initialize-sparksession-scala) inbegrepen binnen de `var mdata` codecel.

![vonk 2.4 laden](./images/migration/spark-scala/load-2.4.png)

>[!TIP]
>
>In Scala, kunt u gebruiken `sys.env()` om een waarde van binnen te verklaren en terug te keren `option`. Dit elimineert de behoefte om variabelen te bepalen als u weet zij slechts één keer zullen worden gebruikt. In het volgende voorbeeld wordt `val userToken` in het bovenstaande voorbeeld het voorbeeld inline gedeclareerd `option`:
> `.option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))`

## Schrijven naar een gegevensset

Net als bij het [lezen van een gegevensset](#notebook-read-dataset-spark), vereist het schrijven naar een gegevensset extra `option` waarden die in het onderstaande voorbeeld worden beschreven. In Scala, kunt u gebruiken `sys.env("PYDASDK_IMS_USER_TOKEN")` om een waarde te verklaren en terug te keren, elimineert dit de behoefte om variabelen zoals `var userToken`te bepalen. In het Scala voorbeeld hieronder, `sys.env` wordt gebruikt om alle vereiste waarden te bepalen en terug te keren nodig om aan een dataset te schrijven.

**Gebruikt[!DNL Spark]([!DNL Spark]2.3 - afgekeurd) -[!DNL Spark]Kernel**

```scala
import com.adobe.platform.dataset.DataSetOptions

var userToken = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.USER_TOKEN").get
var serviceToken = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.SERVICE_TOKEN").get
var serviceApiKey = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.SERVICE_API_KEY").get

df1.write.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, "310C6D375BA5248F0A494212@AdobeOrg")
  .option(DataSetOptions.userToken, userToken)
  .option(DataSetOptions.serviceToken, serviceToken)
  .option(DataSetOptions.serviceApiKey, serviceApiKey)
  .save("5e68141134492718af974844")
```

**Scala ([!DNL Spark]2.4) gebruiken - Scala Kernel**

```scala
import org.apache.spark.sql.{Dataset, SparkSession}

val spark = SparkSession.builder().master("local").getOrCreate()

df1.write.format("com.adobe.platform.query")
  .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
  .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
  .option("ims-org", sys.env("IMS_ORG_ID"))
  .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| element | beschrijving |
| ------- | ----------- |
| df1 | Een variabele die het dataframe van Pandas vertegenwoordigt dat wordt gebruikt om gegevens te lezen en te schrijven. |
| user-token | Uw gebruikerstoken die automatisch wordt opgehaald gebruikend `sys.env("PYDASDK_IMS_USER_TOKEN")`. |
| service-token | Uw servicetoken dat automatisch wordt opgehaald met `sys.env("PYDASDK_IMS_SERVICE_TOKEN")`. |
| ims-org | Uw ims-org-id die automatisch wordt opgehaald met `sys.env("IMS_ORG_ID")`. |
| api-toets | De api-sleutel die automatisch wordt opgehaald met `sys.env("PYDASDK_IMS_CLIENT_ID")`. |