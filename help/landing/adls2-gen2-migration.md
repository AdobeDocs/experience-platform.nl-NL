---
title: Data Lake Migration to Gen2
description: Leer meer over de nieuwe functies die worden geboden door de migratie van het Data Lake naar Gen2 in Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake migratie naar Gen2

Adobe Experience Platform migreert naar Gen2 Data Lake. Dit is een nieuwe generatie gegevens-meer die de gebruikers van Experience Platform voordelen zoals geo-regio replicatie, fijnere op rol-gebaseerde toegangscontroles (RBAC), en betere het schrapen verstrekt.

## Gevolgen voor de gebruiker

Terwijl Adobe het meer van Gegevens van Gen1 aan Gen 2 migreert, zullen de gebruikers **&#x200B;**&#x200B;van het meer van Gegevens kunnen lezen, maar alle mogelijkheden die **&#x200B;**&#x200B;in het meer van Gegevens schrijft zullen worden beïnvloed. Hieronder volgt een lijst met beïnvloede mogelijkheden:

- **Bronnen**: De gegevens die van de bronnen en diverse werkschema&#39;s komen van de gegevensopname zullen worden vertraagd. Gebruikers zien hun gegevens nadat de migratie is voltooid.
- **Dienst van de Vraag**: De gebruikers kunnen vragen uitvoeren maar zullen niet de output van de vraag in een dataset kunnen schrijven.
- **Real-Time Profiel van de Klant**: Gegevens die aan de opslag van het Profiel door **partij** worden opgenomen zullen niet beschikbaar tijdens de migratie zijn. Nochtans, zullen de gegevens die door **worden opgenomen die** worden gestreamd beschikbaar zijn tijdens de migratie. Bovendien is de profielexport niet beschikbaar tijdens de migratie.
- **de Wetenschap van Gegevens Workspace**: Schrijft van de Wetenschap Workspace van Gegevens zal ontbreken.
- **de Dienst van de Segmentatie van de Segmentatie**: Het publiek dat van **wordt afgeleid batch** segmentatie kan niet tijdens de migratie worden geactiveerd. Het publiek dat van **wordt afgeleid die** segmentatie stromen zal niet worden beïnvloed.
- **Customer Journey Analytics**: Customer Journey Analytics rapporteert gegevens kunnen verouderd zijn en zullen niet tijdens de migratie verfrissen, aangezien de partijen niet in het meer van Gegevens worden opgenomen.

## Communicatie naar Experience Platform-gebruikers

Adobe zal contact opnemen met systeembeheerders om de gevolgen van de migratie in detail te bespreken en de migratiedata en -tijden voor specifieke organisaties te bevestigen.
