---
description: Leer over de historische profielkwalificaties die door bestemmingen worden gesteund die met Destination SDK worden gebouwd.
title: Historische profielkwalificaties
exl-id: 8880cff9-865b-4d45-a24d-a78e77419670
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Historische profielkwalificaties

Alle bestemmingen die door Destination SDK worden gecreeerd steunen historische profielkwalificaties door gebrek. Dit betekent dat wanneer de gebruikers eerst opstelling een activeringsgegevensstroom aan uw bestemmingen, de eerste uitvoer alle leden van het publiek bevat die ooit voor dat segment hebben gekwalificeerd.

Dit gedrag wordt gedefinieerd door de parameter `"backfillHistoricalProfileData":true` in de doelconfiguratie.

>[!IMPORTANT]
>
>Historische profielkwalificaties worden ingeschakeld voor alle doelen die met Destination SDK worden gemaakt en de parameter `backfillHistoricalProfileData` kan niet door de gebruiker worden geconfigureerd.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when audiences are activated to the destination. <br> <ul><li> `true`: [!DNL Experience Platform] sends the historical user profiles that qualified for the audience before the audience is activated. </li><li> `false`: [!DNL Experience Platform] only includes user profiles that qualify for the audience after the audience is activated. </li></ul> |

{style="table-layout:auto"} -->


## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u moeten weten dat Experience Platform automatisch een historische populatie van alle profielen uitvoert die ooit voor een geactiveerd publiek hebben gekwalificeerd wanneer het publiek eerst naar de bestemming wordt uitgevoerd. Deze optie kan niet worden geconfigureerd in Destination SDK of in de gebruikersinterface van Experience Platform.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Verificatie door klant](customer-authentication.md)
* [OAuth2-vergunning](oauth2-authorization.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [UI-kenmerken](ui-attributes.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte voor identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Configuratie van metagegevens voor publiek](audience-metadata-configuration.md)
* [Samenvoegingsbeleid](aggregation-policy.md)
* [Batchconfiguratie](batch-configuration.md)
