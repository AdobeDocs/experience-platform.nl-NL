---
keywords: aangepaste personalisatie; bestemming; ervaringsplatformbestemming;
title: Aangepaste aanpassingsverbinding
description: Deze bestemming verstrekt externe verpersoonlijking, inhoudsbeheersystemen, en servers, en andere toepassingen die op uw plaats een manier lopen om segmentinformatie van Adobe Experience Platform terug te winnen. Deze bestemming verstrekt verpersoonlijking in real time die op het segmentlidmaatschap van het gebruikersprofiel wordt gebaseerd.
hide: true
hidefromtoc: true
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 7ac7f533bb8547865b53892d371059aa60d2232e
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# Aangepaste aanpassingsverbinding {#custom-personalization-connection}

## Overzicht {#overview}

Deze bestemming verstrekt een manier om segmentinformatie van Adobe Experience Platform aan externe verpersoonlijkingsplatforms, inhoudsbeheersystemen, en servers, en andere toepassingen terug te winnen die op klantenwebsites lopen.

## Vereisten {#prerequisites}

Deze integratie wordt aangedreven door de [Adobe Experience Platform Web SDK](../../../edge/home.md) of de [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). U moet één van deze SDKs gebruiken om deze bestemming te gebruiken.

>[!IMPORTANT]
>
>Lees voordat u een aangepaste verpersoonlijkingsverbinding maakt de handleiding over het [vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking](../../ui/configure-personalization-destinations.md). Deze gids neemt u door de vereiste configuratiestappen voor zelfde-pagina en volgende-paginagrootte het gebruiksgevallen van het verpersoonlijkingsgebruik, over veelvoudige Experience Platforms.

## Type en frequentie exporteren {#export-type-frequency}

**Profielaanvraag** - u vraagt om alle segmenten die voor één profiel in kaart worden gebracht in de bestemming van de douaneverpersoonlijking. Verschillende aangepaste verpersoonlijkingsdoelen kunnen worden ingesteld voor verschillende [Gegevensstromen voor gegevensverzameling Adobe](../../../edge/datastreams/overview.md).

## Gebruiksscenario’s {#use-cases}

De [!DNL Custom personalization connection] laat u toe om uw eigen platforms van de verpersoonlijkingspartner te gebruiken (bijvoorbeeld [!DNL Optimizely], [!DNL Pega]), en ook leveraging Experience Platform Edge Network data collection &amp; segmentation capabilities, om een diepere klanterigvaring mogelijk te maken.

De hieronder beschreven gebruiksgevallen omvatten zowel personalisatie van de site als gerichte on-site reclame.

Om deze gebruiksgevallen toe te laten, hebben de klanten een snelle, gestroomlijnde manier nodig om segmentinformatie van Experience Platform terug te winnen en deze informatie naar hun aangewezen systemen te verzenden die zij als verbindingen van de douaneverpersoonlijking in het Experience Platform UI vormden.

Deze systemen kunnen externe verpersoonlijkingsplatforms, inhoudsbeheersystemen, en servers, en andere toepassingen zijn die over het Web en de mobiele eigenschappen van klanten lopen.

### Zelfde paginagrootte {#same-page}

Een gebruiker bezoekt een pagina van uw website. De klant kan de huidige informatie van het paginabezoek (bijvoorbeeld, verwijzend URL, browser taal, ingebedde productinfo) gebruiken om de volgende actie/besluit (bijvoorbeeld, verpersoonlijking) te selecteren, gebruikend de verbinding van de douaneverpersoonlijking voor niet-Adobe platforms (bijvoorbeeld, [!DNL Pega], [!DNL Optimizely], enz.).

### Aanpassing van volgende pagina {#next-page}

Een gebruiker bezoekt pagina A op uw website. Gebaseerd op deze interactie, heeft de gebruiker voor een reeks segmenten gekwalificeerd. De gebruiker klikt vervolgens op een koppeling die deze van pagina A naar pagina B verplaatst. De segmenten waarvoor de gebruiker tijdens de vorige interactie op pagina A in aanmerking kwam, samen met de profielupdates die door het huidige websitebezoek worden bepaald, zullen worden gebruikt om de volgende actie/beslissing (bijvoorbeeld welke advertentiebanner aan de bezoeker te tonen, of, in het geval van A/B het testen, welke versie van de pagina aan vertoning) te aandrijven.

### Aanpassing van volgende sessie {#next-session}

Een gebruiker bezoekt verschillende pagina&#39;s op uw website. Gebaseerd op deze interactie, heeft de gebruiker voor een reeks segmenten gekwalificeerd. De gebruiker beëindigt dan de huidige het doorbladeren zitting.

De volgende dag keert de gebruiker terug naar dezelfde klantenwebsite. De segmenten waarvoor zij tijdens de vorige interactie met alle bezochte websitepagina&#39;s in aanmerking kwamen, samen met de profielupdates die door het huidige websitebezoek werden bepaald, zullen worden gebruikt om de volgende actie/beslissing te selecteren (bijvoorbeeld welke advertentiebanner aan de bezoeker moet worden getoond, of, in het geval van A/B-tests, welke versie van de pagina aan vertoning).

## Verbinden met de bestemming {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informatie over gegevensstroom-id&#39;s"
>abstract="Met deze optie bepaalt u in welke gegevensverzamelingsgegevensstroom de segmenten worden opgenomen in het antwoord op de pagina. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. U moet een gegevensstroom vormen alvorens u uw bestemming kunt vormen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Leer hoe u een gegevensstroom configureert"

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **[!UICONTROL Integration alias]**: Deze waarde wordt verzonden naar het Web SDK van het Experience Platform als JSON objecten naam.
* **[!UICONTROL Datastream ID]**: Dit bepaalt in welke gegevensstroom van de Inzameling van Gegevens de segmenten in de reactie op de pagina zullen worden omvat. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. Zie [Een gegevensstroom configureren](../../../edge/datastreams/overview.md) voor meer informatie .

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

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
