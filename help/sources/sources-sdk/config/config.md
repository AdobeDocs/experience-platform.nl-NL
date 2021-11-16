---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Configuration options in Sources SDK
topic-legacy: overview
description: Dit document verstrekt een overzicht van de configuraties u moet voorbereiden om Bronnen SDK te gebruiken.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Configuration options in Sources SDK

>[!IMPORTANT]
>
>Bronnen-SDK bevindt zich momenteel in bètaversie en uw organisatie heeft mogelijk nog geen toegang tot deze SDK. De functionaliteit die in deze documentatie wordt beschreven, kan worden gewijzigd.

Dit document verstrekt een overzicht van de configuraties u moet voorbereiden om Bronnen SDK te gebruiken.

## Verbindingsspecificatie

Verbindingsspecificaties retourneren de verbindingseigenschappen van een bron. Zij omvatten authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen en een vaste identiteitskaart van de verbindingsspecificatie die aan een bepaalde bron wordt toegewezen. De specificaties van de verbinding zijn huurder en organisatie IMS agnostic. Een typische verbindingsspecificatie bevat basisinformatie over een bepaalde bron, evenals drie verschillende secties: `authSpec`, `sourceSpec`, en `exploreSpec`.

| Specificaties | Beschrijving |
| --- | --- |
| `authSpec` | De `authSpec` array bevat informatie over de verificatieparameters die zijn vereist om een bron te verbinden met een Platform. Om het even welke bepaalde bron kan veelvoudige verschillende soorten authentificatie steunen. |
| `sourceSpec` | De `sourceSpec` array bevat algemene informatie met betrekking tot een bron, waaronder informatie over kenmerken die vereist zijn om de bron in de interface weer te geven, documentkoppeling en parameters betreffende paginering, koptekst, hoofdtekst en planning. Bovendien `sourceSpec` beschrijft het schema van de parameters die worden vereist om een bronverbinding van een basisverbinding tot stand te brengen, en is noodzakelijk om een bronverbinding tot stand te brengen. |
| `exploreSpec` | De `exploreSpec` array definieert de parameters die nodig zijn voor het verkennen en inspecteren van objecten in uw bron. De `exploreSpec` definieert ook de indeling voor reacties die wordt geretourneerd wanneer objecten worden onderzocht en geïnspecteerd. |

{style=&quot;table-layout:auto&quot;}

## De waarden van de verbindingsspecificatie invullen

Een verbindingsspecificatie kan in drie verschillende delen worden verdeeld: de verificatiespecificaties, de bronspecificaties en de verkennende specificaties.

Zie de volgende documenten voor instructies over hoe u de waarden van elk deel van een verbindingsspecificatie kunt vullen:

* [Uw verificatiespecificatie configureren](./authspec.md)
* [Uw bronspecificatie configureren](./sourcespec.md)
* [Uw verkenningsspecificatie configureren](./explorespec.md)


