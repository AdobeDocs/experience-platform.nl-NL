---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Configuratieopties in Self-Serve Sources (Batch SDK)
description: Dit document biedt een overzicht van de configuraties die u moet voorbereiden voor het gebruik van Self-Serve Sources (Batch SDK).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Configuratieopties in Self-Serve Sources (Batch SDK)

Dit document biedt een overzicht van de configuraties die u moet voorbereiden voor het gebruik van Self-Serve Sources (Batch SDK).

## Verbindingsspecificatie

Verbindingsspecificaties retourneren de verbindingseigenschappen van een bron. Zij omvatten authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen en een vaste identiteitskaart van de verbindingsspecificatie die aan een bepaalde bron wordt toegewezen. De specificaties van de verbinding zijn huurder en organisatie agnostisch. Een typische verbindingsspecificatie bevat basisinformatie over een bepaalde bron en drie verschillende secties: `authSpec`, `sourceSpec` en `exploreSpec` .

| Specificaties | Beschrijving |
| --- | --- |
| `authSpec` | De array `authSpec` bevat informatie over de verificatieparameters die zijn vereist om een bron te verbinden met Experience Platform. Om het even welke bepaalde bron kan veelvoudige verschillende types van authentificatie steunen. |
| `sourceSpec` | De array `sourceSpec` bevat algemene informatie met betrekking tot een bron, zoals informatie over kenmerken die zijn vereist om de bron in de gebruikersinterface weer te geven, documentatiekoppeling en parameters met betrekking tot paginering, koptekst, hoofdtekst en planning. Bovendien beschrijft `sourceSpec` het schema van de parameters die worden vereist om een bronverbinding van een basisverbinding tot stand te brengen, en is noodzakelijk om een bronverbinding tot stand te brengen. |
| `exploreSpec` | De array `exploreSpec` definieert de parameters die nodig zijn voor het verkennen en inspecteren van objecten in uw bron. De `exploreSpec` definieert ook de responsindeling die wordt geretourneerd wanneer objecten worden doorzocht en geïnspecteerd. |

{style="table-layout:auto"}

## Verbindingsspecificatiewaarden vullen

Een verbindingsspecificatie kan in drie verschillende delen worden verdeeld: de authentificatiespecificaties, de bronspecificaties, en de onderzoeken specificaties.

Zie de volgende documenten voor instructies over hoe u de waarden van elk deel van een verbindingsspecificatie kunt vullen:

* [Uw verificatiespecificatie configureren](./authspec.md)
* [Uw bronspecificatie configureren](./sourcespec.md)
* [Uw verkenningsspecificatie configureren](./explorespec.md)
