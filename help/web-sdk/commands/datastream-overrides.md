---
title: DataStream-configuratieoverschrijvingen
description: Leer hoe te om gegevensstroom met voeten te treden via het Web SDK.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '842'
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
   * Via de `sendEvent` - of `configure` Web SDK-opdrachten.
   * Via de opdracht Mobile SDK `sendEvent` .

Als u met voeten treedt zowel in de configuratie van SDK van het Web als in een specifiek bevel (zoals [`sendEvent`](sendevent/overview.md)), treedt de met voeten in het specifieke bevel belangrijkheid.

## Objecteigenschappen

De volgende eigenschappen zijn beschikbaar in dit object:

* **de opheffing van de Gegevensstroom**: Verzend vraag naar een verschillende gegevensstroom. Als u deze waarde plaatst, moeten andere met voeten treden die configuratie vereisen van de gegevensstroom in de hier geplaatste gegevensstroom worden gevormd.
* **de synchronisatiecontainer van de Derde van de identiteitskaart**: Identiteitskaart voor de de synchronisatiecontainer van de bestemmings derdeidentiteitskaart in Adobe Audience Manager. U moet een containeroverschrijving van een externe id configureren in de instellingen van de gegevensstroom voordat u dit veld kunt gebruiken.
* **het bezitstoken van het Doel**: Het teken voor het bestemmingsbezit in Adobe Target. Het vormen van een de bezitssymbolenopheffing van het Doel in de montages van de gegevensstroom wordt vereist alvorens dit gebied te gebruiken.
* **de reeksen van het Rapport**: De reeks IDs van het rapport om in Adobe Analytics met voeten te treden. U moet rapportsuite configureren met overschrijvingen in de instellingen van de gegevensstroom voordat u dit veld gebruikt.

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

In het onderstaande voorbeeld ziet u hoe een configuratieoverschrijving eruit zou kunnen zien op een `sendEvent` -opdracht.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| Parameter | Beschrijving |
|---|---|
| `edgeConfigOverrides.datastreamId` | Met deze parameter kan één aanvraag naar een andere gegevensstroom gaan dan de gegevensstroom die is gedefinieerd door de opdracht `configure` . |
| `com_adobe_analytics.reportSuites[]` | Een array van tekenreeksen die bepaalt naar welke rapportsuites analytische gegevens moeten worden verzonden. |
| `com_adobe_identity.idSyncContainerId` | De synchronisatiecontainer van een externe id die u in Audience Manager wilt gebruiken. |
| `com_adobe_target.propertyToken` | Het token voor de Adobe Target-doeleigenschap. |

### Configuratieoverschrijvingen verzenden via de opdracht Web SDK `configure` {#send-configure}

In het onderstaande voorbeeld ziet u hoe een configuratieoverschrijving eruit zou kunnen zien op een `configure` -opdracht.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

| Parameter | Beschrijving |
|---|---|
| `edgeConfigOverrides.datastreamId` | Met deze parameter kan één aanvraag naar een andere gegevensstroom gaan dan de gegevensstroom die is gedefinieerd door de opdracht `configure` . |
| `com_adobe_analytics.reportSuites[]` | Een array van tekenreeksen die bepaalt naar welke rapportsuites analytische gegevens moeten worden verzonden. |
| `com_adobe_identity.idSyncContainerId` | De synchronisatiecontainer van een externe id die u in Audience Manager wilt gebruiken. |
| `com_adobe_target.propertyToken` | Het token voor de Adobe Target-doeleigenschap. |
