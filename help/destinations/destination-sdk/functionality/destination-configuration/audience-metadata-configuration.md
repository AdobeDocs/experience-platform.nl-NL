---
description: Leer hoe te om de montages van publiekmeta-gegevens voor bestemmingen te vormen die met Destination SDK worden gebouwd.
title: Configuratie van metagegevens voor publiek
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---


# Configuratie van metagegevens voor publiek

Wanneer het uitvoeren van gegevens van Experience Platform aan uw bestemming, zou u specifieke publieksmeta-gegevens, zoals segmentnamen of segment IDs, kunnen nodig hebben die tussen Experience Platform en uw bestemming worden gedeeld.

Destination SDK biedt hulpmiddelen aan die u kunt gebruiken om publiek in uw bestemmingsplatform programmatically tot stand te brengen bij te werken of te schrappen.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in [configuratieopties](../configuration-options.md) documentatie of bekijk de gids over hoe te [gebruik Destination SDK om een het stromen bestemming te vormen](../../guides/configure-destination-instructions.md#create-destination-configuration).

U kunt de sjabloon voor publiekmetagegevens configureren via de `/authoring/audience-templates` eindpunt. Nadat u de configuratie van de metagegevens van uw publiek hebt gemaakt, kunt u de opdracht `/authoring/destinations` eindpunt om te vormen `audienceMetadataConfig` sectie. Deze sectie vertelt uw bestemming welke segmentmeta-gegevens het aan uw publiekssjabloon zou moeten in kaart brengen.

Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Een publiekssjabloon maken](../../metadata-api/create-audience-template.md)
* [Een publiekssjabloon bijwerken](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja |

## Ondersteunde parameters {#supported-parameters}

Wanneer het creëren van uw configuratie van publieksmeta-gegevens, kunt u de parameters gebruiken die in de lijst hieronder worden beschreven om de montages van de segmentafbeelding te vormen.

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Boolean | Geeft aan of de [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) De waarde in de workflow voor doelactivering moet de segmentnaam van het Experience Platform zijn. |
| `mapExperiencePlatformSegmentId` | Boolean | Geeft aan of de [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) De waarde in het werkschema van de bestemmingsactivering zou identiteitskaart van het Experience Platform moeten zijn. |
| `mapUserInput` | Boolean | Hiermee wordt gebruikersinvoer voor de [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) waarde in de workflow voor doelactivering. Indien ingesteld op `true`, `audienceTemplateId` kan niet aanwezig zijn. |
| `audienceTemplateId` | Boolean | De `instanceId` van de [sjabloon voor doelmetagegevens](../../metadata-api/create-audience-template.md) gebruikt voor uw doel. |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe u publieksmeta-gegevens voor uw bestemming kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Configuratie van klantverificatie](customer-authentication.md)
* [OAuth2-verificatie](oauth2-authentication.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [UI-kenmerken](ui-attributes.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Samenvoegingsbeleid](aggregation-policy.md)
* [Batchconfiguratie](batch-configuration.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)