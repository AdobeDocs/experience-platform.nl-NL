---
title: Data Lake Migration to Gen2
description: Leer meer over de nieuwe functies van de migratie van het Data Lake naar Gen2 in Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake migratie naar Gen2

Adobe Experience Platform migreert naar Gen2 Data Lake. Dit is een nieuwe generatie van gegevens meer die de gebruikers van het Platform voordelen zoals geo-regio replicatie, fijnere op rol-gebaseerde toegangscontroles (RBAC), en betere het schrapen verstrekt.

## Gevolgen voor de gebruiker

Terwijl Adobe het Data Lake van Gen1 naar Gen2 migreert, kunnen gebruikers **lezen** uit het Data Lake, maar alle mogelijkheden die **schrijven** in het Datameer zal worden beïnvloed. Hieronder volgt een lijst met beïnvloede mogelijkheden:

- **Bronnen**: Gegevens die afkomstig zijn uit de bronnen en verschillende workflows voor het opnemen van gegevens worden vertraagd. Gebruikers zien hun gegevens nadat de migratie is voltooid.
- **Query-service**: De gebruikers kunnen vragen uitvoeren maar zullen niet de output van de vraag in een dataset kunnen schrijven.
- **Klantprofiel in realtime**: Gegevens die via **partij** Inname is niet beschikbaar tijdens de migratie. Nochtans, gegevens die door worden opgenomen **streaming** tijdens de migratie is inname beschikbaar . Bovendien is de profielexport niet beschikbaar tijdens de migratie.
- **Werkruimte voor gegevenswetenschap**: Schrijven vanuit de werkruimte voor wetenschap van gegevens zullen mislukken.
- **Segmenteringsservice**: Soorten publiek afgeleid van **partij** segmentatie kan niet worden geactiveerd tijdens de migratie. Soorten publiek afgeleid van **streaming** de segmentatie wordt niet beïnvloed.
- **Customer Journey Analytics**: Customer Journey Analytics rapporteert mogelijk gegevens zijn verouderd en worden tijdens de migratie niet vernieuwd, omdat er geen batches worden opgenomen in het Data Lake.

## Communicatie naar gebruikers in de Platform

Adobe zal contact opnemen met systeembeheerders om de gevolgen van de migratie in detail te bespreken en de migratiedata en -tijden voor specifieke IMS-organisaties te bevestigen.
