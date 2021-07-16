---
title: Veelgestelde vragen
description: Antwoorden op veelgestelde vragen over tags in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Handleiding voor het oplossen van problemen met tags

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](./term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Dit document bevat antwoorden op veelgestelde vragen over tags in Adobe Experience Platform.

## Wat zijn labels?

Tags zijn de volgende generatie mogelijkheden voor tagbeheer die door Adobe worden geboden en die in Adobe Experience Platform zijn ingebouwd. Met labels kunnen clients:

- Webproducten aan de clientzijde implementeren met behulp van integratie die *extensions* wordt genoemd
- Dynamisch leveren van configuratie om clientimplementaties bij te werken in systeemeigen mobiele toepassingen
- Op consistente wijze gegevens vastleggen, definiëren, beheren en uitwisselen tussen marketing- en advertentieproducten van andere leveranciers en van Adobe

De markeringen zijn een geavanceerd code en systeem van de configuratielevering dat voorwaarden evalueert en acties uitvoert om cliënt-zijbibliotheken en producten efficiënt en effectief op te stellen. Zij verstrekken ook een hoogst scalable benadering van het beheren van en het bouwen van integratie en hebben een robuuste reeks APIs voor programmatic interactie.

## Hoeveel kost tags?

Er worden geen extra kosten in rekening gebracht voor tags. Deze zijn beschikbaar voor elke [!DNL Adobe Experience Cloud]-klant.

## Ik hoorde dat er nu plug-ins zijn. Waar gaat het om?

Tags zijn ingebouwd in de Adobe Experience Platform en zijn volledig uitbreidbaar. De klanten, de Partners van de Adobe, de bureaus, en marketing of reclametechnologieleveranciers kunnen een markeringsuitbreiding bouwen die nieuwe functionaliteit toevoegt of bestaande functionaliteit wijzigt. Het systeem staat partners en cliënten toe om, hun eigen integraties te bouwen te beheren en bij te werken. Dit is slechts één manier Adobe opent Adobe Experience Platform zodat kunnen de klanten en de partners producten en ondernemingen op het bouwen. Dit helpt iedereen Adobe technologie aan marketing en reclametechnologieën van andere verkopers met meer gemak verbinden.

## Zijn alle extensies van derden meteen beschikbaar?

Er zijn al extensies beschikbaar voor Adobe-oplossingen en een groot en groeiend aantal onafhankelijke analytische, marketing-, reclame- en toestemmingsleveranciers en -technologieën. We blijven samenwerken met onze partners om het ecosysteem uit te breiden. Omdat de uitbreidingen door de technologieeigenaars kunnen worden gebouwd, worden beheerd en worden bijgewerkt, moeten de klanten niet op Adobe engineering wachten om hen te bouwen.

## Wanneer kunnen de cliënten of de partners uitbreidingen bouwen?

Tags hebben het vrijwel zelfbedieningsportaal geopend, dat extensieontwikkelaars kunnen gebruiken om hun eigen integratie met de Adobe Cloud Platform te bouwen.

Wij hebben vele klanten die ook verkiezen om hun eigen privé uitbreidingen voor gebruik slechts binnen hun eigen bedrijven te bouwen gebruikend de zelfde methodes van de uitbreidingsontwikkeling.

## Voldoen de labels aan de beveiligingsnormen van mijn bedrijf?

Tags zijn gereed voor SOC-2 en Gramm-Leach-Bliley Act. Tags bieden ook de mogelijkheid om zelf te worden gehost. JavaScript-bibliotheken en mobiele configuraties kunnen via uw eigen servers of de CDN van uw keuze worden aangeboden. Voor IT. en veiligheidsteams, geeft dit u de capaciteit om geautomatiseerde het testen in werking te stellen, de dossiers in uw eigen systeem van de versiecontrole te controleren, en om volledig om het even welke interne processen van de productiemigratie, veiligheid-gerelateerd of anders te voldoen.

## Wanneer kan ik naar tags gaan?

Nu is het de beste tijd om over te gaan naar labels. Door het migratieproces kunt u uw DTM-eigenschappen eenvoudig naar codes kopiëren. We raden uitgebreide tests aan, maar we hebben zoveel mogelijk geautomatiseerd (geen wijzigingen in de on-page-insluiting en geautomatiseerde migratie van regels en gegevenselementen).

## Ondersteunt tags apps van één pagina en mijn favoriete framework?

Ja. Tags bieden gebruikers en extensieontwikkelaars de mogelijkheid om gegevens te verzamelen, te beheren en te verspreiden binnen toepassingen van één pagina of Ajax-pagina&#39;s of sites. Dit geldt ongeacht uw voorkeuren voor het ontwikkelframework, of dat nu Angular, React.js, Ember, Meteor enzovoort is.

## Tags ondersteunen dynamische gegevenslagen?

Ja. Tags bevatten een extensie die gespecialiseerd is in het luisteren naar wijzigingen in dynamische gegevenslagen.

## Welke gebeurtenistypen worden door labels ondersteund?

Gebeurtenistypen zijn beschikbaar via extensies. De hoeveelheid ondersteunde gebeurtenistypen varieert per extensie. De extensie YouTube bevat bijvoorbeeld vier typen videogebeurtenissen: afspelen, pauzeren, beëindigen en afspelen van de tijd. Door middel van extensies kunnen tags andere browsergebeurtenistypen of synthetische gebeurtenistypen ondersteunen, zoals specifieke reeksen bezoekersactiviteit.

## Zullen tags mijn website versnellen (of vertragen)?

Tags zijn ontworpen om marketing- en advertentietechnologieën zo efficiënt mogelijk op uw website te leveren en uit te voeren met de beste praktijken van vandaag. Als tags correct worden gebruikt, is bewezen dat ze de prestaties van websites verbeteren in plaats van alternatieve methoden die vergelijkbare functionaliteit bieden.

## Welke browsers ondersteunen tags?

Browserondersteuning voor tags:

- [!DNL Chrome] (laatste)
- [!DNL Safari] (laatste)
- [!DNL Firefox] (laatste)
- [!DNL Microsoft Edge] (laatste)
- [!DNL Internet Explorer] (10 en hoger)
- [!DNL iOS Safari] (laatste)
- [!DNL Android Chrome] (laatste)

Browserondersteuning voor de interface van de tagtoepassing:

- [!DNL Chrome] (laatste)
- [!DNL Safari] (laatste)
- [!DNL Firefox] (laatste)
- [!DNL Microsoft Edge] (laatste)

De meeste Adobe-clients maken gebruik van modernere webplatformfuncties in de huidige browsers om betere gebruikerservaring te creëren, waaronder toepassingen van één pagina en interactieve Ajax-zware websites en pagina&#39;s. Terwijl de meeste klanten naar modernere benaderingen met hun sites gaan, vragen ze om een oplossing zoals tags die deze benaderingen mogelijk maakt.

## Werken labels voor systeemeigen mobiele apps?

Ja! Tags ondersteunen nu mobiele eigenschappen en configuratie voor de nieuwe Adobe Experience Platform [Mobile SDK&#39;s](https://sdkdocs.com) om gegevensverzameling en -levering te implementeren in een systeemeigen mobiele app-omgeving. Raadpleeg [documentatie](https://sdkdocs.com) voor meer informatie.

## Wat als ik andere vragen heb?

Als u andere vragen hebt, kunt u deze in de Gemeenschap Adobe vragen op de pagina met hoofdcodes op [https://adobe.com/go/launchme](https://adobe.com/go/launchme).

Tags zijn slechts een voorbeeld van waar ons platform naartoe gaat: opener, beter geïntegreerd en zoals altijd toegewijd aan het succes van de klant.
