---
title: edgeConfigOverrides
description: Vorm gegevensstroom met voeten treedt voor enkel het sendEvent bevel.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# `edgeConfigOverrides` (`sendEvent` opdracht)

Met het `edgeConfigOverrides` -object kunt u alleen voor de huidige `sendEvent` -opdracht de configuratie-instellingen overschrijven. Dit object is handig wanneer u specifieke opdrachten op dezelfde pagina hebt die u met andere configuratie-instellingen wilt uitvoeren dan de rest van de SDK-implementatie voor Web. Als u configuratiemontages voor alle bevelen op een bepaalde pagina wilt met voeten treden, denk na gebruikend het [`edgeConfigOverrides` voorwerp in het `configure` bevel ](../configure/edgeconfigoverrides.md).

Het overkoepelende proces van de gegevensstroomconfiguratie bestaat uit twee belangrijkste stappen:

1. Eerst, moet u uw de configuratieopheffing van de gegevensstroom bepalen wanneer [ vormend een datastream ](/help/datastreams/configure.md) in de UI van Gegevensstromen. Zie [ de configuratie DataStream met voeten treedt ](/help/datastreams/overrides.md) in de documentatie van gegevensstromen voor instructies op hoe te om met voeten te treden.
1. Nadat u de gegevensstroomoverschrijving in de gegevensstreams-gebruikersinterface hebt geconfigureerd, kunt u het `edgeConfigOverrides` -object configureren.

De opdracht `configure` ondersteunt ook een object `edgeConfigOverrides` . Zie [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) onder de opdracht `configure` . Het object `edgeConfigOverrides` in de opdracht `sendEvent` heeft voorrang op het object `edgeConfigOverrides` in de opdracht `configure` als beide zijn ingesteld.

## Voorbeeld

Als in uw configuratie van de gegevensstroom alle ondersteunde services zijn ingeschakeld, wordt in het onderstaande voorbeeld deze instelling genegeerd en worden alle services uitgeschakeld (zie de instelling `enabled: false` voor elke service). Dit object ondersteunt dezelfde eigenschappen als het object [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) in de opdracht `configure` .

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## De configuratie DataStream treedt met voeten gebruikend de de markeringsuitbreiding van SDK van het Web

Het de markeringsuitbreidingsequivalent van SDK van het Web van dit voorwerp is de [ configuratie DataStream treedt ](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides) sectie met voeten wanneer het vormen van &quot;[!UICONTROL Send event]&quot;actie.
