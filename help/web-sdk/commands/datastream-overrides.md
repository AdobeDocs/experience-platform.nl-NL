---
title: DataStream-configuratieoverschrijvingen
description: Leer hoe te om gegevensstroom met voeten te treden via het Web SDK.
source-git-commit: 9cb46957a1c9755dcad6279aae5f5cc04eb6b305
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---


# Gegevensstroomoverschrijvingen configureren

De `edgeConfigOverrides` kunt u de configuratie-instellingen overschrijven voor opdrachten die op de huidige pagina worden uitgevoerd. Dit met voeten getreden voorwerp is geen bevel, maar eerder een voorwerp dat u in de meeste bevelen van SDK van het Web kunt omvatten.

Dit object is handig wanneer u verschillende websites of subdomeinen voor verschillende landen hebt of wanneer u meerdere sandboxen voor Experience Platforms hebt om gegevens op te slaan die specifiek zijn voor verschillende bedrijfseenheden.

>[!IMPORTANT]
>
>Voor gedetailleerde, end-to-end configuratieinstructies voor gegevensstroomoverschrijvingen, zie [gegevensstroomconfiguratie overschrijft](../../datastreams/overrides.md#configure-overrides) documentatie.

De configuratieopheffing van gegevensstroom is een proces in twee stappen:

1. Eerst moet u de configuratieoverschrijving voor de gegevensstroom definiëren in het dialoogvenster [configuratiepagina gegevensstroom](../../datastreams/configure.md), binnen de UI van Datastreams. Zie de [gegevensstroomconfiguratie overschrijft](../../datastreams/overrides.md#configure-overrides) documentatie voor instructies over hoe te om overschrijvingen te vormen.
2. Nadat u de gegevensstroomopheffing in UI hebt gevormd, moet u de overschrijvingen naar het Netwerk van de Rand op één van de volgende manieren verzenden:
   * Via de web SDK [tagextensie](#tag-extension).
   * Via de `sendEvent` of `configure` Web SDK-opdrachten.
   * Via de mobiele SDK `sendEvent` gebruiken.

Als u plaatst treedt zowel in de configuratie van SDK van het Web als in een specifiek bevel met voeten (zoals [`sendEvent`](sendevent/overview.md)), hebben de overschrijvingen in het specifieke bevel voorrang.

## Objecteigenschappen

De volgende eigenschappen zijn beschikbaar in dit object:

* **DataStream overschrijven**: Verzend aanroepen naar een andere gegevensstroom. Als u deze waarde plaatst, moeten andere met voeten treden die configuratie vereisen van de gegevensstroom in de hier geplaatste gegevensstroom worden gevormd.
* **Identiteitskaart van derden synchronisatiecontainer**: De id voor de synchronisatiecontainer van de doel-id van derden in Adobe Audience Manager. U moet een containeroverschrijving van een externe id configureren in de instellingen van de gegevensstroom voordat u dit veld kunt gebruiken.
* **Eigenschap-token doel**: De token voor de eigenschap destination in Adobe Target. Het vormen van een de bezitssymbolenopheffing van het Doel in de montages van de gegevensstroom wordt vereist alvorens dit gebied te gebruiken.
* **Reeksen rapporteren**: De rapportsuite-id&#39;s die in Adobe Analytics moeten worden genegeerd. U moet rapportsuite configureren met overschrijvingen in de instellingen van de gegevensstroom voordat u dit veld gebruikt.

## Verstuur gegevensstroom met voeten treedt aan het Netwerk van de Rand door de de markeringsuitbreiding van SDK van het Web {#tag-extension}

Zie de documentatie op [configureren van gegevensstroomoverschrijvingen](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) van de de markeringsuitbreiding van SDK van het Web voor gedetailleerde configuratieinstructies.

Als u gegevensstroomoverschrijvingen van de de markeringsuitbreiding van SDK van het Web wilt vormen, plaats elk gewenst gebied onder **[!UICONTROL Datastream configuration overrides]** wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de **[!UICONTROL Datastream configuration overrides]** sectie. Stel elke gewenste overschrijvingswaarde in.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

Als u alleen voor een bepaalde opdracht overschrijvingen wilt instellen, stelt u elk gewenst veld in binnen de handelingen van een labelregel.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Send event]**.
1. Omlaag schuiven naar de sectie met het label **[!UICONTROL Datastream configuration overrides]**.
1. Stel elk veld in deze sectie in op de gewenste overschrijvingswaarde.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

Afzonderlijke velden zijn voorzien van [!UICONTROL Development], [!UICONTROL Staging], en [!UICONTROL Production] omgevingen. Zorg ervoor dat u elk gewenst veld voor elke omgeving invult.

## De overschrijvingen naar het Edge Network verzenden via de Web SDK JavaScript-bibliotheek {#library}

Na [configureren van gegevensstroomoverschrijvingen](../../datastreams/overrides.md) in de UI van de Inzameling van Gegevens, kunt u de met voeten getreden aan het Netwerk van de Rand, via de bibliotheek van SDK JavaScript van het Web verzenden.

Als u Web SDK gebruikt, verzendt het verzenden van de overschrijvingen naar het Netwerk van de Rand via `edgeConfigOverrides` bevel is de tweede en definitieve stap van het activeren van de configuratieoverschrijvingen van de gegevensstroom.

De gegevensstroomconfiguratieoverschrijvingen worden verzonden naar het Netwerk van de Rand door `edgeConfigOverrides` Web SDK, opdracht. Met deze opdracht maakt u gegevensstroomoverschrijvingen die worden doorgegeven aan de [!DNL Edge Network] op de volgende opdracht. Als u het `configure` , worden de overschrijvingen voor elk verzoek overgegaan.

De `edgeConfigOverrides` wordt gebruikt om gegevensstroomoverschrijvingen te maken die worden doorgegeven aan de [!DNL Edge Network] op de volgende opdracht.

Wanneer een configuratieopheffing met wordt verzonden `configure` bevel, is het inbegrepen op de volgende bevelen van SDK van het Web.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [vormen](../commands/configure/overview.md)

De opties globaal worden gespecificeerd kunnen door de configuratieoptie op individuele bevelen worden met voeten getreden.

### Verstuur configuratiemet voeten treedt via Web SDK `sendEvent` command {#send-event}

In het onderstaande voorbeeld ziet u hoe een configuratieoverschrijving eruit kan zien op een `sendEvent` gebruiken.

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
| `edgeConfigOverrides.datastreamId` | Met deze parameter kan één aanvraag naar een andere gegevensstroom gaan dan de gegevensstroom die door de `configure` gebruiken. |
| `com_adobe_analytics.reportSuites[]` | Een array van tekenreeksen die bepaalt naar welke rapportsuites analytische gegevens moeten worden verzonden. |
| `com_adobe_identity.idSyncContainerId` | De synchronisatiecontainer van een externe id die u in Audience Manager wilt gebruiken. |
| `com_adobe_target.propertyToken` | Het token voor de Adobe Target-doeleigenschap. |

### Verstuur configuratiemet voeten treedt via Web SDK `configure` command {#send-configure}

In het onderstaande voorbeeld ziet u hoe een configuratieoverschrijving eruit kan zien op een `configure` gebruiken.

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
| `edgeConfigOverrides.datastreamId` | Met deze parameter kan één aanvraag naar een andere gegevensstroom gaan dan de gegevensstroom die door de `configure` gebruiken. |
| `com_adobe_analytics.reportSuites[]` | Een array van tekenreeksen die bepaalt naar welke rapportsuites analytische gegevens moeten worden verzonden. |
| `com_adobe_identity.idSyncContainerId` | De synchronisatiecontainer van een externe id die u in Audience Manager wilt gebruiken. |
| `com_adobe_target.propertyToken` | Het token voor de Adobe Target-doeleigenschap. |