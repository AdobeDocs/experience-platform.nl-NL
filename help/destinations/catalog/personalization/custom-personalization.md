---
keywords: aangepaste personalisatie; bestemming; ervaringsplatformbestemming;
title: Aangepaste aanpassingsverbinding (bèta)
description: Deze bestemming verstrekt externe verpersoonlijking, inhoudsbeheersystemen, en servers, en andere toepassingen die op uw plaats een manier lopen om segmentinformatie van Adobe Experience Platform terug te winnen. Deze bestemming verstrekt in real time 1:1 en verpersoonlijking die op het segmentlidmaatschap van een gebruikersprofiel wordt gebaseerd.
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Aangepaste aanpassingsverbinding (bèta) {#custom-personalization-connection}

## Overzicht {#overview}

>[!IMPORTANT]
>
>De aangepaste aanpassingsverbinding in Adobe Experience Platform bevindt zich momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

Deze bestemming verstrekt een manier om segmentinformatie van Adobe Experience Platform aan externe verpersoonlijkingsplatforms, inhoudsbeheersystemen, en servers, en andere toepassingen terug te winnen die op klantenwebsites lopen.

## Vereisten {#prerequisites}

Deze integratie wordt aangedreven door [Adobe Experience Platform Web SDK](../../../edge/home.md). U moet deze SDK gebruiken om deze bestemming te gebruiken.

## Exporttype {#export-type}

**Verzoek**  van het profiel - u vraagt om alle segmenten die in de bestemming van de douaneverpersoonlijking voor één enkel profiel in kaart worden gebracht. Verschillende aangepaste verpersoonlijkingsbestemmingen kunnen worden ingesteld voor verschillende [gegevensstromen van de Gegevensverzameling van Adobe.](../../../edge/fundamentals/datastreams.md)

## Gebruiksscenario’s {#use-cases}

Deze bestemming deelt publiek met advertentieservers en niet-Adobe verpersoonlijkingstoepassingen, die in real time moeten worden gebruikt, om te beslissen welke reclame gebruikers op een website zouden moeten zien.

### Hoofdletters en kleine letters gebruiken 1

**Homepage aanpassen**

Een homepage- en verkoopwebsite wil hun homepage aanpassen op basis van segmentkwalificaties in Adobe Experience Platform. Het bedrijf kan selecteren welk publiek een gepersonaliseerde ervaring zou moeten krijgen en die in kaart brengen aan de bestemming van de douaneverpersoonlijking die voor hun niet-Adobe verpersoonlijkingstoepassing zoals het richten criteria was opgesteld.

**Gerichte on-site reclame**

Dezelfde website kan on-site advertenties aanwijzen met een andere set segmenten van Adobe Experience Platform als doelcriteria, waarbij een afzonderlijke aangepaste personalisatiebestemming voor de advertentieserver wordt gebruikt.

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **[!UICONTROL Integration alias]**: Deze waarde wordt verzonden naar het Web SDK van het Experience Platform als JSON objecten naam.
* **[!UICONTROL Datastream ID]**: Dit bepaalt in welke gegevensstroom van de Inzameling van Gegevens de segmenten in de reactie op de pagina zullen worden omvat. In het vervolgkeuzemenu worden alleen gegevensstromen weergegeven waarvoor de doelconfiguratie is ingeschakeld. Zie [Een gegevensstroom configureren](../../../edge/fundamentals/datastreams.md) voor meer informatie.

## Segmenten naar dit doel activeren {#activate}

Lees [Activate profielen en segmenten aan profiel verzoekbestemmingen](../../ui/activate-profile-request-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Als u [Adobe Tags](../../../tags/home.md) gebruikt om de SDK van het Web van het Experience Platform op te stellen, gebruik [gebeurtenis complete](../../../edge/extension/event-types.md) functionaliteit en uw actie van de douanecode zal een `event.destinations` variabele hebben die u kunt gebruiken om de uitgevoerde gegevens te zien.

Als u [Adobe Tags](../../../tags/home.md) niet gebruikt om de SDK van het Web van het Experience Platform op te stellen, gebruik [behandelende reacties van gebeurtenissen](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) functionaliteit om de uitgevoerde gegevens te zien.

Het JSON-antwoord van Adobe Experience Platform kan worden geparseerd om de bijbehorende integratiealias te zoeken van de toepassing die u integreert met Adobe Experience Platform. De segment-id&#39;s kunnen als doelparameters worden doorgegeven aan de code van de toepassing. Hieronder ziet u een voorbeeld van hoe dit er specifiek uitziet voor de doelrespons.

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(results) {
    if(results.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = results.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = results.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Lees voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt het [Overzicht gegevensbeheer](../../../data-governance/home.md).
