---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Bronbestanden in een recept plaatsen
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 0%

---


# Bronbestanden in een recept plaatsen

Deze zelfstudie bevat instructies voor het verpakken van de voorbeeldbronbestanden voor de detailhandel in een archiefbestand. U kunt dit bestand gebruiken om een recept in Adobe Experience Platform te maken [!DNL Data Science Workspace] door de workflow voor het importeren van recept in de gebruikersinterface of met de API uit te voeren.

Concepten om te begrijpen:

- **Recipes**: Een recept is de term van Adobe voor een Model specificatie en is een top-level container die een specifiek machine het leren, een kunstmatig intelligentiealgoritme of een samenstel van algoritmen, verwerkingslogica, en configuratie vertegenwoordigt die wordt vereist om een opgeleid model te bouwen en uit te voeren en daardoor helpen specifieke bedrijfsproblemen oplossen.
- **Bronbestanden**: Afzonderlijke bestanden in uw project die de logica voor een recept bevatten.

## Vereisten

- [!DNL Docker](https://docs.docker.com/install/#supported-platforms)
- [!DNL Python 3 and pip](https://docs.conda.io/en/latest/miniconda.html)
- [!DNL Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [!DNL Maven](https://maven.apache.org/install.html)

## Ontvanger maken

Het maken van recept begint met het verpakken van bronbestanden om een archiefbestand te maken. De brondossiers bepalen de machine het leren logica en de algoritmen die worden gebruikt om een specifiek probleem op te lossen bij de hand, en in of [!DNL Python], R, PySpark, of Scala geschreven. Gebouwde archiefbestanden hebben de vorm van een Docker-afbeelding. Nadat het archiefbestand in het pakket is gemaakt, wordt het geïmporteerd [!DNL Data Science Workspace] om een recept te maken [in de gebruikersinterface](./import-packaged-recipe-ui.md) of [met de API](./import-packaged-recipe-api.md).

### Ontwerpmodel gebaseerd op docker {#docker-based-model-authoring}

Met een Docker-afbeelding kan een ontwikkelaar een toepassing verpakken met alle benodigde onderdelen, zoals bibliotheken en andere afhankelijkheden, en deze als één pakket verzenden.

De ingebouwde afbeelding van de Docker wordt geduwd aan het Azure Registratie van de Container gebruikend geloofsbrieven die aan u tijdens de het creatieve werkschema van het recept worden geleverd.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>om uw Azure Container Registry-referenties te verkrijgen. Navigeer in de linkernavigatiekolom naar **[!UICONTROL Workflows]**. Selecteer Recipe **[!UICONTROL importeren]** , gevolgd door **[!UICONTROL Starten]**. Zie de schermafbeelding hieronder ter referentie.

![](../images/models-recipes/package-source-files/import.png)

De pagina *Configureren* wordt geopend. Geef een geschikte *recept-naam* op, bijvoorbeeld &quot;Retail Sales recipe&quot;, en geef desgewenst een beschrijving of documentatie-URL op. Klik op **[!UICONTROL Volgende]** als de bewerking is voltooid.

![](../images/models-recipes/package-source-files/configure.png)

Selecteer de juiste *runtime* en kies een **[!UICONTROL classificatie]** voor *Type*. Uw Azure Container Registry-referenties worden gegenereerd zodra dit is voltooid.

>[!NOTE]
>*Type *is het leerprobleem van de machine waarvoor het recept is ontworpen en wordt na training gebruikt om de trainingsrun op maat te maken of te evalueren.

>[!TIP]
>- Selecteer voor [!DNL Python] recepten de **[!UICONTROL Python]** -runtime.
>- Selecteer voor R-recepten de **[!UICONTROL R]** -runtime.
>- Voor PySpark-recepten selecteert u de **[!UICONTROL PySpark]** -runtime. Een artefacttype dat automatisch wordt gevuld.
>- Selecteer voor Scala-recepten de **[!UICONTROL Spark]** -runtime. Een artefacttype dat automatisch wordt gevuld.


![](../images/models-recipes/package-source-files/docker-creds.png)

Maak een notitie van de waarden voor *Docker Host*, *Gebruikersnaam* en *Wachtwoord*. Deze worden gebruikt om uw [!DNL Docker] afbeelding samen te stellen en te duwen in de hieronder beschreven workflows.

>[!NOTE]
>De bron-URL wordt opgegeven nadat de hieronder beschreven stappen zijn uitgevoerd. Het configuratiebestand wordt uitgelegd in volgende zelfstudies in de [volgende stappen](#next-steps).

### De bronbestanden verpakken

Begin door de steekproefcodebase te verkrijgen die in de de Werkruimte van de Referentie <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">van de Werkruimte van de Gegevens van het</a> Experience Platform wordt gevonden.

- [Python Docker-afbeelding samenstellen](#python-docker)
- [Afbeelding samenstellen of docker](#r-docker)
- [Afbeelding van PySpark Docker maken](#pyspark-docker)
- [Schaaldockerafbeelding (Spark) maken](#scala-docker)

### Docker- [!DNL Python] afbeelding samenstellen {#python-docker}

Als u dit nog niet hebt gedaan, kloont de [!DNL GitHub] opslagplaats op uw lokale systeem met de volgende opdracht:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer naar de map `experience-platform-dsw-reference/recipes/python/retail`. Hier vindt u de scripts `login.sh` en `build.sh` gebruikt u om u aan te melden bij Docker en het [!DNL Python Docker] image te maken. Als u uw geloofsbrieven [van de](#docker-based-model-authoring) Dokker klaar hebt, ga de volgende bevelen in orde in:

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

Kopieer deze URL en ga naar de [volgende stappen](#next-steps).

### R- [!DNL Docker] afbeelding samenstellen {#r-docker}

Als u dit nog niet hebt gedaan, kloont de [!DNL GitHub] opslagplaats op uw lokale systeem met de volgende opdracht:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer naar de map `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` in de gekloonde opslagplaats. Hier, zult u de dossiers vinden `login.sh` en `build.sh` die u aan login aan Docker zult gebruiken en het beeld van Docker van R bouwt. Als u uw geloofsbrieven [van de](#docker-based-model-authoring) Dokker klaar hebt, ga de volgende bevelen in orde in:

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

Kopieer deze URL en ga naar de [volgende stappen](#next-steps).

### Afbeelding van PySpark Docker maken {#pyspark-docker}

Begin met het klonen van de [!DNL GitHub] opslagplaats op uw lokale systeem met de volgende opdracht:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer naar de map `experience-platform-dsw-reference/recipes/pyspark/retail`. De manuscripten `login.sh` en `build.sh` worden gevestigd hier en gebruikt aan login aan Docker en om het beeld van de Docker te bouwen. Als u uw geloofsbrieven [van de](#docker-based-model-authoring) Dokker klaar hebt, ga de volgende bevelen in orde in:

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

Kopieer deze URL en ga naar de [volgende stappen](#next-steps).

### Afbeelding van Scala Docker maken {#scala-docker}

Begin door de [!DNL GitHub] opslagplaats op uw lokale systeem met het volgende bevel in terminal te klonen:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer vervolgens naar de map `experience-platform-dsw-reference/recipes/scala/retail` waar u de scripts `login.sh` en `build.sh`. Deze scripts worden gebruikt om u aan te melden bij Docker en de Docker-afbeelding te maken. Als u uw geloofsbrieven [van het](#docker-based-model-authoring) Docker klaar hebt, ga de volgende bevelen aan eind in orde in:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Wanneer het uitvoeren van het login manuscript, moet u de gastheer van het Docker, gebruikersbenaming, en wachtwoord verstrekken. Tijdens het bouwen, moet u de gastheer van de Dokker en een versietag voor de bouwstijl verstrekken.

Zodra het bouwstijlmanuscript volledig is, wordt u gegeven een van het brondossier van de Docker URL in uw consoleoutput. Voor dit specifieke voorbeeld ziet het er ongeveer als volgt uit:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Kopieer deze URL en ga naar de [volgende stappen](#next-steps).

## Volgende stappen {#next-steps}

Deze zelfstudie ging over het verpakken van bronbestanden naar een ontvanger, de noodzakelijke stap voor het importeren van een Recipe in [!DNL Data Science Workspace]. U moet nu een Docker-afbeelding in het Azure Container-register hebben samen met de bijbehorende afbeelding-URL. U kunt nu beginnen met de zelfstudie over het importeren van een verpakt recept in [!DNL Data Science Workspace]. Selecteer een van de onderstaande koppelingen voor zelfstudie om aan de slag te gaan:

- [Een gecomprimeerde ontvanger importeren in de gebruikersinterface](./import-packaged-recipe-ui.md)
- [Een gecomprimeerde ontvanger importeren met de API](./import-packaged-recipe-api.md)