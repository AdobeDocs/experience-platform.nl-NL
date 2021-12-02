---
keywords: Experience Platform;lumawebgegevens;Data Science Workspace;populaire onderwerpen;recepten;demo-gegevens;demo-webgegevens;lumagegevens
solution: Experience Platform
title: Webschema's en gegevenssets voor Luma's maken
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor het Luma-model voor de demo-eigenschappen.
source-git-commit: fd0f6aa2ac73bdc0a5413c437d091df6bb5d38a6
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Maak de schema&#39;s en gegevenssets van het model Luma-propenstiy

Deze zelfstudie biedt u de voorwaarden en elementen die vereist zijn voor alle andere onderdelen [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] zelfstudies. Zodra volledig, zullen de volgende schema&#39;s en datasets aan u en uw organisatie IMS beschikbaar zijn.

**Schema&#39;s:**

- Luminagegegevensschema
- Score resultatenschema van pop-upmodel

**Gegevenssets:**

- Luminagewebgegevensset
- Gegevensset betreffende de opleiding van het propensatiemodel
- Gegevensset voor het scoren van het propensemodel
- Gegevensset van scores op basis van pop-upmodel

## De middelen downloaden {#assets}

In de volgende zelfstudie wordt een aangepast model voor de koopsterkte van luminantie gebruikt. Voordat u verdergaat, [de vereiste middelen downloaden](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip?lang=en) ZIP-map. Deze map bevat:

- De laptop met koopkrachtmodel
- Een notitieboekje dat wordt gebruikt om gegevens aan een opleiding en het scoren dataset (een ondergroep van de Webgegevens van de Luma) in te voeren
- Een demo-JSON-bestand met de webgegevens van 730.000 gebruikers met Luma&#39;s
- Een optioneel Python 3 EDA-notebook (verkennende gegevensanalyse) dat kan worden gebruikt voor het begrijpen van de webgegevens en het webmodel.

>[!NOTE]
>
> U kunt uw eigen schema en gegevens voor om het even welke leerprogramma&#39;s gebruiken. Nochtans, werkt het demomodel dat in de activa wordt verstrekt niet tenzij het de juiste configuratiedossiers en het vereiste dossier heeft verstrekt. Dit model voor demo-eigenschappen is ontworpen voor gebruik met Luma-webgegevens.

### Maak het schema Luminagewebgegevens en voeg de gegevens in

Om een model te creëren, moet u een dataset in Platform hebben die wordt gebruikt om uw model te trainen en te scoren. De volgende videozelfstudie van de [Cursus over wetenschapswerkruimte](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw) begeleidt u door het creëren van het schema van de Luma en het opnemen van de gegevens die door het model van de koopkrachtsverhouding worden gebruikt.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### De datasets voor trainingsresultaten, scores en scores maken

Als u het recept builder-notebook wilt gebruiken of de API wilt gebruiken om een model op te leiden en te scoren, moet u de dataset(s) en schema(s) opgeven die worden gebruikt voor training/scoring. De volgende videozelfstudie begeleidt u door het instellen van de gegevenssets voor training, scoring en scoring, evenals het schema voor scoringresultaten dat wordt gebruikt in het koopmodel Luma.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes de vereiste schema&#39;s en datasets voor het model van de Luminantiedreiging gecreeerd. U bent nu klaar om door te gaan naar de volgende zelfstudie en het model te maken met de [recept builder-notebook](../jupyterlab/create-a-model.md) zelfstudie.

Bovendien kunt u de gegevens verkennen met behulp van de geleverde EDA-laptop (Exploratory Data Analysis). Deze laptop kan worden gebruikt om inzicht te krijgen in de patronen in de Luminagegegevens, de gegevenshygiëne te controleren en een overzicht te geven van de relevante gegevens voor het voorspellende-heimodel. Meer over de Verkennende Analyse van Gegevens leren, bezoek [EDA-documentatie](../jupyterlab/eda-notebook.md).