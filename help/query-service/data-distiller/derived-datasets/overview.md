---
title: Afgeleide Datasets
description: De afgeleide datasets verstrekken een geschikte manier om datasets van uw keus te produceren die bij om het even welke regelmatige kring en naar keuze gepubliceerd in uw gegevens van het Profiel van de Klant in real time kunnen worden vernieuwd. Dit document verstrekt een overzicht van hoe te om de Dienst van de Vraag te gebruiken om afgeleide datasets voor gebruik met uw gegevens van het Profiel tot stand te brengen.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 7364da23c261d83681af605047a7cd7539f4a83f
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Afgeleide datasets

De afgeleide dataseteigenschap verstrekt een geschikte manier om datasets van uw keus van andere informatie te produceren beschikbaar in het gegevensmeer. Deze datasets kunnen bij om het even welke regelmatige kappigheid worden verfrist en naar keuze in uw gegevens van het Profiel van de Klant worden gepubliceerd in real time. De afgeleide datasets richten op de behoefte om complexe datasets zoals decile, percentile, en kwartiel over eenvoudigere degenen zoals maximum, telling, en gemiddelde te bouwen. Deze datasets kunnen specifiek voor een individuele gebruiker of voor een bedrijfsentiteit worden berekend. Dit laat u toe om datasets af te leiden die direct aan een herkenningsteken, zoals e-mailadressen, apparaat IDs, en telefoonaantallen kunnen worden geaccrediteerd, en ook datasets af te leiden die onrechtstreeks met dat gebruiker of bedrijfsprofiel worden geassocieerd.

De afgeleide datasets zijn nodig voor een verscheidenheid van gebruiksgevallen wanneer de gegevens op het gegevens meer worden geanalyseerd. Deze gegevens kunnen vervolgens worden gemarkeerd voor gebruik in Real-Time Klantprofiel en worden gebruikt in gevallen van downstreamgebruik, zoals het creëren van een sterk gericht publiek. U kunt deze functie bijvoorbeeld gebruiken in de volgende gevallen:

* De laagste 10% van de abonnees identificeren op basis van viewer per kanaal. Op die manier kunnen marketeers zich richten op een bepaald publiek en een nieuw abonneepakket verkopen.
* Een publiek identificeren dat zich in de top 10% van de vliegers bevindt op basis van hun totale afgelegde kilometers en de &quot;Flyer&quot;-status hebben. Dit publiek zou kunnen worden gebruikt om selectief de verkoop van een nieuw creditcardaanbod te richten.
* Bepaal de churn rate die op abonnement wordt gebaseerd.
* De top 1% van het gezinsinkomen in een provincie of staat identificeren en een maatstaf geven voor het aantal personen dat zich de laatste &quot;n&quot; maanden uit die collectieve groep heeft verplaatst.

## Complexe afgeleide gegevenssets

Om een rangschikking tot stand te brengen die op één of meerdere metriek (zoals opbrengst, kijkersduur, etc.) op een bepaalde dimensie (categorie) wordt gebaseerd, worden de complexe afgeleide datasets vereist. Decielen, kwartielen en percentielen maken flexibiliteit en nauwkeurigheid mogelijk wanneer gegevens met afgeleide gegevenssets worden gerangschikt.

Een decile is een methode om een reeks gerangschikte gegevens op te splitsen in tien gelijke delen. Wanneer de gegevens in deciles worden verdeeld, wordt een decile rang toegewezen aan elke rij in de gegevensreeks. Hierdoor kunnen de gegevens in aflopende of oplopende volgorde worden gesorteerd.

Bij een lagere rangschikking worden de gegevens gerangschikt op een schaal van 1 tot 10, waarbij elk opeenvolgend getal overeenkomt met een verhoging van 10 procentpunten.

Decile emmers vertegenwoordigen het aantal gerangschikte groepen en worden gebruikt om een ranking aan een dimensie (categorie) in de dataset toe te wijzen. Het emmertje kan een aantal of een uitdrukking zijn die tot een positieve geheelwaarde voor elke verdeling evalueert. De emmers mogen geen null-waarde hebben.

De kwartjes worden gebruikt om de verdeling door vier en percentielen door 100 te verdelen.

## Analytische afgeleide gegevensreeksen

De Dienst van de vraag verstrekt ingebouwde functies zoals sessionization en laatste aanraking, onder andere, die u op om het even welke gegevens van de tijdreeksen kunt toepassen om bedrijfsgerelateerde derivatendatasets te produceren. U hebt de optie om deze analytische afgeleide datasets op één of meerdere identiteit te baseren en naar keuze de gegevens aan het Profiel van de Klant in real time te publiceren indien vereist.

Sommige mogelijke gebruiksgevallen voor dit type van afgeleid attribuut zouden kunnen omvatten:

* Producten bijhouden die tijdens een gebruikerssessie zijn gescand en die niet in voorraad zijn.
* Veelgebruikte maatstaven zoals grootte, kleur of productcategorie bijhouden van de producten die worden gebladerd of aangeschaft.
* De platformbron volgen die tot een productbrowser of aankoop heeft geleid.
* Het onlangs doorbladerde item bijhouden op basis van een identiteit.
* Metrische gegevens bijhouden, zoals het gemiddelde aantal artikelen in een winkelwagentje, het verlaten van het winkelwagentje of de gemiddelde aankoopfrequentie.

## Andere afgeleide gegevensbestanden

U kunt bedrijfsmetriek als afgeleid attribuut ook berekenen en hen gebruiken samen met eenvoudige datasets zoals postcode of samengevoegde metrisch zoals totale telling. Bijvoorbeeld, een totaal aantal gebaseerd op een stad of een provincie, of totaal aantal gebaseerd op een bedrijfscategorie en een stad/provincie.

## Volgende stappen en gebruiksscenario&#39;s

Door dit document te lezen, hebt u een beter inzicht in hoe de Dienst van de Vraag afgeleide datasets complexe gebruiksgevallen voor het maximaliseren van het nut van uw gegevens vergemakkelijken. Daarna, zou u het [&#x200B; op decile-Gebaseerde afgeleide attributengebruik &#x200B;](../../use-cases/deciles-use-case.md) moeten lezen om te zien hoe deze eigenschap in een real-world scenario wordt toegepast.
