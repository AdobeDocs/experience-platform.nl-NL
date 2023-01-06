---
keywords: Experience Platform;pakket bronbestanden;Data Science Workspace;populaire onderwerpen;Docker;docker-afbeelding
solution: Experience Platform
title: Bronbestanden in een ontvanger verpakken
type: Tutorial
description: Deze zelfstudie bevat instructies voor het verpakken van de voorbeeldbronbestanden voor de detailhandel in een archiefbestand. Deze kan worden gebruikt om een recept te maken in de Adobe Experience Platform Data Science Workspace door de workflow voor het importeren van recept in de gebruikersinterface of met de API uit te voeren.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# Bronbestanden in een recept plaatsen

Deze zelfstudie bevat instructies voor het verpakken van de beschikbare bronbestanden voor de detailhandel in een archiefbestand, waarmee u een recept kunt maken in Adobe Experience Platform [!DNL Data Science Workspace] door de workflow voor het importeren van recept te volgen in de gebruikersinterface of met de API.

Concepten om te begrijpen:

- **Ontvangers**: Een recept is Adobe voor een Model specificatie en is een top-level container die een specifiek machine het leren, kunstmatig intelligentiealgoritme of samenstel van algoritmen, verwerkingslogica, en configuratie vertegenwoordigt die wordt vereist om een opgeleid model te bouwen en uit te voeren en vandaar helpen specifieke bedrijfsproblemen oplossen.
- **Bronbestanden**: Afzonderlijke bestanden in uw project die de logica voor een recept bevatten.

## Vereisten

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Ontvanger maken

Het maken van recept begint met het verpakken van bronbestanden om een archiefbestand te maken. De brondossiers bepalen de machine het leren logica en algoritmen die worden gebruikt om een specifiek probleem op te lossen bij de hand, en in of geschreven [!DNL Python], R, PySpark of Scala. Gebouwde archiefbestanden hebben de vorm van een Docker-afbeelding. Nadat het archiefbestand in het pakket is gemaakt, wordt het geïmporteerd in [!DNL Data Science Workspace] om een recept te maken [in de gebruikersinterface](./import-packaged-recipe-ui.md) of [API gebruiken](./import-packaged-recipe-api.md).

### Ontwerpmodel gebaseerd op docker {#docker-based-model-authoring}

Met een Docker-afbeelding kan een ontwikkelaar een toepassing verpakken met alle benodigde onderdelen, zoals bibliotheken en andere afhankelijkheden, en deze als één pakket verzenden.

De ingebouwde afbeelding van de Docker wordt geduwd aan de Azure Registratie van de Container gebruikend geloofsbrieven die aan u tijdens de het creatieve werkschema van het recept worden geleverd.

