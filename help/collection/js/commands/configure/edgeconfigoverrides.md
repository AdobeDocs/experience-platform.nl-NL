---
title: edgeConfigOverrides
description: Configureer gegevensstroomoverschrijvingen voor uw implementatie.
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides` (`configure` opdracht)

Met het `edgeConfigOverrides` -object kunt u configuratie-instellingen negeren voor opdrachten die op de huidige pagina worden uitgevoerd. Dit object is handig wanneer u verschillende websites of subdomeinen voor verschillende landen hebt of wanneer u meerdere Experience Platform-sandboxen hebt om gegevens op te slaan die specifiek zijn voor verschillende bedrijfseenheden. Als u configuratiemontages voor slechts één enkel bevel op de pagina wilt met voeten treden, denk na gebruikend het [`edgeConfigOverrides` voorwerp in het `sendEvent` bevel &#x200B;](../sendevent/edgeconfigoverrides.md).

Het configuratieoverschrijfproces van de gegevensstroom bestaat uit twee hoofdstappen:

1. Eerst, moet u uw de configuratieopheffing van de gegevensstroom bepalen wanneer [&#x200B; vormend een datastream &#x200B;](/help/datastreams/configure.md) in de UI van Gegevensstromen. Zie [&#x200B; de configuratie DataStream met voeten treedt &#x200B;](/help/datastreams/overrides.md) in de documentatie van gegevensstromen voor instructies op hoe te om met voeten te treden.
1. Nadat u de gegevensstroomoverschrijving in de gegevensstreams-gebruikersinterface hebt geconfigureerd, kunt u het `edgeConfigOverrides` -object configureren.

Wanneer u het `edgeConfigOverrides` -object instelt in de opdracht `configure` , geldt dit voor alle gegevens die naar Adobe worden verzonden. De volgende bevelen __ steunen ook het `edgeConfigOverrides` voorwerp:

* [` sendEvent`](../sendevent/edgeconfigoverrides.md)
* [` setConsent`](../setconsent.md)
* [getIdentity&grave;](../getidentity.md)
* [` appendIdentityToUrl`](../appendidentitytourl.md)

Het instellen van `edgeConfigOverrides` in een van de bovenstaande opdrachten heeft voorrang op het object `edgeConfigOverrides` in de opdracht `configure` als beide opdrachten zijn ingesteld. Als een van deze opdrachten geen `edgeConfigOverrides` -object bevat, wordt het `edgeConfigOverrides` -object in de opdracht `configure` gebruikt.

## Voorbeeld

Als alle ondersteunde services zijn ingeschakeld in uw configuratie van de gegevensstroom, overschrijft het voorbeeld hieronder deze instelling en worden alle services uitgeschakeld.

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| Parameter | Type | Beschrijving |
| --- | --- | --- |
| **`orgId`** | `string` | De IMS org-id van uw bedrijf. |
| **`datastreamId`** | `string` | De gegevensstroom-id waarnaar gegevens moeten worden verzonden. |
| **`com_adobe_experience_platform`** | `object` | Definieert de dynamische gegevensstroomconfiguratie voor Adobe Experience Platform-services. |
| **`com_adobe_experience_platform.enabled`** | `boolean` | Bepaalt of de gebeurtenis naar Adobe Experience Platform wordt verzonden. |
| **`com_adobe_experience_platform.datasets`** | `object` | Bepaalt de datasets die voor de gebeurtenis worden gebruikt. |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | Bepaalt of de gebeurtenis naar Offer Decisioning wordt verzonden. |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | Bepaalt of de gebeurtenis naar Edge Segmentation wordt verzonden. |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | Hiermee wordt bepaald of de gebeurtenis naar Edge-doelen wordt verzonden. |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | Bepaalt of de gebeurtenis Adobe Journey Optimizer wordt verzonden. |
| **`com_adobe_analytics.enabled`** | `boolean` | Bepaalt of de gebeurtenis naar Adobe Analytics wordt verzonden. |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | Een array van tekenreeksen die bepaalt naar welke rapportsuites analytische gegevens moeten worden verzonden. |
| **`com_adobe_audience_manager.enabled`** | `boolean` | Bepaalt of de gebeurtenis naar Adobe Audience Manager wordt verzonden. |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | De synchronisatie-container voor externe id&#39;s die u in Audience Manager wilt gebruiken. Vereist dat `com_adobe_audience_manager.enabled` is ingesteld op `true` . Anders wordt de Audience Manager-service uitgeschakeld. |
| **`com_adobe_target.enabled`** | `boolean` | Bepaalt of de gebeurtenis naar Adobe Target wordt verzonden. |
| **`com_adobe_target.propertyToken`** | `string` | Het token voor de Adobe Target-doeleigenschap. |
| **`com_adobe_launch_ssf`** | `boolean` | Bepaalt als de gebeurtenis wordt verzonden naar server-kant door:sturen. |

## Configuratieoverschrijvingen met de Web SDK-tagextensie

Het de markeringsequivalent van SDK van het Web van dit gebied is onder [&#x200B; met voeten treedt van de Configuratie &#x200B;](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md) wanneer het vormen van de markeringsuitbreiding.
