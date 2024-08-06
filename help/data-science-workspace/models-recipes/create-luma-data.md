---
keywords: Experience Platform;lumawebgegevens;Data Science Workspace;populaire onderwerpen;recepten;demo-gegevens;demo-webgegevens;lumagegevens
solution: Experience Platform
title: Webschema's en gegevenssets voor Luma's maken
type: Tutorial
description: Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor het Luma-model voor de demo-eigenschappen.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Maak de schema&#39;s en gegevenssets voor het waarschijnlijkheidsmodel Luma

>[!NOTE]
>
>Data Science Workspace is niet meer verkrijgbaar.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten voor Data Science Workspace.

Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor alle andere [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] -zelfstudies. Zodra volledig, zullen de volgende schema&#39;s en de datasets voor u en uw organisatie beschikbaar zijn.

**Schema&#39;s:**

- Luma-webgegevensschema
- Score resultaatschema van eigenschappenmodel

**Datasets:**

- Luminagewebgegevensset
- Gegevensset betreffende de opleiding van het propensatiemodel
- Gegevensset met scores op basis van eigenschapmodel
- Gegevensset van de resultaten van scores voor het betrouwbaarheidsmodel

## Download de middelen {#assets}

De volgende zelfstudie gebruikt een aangepast waarschijnlijkheidsmodel voor aanschaf Luma. Alvorens te werk te gaan, [ download de vereiste activa ](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) zip omslag. Deze map bevat:

- De aanschafneigheidsmodellaptop
- Een notebook dat wordt gebruikt om gegevens in te voegen in een trainings- en scoregegevensset (een subset van de Luma-webgegevens)
- Een demo-JSON-bestand met de webgegevens van 730.000 Luma-gebruikers
- Een optioneel Python 3 EDA-notebook (verkennende gegevensanalyse) dat kan worden gebruikt voor het begrijpen van de webgegevens en het webmodel.

>[!NOTE]
>
> U kunt uw eigen schema en gegevens voor om het even welke leerprogramma&#39;s gebruiken. Nochtans, werkt het demomodel dat in de activa wordt verstrekt niet tenzij het de juiste configuratiedossiers en het vereiste dossier heeft verstrekt. Dit model voor demo-eigenschappen is ontworpen voor gebruik met Luma-webgegevens.

### Maak het webgegevensschema Luma en voeg de gegevens in

Als u een model wilt maken, moet u beschikken over een dataset in Platform waarmee u uw model kunt trainen en scoren. De volgende videoleerprogramma van de [ cursus van de Werkruimte van de Wetenschap van Gegevens ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) loopt u door het creëren van het schema van de Luma en het opnemen van de gegevens die door het model van de koopkracht worden gebruikt.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Maak de datasets voor training, scores en scores voor resultaten

Als u het recept builder-notebook wilt gebruiken of de API wilt gebruiken om een model op te leiden en te scoren, moet u de gegevenssets en schema&#39;s opgeven die worden gebruikt voor training/scores. In de volgende videozelfstudie worden de gegevenssets met trainingsresultaten, scores en scores weergegeven, evenals het schema voor scores dat wordt gebruikt in het aanschafmodel Luma.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u de vereiste schema&#39;s en gegevenssets voor het waarschijnlijkheidsmodel Luma gemaakt. U bent nu bereid om aan het volgende leerprogramma verder te gaan en het model tot stand te brengen gebruikend het [ recept builder notitieboekje ](../jupyterlab/create-a-model.md) leerprogramma.

Bovendien kunt u de gegevens verkennen met behulp van de geleverde EDA-laptop (Exploratory Data Analysis). Deze laptop kan worden gebruikt om inzicht te krijgen in de patronen in de Luminagegegevens, de gegevenshygiëne te controleren en een overzicht te geven van de relevante gegevens voor het voorspellende-heimodel. Meer over de Verkennende Analyse van Gegevens leren, bezoek de [ documentatie EDA ](../jupyterlab/eda-notebook.md).
