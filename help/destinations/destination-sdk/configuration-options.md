---
description: De bestemmingsdienst in Adobe Experience Platform gebruikt configuratiemalplaatjes voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen. Samen, staan deze componenten Experience Platform toe om met bestemmingspartners te verbinden, douaneberichten te verzenden, en profielgegevens over het digitale ecosysteem te activeren.
seo-description: The destinations service in Adobe Experience Platform uses configuration templates for several components that build up the destinations functionality. Combined, these components allow Experience Platform to connect to destination partners, send custom messages, and activate profile data across the digital ecosystem.
seo-title: Configuration options in Destination SDK
title: Configuratieopties in SDK van bestemming
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Configuratieopties in SDK van bestemming

## Overzicht {#overview}

De bestemmingsdienst in Adobe Experience Platform gebruikt configuratiemalplaatjes voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen. Samen, staan deze componenten Experience Platform toe om met bestemmingspartners te verbinden, douaneberichten te verzenden, en profielgegevens over het digitale ecosysteem te activeren. In Adobe Experience Platform worden de volgende templates gebruikt:

* **Doelconfiguratie**: Bevat basisinformatie over uw bestemming. Deze configuratie bevat de identiteitstypen die uw bestemming kan ondersteunen en diverse UI-kenmerken voor uw doelkaart in de Adobe Experience Platform-gebruikersinterface.
* **Server- en sjabloonspecificaties**: Verdeelt informatie over uw serverspecificaties en het malplaatje dat door Adobe wordt gebruikt om ladingen aan uw bestemming te leveren.
   * **Serverspecificaties**: Een malplaatje dat uw eindpuntdetails opslaat.
   * **Sjabloonspecificaties**: In deze sjabloon kunt u definiëren hoe u profielkenmerkvelden transformeert tussen het XDM-schema en de indeling die uw platform ondersteunt. Lees [Berichtindeling](./message-format.md) voor uitgebreide informatie over ondersteunde sjabloontalen, berichtindelingen en de informatie die Adobe nodig heeft om de integratie met uw platform in te stellen.
* **Verificatieconfiguratie**: Deze instellingen bepalen hoe Adobe Experience Platform-gebruikers verbinding maken met uw bestemming.
* **Configuratie** metagegevens publiek: Dit malplaatje staat u toe om te vormen hoe het publiek/de segmenten programmatically worden gecreeerd, bijgewerkt, of in uw bestemming geschrapt.

![Sjablonen en configuraties voor de SDK-bestemming](./assets/self-service-configuration.png)

## Verwante koppelingen {#related-links}

De pagina&#39;s hieronder verstrekken meer details over de functionaliteit en de configuratieopties beschikbaar in Doel SDK, en de overeenkomstige API verrichtingen die u kunt uitvoeren.

| Functiebeschrijving | API-referentie |
|--- |--- |
| [Doelconfiguratie](./destination-configuration.md) | [API-eindpuntbewerkingen voor doelen](./destination-configuration-api.md) |
| [Server- en sjabloonspecificaties](./server-and-template-configuration.md) | [API-eindpuntbewerkingen voor doelservers](./destination-server-api.md) |
| [Verificatieconfiguratie](./credentials-configuration.md) | [API-bewerkingen van het eindpunt Credentials](./credentials-configuration-api.md) |
| [Metagegevensbeheer voor het publiek](./audience-metadata-management.md) | [API-bewerkingen voor het eindpunt van metagegevens van het publiek](./audience-metadata-api.md) |
| [OAuth 2-configuratie](./oauth2-authentication.md) | Vorm gebruikend de `customerAuthenticationConfigurations` parameter in [/bestemmingen API eindpunt](./destination-configuration-api.md). |
| [Berichtindeling](./message-format.md) | - |
| [Doelstelling testen](./test-destination.md) | [API-bewerkingen voor doeltesten](./destination-testing-api.md) |
| [Publicatie van bestemming](./configure-destination-instructions.md#publish-destination) | [API-bewerkingen voor publiceren bestemming](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
