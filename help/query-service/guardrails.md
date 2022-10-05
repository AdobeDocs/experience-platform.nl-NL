---
keywords: Experience Platform;query;query-service;problemen oplossen;instructies;richtlijnen;limiet;
title: Guardrails voor Query-service
description: Dit document bevat informatie over gebruiksbeperkingen voor gegevens van Query Service om u te helpen uw querygebruik te optimaliseren.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: f8913fd8f5d6f4acf70a43c0a047bcd034dfd402
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# Guardrails voor Query-service

De begeleiding is drempels die begeleiding voor gegevens en systeemgebruik, prestatiesoptimalisering, en vermijding van fouten of onverwachte resultaten in Adobe Experience Platform verstrekken.

Dit document biedt standaardgebruikslimieten voor gegevens van Query Service om u te helpen de systeemprestaties te optimaliseren wanneer u gegevens opvraagt met betrekking tot uw licentierechten.

## Vereisten

Voordat u doorgaat met dit document, hebt u een goed inzicht in de twee hieronder beschreven mogelijkheden van Query Service:

* **Ad-hocquery&#39;s**: Voor uitvoering `SELECT` query&#39;s voor het verkennen, experimenteren en valideren van gegevens waar de resultaten van de query&#39;s **zijn niet opgeslagen** op het data Lake.

* **Batchquery&#39;s**: Voor uitvoering `INSERT TABLE AS SELECT` en `CREATE TABLE AS SELECT` query&#39;s voor het opschonen, vormgeven, manipuleren en verrijken van gegevens. De resultaten van deze query&#39;s **worden opgeslagen** op het data Lake. De maatstaf voor het meten van het verbruik van deze functionaliteit is computeruren.

In de onderstaande afbeelding ziet u hoe de mogelijkheden van Query Service momenteel zijn verpakt en in licentie worden gegeven:

![Een diagram om de distributie en de verpakking van de mogelijkheden van de Dienst van de Vraag met betrekking tot vergunning te verklaren.](./images/guardrails/query-capabilities.png)

## Limiettypen

Dit document bevat twee typen standaardlimieten:

* **Zachte limiet**: U kunt een zachte limiet overschrijden, maar zachte limieten bieden een aanbevolen richtlijn voor systeemprestaties.

* **Harde limiet**: Een harde grens verstrekt een absoluut maximum.

>[!NOTE]
>
>De standaardlimieten die in dit document worden beschreven, worden voortdurend verbeterd. Kom regelmatig terug voor updates.

## Prestatiegaranties primaire entiteit

De lijsten hieronder verstrekken de geadviseerde guardrailgrenzen en beschrijvingen voor vraaguitvoering wanneer het gebruiken van een bepaald vraagpatroon.

**Ad-hocquery&#39;s**

| **Guardrail** | **Limiet** | **Type limiet** | **Beschrijving** |
|---|---|---|---|
| Maximale uitvoeringstijd | 10 minuten | Hard | Hiermee wordt de maximale uitvoertijd voor een ad-hoc SQL-query gedefinieerd. Als u de tijdslimiet voor het retourneren van een resultaat overschrijdt, wordt de foutcode 53400 gegenereerd. |
| Gelijktijdige query | <ul><li>Zoals gespecificeerd in de productbeschrijving van de toepassing.</li><li>+1 (waarbij elke extra SKU-pack voor ad-hocquery-gebruikers is aangeschaft)</li></ul> | Hard | Dit bepaalt hoeveel vragen gelijktijdig voor een bepaalde organisatie kunnen worden uitgevoerd. Als de gelijktijdige limiet wordt overschreden, worden de query&#39;s in een wachtrij geplaatst. |
| Client-connector en resultaatuitvoerlimiet | Clientconnector<ul><li>Query-gebruikersinterface (100 rijen)</li><li>Client van derden (50.000)</li><li>[!DNL PostgresSQL] client (50.000)</li></ul> | Hard | Het resultaat van een vraag kan door de volgende middelen worden ontvangen:<ul><li>Gebruikersinterface Query Service</li><li>Client van derden</li><li>[!DNL PostgresSQL] client</li></ul>Opmerking: Het toevoegen van een beperking aan de outputtelling kan resultaten sneller terugkeren. Bijvoorbeeld: `LIMIT 5`, `LIMIT 10`, enzovoort. |
| Resultaten geretourneerd via | Gebruikersinterface client | N.v.t. | Hiermee bepaalt u hoe de resultaten ter beschikking worden gesteld van de gebruikers. |

