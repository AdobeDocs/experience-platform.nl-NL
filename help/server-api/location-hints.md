---
title: Tips voor locatie
description: Dit artikel verklaart hoe plaatswenken in de Server API van de Edge Network werken, zodat de eindgebruikerverzoeken altijd aan de zelfde server kunnen worden verpletterd.
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 2c7a5f007189d897ed32302a2a80c1e16af6af80
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Tips voor locatie

## Overzicht {#overview}

In [!DNL Adobe Experience Platform Edge Network] worden verschillende globaal gedistribueerde servers gebruikt voor snelle responstijden, ongeacht de locatie van de eindgebruiker. Het gebruikt ook op DNS-Gebaseerd verpletteren om ervoor te zorgen dat de verzoeken altijd aan de plaats van de Edge Network worden verpletterd die aan het eind - gebruikers het dichtst is.

Als eind - de gebruikers met VPN verbinden, of netwerktypes op hun mobiele apparaten tijdens een zitting schakelen, kunnen de verzoeken van de Edge Network vaak aan een verschillende plaats worden verpletterd. Het kan problematisch zijn om de routering halverwege de sessie tussen servers uit te voeren, aangezien Adobe Experience Platform- en Adobe Experience Cloud-oplossingen informatie over het gebruikersprofiel op de Edge Network opslaan.

Hier worden locatietips weergegeven.

Om ervoor te zorgen dat eindgebruikers altijd met de Edge Network regionale server in wisselwerking staan die hun huidige profielgegevens bevat, zorgt de functionaliteit van plaatswenken ervoor dat alle verzoeken aan de Edge Network worden verzonden naar de zelfde server waar het eerste verzoek van een zitting werd gemaakt. Dit helpt gebruikers een verenigbare ervaring hebben, ongeacht welke netwerkveranderingen zij tijdens een zitting kunnen ervaren.

## Gebruik van locatiepunten

De wenken van de plaats zijn inbegrepen in het antwoord van het aanvankelijke verzoek van de Edge Network, en in alle verdere verzoeken, zoals aangetoond in het hieronder voorbeeld:

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

Het bereik `EdgeNetwork` bevat alle relevante informatie die de Edge Network nodig heeft om volgende aanvragen dienovereenkomstig te verzenden. Als reactie op het eerste en volgende verzoek aan het Edge-netwerk, bevat de greep een sectie met een type `locationHint:result` .

De tip die aan het bereik `EdgeNetwork` is gekoppeld, kan een van de volgende waarden bevatten:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API formaat**

Om ervoor te zorgen dat volgende aanvragen correct worden gerouteerd, voegt u de locatiehint in het URL-pad in van volgende API-aanroepen tussen het basispad (doorgaans `ee` en de `v2` API-versie).

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Locatiepunten opslaan in cookies {#storing-hints-in-cookies}

Om ervoor te zorgen dat de door de Edge Network geretourneerde locatiehint gedurende de sessie blijft bestaan, kunt u de waarde van de locatiehint in een cookie opslaan, samen met de levensduur van het cookie, die zich in het veld `ttlSeconds` bevindt (doorgaans 1800 seconden).

Net als bij de meeste cookies dient u de levensduur van deze cookie te verlengen telkens wanneer de Edge Network reageert. Gebruik de cookienaam `kndctr_{IMSORG}_AdobeOrg_cluster` om maximale compatibiliteit met de SDK van het web te garanderen. Organisatie-id&#39;s eindigen doorgaans met `@AdobeOrg` . De waarde `@` moet worden omgezet in een onderstrepingsteken om ervoor te zorgen dat de cookie de juiste notatie heeft.
