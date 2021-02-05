---
keywords: Experience Platform;pakket bronbestanden;Data Science Workspace;populaire onderwerpen;Docker;docker-afbeelding
solution: Experience Platform
title: Bronbestanden in een ontvanger verpakken
topic: tutorial
type: Tutorial
description: Deze zelfstudie bevat instructies voor het verpakken van de voorbeeldbronbestanden voor de detailhandel in een archiefbestand. Deze kan worden gebruikt om een recept te maken in de Adobe Experience Platform Data Science Workspace door de workflow voor het importeren van recept in de gebruikersinterface of met de API uit te voeren.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---


# Bronbestanden in een recept plaatsen

Deze zelfstudie bevat instructies voor het verpakken van de voorbeeldbronbestanden voor de detailhandel in een archiefbestand. Deze kunnen worden gebruikt om een recept te maken in Adobe Experience Platform [!DNL Data Science Workspace] door de workflow voor het importeren van recept te volgen in de gebruikersinterface of met de API.

Concepten om te begrijpen:

- **Recipes**: Een recept is Adobe voor een Model specificatie en is een top-level container die een specifiek machine het leren, kunstmatig intelligentiealgoritme of samenstel van algoritmen, verwerkingslogica, en configuratie vertegenwoordigt die wordt vereist om een opgeleid model te bouwen en uit te voeren en vandaar helpen specifieke bedrijfsproblemen oplossen.
- **Bronbestanden**: Afzonderlijke bestanden in uw project die de logica voor een recept bevatten.

## Vereisten

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Ontvanger maken

Het maken van recept begint met het verpakken van bronbestanden om een archiefbestand te maken. De brondossiers bepalen de machine het leren logica en de algoritmen die worden gebruikt om een specifiek probleem op te lossen bij de hand, en in of [!DNL Python], R, PySpark, of Scala geschreven. Gebouwde archiefbestanden hebben de vorm van een Docker-afbeelding. Nadat het archiefbestand in het pakket is gemaakt, wordt het geïmporteerd in [!DNL Data Science Workspace] om een recept [in de UI](./import-packaged-recipe-ui.md) of [te maken met behulp van de API](./import-packaged-recipe-api.md).

### Ontwerpmodel op basis van docker {#docker-based-model-authoring}

Met een Docker-afbeelding kan een ontwikkelaar een toepassing verpakken met alle benodigde onderdelen, zoals bibliotheken en andere afhankelijkheden, en deze als één pakket verzenden.

De ingebouwde afbeelding van de Docker wordt geduwd aan de Azure Registratie van de Container gebruikend geloofsbrieven die aan u tijdens de het creatieve werkschema van het recept worden geleverd.

