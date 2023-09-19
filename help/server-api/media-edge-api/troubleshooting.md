---
solution: Experience Platform
title: Aan de slag met Media Edge-API's
description: Handleiding voor probleemoplossing voor mediarand-API's
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---


# Handleiding voor probleemoplossing voor Media Edge API

Deze gids verstrekt het oplossen van problemen instructies voor de behandeling van fouten en voor het verkrijgen van succesvolle reacties.

## Hulpmiddelen voor foutreacties gebruiken

Om het oplossen van problemen te helpen onsuccesvolle reacties problemen oplossen, gaan de fouten vergezeld van een antwoordlichaam dat een foutenvoorwerp bevat. In dit geval bevat de responsinstantie probleemdetails, zoals gedefinieerd door [RFC 7807 — Probleemdetails voor HTTP API&#39;s](https://datatracker.ietf.org/doc/html/rfc7807). Om de gebruikerservaring van de API te verbeteren, zijn de probleemdetails beschrijvend (de details van de seriesleutels worden getoond gebruikend JsonPath aan het ontbrekende of ongeldige gebied). Ze zijn ook cumulatief (alle ongeldige velden worden in dezelfde aanvraag gerapporteerd).


## Het valideren van de sessie wordt gestart

De meeste problemen met de verzoeken van het Begin van de Zitting resulteren in een 207 multi-statusreactie.
De lading lijkt op [Server-API](../error-handling.md)Niet-fatale fouten. Alle fouten in Media Analytics hebben het volgende type:  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. De getallen in het antwoord komen overeen met de foutstatus.

Het volgende voorbeeld toont een antwoordlichaam voor een verzoek van het Begin van de Zitting dat allebei een verplicht gebied mist en ongeldige heeft.

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

In het bovenstaande voorbeeld worden beide problemen opgemerkt door `name` en `reason` krachtens `details`: de eerste reden wordt weergegeven `missing required field` en in de tweede plaats wordt beschreven dat niet aan de ISO 8601-norm is voldaan.


>[!NOTE]
>
> Voor fouten die stroomopwaarts van Media Analytics worden veroorzaakt, adviseert de Adobe dat u de geproduceerde media zitting blijft verwerken.

## Gebeurtenissen valideren

De meeste ongeldige gebeurtenisverzoeken resulteren in een slechte reactie van 400 aanvragen. In deze gevallen is de payload vergelijkbaar met fatale fouten in de server-API.

Voor gebeurtenisaanvragen bevat de Media Edge API-service aanvullende controles die niet in het XDM-model zelf zijn vastgelegd. Dit omvat een controle dat de weg `eventType` komt overeen met de payload van de aanvraag `eventType`.


In het volgende voorbeeld wordt een `eventType` niet overeenkomen met een `adBreakStart` lading verzonden naar `ee/va/v1/chapterStart`:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

In het volgende voorbeeld ziet u een extra Media Edge API-controle om een `chapterStart` oproep ontbreekt `chapterDetails` info:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## Fouten op 400 en 500 niveaus verwerken

In de volgende tabel vindt u instructies voor de verwerking van statusresponsfouten:


| Foutcode | Beschrijving |
| ---------- | --------- |
| 4xx onjuist verzoek | De meeste 4xx-fouten (bijvoorbeeld `400`, `403`, `404`) mag niet opnieuw worden geprobeerd door de gebruiker. Het opnieuw proberen van het verzoek zal niet in een succesvolle reactie resulteren. De gebruiker moet de fout verhelpen voordat hij of zij de aanvraag opnieuw probeert. Gebeurtenissen die resulteren in 4xx-statuscodes worden niet bijgehouden, wat de nauwkeurigheid van gegevens kan beïnvloeden in sessies die 4xx-reacties hebben ontvangen. |
| 410 Gone | Geeft aan dat de sessie die bedoeld is voor &#39;tracking&#39; niet meer wordt berekend op de server. De meest voorkomende reden hiervoor is dat de zitting langer is dan 24 uur. Na ontvangst van een `410`, probeer een nieuwe sessie te starten en volg deze. |
| 429 Te veel verzoeken | Deze antwoordcode wijst erop dat de server tarief beperkt de verzoeken is. Volg de **Opnieuw proberen na** de instructies in de reactiekop zorgvuldig. Alle reacties die teruglopen, moeten de HTTP-antwoordcode bevatten met een domeinspecifieke foutcode. |
| 500 Interne serverfout | `500` Fouten zijn algemene, &#39;catch-all&#39;-fouten. `500` fouten moeten niet opnieuw worden geprobeerd, behalve voor `502`, `503` en `504`. |
| 502 Onjuiste gateway | Deze foutcode geeft aan dat de server, terwijl deze als gateway fungeert, een ongeldige reactie van upstream-servers heeft ontvangen. Dit kan gebeuren door netwerkproblemen tussen servers. Het tijdelijke netwerkprobleem kan zichzelf oplossen, dus het opnieuw proberen van het verzoek kan het probleem oplossen. |
| 503 Service niet beschikbaar | Deze foutcode geeft aan dat de service tijdelijk niet beschikbaar is. Dit kan gebeuren tijdens onderhoudsperioden. Ontvangers van `503` De fouten kunnen het verzoek opnieuw proberen, maar zouden ook moeten volgen **Opnieuw proberen na** koptekstinstructies. |


## Gebeurtenissen in de wachtrij wanneer de reacties op de sessie traag zijn

Nadat een mediatrackingsessie is gestart, kan de mediaspeler branden voordat het antwoord op de sessie (met de parameter Session ID) vanaf de achtergrond wordt geretourneerd. Als dit gebeurt, moet uw toepassing alle volgende gebeurtenissen in de wachtrij plaatsen die aankomen tussen de aanvraag voor het starten van de sessie en het antwoord daarop. Wanneer de reactie van Sessies aankomt, moet u eerst alle gebeurtenissen in de wachtrij verwerken, waarna u kunt beginnen met het verwerken van live gebeurtenissen.

Voor beste resultaten, controleer de Speler van de Verwijzing in uw distributie instructies op hoe te om gebeurtenissen te verwerken alvorens een identiteitskaart van de Zitting te ontvangen.

In het volgende voorbeeld wordt een methode getoond voor het verwerken van gebeurtenissen voordat een sessie-id wordt ontvangen:


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```


