---
title: Tips voor locatie
description: Dit artikel verklaart hoe plaatswenken in de Server API van het Netwerk van Edge werken, zodat de eindgebruikerverzoeken altijd aan de zelfde server kunnen worden verpletterd.
source-git-commit: 7f1d8fba34c5478f0d6e727a5a52af642852c9dd
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---


# Tips voor locatie

## Overzicht {#overview}

De [!DNL Adobe Experience Platform Edge Network] gebruikt verschillende globaal gedistribueerde servers om snelle responstijden te garanderen, ongeacht de locatie van de eindgebruiker. Het gebruikt ook op DNS-Gebaseerd verpletteren om ervoor te zorgen dat de verzoeken altijd aan de plaats van het Netwerk van de Rand worden verpletterd die aan het eind - gebruikers het dichtst is.

Als de eindgebruikers met VPN verbinden, of netwerktypes op hun mobiele apparaten tijdens een zitting schakelen, kunnen de verzoeken van het Netwerk van de Rand vaak aan een verschillende plaats worden verpletterd. Het kan problematisch zijn om de routering halverwege de sessie tussen servers uit te voeren, aangezien Adobe Experience Platform- en Adobe Experience Cloud-oplossingen informatie over het eindgebruikersprofiel opslaan op het Edge-netwerk.

Hier worden locatietips weergegeven.

Om ervoor te zorgen dat eindgebruikers altijd met de regionale server van het Netwerk van Edge in wisselwerking staan die hun huidige profielgegevens bevat, zorgt de functionaliteit van plaatswenken ervoor dat alle verzoeken aan het Netwerk van de Rand worden verzonden naar de zelfde server waar het eerste verzoek van een zitting werd gedaan. Dit helpt gebruikers een verenigbare ervaring hebben, ongeacht welke netwerkveranderingen zij tijdens een zitting kunnen ervaren.

## Gebruik van locatiepunten

De wenken van de plaats zijn inbegrepen in het antwoord van het aanvankelijke verzoek van het Netwerk van de Rand, en in alle verdere verzoeken, zoals aangetoond in het hieronder voorbeeld:

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

De `EdgeNetwork` Het bereik bevat alle relevante informatie die het Edge-netwerk nodig heeft om verdere verzoeken dienovereenkomstig te kunnen verzenden. In de reactie op het eerste en elk volgend verzoek aan het Edge-netwerk wordt een sectie in de greep weergegeven met een type van `locationHint:result`.

De aan de `EdgeNetwork` bereik kan een van de volgende waarden bevatten:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API-indeling**

Om ervoor te zorgen dat volgende aanvragen correct worden gerouteerd, voegt u de locatiehint in het URL-pad van volgende API-aanroepen tussen het basispad in, meestal `ee`, en `v2` API-versie.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Locatiepunten opslaan in cookies {#storing-hints-in-cookies}

Om ervoor te zorgen dat de plaatswenk door het Netwerk van de Rand voor de duur van de zitting is teruggekeerd, kunt u de waarde van de plaatswenk in een koekje, samen met het koekjesleven opslaan, dat in bevat is `ttlSeconds` veld (doorgaans 1800 seconden).

Net als bij de meeste cookies dient u de levensduur van deze cookie te verlengen telkens wanneer er een reactie van het Edge-netwerk wordt ontvangen. Gebruik de cookienaam om maximale compatibiliteit met de Web SDK te garanderen `kndctr_{IMSORG}_AdobeOrg_cluster`. IMS-organisatie-id&#39;s eindigen doorgaans met `@AdobeOrg`. De `@` Deze waarde moet worden omgezet in een onderstrepingsteken om ervoor te zorgen dat de cookie de juiste notatie heeft.
