---
title: AI Assistant Natural Language naar SQL Model Details
description: Meer informatie over het AI Assistant Natural Language-model van SQL.
hide: true
hidefromtoc: true
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: a8cc7c6f202cdd2786a69e548810b3957d69fdb3
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# AI Assistant Operational Insights Natural Language to SQL Model Details

## Modeloverzicht {#model-overview}

* **Modelnaam en versie**: De Operationele Taal van de Inzichten van Adobe Experience Platform AI van de Medewerking van Inzichten aan SQL Model ([!DNL NL2SQL]).
* **Model versiedatum**: Februari 2025
* **Model doel**: Het model wordt ontworpen om klanten&#39; natuurlijke taalvragen over operationele inzichten in SQL vragen te vertalen. Deze SQL-query&#39;s worden uitgevoerd in de Adobe Experience Platform-kennisgrafiek, die metagegevens bevat over de Experience Platform-entiteiten van de klant, zoals schema&#39;s, datasets, publiek, bestemmingen en reizen. De resultaten van de SQL vragen worden dan gebruikt om reacties op de originele natuurlijke taalvragen van de klanten te produceren.
* **Beoogde gebruikers**: De primaire gebruikers van dit model zijn marketing beroeps, gegevensanalisten, of klant reis manager-die probeert om operationele inzichten binnen Experience Platform te begrijpen en op te treden gebruikend natuurlijke taal. Ze zijn mogelijk geen experts in SQL- of gegevenstechniek, maar hebben snelle, nauwkeurige antwoorden nodig over hun Experience Platform-entiteiten om geïnformeerde beslissingen te nemen en de ervaringen van klanten te optimaliseren.
* **gevallen van het Gebruik**: Dit model helpt gebruikers tot meta-gegevens over hun entiteiten van Experience Platform zoals publiek, reizen, schema&#39;s, attributen, datasets, en bestemmingen toegang hebben. De gebruikers kunnen vragen in natuurlijke taal-als stellen welk publiek wordt geactiveerd of welk publiek een specifiek schema-gebruikt en het model vertaalt deze in SQL vragen over de de kennisgrafiek van Experience Platform. Dit laat gebruikers toe om operationele zicht snel te bereiken en geïnformeerde besluiten te nemen zonder het moeten het systeem manueel onderzoeken of vragen.
* **Punten van het Pijn**: Dit model richt zeer belangrijke pijnpunten die door bedrijfsgebruikers en analisten worden geconfronteerd die met Experience Platform werken, zoals de ingewikkeldheid van het navigeren van grote volumes van onderling verbonden meta-gegevens, de behoefte om SQL vragen manueel te schrijven om operationele inzichten terug te winnen, en het gebrek aan zicht in hoe de entiteiten van Experience Platform zoals publiek, datasets, en reizen worden verbonden of presteren. Door natuurlijke taaltoegang tot meta-gegevens toe te laten en SQL generatie te automatiseren, vermindert het model afhankelijkheid van technische middelen, verkort insight ontdekkingstijd, en machtigt gebruikers om snellere, data-gedreven besluiten te nemen.

## Modeldetails {#model-details}

* **Model type**: Herinnering LLM met het Dynamische In-Context Leren
* **Input**: De vragen van de natuurlijke taal van de gebruiker.
* **Output**: De modeloutput SQL vragen in [!DNL Snowflake] syntaxis, die over de kennisgrafiek van Experience Platform zal worden uitgevoerd.

**input van het Voorbeeld**

```console
How many datasets were created within the last 10 days?
```

**output van het Voorbeeld**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## Modelevaluatie {#model-evaluation}

* **de metriek en de procedures van de Evaluatie**: Het model wordt geëvalueerd gebruikend nauwkeurigheid. Bijvoorbeeld, van alle [!DNL NL2SQL] verzoeken, hoeveel van de verzoeken de correcte SQL resultaten opleveren. Het evaluatieproces is een combinatie op regel-gebaseerde aanpassing (SQL normalisatie en dan directe SQL koordaanpassing), op LLM-Gebaseerde SQL solver, en menselijke evaluatie.
* **gegevens van de Evaluatie en preprocessing**: Wij gebruiken open reeks(s) voor regressietest en wij hebben ook wekelijkse annotatieprojecten om de prestaties van het model door bemonsterd echt klantenverkeer te controleren.

## Modelimplementatie {#model-deployment}

* **Model controle**: Het basismodel wordt ontvangen door [!DNL Azure].
* **Model update**: Het model wordt regelmatig bijgewerkt, op een wekelijkse basis, door vraagbankwisseluitbreiding. Het model wordt ook bijgewerkt door nieuwe het vragen strategieën en instructies wanneer nodig.

## Fairness en afwijking {#fairness-and-bias}

* **Model billijkheid**: Om het model te verzekeren interpreteert en produceert vragen over verschillende gebruikersintenties en taalvariaties constant zonder vooroordelen te introduceren of stereotiepen te versterken, gebruikt Adobe snelle controle, verklaarbaarheid, en waarborgen tegen het produceren van vooroordelen of onethische output.
* **de vooroordelen van Gegevens**: De modeloutput wordt beïnvloed door de In-Context het Leren voorbeelden, en wat terugwinnen in de herinnering selecteert. De voorbeelden van de vraagbank bevatten voorbeelden die vanuit het perspectief van Productbeheer representatief worden geacht. Afhankelijk van het gebruiksgeval, zouden de klanten moeten overwegen hoe de potentiële vooroordelen in modeloutput zich kunnen richten op of hun voorgenomen toepassing beïnvloeden.

## Ethische overwegingen {#ethical-considerations}

**Ethische overwegingen verbonden aan het model**: Om het blootstellen van PII of gevoelige attributen te vermijden, is het model ontworpen om het versterken van bestaande gegevensvooroordelen te vermijden, en toegangsbeheergrenzen te respecteren. Dit omvat het filtreren, het etiketteren, en de controleschemagebieden voor verantwoordelijk gebruik.