{style=&quot;table-layout:auto&quot;}

**Batchquery&#39;s**

| **Guardrail** | **Limiet** | **Type limiet** | **Beschrijving** |
|---|---|---|---|
| Maximale uitvoeringstijd | 24 uur | Hard | Dit bepaalt de maximumuitvoeringstijd voor een partijSQL vraag.<br>De verwerkingstijd van een vraag is afhankelijk van het volume van te verwerken gegevens en vraagingewikkeldheid. |
| Gelijktijdige gebruiker | Geen gebruikersbeperking | N.v.t. | De Geplande Vragen van de Partij zijn asynchrone banen zodat is er geen gebruikersbeperking. |
| Rekenuren voor batchverwerking | Zoals gespecificeerd in de Adobe Experience Platform Intelligence Query Custom SKU-verkooporder van de klant | Zacht | Dit bepaalt de scoped hoeveelheid verwerkingstijd per jaar een klant wordt toegestaan voor het uitvoeren van partijvragen om gegevens terug in het gegevens meer af te tasten, te verwerken en te schrijven. |
| Gelijktijdige query | Ondersteund | N.v.t. | Gepland partijvragen zijn asynchrone banen, daarom worden de gezamenlijke vragen gesteund. |
| Clientconnector en uitvoerlimiet van resultaat | Clientconnector<ul><li>Query-gebruikersinterface (geen bovenlimiet voor rijen)</li><li>Client van derden (geen bovenlimiet voor rijen)</li><li>[!DNL PostgresSQL] client (geen bovenlimiet voor rijen)</li><li>REST API&#39;s (geen bovengrens voor rijen)</li></ul> | Hard | Het resultaat van een query kan op de volgende manieren beschikbaar worden gemaakt:<ul><li>Kan worden opgeslagen als afgeleide gegevenssets</li><li>Kan in de bestaande afgeleide gegevenssets worden opgenomen</li></ul>Opmerking: Er is geen bovengrens aan het aantal van de verslagtelling van het vraagresultaat. |
| Resultaten geretourneerd via | Gegevensset | N.v.t. | Hiermee bepaalt u hoe de resultaten ter beschikking worden gesteld van de gebruikers. |

{style=&quot;table-layout:auto&quot;}

## Dashboards-inzichten die zijn gegenereerd met query&#39;s {#dashboard-insights}

Om ervoor te zorgen dat elke query voor een Real-time Customer Data Platform-inzichten over voldoende bronnen beschikt om efficiënt te worden uitgevoerd, houdt de API het gebruik van bronnen bij door er corrency-sleuven aan elke query toe te wijzen. Het systeem kan tot vier gezamenlijke vragen verwerken, en daarom zijn vier gezamenlijke vraaggroeven beschikbaar op elk bepaald ogenblik. Vragen worden in een wachtrij geplaatst op basis van sleuven voor gelijktijdige uitvoering en wachten vervolgens in de wachtrij totdat voldoende sleuven voor gelijktijdige uitvoering beschikbaar zijn.

## Volgende stappen

Na het lezen van dit document zou u een beter inzicht in de standaardgrenzen voor vraaguitvoering met de beschikbare vraagpatronen moeten hebben.

Zie de volgende documentatie voor meer informatie over de Dienst van de Vraag:

* [Query Service-API](./api/getting-started.md)
* [Gebruikersinterface Query Service](./ui/overview.md)
