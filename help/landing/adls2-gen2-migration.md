---
title: Data Lake Migration to Gen2
description: Leer meer over de nieuwe functies van de migratie van het Data Lake naar Gen2 in Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake migratie naar Gen2

Adobe Experience Platform migreert naar Gen2 Data Lake. Dit is een nieuwe generatie van gegevens meer die de gebruikers van het Platform voordelen zoals geo-regio replicatie, fijnere op rol-gebaseerde toegangscontroles (RBAC), en betere het schrapen verstrekt.

## Gevolgen voor de gebruiker

Terwijl Adobe het Datameer van Gen1 naar Gen 2 migreert, kunnen gebruikers **read** vanaf het Datameer, maar alle mogelijkheden die **write** in het Datameer zullen worden beïnvloed. Hieronder volgt een lijst met beïnvloede mogelijkheden:

- **Bronnen**: Gegevens die afkomstig zijn uit de bronnen en verschillende workflows voor het opnemen van gegevens worden vertraagd. Gebruikers zien hun gegevens nadat de migratie is voltooid.
- **Query-service**: De gebruikers kunnen vragen uitvoeren maar zullen niet de output van de vraag in een dataset kunnen schrijven.
- **Klantprofiel** in realtime: Gegevens die via  **** batchverwerking in de profielopslag worden ingevoerd, zijn niet beschikbaar tijdens de migratie. Gegevens die via **streaming**-opname worden ingevoerd, zijn echter tijdens de migratie beschikbaar. Bovendien is de profielexport niet beschikbaar tijdens de migratie.
- **Werkruimte** voor gegevenswetenschap: Schrijven vanuit de werkruimte voor wetenschap van gegevens zullen mislukken.
- **Segmenteringsservice**: Soorten publiek dat is afgeleid van  **** batchsegmentatie kan tijdens de migratie niet worden geactiveerd. Soorten publiek dat is afgeleid van **streaming** segmentatie wordt niet beïnvloed.
- **Customer Journey Analytics**: Customer Journey Analytics rapporteert mogelijk gegevens zijn verouderd en worden tijdens de migratie niet vernieuwd, omdat er geen batches worden opgenomen in het Data Lake.

## Communicatie naar gebruikers in de Platform

Adobe zal contact opnemen met systeembeheerders om de gevolgen van de migratie in detail te bespreken en de migratiedata en -tijden voor specifieke IMS-organisaties te bevestigen.