Als u uw Azure Container Registry-referenties wilt verkrijgen, meldt u zich aan bij [Adobe Experience Platform](https://platform.adobe.com). Navigeer in de linkernavigatiekolom naar **[!UICONTROL Workflows]**. Selecteer **[!UICONTROL Recipe importeren]** gevolgd door **[!UICONTROL Launch]** te selecteren. Zie de schermafbeelding hieronder ter referentie.

![](../images/models-recipes/package-source-files/import.png)

De **[!UICONTROL Configure]** pagina opent. Verstrek aangewezen **[!UICONTROL Naam van recept]**, bijvoorbeeld, &quot;Detailhandel recept van de Verkoop&quot;, en verstrek naar keuze een beschrijving of documentatie URL. Klik op **[!UICONTROL Volgende]** als u klaar bent.

![](../images/models-recipes/package-source-files/configure.png)

Selecteer de juiste *Runtime* en kies vervolgens een **[!UICONTROL Classificatie]** voor *Type*. Uw Azure Container Registry-referenties worden gegenereerd zodra dit is voltooid.

>[!NOTE]
>
>*Het* type is het leerprobleem voor computers waarvoor het recept is ontworpen en wordt na de training gebruikt om de trainingsrun op maat te maken of te evalueren.

>[!TIP]
>
>- Voor [!DNL Python] recepten selecteert u de **[!UICONTROL Python]** runtime.
>- Voor R-recepten selecteert u de **[!UICONTROL R]**-runtime.
>- Voor PySpark-recepten selecteert u de runtime **[!UICONTROL PySpark]**. Een artefacttype dat automatisch wordt gevuld.
>- Voor Scala recipes selecteer **[!UICONTROL Spark]** runtime. Een artefacttype dat automatisch wordt gevuld.


![](../images/models-recipes/package-source-files/docker-creds.png)

Noteer de waarden voor Docker-host, gebruikersnaam en wachtwoord. Deze worden gebruikt om uw [!DNL Docker]-afbeelding te maken en te duwen in de hieronder beschreven workflows.

>[!NOTE]
>
>De bron-URL wordt opgegeven nadat de hieronder beschreven stappen zijn uitgevoerd. Het configuratiedossier wordt verklaard in verdere leerprogramma&#39;s die in [volgende stappen](#next-steps) worden gevonden.

### De bronbestanden verpakken

Begin door steekproefcodebase te verkrijgen die in <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">de Werkruimte van de Werkruimte van de Wetenschap van Gegevens van het Experience Platform wordt gevonden </a> bewaarplaats.

- [Python Docker-afbeelding samenstellen](#python-docker)
- [Afbeelding samenstellen of docker](#r-docker)
- [Afbeelding van PySpark Docker maken](#pyspark-docker)
- [Schaaldockerafbeelding (Spark) maken](#scala-docker)

### [!DNL Python] Dockerafbeelding {#python-docker} samenstellen

Als u dit niet hebt gedaan, kloont de [!DNL GitHub] bewaarplaats op uw lokaal systeem met het volgende bevel:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer naar de map `experience-platform-dsw-reference/recipes/python/retail`. Hier vindt u de scripts `login.sh` en `build.sh` waarmee u zich aanmeldt bij Docker en de [!DNL Python Docker]-afbeelding bouwt. Als u uw [geloofsbrieven van de Dokker](#docker-based-model-authoring) klaar hebt, ga de volgende bevelen in orde in:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Merk op dat wanneer het uitvoeren van het login manuscript, u de gastheer van de Docker, gebruikersbenaming, en wachtwoord moet verstrekken. Tijdens het bouwen, moet u de gastheer van de Dokker en een versietag voor de bouwstijl verstrekken.

Zodra het bouwstijlmanuscript volledig is, wordt u gegeven een van het brondossier van de Docker URL in uw consoleoutput. Voor dit specifieke voorbeeld ziet het er ongeveer als volgt uit:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Kopieer deze URL en ga naar [volgende stappen](#next-steps).

### R [!DNL Docker]-afbeelding {#r-docker} samenstellen

Als u dit niet hebt gedaan, kloont de [!DNL GitHub] bewaarplaats op uw lokaal systeem met het volgende bevel:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer naar de directory `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` in de gekloonde opslagplaats. Hier, zult u de dossiers `login.sh` en `build.sh` vinden die u aan login aan Docker zult gebruiken en het beeld van het Docker van R bouwt. Als u uw [geloofsbrieven van de Dokker](#docker-based-model-authoring) klaar hebt, ga de volgende bevelen in orde in:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Merk op dat wanneer het uitvoeren van het login manuscript, u de gastheer van de Docker, gebruikersbenaming, en wachtwoord moet verstrekken. Tijdens het bouwen, moet u de gastheer van de Dokker en een versietag voor de bouwstijl verstrekken.

Zodra het bouwstijlmanuscript volledig is, wordt u gegeven een van het brondossier van de Docker URL in uw consoleoutput. Voor dit specifieke voorbeeld ziet het er ongeveer als volgt uit:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Kopieer deze URL en ga naar [volgende stappen](#next-steps).

### Afbeelding PySpark Docker maken {#pyspark-docker}

Begin door de [!DNL GitHub] bewaarplaats op uw lokaal systeem met het volgende bevel te klonen:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer naar de map `experience-platform-dsw-reference/recipes/pyspark/retail`. De scripts `login.sh` en `build.sh` bevinden zich hier en worden gebruikt om u aan te melden bij Docker en om de Docker-afbeelding te maken. Als u uw [geloofsbrieven van de Dokker](#docker-based-model-authoring) klaar hebt, ga de volgende bevelen in orde in:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Merk op dat wanneer het uitvoeren van het login manuscript, u de gastheer van de Docker, gebruikersbenaming, en wachtwoord moet verstrekken. Tijdens het bouwen, moet u de gastheer van de Dokker en een versietag voor de bouwstijl verstrekken.

Zodra het bouwstijlmanuscript volledig is, wordt u gegeven een van het brondossier van de Docker URL in uw consoleoutput. Voor dit specifieke voorbeeld ziet het er ongeveer als volgt uit:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Kopieer deze URL en ga naar [volgende stappen](#next-steps).

### Afbeelding voor Scala Docker maken {#scala-docker}

Begin door de [!DNL GitHub] bewaarplaats op uw lokaal systeem met het volgende bevel in terminal te klonen:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer vervolgens naar de map `experience-platform-dsw-reference/recipes/scala` waar u de scripts `login.sh` en `build.sh` kunt vinden. Deze scripts worden gebruikt om u aan te melden bij Docker en de Docker-afbeelding te maken. Als u uw [geloofsbrieven van de Dokker](#docker-based-model-authoring) klaar hebt, ga de volgende bevelen aan eind in orde in:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Als u een toestemmingsfout ontvangt wanneer het proberen om aan Docker aan te melden gebruikend het `login.sh` manuscript, probeer gebruikend het bevel `bash login.sh`.

Wanneer het uitvoeren van het login manuscript, moet u de gastheer van het Docker, gebruikersbenaming, en wachtwoord verstrekken. Tijdens het bouwen, moet u de gastheer van de Dokker en een versietag voor de bouwstijl verstrekken.

Zodra het bouwstijlmanuscript volledig is, wordt u gegeven een van het brondossier van de Docker URL in uw consoleoutput. Voor dit specifieke voorbeeld ziet het er ongeveer als volgt uit:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Kopieer deze URL en ga naar [volgende stappen](#next-steps).

## Volgende stappen {#next-steps}

Deze zelfstudie ging over het verpakken van bronbestanden naar een recept, de noodzakelijke stap voor het importeren van een recept naar [!DNL Data Science Workspace]. U moet nu een Docker-afbeelding in het Azure Container-register hebben samen met de bijbehorende afbeelding-URL. U bent nu klaar om met de zelfstudie te beginnen over het importeren van een verpakt recept in [!DNL Data Science Workspace]. Selecteer een van de onderstaande koppelingen voor zelfstudie om aan de slag te gaan:

- [Een gecomprimeerde ontvanger importeren in de gebruikersinterface](./import-packaged-recipe-ui.md)
- [Een gecomprimeerde ontvanger importeren met de API](./import-packaged-recipe-api.md)