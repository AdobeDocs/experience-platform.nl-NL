---
title: Aanvullende informatie
description: De meest recente releaseopmerkingen voor tags in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 2056f7f6e7372fa1dee2e975a75e7ba3b8dfe518
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Aanvullende informatie

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

## 15 november 2021

**ES6-code in tags accepteren** - Extensies en aangepaste code met ES6-code kunnen nu worden gebruikt in tags. In de extensiecatalogus wordt een ES6+-label weergegeven in de kaart van elke extensie die ES6-code bevat. IE10 en IE11 ondersteunen geen ES6-code. Voordat u ES6-code gebruikt in uw tagbibliotheken, moet u uw uiterste best doen.

**Terser gebruiken als JavaScript-compressor** - Uglifier is vervangen door Terser. Vanaf deze release worden alle tagbibliotheken geminiateerd door Terser.

## 21 oktober 2021

**Gegevens verzenden naar geverifieerde eindpunten bij het doorsturen van gebeurtenissen** - Gebruikend geheimen, kunt u gegevens naar eindpunten verzenden die de volgende authentificatieprotocollen vereisen:

* **[!UICONTROL Token]**: Een enkele tekenreeks met tekens die een verificatietoken-waarde vertegenwoordigt.
* **[!UICONTROL Simple HTTP]**: Bevat twee tekenreekskenmerken voor een gebruikersnaam en wachtwoord.
* **[!UICONTROL OAuth2]**: Bevat diverse kenmerken die de [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) specificatie.

Zie de hulplijnen op voor meer informatie [het beheren van geheimen in de UI van de Inzameling van Gegevens](../ui/event-forwarding/secrets.md) of [geheimen beheren in de Reactor-API](../api/guides/secrets.md).

## 19 juli 2021

**Aanpassingen aan het recht &quot;Eigenschappen beheren&quot;** - Het beheerrecht van Eigenschappen kwam een kwestie tegen waar een gebruiker de toestemming had om een nieuw bezit tot stand te brengen maar kon het niet zien nadat het werd gecreeerd (zoals die in de communautaire draad wordt geschetst [hier](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176)). Een moeilijke situatie is nu levend met toestemmingen die worden afgedwongen zoals die in het artikel worden beschreven.

>[!NOTE]
>
>Als u het nieuwe recht &quot;Edit Bezit&quot;aan een gebruikersgroep toewijst, zal UI niet bijwerken om de gebieden in het scherm van de bezitsconfiguratie toe te laten. In een volgende release wordt een oplossing voor dit probleem geïmplementeerd.

## 17 mei 2021

**Betere verwerking van niet-opgeslagen wijzigingen** - Het was altijd zo dat wanneer u vanaf een montagesmening (uitbreidingen, gegevenselementen, en regelcomponenten) navigeerde, u een herinnering op zou krijgen of u uw veranderingen wilde verwerpen. Maar de logica om dat te bepalen was niet geweldig, dus de meeste tijd werd u ertoe aangezet om veranderingen te bewaren alhoewel er geen waren.  Dat is opgelost.  Van nu af aan zou u die herinnering slechts moeten zien wanneer u daadwerkelijk veranderingen hebt aangebracht.

## 10 mei 2021

**Vereenvoudigde publicatie** - Het bouwen aan de testomgeving is niet langer nodig.  Als u over de juiste rechten beschikt, kunt u de staat Ingediend volledig overslaan en rechtstreeks vanuit Development publiceren zolang u een geslaagde build hebt uitgevoerd en er geen andere bibliotheken upstream zijn.

## 22 april 2021

**Gegevensverzameling in Adobe Experience Platform** - Het verzenden van gegevens naar Adobe gaat niet alleen over het implementeren van tags naar uw site of configuratie naar uw app.  Het gebruik van de Experience Platform SDKs en het Netwerk van de Rand vereist toegang tot andere mogelijkheden van het Platform.  Dit vereiste vroeger om zich in een paar verschillende hulpmiddelen te registreren, maar nu zijn zij samen op één plaats.

De Inzameling van gegevens in Platform bestaat uit zes mogelijkheden, en uw onlangs gestroomlijnde navigatie zal slechts de punten bevatten die uw bedrijf en gebruikersrekening toegang hebben tot.  Sommige capaciteitsnamen zijn ook bijgewerkt om Experience Platform noemende patronen aan te passen.

* Client (voorheen geopend als Client Side)
* Gegevensstromen (die vroeger als Configuraties van de Rand werden betreden)
* Server (voorheen geopend als serverzijde)
* App Configurations
* Schema&#39;s
* Identiteiten

De blik kijkt naar meer updates aangezien de Inzameling van Experience Platform en van Gegevens zich blijft ontwikkelen.

## 18 februari 2021

* De interface voor gegevensverzameling is bijgewerkt met responsspectrum v3
* Bijgewerkte uitbreidingskaarten aan de recentste patronen van het Spectrum
* De naamvelden zijn in de hele app groter geworden

## 13 januari 2021

**Algemene beschikbaarheid: Gebeurtenis doorsturen** Verzend gegevens op gebeurtenisniveau naar het Adobe Experience Platform Edge-netwerk en gebruik vervolgens gebeurtenis die wordt doorgestuurd om die gegevens te transformeren, te verrijken en te verzenden naar een niet-Adobe-eindpunt dat Adobe gebruikt, niet de client, met lage latentie.

Zie de [overzicht van gebeurtenissen doorsturen](../ui/event-forwarding/overview.md) en [gids Aan de slag](../ui/event-forwarding/getting-started.md) voor meer informatie .
