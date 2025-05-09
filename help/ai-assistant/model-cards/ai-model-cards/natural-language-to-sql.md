---
title: AI Assistant Natural Language voor SQL-modelkaart
description: Meer informatie over het AI Assistant Natural Language-model van SQL.
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AI Assistant Operational Insights Natural Language to SQL Model Card

## Modeloverzicht {#model-overview}

* De officiële naam van het model is AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]) en is in februari 2025 gepubliceerd in de nieuwste GA-versie.
* Het model wordt ontworpen om de vragen van de natuurlijke taal van klanten over operationele inzichten in SQL vragen te vertalen. Deze SQL-query&#39;s worden uitgevoerd in de Adobe Experience Platform-kennisgrafiek, die metagegevens bevat over de Experience Platform-entiteiten van de klant, zoals schema&#39;s, datasets, publiek, bestemmingen en reizen. De resultaten van de SQL vragen worden dan gebruikt om reacties op de originele natuurlijke taalvragen van de klanten te produceren.
* De primaire gebruikers van dit model zijn marketing beroeps, gegevensanalisten, of klant reismanager-die probeert om operationele inzichten binnen Experience Platform te begrijpen en te handelen gebruikend natuurlijke taal. Ze zijn mogelijk geen experts in SQL- of gegevenstechniek, maar hebben snelle, nauwkeurige antwoorden nodig over hun Experience Platform-entiteiten om geïnformeerde beslissingen te nemen en de ervaringen van klanten te optimaliseren.
* Dit model maakt deel uit van de AI Assistant for Operational Insights, waarin gebruikers toegang krijgen tot metagegevens over hun Experience Platform-entiteiten, zoals publiek, reizen, schema&#39;s, kenmerken, gegevenssets en bestemmingen. De gebruikers kunnen vragen in natuurlijke taal-als stellen welk publiek wordt geactiveerd of welk publiek een specifiek schema-gebruikt en het model vertaalt deze in SQL vragen over de de kennisgrafiek van Experience Platform. Dit laat gebruikers toe om operationele zicht snel te bereiken en geïnformeerde besluiten te nemen zonder het moeten het systeem manueel onderzoeken of vragen.
* Dit model behandelt belangrijke pijnpunten waarmee zakelijke gebruikers en analisten die met Experience Platform werken worden geconfronteerd, zoals de complexiteit van het navigeren door grote hoeveelheden onderling verbonden metagegevens, de noodzaak om SQL-query&#39;s handmatig te schrijven om operationele inzichten op te halen en het gebrek aan zichtbaarheid in de manier waarop Experience Platform-entiteiten zoals publiek, datasets en reizen worden verbonden of uitgevoerd. Door natuurlijke taaltoegang tot meta-gegevens toe te laten en SQL generatie te automatiseren, vermindert het model afhankelijkheid van technische middelen, verkort insight ontdekkingstijd, en machtigt gebruikers om snellere, data-gedreven besluiten te nemen.
* Het model mag niet worden gebruikt voor toegang tot PII (Personeel Identified Information), zoals klantnamen, e-mailadressen of telefoonnummers, zelfs niet als dergelijke gegevens op het platform aanwezig zijn.
* Daarnaast mag het niet worden gebruikt voor nalevings- of governancecontroles, zoals het valideren van beleid voor gegevensbewaring, toegangsbeheerregels of toestemmingsstatus. Deze taken vereisen gespecialiseerde systemen en strategieën.

## Modeldetails {#model-details}

* Het modeltype is Vragen LLM met Dynamisch In-Context Leren.
* De modelinvoer zijn query&#39;s voor natuurlijke talen van gebruikers.
* Het model geeft SQL-query&#39;s als uitvoer in [!DNL Snowflake] syntaxis, die worden uitgevoerd via Experience Platform Knowledge Graph.

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

## Modeltraining {#model-training}

* [!DNL NL2SQL] gebruikte [!DNL OpenAI] GPT-modellen voor in-context leren.
* De [!DNL NL2SQL] -vraagbank bevat 428 query&#39;s van het [!DNL Operational Insights] -team en 524 query&#39;s van externe teams voor alfa-gebruik.

## Modelevaluatie {#model-evaluation}

* Het model wordt met nauwkeurigheid geëvalueerd. Bijvoorbeeld, van alle [!DNL NL2SQL] verzoeken, hoeveel van de verzoeken de correcte SQL resultaten opleveren.
* Het evaluatieproces is een combinatie op regel-gebaseerde aanpassing (SQL normalisatie en dan directe SQL koordaanpassing), op LLM-Gebaseerde SQL solver, en menselijke evaluatie
* De open reeksen worden gebruikt voor regressietests, en de wekelijkse annotatieprojecten controleren de prestaties van het model door bemonsterd echt klantenverkeer.
* In termen van contradictoire evaluatie, is er een afzonderlijk in-werkingsgebied en buiten-werkingsgebied model dat als leidraad voor [!DNL NL2SQL] werkt.

## Modelimplementatie {#model-deployment}

* Het LLM-model is een op GPT gebaseerd model dat wordt gehost door [!DNL Azure OpenAI] API&#39;s.
* Het basismodel wordt gehost door [!DNL Azure] .
* Het model wordt regelmatig, wekelijks, geactualiseerd door uitbreiding van de vraagbank. De moduslijst wordt ook bijgewerkt met behulp van nieuwe aanroepstrategieën en instructies wanneer dat nodig is.

## Uitlegbaarheid {#explainability}

Het model gebruikt een afzonderlijk verklaringsmodel voor SQL.

## Fairness en afwijking {#fairness-and-bias}

* Om ervoor te zorgen dat het model vragen consistent interpreteert en genereert over verschillende gebruikersinzichten en taalkundige variaties zonder vooroordelen in te voeren of stereotypen te versterken, gebruikt Adobe snelle controle, verklaarbaarheid en waarborgen tegen het genereren van vooroordelen of onethische output.
* De modeloutput wordt beïnvloed door de In-Context het Leren voorbeelden, en wat terugwinnen in de herinnering selecteert. De voorbeelden van de vraagbank bevatten voorbeelden die vanuit het perspectief van PM als representatief worden beschouwd, en we breiden ook de vraagbanken uit op basis van echt klantenverkeer.

## Robuustheid {#robustness}

Aangezien de meeste vragen die zij ontvangt, niet in de vraagbank worden behandeld, weerspiegelt de nauwkeurigheid van het productieverkeer de robuustheid van het model.

## Overwegingen met betrekking tot privacy en beveiliging {#privacy-and-security-considerations}

Het model verwerkt of bewaart geen persoonlijk identificeerbare informatie (PII), en die informatie wordt gemaskeerd voor SQL generatie. Voor op attribuut-gebaseerde toegangsbeheertoestemmingscontrole, zal geproduceerde SQL verder door het team van de Grafiek van de Kennis van Experience Platform worden verwerkt om governancekwaliteit te verzekeren.

## Ethische overwegingen {#ethical-considerations}

Om het blootstellen van PII of gevoelige attributen te vermijden, is het model ontworpen om privacy te steunen, bestaande gegevensvooroordelen te vermijden, en toegangsbeheergrenzen te respecteren. Dit omvat het filtreren, het etiketteren, en de controleschemagebieden voor verantwoordelijk gebruik.

