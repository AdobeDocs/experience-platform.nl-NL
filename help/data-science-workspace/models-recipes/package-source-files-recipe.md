---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Bronbestanden in een recept plaatsen
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# Bronbestanden in een recept plaatsen

Deze zelfstudie bevat instructies voor het verpakken van de voorbeeldbronbestanden voor de detailhandel in een archiefbestand. U kunt dit bestand gebruiken om een recept te maken in de Adobe Experience Platform Data Science Workspace door de workflow voor het importeren van recept in de gebruikersinterface of met de API te volgen.

Concepten om te begrijpen:

- **Recipes**: Een recept is de term van Adobe voor een Model specificatie en is een top-level container die een specifiek machine het leren, een kunstmatig intelligentiealgoritme of een samenstel van algoritmen, verwerkingslogica, en configuratie vertegenwoordigt die wordt vereist om een opgeleid model te bouwen en uit te voeren en daardoor helpen specifieke bedrijfsproblemen oplossen.
- **Bronbestanden**: Afzonderlijke bestanden in uw project die de logica voor een recept bevatten.

## Vereisten

- [Docker](https://docs.docker.com/install/#supported-platforms)
- [Python 3 en pip](https://docs.conda.io/en/latest/miniconda.html)
- [Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [Maven](https://maven.apache.org/install.html)

## Ontvanger maken

Het maken van recept begint met het verpakken van bronbestanden om een archiefbestand te maken. De brondossiers bepalen de machine het leren logica en de algoritmen die worden gebruikt om een specifiek probleem op te lossen bij de hand, en in of Python, R, PySpark, of Scala Spark geschreven. Afhankelijk van de taal waarin de bronbestanden worden geschreven, zijn de ingebouwde archiefbestanden een Docker-afbeelding of een binair bestand. Nadat het archiefbestand in het pakket is gemaakt, wordt het geïmporteerd in de Data Science Workspace om een recept te maken [in de gebruikersinterface](./import-packaged-recipe-ui.md) of [met de API](./import-packaged-recipe-api.md).

### Ontwerpmodel gebaseerd op docker

Met een Docker-afbeelding kan een ontwikkelaar een toepassing verpakken met alle benodigde onderdelen, zoals bibliotheken en andere afhankelijkheden, en deze als één pakket verzenden.

De ingebouwde Docker-afbeelding wordt naar Azure Container Registry geduwd met referenties die aan u worden geleverd tijdens de workflow voor het maken van het recept.

>[!NOTE] Alleen bronbestanden die in **Python**, **R** en **Tensorflow** zijn geschreven, vereisen de Azure Container Registry-referenties.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>om uw Azure Container Registry-referenties te verkrijgen. Navigeer in de linkernavigatiekolom naar **Workflows**. Selecteer Ontvanger **importeren uit bronbestand** en **start** een nieuwe importprocedure. Zie de schermafbeelding hieronder ter referentie.

![](../images/models-recipes/package-source-files/workflow_ss.png)

Geef een geschikte **recept-naam** op, bijvoorbeeld &quot;Retail Sales recipe&quot;, en geef desgewenst een beschrijving of documentatie-URL op. Klik op **Volgende** als de bewerking is voltooid.

![](../images/models-recipes/package-source-files/recipe_info.png)

Selecteer de juiste **runtime** en kies vervolgens **Classificatie** voor **Type**. Uw Azure Container Registry-referenties worden gegenereerd.

![](../images/models-recipes/package-source-files/recipe_workflow_recipe_source.png)

Maak een notitie van de waarden voor **Docker Host**, **Gebruikersnaam** en **Wachtwoord**. Deze worden later gebruikt om uw Docker-afbeelding te maken en te duwen.

Wanneer deze optie is ingeschakeld, hebben u en andere gebruikers toegang tot de afbeelding via URL. In het veld **Bronbestand** wordt deze URL als invoer verwacht.

### Binair model maken

Voor brondossiers die in Scala of PySpark worden geschreven, zal een binair dossier worden geproduceerd. De bouw van het binaire dossier is zo eenvoudig zoals het runnen van het verstrekte bouwstijlmanuscript.
>[!NOTE] Slechts zullen de brondossiers die in ScalaSpark of PySpark worden geschreven een binair dossier op het runnen van het bouwstijlmanuscript produceren.

### De bronbestanden verpakken

Begin door steekproefcodebase te verkrijgen die in de de Verwijzing <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">van de Werkruimte van de Werkruimte van de Gegevens van het Platform van de</a> Ervaring wordt gevonden. Afhankelijk van de programmeertaal waarin de bronbestanden van het voorbeeld worden geschreven, verschilt het samenstellen van het respectievelijke archiefbestand in de procedure.

- [Python Docker-afbeelding samenstellen](#build-python-docker-image)
- [Afbeelding samenstellen of docker](#build-r-docker-image)
- [PySpark-binaire bestanden maken](#build-pyspark-binaries)
- [Scala-binaire bestanden maken](#build-scala-binaries)

#### Python Docker-afbeelding samenstellen

Als u dit nog niet hebt gedaan, kloont u de gegevensopslagruimte van de Glitb op uw lokale systeem met de volgende opdracht:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer naar de map `experience-platform-dsw-reference/recipes/python/retail`. Hier, zult u de manuscripten vinden `login.sh` en `build.sh` die u aan login aan Docker zult gebruiken en het pythonDocker beeld bouwen. Als u uw geloofsbrieven [van de](#docker-based-model-authoring) Dokker klaar hebt, ga de volgende bevelen in orde in:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Merk op dat wanneer het uitvoeren van het login manuscript, u de gastheer van de Docker, gebruikersbenaming, en wachtwoord zult moeten verstrekken. Tijdens het bouwen, moet u de gastheer van de Dokker en een versietag voor de bouwstijl verstrekken.

Zodra het bouwstijlmanuscript volledig is, wordt u gegeven een van het brondossier van de Docker URL in uw consoleoutput. Voor dit specifieke voorbeeld ziet het er ongeveer als volgt uit:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Kopieer deze URL en ga naar de [volgende stappen](#next-steps).

#### Afbeelding samenstellen of docker

Als u dit nog niet hebt gedaan, kloont u de gegevensopslagruimte van de Glitb op uw lokale systeem met de volgende opdracht:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer naar de map `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` in de gekloonde opslagplaats. Hier, zult u de dossiers vinden `login.sh` en `build.sh` die u aan login aan Docker zult gebruiken en het beeld van het Docker van R bouwt. Als u uw geloofsbrieven [van de](#docker-based-model-authoring) Dokker klaar hebt, ga de volgende bevelen in orde in:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Merk op dat wanneer het uitvoeren van het login manuscript, u de gastheer van de Docker, gebruikersbenaming, en wachtwoord zult moeten verstrekken. Tijdens het bouwen, moet u de gastheer van de Dokker en een versietag voor de bouwstijl verstrekken.

Zodra het bouwstijlmanuscript volledig is, wordt u gegeven een van het brondossier van de Docker URL in uw consoleoutput. Voor dit specifieke voorbeeld ziet het er ongeveer als volgt uit:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Kopieer deze URL en ga naar de [volgende stappen](#next-steps).

#### PySpark-binaire bestanden maken

Als u dit nog niet hebt gedaan, kloont u de gegevensopslagruimte van de Glitb op uw lokale systeem met de volgende opdracht:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer naar de gekloonde opslagplaats op uw lokale systeem en voer de volgende opdrachten uit om het vereiste `.egg` bestand te maken voor het importeren van een PySpark-recept:

```BASH
cd recipes/pyspark
./build.sh
```

Het `.egg` bestand wordt in de `dist` map gegenereerd.

U kunt nu verdergaan naar de [volgende stappen](#next-steps).

#### Scala-binaire bestanden maken

Als u dit nog niet hebt gedaan, voert u de volgende opdracht uit om de gegevensopslagruimte van Github naar uw lokale systeem te klonen:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Als u het `.jar` artefact wilt maken dat wordt gebruikt voor het importeren van een Scala-recept, navigeert u naar de gekloonde opslagplaats en volgt u de onderstaande stappen:

```BASH
cd recipes/scala/
./build.sh
```

Het gegenereerde `.jar` artefact met afhankelijkheden vindt u in de `/target` map.

U kunt nu verdergaan naar de [volgende stappen](#next-steps).

## Volgende stappen

Deze zelfstudie ging over het verpakken van bronbestanden naar een recept, de noodzakelijke stap voor het importeren van een recept naar de werkruimte voor wetenschap van gegevens. U moet nu een Docker-afbeelding in het Azure Container-register hebben samen met de bijbehorende URL van de afbeelding of een binair bestand dat lokaal in uw bestandssysteem is opgeslagen. U bent nu klaar om met de zelfstudie te beginnen over het **importeren van een verpakte recept in de werkruimte** van de wetenschap van gegevens. Selecteer een van de onderstaande koppelingen naar zelfstudies om aan de slag te gaan.

- [Een gecomprimeerde ontvanger importeren in de gebruikersinterface](./import-packaged-recipe-ui.md)
- [Een gecomprimeerde ontvanger importeren met de API](./import-packaged-recipe-api.md)