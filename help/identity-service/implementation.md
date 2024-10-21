---
title: Implementatiehandleiding voor identiteitsservice
description: Leer hoe gegevens die aan Adobe Experience Platform zijn verstrekt worden verwerkt voordat ze door Identity Service worden gebruikt om identiteitsgrafieken samen te stellen.
exl-id: c961bbf6-6b46-470f-a671-93ff4173876c
source-git-commit: 4ba25ed684ff126ab1c4f1a33e6503f0342e8720
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Implementatiegids voor identiteitsservice

Dit document bevat informatie over de manier waarop aan Adobe Experience Platform verstrekte gegevens worden verwerkt voordat ze door Identity Service worden gebruikt om een identiteitsgrafiek voor een bepaalde klant te maken.

## Beslissen over identiteitsvelden

Afhankelijk van uw strategie van de de gegevensinzameling van ondernemingsgegevens, bepalen de gegevensgebieden u als identiteiten etiketteert welke gegevens in uw identiteitskaart inbegrepen zijn. Om het maximale voordeel van Experience Platform en de meest uitgebreide klantenidentiteiten mogelijk te krijgen, zou u zowel online als off-line gegevens moeten uploaden.

* Onlinegegevens zijn gegevens die de online aanwezigheid en het gedrag beschrijven, zoals gebruikersnamen en e-mailadressen.

* Offlinegegevens hebben betrekking op gegevens die niet rechtstreeks verband houden met online aanwezigheid, zoals id&#39;s van CRM-systemen. Dit type gegevens maakt uw identiteiten robuuster en steunt gegevenscohesie over uw verschillende systemen.

## Extra naamruimten maken

Hoewel Experience Platform verschillende standaardnaamruimten biedt, moet u mogelijk extra naamruimten maken om uw identiteiten correct te categoriseren. Voor meer informatie, lees de gids bij [ het creëren van douane namespaces voor uw organisatie ](./features/namespaces.md).

>[!NOTE]
>
>Naamruimten zijn een kwalificatie voor identiteiten. Als er eenmaal een naamruimte is gemaakt, kan deze daarom niet worden verwijderd.

## Identiteitsgegevens opnemen in XDM (Experience Data Model)

Als gestandaardiseerd kader waardoor het Experience Platform klantengegevens organiseert, laat het Model van Gegevens van de Ervaring (XDM) gegevens toe om over Experience Platform en andere diensten worden gedeeld en worden begrepen die met Experience Platform in wisselwerking staan. Voor meer informatie lees het [ XDM overzicht van het Systeem ](../xdm/home.md).

Zowel de verslagen als de tijdreeksschema&#39;s verstrekken de middelen om identiteitsgegevens te omvatten. Terwijl gegevens worden opgenomen, maakt de identiteitsgrafiek nieuwe relaties tussen gegevensfragmenten van verschillende naamruimten als deze gemeenschappelijke identiteitsgegevens delen.

## XDM-velden als identiteit labelen

Om het even welk gebied van type `string` in schema&#39;s die of verslag of tijdreeks XDM klassen uitvoeren kan als identiteitsgebied worden geëtiketteerd. Als gevolg hiervan worden alle gegevens die in dat veld worden ingevoerd, beschouwd als identiteitsgegevens.

Identiteitsvelden maken het ook mogelijk om identiteiten te koppelen als ze gemeenschappelijke PII-gegevens delen.
Bijvoorbeeld, door de gebieden van het telefoonaantal als identiteitsgebieden te etiketteren, grafiekt de Dienst van de Identiteit automatisch relaties met de andere individuen die worden gevonden om het zelfde telefoonaantal te gebruiken.

>[!NOTE]
>
>* Array- en toewijzingsvelden worden niet ondersteund en kunnen niet worden gemarkeerd en gelabeld als identiteitsvelden.
>* De naamruimte van resulterende identiteiten wordt opgegeven op het moment dat het veld wordt gelabeld.
>* Een veld kan als identiteit worden gemarkeerd, zolang dit veld zich niet onder een matrixobject bevindt.

Voor meer informatie, lees de gids op [ bepalend identiteitsgebieden in UI ](../xdm/ui/fields/identity.md).

## Een dataset voor Identiteitsservice configureren

Tijdens het streamingingingproces extraheert de Identiteitsservice automatisch identiteitsgegevens uit record- en tijdreeksgegevens. Nochtans, alvorens de gegevens kunnen worden opgenomen, moet het voor de Dienst van de Identiteit worden toegelaten. Lees het leerprogramma op [ vormend een dataset voor het Profiel van de Klant in real time en de Dienst van de Identiteit gebruikend APIs ](../profile/tutorials/dataset-configuration.md) voor meer informatie.

## Gegevens opnemen in de identiteitsservice

De Dienst van de identiteit verbruikt XDM-Volgzame gegevens die naar Experience Platform of door [ partij worden verzonden ](../ingestion/batch-ingestion/overview.md) of [ het stromen opname ](../ingestion/streaming-ingestion/overview.md).

De volgende video is bedoeld om uw begrip van de Dienst van de Identiteit te steunen. In deze video ziet u hoe u gegevensvelden kunt labelen als identiteiten, identiteitsgegevens kunt invoeren en vervolgens kunt controleren of de gegevens zijn omgezet in de persoonlijke grafiek van de Adobe Experience Platform Identity Service.

>[!WARNING]
>
>De interface van het Experience Platform die in de volgende video wordt getoond is verouderd. Raadpleeg de documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)
