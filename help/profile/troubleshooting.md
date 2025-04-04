---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Handleiding voor het oplossen van problemen in realtime-klantprofiel
type: Documentation
description: Dit document bevat antwoorden op veelgestelde vragen over Real-Time klantprofiel en een gids voor probleemoplossing voor algemene fouten bij het werken met profielgegevens met Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---

# Handleiding voor het oplossen van problemen in realtime van klantprofielen

Dit document biedt antwoorden op veelgestelde vragen over Real-Time Klantprofiel en een gids voor probleemoplossing voor algemene fouten. Voor vragen en het oplossen van problemen met betrekking tot andere diensten in Adobe Experience Platform, gelieve te verwijzen naar de [ het oplossen van problemengids van Experience Platform ](../landing/troubleshooting.md).

Met [!DNL Real-Time Customer Profile], kunt u een holistische mening van elke individuele klant zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derde te combineren. Dit laat marketers toe om gecoördineerde, verenigbare, en relevante ervaringen voor klanten over veelvoudige kanalen te drijven.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over Real-Time klantprofiel.

### Welke soorten gegevens worden geaccepteerd voor Real-Time Klantprofiel?

Het profiel keurt zowel **verslag** als **tijd-reeks** gegevens goed, zolang de gegevens in kwestie minstens één identiteitswaarde bevat die de gegevens met een unieke individuele persoon associeert.

Net als bij alle Experience Platform-services moeten de gegevens van het profiel semantisch zijn gestructureerd volgens een XDM-schema (Experience Data Model). Omgekeerd, moet dit schema a **primaire identiteit** hebben bepaald en voor gebruik in Profiel worden toegelaten.

