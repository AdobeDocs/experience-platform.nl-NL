---
source-git-commit: b9816767556b9d50cf2ff5268816d1de6b85fc63
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---
# Adobe Experience Platform Data Lake migratie naar Gen2

Adobe Experience Platform migreert naar Gen2 Data Lake. Dit is een nieuwe generatie van gegevens meer die de gebruikers van het Platform voordelen zoals geo-regio replicatie, fijnere op rol-gebaseerde toegangscontroles (RBAC), en betere het schrapen verstrekt.

## Gevolgen voor de gebruiker

Terwijl Adobe het Data Lake van Gen1 naar Gen 2 migreert, zullen gebruikers van het Data Lake kunnen **lezen** , maar alle mogelijkheden die **in het Data Lake schrijven** zullen worden beïnvloed. Hieronder volgt een lijst met beïnvloede mogelijkheden:

- **Bronnen**: Gegevens die afkomstig zijn uit de bronnen en verschillende workflows voor het opnemen van gegevens worden vertraagd. Gebruikers zien hun gegevens nadat de migratie is voltooid.
- **Query-service**: De gebruikers kunnen vragen uitvoeren maar zullen niet de output van de vraag in een dataset kunnen schrijven.
- **Klantprofiel** in realtime: Gegevens die via **batch** inname in de profielopslag worden ingevoerd, zijn niet beschikbaar tijdens de migratie. Gegevens die via **streaming** worden ingevoerd, zijn echter tijdens de migratie beschikbaar. Bovendien is de profielexport niet beschikbaar tijdens de migratie.
- **Werkruimte** voor gegevenswetenschap: Schrijven vanuit de werkruimte voor wetenschap van gegevens zullen mislukken.
- **Segmenteringsservice**: Soorten publiek dat is afgeleid van **batchsegmentatie** kan tijdens de migratie niet worden geactiveerd. De soorten publiek die worden afgeleid van **streaming** segmentatie worden niet beïnvloed.
- **Customer Journey Analytics**: Customer Journey Analytics rapporteert mogelijk gegevens zijn verouderd en worden tijdens de migratie niet vernieuwd, omdat er geen batches worden opgenomen in het Data Lake.

## Communicatie naar gebruikers in de Platform

Adobe zal contact opnemen met systeembeheerders om de gevolgen van de migratie in detail te bespreken en de migratiedata en -tijden voor specifieke IMS-organisaties te bevestigen.