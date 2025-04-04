---
description: De bestemmingsdienst in Adobe Experience Platform gebruikt configuratieeindpunten voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen. Leer hoe deze componenten gecombineerd Experience Platform toestaan om met bestemmingspartners te verbinden, douaneberichten te verzenden, en profielgegevens over het digitale ecosysteem te activeren.
title: Configuratieopties in Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Configuratieopties in Destination SDK

De bestemmingsdienst in Adobe Experience Platform gebruikt configuratieeindpunten voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen.

In combinatie hiermee kan Experience Platform verbinding maken met doelplatforms, aangepaste berichten verzenden, aangepaste bestanden exporteren en profielgegevens activeren in het digitale ecosysteem.

Het diagram hieronder toont een overzicht op hoog niveau van de componenten die u door Destination SDK kunt vormen om uw eigen bestemming te bouwen. Deze componenten worden hieronder nader beschreven.

>[!BEGINSHADEBOX]

![ Diagram die de componenten van Destination SDK, configuratieeindpunten, en de verrichtingen tonen door hen worden gesteund.](../assets/functionality/destination-sdk-components-diagram.png){zoomable="yes"}

>[!ENDSHADEBOX]

## Serverconfiguratie {#server-configuration}

De configuratie van de bestemmingsserver verbindt samen informatie over uw serverspecificaties en het malplaatje dat door Adobe wordt gebruikt om ladingen aan uw bestemming te leveren.

Hier geeft u bijvoorbeeld de API-eindpunten op die Experience Platform nodig heeft om verbinding te maken met de headers en de indeling van de API-aanroepen die Experience Platform zal uitvoeren.

Voor op bestanden gebaseerde doelen bevat deze configuratie ook de ondersteunde bestandsindelingen en compressie-indelingen voor uw doel. U kunt de hieronder beschreven functies vormen via het [ bestemmings-servers eindpunt ](../authoring-api/destination-server/create-destination-server.md).

* [ specs van de Server ](destination-server/server-specs.md): Een configuratiemalplaatje dat informatie over de opslagplaats of het eindpunt van HTTP bevat waar het gegeven wordt verzonden naar.
* [ Sjabloon specs ](destination-server/templating-specs.md): In dit malplaatje, kunt u bepalen hoe te om het HTTP API verzoek aan uw eindpunt te structureren, met inbegrip van hoe te om de gebieden van de profielattributen tussen het XDM schema en het formaat om te zetten dat uw platform steunt. Gebruik deze informatie samen met de [ documentatie van het berichtformaat ](destination-server/message-format.md).
* [ formaat van het Bericht ](destination-server/message-format.md): Deze sectie richt diepgaande informatie over gesteunde sjabloontalen, berichtformaten, en de informatie die door Adobe wordt vereist aan opstelling de integratie met uw platform. Gebruik deze informatie samen met de [ malplaatjespecs ](destination-server/templating-specs.md) documentatie.
* [ specs van het Dossier ](destination-server/file-formatting.md): Een configuratiemalplaatje dat het dossier het formatteren en compressieopties voor uw partijbestemming omvat.

## Doelconfiguratie {#destination-configuration}

Dit configuratieeindpunt bevat fundamentele en geavanceerde informatie over uw bestemming. Hier geeft u bijvoorbeeld de identiteitstypen op die uw bestemming kan ondersteunen, de gewenste indeling van geëxporteerde bestanden (voor op bestanden gebaseerde doelen) en diverse UI-kenmerken voor uw doelkaart in de gebruikersinterface van Adobe Experience Platform.

Zie de documentatie hieronder voor details over elk van de componenten van de bestemmingsconfiguratie. U kunt de hieronder beschreven functionaliteit vormen via het [ bestemmingsparameter ](../authoring-api/destination-configuration/create-destination-configuration.md).