Als u met XDM onbekend bent, begin met het [ XDM overzicht ](../xdm/home.md) om meer te leren. Daarna, zie de XDM gebruikersgids voor stappen op hoe te [ plaats identiteitsgebieden ](../xdm/tutorials/create-schema-ui.md#identity-field) en [ een schema voor Profiel ](../xdm/tutorials/create-schema-ui.md#profile) toelaten.

### Waar worden profielgegevens opgeslagen?

In real time houdt het Profiel van de Klant zijn eigen gegevensopslag (die als &quot;opslag van het Profiel&quot;wordt bedoeld), los van het meer van Gegevens die andere opgenomen gegevens van Experience Platform bevat.

### Als ik al gegevens in Experience Platform heb ingevoerd, kan ik deze dan beschikbaar stellen in de winkel Profiel?

Als de gegevens in een niet-Profiel dataset zijn opgenomen, moet u die gegevens in een profiel-Toegelaten dataset opnieuw opnemen om het in de opslag van het Profiel ter beschikking te stellen. Het is mogelijk om een bestaande dataset voor Profiel toe te laten, echter om het even welke gegevens die voorafgaand aan die configuratie werden opgenomen zullen nog niet in de opslag van het Profiel verschijnen.

Als u wenst om eerder opgenomen gegevens aan de opslag van het Profiel toe te voegen, volg het [ leerprogramma van de datasetconfiguratie ](./tutorials/dataset-configuration.md) om een nieuwe dataset tot stand te brengen of een bestaande dataset om voor Profiel worden toegelaten om te zetten, en dan de gewenste gegevens in die dataset opnieuw op te nemen.

### Hoe kan ik mijn ingesloten profielgegevens bekijken?

Er zijn meerdere methoden om profielgegevens weer te geven, afhankelijk van het feit of u de API of UI gebruikt.

#### De API gebruiken

Als u de id&#39;s kent van de profielentiteiten waartoe u toegang wilt hebben, kunt u het eindpunt `/entities` (toegang tot profiel) in de profiel-API gebruiken om die entiteiten op te zoeken. Zie de sectie op [ entiteiten ](./api/entities.md) in de ontwikkelaarsgids voor meer informatie.

U kunt de Adobe Experience Platform Segmentation Service API ook gebruiken om toegang te krijgen tot de individuele profielen van klanten die voor een publiekslidmaatschap in aanmerking zijn gekomen. Zie het [ overzicht van de Dienst van de Segmentatie ](../segmentation/home.md) voor meer informatie.

#### UI gebruiken

In de gebruikersinterface van Experience Platform kunt u op het tabblad **[!UICONTROL Browse]** in de **[!UICONTROL Profiles]** -werkruimte het totale aantal profielen weergeven en naar afzonderlijke profielen zoeken op basis van hun identiteitswaarde. Zie de [ de gebruikersgids van het Profiel ](./ui/user-guide.md) voor meer informatie.

U kunt ook een lijst met uw publiek weergeven onder het tabblad **[!UICONTROL Browse]** in de werkruimte van **[!UICONTROL Audiences]** . Nadat u een publiek hebt geselecteerd, wordt een voorbeeld weergegeven van profielen die voor dat publiek zijn gekwalificeerd. Vervolgens kunt u een van deze profielen selecteren om de details weer te geven. Zie het [ overzicht van de Segmentatie UI ](../segmentation/ui/overview.md) voor meer informatie.

## Foutcodes

Hieronder volgt een lijst met foutberichten die u kunt tegenkomen wanneer u werkt met de Real-Time Customer Profile API. Als de fout u ontmoet niet hier vermeld is, kunt u het in de algemene [ het oplossen van problemengids van Experience Platform ](../landing/troubleshooting.md) in plaats daarvan vinden.

### Kan het opzoekschema van het berekende kenmerk voor het opgegeven pad niet opzoeken

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Wanneer het creëren van een nieuw gegevens verwerkt attribuut, komt deze fout voor wanneer het systeem niet het schema kon vinden dat in de verzoeklading wordt verstrekt. Zorg ervoor dat u de juiste huurder-id hebt opgegeven in de eigenschap `path` van de payload en dat de waarden van `schema.name` een geldige schemanaam zijn.

Als u uw huurdersidentiteitskaart niet kent, kunt u het terugwinnen door de stappen in de [ de ontwikkelaarsgids van de Registratie van het Schema ](../xdm/api/getting-started.md) te volgen.

### Functie met dezelfde naam bestaat al voor het opgegeven schema of definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Wanneer u een nieuw berekende kenmerk maakt, treedt deze fout op wanneer de opgegeven eigenschap `name` al wordt gebruikt voor het schema dat onder `schema.name` wordt aangegeven. Vervang de waarde door een unieke naam voordat u het opnieuw probeert.

### Retourschema van de expressie is niet hetzelfde als het schema van het berekende kenmerk in het XDM-schema

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Wanneer u een nieuw berekende kenmerk maakt, treedt deze fout op wanneer de opgegeven eigenschap `name` al wordt gebruikt voor het schema dat onder `schema.name` wordt aangegeven. Vervang de waarde door een unieke naam voordat u het opnieuw probeert.

### Ongeldig verwijderingsverzoek (profielsysteemtaak)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Deze fout treedt op wanneer een ongeldige lading voor een verwijdersysteembaan wordt verstrekt. Zorg ervoor dat u een geldige gegevensset of batch-id opgeeft onder de eigenschap `dataSetID` of `batchID` van de payload. Zie de sectie op [ creërend een schrappingsverzoek ](./api/profile-system-jobs.md#create-a-delete-request) in de de ontwikkelaarsgids van het Profiel voor meer informatie.

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

### Niet-ondersteund mediatype

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Deze fout treedt op wanneer een POST- of PUT-aanvraag met een ongeldige Content-Type-header wordt verzonden. Controleer tweemaal dat u een geldige Content-Type waarde voor het eindpunt verstrekt u gebruikt.

De meeste eindpunten van het Profiel keuren &quot;application/json&quot;voor hun Content-Type kopbal, met de volgende uitzonderingen goed:

| Endpoint | Inhoudstype |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
