---
title: Foutafhandeling
description: Meer informatie over de mogelijke fouten die kunnen optreden bij het uitvoeren van API-aanvragen bij de Adobe Experience Platform Edge Network Server-API.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 1%

---

# Foutafhandeling

## Overzicht {#overview}

API-fouten in de Adobe Experience Platform Edge Network Server-API kunnen verschillende oorzaken hebben: intern (Edge Network zelf) of extern (invoer, configuratie of upstream gerelateerd).

## Fouttypen {#error-types}

| Fout | Type | Beschrijving | Statuscode |
| --- | --- | --- | --- |
| `RequestProcessingError` | Intern | Algemene doelfout die door de Adobe Experience Platform Edge Network is uitgegeven in onverwachte omstandigheden. | `500` |
| `InputError` | Extern | Omvat fouten die door misvormde input worden veroorzaakt, evenals de fouten van de entiteitbevestiging. | `4xx` |
| `ConfigurationError` | Extern | Configuratiefouten op de server. | `422` |
| `UpstreamError` | Extern | Communicatiefouten met upstream services. | `207 Multi-Status` |

## Ernst

Server-API-fouten kunnen ook worden gesplitst op ernst:

* **de Fatale fouten** zullen de verzendingspijplijn tegenhouden.
* **de niet-fatale fouten** konden een gedeeltelijke verwerking, terwijl het toestaan voor verzoekverwerking om verder te gaan signaleren.
   * Indien aanwezig wordt de algemene statuscode van het verzoek gewijzigd in `207 Multi-Status` .

| Fout | Type | Opmerkingen |
| --- | --- | --- |
| `RequestProcessingError` | Dodelijk | Dit kan op elk gewenst moment tijdens de verwerking van een verzoek gebeuren. |
| `InputError` | Dodelijk | Vindt plaats wanneer u de aanvraag accepteert, voordat u deze upstream verzendt. |
| `ConfigurationError` | Dodelijk | Vindt plaats wanneer u de aanvraag accepteert, voordat u deze upstream verzendt. |
| `UpstreamError` | Niet-fataal | Communicatiefouten met upstream services. |

### Fatale fouten {#fatal-errors}

Fatale fouten stoppen de verzoekverwerking en veroorzaken dat een non-2xx reactiestatus wordt teruggekeerd. Controle uit de [ foutentypes ](#error-types) sectie om de verwachte statuscode te zien, die aan elk foutentype beantwoordt.

Fouten gaan vergezeld van een antwoordinstantie die een foutobject bevat. In dit geval, bevat het reactielichaam een probleemdetail, zoals bepaald door [ RFC 7807 Details van het Probleem voor HTTP APIs ](https://tools.ietf.org/html/rfc7807).

Het geretourneerde inhoudstype is het mediatype `application/problem+json` . Indien aanwezig bevat dit antwoord machineleesbare details met betrekking tot de fout. De details van het probleem omvatten een type van URI.

Alle foutobjecten hebben een berichteigenschap `type` , `status` , `title` , `detail` en `report` , zodat de API-client kan zien wat het probleem is.

| Eigenschap | Type | Beschrijving |
| -------- | ------ | ----------- |
| `type` | String | Een URI-referentie (RFC3986) die het probleemtype aangeeft, in de notatie `https://ns.adobe.com/aep/errors/<ERROR-CODE>` . |
| `status` | Getal | De HTTP-statuscode die door de server voor deze instantie van het probleem wordt gegenereerd. |
| `title` | String | Een korte, leesbare samenvatting van het type probleem. |
| `detail` | String | Een korte, leesbare beschrijving van het type probleem. |
| `report` | Object | Een kaart van extra eigenschappen die in het zuiveren zoals verzoekidentiteitskaart of org identiteitskaart helpen In sommige gevallen bevat het mogelijk gegevens die specifiek zijn voor de betreffende fout, zoals een lijst met validatiefouten. |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### Niet-fatale fouten {#non-fatal-errors}

Niet-fatale fouten kunnen verder worden onderverdeeld in:

* Fouten: problemen die zich tijdens de behandeling van het verzoek hebben voorgedaan, maar niet tot afwijzing van het volledige verzoek hebben geleid (bijvoorbeeld een niet-kritieke stroomopwaartse fout).
* Waarschuwingen: berichten van upstream-services die zouden kunnen aangeven dat een gedeeltelijke verwerking van het verzoek heeft plaatsgevonden.

Bij niet-fatale fouten (behalve waarschuwingen) wijzigt [!DNL Server API] de status van de reactie in `207 Multi-Status` .

Waarschuwingen daarentegen zijn meestal informatief, aangezien ze over het algemeen een potentieel voorbijgaande voorwaarde vormen, die het verzoek niet volledig heeft beïnvloed. Een voorbeeld hiervan is een gedeeltelijk profiel dat in de segmenteringsengine wordt gelezen. In dat geval wordt de nauwkeurigheid enigszins beïnvloed, maar de functionaliteit wordt nog steeds geleverd.

De niet fatale fouten worden vertegenwoordigd in het _formaat van de Details van het Probleem_, maar zijn direct ingebed in de standaardreactie van de gateway van Edge, die van type `application/json` is.

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## `4xx` - en `5xx` reacties verwerken

| Foutcode | Beschrijving |
|---|---|
| `4xx Bad Request` | De meeste `4xx` fouten, zoals 400, 403 en 404, mogen niet opnieuw worden geprobeerd namens de client, behalve voor `429` . Dit zijn clientfouten die niet worden opgelost. De client moet de fout verhelpen voordat u de aanvraag opnieuw probeert. |
| `429 Too Many Requests` | `429` HTTP-antwoordcode geeft aan dat de Adobe Experience Platform-Edge Network of een upstream-service een snelheidsbeperking voor de aanvragen is. In dat geval moet de aanroeper in een dergelijk scenario de antwoordheader `Retry-After` respecteren. Alle reacties die teruglopen, moeten de HTTP-antwoordcode bevatten met een domeinspecifieke foutcode. |
| `500 Internal Server Error` | `500` -fouten zijn algemene, &#39;catch-all&#39;-fouten. `500` fouten mogen niet opnieuw worden geprobeerd, behalve voor `502` en `503` . De intermediairs moeten met een `500` fout antwoorden en kunnen met een generische foutencode/een bericht, of een meer domein-specifieke foutencode/bericht antwoorden. |
| `502 Bad Gateway` | Geeft aan dat de Adobe Experience Platform-Edge Network een ongeldige reactie van upstream-servers heeft ontvangen. Dit kan gebeuren door netwerkproblemen tussen servers. Het probleem met het tijdelijke netwerk kan worden verholpen en het probleem kan dus opnieuw worden opgelost. Ontvangers van `502` -fouten kunnen het verzoek na verloop van tijd opnieuw proberen. |
| `503 Service Unavailable` | Deze foutcode geeft aan dat de service tijdelijk niet beschikbaar is. Dit kan gebeuren tijdens onderhoudsperioden. Ontvangers van `503` fouten kunnen de aanvraag opnieuw proberen, maar moeten de header van `Retry-After` respecteren. |
| `504 Gateway Timeout` | Geeft aan dat er een time-out is opgetreden voor Adobe Experience Platform Edge Network request to the upstream servers. Dit kan als gevolg van netwerkproblemen tussen servers, DNS-problemen of andere netwerkproblemen gebeuren. De tijdelijke netwerkkwesties kunnen na wat tijd worden opgelost en een herpoging kan de kwestie oplossen. |
