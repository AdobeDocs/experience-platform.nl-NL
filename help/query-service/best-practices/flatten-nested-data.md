---
keywords: Experience Platform;query-service;Query-service;geneste gegevensstructuren;geneste gegevens;afvlakken;geneste gegevens afvlakken;samenvoegen;
title: Geneste gegevensstructuren samenvoegen voor gebruik met BI-gereedschappen
description: In dit document wordt uitgelegd hoe u XDM-schema's voor alle tabellen en weergaven tijdens een sessie afvlakt wanneer u BI-gereedschappen van derden gebruikt met Query Service.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: a7f273383293359cf6adbcc0a508fb19d2789339
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Geneste gegevensstructuren samenvoegen voor gebruik met BI-gereedschappen van derden

Adobe Experience Platform Query Service ondersteunt de `FLATTEN` het plaatsen wanneer het verbinden met een gegevensbestand door derdehulpmiddelen van BI. Met deze functie worden geneste gegevensstructuren in BI-tools van derden afgevlakt om de bruikbaarheid ervan te verbeteren en de vereiste werklast voor het ophalen, analyseren, transformeren en rapporteren van gegevens te verminderen.

Veel BI-gereedschappen zoals [!DNL Tableau] en [!DNL Power BI] ondersteunen native geen geneste gegevensstructuren. De `FLATTEN` het plaatsen verwijdert de behoefte om SQL meningen bovenop uw gegevens tot stand te brengen om een vlakke versie te verstrekken, of de Dienst van de Vraag te gebruiken `CTAS` of `INSERT INTO` taken om uw datasets in vlakke versies te dupliceren wanneer het gebruiken van ad hoc regelingen.

De `FLATTEN` met deze instelling wordt de structuur van elk bladveld naar de hoofdmap van de tabel verplaatst en wordt het veld een naam na de oorspronkelijke naamruimte gegeven. Hierdoor kunt u puntnotatie gebruiken om een veld aan te passen aan het XDM-pad (Experience Data Model), terwijl de context van het veld behouden blijft.

## Vereisten

Met de `FLATTEN` voor het instellen is een goed begrip van de volgende onderdelen van Adobe Experience Platform vereist:

* [XDM-systeem](../../xdm/home.md): Een overzicht op hoog niveau van XDM en zijn implementatie in Experience Platform.

   * [Een ad-hocschema maken](../../xdm/tutorials/ad-hoc.md): Een XDM-schema met velden die alleen voor gebruik door één gegevensset worden genoemd, wordt een ad-hocschema genoemd. Ad-hocschema&#39;s worden gebruikt in diverse werkstromen voor gegevensinvoer voor Experience Platform en het creëren van bepaalde soorten bronverbindingen.

