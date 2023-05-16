---
description: De bestemmingsdienst in Adobe Experience Platform gebruikt configuratieeindpunten voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen. Leer hoe deze componenten gecombineerd Experience Platform toestaan om met bestemmingspartners te verbinden, douaneberichten te verzenden, en profielgegevens over het digitale ecosysteem te activeren.
title: Configuratieopties in Destination SDK
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# Configuratieopties in Destination SDK

De bestemmingsdienst in Adobe Experience Platform gebruikt configuratieeindpunten voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen.

Samen staan deze componenten Experience Platform toe om met bestemmingsplatforms te verbinden, douaneberichten te verzenden, douanedossiers uit te voeren, en profielgegevens over het digitale ecosysteem te activeren.

Het diagram toont hieronder een overzicht op hoog niveau van de componenten die u door Destination SDK kunt vormen om uw eigen bestemming te bouwen. Deze componenten worden hieronder nader beschreven.

![Diagram die de componenten van de Destination SDK, configuratieeindpunten, en de verrichtingen tonen door hen worden gesteund.](../assets/functionality/destination-sdk-components-diagram.png)

## Serverconfiguratie {#server-configuration}

De configuratie van de bestemmingsserver bindt samen informatie over uw serverspecificaties en het malplaatje dat door Adobe wordt gebruikt om ladingen aan uw bestemming te leveren.

Hier geeft u bijvoorbeeld de API-eindpunten op aan uw zijde waarmee het Experience Platform verbinding moet maken, evenals de headers en de indeling van de API-aanroepen die het Platform zal uitvoeren.

Voor op bestanden gebaseerde doelen bevat deze configuratie ook de ondersteunde bestandsindelingen en compressie-indelingen voor uw doel. U kunt de hieronder beschreven functies configureren via de [doel-servers eindpunt](../authoring-api/destination-server/create-destination-server.md).

* [Serverspecificaties](destination-server/server-specs.md): Een configuratiesjabloon dat informatie bevat over de opslaglocatie of het HTTP-eindpunt waarnaar gegevens worden verzonden.
* [Sjabloonspecificaties](destination-server/templating-specs.md): In dit malplaatje, kunt u bepalen hoe te om het HTTP API verzoek aan uw eindpunt te structureren, met inbegrip van hoe te om de gebieden van de profielattributen tussen het XDM schema en het formaat om te zetten dat uw platform steunt. Gebruik deze informatie samen met de [berichtindeling](destination-server/message-format.md) documentatie.
* [Berichtindeling](destination-server/message-format.md): In deze sectie wordt diepgaande informatie besproken over ondersteunde sjabloontalen, berichtindelingen en de informatie die Adobe nodig heeft om de integratie met uw platform in te stellen. Gebruik deze informatie samen met de [sjabloonspecificaties](destination-server/templating-specs.md) documentatie.
* [Bestandsspecificaties](destination-server/file-formatting.md): Een configuratiesjabloon dat de opties voor bestandsindeling en -compressie voor de batchbestemming bevat.

## Doelconfiguratie {#destination-configuration}

Dit configuratieeindpunt bevat fundamentele en geavanceerde informatie over uw bestemming. Hier geeft u bijvoorbeeld de identiteitstypen op die uw bestemming kan ondersteunen, de gewenste indeling van geëxporteerde bestanden (voor op bestanden gebaseerde doelen) en diverse UI-kenmerken voor uw doelkaart in de gebruikersinterface van Adobe Experience Platform.

