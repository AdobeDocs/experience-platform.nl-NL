---
title: DataStream-configuratieoverschrijvingen
description: Leer hoe te om gegevensstroom met voeten te treden via het Web SDK.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# Gegevensstroomoverschrijvingen configureren

Met het `edgeConfigOverrides` -object kunt u configuratie-instellingen negeren voor opdrachten die op de huidige pagina worden uitgevoerd. Dit met voeten getreden voorwerp is geen bevel, maar eerder een voorwerp dat u in de meeste bevelen van SDK van het Web kunt omvatten.

Dit object is handig wanneer u verschillende websites of subdomeinen voor verschillende landen hebt of wanneer u meerdere sandboxen voor Experience Platforms hebt om gegevens op te slaan die specifiek zijn voor verschillende bedrijfseenheden.

>[!IMPORTANT]
>
>Voor gedetailleerde, van begin tot eind configuratieinstructies voor gegevensstroom treedt met voeten, zie de [ configuratie datastream met voeten ](../../datastreams/overrides.md#configure-overrides) documentatie.

De configuratieopheffing van gegevensstroom is een proces in twee stappen:

1. Eerst, moet u uw de configuratieopheffing van de gegevensstroom in de [ gegevenstream configuratiepagina ](../../datastreams/configure.md), binnen de Gebruikersstromen UI bepalen. Zie de [ configuratie datastream met voeten treedt ](../../datastreams/overrides.md#configure-overrides) documentatie voor instructies op hoe te om met voeten te treden.
2. Nadat u de gegevensstroomopheffing in UI hebt gevormd, moet u de overschrijvingen naar de Edge Network op één van de volgende manieren verzenden:
   * Door het Web SDK [ markeringsuitbreiding ](#tag-extension).
   * Via de [`sendEvent`](../commands/sendevent/overview.md) - of [`configure`](../commands/configure/overview.md) Web SDK-opdrachten.
   * Via de SDK van Mobile [`sendEvent` ](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network) bevel.

Als u met voeten treedt zowel in de configuratie van SDK van het Web als in een specifiek bevel (zoals [`sendEvent`](sendevent/overview.md)), treedt de met voeten in het specifieke bevel belangrijkheid.

>[!NOTE]
>
>Als u een configuratieopheffing wilt **&#x200B; onbruikbaar maken de dienst van het Experience Cloud, moet u ervoor zorgen dat de dienst eerst &#x200B;** in de configuratie van de gegevensstroom wordt toegelaten. Zie de documentatie op hoe te [ gegevensstromen ](../../datastreams/configure.md#add-services) voor details vormen over hoe te om de diensten aan een gegevensstroom toe te voegen.

## Verstuur gegevensstroom met voeten treedt aan de Edge Network door de de markeringsuitbreiding van SDK van het Web {#tag-extension}

Zie de documentatie op [ vormend datastream treedt ](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) van de de markeringsuitbreiding van SDK van het Web voor gedetailleerde configuratieinstructies met voeten.

Als u datastream met voeten treedt van de de markeringsuitbreiding van SDK van het Web wilt vormen, plaats elk gewenst gebied onder **[!UICONTROL Datastream configuration overrides]** wanneer [ vormend de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Datastream configuration overrides]** . Stel elke gewenste overschrijvingswaarde in.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

Als u alleen voor een bepaalde opdracht overschrijvingen wilt instellen, stelt u elk gewenst veld in binnen de handelingen van een labelregel.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Send event]** .
1. Schuif omlaag naar de sectie met het label **[!UICONTROL Datastream configuration overrides]** .
1. Stel elk veld in deze sectie in op de gewenste overschrijvingswaarde.
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

Afzonderlijke velden zijn beschikbaar voor [!UICONTROL Development] -, [!UICONTROL Staging] - en [!UICONTROL Production] -omgevingen. Zorg ervoor dat u elk gewenst veld voor elke omgeving invult.

## De overschrijvingen naar de Edge Network verzenden via de Web SDK JavaScript-bibliotheek {#library}

Na [ het vormen van de gegevensstroom treedt ](../../datastreams/overrides.md) in de Inzameling UI van Gegevens met voeten, kunt u de met voeten treedt naar de Edge Network, via de bibliotheek van JavaScript van SDK van het Web nu verzenden.

Als u Web SDK gebruikt, is het verzenden van de overschrijvingen naar de Edge Network via het `edgeConfigOverrides` bevel de tweede en laatste stap van het activeren van gegevensstroomconfiguratieoverschrijvingen.

De gegevensstroomconfiguratieoverschrijvingen worden verzonden naar de Edge Network door het `edgeConfigOverrides` bevel van SDK van het Web. Met deze opdracht maakt u gegevensstroomoverschrijvingen die worden doorgegeven aan de [!DNL Edge Network] op de volgende opdracht. Als u de opdracht `configure` gebruikt, worden de overschrijvingen voor elke aanvraag doorgegeven.

Met de opdracht `edgeConfigOverrides` maakt u gegevensstroomoverschrijvingen die worden doorgegeven aan de [!DNL Edge Network] op de volgende opdracht.

Wanneer een configuratieopheffing met het `configure` bevel wordt verzonden, is het inbegrepen op de volgende bevelen van SDK van het Web.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [vormen](../commands/configure/overview.md)

De opties globaal worden gespecificeerd kunnen door de configuratieoptie op individuele bevelen worden met voeten getreden.

### Configuratieoverschrijvingen verzenden via de opdracht Web SDK `sendEvent` {#send-event}

In het onderstaande voorbeeld worden alle dynamische configuratieopties voor de gegevensstroom weergegeven die door een `sendEvent` -aanroep worden ondersteund.

Als in uw configuratie van de gegevensstroom alle ondersteunde services zijn ingeschakeld, wordt deze instelling in het onderstaande voorbeeld genegeerd en worden alle services uitgeschakeld (zie de instelling `enabled: false` voor elke service).

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
      reportSuites: ["ujslconfigoverrides3"],
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

| Parameter | Beschrijving |
|---|---|
| `renderDecisions` |  |
| `edgeConfigOverrides.datastreamId` | Met deze parameter kan één aanvraag naar een andere gegevensstroom gaan dan de gegevensstroom die is gedefinieerd door de opdracht `configure` . |
| `edgeConfigOverrides.com_adobe_experience_platform` | Bepaalt de dynamische configuratie van de gegevensstroom voor de dienst van het Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Bepaalt of de gebeurtenis naar de dienst van het Experience Platform of niet zal worden verzonden. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Bepaalt de datasets die voor de gebeurtenis worden gebruikt. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Bepaalt of de gebeurtenis wordt verzonden naar de dienst van de Offer decisioning of niet. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Bepaalt of de gebeurtenis naar de dienst van de randsegmentatie wordt verzonden of niet. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Bepaalt of de gebeurtenisgegevens naar de randbestemmingen worden verzonden of niet. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definieert of de gebeurtenisgegevens naar de Adobe Journey Optimizer-service worden verzonden. |
| `com_adobe_analytics.enabled` | Definieert of de gebeurtenisgegevens naar Adobe Analytics worden verzonden. |
| `com_adobe_analytics.reportSuites[]` | Een array van tekenreeksen die bepaalt naar welke rapportsuites u analysegegevens wilt verzenden. |
| `com_adobe_identity.idSyncContainerId` | De synchronisatiecontainer van een externe id die u in Audience Manager wilt gebruiken. Deze ID-synchronisatiecontainer werkt alleen als u `com_adobe_audience_manager.enabled` instelt op `true` . Anders wordt de service Audience Manager uitgeschakeld. |
| `com_adobe_target.enabled` | Definieert of de gebeurtenisgegevens naar Adobe Target worden verzonden. |
| `com_adobe_target.propertyToken` | Het token voor de Adobe Target-doeleigenschap. |
| `com_adobe_audience_manager.enabled` | Bepaalt of de gebeurtenisgegevens naar de dienst van de Audience Manager worden verzonden. |
| `com_adobe_launch_ssf` | Bepaalt of de gebeurtenisgegevens naar server-kant door:sturen worden verzonden. |

### Configuratieoverschrijvingen verzenden via de opdracht Web SDK `configure` {#send-configure}

In het onderstaande voorbeeld ziet u hoe een configuratieoverschrijving eruit zou kunnen zien op een `configure` -opdracht.

Als in uw configuratie van de gegevensstroom alle ondersteunde services zijn ingeschakeld, wordt deze instelling in het onderstaande voorbeeld genegeerd en worden alle services uitgeschakeld (zie de instelling `enabled: false` voor elke service).

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77",
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
      reportSuites: ["ujslconfigoverrides2"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34373,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94",
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

| Parameter | Beschrijving |
|---|---|
| `orgId` | De IMS-organisatie-id die overeenkomt met uw Adobe-account. |
| `edgeConfigOverrides.datastreamId` | Met deze parameter kan één aanvraag naar een andere gegevensstroom gaan dan de gegevensstroom die is gedefinieerd door de opdracht `configure` . |
| `edgeConfigOverrides.com_adobe_experience_platform` | Bepaalt de dynamische configuratie van de gegevensstroom voor de dienst van het Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Bepaalt of de gebeurtenis naar de dienst van het Experience Platform of niet zal worden verzonden. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Bepaalt de datasets die voor de gebeurtenis worden gebruikt. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Bepaalt of de gebeurtenis wordt verzonden naar de dienst van de Offer decisioning of niet. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Bepaalt of de gebeurtenis naar de dienst van de randsegmentatie wordt verzonden of niet. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Bepaalt of de gebeurtenisgegevens naar de randbestemmingen worden verzonden of niet. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definieert of de gebeurtenisgegevens naar de Adobe Journey Optimizer-service worden verzonden. |
| `com_adobe_analytics.enabled` | Definieert of de gebeurtenisgegevens naar Adobe Analytics worden verzonden. |
| `com_adobe_analytics.reportSuites[]` | Een array van tekenreeksen die bepaalt naar welke rapportsuites u analysegegevens wilt verzenden. |
| `com_adobe_identity.idSyncContainerId` | De synchronisatiecontainer van een externe id die u in Audience Manager wilt gebruiken. Deze ID-synchronisatiecontainer werkt alleen als u `com_adobe_audience_manager.enabled` instelt op `true` . Anders wordt de service Audience Manager uitgeschakeld. |
| `com_adobe_target.enabled` | Definieert of de gebeurtenisgegevens naar Adobe Target worden verzonden. |
| `com_adobe_target.propertyToken` | Het token voor de Adobe Target-doeleigenschap. |
| `com_adobe_audience_manager.enabled` | Bepaalt of de gebeurtenisgegevens naar de dienst van de Audience Manager worden verzonden. |
| `com_adobe_launch_ssf` | Bepaalt of de gebeurtenisgegevens naar server-kant door:sturen worden verzonden. |

