---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Handleiding voor het oplossen van problemen in realtime-profielen van klanten
topic: guide
type: Documentation
description: Dit document bevat antwoorden op veelgestelde vragen over het realtime-klantprofiel en een gids voor probleemoplossing voor algemene fouten bij het werken met profielgegevens met Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# Handleiding voor het oplossen van problemen in realtime van klantprofielen

Dit document biedt antwoorden op veelgestelde vragen over het Real-time profiel van de Klant en een gids voor probleemoplossing voor algemene fouten. Raadpleeg de [handleiding voor het oplossen van Experience Platforms](../landing/troubleshooting.md) voor vragen en het oplossen van problemen met betrekking tot andere services in Adobe Experience Platform.

Met [!DNL Real-time Customer Profile] kunt u een holistische mening van elke individuele klant zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derde te combineren. Dit laat marketers toe om gecoördineerde, verenigbare, en relevante ervaringen voor klanten over veelvoudige kanalen te drijven.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over Real-time klantprofiel.

### Welke soorten gegevens worden goedgekeurd voor het Profiel van de Klant in real time?

Profiel accepteert zowel **record**- als **tijdreeks**-gegevens, mits de gegevens in kwestie ten minste één identiteitswaarde bevatten die de gegevens aan een unieke individuele persoon koppelt.

Zoals alle diensten van het Platform, vereist het Profiel dat zijn gegevens semantisch onder een schema van de Gegevens van de Ervaring van het Model (XDM) worden gestructureerd. Dit schema moet op zijn beurt een **primaire identiteit** hebben gedefinieerd en zijn ingeschakeld voor gebruik in Profiel.

