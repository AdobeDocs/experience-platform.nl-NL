---
title: Configuratie-hulplijn voor identiteitsgrafiek met koppelingsregels
description: Leer de aanbevolen stappen die u moet volgen wanneer u uw gegevens implementeert met configuraties van regels voor identiteitsgrafieken.
badge: Beta
source-git-commit: 72773f9ba5de4387c631bd1aa0c4e76b74e5f1dc
workflow-type: tm+mt
source-wordcount: '799'
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

## Machtigingen instellen {#set-permissions}

De eerste stap in het implementatieproces voor Identity Service is ervoor te zorgen dat uw account voor Experience Platforms wordt toegevoegd aan een rol die is voorzien van de vereiste machtigingen. Uw beheerder kan machtigingen voor uw account configureren door naar de gebruikersinterface voor machtigingen in Adobe Experience Cloud te navigeren. Van daar, moet uw rekening aan een rol met de volgende toestemmingen worden toegevoegd:

* [!UICONTROL View Identity Settings]: pas deze machtiging toe om unieke naamruimten en naamruimtenprioriteit weer te geven in de pagina Bladeren naar naamruimte voor identiteiten.
* [!UICONTROL Edit Identity Settings]: pas deze machtiging toe om uw identiteitsinstellingen te kunnen bewerken en opslaan.

Voor meer informatie over toestemmingen, lees de [ gids van toestemmingen ](../../access-control/abac/ui/permissions.md).

## Uw naamruimten maken {#namespace}

Als dit voor uw gegevens nodig is, moet u eerst de juiste naamruimten voor uw organisatie maken. Voor stappen op hoe te om tot een douane te leiden namespace, lees de gids bij [ creërend een douanespatie in UI ](../features/namespaces.md#create-custom-namespaces).

## Het gereedschap Grafieksimulatie gebruiken {#graph-simulation}

Daarna, navigeer aan het [ hulpmiddel van de grafieksimulatie ](./graph-simulation.md) in de werkruimte UI van de Dienst van de Identiteit. U kunt het hulpmiddel van de grafieksimulatie gebruiken om identiteitsgrafieken te simuleren, die met een verscheidenheid van verschillende unieke namespace en namespace prioritaire configuraties worden gebouwd.

Door verschillende configuraties te maken, kunt u het gereedschap voor grafieksimulatie gebruiken om te leren en beter te begrijpen hoe het algoritme voor identiteitsoptimalisatie en bepaalde configuraties het gedrag van de grafiek beïnvloeden.

## Identiteitsinstellingen configureren {#identity-settings}

Zodra u een beter idee van hebt hoe u uw grafiek wilt gedragen, navigeer aan het [ hulpmiddel van identiteitsmontages ](./identity-settings-ui.md) in de werkruimte UI van de Dienst van de Identiteit.

Gebruik het hulpmiddel van identiteitsinstellingen om uw unieke naamruimten aan te wijzen en uw naamruimten op volgorde van prioriteit te vormen. Zodra u met het toepassen van uw montages wordt gebeëindigd, moet u minstens zes uren wachten alvorens u te werk gaat om gegevens in te voeren, aangezien het minstens zes uren voor nieuwe montages om in de Dienst van de Identiteit moet worden weerspiegeld.

## Een XDM-schema maken {#schema}

Wanneer uw unieke naamruimten en naamruimteprioriteiten zijn ingesteld, kunt u nu doorgaan naar de vereiste instelling om uw gegevens in te voeren. Eerst moet u een XDM-schema maken. Afhankelijk van uw gegevens moet u mogelijk een schema maken voor zowel XDM Individual Profile als XDM ExperienceEvent.

Om gegevens in het Profiel van de Klant in real time in te voeren, moet u ervoor zorgen dat uw schema minstens één gebied bevat dat als primaire identiteit is aangewezen. Door een primaire identiteit in te stellen, kunt u een bepaald schema inschakelen voor profielopname.

Voor instructies op hoe te om een schema tot stand te brengen, lees de gids bij [ creërend een schema XDM in UI ](../../xdm/tutorials/create-schema-ui.md).

## Een gegevensset maken {#dataset}

Daarna, creeer een dataset om een structuur voor de gegevens te verstrekken die u gaat opnemen. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets werken in combinatie met schema&#39;s en om gegevens in te voeren in het Real-Time Klantprofiel, moet uw gegevensset zijn ingeschakeld voor het opnemen van profielen. Opdat uw dataset voor Profiel wordt toegelaten, moet het een schema van verwijzingen voorzien dat voor de opname van het Profiel wordt toegelaten.

Voor instructies op hoe te om een dataset tot stand te brengen, lees de [ gids UI van de dataset ](../../catalog/datasets/user-guide.md).

## Gegevens verzamelen {#ingest}

Op dit punt, zou u het volgende moeten hebben:

* De noodzakelijke toestemmingen om tot de eigenschappen van de Dienst van de Identiteit toegang te hebben.
* Naamruimten voor uw gegevens.
* Aangewezen unieke naamruimten en geconfigureerde prioriteiten voor uw naamruimten.
* Minstens één XDM-schema. (Afhankelijk van uw gegevens en het specifieke gebruiksgeval, kunt u zowel profiel als ervaringsschema&#39;s moeten tot stand brengen.)
* Een dataset die van uw schema gebaseerd is.

Zodra u alle hierboven vermelde punten hebt, kunt u beginnen uw gegevens aan Experience Platform in te voeren. U kunt gegevensinvoer op verschillende manieren uitvoeren. U kunt de volgende services gebruiken om uw gegevens naar het Experience Platform te brengen:

* [ Partij en het stromen opname ](../../ingestion/home.md)
* [Gegevensverzameling in Experience Platform](../../collection/home.md)
* [Experience Platforms](../../sources/home.md)

>[!TIP]
>
>Als uw gegevens eenmaal zijn ingevoerd, verandert de XDM Raw-gegevenslading niet meer. U kunt uw primaire identiteitsconfiguraties in UI nog zien. Deze configuraties worden echter overschreven door identiteitsinstellingen.

Gebruik voor alle feedback de optie **[!UICONTROL Beta feedback]** in de gebruikersinterface van de identiteitsservice.