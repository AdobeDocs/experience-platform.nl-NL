---
keywords: Experience Platform;query;query-service;problemen oplossen;instructies;richtlijnen;limiet;
title: Guardrails voor Query-service
description: Dit document bevat informatie over gebruiksbeperkingen voor gegevens van Query Service om u te helpen uw querygebruik te optimaliseren.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 23c7a4590b365a49edb066567b6ebe2ac08c67e8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 1%

---

# Guardrails voor Query-service

De begeleiding is drempels die gegevens en systeemgebruik, prestatiesoptimalisering, en vermijding van fouten of onverwachte resultaten in Adobe Experience Platform begeleiden.
Dit document biedt standaardgebruikslimieten voor gegevens van Query Service om u te helpen de systeemprestaties te optimaliseren wanneer u gegevens opvraagt met betrekking tot uw licentierechten.

>[!IMPORTANT]
>
>Controleer uw vergunningsrechten in uw Orde van de Verkoop en de overeenkomstige [ Beschrijving van het Product ](https://helpx.adobe.com/nl/legal/product-descriptions.html) op daadwerkelijke gebruiksgrenzen naast deze guardrails pagina.

## Vereisten

Alvorens met dit document verder te gaan, zou u een goed inzicht in de belangrijkste definities en de mogelijkheden van de Dienst van de Vraag moeten hebben. Deze worden hieronder beschreven:

* **Ad hoc vragen**: Voor het uitvoeren van `SELECT` vragen om te onderzoeken, te experimenteren, en gegevens te bevestigen waar de resultaten van de vragen **niet** op het gegevensmeer worden opgeslagen.

* **de vragen van de Partij**: Voor het uitvoeren `INSERT TABLE AS SELECT` en `CREATE TABLE AS SELECT` vragen om, gegevens schoon te maken vorm te manipuleren en te verrijken. De resultaten van deze vragen **worden opgeslagen** op het gegevensmeer. De maatstaf voor het meten van het verbruik van deze functionaliteit is computeruren.

* **de gebruikers van de Dienst van de Vraag**: De gebruikers van de Dienst van de vraag die binnen uw huidige vergunning voor Customer Journey Analytics, Adobe Real-Time Customer Data Platform, en/of Adobe Journey Optimizer worden verstrekt kunnen ook met Gegevens Distiller worden gebruikt. De gebruikers van de Dienst van de vraag worden gedeeld tussen eigenschappen.

* **Ad hoc gebruikers**: Ad hoc gebruikers zijn degenen die ad hoc vragen uitvoeren.

* **de gebruikers van de Partij**: De gebruikers van de partij zijn degenen die partijvragen uitvoeren.

* **Meldend API**: API voor het maken van gegevens haalt vraag (intern of extern). Uitgebreide rapporteringsgegevensmodellen worden afgeleid van de native rapporteringsgegevensmodellen in Adobe Experience Platform, zoals het Real-Time CDP-dashboardgegevensmodel.

## Typen guardrail

Dit document bevat twee typen standaardlimieten:

| Het type Guardrail | Beschrijving |
|----------|---------|
| **Gegarandeerde van Prestaties (Zachte grens)** | Prestatiegaranties zijn gebruikslimieten die betrekking hebben op het bereik van uw gebruiksgevallen. Als u de prestatiegaranties overschrijdt, kan de prestaties achteruitgaan en de latentie vertragen. Adobe is niet verantwoordelijk voor deze verslechtering van de prestaties. Klanten die een prestatiegarantie consequent overschrijden, kunnen ervoor kiezen om extra capaciteit te licentiëren om prestatievermindering te voorkomen. |
| **systeem-afgedwongen grails (Harde grens)** | De door het systeem afgedwongen instructies worden afgedwongen door de gebruikersinterface of API van Real-Time CDP. Dit zijn grenzen die u niet kunt overschrijden aangezien UI en API u zal tegenhouden dit te doen of een fout zal terugkeren. |

{style="table-layout:auto"}

>[!NOTE]
>
>De standaardlimieten die in dit document worden beschreven, worden voortdurend verbeterd. Kom regelmatig terug voor updates.

## Prestatiegaranties primaire entiteit

De lijsten hieronder verstrekken de geadviseerde guardrailgrenzen en beschrijvingen voor vraaguitvoering wanneer het gebruiken van een bepaald vraagpatroon.

**Ad hoc vragen**

| Guardrail | Limiet | Type limiet | Beschrijving |
|---|---|---|---|
| Maximale uitvoeringstijd | 10 minuten | Door het systeem afgedwongen geleiding | Hiermee wordt de maximale uitvoertijd voor een ad-hoc SQL-query gedefinieerd. Als u de tijdslimiet voor het retourneren van een resultaat overschrijdt, wordt de foutcode 53400 gegenereerd. |
| Gelijktijdige gebruikers van Query Service | <ul><li>Zoals gespecificeerd in de productbeschrijving van de toepassing.</li><li>+5 (met elke extra Ad-hocpakket voor gebruikers van add-on aangeschaft)</li></ul> | Door het systeem afgedwongen geleiding | Hiermee bepaalt u hoeveel gebruikers sessies tegelijk voor een bepaalde organisatie kunnen maken. Als de gelijktijdige limiet wordt overschreden, ontvangt de gebruiker een `Session Limit Reached` -fout. |
| Gelijktijdige zoekopdracht | <ul><li>Zoals gespecificeerd in de productbeschrijving van de toepassing.</li><li>+1 (met elke extra aangeschafte SKU-pack voor Ad hoc-querygebruikers)</li></ul> | Door het systeem afgedwongen geleiding | Dit bepaalt hoeveel vragen gelijktijdig voor een bepaalde organisatie kunnen worden uitgevoerd. Als de gelijktijdige limiet wordt overschreden, worden de query&#39;s in een wachtrij geplaatst. |
| Client-connector en resultaatuitvoerlimiet | Clientconnector<ul><li>Query-gebruikersinterface (100 rijen)</li><li>Client van derden (50.000)</li><li>[!DNL PostgresSQL] client (50.000)</li></ul> | Door het systeem afgedwongen geleiding | Het resultaat van een vraag kan door de volgende middelen worden ontvangen:<ul><li>Gebruikersinterface Query Service</li><li>Client van derden</li><li>[!DNL PostgresSQL] client</li></ul>Opmerking: het toevoegen van een beperking aan het uitvoeraantal kan sneller resultaten opleveren. Bijvoorbeeld `LIMIT 5` , `LIMIT 10` , enzovoort. |
| Resultaten geretourneerd via | Gebruikersinterface client | N.v.t. | Hiermee bepaalt u hoe de resultaten ter beschikking worden gesteld van de gebruikers. |

{style="table-layout:auto"}

**de vragen van de Partij**

| **Guardrail** | **Grens** | **Type van Grens** | **Beschrijving** |
|---|---|---|---|
| Maximale uitvoeringstijd | 24 uur | Door het systeem afgedwongen geleiding | Dit bepaalt de maximumuitvoeringstijd voor een partijSQL vraag.<br> de verwerkingstijd van een vraag is afhankelijk van het volume van te verwerken gegevens en vraagingewikkeldheid. |
| Gelijktijdige gebruikers van Query-service voor niet-geplande batch | <ul><li>Zoals gespecificeerd in de productbeschrijving van de toepassing.</li><li>+5 (met elke extra Ad-hocpakket voor gebruikers van add-on aangeschaft)</li></ul> | Door het systeem afgedwongen geleiding | Voor ongeplande partijvragen (bijvoorbeeld vragen CTAS/ITAS op interactieve wijze), bepaalt dit hoeveel gebruikers zittingen voor een bepaalde organisatie gelijktijdig kunnen tot stand brengen. Als de gelijktijdige limiet wordt overschreden, ontvangt de gebruiker een `Session Limit Reached` -fout. |
| Gelijktijdige gebruikers van Query-service voor geplande batch | Geen gebruikersbeperking | N.v.t. | Gepland partijvragen zijn asynchrone banen zodat is er geen gebruikersbeperking. |
| Rekenuren voor batchverwerking | Zoals gespecificeerd in de Adobe Experience Platform Intelligence Query Custom SKU-verkooporder van de klant | Prestatiegerichting | Dit bepaalt de scoped hoeveelheid verwerkingstijd per jaar een klant voor het uitvoeren van partijvragen wordt toegestaan om, gegevens terug in het gegevens meer af te tasten te verwerken en te schrijven. |
| Gelijktijdige zoekopdracht | Ondersteund | N.v.t. | Gepland partijvragen zijn asynchrone banen, daarom worden de gezamenlijke vragen gesteund. |
| Clientconnector en uitvoerlimiet van resultaat | Clientconnector<ul><li>Query-gebruikersinterface (geen bovenlimiet voor rijen)</li><li>Client van derden (geen bovenlimiet voor rijen)</li><li>[!DNL PostgresSQL] client (geen bovenlimiet voor rijen)</li><li>REST API&#39;s (geen bovengrens voor rijen)</li></ul> | Door het systeem afgedwongen geleiding | Het resultaat van een query kan op de volgende manieren beschikbaar worden gemaakt:<ul><li>Kan worden opgeslagen als afgeleide gegevenssets</li><li>Kan in de bestaande afgeleide gegevenssets worden opgenomen</li></ul>Nota: Er is geen bovengrens aan het aantal van het verslagaantal van het vraagresultaat. |
| Resultaten geretourneerd via | Gegevensset | N.v.t. | Hiermee bepaalt u hoe de resultaten ter beschikking worden gesteld van de gebruikers. |

{style="table-layout:auto"}

## Winkel met query-versnelling {#query-accelerated-store}

De lijst hieronder verstrekt de geadviseerde guardrailgrenzen en beschrijving voor de vraag versnelde opslag.

| Guardrail | Limiet | Type limiet | Beschrijving |
|---|---|---|---|
| Gelijktijdige zoekopdracht | 4 | Door het systeem afgedwongen geleiding | Om ervoor te zorgen dat de vragen over samengevoegde gegevens via rapporteringsAPI (met inbegrip van vragen die gegevensmodellen zoals de gegevensmodellen van Real-Time CDP verbeteren) de middelen hebben om efficiënt uit te voeren, houdt het rapporterende API middelgebruik door de opeenvolgingen van de wisselingscapaciteit aan elke vraag toe te wijzen. Het systeem zet vragen in een rij en wacht tot de opeenslagen van de gelijktijdige dienst beschikbaar worden of zij van het geheime voorgeheugen kunnen worden gediend. Een maximum van vier gezamenlijke vraaggroeven is beschikbaar op elk bepaald ogenblik.<br> als u tot het melden API door een hulpmiddel van BI toegang hebt en meer gelijktijdige uitvoering vereist, wordt een server van BI vereist. |

{style="table-layout:auto"}

## Volgende stappen

Na het lezen van dit document zou u een beter inzicht in de standaardgrenzen voor vraaguitvoering met de beschikbare vraagpatronen moeten hebben.

Zie de volgende documentatie voor meer informatie over de Dienst van de Vraag:

* [Query Service-API](./api/getting-started.md)
* [Gebruikersinterface Query Service](./ui/overview.md)

Raadpleeg de volgende documentatie voor meer informatie over andere Experience Platform Services-instructies, informatie over end-to-end latentie en licentiegegevens uit Real-Time CDP Product Description-documenten:

* [Real-Time CDP guardrails](/help/rtcdp/guardrails/overview.md)
* [ de diagrammen van de de latentie van begin tot eind ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=nl-NL#end-to-end-latency-diagrams) voor diverse diensten van Experience Platform.
* [ Real-Time Customer Data Platform (B2C Uitgave - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2P - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2B - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)