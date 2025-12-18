---
description: Leer hoe te opstelling een samenvoegingsbeleid om te bepalen hoe de verzoeken van HTTP aan uw bestemming zouden moeten worden gegroepeerd en worden gegroepeerd.
title: Samenvoegingsbeleid
exl-id: 2dfa8815-2d69-4a22-8938-8ea41be8b9c5
source-git-commit: 92d7abcbd642cea4e0fa041d2926ba8868f506e5
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Samenvoegingsbeleid

Voor maximale efficiëntie bij het exporteren van gegevens naar het API-eindpunt kunt u verschillende instellingen gebruiken om geëxporteerde profielen samen te voegen tot grotere of kleinere batches, deze te groeperen op basis van identiteit en andere gebruiksgevallen. Hierdoor kunt u ook gegevens exporteren naar eventuele lagere beperkingen op het API-eindpunt (snelheidsbeperking, aantal identiteiten per API-aanroep, enz.).

Gebruik configureerbare aggregatie om diep in de montages te duiken die door Destination SDK worden verstrekt of beste inspanningssamenvoeging te gebruiken om Destination SDK te vertellen om de API vraag zo best te partijgen als het kan.

Wanneer u een realtime (streaming) bestemming maakt met Destination SDK, kunt u configureren hoe de geëxporteerde profielen moeten worden gecombineerd in de resulterende export. Dit gedrag wordt bepaald door de instellingen van het aggregatiebeleid.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in de [&#x200B; configuratieopties &#x200B;](../configuration-options.md) documentatie of zie de gids op hoe te [&#x200B; Destination SDK gebruiken om een het stromen bestemming &#x200B;](../../guides/configure-destination-instructions.md#create-destination-configuration) te vormen.

U kunt de montages van het samenvoegingsbeleid via het `/authoring/destinations` eindpunt vormen. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

In dit artikel worden alle ondersteunde instellingen voor samenvoegingsbeleid beschreven die u voor uw bestemming kunt gebruiken.

Na het lezen door dit document, verwijs naar de documentatie op [&#x200B; gebruikend het templating &#x200B;](../../functionality/destination-server/message-format.md#using-templating) en de [&#x200B; belangrijkste voorbeelden van de samenvoeging &#x200B;](../../functionality/destination-server/message-format.md#template-aggregation-key) om te begrijpen hoe te om het samenvoegingsbeleid in uw malplaatje van de berichttransformatie te omvatten dat op uw geselecteerd samenvoegingsbeleid wordt gebaseerd.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Nee |

## Beste inspanningsaggregatie {#best-effort-aggregation}

De beste inspanningssamenvoeging werkt het best voor bestemmingen die minder profielen per verzoek verkiezen en eerder meer verzoeken met minder gegevens dan minder verzoeken met meer gegevens zouden nemen.

In de onderstaande voorbeeldconfiguratie ziet u een aggregatieconfiguratie voor de beste inspanning. Voor een voorbeeld van configureerbare samenvoeging, zie de [&#x200B; configureerbare samenvoeging &#x200B;](#configurable-aggregation) sectie. De parameters die van toepassing zijn op de aggregatie van de best mogelijke inspanning worden in de onderstaande tabel beschreven.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false,
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
| `aggregationType` | String | Wijst op het type van samenvoegingsbeleid dat uw bestemming zou moeten gebruiken. Ondersteunde aggregatietypen: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Geheel | Experience Platform kan meerdere geëxporteerde profielen samenvoegen in één HTTP-oproep. <br><br> Deze waarde wijst op het maximumaantal profielen dat uw eindpunt in één enkele vraag van HTTP zou moeten ontvangen. Merk op dat dit een beste inspanningssamenvoeging is. Bijvoorbeeld, als u waarde 100 specificeert, zou Experience Platform om het even welk aantal profielen kunnen verzenden kleiner dan 100 op een vraag. <br><br> Als uw server niet per aanvraag meerdere gebruikers accepteert, stelt u deze waarde in op `1` . |
| `bestEffortAggregation.splitUserById` | Boolean | Gebruik deze vlag als de vraag aan de bestemming door identiteit zou moeten worden verdeeld. Stel deze markering in op `true` als uw server slechts één identiteit per aanroep accepteert, voor een opgegeven naamruimte voor de identiteit. |
| `bestEffortAggregation.aggregationKey` | Object | *Facultatief*. Hiermee kunt u de geëxporteerde profielen samenvoegen die aan de bestemming zijn toegewezen op basis van de hieronder beschreven parameters. Deze parameter kan worden weggelaten of op `null` worden ingesteld als aggregatie niet nodig is. Indien opgegeven, functioneert deze op dezelfde manier als de aggregatietoets in configureerbare aggregatie. |
| `bestEffortAggregation.aggregationKey.includeSegmentId` | Boolean | Stel deze parameter in op `true` als u profielen wilt groeperen die naar uw doel zijn geëxporteerd op basis van gebruikers-id. |
| `bestEffortAggregation.aggregationKey.includeSegmentStatus` | Boolean | Stel deze parameter en `includeSegmentId` in op `true` als u profielen wilt groeperen die naar uw doel zijn geëxporteerd op basis van gebruikers-id en de status van het publiek. |
| `bestEffortAggregation.aggregationKey.includeIdentity` | Boolean | Stel deze parameter in op `true` als u profielen wilt groeperen die via naamruimte naar uw doel worden geëxporteerd. |
| `bestEffortAggregation.aggregationKey.oneIdentityPerGroup` | Boolean | Stel deze parameter in op `true` als u wilt dat de geëxporteerde profielen worden samengevoegd in groepen op basis van één identiteit (GAID, IDFA, telefoonnummers, e-mail, enz.). Stel dit in op `false` als u de parameter `groups` wilt gebruiken om aangepaste naamruimtegroepen voor identiteiten te definiëren. |
| `bestEffortAggregation.aggregationKey.groups` | Array | Gebruik deze parameter wanneer `oneIdentityPerGroup` is ingesteld op `false` . Maak lijsten met identiteitsgroepen als u profielen wilt groeperen die naar uw doel zijn geëxporteerd door groepen naamruimten. U kunt bijvoorbeeld profielen die de mobiele id&#39;s IDFA en GAID bevatten, combineren in één aanroep naar uw bestemming en e-mails in een andere via de configuratie die in het bovenstaande voorbeeld wordt getoond. |

{style="table-layout:auto"}

>[!TIP]
>
>Gebruik aggregatie van de best mogelijke inspanning als uw API eindpunt minder dan 100 profielen per API vraag goedkeurt.

## Configureerbare samenvoeging {#configurable-aggregation}

De configureerbare samenvoeging werkt het best als u eerder in grote partijen, met duizenden profielen op de zelfde vraag zou nemen. Met deze optie kunt u ook de geëxporteerde profielen samenvoegen op basis van complexe aggregatieregels.

De voorbeeldconfiguratie toont hieronder een configureerbare samenvoegingsconfiguratie. Voor een voorbeeld van beste inspanningssamenvoeging, zie de [&#x200B; best inspanningssamenvoeging &#x200B;](#best-effort-aggregation) sectie. De parameters die van toepassing zijn op configureerbare aggregatie worden in de onderstaande tabel beschreven.

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
| `aggregationType` | String | Wijst op het type van samenvoegingsbeleid dat uw bestemming zou moeten gebruiken. Ondersteunde aggregatietypen: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Boolean | Gebruik deze vlag als de vraag aan de bestemming door identiteit zou moeten worden verdeeld. Stel deze markering in op `true` als uw server slechts één identiteit per aanroep accepteert, voor een opgegeven naamruimte voor de identiteit. |
| `configurableAggregation.maxBatchAgeInSecs` | Geheel | Deze parameter wordt gebruikt in combinatie met `maxNumEventsInBatch` en bepaalt hoe lang Experience Platform moet wachten totdat een API-aanroep naar het eindpunt wordt verzonden. <ul><li>Minimumwaarde (in seconden): 301</li><li>Maximumwaarde (in seconden): 3.600</li></ul> Als u bijvoorbeeld de maximumwaarde voor beide parameters gebruikt, wacht Experience Platform 3600 seconden OF tot er 10000 gekwalificeerde profielen zijn voordat de API-aanroep wordt uitgevoerd, afhankelijk van wat zich het eerst voordoet. |
| `configurableAggregation.maxNumEventsInBatch` | Geheel | Deze parameter wordt gebruikt in combinatie met `maxBatchAgeInSecs` en bepaalt hoeveel gekwalificeerde profielen moeten worden samengevoegd in een API-aanroep. <ul><li>Minimumwaarde: 1.000</li><li>Maximumwaarde: 10.000</li></ul> Als u bijvoorbeeld de maximumwaarde voor beide parameters gebruikt, wacht Experience Platform 3.600 seconden OF tot er 10.000 gekwalificeerde profielen zijn voordat de API-aanroep wordt uitgevoerd, afhankelijk van wat zich het eerst voordoet. |
| `configurableAggregation.aggregationKey` | - | Hiermee kunt u de geëxporteerde profielen samenvoegen die aan de bestemming zijn toegewezen op basis van de hieronder beschreven parameters. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Boolean | Stel deze parameter in op `true` als u profielen wilt groeperen die naar uw doel zijn geëxporteerd op basis van gebruikers-id. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Boolean | Stel deze parameter en `includeSegmentId` in op `true` als u profielen wilt groeperen die naar uw doel zijn geëxporteerd op basis van gebruikers-id en de status van het publiek. |
| `configurableAggregation.aggregationKey.includeIdentity` | Boolean | Stel deze parameter in op `true` als u profielen wilt groeperen die via naamruimte naar uw doel worden geëxporteerd. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolean | Stel deze parameter in op `true` als u wilt dat de geëxporteerde profielen worden samengevoegd in groepen op basis van één identiteit (GAID, IDFA, telefoonnummers, e-mail, enz.). Stel dit in op `false` als u de parameter `groups` wilt gebruiken om aangepaste naamruimtegroepen voor identiteiten te definiëren. |
| `configurableAggregation.aggregationKey.groups` | Array | Gebruik deze parameter wanneer `oneIdentityPerGroup` is ingesteld op `false` . Maak lijsten met identiteitsgroepen als u profielen wilt groeperen die naar uw doel zijn geëxporteerd door groepen naamruimten. U kunt bijvoorbeeld profielen die de mobiele id&#39;s IDFA en GAID bevatten, combineren in één aanroep naar uw bestemming en e-mails in een andere via de configuratie die in het bovenstaande voorbeeld wordt getoond. |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe u samenvoegingsbeleid voor uw bestemming kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Configuratie van klantverificatie](customer-authentication.md)
* [OAuth2-vergunning](oauth2-authorization.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [UI-kenmerken](ui-attributes.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte voor identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Configuratie van metagegevens voor publiek](audience-metadata-configuration.md)
* [Batchconfiguratie](batch-configuration.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)