U kunt uw aanmeldingsgegevens voor de Azure Container Registry verkrijgen door u aan te melden [Adobe Experience Platform](https://platform.adobe.com). Navigeer in de linkernavigatiekolom naar **[!UICONTROL Workflows]**. Selecteren **[!UICONTROL Import Recipe]** gevolgd door selecteren **[!UICONTROL Launch]**. Zie de schermafbeelding hieronder ter referentie.

![](../images/models-recipes/package-source-files/import.png)

De **[!UICONTROL Configure]** pagina wordt geopend. Verstrek passend **[!UICONTROL Recipe Name]**, bijvoorbeeld &quot;Retail Sales recipe&quot; en eventueel een beschrijving of documentatie-URL opgeven. Klik op **[!UICONTROL Next]**.

![](../images/models-recipes/package-source-files/configure.png)

Selecteer de juiste *Runtime* kiest u vervolgens een **[!UICONTROL Classification]** for *Type*. Uw Azure Container Registry-referenties worden gegenereerd zodra dit is voltooid.

>[!NOTE]
>
>*Type* Dit is de klasse van het probleem van machinaal leren waarvoor het recept is ontworpen en wordt na training gebruikt om de trainingsrun op maat te maken of te evalueren.

>[!TIP]
>
>- Voor [!DNL Python] recepten selecteren de **[!UICONTROL Python]** runtime.
>- Selecteer voor R-recepten de optie **[!UICONTROL R]** runtime.
>- Voor PySpark-recepten selecteert u de optie **[!UICONTROL PySpark]** runtime. Een artefacttype dat automatisch wordt gevuld.
>- Selecteer voor Scala-recepten de optie **[!UICONTROL Spark]** runtime. Een artefacttype dat automatisch wordt gevuld.


![](../images/models-recipes/package-source-files/docker-creds.png)

Noteer de waarden voor Docker-host, gebruikersnaam en wachtwoord. Deze worden gebruikt om uw [!DNL Docker] in de hieronder beschreven workflows.

>[!NOTE]
>
>De bron-URL wordt opgegeven nadat de hieronder beschreven stappen zijn uitgevoerd. Het configuratiebestand wordt uitgelegd in volgende zelfstudies die u vindt in [volgende stappen](#next-steps).

### De bronbestanden verpakken

Begin met het ophalen van de voorbeeldcodebase in het dialoogvenster <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Referentie voor werkruimte Experience Platform Data Science</a> opslagplaats.

- [Python Docker-afbeelding samenstellen](#python-docker)
- [Afbeelding samenstellen of docker](#r-docker)
- [Afbeelding van PySpark Docker maken](#pyspark-docker)
- [Schaaldockerafbeelding (Spark) maken](#scala-docker)

### Opbouwen [!DNL Python] Afbeelding dokken {#python-docker}

Als u dat nog niet hebt gedaan, kloont dan de [!DNL GitHub] opslagplaats op uw lokale systeem met de volgende opdracht:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Ga naar de map `experience-platform-dsw-reference/recipes/python/retail`. Hier vindt u de scripts `login.sh` en `build.sh` gebruikt om zich aan te melden bij Docker en om het [!DNL Python Docker] afbeelding. Als u uw [Aanmeldingsgegevens docken](#docker-based-model-authoring) klaar, ga de volgende bevelen in orde in:

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

### Build R [!DNL Docker] image {#r-docker}

Als u dat nog niet hebt gedaan, kloont dan de [!DNL GitHub] opslagplaats op uw lokale systeem met de volgende opdracht:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Ga naar de map `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` in uw gekloonde opslagplaats. Hier vindt u de bestanden `login.sh` en `build.sh` die u aan login aan Docker zult gebruiken en het beeld van het Docker van R bouwt. Als u uw [Aanmeldingsgegevens docken](#docker-based-model-authoring) klaar, ga de volgende bevelen in orde in:

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

Ga naar de map `experience-platform-dsw-reference/recipes/pyspark/retail`. De scripts `login.sh` en `build.sh` bevinden zich hier en worden gebruikt om u aan te melden bij Docker en om de Docker-afbeelding te maken. Als u uw [Aanmeldingsgegevens docken](#docker-based-model-authoring) klaar, ga de volgende bevelen in orde in:

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

Begin met het klonen van de [!DNL GitHub] opslagplaats op uw lokale systeem met het volgende bevel in terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigeer vervolgens naar de map `experience-platform-dsw-reference/recipes/scala` waar u de manuscripten kunt vinden `login.sh` en `build.sh`. Deze scripts worden gebruikt om u aan te melden bij Docker en de Docker-afbeelding te maken. Als u uw [Aanmeldingsgegevens docken](#docker-based-model-authoring) klaar, ga de volgende bevelen aan eind in orde in:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Als u een machtigingsfout ontvangt bij het aanmelden bij Docker via de `login.sh` script, probeer het met de opdracht `bash login.sh`.

Wanneer het uitvoeren van het login manuscript, moet u de gastheer van het Docker, gebruikersbenaming, en wachtwoord verstrekken. Tijdens het bouwen, moet u de gastheer van de Dokker en een versietag voor de bouwstijl verstrekken.

Zodra het bouwstijlmanuscript volledig is, wordt u gegeven een van het brondossier van de Docker URL in uw consoleoutput. Voor dit specifieke voorbeeld ziet het er ongeveer als volgt uit:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Kopieer deze URL en ga naar de [volgende stappen](#next-steps).

## Volgende stappen {#next-steps}

Deze zelfstudie ging over het verpakken van bronbestanden naar een recept, de noodzakelijke stap voor het importeren van een recept in [!DNL Data Science Workspace]. U moet nu een Docker-afbeelding in het Azure Container-register hebben samen met de bijbehorende afbeelding-URL. U bent nu klaar om de zelfstudie over het importeren van een verpakt recept naar te starten [!DNL Data Science Workspace]. Selecteer een van de onderstaande koppelingen voor zelfstudie om aan de slag te gaan:

- [Een gecomprimeerde ontvanger importeren in de gebruikersinterface](./import-packaged-recipe-ui.md)
- [Een gecomprimeerde ontvanger importeren met de API](./import-packaged-recipe-api.md)
