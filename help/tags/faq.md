---
title: Handleiding voor het oplossen van problemen met tags
description: Antwoorden op veelgestelde vragen over tags in Adobe Experience Platform.
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Handleiding voor het oplossen van problemen met tags

Dit document bevat antwoorden op veelgestelde vragen over tags in Adobe Experience Platform.

## Wat zijn labels?

Tags zijn de volgende generatie mogelijkheden voor tagbeheer die Adobe biedt en die in Adobe Experience Platform zijn ingebouwd. Met labels kunnen clients:

- Stel cliënt-zijWebproducten op gebruikend integratie genoemd *uitbreidingen*
- Dynamisch leveren van configuratie om clientimplementaties bij te werken in systeemeigen mobiele toepassingen
- Op consistente wijze gegevens vastleggen, definiëren, beheren en uitwisselen tussen marketing- en advertentieproducten van andere leveranciers en van Adobe

De markeringen zijn een geavanceerd code en systeem van de configuratielevering dat voorwaarden evalueert en acties uitvoert om cliënt-zijbibliotheken en producten efficiënt en effectief op te stellen. Zij verstrekken ook een hoogst scalable benadering van het beheren van en het bouwen van integratie en hebben een robuuste reeks APIs voor programmatic interactie.

## Hoeveel kost tags?

Er worden geen extra kosten in rekening gebracht voor tags. Deze zijn beschikbaar voor elke [!DNL Adobe Experience Cloud] -klant.

## Ik hoorde dat er nu plug-ins zijn. Waar gaat het om?

Tags zijn ingebouwd in de Adobe Experience Platform en zijn volledig uitbreidbaar. Klanten, Adobe Partners, bureaus en leveranciers van marketing- of advertentietechnologie kunnen een tagextensie bouwen die nieuwe functionaliteit toevoegt of bestaande functionaliteit wijzigt. Het systeem staat partners en cliënten toe om, hun eigen integraties te bouwen te beheren en bij te werken. Dit is slechts één manier waarop Adobe de Adobe Experience Platform opent, zodat klanten en partners producten en bedrijven kunnen bouwen. Dit helpt iedereen Adobe technologie aan marketing en reclametechnologieën van andere verkopers met meer gemak aan te sluiten.

## Zijn alle extensies van derden meteen beschikbaar?

Er zijn al extensies beschikbaar voor Adobe-oplossingen en een groot en groeiend aantal onafhankelijke analytische, marketing-, reclame- en toestemmingsleveranciers en -technologieën. We blijven samenwerken met onze partners om het ecosysteem uit te breiden. Omdat extensies kunnen worden gebouwd, beheerd en bijgewerkt door de technologieeigenaars, hoeven klanten niet te wachten op Adobe-engineering om ze te bouwen.

## Wanneer kunnen de cliënten of de partners uitbreidingen bouwen?

Tags hebben een vrijwel zelfbedieningsportaal geopend, dat door ontwikkelaars van extensies kan worden gebruikt om hun eigen integratie met het Adobe Cloud Platform te maken.

Wij hebben vele klanten die ook verkiezen om hun eigen privé uitbreidingen voor gebruik slechts binnen hun eigen bedrijven te bouwen gebruikend de zelfde methodes van de uitbreidingsontwikkeling.

Om een uitbreiding te ontwikkelen, controleer de [ pagina van het Overzicht van de Ontwikkeling van de Uitbreiding van de Uitbreiding ](./extension-dev/overview.md).

## Voldoen de labels aan de beveiligingsnormen van mijn bedrijf?

Tags zijn gereed voor SOC-2 en Gramm-Leach-Bliley Act. Tags bieden ook de mogelijkheid om zelf te worden gehost. JavaScript-bibliotheken en mobiele configuraties kunnen via uw eigen servers of de CDN van uw keuze worden aangeboden. Voor I.T. en veiligheidsteams, geeft dit u de capaciteit om geautomatiseerde het testen in werking te stellen, de dossiers in uw eigen systeem van de versiecontrole te controleren, en om volledig aan om het even welke interne processen van de productiemigratie, veiligheid-gerelateerd of anders te voldoen.

## Wanneer kan ik naar tags gaan?

