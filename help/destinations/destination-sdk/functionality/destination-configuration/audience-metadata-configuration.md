---
description: Leer hoe u de metagegevensinstellingen voor de doelgroep configureert voor bestemmingen die zijn gemaakt met Destination SDK.
title: Configuratie van metagegevens voor publiek
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 804370a778a4334603f3235df94edaa91b650223
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Configuratie van metagegevens voor publiek

Wanneer u gegevens van Experience Platform naar uw bestemming exporteert, hebt u mogelijk specifieke publieksmetagegevens nodig, zoals publieksnamen of gebruikers-id&#39;s, die tussen Experience Platform en uw bestemming moeten worden gedeeld.

Destination SDK biedt hulpprogramma&#39;s waarmee u doelgroepen in uw doelplatform via programmacode kunt maken, bijwerken of verwijderen.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in de [ configuratieopties ](../configuration-options.md) documentatie of zie de gids op hoe te [ Destination SDK gebruiken om een het stromen bestemming ](../../guides/configure-destination-instructions.md#create-destination-configuration) te vormen.

U kunt de publieksmeta-gegevensmalplaatje via het `/authoring/audience-templates` eindpunt vormen. Nadat u de configuratie van de publieksmetagegevens hebt gemaakt, kunt u het `/authoring/destinations` -eindpunt gebruiken om de secties `segmentMappingConfig` en `audienceMetadataConfig` te configureren. Deze sectie vertelt uw bestemming welke publieksmeta-gegevens het aan uw publiekssjabloon zou moeten in kaart brengen.

Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Een publiekssjabloon maken](../../metadata-api/create-audience-template.md)
* [Een publiekssjabloon bijwerken](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja |

## Ondersteunde parameters {#supported-parameters}

Wanneer het creëren van uw configuratie van publieksmeta-gegevens, kunt u de parameters gebruiken die in de lijst hieronder worden beschreven om de montages van de publiekstoewijzing te vormen.

```json
"segmentMappingConfig": {
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
 },
"audienceMetadataConfig":{
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Boolean | Geeft aan of de [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) -waarde in de doelactiveringsworkflow de Experience Platform-publieksnaam moet zijn. |
| `mapExperiencePlatformSegmentId` | Boolean | Geeft aan of de [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) -waarde in de workflow voor doelactivering de Experience Platform-gebruikers-id moet zijn. |
| `mapUserInput` | Boolean | Schakelt gebruikersinvoer voor de [[!UICONTROL Mapping ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) -waarde in of uit in de doelactiveringsworkflow. Indien ingesteld op `true` , kan `audienceTemplateId` niet aanwezig zijn. |
| `audienceTemplateId` | String | `instanceId` van het [ malplaatje van publieksmeta-gegevens ](../../metadata-api/create-audience-template.md) dat voor uw bestemming wordt gebruikt. |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe u publieksmeta-gegevens voor uw bestemming kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Configuratie van klantverificatie](customer-authentication.md)
* [OAuth2-vergunning](oauth2-authorization.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [UI-kenmerken](ui-attributes.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte voor identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Samenvoegingsbeleid](aggregation-policy.md)
* [Batchconfiguratie](batch-configuration.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)
