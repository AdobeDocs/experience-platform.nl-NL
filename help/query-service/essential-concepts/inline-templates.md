---
title: Inline sjablonen
description: Leer hoe te om veelvoudige voorwaarden in talrijke vragen met gealigneerde malplaatjes opnieuw te gebruiken.
exl-id: 78959070-f9e5-4736-b72a-a8ef518bfa4f
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# Inline-sjablonen

Met inlinesjablonen kunt u meerdere voorwaarden hergebruiken in meerdere query&#39;s. U kunt criteria in een malplaatje opslaan en dan hen opnieuw gebruiken in veelvoudige vragen. De herbruikbare SQL malplaatjes verminderen ontwikkelingsinspanningen en ook het risico van fouten van het kopiëren van lange verklaringen tussen vragen. Met gealigneerde malplaatjes, kunt u veranderingen in één plaats aanbrengen en hebben die veranderingen in om het even welke vraag weerspiegelen die naar dit malplaatje verwijst.

Dit document behandelt het gebruik en de beperkingen van gealigneerde malplaatjes binnen de Redacteur van de Vraag.

## Vereisten

Inlinesjablonen worden ondersteund door zowel de UI als de API van de Query Service. Lees voordat u verdergaat met deze handleiding de documentatie over hoe u [een querysjabloon maken via de API](../api/query-templates.md#create-a-query-template) of met de [Query-editor](../ui/user-guide.md#query-authoring).

## Inline sjabloonsyntaxis {#syntax}

Als een query eenmaal is opgeslagen, wordt deze een sjabloon genoemd. Wanneer de sjabloon naar een andere sjabloon binnen de instructie verwijst, wordt deze een inline sjabloon genoemd. Inline sjablonen worden in uw SQL aangegeven met het hashsymbool (#) gevolgd door de sjabloonnaam. Een voorbeeld van deze syntaxis is `#YOUR_TEMPLATE_NAME`.

## Gebruiksscenario {#use-case}

De volgende SQL malplaatjes tonen het nut van gealigneerde malplaatjes aan, met een voorbeeld om het aantal klanten van de V.S. van om het even welk gebied te tellen die meer dan de &quot;maximum opbrengst&quot;besteedden en vóór Juni 2023 bevolen. Het voordeel van de inlinesjabloon is dat u de onderliggende sjabloon gemakkelijk kunt bewerken (in dit geval de maximale omzet- en besteldatum) en dat u de bovenliggende sjabloon niet hoeft te wijzigen.

**Voorbeeld**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

Wanneer het uitvoeren van de vraag, vervangt de Dienst van de Vraag de malplaatjenaam die van het knoeiboelsymbool met de genoemde SQL verklaring van het malplaatje begint.

>[!NOTE]
>
>Zoeksjablonen kunnen een willekeurig aantal andere inlinesjablonen aanroepen. Er is geen beperking op het aantal gealigneerde malplaatjes die u van één enkele vraag kunt aanhalen. Sjablonen kunnen ook worden genest binnen andere inlinesjablonen.

U kunt sjablonen gebruiken om een of meerdere voorwaarden op te slaan. Ze hoeven op zich geen volledige query te zijn. Als uw malplaatje een geldige vraag bevat, kunt u de vraag eenvoudig uitvoeren door de malplaatjenaam te roepen die met een knoeiboelsymbool wordt voorafgegaan. Als u bijvoorbeeld `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` als een sjabloon met de naam `JUNE_2023_LOYALTY_MEMBERS`, de opdracht  `#JUNE_2023_LOYALTY_MEMBERS;` wordt de geldige query in de sjabloon uitgevoerd.

>
>
>In de gebruikersinterface van Adobe Experience Platform worden inlinesjablonen in de vorm van geparameteriiseerde query&#39;s alleen op het hoofdniveau ondersteund. Dit betekent dat de parameters bepaalde vragen slechts werken wanneer gebruikt in het originele malplaatje. Het kindmalplaatje moet een statisch malplaatje zijn en kan geen dynamische parameters hebben. Zie de [parameterized vragen documentatie](../ui/parameterized-queries.md) voor meer informatie.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om andere malplaatjes binnen uw SQL, of in de Redacteur van de Vraag of door de Dienst API van de Vraag van verwijzingen te voorzien.

Bovendien moet u de [anonieme blokgids](./anonymous-block.md), waarin wordt uitgelegd hoe u ontwikkelingsoverheadkosten kunt minimaliseren door een of meer SQL-instructies in een keten te koppelen die op volgorde worden uitgevoerd.
