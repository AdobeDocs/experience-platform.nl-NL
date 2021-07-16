---
title: Overzicht van doorzending van gebeurtenissen
description: Leer over gebeurtenis door:sturen in Adobe Experience Platform, die u toestaat om het Netwerk van de Rand van het Platform te gebruiken om taken uit te voeren zonder uw markeringsimplementatie te veranderen.
source-git-commit: 7a6bec77895458cf1735bc7a00d16b78df9776a5
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 1%

---

# Overzicht van het doorsturen van gebeurtenissen

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Het doorsturen van gebeurtenissen in Adobe Experience Platform vermindert het gewicht van de webpagina en de toepassing door Adobe Experience Platform Edge Network te gebruiken om taken uit te voeren die normaal op de client worden uitgevoerd. De gebeurtenis die regels door:sturen kan gegevens omzetten en verzenden naar nieuwe bestemmingen zonder cliënt-zijimplementaties te veranderen.

Het door:sturen van gebeurtenissen in combinatie met het Web van Adobe Experience Platform en Mobiele SDKs maakt het mogelijk om:

* Maak één enkele vraag van de pagina die een lading van gegevens bevat. De gegevens federaliseren dan server-kant om cliënt-zijnetwerkverkeer te verminderen en een snellere ervaring voor klanten te leveren.
* Verlaag de tijd die het duurt voordat webpagina&#39;s worden geladen, zodat uw site voldoet aan de best practices van de branche op het gebied van prestaties.
* Verhoog de transparantie en controleer welke gegevenstypen naar de andere tag-eigenschappen worden verzonden.
* Creeer een gebeurtenis-door:sturen regel om eerder gevolgde gegevens naar een nieuwe bestemming te verzenden.

## Verbeterde prestaties

In een steeds concurrerender omgeving moeten bedrijven prioriteit geven aan prestaties om marktaandeel te behouden en uit te breiden. Het door:sturen van gebeurtenissen verbetert website en toepassingsprestaties over mobiele, IoT, en OTT apparaten. De conversiesnelheden van websites kunnen stijgen als gevolg van snellere laadtijden, mobiele apps leiden niet zo snel tot het afvoeren van batterijen en OTT-apps hebben hetzelfde gevoel als toepassingen die op mobiele apparaten worden uitgevoerd. Naarmate de prestaties toenemen, neemt ook de conversiegraad toe.

## Betere gegevensgovernance

Aangezien de technologiestapel groeit en het gegeven wordt verzonden naar meer en meer bestemmingen, de uitdaging om te controleren welke gegevens worden verzonden waar moeilijker wordt. De normalisatie van regels zoals de GDPR en de CCPA dwingt bedrijven meer controle uit te oefenen over een gegevensprobleem dat steeds moeilijker wordt.

Het door:sturen van de gebeurtenis helpt marketing teams hun zaken kweken terwijl het controleren van gegevens. Het vermindert het aantal cliënt-zijtechnologieën die de marketers moeten gebruiken om hun doelmarkt te bereiken en gegevens naar niet-Adobe bestemmingen te verzenden. Dit maakt het voor implementatieteams gemakkelijker om de gegevens te beheren die van de cliënt aan diverse bestemmingen stromen.

## Verschillen tussen het doorsturen van gebeurtenissen en tags

Het is belangrijk om op de volgende verschillen tussen gebeurtenis te letten die en markeringen door:sturen:

* Tokenisering gegevenselement

   * Tags: In een regel worden gegevenselementen aan het begin en einde van de naam van het gegevenselement gekoppeld met een `%`. Bijvoorbeeld, `%viewportHeight%`.

   * Gebeurtenis doorsturen: In een regel worden gegevenselementen aan het begin en `}}` aan het einde van de naam van het gegevenselement gekoppeld. `{{` Bijvoorbeeld, `{{viewportHeight}}`.

* Hoe wordt verwezen naar gegevens

   Als u wilt verwijzen naar gegevens van het Edge-netwerk, moet het pad voor het gegevenselement `arc.event._<element>_` zijn.

   `arc` staat voor Adobe Response Context.

   Bijvoorbeeld: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Als dit pad onjuist is opgegeven, worden geen gegevens verzameld.


* Reeks handelingen

   In de sectie van de Actie van een regel, gebeurtenis die regels door:sturen wordt altijd opeenvolgend uitgevoerd. Zorg ervoor dat de volgorde van de handelingen correct is wanneer u een regel opslaat. Deze uitvoeringsreeks kan niet worden gekozen zoals dit kan met tags.

* JavaScript-versies voor aangepaste code

   Tags gebruiken JavaScript-versie es5. Voor het doorsturen van gebeurtenissen wordt versie es6 gebruikt.

<!--doc Adobe Cloud Connector extension, get from Jon-->
