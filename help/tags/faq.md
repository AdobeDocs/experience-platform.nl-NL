---
title: Handleiding voor het oplossen van problemen met tags
description: Antwoorden op veelgestelde vragen over tags in Adobe Experience Platform.
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: 9701a14dc2915e0d6dcc6051c15d5113f305487f
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 0%

---

# Handleiding voor het oplossen van problemen met tags

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](./term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Dit document bevat antwoorden op veelgestelde vragen over tags in Adobe Experience Platform.

## Wat zijn labels?

Tags zijn de volgende generatie mogelijkheden voor tagbeheer die door Adobe worden geboden en die in Adobe Experience Platform zijn ingebouwd. Met labels kunnen clients:

- Webproducten aan de clientzijde implementeren met behulp van integraties die u noemt *extensions*
- Dynamisch leveren van configuratie om clientimplementaties bij te werken in systeemeigen mobiele toepassingen
- Op consistente wijze gegevens vastleggen, definiëren, beheren en uitwisselen tussen marketing- en advertentieproducten van andere leveranciers en van Adobe

De markeringen zijn een geavanceerd code en systeem van de configuratielevering dat voorwaarden evalueert en acties uitvoert om cliënt-zijbibliotheken en producten efficiënt en effectief op te stellen. Zij verstrekken ook een hoogst scalable benadering van het beheren van en het bouwen van integratie en hebben een robuuste reeks APIs voor programmatic interactie.

## Hoeveel kost tags?

Er worden geen extra kosten in rekening gebracht voor tags. Ze zijn beschikbaar voor alle [!DNL Adobe Experience Cloud] klant.

## Ik hoorde dat er nu plug-ins zijn. Waar gaat het om?

Tags zijn ingebouwd in de Adobe Experience Platform en zijn volledig uitbreidbaar. De klanten, de Partners van de Adobe, de bureaus, en marketing of reclametechnologieleveranciers kunnen een markeringsuitbreiding bouwen die nieuwe functionaliteit toevoegt of bestaande functionaliteit wijzigt. Het systeem staat partners en cliënten toe om, hun eigen integraties te bouwen te beheren en bij te werken. Dit is slechts één manier Adobe opent Adobe Experience Platform zodat kunnen de klanten en de partners producten en ondernemingen op het bouwen. Dit helpt iedereen Adobe technologie aan marketing en reclametechnologieën van andere verkopers met meer gemak verbinden.

## Zijn alle extensies van derden meteen beschikbaar?

Er zijn al extensies beschikbaar voor Adobe-oplossingen en een groot en groeiend aantal onafhankelijke analytische, marketing-, reclame- en toestemmingsleveranciers en -technologieën. We blijven samenwerken met onze partners om het ecosysteem uit te breiden. Omdat de uitbreidingen door de technologieeigenaars kunnen worden gebouwd, worden beheerd en worden bijgewerkt, moeten de klanten niet op Adobe engineering wachten om hen te bouwen.

## Wanneer kunnen de cliënten of de partners uitbreidingen bouwen?

Tags hebben het vrijwel zelfbedieningsportaal geopend, dat extensieontwikkelaars kunnen gebruiken om hun eigen integratie met de Adobe Cloud Platform te bouwen.

Wij hebben vele klanten die ook verkiezen om hun eigen privé uitbreidingen voor gebruik slechts binnen hun eigen bedrijven te bouwen gebruikend de zelfde methodes van de uitbreidingsontwikkeling.

Als u een extensie wilt ontwikkelen, checkt u de [Overzicht van Extension Development](./extension-dev/overview.md) pagina.

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

Zie de ondersteunde browsers [hier](./extension-dev/browsers.md).

De meeste Adobe-clients maken gebruik van modernere webplatformfuncties in de huidige browsers om betere gebruikerservaring te creëren, waaronder toepassingen van één pagina en interactieve Ajax-zware websites en pagina&#39;s. Terwijl de meeste klanten naar modernere benaderingen met hun sites gaan, vragen ze om een oplossing zoals tags die deze benaderingen mogelijk maakt.

## Werken labels voor systeemeigen mobiele apps?

Ja! Tags ondersteunen nu mobiele eigenschappen en configuratie voor de nieuwe Adobe Experience Platform [Mobiele SDK&#39;s](https://sdkdocs.com) het implementeren van gegevensverzameling en -levering in een systeemeigen mobiele app-omgeving. Ga naar [documentatie](https://sdkdocs.com) voor meer informatie.

## Waarom zegt de UI dat er een fout is opgetreden bij het laden van mijn account?

Als u een bericht ontvangt met de mededeling dat er een fout is opgetreden bij het laden van uw account, betekent dit dat uw account niet tot productprofielen voor tags behoort. Zie de handleiding op [machtigingen beheren](../collection/permissions.md) leren hoe te om een productprofiel in Adobe Admin Console te vormen om toegang tot de eigenschappen van de Inzameling van Gegevens in UI te verlenen.

## Waarom kan ik geen eigenschappen in UI toevoegen?

Als u geen nieuwe eigenschappen kunt maken wanneer u zich aanmeldt bij de gebruikersinterface, houdt dit in dat uw account niet tot een productprofiel behoort dat het recht Eigenschappen beheren heeft.

Zie de handleiding op [machtigingen beheren](../collection/permissions.md) om te leren hoe u een productprofiel in Adobe Admin Console configureert om het recht Eigenschappen beheren te verlenen. Voor meer informatie over de verschillende rechten voor tags raadpleegt u het overzicht over [gebruikersmachtigingen voor tags](./ui/administration/user-permissions.md).

## Wat als ik andere vragen heb?

Als u andere vragen hebt, kunt u vragen stellen over [Community-pagina voor Adobe Experience Platform-gegevensverzameling](https://adobe.com/go/launchme) op Experience League, of sluit zich aan bij [community Slack-werkruimte](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform) voor ontwikkelaars en technische implementatieonderwerpen.
