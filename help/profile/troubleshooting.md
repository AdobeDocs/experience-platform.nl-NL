---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor het oplossen van problemen in realtime van klantprofielen
topic: guide
translation-type: tm+mt
source-git-commit: 94fd6ee324b35acb7ef1185f7851d76d76f3e91c
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---


# Handleiding voor het oplossen van problemen in realtime van klantprofielen

Dit document biedt antwoorden op veelgestelde vragen over het Real-time profiel van de Klant en een gids voor probleemoplossing voor algemene fouten. Voor vragen en het oplossen van problemen met betrekking tot andere diensten in Adobe Experience Platform, gelieve te verwijzen naar de het oplossen van problemengids [van het](../landing/troubleshooting.md)Experience Platform.

Klantprofiel in real-time is een algemene opzoekeenheid die gegevens uit verschillende bedrijfsgegevenselementen samenvoegt en vervolgens toegang tot die gegevens biedt in de vorm van individuele klantprofielen en gerelateerde tijdreeksgebeurtenissen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over Real-time klantprofiel.

### Welke soorten gegevens worden goedgekeurd voor het Profiel van de Klant in real time?

Profiel accepteert zowel **recordgegevens** als **tijdreeksgegevens** , zolang de gegevens in kwestie ten minste één identiteitswaarde bevatten die de gegevens aan een unieke individuele persoon koppelt.

Zoals alle diensten van het Platform, vereist het Profiel dat zijn gegevens semantisch onder een schema van de Gegevens van de Ervaring van het Model (XDM) worden gestructureerd. Voor dit schema moet op zijn beurt een **primaire identiteit** zijn gedefinieerd en ingeschakeld voor gebruik in Profiel.