Nu is het de beste tijd om over te gaan naar labels. Door het migratieproces kunt u uw DTM-eigenschappen eenvoudig naar codes kopiëren. We raden uitgebreide tests aan, maar we hebben zoveel mogelijk geautomatiseerd (geen wijzigingen in de on-page-insluiting en geautomatiseerde migratie van regels en gegevenselementen).

## Ondersteunt tags apps van één pagina en mijn favoriete framework?

Ja. Tags bieden gebruikers en extensieontwikkelaars de mogelijkheid om gegevens te verzamelen, te beheren en te verspreiden binnen toepassingen van één pagina of Ajax-pagina&#39;s of sites. Dit geldt ongeacht uw voorkeuren voor het ontwikkelframework, of dat nu Angular, React.js, Ember, Meteor enzovoort is.

## Tags ondersteunen dynamische gegevenslagen?

Ja. Tags bevatten een extensie die gespecialiseerd is in het luisteren naar wijzigingen in dynamische gegevenslagen.

## Welke gebeurtenistypen worden door labels ondersteund?

Gebeurtenistypen zijn beschikbaar via extensies. De hoeveelheid ondersteunde gebeurtenistypen varieert per extensie. De extensie YouTube bevat bijvoorbeeld vier typen videogebeurtenissen: afspelen, pauzeren, beëindigen en afspelen. Door middel van extensies kunnen tags andere browsergebeurtenistypen of synthetische gebeurtenistypen ondersteunen, zoals specifieke reeksen bezoekersactiviteit.

## Zullen tags mijn website versnellen (of vertragen)?

Tags zijn ontworpen om marketing- en advertentietechnologieën zo efficiënt mogelijk op uw website te leveren en uit te voeren met de beste praktijken van vandaag. Als tags correct worden gebruikt, is bewezen dat ze de prestaties van websites verbeteren in plaats van alternatieve methoden die vergelijkbare functionaliteit bieden.

## Welke browsers ondersteunen tags?

Zie gesteunde browsers [ hier ](./extension-dev/browsers.md).

De meeste Adobe-clients maken gebruik van modernere functies van webplatforms in de huidige browsers om een betere gebruikerservaring te creëren, waaronder toepassingen van één pagina en interactieve Ajax-zware websites en pagina&#39;s. Terwijl de meeste klanten naar modernere benaderingen met hun sites gaan, vragen ze om een oplossing zoals tags die deze benaderingen mogelijk maakt.

## Werken labels voor systeemeigen mobiele apps?

Ja! De markeringen steunen nu mobiele eigenschappen en configuratie voor nieuwe Adobe Experience Platform [ Mobiele SDKs ](https://sdkdocs.com) om gegevensinzameling en levering in een inheems mobiel toepassingsmilieu uit te voeren. Gelieve te bezoeken [ documentatie ](https://sdkdocs.com) om meer te leren.

## Waarom zegt de UI dat er een fout is opgetreden bij het laden van mijn account?

Als u een bericht ontvangt met de mededeling dat er een fout is opgetreden bij het laden van uw account, betekent dit dat uw account niet tot productprofielen voor tags behoort. Zie de gids op [ het leiden toestemmingen ](../collection/permissions.md) leren hoe te om een productprofiel in Adobe Admin Console te vormen om toegang tot de eigenschappen van de Inzameling van Gegevens in UI te verlenen.

## Waarom kan ik geen eigenschappen in UI toevoegen?

Als u bij het aanmelden bij de gebruikersinterface geen nieuwe eigenschappen kunt maken, betekent dit dat uw account niet tot een productprofiel behoort dat het recht Eigenschappen beheren heeft.

Zie de gids op [ het leiden toestemmingen ](../collection/permissions.md) leren hoe te om een productprofiel in Adobe Admin Console te vormen om het Manage recht van Eigenschappen te verlenen. Voor meer informatie over de verschillende rechten voor markeringen, zie het overzicht op [ gebruikerstoestemmingen voor markeringen ](./ui/administration/user-permissions.md).

## Wat als ik andere vragen heb?

Als u andere vragen hebt, kunt u op de [ de communautaire pagina van de Inzameling van Gegevens van Adobe Experience Platform ](https://adobe.com/go/launchme) op Experience League vragen, of zich bij de [ gemeenschapSlack werkruimte ](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform) voor ontwikkelaars &amp; technische implementatieonderwerpen aansluiten.
