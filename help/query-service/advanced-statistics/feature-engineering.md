---
title: SQL-extensie met functies Engineering
description: Meer informatie over de Distiller-functie voor gegevens vindt u in SQL-extensie voor het vooraf verwerken van gegevens voor geavanceerde statistische modellering. Het behandelt de beschikbare eigenschappen extractie, transformatie, en selectietechnieken.
role: Developer
exl-id: 622c8ef3-9651-46b3-ad22-021a93190149
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---

# Functietechniek SQL-extensie

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die de Data Distiller-add hebben aangeschaft. Neem voor meer informatie contact op met uw Adobe-vertegenwoordiger.

Om aan uw eigenschaptechnische behoeften te voldoen, gebruik de SQL transformatoruitbreiding om uw gegevens te vereenvoudigen en te automatiseren preprocessing. Gebruik deze extensie om functies te bouwen en probleemloos te experimenteren met verschillende technieken voor functietechnieken, waaronder het koppelen van deze eigenschappen aan modellen. Ontworpen voor gedistribueerde gegevensverwerking, kunt u eigenschapengineering op grote datasets op een parallelle en scalable manier uitvoeren, beduidend verminderend de tijd die voor gegevens wordt vereist preprocessing met de de eigenschapengineering SQL van Distiller van Gegevens uitbreiding.

## Overzicht van technieken {#technique-overview}

De mogelijkheden voor functietechniek bestrijken drie hoofdgebieden: de Extractie van functies, de Transformatie van functies en de Selectie van functies. Elk gebied bevat specifieke functies die zijn ontworpen voor het ophalen, omzetten, scherpstellen en verbeteren van de gegevensvoorbewerking.

### Functie extraheren {#feature-extraction}

Haal relevante informatie uit uw gegevens, vooral tekstgegevens, en zet het in een numeriek formaat om dat de gesteunde modellen kunnen verbruiken of omzetten en datasets afleiden. Gebruik de volgende functies om functie-extractie uit te voeren:

