---
title: Overzicht van publicatie
description: Meer informatie over het publiceren van wijzigingen in uw codebibliotheken voor tagbeheer in Adobe Experience Platform.
exl-id: 32eaad87-d7dc-4812-b546-a136511512fe
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Overzicht van publicatie

Met Adobe Experience Platform kunt u wijzigingen in uw code voor tagbeheer opnemen in afzonderlijke bibliotheken. Aangezien meerdere bibliotheken nu parallel door verschillende teams kunnen worden ontwikkeld, moeten deze bibliotheken een weloverwogen, toegestane procedure volgen voor het samenvoegen van wijzigingen voordat ze naar uw productieomgeving worden geduwd.

Op basisniveau voert elke bibliotheek het volgende publicatieproces uit:

1. Maak een nieuwe bibliotheek (of bewerk een bestaande bibliotheek) in een ontwikkelomgeving.
1. Test waar nodig de functionaliteit van de bibliotheek in een testomgeving.
1. Implementeer de bibliotheek in de productieomgeving.

Overweeg een situatie waarin u een nieuwe &quot;checkout&quot;gebeurtenis creeert, een element van opbrengstgegevens met betrekking tot die gebeurtenis creeert, en een verandering in de de uitbreidingsconfiguratie van Adobe Analytics aanbrengt om de nieuwe gebeurtenis en het gegevenselement te steunen. U kunt al deze wijzigingen in een nieuwe bibliotheek opnemen en het publicatieproces gebruiken om de wijzigingen als één eenheid te testen, goed te keuren en te publiceren.

Voor een overzicht op hoog niveau van het bibliotheek het publiceren werkschema, met inbegrip van details over hoe de bibliotheken middelen van upstream bouwt afhankelijk van hun het publiceren staat erven, zie de [ het publiceren stroomgids ](./publishing-flow.md).

Naast de publicatiestroom zijn er diverse componenten en relaties die u belangrijk kunt begrijpen om uw bibliotheken effectief te kunnen ontwikkelen en publiceren. De volgende lijst schetst elk van deze zeer belangrijke concepten, en verstrekt verbindingen aan documentatie om u te helpen meer over elk leren:

| Component | Beschrijving |
| --- | --- |
| Bibliotheken | Een bibliotheek is een set instructies voor hoe extensies, gegevenselementen en regels met elkaar en met uw website moeten communiceren. Wanneer een bibliotheek wordt gecompileerd om aan een milieu worden opgesteld, wordt die bibliotheek een bouwstijl.<br><br> zie het overzicht op [ bibliotheken ](./libraries.md) voor meer informatie over om, bibliotheken in UI tot stand te brengen te leiden en te activeren. |
| Builds | Een build is een gecompileerde bibliotheek. Wanneer opgesteld in een milieu, verstrekt een bouwstijl de daadwerkelijke reeks dossiers die de code bevatten die aan browser van elke gebruiker wordt geleverd wanneer zij uw plaats bekijken.<br><br> zie het overzicht op [ bouwt ](./builds.md) voor meer informatie over de inhoud en het formaat van bouwt. |
| Omgevingen | Een markeringsmilieu is een reeks plaatsingsinstructies die Experience Platform vertelt welke formaat u uw bouwstijl binnen wilt en waar u die geleverde bouwstijl zou willen.<br><br> zie het overzicht op [ milieu&#39;s ](./environments.md) voor meer informatie over de verschillende soorten milieu&#39;s, om bestaande milieu&#39;s te installeren en te vormen, en hoe te om nieuwe milieu&#39;s tot stand te brengen. |
| Gastheren | Een gastheer vertegenwoordigt de verbindingsdetails voor een milieu om een bouwstijl aan uw website te leveren. U kunt ervoor kiezen om Adobe de hosting van uw build te laten beheren, of u kunt in plaats daarvan informatie voor uw eigen hostservers opgeven.<br><br> zie het overzicht op [ gastheren ](./hosts/hosts-overview.md) voor meer informatie over elke het ontvangen optie. |
| Code aan de clientzijde | De client-side code is de set scripts die u in de broncode voor uw site of toepassing plaatst die elk clientapparaat vertelt waar de build moet worden opgehaald. De code is in bijlage aan een milieu en kan veranderen wanneer u uw milieuconfiguratie verandert.<br><br> zie de sectie op [ bed codes ](./environments.md#embed-code) in het milieu- overzicht in om meer te leren. |

## Volgende stappen

In dit document wordt een overzicht gegeven van de verschillende componenten die zijn betrokken bij het publiceren van tagbibliotheken in Adobe Experience Platform. Raadpleeg de documentatie in deze handleiding voor meer informatie over het publicatieproces.
