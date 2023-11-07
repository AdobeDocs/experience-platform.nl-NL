---
description: Leer hoe te om de montages van de bestemmingslevering voor bestemmingen te vormen die met Destination SDK worden gebouwd, om erop te wijzen waar de uitgevoerde gegevens gaan en welke authentificatieregel in de plaats wordt gebruikt waar de gegevens zullen landen.
title: Levering bestemming
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---

# Levering bestemming

Om meer controle over aan te bieden waar de gegevens die naar uw bestemmingslanden worden uitgevoerd, staat Destination SDK u toe om de montages van de bestemmingslevering te specificeren.

De sectie van de bestemmingslevering wijst op waar de uitgevoerde gegevens gaan en welke authentificatieregel in de plaats wordt gebruikt waar de gegevens zullen landen.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in [configuratieopties](../configuration-options.md) documentatie of zie de volgende pagina&#39;s van het overzicht van bestemmingsconfiguratie:

* [Gebruik Destination SDK om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

U kunt de instellingen voor de levering van de bestemming configureren via `/authoring/destinations` eindpunt. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

In dit artikel worden alle ondersteunde leveringsopties voor de bestemming beschreven.

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

Wanneer het vormen van uw montages van de bestemmingslevering, kunt u de parameters gebruiken die in de lijst hieronder worden beschreven om te bepalen waar de uitgevoerde gegevens zouden moeten worden verzonden.

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform] moet verbinding maken met uw doel. Ondersteunde waarden:<ul><li>`CUSTOMER_AUTHENTICATION`: Gebruik deze optie als de klanten van het Platform zich bij uw systeem via om het even welke beschreven authentificatiemethodes aanmelden [hier](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Gebruik deze optie als er een algemeen verificatiesysteem is tussen Adobe en uw doel en de [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een object credentials maken met de opdracht [aanmeldAPI](../../credentials-api/create-credential-configuration.md) configuratie. </li><li>`NONE`: Gebruik deze optie als er geen verificatie vereist is om gegevens naar het doelplatform te verzenden. </li></ul> |
| `destinationServerId` | Tekenreeks | De `instanceId` van de [doelserver](../../authoring-api/destination-server/create-destination-server.md) waarnaar u gegevens wilt exporteren. |
| `deliveryMatchers.type` | Tekenreeks | <ul><li>Wanneer het vormen van bestemmingslevering voor op dossier-gebaseerde bestemmingen, plaats altijd dit aan `SOURCE`.</li><li>Wanneer het vormen van bestemmingslevering voor een het stromen bestemming, `deliveryMatchers` is niet vereist.</li></ul> |
| `deliveryMatchers.value` | Tekenreeks | <ul><li>Wanneer het vormen van bestemmingslevering voor op dossier-gebaseerde bestemmingen, plaats altijd dit aan `batch`.</li><li>Wanneer het vormen van bestemmingslevering voor een het stromen bestemming, `deliveryMatchers` is niet vereist.</li></ul> |

{style="table-layout:auto"}

## Instellingen voor levering van bestemming voor streamingdoelen {#destination-delivery-streaming}

In het onderstaande voorbeeld ziet u hoe de instellingen voor de doellevering moeten worden geconfigureerd voor een streamingbestemming. Let erop dat de `deliveryMatchers` sectie is niet vereist voor streamingdoelen.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## De leveringsmontages van de bestemming voor op dossier-gebaseerde bestemmingen {#destination-delivery-file-based}

In het onderstaande voorbeeld ziet u hoe de instellingen voor de doellevering moeten worden geconfigureerd voor een op een bestand gebaseerde bestemming. Let erop dat de `deliveryMatchers` sectie is vereist voor op bestanden gebaseerde doelen.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben hoe u de plaatsen kunt vormen waar uw bestemming gegevens, voor zowel het stromen als op dossier-gebaseerde bestemmingen zou moeten uitvoeren.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Verificatie door klant](customer-authentication.md)
* [OAuth2-verificatie](oauth2-authorization.md)
* [UI-kenmerken](ui-attributes.md)
* [Gegevensvelden van de klant](customer-data-fields.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte voor identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Configuratie van metagegevens voor publiek](audience-metadata-configuration.md)
* [Samenvoegingsbeleid](aggregation-policy.md)
* [Batchconfiguratie](batch-configuration.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)
