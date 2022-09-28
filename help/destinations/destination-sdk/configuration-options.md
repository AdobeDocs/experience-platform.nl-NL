---
description: De bestemmingsdienst in Adobe Experience Platform gebruikt configuratieeindpunten voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen. Samen, staan deze componenten Experience Platform toe om met bestemmingspartners te verbinden, douaneberichten te verzenden, en profielgegevens over het digitale ecosysteem te activeren.
title: Configuratieopties in Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Configuratieopties in Destination SDK

## Overzicht {#overview}

De bestemmingsdienst in Adobe Experience Platform gebruikt configuratieeindpunten voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen. Samen staan deze componenten Experience Platform toe om met bestemmingsplatforms te verbinden, douaneberichten te verzenden, douanedossiers uit te voeren, en profielgegevens over het digitale ecosysteem te activeren. De configuraties die in Adobe Experience Platform Destination SDK worden gebruikt zijn:

* **Doelconfiguratie**: Bevat basisinformatie over uw bestemming. Deze configuratie omvat de identiteitstypen die uw bestemming kan steunen, het gewenste formaat van uitgevoerde dossiers (voor op dossier-gebaseerde bestemmingen), en diverse eigenschappen UI voor uw bestemmingskaart in het gebruikersinterface van Adobe Experience Platform.
* **Server-, bestands- en sjabloonspecificaties**: Verdeelt informatie over uw serverspecificaties en het malplaatje dat door Adobe wordt gebruikt om ladingen aan uw bestemming te leveren. Voor op bestanden gebaseerde doelen bevat deze configuratie ook de ondersteunde bestandsindelingen en compressie-indelingen voor uw doel.
   * **Serverspecificaties**: Een configuratiesjabloon dat informatie bevat over de opslaglocatie of het HTTP-eindpunt waarnaar gegevens worden verzonden.&quot;
   * **Bestandsspecificaties**: Een configuratiesjabloon dat de opties voor bestandsindeling en -compressie voor de batchbestemming bevat.
   * **Sjabloonspecificaties**: In deze sjabloon kunt u definiëren hoe u profielkenmerkvelden transformeert tussen het XDM-schema en de indeling die uw platform ondersteunt. Voor uitgebreide informatie over ondersteunde sjabloontalen, berichtindelingen en de informatie die Adobe nodig heeft om de integratie met uw platform in te stellen, leest u [Berichtindeling](./message-format.md).
* **Verificatieconfiguratie**: Deze instellingen bepalen hoe Adobe Experience Platform-gebruikers verbinding maken met uw bestemming.
* **Configuratie van metagegevens voor publiek**: Dit configuratieeindpunt staat u toe om te vormen hoe het publiek/de segmenten programmatically worden gecreeerd, bijgewerkt, of in uw bestemming worden geschrapt. Voor batchbestemmingen kunt u een melding instellen wanneer bestanden met succes naar uw bestemming worden afgeleverd.

![Diagram die de de configuratieeindpunten van de Destination SDK tonen en hoe deze samen worden gebruikt.](./assets/self-service-configuration.png)

## Verwante koppelingen {#related-links}

De onderstaande pagina&#39;s bevatten meer informatie over de functionaliteit en configuratieopties die beschikbaar zijn in Destination SDK en de bijbehorende API-bewerkingen die u kunt uitvoeren.

| Beschrijving van functionaliteit (streamingdoelen) | Functionaliteitsbeschrijving (batchbestemmingen) | API-referentie |
|--- |--- |--- |
| [Opties voor doelconfiguratie](./destination-configuration.md) | [Bestandsgebaseerde opties voor doelconfiguratie](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [API-eindpuntbewerkingen voor doelen](./destination-configuration-api.md) |
| [Server- en sjabloonspecificaties](./server-and-template-configuration.md) | [Specificaties voor server- en bestandsconfiguratie](/help/destinations/destination-sdk/server-and-file-configuration.md) | [API-eindpuntbewerkingen voor doelservers](./destination-server-api.md) |
| [Verificatieconfiguratie](./authentication-configuration.md) | Hetzelfde als voor streamingdoelen. | U kunt de authentificatieinformatie voor uw bestemming via vormen `customerAuthenticationConfigurations` parameters van de `/destinations` eindpunt. Meer informatie voor [streaming](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) en [partij](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) bestemmingen. |
| [Metagegevensbeheer voor het publiek](./audience-metadata-management.md) | Hetzelfde als bij streaming. Zie [bestandsgebaseerd voorbeeld](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) om te begrijpen hoe publieksmeta-gegevens in een partijbestemmingscontext kunnen worden gebruikt. | [API-bewerkingen voor het eindpunt van metagegevens van het publiek](./audience-metadata-api.md) |
| [OAuth 2-configuratie](./oauth2-authentication.md) | Hetzelfde als voor streamingdoelen | Configureren met de `customerAuthenticationConfigurations` in de [/bestemmingen API-eindpunt](./destination-configuration-api.md). |
| [Berichtindeling](./message-format.md) | - | - |
| [Testgereedschappen voor streamingdoelen](./test-destination.md) | [Testgereedschappen voor op bestanden gebaseerde doelen](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [API-bewerkingen voor doeltesten](./destination-testing-api.md) |
| [Publicatie van bestemming](./configure-destination-instructions.md#publish-destination) | Hetzelfde als voor streamingdoelen | [API-bewerkingen voor publiceren bestemming](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen {#next-steps}

Door dit artikel te lezen, hebt u nu een algemeen overzicht van de functionaliteit die door Destination SDK wordt verstrekt en welke pagina&#39;s voor meer informatie over specifieke configuraties te lezen. Vervolgens kunt u de hulplijnen lezen die alle stappen bevatten tot [streaming configureren](/help/destinations/destination-sdk/configure-destination-instructions.md) of [bestandsgebaseerd doel](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) door Destination SDK te gebruiken.