* [ de authentificatieconfiguratie van de Klant ](destination-configuration/customer-authentication.md): Selecteer het authentificatiemechanisme dat Experience Platform zou moeten gebruiken om met uw bestemming te verbinden. Deze configuratie produceert [ nieuwe bestemmings ](../../ui/connect-destination.md) pagina in het gebruikersinterface van Experience Platform, waar de gebruikers Experience Platform met de rekeningen verbinden zij met uw bestemming hebben.
* [ OAuth2 vergunning ](destination-configuration/oauth2-authorization.md): Leer over alle [!DNL OAuth2] authentificatiestromen die door Destination SDK worden gesteund, en krijg instructies aan opstelling [!DNL OAuth2] authentificatie voor uw bestemming.
* [ de gegevensgebieden van de Klant ](destination-configuration/customer-data-fields.md): Leer hoe te om inputgebieden in Experience Platform UI tot stand te brengen die uw gebruikers toestaan om diverse informatie relevant voor te specificeren hoe te om gegevens aan uw bestemming te verbinden en uit te voeren.
* [ attributen UI ](destination-configuration/ui-attributes.md): Leer hoe te om de attributen UI, zoals de documentatiekoppeling, de categorie van de bestemmingskaart, en het type en de frequentie van de bestemmingsverbinding, voor bestemmingen te vormen die met Destination SDK worden gebouwd.
* [ configuratie van het Schema ](destination-configuration/schema-configuration.md): Leer hoe te om het doelschema van uw bestemming te bepalen waaraan de gebruikers profielattributen en identiteiten kunnen in kaart brengen.
* [ Identiteit namespace configuratie ](destination-configuration/identity-namespace-configuration.md): Leer hoe te om de identiteiten te vormen die door uw bestemming worden gesteund. Deze configuratie bevolkt de doelidentiteiten in de [ toewijzingsstap ](../../ui/activate-segment-streaming-destinations.md#mapping) van het gebruikersinterface van Experience Platform, waar de gebruikers identiteiten en attributen van hun XDM- schema&#39;s aan het schema in uw bestemming in kaart brengen.
* [ levering van de Bestemming ](destination-configuration/destination-delivery.md): Leer hoe te te vormen waar precies de uitgevoerde gegevens gaan en welke authentificatieregel in de plaats wordt gebruikt waar de gegevens zullen landen.
* [ de meta-gegevensconfiguratie van het publiek ](destination-configuration/audience-metadata-configuration.md): Leer hoe publieksmeta-gegevens zoals publieksnamen of IDs tussen Experience Platform en uw bestemming zouden moeten worden gedeeld.
* [ het beleid van de Samenvoeging ](destination-configuration/aggregation-policy.md): Leer hoe te opstelling een samenvoegingsbeleid om te bepalen hoe de verzoeken van HTTP aan uw bestemming zouden moeten worden gegroepeerd en worden gevangen.
* [ de configuratie van de Partij ](destination-configuration/batch-configuration.md): Opstelling diverse dossier het noemen en de uitvoer het plannen montages beschikbaar aan gebruikers wanneer het verbinden met uw bestemming in het gebruikersinterface van Experience Platform.
* [ Historische profielkwalificaties ](destination-configuration/historical-profile-qualifications.md): Leer over de historische profielkwalificaties die door bestemmingen worden gesteund die met Destination SDK worden gebouwd.

## Configuratie van metagegevens voor publiek {#audience-metadata-configuration}

Deze component staat u toe om te vormen hoe het publiek programmatically wordt gecreeerd, bijgewerkt, of geschrapt in uw bestemming. Voor op dossier-gebaseerde bestemmingen, staat het u toe om een bericht op te zetten wanneer de dossiers met succes aan uw bestemming worden geleverd. U kunt deze functionaliteit via het [ publiek-malplaatjeeindpunt ](../metadata-api/create-audience-template.md) vormen.

## Volgende stappen {#next-steps}

Door dit artikel te lezen, hebt u nu een algemeen overzicht van de functionaliteit die door Destination SDK wordt verstrekt en welke pagina&#39;s voor meer informatie over specifieke configuraties te lezen. Daarna, kunt u de gidsen lezen die alle stappen omvatten om [ een het stromen ](../guides/configure-destination-instructions.md) of a [ op dossier-gebaseerde bestemming ](../guides/configure-file-based-destination-instructions.md) te vormen door Destination SDK te gebruiken.
