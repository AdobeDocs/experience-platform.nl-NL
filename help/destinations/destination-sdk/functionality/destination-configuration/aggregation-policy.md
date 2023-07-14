---
description: Leer hoe te opstelling een samenvoegingsbeleid om te bepalen hoe de verzoeken van HTTP aan uw bestemming zouden moeten worden gegroepeerd en worden gegroepeerd.
title: Samenvoegingsbeleid
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 1%

---


# Samenvoegingsbeleid

Voor maximale efficiëntie bij het exporteren van gegevens naar het API-eindpunt kunt u verschillende instellingen gebruiken om geëxporteerde profielen samen te voegen tot grotere of kleinere batches, deze te groeperen op basis van identiteit en andere gebruiksgevallen. Hierdoor kunt u ook gegevens exporteren naar eventuele lagere beperkingen op het API-eindpunt (snelheidsbeperking, aantal identiteiten per API-aanroep, enz.).

Gebruik configureerbare samenvoeging om diep in de montages te duiken die door Destination SDK worden verstrekt of beste inspanningssamenvoeging te gebruiken om Destination SDK te vertellen om de API vraag zo best te partijgen als het kan.

Wanneer u een realtime (streaming) bestemming maakt met Destination SDK, kunt u configureren hoe de geëxporteerde profielen moeten worden gecombineerd in de resulterende export. Dit gedrag wordt bepaald door de instellingen van het aggregatiebeleid.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in [configuratieopties](../configuration-options.md) documentatie of bekijk de gids over hoe te [gebruik Destination SDK om een het stromen bestemming te vormen](../../guides/configure-destination-instructions.md#create-destination-configuration).

U kunt de montages van het samenvoegingsbeleid via vormen `/authoring/destinations` eindpunt. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

In dit artikel worden alle ondersteunde instellingen voor samenvoegingsbeleid beschreven die u voor uw bestemming kunt gebruiken.

Nadat u dit document hebt gelezen, raadpleegt u de documentatie op [gebruiken van sjablonen](../../functionality/destination-server/message-format.md#using-templating) en de [samenvoegingssleutelvoorbeelden](../../functionality/destination-server/message-format.md#template-aggregation-key) om te begrijpen hoe te om het samenvoegingsbeleid in uw malplaatje van de berichttransformatie te omvatten dat op uw geselecteerd samenvoegingsbeleid wordt gebaseerd.

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Nee |

## Beste inspanningsaggregatie {#best-effort-aggregation}

De beste inspanningssamenvoeging werkt het best voor bestemmingen die minder profielen per verzoek verkiezen en eerder meer verzoeken met minder gegevens dan minder verzoeken met meer gegevens zouden nemen.

In de onderstaande voorbeeldconfiguratie ziet u een aggregatieconfiguratie voor de beste inspanning. Voor een voorbeeld van configureerbare samenvoeging, zie [configureerbare samenvoeging](#configurable-aggregation) sectie. De parameters die van toepassing zijn op de aggregatie van de best mogelijke inspanning worden in de onderstaande tabel beschreven.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `aggregationType` | Tekenreeks | Wijst op het type van samenvoegingsbeleid dat uw bestemming zou moeten gebruiken. Ondersteunde aggregatietypen: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Geheel | Experience Platform kan meerdere geëxporteerde profielen samenvoegen in één HTTP-aanroep. <br><br>Deze waarde wijst op het maximumaantal profielen dat uw eindpunt in één enkele vraag van HTTP zou moeten ontvangen. Merk op dat dit een beste inspanningssamenvoeging is. Bijvoorbeeld, als u waarde 100 specificeert, zou het Platform om het even welk aantal profielen kunnen verzenden kleiner dan 100 op een vraag. <br><br> Als uw server niet meerdere gebruikers per aanvraag accepteert, stelt u deze waarde in op `1`. |
| `bestEffortAggregation.splitUserById` | Boolean | Gebruik deze vlag als de vraag aan de bestemming door identiteit zou moeten worden verdeeld. Deze markering instellen op `true` als uw server slechts één identiteit per vraag goedkeurt, voor een bepaalde identiteitsnaamruimte. |

{style="table-layout:auto"}

>[!TIP]
>
>Gebruik aggregatie van de best mogelijke inspanning als uw API eindpunt minder dan 100 profielen per API vraag goedkeurt.

## Configureerbare samenvoeging {#configurable-aggregation}

De configureerbare samenvoeging werkt het best als u eerder in grote partijen, met duizenden profielen op de zelfde vraag zou nemen. Met deze optie kunt u ook de geëxporteerde profielen samenvoegen op basis van complexe aggregatieregels.

De voorbeeldconfiguratie toont hieronder een configureerbare samenvoegingsconfiguratie. Voor een voorbeeld van de beste inspanningssamenvoeging, zie [beste inspanningsaggregatie](#best-effort-aggregation) sectie. De parameters die van toepassing zijn op configureerbare aggregatie worden in de onderstaande tabel beschreven.

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `aggregationType` | Tekenreeks | Wijst op het type van samenvoegingsbeleid dat uw bestemming zou moeten gebruiken. Ondersteunde aggregatietypen: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Boolean | Gebruik deze vlag als de vraag aan de bestemming door identiteit zou moeten worden verdeeld. Deze markering instellen op `true` als uw server slechts één identiteit per vraag goedkeurt, voor een bepaalde identiteitsnaamruimte. |
| `configurableAggregation.maxBatchAgeInSecs` | Geheel | Gebruikt in combinatie met `maxNumEventsInBatch`, bepaalt deze parameter hoe lang Experience Platform zou moeten wachten tot het verzenden van een API vraag naar uw eindpunt. <ul><li>Minimumwaarde (seconden): 1800</li><li>Maximumwaarde (seconden): 3600</li></ul> Bijvoorbeeld, als u de maximumwaarde voor beide parameters gebruikt, zal het Experience Platform of 3600 seconden OF wachten tot er 10000 gekwalificeerde profielen zijn alvorens de API vraag te maken, welke eerst gebeurt. |
| `configurableAggregation.maxNumEventsInBatch` | Geheel | Wordt gebruikt in combinatie met `maxBatchAgeInSecs`, bepaalt deze parameter hoeveel gekwalificeerde profielen moeten worden samengevoegd in een API-aanroep. <ul><li>Minimumwaarde: 1000</li><li>Maximumwaarde: 10000</li></ul> Bijvoorbeeld, als u de maximumwaarde voor beide parameters gebruikt, zal het Experience Platform of 3600 seconden OF wachten tot er 10000 gekwalificeerde profielen zijn alvorens de API vraag te maken, welke eerst gebeurt. |
| `configurableAggregation.aggregationKey` | - | Hiermee kunt u de geëxporteerde profielen samenvoegen die aan de bestemming zijn toegewezen op basis van de hieronder beschreven parameters. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Boolean | Deze parameter instellen op `true` als u profielen wilt groeperen die naar uw bestemming door publiek-id worden uitgevoerd. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Boolean | Deze parameter en `includeSegmentId` tot `true`, als u profielen wilt groeperen die naar uw bestemming door publiek-identiteitskaart en publieksstatus worden uitgevoerd. |
| `configurableAggregation.aggregationKey.includeIdentity` | Boolean | Deze parameter instellen op `true` als u profielen wilt groeperen die naar uw bestemming door identiteitsnamespace worden uitgevoerd. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolean | Deze parameter instellen op `true` als u wilt dat de geëxporteerde profielen worden samengevoegd tot groepen op basis van één identiteit (GAID, IDFA, telefoonnummers, e-mail, enz.). |
| `configurableAggregation.aggregationKey.groups` | Array | Maak lijsten met identiteitsgroepen als u profielen wilt groeperen die naar uw doel zijn geëxporteerd door groepen naamruimten. U kunt bijvoorbeeld profielen die de mobiele id&#39;s IDFA en GAID bevatten, combineren in één aanroep naar uw bestemming en e-mails in een andere via de configuratie die in het bovenstaande voorbeeld wordt getoond. |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe u samenvoegingsbeleid voor uw bestemming kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Configuratie van klantverificatie](customer-authentication.md)
* [OAuth2-verificatie](oauth2-authentication.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [UI-kenmerken](ui-attributes.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Configuratie van metagegevens voor publiek](audience-metadata-configuration.md)
* [Batchconfiguratie](batch-configuration.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)