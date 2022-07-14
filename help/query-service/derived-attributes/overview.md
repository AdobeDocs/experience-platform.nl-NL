---
title: Afgeleide kenmerken
description: Afgeleide attributen verstrekken een geschikte manier om attributen van uw keus te produceren die bij om het even welke regelmatige kappigheid en naar keuze gepubliceerd in uw gegevens van het Profiel van de Klant in real time kunnen worden vernieuwd. Dit document biedt een overzicht van hoe u de Query-service kunt gebruiken om afgeleide kenmerken te maken voor gebruik met uw profielgegevens.
hide: true
hidefromtoc: true
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: ae11d6f622c42d08373b7454ef920a80abaf2425
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Afgeleide kenmerken

De afgeleide attributeneigenschap verstrekt een geschikte manier om attributen van uw keus van andere informatie te produceren beschikbaar in het gegevenspeer. Deze kenmerken kunnen op elke normale manier worden vernieuwd en optioneel worden gepubliceerd in uw gegevens van het profiel van de klant in realtime. Afgeleide attributen richten zich op de behoefte om complexe attributen zoals decile, percentiel, en kwartiel over eenvoudigere degenen zoals maximum, telling, en gemiddelde te bouwen. Deze eigenschappen kunnen specifiek voor een individuele gebruiker of voor een bedrijfsentiteit worden berekend. Hierdoor kunt u kenmerken afleiden die rechtstreeks aan een id kunnen worden geaccrediteerd, zoals e-mailadressen, apparaat-id&#39;s en telefoonnummers, en ook kenmerken afleiden die indirect aan dat gebruikers- of bedrijfsprofiel zijn gekoppeld.

Afgeleide attributen zijn nodig voor een verscheidenheid van gebruiksgevallen wanneer de gegevens op het gegevens meer worden geanalyseerd. Deze gegevens kunnen vervolgens worden gemarkeerd voor gebruik in het Real-time Klantprofiel en worden gebruikt in gevallen van downstreamgebruik, zoals het creëren van een sterk gericht publiek. U kunt deze functie bijvoorbeeld gebruiken in de volgende gevallen:

* De laagste 10% van de abonnees identificeren op basis van viewer per kanaal. Op die manier kunnen marketeers zich richten op een bepaald publiek en een nieuw abonneepakket verkopen.
* Een publiek identificeren dat zich in de top 10% van de vliegers bevindt op basis van hun totale afgelegde kilometers en de &quot;Flyer&quot;-status hebben. Dit publiek zou kunnen worden gebruikt om selectief de verkoop van een nieuw creditcardaanbod te richten.
* Bepaal de churn rate die op abonnement wordt gebaseerd.
* De top 1% van het gezinsinkomen in een provincie of staat identificeren en een maatstaf geven voor het aantal personen dat zich de laatste &quot;n&quot; maanden uit die collectieve groep heeft verplaatst.

## Complexe afgeleide kenmerken

Om een rangschikking tot stand te brengen die op één of meerdere metriek (zoals opbrengst, kijkerduur, etc.) op een bepaalde afmeting (categorie) wordt gebaseerd, worden de complexe afgeleide attributen vereist. Decielen, kwartielen en percentielen maken flexibiliteit en nauwkeurigheid mogelijk wanneer gegevens met afgeleide kenmerken worden gerangschikt.

Een decile is een methode om een reeks gerangschikte gegevens op te splitsen in tien gelijke delen. Wanneer de gegevens in deciles worden verdeeld, wordt een decile rang toegewezen aan elke rij in de gegevensreeks. Hierdoor kunnen de gegevens in aflopende of oplopende volgorde worden gesorteerd.

Bij een lagere rangschikking worden de gegevens gerangschikt op een schaal van 1 tot 10, waarbij elk opeenvolgend getal overeenkomt met een verhoging van 10 procentpunten.

Decile emmers vertegenwoordigen het aantal gerangschikte groepen en worden gebruikt om een ranking aan een dimensie (categorie) in de dataset toe te wijzen. Het emmertje kan een aantal of een uitdrukking zijn die tot een positieve geheelwaarde voor elke verdeling evalueert. De emmers mogen geen null-waarde hebben.

De kwartjes worden gebruikt om de verdeling door vier en percentielen door 100 te verdelen.

## Analytische afgeleide kenmerken

De Dienst van de vraag verstrekt ingebouwde functies zoals sessionization en laatste aanraking, onder andere, die u op om het even welke gegevens van de tijdreeksen kunt toepassen om zaken verwante afleidingsattributen te produceren. U kunt deze analytische afgeleide kenmerken baseren op een of meer identiteiten en de gegevens desgewenst publiceren naar het realtime profiel van de klant.

Sommige mogelijke gebruiksgevallen voor dit type van afgeleid attribuut zouden kunnen omvatten:

* Producten bijhouden die tijdens een gebruikerssessie zijn gescand en die niet in voorraad zijn.
* Veelgebruikte maatstaven zoals grootte, kleur of productcategorie bijhouden van de producten die worden gebladerd of aangeschaft.
* De platformbron volgen die tot een productbrowser of aankoop heeft geleid.
* Het onlangs doorbladerde item bijhouden op basis van een identiteit.
* Metrische gegevens bijhouden, zoals het gemiddelde aantal artikelen in een winkelwagentje, het verlaten van het winkelwagentje of de gemiddelde aankoopfrequentie.

## Overige afgeleide kenmerken

U kunt bedrijfsmetriek ook als afgeleid attribuut berekenen en hen gebruiken samen met eenvoudige attributen zoals postcode of een samengevoegde metrisch zoals totale telling. Bijvoorbeeld, een totaal aantal gebaseerd op een stad of een provincie, of totaal aantal gebaseerd op een bedrijfscategorie en een stad/provincie.

## Volgende stappen en gebruiksgevallen

Door dit document te lezen hebt u een beter inzicht in hoe de Dienst van de Vraag afgeleide attributen complexe gebruiksgevallen voor het maximaliseren van het nut van uw gegevens vergemakkelijken. Lees nu de [op decile gebaseerde, afgeleide gebruikscase van kenmerken](./deciles-use-case.md) om te zien hoe deze eigenschap in een real-world scenario wordt toegepast.
