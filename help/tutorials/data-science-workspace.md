---
keywords: Experience Platform;thuis;populaire onderwerpen;dsw;DSW
solution: Experience Platform
title: Zelfstudies over de werkruimte voor gegevenswetenschap
topic: tutorial
type: Tutorial
description: De Adobe Experience Platform Data Science Workspace maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten van uw gegevens te creëren. De Data Science Workspace is geïntegreerd in Adobe Experience Platform en helpt u om voorspellingen te maken met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---


# [!DNL Data Science Workspace]-tutorials

Adobe Experience Platform [!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten van uw gegevens te creëren. [!DNL Data Science Workspace] is geïntegreerd in Adobe Experience Platform en helpt u om voorspellingen te maken met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen. Gegevenswetenschappers van alle vaardigheidsniveaus hebben geavanceerde, gebruiksvriendelijke hulpmiddelen die snelle ontwikkeling, opleiding, en het stemmen van machine het leren recepten steunen - alle voordelen van AI technologie, zonder de ingewikkeldheid.

Om meer te leren, begin door [Overzicht van de Werkruimte van de Wetenschap van Gegevens te lezen](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

De [!DNL Sensei Machine Learning] API biedt een mechanisme voor gegevenswetenschappers om services voor machinaal leren te organiseren en te beheren, van algoritme aan boord tot experimenteren en implementatie van services.

**De volgende API-ontwikkelaarshulplijnen zijn beschikbaar:**
- [De motoren](../data-science-workspace/api/engines.md)  - leren hoe te om uw  [!DNL Docker] registratie op te zoeken, een Motor tot stand te brengen, een motor van de eigenschappijpleiding tot stand te brengen, de informatie voor een Motor terug te winnen, een Motor bij te werken, en een Motor te schrappen.
- [MLInstances (recepten)](../data-science-workspace/api/mlinstances.md)  - Leer hoe te om een MLInstance tot stand te brengen, de informatie voor een MLInstance terug te winnen, een MLInstance bij te werken, en een MLInstance te schrappen.
- [Experimenten](../data-science-workspace/api/experiments.md)  - Leer hoe u een experiment maakt, informatie ophaalt over een expert of een expert op het gebied van experimenten, een experiment bijwerkt en een experiment verwijdert.
- [Modellen](../data-science-workspace/api/models.md)  - Leer hoe u uw eigen model registreert, de informatie voor een model ophaalt, een model bijwerkt, een model verwijdert, een nieuwe transcodering voor een model maakt en de details van een getranscodeerd model ophaalt.
- [MLServices](../data-science-workspace/api/mlservices.md)  - Leer hoe u een MLService kunt maken, de informatie voor een dienst MLService kunt ophalen, een dienst MLService kunt bijwerken en een dienst MLService kunt verwijderen.
- [Inzichten](../data-science-workspace/api/insights.md)  - Leer hoe te om de informatie voor een Inzicht terug te winnen, een nieuw ModelInzicht toe te voegen, en een lijst van standaardmetriek voor algoritmen terug te winnen.

Als u meer wilt leren en de vereiste waarden voor het uitvoeren van CRUD-bewerkingen met de API voor leren van de Sensei-machine wilt opvragen, gaat u naar [Aan de slag-handleiding](../data-science-workspace/api/getting-started.md).

## Hoe te om [!DNL JupyterLab] Notitieboekjes te gebruiken

[!DNL JupyterLab] is een webgebaseerde gebruikersinterface voor  [!DNL Project Jupyter] en is nauw geïntegreerd in Adobe Experience Platform. Het verstrekt een interactieve ontwikkelomgeving voor gegevenswetenschappers om met [!DNL Jupyter Notebooks], code, en gegevens te werken. Dit document biedt een overzicht van [!DNL JupyterLab] en de bijbehorende functies, evenals instructies om algemene handelingen uit te voeren.

**Deze handleiding helpt u:**
- Heb toegang tot en begrijp de [!DNL JupyterLab] interface.
- Begrijp codecellen en de beschikbare kernels binnen [!DNL JupyterLab].
- Begrijp GPU- en geheugenserverconfiguratie in [!DNL Python]/R.

Voor meer informatie raadpleegt u de [JupyterLab-gebruikershandleiding](../data-science-workspace/jupyterlab/overview.md).

## Toegang tot gegevens in JupyterLab-laptops

JupyterLab in de Werkruimte van de Wetenschap van Gegevens steunt laptops voor [!DNL Python], R, PySpark, en Scala. Elke ondersteunde kernel biedt ingebouwde functies waarmee u gegevens van een Platform in een notitieboekje kunt lezen. Ondersteuning voor paginering van gegevens is echter beperkt tot [!DNL Python]- en R-laptops. Deze handleiding is gericht op het gebruik van JupyterLab-laptops voor toegang tot uw gegevens.

**Deze handleiding helpt u:**
- Lees, schrijf, en vraag de gegevens van het Platform gebruikend de laptops van Python, R, PySpark, of Scala.
- Begrijp de leesbeperkingen van elk type laptop.

Voor meer informatie raadpleegt u de [JupyterLab-handleiding voor toegang tot gegevens van laptops](../data-science-workspace/jupyterlab/access-notebook-data.md)

## Bronbestanden verpakken voor het maken van [!DNL Docker] recept

Met een [!DNL Docker]-afbeelding kunt u een toepassing verpakken met alle onderdelen die deze nodig heeft. Dit omvat bibliotheken en andere gebiedsdelen allen in één pakket. De ingebouwde [!DNL Docker]-afbeelding wordt naar [!DNL Azure Container Registry] geduwd met behulp van referenties die u worden verschaft tijdens de workflow voor het maken van het recept.

**Deze zelfstudie helpt u:**
- Download de vereiste voorwaarden voor het maken van het recept.
- Op [!DNL Docker] gebaseerde ontwerpmethoden begrijpen.
- Maak een [!DNL Docker]-afbeelding voor [!DNL Python], R, PySpark of Scala ([!DNL Spark]).
- Verkrijg een [!DNL Docker] bron dossier URL.

Voor meer informatie volgt u de [bronbestanden in een recept-zelfstudie](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Een recept importeren

>[!NOTE]
>
>Deze zelfstudie vereist dat u een URL voor het bronbestand [!DNL Docker] hebt. Bezoek de [pakketbronbestanden in een recept-zelfstudie](../data-science-workspace/models-recipes/package-source-files-recipe.md) als u geen [!DNL Docker]-URL voor bronbestand hebt.

De zelfstudies over het importrecept bieden inzicht in het configureren en importeren van een verpakt recept. Aan het einde van deze zelfstudie kunt u een model maken, trainen en evalueren in Adobe Experience Platform [!DNL Data Science Workspace].

**Deze zelfstudie helpt u:**
- Maak een set configuraties voor een recept.
- Importeer een op [!DNL Docker] gebaseerd recept voor [!DNL Python], R, PySpark, of Scala ([!DNL Spark]).

Voor meer informatie volgt u het importeren van een verpakt recept [UI-zelfstudie](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) of de [API-zelfstudie](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Een model trainen en evalueren

In Adobe Experience Platform [!DNL Data Science Workspace] wordt een model voor machinaal leren gemaakt door een bestaande ontvanger op te nemen die geschikt is voor de intentie van het model. Het model wordt vervolgens getraind en geëvalueerd om de efficiëntie en werkzaamheid van de werking te optimaliseren door de bijbehorende hyperparameters te verfijnen. Ontvangers zijn herbruikbaar, wat betekent dat er meerdere modellen kunnen worden gemaakt en op specifieke doeleinden kunnen worden afgestemd met één ontvanger.

**Deze zelfstudie helpt u:**
- Maak een nieuw model.
- Maak een trainingsrun voor uw model.
- Evalueer uw modeltrainingsprogramma&#39;s.

Om aan de slag te gaan, volgt u de training en evalueert u een model [API-zelfstudie](../data-science-workspace/models-recipes/train-evaluate-model-api.md) of de [UI-zelfstudie](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Een model optimaliseren met behulp van het raamwerk voor Inzichten in modellen

Het Model Insights Framework biedt de gegevenswetenschapper in Adobe Experience Platform tools om snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten. [!DNL Data Science Workspace] Het kader zal de snelheid en doeltreffendheid van de werkstroom voor machinaal leren verbeteren en het gebruiksgemak voor gegevenswetenschappers verbeteren. Dit wordt gedaan door een standaardmalplaatje voor elk machine het leren algoritme type te verstrekken om met model het stemmen bij te wonen. Dankzij het eindresultaat kunnen wetenschappers op het gebied van gegevens en burgergegevens betere modeloptimalisatiebeslissingen maken voor hun eindgebruikers.

**Deze zelfstudie helpt u:**
- Conceptcode configureren.
- Definieer aangepaste metriek.
- Gebruik vooraf gebouwde evaluatiemetriek en visualisatiekaarten.

Volg de zelfstudie om aan de slag te gaan op [het optimaliseren van een model](../data-science-workspace/models-recipes/optimize-model.md).

## Score een model

Scores in Adobe Experience Platform [!DNL Data Science Workspace] kunnen worden bereikt door inputgegevens in een bestaand getraind Model in te voeren. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij.

**Deze zelfstudie helpt u:**
- Maak een nieuwe scoring-run.
- Bekijk de resultaten van uw scoring.

Om aan de slag te gaan, volgt u de score van een model [API-zelfstudie](../data-science-workspace/models-recipes/score-model-api.md) of de [UI-zelfstudie](../data-science-workspace/models-recipes/score-model-ui.md).

## Een model publiceren als service

Met Adobe Experience Platform [!DNL Data Science Workspace] kunt u uw model publiceren als service, zodat gebruikers binnen uw IMS-organisatie gegevens kunnen scoren zonder dat ze hun eigen modellen hoeven te maken. Dit kan worden gedaan gebruikend [!DNL Platform] gebruikersinterface of [!DNL Sensei Machine Learning] API.

**Deze zelfstudie helpt u:**
- Publiceer een Model als dienst.
- Score data using a service via [!DNL Platform] [!UICONTROL Service Gallery].

Volg om aan de slag te gaan de publicatie van een model als service [API-zelfstudie](../data-science-workspace/models-recipes/publish-model-service-api.md) of de [UI-zelfstudie](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## Training en scores voor een model plannen

Met Adobe Experience Platform [!DNL Data Science Workspace] kunt u geplande scoring- en trainingssessies instellen voor een computerleerservice. Het automatiseren van het trainings- en scoringsproces kan de efficiëntie van een service helpen behouden en verbeteren door patronen in uw gegevens bij te houden.

**Deze zelfstudie helpt u:**
- Geplande scoring configureren
- Geplande training configureren

Om te beginnen, volg [planning een modelleerprogramma UI](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Een functiepijplijn maken

>[!NOTE]
>
>Functiepijpleidingen zijn momenteel alleen beschikbaar via API.

Met Adobe Experience Platform kunt u aangepaste functiepijpleidingen maken en maken om op schaal functionaliteit te engineeren via de [!DNL Sensei Machine Learning Framework Runtime].

**Deze handleiding helpt u:**
- Implementeer de klassen van de eigenschappijpleiding.
- Creeer een motor van de eigenschappijpleiding gebruikend API.

Meer leren, bezoek het leerprogramma voor [het creëren van een eigenschappijpleiding](../data-science-workspace/authoring/feature-pipeline.md).

## Een [!DNL Real-Time Machine Learning]-toepassing (alfa) maken

Een combinatie naadloze berekening op zowel de Hub als [!DNL Edge] vermindert dramatisch de latentie die traditioneel betrokken bij het aandrijven van hyper-gepersonaliseerde ervaringen is die zowel relevant als ontvankelijk zijn. Daarom biedt [!DNL Real-time Machine Learning] conclusies met een ongelooflijk lage latentie voor synchrone besluitvorming. Voorbeelden hiervan zijn het renderen van gepersonaliseerde webpagina-inhoud, het surfen op een aanbieding en kortingen om het aantal kleuren te verminderen en tegelijk de conversie in een webwinkel te verhogen.

**Deze handleiding helpt u:**
- Begrijp de [!DNL Real-time Machine Learning] architectuur.
- Begrijp het [!DNL Real-time Machine Learning] werkschema.
- Begrijp de huidige functionaliteit voor [!DNL Real-time Machine Learning].
- Geef de volgende stappen op voor het maken van uw eigen [!DNL Real-time Machine Learning model].

Voor meer informatie gaat u naar [Real-time Machine Learning overview](../data-science-workspace/real-time-machine-learning/home.md).