Zie de documentatie hieronder voor details over elk van de componenten van de bestemmingsconfiguratie. U kunt de hieronder beschreven functies configureren via de [doelen, eindpunt](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configuratie van klantverificatie](destination-configuration/customer-authentication.md): Selecteer het authentificatiemechanisme dat het Experience Platform zou moeten gebruiken om met uw bestemming te verbinden. Deze configuratie genereert de [Nieuwe bestemming configureren](../../ui/connect-destination.md) pagina in het gebruikersinterface van het Experience Platform, waar de gebruikers Experience Platform met de rekeningen verbinden zij met uw bestemming hebben.
* [OAuth2-verificatie](destination-configuration/oauth2-authentication.md): Meer informatie over alle [!DNL OAuth2] verificatiestromen die worden ondersteund door Destination SDK en instructies krijgen voor het instellen [!DNL OAuth2] verificatie voor uw bestemming...
* [Gegevensvelden van de klant](destination-configuration/customer-data-fields.md): Leer hoe u invoervelden maakt in de interface van het Experience Platform waarmee uw gebruikers verschillende informatie kunnen opgeven die relevant is voor het maken van een verbinding en het exporteren van gegevens naar uw bestemming.
* [UI-kenmerken](destination-configuration/ui-attributes.md): Leer hoe te om de attributen UI, zoals de documentatiekoppeling, de categorie van de bestemmingskaart, en het type en de frequentie van de bestemmingsverbinding, voor bestemmingen te vormen die met Destination SDK worden gebouwd.
* [Schema-configuratie](destination-configuration/schema-configuration.md): Leer hoe u het doelschema van uw bestemming definieert waaraan gebruikers profielkenmerken en identiteiten kunnen toewijzen.
* [Configuratie naamruimte identiteit](destination-configuration/identity-namespace-configuration.md): Leer hoe te om de identiteiten te vormen die door uw bestemming worden gesteund. Deze configuratie vult de doelidentiteiten in [toewijzingsstap](../../ui/activate-segment-streaming-destinations.md#mapping) van de gebruikersinterface van het Experience Platform, waar de gebruikers identiteiten en attributen van hun schema&#39;s XDM aan het schema in uw bestemming in kaart brengen.
* [Levering bestemming](destination-configuration/destination-delivery.md): Leer hoe te om te vormen waar precies de uitgevoerde gegevens gaan en welke authentificatieregel in de plaats wordt gebruikt waar de gegevens zullen landen.
* [Configuratie van metagegevens voor publiek](destination-configuration/audience-metadata-configuration.md): Leer hoe segmentmeta-gegevens zoals segmentnamen of IDs tussen Experience Platform en uw bestemming zouden moeten worden gedeeld.
* [Samenvoegingsbeleid](destination-configuration/aggregation-policy.md): Leer hoe te opstelling een samenvoegingsbeleid om te bepalen hoe de verzoeken van HTTP aan uw bestemming zouden moeten worden gegroepeerd en worden gegroepeerd.
* [Batchconfiguratie](destination-configuration/batch-configuration.md): Stel verschillende instellingen voor bestandsnaam en exportplanning in die beschikbaar zijn voor gebruikers wanneer zij verbinding maken met uw doel in de gebruikersinterface van het Experience Platform.
* [Historische profielkwalificaties](destination-configuration/historical-profile-qualifications.md): Leer over de historische profielkwalificaties die door bestemmingen worden gesteund die met Destination SDK worden gebouwd.

## Configuratie van metagegevens voor publiek {#audience-metadata-configuration}

Deze component staat u toe om te vormen hoe het publiek/de segmenten programmatically worden gecreeerd, bijgewerkt, of in uw bestemming geschrapt. Voor op dossier-gebaseerde bestemmingen, staat het u toe om een bericht op te zetten wanneer de dossiers met succes aan uw bestemming worden geleverd. U kunt deze functionaliteit configureren via de [publiek-sjablonen, eindpunt](../metadata-api/create-audience-template.md).

## Volgende stappen {#next-steps}

Door dit artikel te lezen, hebt u nu een algemeen overzicht van de functionaliteit die door Destination SDK wordt verstrekt en welke pagina&#39;s voor meer informatie over specifieke configuraties te lezen. Vervolgens kunt u de hulplijnen lezen die alle stappen bevatten tot [streaming configureren](../guides/configure-destination-instructions.md) of [bestandsgebaseerd doel](../guides/configure-file-based-destination-instructions.md) door Destination SDK te gebruiken.
