---
keywords: Experience Platform;query-service;Query-service;geneste gegevensstructuren;geneste gegevens;afvlakken;geneste gegevens samenvoegen; samenvoegen;
title: Geneste gegevensstructuren samenvoegen voor gebruik met BI-gereedschappen
description: In dit document wordt uitgelegd hoe u XDM-schema's voor alle tabellen en weergaven tijdens een sessie afvlakt wanneer u BI-gereedschappen van derden gebruikt met Query Service.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: fc98b111aa15cdeb64eacdc05cac33a00ee98d80
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 0%

---

# Geneste gegevensstructuren samenvoegen voor gebruik met BI-gereedschappen van derden

Adobe Experience Platform Query Service ondersteunt de instelling `FLATTEN` wanneer u verbinding maakt met een database via externe BI-hulpprogramma&#39;s. Met deze functie worden geneste gegevensstructuren in BI-tools van derden afgevlakt om de bruikbaarheid ervan te verbeteren en de vereiste werklast voor het ophalen, analyseren, transformeren en rapporteren van gegevens te verminderen.

Veel BI-gereedschappen, zoals [!DNL Tableau] en [!DNL Power BI] , bieden geen native ondersteuning voor geneste gegevensstructuren. Met de instelling `FLATTEN` hoeft u geen SQL-weergaven boven op uw gegevens te maken om een platte versie te leveren of kunt u via Query Service `CTAS` - of `INSERT INTO` -taken uw gegevenssets dupliceren naar platte versies wanneer u ad-hocschema&#39;s gebruikt.

Met de instelling `FLATTEN` wordt de structuur van elk bladveld naar de hoofdmap van de tabel verplaatst en wordt het veld een naam na de oorspronkelijke naamruimte gegeven. Hierdoor kunt u puntnotatie gebruiken om een veld aan te passen aan het XDM-pad (Experience Data Model), terwijl de context van het veld behouden blijft.

## Vereisten

Voor het gebruik van de instelling `FLATTEN` is een goed begrip van de volgende componenten van Adobe Experience Platform vereist:

* [ XDM Systeem ](../../xdm/home.md): Een overzicht op hoog niveau van XDM en zijn implementatie in Experience Platform.

   * [ creeer een ad hoc schema ](../../xdm/tutorials/ad-hoc.md): Een schema XDM met gebieden die namespaced voor gebruik slechts door één enkele dataset zijn, wordt bedoeld als ad hoc schema. Ad-hocschema&#39;s worden gebruikt in verschillende workflows voor gegevensinvoer voor Experience Platform en het maken van bepaalde soorten bronverbindingen.

* [ Sandboxes ](../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

* [ Genestelde gegevensstructuren ](./nested-data-structures.md): Dit document verstrekt voorbeelden van hoe te om, datasets met complexe gegevenstypes tot stand te brengen te verwerken of om te zetten met inbegrip van genestelde gegevensstructuren.

## Verbinding maken met een database met behulp van de FLATTEN-instelling {#connect-with-flatten}

Met de instelling `FLATTEN` voegt u geneste gegevensstructuren samen tot afzonderlijke kolommen, waarbij de kenmerknaam de kolomnaam wordt die de rijwaarden bevat. Als u werkt met gegevens in BI-gereedschappen die geen ondersteuning bieden voor geneste gegevensstructuren, verbetert deze instelling de bruikbaarheid van ad-hocschema&#39;s en vermindert de benodigde werklast.

Wanneer u verbinding maakt met de Query-service met een door u gekozen externe client, voegt u de instelling `FLATTEN` toe aan de databasenaam. Voor informatie over hoe te om een specifiek hulpmiddel van BI aan te sluiten, te zien gelieve zijn respectieve documentatie in [ cliënten aan het overzicht van de Dienst van de Vraag ](../clients/overview.md) verbinden. De verbindingstekenreeks moet het volgende bevatten:

* De naam van de sandbox.
* Een dubbele punt, gevolgd door `all` of een specifieke gegevensset-id, weergave-id of databasenaam.
* Een vraagteken (?) gevolgd door het trefwoord `FLATTEN` .

De invoer moet de volgende indeling hebben:

```bash
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Een voorbeeld van een verbindingstekenreeks kan er als volgt uitzien:

```bash
prod:all?FLATTEN
```

## Voorbeeld {#example}

In het voorbeeldschema dat in deze handleiding wordt gebruikt, wordt de standaardveldgroep [!UICONTROL Commerce Details] gebruikt, die de `commerce` -objectstructuur en de `productListItems` -array gebruikt. Zie de documentatie XDM voor [ meer informatie over de [!UICONTROL Commerce Details] gebiedsgroep ](../../xdm/field-groups/event/commerce-details.md). In de onderstaande afbeelding ziet u een weergave van de schemastructuur.

![ het schemadiagram van A van de het gebiedsgroep van Details van Commerce met inbegrip van `commerce` en `productListItems` structuren.](../images/key-concepts/commerce-details.png)

Als uw hulpmiddel van BI geen genestelde gegevensstructuren steunt, kan het moeilijk zijn om van genestelde gebieden van verwijzingen te voorzien als zij geserialiseerde waarden (zoals `commerce` en `productListItems` in het voorbeeldschema) bevatten. Deze waarden kunnen verschijnen als delen van één gecodeerd `commerce` tekenreeksveld en zijn realistisch gezien niet onbruikbaar.

De volgende waarden vertegenwoordigen `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) en `commerce.purchases.value` (1.0) in slecht opgemaakte geneste velden.

```bash
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Met de instelling `FLATTEN` hebt u toegang tot afzonderlijke velden in uw schema of tot hele secties van de geneste gegevensstructuur met behulp van puntnotatie en de oorspronkelijke padnaam. Hieronder ziet u een voorbeeld van deze notatie waarbij de veldgroep `commerce` wordt gebruikt.

```bash
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

De instelling `FLATTEN` heeft bepaalde beperkingen wanneer u werkt met andere gegevensstructuren. De volledige details worden verstrekt in de [ sectie van beperkingen ](#limitations).

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

Met de instelling `FLATTEN` worden momenteel de volgende gegevensstructuren niet samengevoegd:

| Gegevensstructuur | Beperking |
|---|---|
| Arrays | Gebruik een expliciete arrayindex of de functie `EXPLODE` om toegang te krijgen tot arrays. |
| Kaarten | Gebruik de tekenreekssleutel om een waarde onder een kaart te openen voor toegang tot kaarten. |

Om zowel de Kaart als de beperkingen van de Serie op te lossen moet u de hulpmiddelen gebruiken BBI ruw SQL het uitgeven zoals de Geavanceerde Opties -> SQL Verklaring in Power BI.

BI-gereedschappen, zoals onbewerkte SQL-bewerkingen, zijn nodig om zowel de map- als arraybeperkingen op te lossen. Zie de gids op hoe te [ gebruik Power BI geavanceerde opties om een douaneSQL vraag ](../clients/power-bi.md#import-tables-using-custom-sql) in de SQL verklaringssectie in te gaan.

## Volgende stappen

In dit document wordt beschreven hoe u geneste gegevensstructuren kunt afvlakken voor gebruik met externe BI-gereedschappen. Als u nog niet uw cliënt hebt verbonden, zie [ het overzicht van de cliëntverbinding ](../clients/overview.md) voor een lijst van gesteunde derdecliënten.