- **[Textual Transformer](./feature-transformation.md#textual-transformations)**: Zet tekstuele gegevens in numerieke eigenschappen om.
- **[Vectorizer van de Telling](./feature-transformation.md#countvectorizer)**: Transformeer een inzameling van tekstdocumenten in vectoren van symbolische tellingen.
- **[n-gram](./feature-transformation.md#ngram)**: produceer opeenvolgingen van n-grammen van tekstgegevens.
- **[Woorden van het Einde verwijderen](./feature-transformation.md#stopwordsremover)**: Filter gemeenschappelijke woorden uit die geen significante betekenis hebben.
- **[TF-IDF](./feature-transformation.md#tf-idf)**: Meet het belang van woorden in een document met betrekking tot een corpus.
- **[Tokenizer](./feature-transformation.md#tokenizer)**: Breek onderaan tekst in individuele termijnen (woorden).
- **[Word2Vec](./feature-transformation.md#word2vec)**: De woorden van de kaart aan vaste - groottevectoren en leiden woordinbedingen.

### Eigenschaptransformatie {#feature-transformation}

Naast het extraheren van eigenschappen, gebruik de volgende algemene transformatoren om uw eigenschappen voor geavanceerde statistische modellen en afgeleide datasets voor te bereiden. Pas schalen, normaliseren of coderen toe om ervoor te zorgen dat de functies op dezelfde schaal worden uitgevoerd en een vergelijkbare distributie hebben.

#### Algemene transformatoren

Hieronder vindt u een lijst met gereedschappen voor het verwerken van een groot aantal gegevenstypen om de workflow voor het voorbewerken van gegevens te verbeteren.

- **[Numerieke Imputer](./feature-transformation.md#numeric-imputer)**: Vul ontbrekende waarden in numerieke kolommen met een gespecificeerde waarde, zoals het gemiddelde of mediaan.
- **[Imputer van het Koord](./feature-transformation.md#string-imputer)**: Vervang ontbrekende koordwaarden met een gespecificeerde waarde, zoals het meest frequente koord in de kolom.
- **[VectorAssembler](./feature-transformation.md#vector-assembler)**: Combineer veelvoudige kolommen in één enkele vectorkolom om gegevens voor machine het leren modellen voor te bereiden.
- **[Imputer Van Boole](./feature-transformation.md#boolean-imputer)**: Vul ontbrekende booleaanse waarden met een gespecificeerde waarde, zoals `true` of `false`.

#### Numerieke transformatoren

Pas deze technieken toe om numerieke gegevens effectief te verwerken en te schalen voor verbeterde modelprestaties.

- **[Binarizer](./feature-transformation.md#binarizer)**: Zet ononderbroken eigenschappen in binaire waarden om die op een drempel worden gebaseerd.
- **[Bucketizer](./feature-transformation.md#bucketizer)**: De ononderbroken eigenschappen van de kaart in discrete emmers.
- **[Min-Max Scaler](./feature-transformation.md#minmaxscaler)**: De eigenschappen van het opnieuw schalen aan een gespecificeerde waaier, typisch [ 0, 1 ].
- **[Max Abs Scaler](./feature-transformation.md#maxabsscaler)**: De eigenschappen van Rescale aan waaier [ - 1, 1 ] zonder onveranderlijke flexibiliteit.
- **[Normalizer](./feature-transformation.md#normalizer)**: Normaliseer vectoren om eenheidsnorm te hebben.
- **[Kwandige Discretizer](./feature-transformation.md#quantilediscretizer)**: Zet ononderbroken eigenschappen in categoriale eigenschappen door hen in hoeveelheden te binden.
- **[Standaard Scaler](./feature-transformation.md#standardscaler)**: Normaliseer eigenschappen om een eenheidsstandaardafwijking en/of nul gemiddelde te hebben.

#### Categorische transformatoren

Gebruik deze transformatoren om categoriale gegevens om te zetten en te coderen in indelingen die geschikt zijn voor modellen voor machinaal leren.

- **[Indexer van het Koord](./feature-transformation.md#stringindexer)**: Zet categoriale koordgegevens in numerieke indexen om.
- **[Één Hete Codeur](./feature-transformation.md#onehotencoder)**: De categoriale gegevens van de kaart in binaire vectoren.

### Functie selecteren {#feature-selection}

Selecteer vervolgens een subset met de belangrijkste functies uit de oorspronkelijke set. Dit proces helpt de afmeting van uw gegevens te verminderen, waardoor het voor uw modellen gemakkelijker wordt om te verwerken en algemene modelprestaties te verbeteren.

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## De OPTIONS-clausule implementeren {#options-clause}

Wanneer u uw model definieert, gebruikt u de component `OPTIONS` om het algoritme en de bijbehorende parameters op te geven. Stel eerst de parameter `type` in om het algoritme aan te geven dat u gebruikt, zoals `K-Means` . Vervolgens definieert u de relevante parameters in de `OPTIONS` -component als sleutel-waardeparen om uw model te perfectioneren. Als u ervoor kiest om bepaalde parameters niet aan te passen, past het systeem standaardinstellingen toe. Raadpleeg de relevante documentatie voor een beter begrip van de functie en standaardwaarden van elke parameter.

### Volgende stappen

Na het leren van de technieken van de eigenschaptechniek die in dit document worden geschetst, vooruitgang op het [&#x200B; Modellen &#x200B;](./models.md) document. Het begeleidt u door het proces van het creëren, de opleiding, en het beheren van vertrouwde modellen gebruikend de eigenschappen u hebt ontworpen. Zodra uw modellen worden gebouwd, ga aan [&#x200B; te werk voert geavanceerde statistische modellendocument uit.](./implement-models/implement-models.md). Dit document fungeert als een overzicht, dat is gekoppeld aan diepgaande hulplijnen voor verschillende modelleringstechnieken, waaronder clustering, classificatie en regressie. Door deze documenten te volgen, leert u om diverse vertrouwde modellen binnen uw SQL werkschema&#39;s te vormen en uit te voeren en uw modellen voor geavanceerde gegevensanalyse te optimaliseren.
