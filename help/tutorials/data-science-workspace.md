---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zelfstudies over de werkruimte voor gegevenswetenschap
topic: tutorial
translation-type: tm+mt
source-git-commit: 4d7d61660e6691d77701db1c089b84eee7f60974
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---


# Zelfstudies over de werkruimte voor gegevenswetenschap

De Werkruimte van de Wetenschap van Gegevens van het Adobe Experience Platform gebruikt machine het leren en kunstmatige intelligentie om inzichten van uw gegevens tot stand te brengen. Met de Data Science Workspace, die in Adobe Experience Platform is geïntegreerd, kunt u voorspellingen maken met behulp van uw inhoud en gegevenselementen voor alle Adobe-oplossingen. Gegevenswetenschappers van alle vaardigheidsniveaus hebben geavanceerde, gebruiksvriendelijke hulpmiddelen die snelle ontwikkeling, opleiding, en het stemmen van machine het leren recepten steunen - alle voordelen van AI technologie, zonder de ingewikkeldheid.

Om meer te leren, begin door het overzicht [van de Werkruimte van de Wetenschap van](../data-science-workspace/home.md)Gegevens te lezen.

## API Sensei Machine Learning

De Sensei Machine Learning-API biedt een mechanisme voor gegevenswetenschappers om leerservices voor machines te organiseren en te beheren, van algoritme aan boord tot experimenteren en implementatie van services.

**De volgende API-ontwikkelaarshulplijnen zijn beschikbaar:**
- [De motoren](../data-science-workspace/api/engines.md) - leren hoe te om uw registratie van het Docker op te zoeken, een Motor tot stand te brengen, een motor van de eigenschappijpleiding tot stand te brengen, de informatie voor een Motor terug te winnen, een Motor bij te werken, en een Motor te schrappen.
- [MLInstances (recepten)](../data-science-workspace/api/mlinstances.md) - Leer hoe te om een MLInstance tot stand te brengen, de informatie voor een MLInstance terug te winnen, een MLInstance bij te werken, en een MLInstance te schrappen.
- [Experimenten](../data-science-workspace/api/experiments.md) - Leer hoe u een expert maakt, informatie ophaalt over een expert of een expert op het gebied van experimenten, een experiment bijwerkt en een experiment verwijdert.
- [Modellen](../data-science-workspace/api/models.md) - Leer hoe u uw eigen model registreert, de informatie voor een model ophaalt, een model bijwerkt, een model verwijdert, een nieuwe transcodering voor een model maakt en de details van een getranscodeerd model ophaalt.
- [MLServices](../data-science-workspace/api/mlservices.md) - Leer hoe u een MLService kunt maken, de informatie voor een dienst MLService terugwinnen, een dienst MLService bijwerken, en een dienst MLService schrappen.
- [Inzichten](../data-science-workspace/api/insights.md) - Leer hoe te om de informatie voor een Inzicht terug te winnen, een nieuw ModelInzicht toe te voegen, en een lijst van standaardmetriek voor algoritmen terug te winnen.

Voor meer informatie en de vereiste waarden voor het uitvoeren van CRUD-bewerkingen met de Sensei Machine Learning-API, raadpleegt u de gids [Aan de slag](../data-science-workspace/api/getting-started.md).

## JupyterLab-laptops gebruiken

[!DNL JupyterLab] is een web-based gebruikersinterface voor [!DNL Project Jupyter] en is strak geïntegreerd in Adobe Experience Platform. Het biedt een interactieve ontwikkelomgeving voor gegevenswetenschappers die werken met Jupyter-laptops, -code en -gegevens. Dit document biedt een overzicht van [!DNL JupyterLab] en de bijbehorende functies en instructies voor het uitvoeren van algemene handelingen.

**Deze handleiding helpt u:**
- Heb toegang tot en begrijp de [!DNL JupyterLab] interface.
- Begrijp codecellen en de beschikbare kernels binnen [!DNL JupyterLab].
- Begrijp GPU- en geheugenserverconfiguratie in Python/R.
- Lees en vraag [!DNL Platform] gegevens gebruikend Notities.
- Begrijp de gegevenslimieten voor laptops.