Als u niet vertrouwd met XDM bent, begin met [XDM overzicht](../xdm/home.md) om meer te leren. Zie vervolgens de XDM-gebruikershandleiding voor stappen voor het [instellen van identiteitsvelden](../xdm/tutorials/create-schema-ui.md#identity-field) en [inschakelen van een schema voor Profiel](../xdm/tutorials/create-schema-ui.md#profile).

### Waar worden profielgegevens opgeslagen?

Klantprofiel in realtime onderhoudt zijn eigen gegevensopslag (de &quot;profielopslag&quot; genoemd), gescheiden van het Data Lake dat andere opgenomen gegevens van het Platform bevat.

### Als ik al gegevens in het Platform heb ingevoerd, kan ik deze dan beschikbaar stellen in het archief met profielen?

Als de gegevens in een niet-Profiel dataset zijn opgenomen, moet u die gegevens in een profiel-Toegelaten dataset opnieuw opnemen om het in de opslag van het Profiel ter beschikking te stellen. Het is mogelijk om een bestaande dataset voor Profiel toe te laten, echter om het even welke gegevens die voorafgaand aan die configuratie werden opgenomen zullen nog niet in de opslag van het Profiel verschijnen.

Als u wenst om eerder ingebedde gegevens aan de opslag van het Profiel toe te voegen, volg [de zelfstudie van de datasetconfiguratie](./tutorials/dataset-configuration.md) om een nieuwe dataset tot stand te brengen of een bestaande dataset om te zetten die voor Profiel moet worden toegelaten, en dan de gewenste gegevens in die dataset opnieuw op te nemen.

### Hoe kan ik mijn ingesloten profielgegevens bekijken?

Er zijn meerdere methoden om profielgegevens weer te geven, afhankelijk van het feit of u de API of UI gebruikt.

#### De API gebruiken

Als u de id&#39;s kent van de profielentiteiten waartoe u toegang wilt hebben, kunt u het `/entities`-eindpunt (toegang tot profiel) in de profiel-API gebruiken om die entiteiten op te zoeken. Zie de sectie over [entiteiten](./api/entities.md) in de ontwikkelaarsgids voor meer informatie.

U kunt de Adobe Experience Platform Segmentation Service API ook gebruiken om tot de individuele profielen van klanten toegang te hebben die voor een segmentlidmaatschap gekwalificeerd zijn. Zie [Overzicht van de Dienst van de Segmentatie](../segmentation/home.md) voor meer informatie.

#### De gebruikersinterface gebruiken

In het Experience Platform UI, **[!UICONTROL Browse]** lusje in **[!UICONTROL Profielen]** werkruimte staat u toe om het totale profielaantal te bekijken en naar individuele profielen op hun identiteitswaarde te zoeken. Zie [Gebruikershandleiding voor profielen](./ui/user-guide.md) voor meer informatie.

U kunt een lijst van uw segmenten onder **[!UICONTROL Browse]** lusje in **[!UICONTROL Segmenten]** werkruimte ook bekijken. Nadat u een segment hebt geselecteerd, wordt een voorbeeld met profielen weergegeven die voor dat segment zijn gekwalificeerd. Vervolgens kunt u een van deze profielen selecteren om de details weer te geven. Zie [Overzicht van de Segmentatie UI](../segmentation/ui/overview.md) voor meer informatie.

## Foutcodes

Hieronder volgt een lijst met foutberichten die u kunt tegenkomen wanneer u werkt met de Real-Time Customer Profile API. Als de fout u ontmoet niet hier vermeld is, kunt u het in plaats daarvan in de algemene [gids van de het oplossen van problemenoplossing van het Platform](../landing/troubleshooting.md) vinden.

### Kan het opzoekschema van het berekende kenmerk voor het opgegeven pad niet opzoeken

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Wanneer het creëren van een nieuw gegevens verwerkt attribuut, komt deze fout voor wanneer het systeem niet het schema kon vinden dat in de verzoeklading wordt verstrekt. Zorg ervoor dat u correcte huurdersidentiteitskaart in het bezit `path` van de lading hebt verstrekt, en dat de waarden van `schema.name` een geldige schemanaam zijn.

Als u uw huurder identiteitskaart niet kent, kunt u het terugwinnen door de stappen in [de ontwikkelaarsgids van de Registratie van het Schema](../xdm/api/getting-started.md) te volgen.

### Functie met dezelfde naam bestaat al voor het opgegeven schema of definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Wanneer het creëren van een nieuw gegevens verwerkt attribuut, komt deze fout voor wanneer het verstrekte `name` bezit reeds voor het schema wordt gebruikt dat onder `schema.name` wordt vermeld. Vervang de waarde door een unieke naam voordat u het opnieuw probeert.

### Retourschema van de expressie is niet hetzelfde als het schema van het berekende kenmerk in het XDM-schema

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Wanneer het creëren van een nieuw gegevens verwerkt attribuut, komt deze fout voor wanneer het verstrekte `name` bezit reeds voor het schema wordt gebruikt dat onder `schema.name` wordt vermeld. Vervang de waarde door een unieke naam voordat u het opnieuw probeert.

### Ongeldig verwijderingsverzoek (profielsysteemtaak)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Deze fout treedt op wanneer een ongeldige lading voor een verwijdersysteembaan wordt verstrekt. Zorg ervoor dat u een geldige dataset of batch-id opgeeft onder de eigenschap `dataSetID` of `batchID` van de payload. Zie de sectie over [het creëren van een schrappingsverzoek](./api/profile-system-jobs.md#create-a-delete-request) in de de ontwikkelaarsgids van het Profiel voor meer informatie.

### Batch niet gevonden voor profielgegevensset

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

Deze fout treedt op wanneer een geldige batch niet kan worden gevonden tijdens een poging een aanvraag tot verwijderen van profielgegevens te maken. Controleer of u de juiste id hebt ingevoerd voor een gegevensset waarvoor profiel is ingeschakeld voordat u het opnieuw probeert.

### De projectiebestemming is nog niet gecreeerd

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Deze fout treedt op wanneer de `destinationId` die in een `POST /config/projections` verzoek wordt verstrekt ongeldig is. Controleer of u een geldige doel-id hebt opgegeven voordat u het opnieuw probeert. Om een nieuwe bestemming tot stand te brengen, volg de stappen in [de gids van de ontwikkelaar van het profiel](./api/edge-projections.md#create-a-destination) worden geschetst.

### Niet-ondersteund mediatype

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Deze fout treedt op wanneer een POST- of PUT-aanvraag wordt verzonden met een ongeldige Content-Type-header. Controleer tweemaal dat u een geldige Content-Type waarde voor het eindpunt verstrekt u gebruikt.

De meeste eindpunten van het Profiel keuren &quot;application/json&quot;voor hun Content-Type kopbal, met de volgende uitzonderingen goed:

| Endpoint | Inhoudstype |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |