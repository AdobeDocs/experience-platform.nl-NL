---
title: Configuratie-hulplijn voor identiteitsgrafiek met koppelingsregels
description: Leer de aanbevolen stappen die u moet volgen wanneer u uw gegevens implementeert met configuraties van regels voor identiteitsgrafieken.
badge: Beta
source-git-commit: d8a36650b2cd3ec9683763f536ea5c2c2e27455c
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# Configuratie-hulplijn voor identiteitsgrafiek met koppelingsregels

Lees dit document voor een stapsgewijze uitleg die u kunt volgen bij het implementeren van uw gegevens met Adobe Experience Platform Identity Service.

Stapsgewijze omtrek:

1. [De benodigde naamruimten maken](#namespace)
2. [Gebruik het grafieksimulatiehulpmiddel om met het algoritme van de identiteitsoptimalisering vertrouwd te maken](#graph-simulation)
3. [Gebruik het hulpmiddel van identiteitsinstellingen om uw unieke naamruimten aan te wijzen en prioritaire classificaties voor uw naamruimten te vormen](#identity-settings)
4. [Een XDM-schema (Experience Data Model) maken](#schema)
5. [Een gegevensset maken](#dataset)
6. [Gegevens naar Experience Platform verzenden](#ingest)

## Voorwaarden voor de implementatie vooraf

Voordat u aan de slag kunt, moet u er eerst voor zorgen dat geverifieerde gebeurtenissen in uw systeem altijd een persoon-id bevatten.

<!-- ## Set permissions {#set-permissions}

The first step in the implementation process for Identity Service is to ensure that your Experience Platform account is added to a role that is provisioned with the necessary permissions. Your administrator can configure permissions for your account by navigating to the Permissions UI in Adobe Experience Cloud. From there, your account must be added to a role with the following permissions:

* manage-identity-settings
* view-identity-dashboard
* view-identity-simulation

For more information on permissions, read the [permissions guide](../../access-control/abac/ui/permissions.md). -->

## Uw naamruimten maken {#namespace}

Als dit voor uw gegevens nodig is, moet u eerst de juiste naamruimten voor uw organisatie maken. Voor stappen voor het maken van een aangepaste naamruimte leest u de handleiding op [een aangepaste naamruimte maken in de gebruikersinterface](../features/namespaces.md#create-custom-namespaces).

## Het gereedschap Grafieksimulatie gebruiken {#graph-simulation}

Navigeer vervolgens naar de [grafieksimulatie](./graph-simulation.md) in de werkruimte van de gebruikersinterface van de identiteitsservice. U kunt het hulpmiddel van de grafieksimulatie gebruiken om identiteitsgrafieken te simuleren, die met een verscheidenheid van verschillende unieke namespace en namespace prioritaire configuraties worden gebouwd.

Door verschillende configuraties te maken, kunt u het gereedschap voor grafieksimulatie gebruiken om te leren en beter te begrijpen hoe het algoritme voor identiteitsoptimalisatie en bepaalde configuraties het gedrag van de grafiek beïnvloeden.

## Identiteitsinstellingen configureren {#identity-settings}

Als u een beter idee hebt van hoe de grafiek zich moet gedragen, navigeert u naar de [hulpmiddel Identiteitsinstellingen](./identity-settings-ui.md) in de werkruimte van de gebruikersinterface van de identiteitsservice.

Gebruik het hulpmiddel van identiteitsinstellingen om uw unieke naamruimten aan te wijzen en uw naamruimten op volgorde van prioriteit te vormen. Zodra u met het toepassen van uw montages wordt gebeëindigd, moet u minstens zes uren wachten alvorens u te werk gaat om gegevens in te voeren, aangezien het minstens zes uren voor nieuwe montages om in de Dienst van de Identiteit moet worden weerspiegeld.

## Een XDM-schema maken {#schema}

Wanneer uw unieke naamruimten en naamruimteprioriteiten zijn ingesteld, kunt u nu doorgaan naar de vereiste instelling om uw gegevens in te voeren. Eerst moet u een XDM-schema maken. Afhankelijk van uw gegevens moet u mogelijk een schema maken voor zowel XDM Individual Profile als XDM ExperienceEvent.

Om gegevens in het Profiel van de Klant in real time in te voeren, moet u ervoor zorgen dat uw schema minstens één gebied bevat dat als primaire identiteit is aangewezen. Door een primaire identiteit in te stellen, kunt u een bepaald schema inschakelen voor profielopname.

Voor instructies over hoe te om een schema tot stand te brengen, lees de gids op [een XDM-schema maken in de gebruikersinterface](../../xdm/tutorials/create-schema-ui.md).

## Een gegevensset maken {#dataset}

Daarna, creeer een dataset om een structuur voor de gegevens te verstrekken die u gaat opnemen. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets werken in combinatie met schema&#39;s en om gegevens in te voeren in het Real-Time Klantprofiel, moet uw gegevensset zijn ingeschakeld voor het opnemen van profielen. Opdat uw dataset voor Profiel wordt toegelaten, moet het een schema van verwijzingen voorzien dat voor de opname van het Profiel wordt toegelaten.

Voor instructies over hoe te om een dataset tot stand te brengen, lees [UI-gids voor gegevensset](../../catalog/datasets/user-guide.md).

## Gegevens verzamelen {#ingest}

Op dit punt, zou u het volgende moeten hebben:

* De noodzakelijke toestemmingen om tot de eigenschappen van de Dienst van de Identiteit toegang te hebben.
* Naamruimten voor uw gegevens.
* Aangewezen unieke naamruimten en geconfigureerde prioriteiten voor uw naamruimten.
* Minstens één XDM-schema. (Afhankelijk van uw gegevens en het specifieke gebruiksgeval, kunt u zowel profiel als ervaringsschema&#39;s moeten tot stand brengen.)
* Een dataset die van uw schema gebaseerd is.

Zodra u alle hierboven vermelde punten hebt, kunt u beginnen uw gegevens aan Experience Platform in te voeren. U kunt gegevensinvoer op verschillende manieren uitvoeren. U kunt de volgende services gebruiken om uw gegevens naar het Experience Platform te brengen:

* [Inslikken via batch en streaming](../../ingestion/home.md)
* [Gegevensverzameling in Experience Platform](../../collection/home.md)
* [Experience Platforms](../../sources/home.md)

>[!TIP]
>
>Als uw gegevens eenmaal zijn ingevoerd, verandert de XDM Raw-gegevenslading niet meer. U kunt uw primaire identiteitsconfiguraties in UI nog zien. Deze configuraties worden echter overschreven door identiteitsinstellingen.

Gebruik voor alle feedback de **[!UICONTROL Beta feedback]** in de werkruimte van de gebruikersinterface van Identiteitsservice.