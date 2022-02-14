---
keywords: aangepaste personalisatie; bestemming; ervaringsplatformbestemming;
title: Aangepaste aanpassingsverbinding
description: Deze bestemming verstrekt externe verpersoonlijking, inhoudsbeheersystemen, en servers, en andere toepassingen die op uw plaats een manier lopen om segmentinformatie van Adobe Experience Platform terug te winnen. Deze bestemming verstrekt verpersoonlijking in real time die op het segmentlidmaatschap van het gebruikersprofiel wordt gebaseerd.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: acbee5c4f67dd576b5513c061a67ed4b5af2d254
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# Aangepaste aanpassingsverbinding {#custom-personalization-connection}

## Overzicht {#overview}

Deze bestemming verstrekt een manier om segmentinformatie van Adobe Experience Platform aan externe verpersoonlijkingsplatforms, inhoudsbeheersystemen, en servers, en andere toepassingen terug te winnen die op klantenwebsites lopen.

## Vereisten {#prerequisites}

Deze integratie wordt aangedreven door de [Adobe Experience Platform Web SDK](../../../edge/home.md) of de [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). U moet één van deze SDKs gebruiken om deze bestemming te gebruiken.

## Exporttype {#export-type}

**Profielaanvraag** - u vraagt om alle segmenten die voor één profiel in kaart worden gebracht in de bestemming van de douaneverpersoonlijking. Verschillende aangepaste verpersoonlijkingsdoelen kunnen worden ingesteld voor verschillende [Gegevensstromen voor gegevensverzameling Adobe](../../../edge/fundamentals/datastreams.md).

## Gebruiksscenario’s {#use-cases}

Deze bestemming deelt publiek met advertentieservers en niet-Adobe verpersoonlijkingstoepassingen, die in real time moeten worden gebruikt, om te beslissen welke reclame gebruikers op een website zouden moeten zien.

### Hoofdletters en kleine letters gebruiken 1

**Homepage aanpassen**

Een homepage- en verkoopwebsite wil hun homepage aanpassen op basis van segmentkwalificaties in Adobe Experience Platform. Het bedrijf kan selecteren welk publiek een gepersonaliseerde ervaring zou moeten krijgen en die in kaart brengen aan de bestemming van de douaneverpersoonlijking die voor hun niet-Adobe verpersoonlijkingstoepassing zoals het richten criteria was opgesteld.

**Gerichte on-site reclame**

Dezelfde website kan on-site advertenties aanwijzen met een andere set segmenten van Adobe Experience Platform als doelcriteria, waarbij een afzonderlijke aangepaste personalisatiebestemming voor de advertentieserver wordt gebruikt.

## Verbinden met de bestemming {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informatie over gegevensstroom-id&#39;s"
>abstract="Met deze optie bepaalt u in welke gegevensverzamelingsgegevensstroom de segmenten worden opgenomen in het antwoord op de pagina. In het vervolgkeuzemenu worden alleen gegevensstromen weergegeven waarvoor de doelconfiguratie is ingeschakeld. U moet een gegevensstroom vormen alvorens u uw bestemming kunt vormen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Leer hoe u een gegevensstroom configureert."

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **[!UICONTROL Integration alias]**: Deze waarde wordt verzonden naar het Web SDK van het Experience Platform als JSON objecten naam.
* **[!UICONTROL Datastream ID]**: Dit bepaalt in welke gegevensstroom van de Inzameling van Gegevens de segmenten in de reactie op de pagina zullen worden omvat. In het vervolgkeuzemenu worden alleen gegevensstromen weergegeven waarvoor de doelconfiguratie is ingeschakeld. Zie [Een gegevensstroom configureren](../../../edge/fundamentals/datastreams.md) voor meer informatie .

## Segmenten naar dit doel activeren {#activate}

Lezen [Profielen en segmenten activeren om aanvraagdoelen te profileren](../../ui/activate-profile-request-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Als u [Tags in Adobe Experience Platform](../../../tags/home.md) om SDK van het Web van het Experience Platform op te stellen, gebruik [De gebeurtenis send voltooid](../../../edge/extension/event-types.md) functionaliteit en uw aangepaste code-actie heeft een `event.destinations` variabele die u kunt gebruiken om de geëxporteerde gegevens weer te geven.

Hier volgt een voorbeeldwaarde voor de `event.destinations` variabele:

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

Als u dit niet gebruikt [Tags](../../../tags/home.md) om SDK van het Web van het Experience Platform op te stellen, gebruik [reacties van gebeurtenissen afhandelen](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) om de geëxporteerde gegevens weer te geven.

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
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
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

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](../../../data-governance/home.md).