* [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

* [Geneste gegevensstructuren](./nested-data-structures.md): Dit document verstrekt voorbeelden van om, datasets met complexe gegevenstypes met inbegrip van genestelde gegevensstructuren tot stand te brengen te verwerken of om te zetten.

## Verbinding maken met een database met behulp van de FLATTEN-instelling {#connect-with-flatten}

De `FLATTEN` bij het instellen worden geneste gegevensstructuren afgevlakt in afzonderlijke kolommen, waarbij de kenmerknaam de kolomnaam wordt die de rijwaarden bevat. Als u werkt met gegevens in BI-gereedschappen die geen ondersteuning bieden voor geneste gegevensstructuren, verbetert deze instelling de bruikbaarheid van ad-hocschema&#39;s en vermindert de benodigde werklast.

Wanneer het verbinden met de Dienst van de Vraag met uw gekozen derde cliënt, voeg toe `FLATTEN` instellen op de databasenaam. Voor informatie over hoe te om een specifiek hulpmiddel van BI aan te sluiten, gelieve zijn respectieve documentatie in te zien [Verbind cliënten met het overzicht van de Dienst van de Vraag](../clients/overview.md). De verbindingstekenreeks moet het volgende bevatten:

* De naam van de sandbox.
* Een dubbele punt, gevolgd door `all` of een specifieke dataset-id, weergave-id of databasenaam.
* Een vraagteken (?) gevolgd door de `FLATTEN` trefwoord.

De invoer moet de volgende indeling hebben:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Een voorbeeld van een verbindingstekenreeks kan er als volgt uitzien:

```terminal
prod:all?FLATTEN
```

## Voorbeeld {#example}

In het voorbeeldschema dat in deze handleiding wordt gebruikt, wordt de standaardveldgroep gebruikt [!UICONTROL Commerce Details], die de `commerce` de objectstructuur en de `productListItems` array. Zie de XDM-documentatie voor [meer informatie over de [!UICONTROL Commerce Details] veldgroep](../../xdm/field-groups/event/commerce-details.md). In de onderstaande afbeelding ziet u een weergave van de schemastructuur.

![Een schema van de het gebiedsgroep van de Details van de Handel met inbegrip van `commerce` en `productListItems` structuren.](../images/best-practices/flatten-nested-data/commerce-details.png)

Als uw hulpmiddel van BI geen genestelde gegevensstructuren steunt, kan het moeilijk zijn om van verwijzingen te voorzien genestelde gebieden indien zij geserialiseerde waarden (zoals bevatten `commerce` en `productListItems` in het voorbeeldschema). Deze waarden kunnen verschijnen als delen van één gecodeerde waarde `commerce` tekenreeksveld en zijn niet realistisch onbruikbaar.

De volgende waarden vertegenwoordigen `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180), en `commerce.purchases.value`(1.0) in geneste velden met een slechte opmaak.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Met de `FLATTEN` Als u een instelling instelt, kunt u afzonderlijke velden in uw schema of volledige secties van de geneste gegevensstructuur openen met behulp van puntnotatie en de oorspronkelijke padnaam. Een voorbeeld van deze indeling met de `commerce` de veldgroep wordt hieronder weergegeven.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

De `FLATTEN` het plaatsen heeft bepaalde beperkingen wanneer het behandelen van andere gegevensstructuren. De volledige informatie wordt verstrekt in [sectie beperkingen](#limitations).

### Aanhalingstekens gebruiken voor velden in query&#39;s {#quotation-marks}

De samengevoegde hoofdvelden gebruiken nu puntnotatie om hun XDM-paden aan te passen. Wanneer de velden in een query worden gebruikt, moeten deze tussen aanhalingstekens (&quot; &quot;) staan.

In het onderstaande SQL-voorbeeld wordt de oorspronkelijke status van de geneste query weergegeven:

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Wanneer u de samengevoegde gegevensvelden gebruikt, wordt de query geschreven met behulp van puntnotatie en ingesloten door aanhalingstekens, zoals hieronder wordt getoond:

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Beperkingen {#limitations}

De `FLATTEN` met deze instelling worden momenteel niet de volgende gegevensstructuren samengevoegd:

| Gegevensstructuur | Beperking |
|---|---|
| Arrays | Gebruik een expliciete arrayindex of de `EXPLODE` functie voor toegang tot arrays. |
| Kaarten | Gebruik de tekenreekssleutel om een waarde onder een kaart te openen voor toegang tot kaarten. |

Om zowel de Kaart als de beperkingen van de Serie op te lossen moet u de hulpmiddelen gebruiken BBI ruw SQL het uitgeven zoals de Geavanceerde Opties -> SQL Verklaring in Power BI.

BI-gereedschappen, zoals onbewerkte SQL-bewerkingen, zijn nodig om zowel de map- als arraybeperkingen op te lossen. Zie de handleiding over hoe u [Geavanceerde opties voor Power BI gebruiken om een aangepaste SQL-query in te voeren](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html#import-tables-using-custom-sql) in de SQL-instructiesectie.

## Volgende stappen

In dit document wordt beschreven hoe u geneste gegevensstructuren kunt afvlakken voor gebruik met externe BI-gereedschappen. Als u nog geen verbinding met de client hebt, raadpleegt u [het overzicht van de clientverbinding](../clients/overview.md) voor een lijst met ondersteunde clients van derden.
