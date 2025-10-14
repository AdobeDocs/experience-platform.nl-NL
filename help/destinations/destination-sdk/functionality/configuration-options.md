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

![&#x200B; Diagram die de componenten van Destination SDK, configuratieeindpunten, en de verrichtingen tonen door hen worden gesteund.](../assets/functionality/destination-sdk-components-diagram.png){zoomable="yes"}

>[!ENDSHADEBOX]

## Serverconfiguratie {#server-configuration}

De configuratie van de bestemmingsserver verbindt samen informatie over uw serverspecificaties en het malplaatje dat door Adobe wordt gebruikt om ladingen aan uw bestemming te leveren.

Hier geeft u bijvoorbeeld de API-eindpunten op die Experience Platform nodig heeft om verbinding te maken met de headers en de indeling van de API-aanroepen die Experience Platform zal uitvoeren.

Voor op bestanden gebaseerde doelen bevat deze configuratie ook de ondersteunde bestandsindelingen en compressie-indelingen voor uw doel. U kunt de hieronder beschreven functies vormen via het [&#x200B; bestemmings-servers eindpunt &#x200B;](../authoring-api/destination-server/create-destination-server.md).

* [&#x200B; specs van de Server &#x200B;](destination-server/server-specs.md): Een configuratiemalplaatje dat informatie over de opslagplaats of het eindpunt van HTTP bevat waar het gegeven wordt verzonden naar.
* [&#x200B; Sjabloon specs &#x200B;](destination-server/templating-specs.md): In dit malplaatje, kunt u bepalen hoe te om het HTTP API verzoek aan uw eindpunt te structureren, met inbegrip van hoe te om de gebieden van de profielattributen tussen het XDM schema en het formaat om te zetten dat uw platform steunt. Gebruik deze informatie samen met de [&#x200B; documentatie van het berichtformaat &#x200B;](destination-server/message-format.md).
* [&#x200B; formaat van het Bericht &#x200B;](destination-server/message-format.md): Deze sectie richt diepgaande informatie over gesteunde sjabloontalen, berichtformaten, en de informatie die door Adobe wordt vereist aan opstelling de integratie met uw platform. Gebruik deze informatie samen met de [&#x200B; malplaatjespecs &#x200B;](destination-server/templating-specs.md) documentatie.
* [&#x200B; specs van het Dossier &#x200B;](destination-server/file-formatting.md): Een configuratiemalplaatje dat het dossier het formatteren en compressieopties voor uw partijbestemming omvat.

## Doelconfiguratie {#destination-configuration}

Dit configuratieeindpunt bevat fundamentele en geavanceerde informatie over uw bestemming. Hier geeft u bijvoorbeeld de identiteitstypen op die uw bestemming kan ondersteunen, de gewenste indeling van geëxporteerde bestanden (voor op bestanden gebaseerde doelen) en diverse UI-kenmerken voor uw doelkaart in de gebruikersinterface van Adobe Experience Platform.

Zie de documentatie hieronder voor details over elk van de componenten van de bestemmingsconfiguratie. U kunt de hieronder beschreven functionaliteit vormen via het [&#x200B; bestemmingsparameter &#x200B;](../authoring-api/destination-configuration/create-destination-configuration.md).

* [&#x200B; de authentificatieconfiguratie van de Klant &#x200B;](destination-configuration/customer-authentication.md): Selecteer het authentificatiemechanisme dat Experience Platform zou moeten gebruiken om met uw bestemming te verbinden. Deze configuratie produceert [&#x200B; nieuwe bestemmings &#x200B;](../../ui/connect-destination.md) pagina in het gebruikersinterface van Experience Platform, waar de gebruikers Experience Platform met de rekeningen verbinden zij met uw bestemming hebben.
* [&#x200B; OAuth2 vergunning &#x200B;](destination-configuration/oauth2-authorization.md): Leer over alle [!DNL OAuth2] authentificatiestromen die door Destination SDK worden gesteund, en krijg instructies aan opstelling [!DNL OAuth2] authentificatie voor uw bestemming.
* [&#x200B; de gegevensgebieden van de Klant &#x200B;](destination-configuration/customer-data-fields.md): Leer hoe te om inputgebieden in Experience Platform UI tot stand te brengen die uw gebruikers toestaan om diverse informatie relevant voor te specificeren hoe te om gegevens aan uw bestemming te verbinden en uit te voeren.
* [&#x200B; attributen UI &#x200B;](destination-configuration/ui-attributes.md): Leer hoe te om de attributen UI, zoals de documentatiekoppeling, de categorie van de bestemmingskaart, en het type en de frequentie van de bestemmingsverbinding, voor bestemmingen te vormen die met Destination SDK worden gebouwd.
* [&#x200B; configuratie van het Schema &#x200B;](destination-configuration/schema-configuration.md): Leer hoe te om het doelschema van uw bestemming te bepalen waaraan de gebruikers profielattributen en identiteiten kunnen in kaart brengen.
* [&#x200B; Identiteit namespace configuratie &#x200B;](destination-configuration/identity-namespace-configuration.md): Leer hoe te om de identiteiten te vormen die door uw bestemming worden gesteund. Deze configuratie bevolkt de doelidentiteiten in de [&#x200B; toewijzingsstap &#x200B;](../../ui/activate-segment-streaming-destinations.md#mapping) van het gebruikersinterface van Experience Platform, waar de gebruikers identiteiten en attributen van hun XDM- schema&#39;s aan het schema in uw bestemming in kaart brengen.
* [&#x200B; levering van de Bestemming &#x200B;](destination-configuration/destination-delivery.md): Leer hoe te te vormen waar precies de uitgevoerde gegevens gaan en welke authentificatieregel in de plaats wordt gebruikt waar de gegevens zullen landen.
* [&#x200B; de meta-gegevensconfiguratie van het publiek &#x200B;](destination-configuration/audience-metadata-configuration.md): Leer hoe publieksmeta-gegevens zoals publieksnamen of IDs tussen Experience Platform en uw bestemming zouden moeten worden gedeeld.
* [&#x200B; het beleid van de Samenvoeging &#x200B;](destination-configuration/aggregation-policy.md): Leer hoe te opstelling een samenvoegingsbeleid om te bepalen hoe de verzoeken van HTTP aan uw bestemming zouden moeten worden gegroepeerd en worden gevangen.
* [&#x200B; de configuratie van de Partij &#x200B;](destination-configuration/batch-configuration.md): Opstelling diverse dossier het noemen en de uitvoer het plannen montages beschikbaar aan gebruikers wanneer het verbinden met uw bestemming in het gebruikersinterface van Experience Platform.
* [&#x200B; Historische profielkwalificaties &#x200B;](destination-configuration/historical-profile-qualifications.md): Leer over de historische profielkwalificaties die door bestemmingen worden gesteund die met Destination SDK worden gebouwd.

## Configuratie van metagegevens voor publiek {#audience-metadata-configuration}

Deze component staat u toe om te vormen hoe het publiek programmatically wordt gecreeerd, bijgewerkt, of geschrapt in uw bestemming. Voor op dossier-gebaseerde bestemmingen, staat het u toe om een bericht op te zetten wanneer de dossiers met succes aan uw bestemming worden geleverd. U kunt deze functionaliteit via het [&#x200B; publiek-malplaatjeeindpunt &#x200B;](../metadata-api/create-audience-template.md) vormen.

## Volgende stappen {#next-steps}

Door dit artikel te lezen, hebt u nu een algemeen overzicht van de functionaliteit die door Destination SDK wordt verstrekt en welke pagina&#39;s voor meer informatie over specifieke configuraties te lezen. Daarna, kunt u de gidsen lezen die alle stappen omvatten om [&#x200B; een het stromen &#x200B;](../guides/configure-destination-instructions.md) of a [&#x200B; op dossier-gebaseerde bestemming &#x200B;](../guides/configure-file-based-destination-instructions.md) te vormen door Destination SDK te gebruiken.