Als u niet bekend bent met XDM, start u met het [XDM-overzicht](../xdm/home.md) voor meer informatie. Raadpleeg vervolgens de XDM-gebruikershandleiding voor informatie over het [instellen van identiteitsvelden](../xdm/tutorials/create-schema-ui.md#identity-field) en het [inschakelen van een schema voor Profiel](../xdm/tutorials/create-schema-ui.md#profile).

### Waar worden profielgegevens opgeslagen?

Klantprofiel in realtime onderhoudt zijn eigen gegevensopslag (de &quot;profielopslag&quot; genoemd), gescheiden van het Data Lake dat andere opgenomen gegevens van het Platform bevat.

### Als ik al gegevens in het Platform heb ingevoerd, kan ik deze dan beschikbaar stellen in het archief met profielen?

Als de gegevens in een niet-Profiel dataset zijn opgenomen, moet u die gegevens in een profiel-Toegelaten dataset opnieuw opnemen om het in de opslag van het Profiel ter beschikking te stellen. Het is mogelijk om een bestaande dataset voor Profiel toe te laten, echter om het even welke gegevens die voorafgaand aan die configuratie werden opgenomen zullen nog niet in de opslag van het Profiel verschijnen.

Als u wenst om eerder ingebedde gegevens aan de opslag van het Profiel toe te voegen, volg het [gegevensbestand configuratieleerprogramma](./tutorials/dataset-configuration.md) om een nieuwe dataset tot stand te brengen of een bestaande dataset om voor Profiel worden toegelaten om te zetten, en dan de gewenste gegevens in die dataset opnieuw in te voeren.

### Hoe kan ik mijn ingesloten profielgegevens bekijken?

Er zijn meerdere methoden om profielgegevens weer te geven, afhankelijk van het feit of u de API of UI gebruikt.

#### De API gebruiken

Als u de id&#39;s kent van de profielentiteiten waartoe u toegang wilt hebben, kunt u het eindpunt `/entities` (toegang profiel) in de profiel-API gebruiken om die entiteiten op te zoeken. Zie de sectie over [entiteiten](./api/entities.md) in de ontwikkelaarsgids voor meer informatie.

U kunt de Dienst API van de Segmentatie van het Adobe Experience Platform ook gebruiken om tot de individuele profielen van klanten toegang te hebben die voor een segmentlidmaatschap gekwalificeerd zijn. Zie het overzicht [van de Dienst van de](../segmentation/home.md) Segmentatie voor meer informatie.

#### De gebruikersinterface gebruiken

In de gebruikersinterface van het Experience Platform kunt u op het tabblad **[!UICONTROL Bladeren]** in de werkruimte **[!UICONTROL Profielen]** het totale aantal profielen weergeven en naar afzonderlijke profielen zoeken op basis van hun identiteitswaarde. Raadpleeg de gebruikershandleiding bij [Profiel](./ui/user-guide.md) voor meer informatie.

U kunt ook een lijst met uw segmenten weergeven onder het tabblad **[!UICONTROL Bladeren]** in de werkruimte **[!UICONTROL Segmenten]** . Nadat u een segment hebt geselecteerd, wordt een voorbeeld met profielen weergegeven die voor dat segment zijn gekwalificeerd. Vervolgens kunt u een van deze profielen selecteren om de details weer te geven. Zie het overzicht [van de](../segmentation/ui/overview.md) Segmentatie UI voor meer informatie.

## Foutcodes

Hieronder volgt een lijst met foutberichten die u kunt tegenkomen wanneer u werkt met de Real-Time Customer Profile API. Als de fout u ontmoet niet hier vermeld is, kunt u het in plaats daarvan in de algemene gids [van het oplossen van problemenoplossing van](../landing/troubleshooting.md) Platforms vinden.

### Kan het opzoekschema van het berekende kenmerk voor het opgegeven pad niet opzoeken

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Wanneer het creëren van een nieuw gegevens verwerkt attribuut, komt deze fout voor wanneer het systeem niet het schema kon vinden dat in de verzoeklading wordt verstrekt. Zorg ervoor dat u correcte huurdersidentiteitskaart in het `path` bezit van de nuttige lading hebt verstrekt, en dat de waarden van een geldige schemanaam `schema.name` zijn.

Als u niet uw huurdersidentiteitskaart kent, kunt u het terugwinnen door de stappen in de de ontwikkelaarsgids [van de Registratie van het](../xdm/api/getting-started.md)Schema te volgen.

### Functie met dezelfde naam bestaat al voor het opgegeven schema of definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Wanneer het creëren van een nieuw gegevens verwerkt attribuut, komt deze fout voor wanneer het verstrekte `name` bezit reeds voor het schema wordt gebruikt dat onder wordt vermeld `schema.name`. Vervang de waarde door een unieke naam voordat u het opnieuw probeert.

### Retourschema van de expressie is niet hetzelfde als het schema van het berekende kenmerk in het XDM-schema

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Wanneer het creëren van een nieuw gegevens verwerkt attribuut, komt deze fout voor wanneer het verstrekte `name` bezit reeds voor het schema wordt gebruikt dat onder wordt vermeld `schema.name`. Vervang de waarde door een unieke naam voordat u het opnieuw probeert.

### Ongeldig verwijderingsverzoek (profielsysteemtaak)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Deze fout treedt op wanneer een ongeldige lading voor een verwijdersysteembaan wordt verstrekt. Zorg ervoor dat u een geldige dataset of batch-id opgeeft onder respectievelijk de eigenschap `dataSetID` of `batchID` eigenschap van de payload. Zie de sectie over het [maken van een verwijderaanvraag](./api/profile-system-jobs.md#create-a-delete-request) in de handleiding voor ontwikkelaars van profielen voor meer informatie.

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

Deze fout treedt op wanneer de `destinationId` in een `POST /config/projections` aanvraag opgegeven fout ongeldig is. Controleer of u een geldige doel-id hebt opgegeven voordat u het opnieuw probeert. Als u een nieuwe bestemming wilt maken, volgt u de stappen in de handleiding voor [profielontwikkeling](./api/edge-projections.md#create-a-destination).

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