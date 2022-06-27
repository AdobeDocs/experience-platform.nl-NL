---
description: De bestemmingsdienst in Adobe Experience Platform gebruikt configuratiemalplaatjes voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen. Samen, staan deze componenten Experience Platform toe om met bestemmingspartners te verbinden, douaneberichten te verzenden, en profielgegevens over het digitale ecosysteem te activeren.
title: Configuratieopties in Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Configuratieopties in Destination SDK

## Overzicht {#overview}

De bestemmingsdienst in Adobe Experience Platform gebruikt configuratiemalplaatjes voor verscheidene componenten die omhoog de bestemmingsfunctionaliteit bouwen. Samen, staan deze componenten Experience Platform toe om met bestemmingspartners te verbinden, douaneberichten te verzenden, en profielgegevens over het digitale ecosysteem te activeren. In Adobe Experience Platform worden de volgende templates gebruikt:

* **Doelconfiguratie**: Bevat basisinformatie over uw bestemming. Deze configuratie bevat de identiteitstypen die uw bestemming kan ondersteunen en diverse UI-kenmerken voor uw doelkaart in de Adobe Experience Platform-gebruikersinterface.
* **Server- en sjabloonspecificaties**: Verdeelt informatie over uw serverspecificaties en het malplaatje dat door Adobe wordt gebruikt om ladingen aan uw bestemming te leveren.
   * **Serverspecificaties**: Een malplaatje dat uw eindpuntdetails opslaat.
   * **Sjabloonspecificaties**: In deze sjabloon kunt u definiëren hoe u profielkenmerkvelden transformeert tussen het XDM-schema en de indeling die uw platform ondersteunt. Voor uitgebreide informatie over ondersteunde sjabloontalen, berichtindelingen en de informatie die Adobe nodig heeft om de integratie met uw platform in te stellen, leest u [Berichtindeling](./message-format.md).
* **Verificatieconfiguratie**: Deze instellingen bepalen hoe Adobe Experience Platform-gebruikers verbinding maken met uw bestemming.
* **Configuratie van metagegevens voor publiek**: Dit malplaatje staat u toe om te vormen hoe het publiek/de segmenten programmatically worden gecreeerd, bijgewerkt, of in uw bestemming geschrapt.

![Destination SDK sjablonen en configuraties](./assets/self-service-configuration.png)

## Verwante koppelingen {#related-links}

De onderstaande pagina&#39;s bevatten meer informatie over de functionaliteit en configuratieopties die beschikbaar zijn in Destination SDK en de bijbehorende API-bewerkingen die u kunt uitvoeren.

| Functiebeschrijving | API-referentie |
|--- |--- |
| [Doelconfiguratie](./destination-configuration.md) | [API-eindpuntbewerkingen voor doelen](./destination-configuration-api.md) |
| [Server- en sjabloonspecificaties](./server-and-template-configuration.md) | [API-eindpuntbewerkingen voor doelservers](./destination-server-api.md) |
| [Verificatieconfiguratie](./authentication-configuration.md) | [API-bewerkingen van het eindpunt Credentials](./credentials-configuration-api.md) |
| [Metagegevensbeheer voor het publiek](./audience-metadata-management.md) | [API-bewerkingen voor het eindpunt van metagegevens van het publiek](./audience-metadata-api.md) |
| [OAuth 2-configuratie](./oauth2-authentication.md) | Configureren met de `customerAuthenticationConfigurations` in de [/bestemmingen API-eindpunt](./destination-configuration-api.md). |
| [Berichtindeling](./message-format.md) | - |
| [Doelstelling testen](./test-destination.md) | [API-bewerkingen voor doeltesten](./destination-testing-api.md) |
| [Publicatie van bestemming](./configure-destination-instructions.md#publish-destination) | [API-bewerkingen voor publiceren bestemming](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