Ga voor meer informatie naar de [JupyterLab-gebruikershandleiding](../data-science-workspace/jupyterlab/overview.md).

## Bronbestanden verpakken voor het schrijven van Docker-recept

Met een Docker-afbeelding kunt u een toepassing verpakken met alle onderdelen die deze nodig heeft. Dit omvat bibliotheken en andere gebiedsdelen allen in één pakket. De ingebouwde afbeelding van de Docker wordt geduwd aan het Azure Registratie van de Container gebruikend geloofsbrieven die aan u tijdens de het creatieve werkschema van het recept worden geleverd.

**Deze zelfstudie helpt u:**
- Download de vereiste voorwaarden voor het maken van het recept.
- Begrijp op docker gebaseerde modelcreatie.
- Bouw een beeld van de Docker voor Python, R, PySpark, of Scala (Vonk).
- Haal een URL voor het bronbestand Docker op.

Voor meer informatie volgt u de bronbestanden van het [pakket in een recept-zelfstudie](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Een recept importeren

>[!NOTE]
>Deze zelfstudie vereist dat u een URL voor het bronbestand Docker hebt. Bezoek de bronbestanden van het [pakket in een recept-zelfstudie](../data-science-workspace/models-recipes/package-source-files-recipe.md) als u geen URL voor het bronbestand Docker hebt.

De zelfstudies over het importrecept bieden inzicht in het configureren en importeren van een verpakt recept. Aan het einde van deze zelfstudie kunt u een model maken, trainen en evalueren in de Adobe Experience Platform Data Science Workspace.

**Deze zelfstudie helpt u:**
- Maak een set configuraties voor een recept.
- Importeer een op docker gebaseerd recept voor Python, R, PySpark of Scala (Spark).

Voor meer informatie volgt u de import van een [UI-zelfstudie](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) voor het verpakken van het recept of de [API-zelfstudie](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Een model trainen en evalueren

In de Werkruimte van de Wetenschap van Gegevens van het Adobe Experience Platform, wordt een machine het leren Model gecreeerd door bestaande Ontvanger op te nemen die voor de intentie van het Model aangewezen is. Het model wordt vervolgens getraind en geëvalueerd om de efficiëntie en werkzaamheid van de werking te optimaliseren door de bijbehorende hyperparameters te verfijnen. Ontvangers zijn herbruikbaar, wat betekent dat er meerdere modellen kunnen worden gemaakt en op specifieke doeleinden kunnen worden afgestemd met één ontvanger.

**Deze zelfstudie helpt u:**
- Maak een nieuw model.
- Maak een trainingsrun voor uw model.
- Evalueer uw modeltrainingsprogramma&#39;s.

Volg om aan de slag te gaan de training en evalueer een model- [API-zelfstudie](../data-science-workspace/models-recipes/train-evaluate-model-api.md) of de [UI-zelfstudie](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Een model optimaliseren met behulp van het raamwerk voor Inzichten in modellen

Het Model Insights Framework biedt de gegevenswetenschapper hulpmiddelen in de Adobe Experience Platform Data Science Workspace om snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten. Het kader zal de snelheid en doeltreffendheid van de werkstroom voor machinaal leren verbeteren en het gebruiksgemak voor gegevenswetenschappers verbeteren. Dit wordt gedaan door een standaardmalplaatje voor elk machine het leren algoritme type te verstrekken om met model het stemmen bij te wonen. Dankzij het eindresultaat kunnen wetenschappers op het gebied van gegevens en burgergegevens betere modeloptimalisatiebeslissingen maken voor hun eindgebruikers.

**Deze zelfstudie helpt u:**
- Conceptcode configureren.
- Definieer aangepaste metriek.
- Gebruik vooraf gebouwde evaluatiemetriek en visualisatiekaarten.

Volg de zelfstudie over het [optimaliseren van een model](../data-science-workspace/models-recipes/optimize-model.md)om aan de slag te gaan.

## Score een model

Scores in de Werkruimte van de Wetenschap van Gegevens van het Adobe Experience Platform kunnen worden bereikt door inputgegevens in een bestaand opgeleid Model te voeren. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij.

**Deze zelfstudie helpt u:**
- Maak een nieuwe scoring-run.
- Bekijk de resultaten van uw scoring.

Volg om aan de slag te gaan de score van een model- [API-zelfstudie](../data-science-workspace/models-recipes/score-model-api.md) of de [UI-zelfstudie](../data-science-workspace/models-recipes/score-model-ui.md).

## Een model publiceren als service

De Werkruimte van de Wetenschap van Gegevens van het Adobe Experience Platform staat u toe om uw Model als dienst te publiceren, toelatend gebruikers binnen uw organisatie IMS om gegevens te scoren zonder de behoefte om hun eigen Modellen te creëren. Dit kan worden gedaan gebruikend het [!DNL Platform] gebruikersinterface of Sensei Machine Leren API.

**Deze zelfstudie helpt u:**
- Publiceer een Model als dienst.
- Score-gegevens die een service via de [!DNL Platform] servicegalerie gebruiken.

Volg om aan de slag te gaan de zelfstudie [van de service-](../data-science-workspace/models-recipes/publish-model-service-api.md) API of de zelfstudie [over de](../data-science-workspace/models-recipes/publish-model-service-ui.md)gebruikersinterface.

## Training en scores voor een model plannen

De Werkruimte van de Wetenschap van de Gegevens van het Adobe Experience Platform staat u aan opstellings geplande het scoren en trainingslooppas op een machine het leren dienst toe. Het automatiseren van het trainings- en scoringsproces kan de efficiëntie van een service helpen behouden en verbeteren door patronen in uw gegevens bij te houden.

**Deze zelfstudie helpt u:**
- Geplande scoring configureren
- Geplande training configureren

Volg de zelfstudie [over](../data-science-workspace/models-recipes/schedule-models-ui.md)een gebruikersmodel om aan de slag te gaan.

## Een functiepijplijn maken

>[!NOTE]
>Functiepijpleidingen zijn momenteel alleen beschikbaar via API.

Met Adobe Experience Platform kunt u aangepaste functiepijpleidingen maken en maken om functies op schaal te engineeren via de Sensei Machine Learning Framework-runtime.

**Deze handleiding helpt u:**
- Implementeer de klassen van de eigenschappijpleiding.
- Creeer een motor van de eigenschappijpleiding gebruikend API.

Meer leren, bezoek het leerprogramma voor het [creëren van een eigenschappijpleiding](../data-science-workspace/authoring/feature-pipeline.md).

## Bouw een Real-Time Machine Learning toepassing (alpha)

Een combinatie naadloze berekening op zowel de Hub als de Rand vermindert dramatisch de latentie die traditioneel betrokken bij het aandrijven van hyper-gepersonaliseerde ervaringen is die zowel relevant als ontvankelijk zijn. Vandaar, het Leren van de machine in real time verstrekt conclusies met ongelooflijk lage latentie voor synchrone besluitvorming. Voorbeelden hiervan zijn het renderen van gepersonaliseerde webpagina-inhoud, het surfen op een aanbieding en kortingen om het aantal kleuren te verminderen en tegelijk de conversie in een webwinkel te verhogen.

**Deze handleiding helpt u:**
- Begrijp de het leren architectuur van de machine in real time.
- Begrijp het Echte werkschema van het Leren van de machine in real time.
- Begrijp de huidige functionaliteit voor het Leren van de machine in real time.
- Verstrek de volgende stappen voor het creëren van uw eigen het Leren model van de machine in real time.

Ga voor meer informatie naar het [Real-time Machine Learning-overzicht](../data-science-workspace/real-time-machine-learning/home.md).