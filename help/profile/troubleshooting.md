---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Handleiding voor het oplossen van problemen in realtime-klantprofiel
type: Documentation
description: Dit document bevat antwoorden op veelgestelde vragen over Real-Time klantprofiel en een gids voor probleemoplossing voor algemene fouten bij het werken met profielgegevens met Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: dde38e230a6bcb10cd38a12f644f2dd03f0cebaf
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# Handleiding voor het oplossen van problemen in realtime van klantprofielen

Dit document biedt antwoorden op veelgestelde vragen over Real-Time Klantprofiel en een gids voor probleemoplossing voor algemene fouten. Voor vragen en problemen met betrekking tot andere services in Adobe Experience Platform raadpleegt u de [Handleiding voor het oplossen van problemen met Experience Platforms](../landing/troubleshooting.md).

Met [!DNL Real-Time Customer Profile], kunt u een holistische mening van elke individuele klant zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derde te combineren. Dit laat marketers toe om gecoördineerde, verenigbare, en relevante ervaringen voor klanten over veelvoudige kanalen te drijven.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over Real-Time klantprofiel.

### Welke soorten gegevens worden geaccepteerd voor Real-Time Klantprofiel?

Profiel accepteert beide **opnemen** en **tijdreeks** gegevens, zolang de gegevens in kwestie ten minste één identiteitswaarde bevatten die de gegevens aan een unieke individuele persoon associeert.

Zoals alle diensten van het Platform, vereist het Profiel dat zijn gegevens semantisch onder een schema van de Gegevens van de Ervaring worden gestructureerd Model (XDM). Dit schema moet een **primaire identiteit** gedefinieerd en ingeschakeld voor gebruik in profiel.

Als u niet bekend bent met XDM, start u met de [XDM-overzicht](../xdm/home.md) voor meer informatie. Raadpleeg de XDM-gebruikershandleiding voor meer informatie over [identiteitsvelden instellen](../xdm/tutorials/create-schema-ui.md#identity-field) en [een schema voor profiel inschakelen](../xdm/tutorials/create-schema-ui.md#profile).

### Waar worden profielgegevens opgeslagen?

Het profiel van de Klant in real time handhaaft zijn eigen gegevensopslag (die als &quot;opslag van het Profiel&quot;wordt bedoeld), los van het meer van Gegevens dat andere opgenomen gegevens van het Platform bevat.

### Als ik al gegevens in Platform heb ingevoerd, kan ik het dan beschikbaar stellen in de opslag van het Profiel?

Als de gegevens in een niet-Profiel dataset zijn opgenomen, moet u die gegevens in een profiel-Toegelaten dataset opnieuw opnemen om het in de opslag van het Profiel ter beschikking te stellen. Het is mogelijk om een bestaande dataset voor Profiel toe te laten, echter om het even welke gegevens die voorafgaand aan die configuratie werden opgenomen zullen nog niet in de opslag van het Profiel verschijnen.

Als u eerder opgenomen gegevens wilt toevoegen aan de profielopslag, volgt u de [Zelfstudie over configuratie van gegevensset](./tutorials/dataset-configuration.md) om een nieuwe dataset tot stand te brengen of een bestaande dataset om te zetten die voor Profiel moet worden toegelaten, en dan de gewenste gegevens in die dataset opnieuw op te nemen.

### Hoe kan ik mijn ingesloten profielgegevens bekijken?

Er zijn meerdere methoden om profielgegevens weer te geven, afhankelijk van het feit of u de API of UI gebruikt.

#### De API gebruiken

Als u de id&#39;s kent van de profielentiteiten waartoe u toegang wilt hebben, kunt u de opdracht `/entities` (Toegang tot profiel) in de profiel-API om die entiteiten op te zoeken. Zie de sectie over [entiteiten](./api/entities.md) in de ontwikkelaarsgids voor meer informatie.

U kunt de Adobe Experience Platform Segmentation Service API ook gebruiken om toegang te krijgen tot de individuele profielen van klanten die voor een publiekslidmaatschap in aanmerking zijn gekomen. Zie de [Overzicht van segmentatieservice](../segmentation/home.md) voor meer informatie .

#### UI gebruiken

In de interface van het Experience Platform **[!UICONTROL Browse]** in de **[!UICONTROL Profiles]** in de werkruimte kunt u het totale aantal profielen weergeven en naar afzonderlijke profielen zoeken op basis van hun identiteitswaarde. Zie de [Gebruikershandleiding voor profielen](./ui/user-guide.md) voor meer informatie .

U kunt ook een lijst met uw doelgroepen weergeven onder de **[!UICONTROL Browse]** in de **[!UICONTROL Audiences]** werkruimte. Nadat u een publiek hebt geselecteerd, wordt een voorbeeld weergegeven van profielen die voor dat publiek zijn gekwalificeerd. Vervolgens kunt u een van deze profielen selecteren om de details weer te geven. Zie de [Overzicht van de segmenteringsinterface](../segmentation/ui/overview.md) voor meer informatie .

## Foutcodes

Hieronder volgt een lijst met foutberichten die u kunt tegenkomen wanneer u werkt met de Real-Time Customer Profile API. Als de fout die u tegenkomt hier niet wordt vermeld, kunt u deze in het algemeen vinden [Handleiding voor probleemoplossing voor platforms](../landing/troubleshooting.md) in plaats daarvan.

### Kan het opzoekschema van het berekende kenmerk voor het opgegeven pad niet opzoeken

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Wanneer het creëren van een nieuw gegevens verwerkt attribuut, komt deze fout voor wanneer het systeem niet het schema kon vinden dat in de verzoeklading wordt verstrekt. Zorg ervoor dat u de juiste huurder-id in de lading hebt opgegeven `path` en dat de waarden van `schema.name` is een geldige schemanaam.

Als u uw huurder-id niet kent, kunt u deze ophalen door de stappen in het dialoogvenster [Handleiding voor ontwikkelaars van het schema Register](../xdm/api/getting-started.md).

### Functie met dezelfde naam bestaat al voor het opgegeven schema of definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Bij het maken van een nieuw berekende kenmerk treedt deze fout op wanneer de opgegeven `name` eigenschap wordt al gebruikt voor het schema dat onder `schema.name`. Vervang de waarde door een unieke naam voordat u het opnieuw probeert.

### Retourschema van de expressie is niet hetzelfde als het schema van het berekende kenmerk in het XDM-schema

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Bij het maken van een nieuw berekende kenmerk treedt deze fout op wanneer de opgegeven `name` eigenschap wordt al gebruikt voor het schema dat onder `schema.name`. Vervang de waarde door een unieke naam voordat u het opnieuw probeert.

### Ongeldig verwijderingsverzoek (profielsysteemtaak)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Deze fout treedt op wanneer een ongeldige lading voor een verwijdersysteembaan wordt verstrekt. Zorg ervoor dat u een geldige dataset of batch-id opgeeft onder de payload `dataSetID` of `batchID` eigenschap. Zie de sectie over [een verwijderaanvraag maken](./api/profile-system-jobs.md#create-a-delete-request) in de gids voor ontwikkelaars van het Profiel voor meer informatie.

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

Deze fout treedt op wanneer een POST- of PUT-aanvraag wordt verzonden met een ongeldige Content-Type-header. Controleer tweemaal dat u een geldige Content-Type waarde voor het eindpunt verstrekt u gebruikt.

De meeste eindpunten van het Profiel keuren &quot;application/json&quot;voor hun Content-Type kopbal, met de volgende uitzonderingen goed:

| Endpoint | Inhoudstype |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
