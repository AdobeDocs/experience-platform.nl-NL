---
keywords: Experience Platform;luma web data;Data Science Workspace;populaire onderwerpen;recepten;demo data;demo web data;luma data
solution: Experience Platform
title: Webschema's en gegevenssets voor Luma's maken
type: Tutorial
description: Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor het Luma-model voor de demo-eigenschappen.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 219305a71c70a5bbec2fad591c166761e3aaa9ee
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Maak de schema&#39;s en gegevenssets van het model Luminantie

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor alle andere zelfstudies van [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] . Zodra volledig, zullen de volgende schema&#39;s en datasets aan u en uw organisatie beschikbaar zijn.

**Schema&#39;s:**

- Luminagegegevensschema
- Score resultatenschema van pop-upmodel

**Datasets:**

- Luminagewebgegevensset
- Gegevensset betreffende de opleiding van het propensatiemodel
- Gegevensset voor het scoren van het propensemodel
- Gegevensset van scores op basis van pop-upmodel

## De middelen downloaden {#assets}

In de volgende zelfstudie wordt een aangepast model voor de koopsterkte van luminantie gebruikt. Alvorens te werk te gaan, [&#x200B; download de vereiste activa &#x200B;](../assets/DSW-course-sample-assets.7z) zip omslag. Deze map bevat:

- De laptop met koopkrachtmodel
- Een notitieboekje dat wordt gebruikt om gegevens aan een opleiding en het scoren dataset (een ondergroep van de Webgegevens van de Luma) in te voeren
- Een demo-JSON-bestand met de webgegevens van 730.000 gebruikers met Luma&#39;s
- Een optioneel Python 3 EDA-notebook (verkennende gegevensanalyse) dat kan worden gebruikt voor het begrijpen van de webgegevens en het webmodel.

>[!NOTE]
>
> U kunt uw eigen schema en gegevens voor om het even welke leerprogramma&#39;s gebruiken. Nochtans, werkt het demomodel dat in de activa wordt verstrekt niet tenzij het de juiste configuratiedossiers en het vereiste dossier heeft verstrekt. Dit model voor demo-eigenschappen is ontworpen voor gebruik met Luma-webgegevens.

### Maak het schema met webinhoud Luma-gegevens en voer de gegevens in

Als u een model wilt maken, moet u een gegevensset in Experience Platform hebben waarmee u uw model kunt trainen en behalen. Het volgende videoleerprogramma van de [&#x200B; cursus van Workspace van de Wetenschap van Gegevens &#x200B;](https://experienceleague.adobe.com/?lang=nl&recommended=ExperiencePlatform-U-1-2021.1.dsw) begeleidt u door het creëren van het schema van de Luma en het opnemen van de gegevens die door het model van de koopkrachtbron worden gebruikt.

>[!VIDEO](https://video.tv.adobe.com/v/3447160?captions=dut)

### De datasets voor trainingsresultaten, scores en scores maken

Als u het recept builder-notebook wilt gebruiken of de API wilt gebruiken om een model op te leiden en te scoren, moet u de dataset(s) en schema(s) opgeven die worden gebruikt voor training/scoring. De volgende videozelfstudie begeleidt u door het instellen van de gegevenssets voor training, scoring en scoring, evenals het schema voor scoringresultaten dat wordt gebruikt in het koopmodel Luma.

>[!VIDEO](https://video.tv.adobe.com/v/3447427?captions=dut)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes de vereiste schema&#39;s en datasets voor het model van de Luminantiedreiging gecreeerd. U bent nu bereid om aan het volgende leerprogramma verder te gaan en het model tot stand te brengen gebruikend het [&#x200B; recept builder notitieboekje &#x200B;](../jupyterlab/create-a-model.md) leerprogramma.

Bovendien kunt u de gegevens verkennen met behulp van de geleverde EDA-laptop (Exploratory Data Analysis). Deze laptop kan worden gebruikt om inzicht te krijgen in de patronen in de Luminagegegevens, de gegevenshygiëne te controleren en een overzicht te geven van de relevante gegevens voor het voorspellende-heimodel. Meer over de Verkennende Analyse van Gegevens leren, bezoek de [&#x200B; documentatie EDA &#x200B;](../jupyterlab/eda-notebook.md).
