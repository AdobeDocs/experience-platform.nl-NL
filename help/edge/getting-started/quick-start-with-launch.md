---
title: Snel starten met starten
seo-title: Adobe Experience Platform Web SDK snel aan de slag met Starten
description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Platform van de Ervaring om gegevens te verzamelen
seo-description: Snelle startgids voor het gebruiken van de uitbreiding van SDK van het Platform van de Ervaring om gegevens te verzamelen
translation-type: tm+mt
source-git-commit: 51acb07efe624c7cf1dfaabc4b03f04c76ac88f8
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# (bèta) Vereisten

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De Adobe Experience Platform Web SDK ondersteunt momenteel alleen het verzenden van gegevens naar het Adobe Experience Platform met behulp van XDM. U moet aan de volgende voorwaarden voldoen.

- Heb een [1st-partijdomein (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) toegelaten. Als u al een CNAME voor Analytics hebt, zou u dat moeten gebruiken.
- Adobe Experience Platform
- Gebruik de nieuwste versie van de service Bezoeker-id

## Platform voorbereiden

Om gegevens naar het Platform van de Ervaring van Adobe te kunnen verzenden, moet u een schema XDM en een dataset tot stand brengen die dat schema gebruikt.

- [Een schema maken](../../xdm/tutorials/create-schema-ui.md)
- Voeg de Adobe Experience Platform Web SDK-mix toe aan het schema dat u hebt gemaakt
- [Creeer een dataset](https://platform.adobe.com/dataset/overview) met uw schema waar u de gegevens zou willen landen

## Een configuratie-id maken

U kunt een configuratie-id maken met het gereedschap [](../fundamentals/edge-configuration.md) Edge-configuratie tijdens het opstarten.

>Opmerking: Uw organisatie moet voor de eigenschap worden gewhitelisteerd. Neem contact op met uw CSM om op de lijst te komen voor eventuele whitelisting.

## SDK installeren in Launch

Meld u aan bij Starten en installeren van de `AEP Web SDK` extensie. Als onderdeel van de installatie van de SDK wordt u gevraagd om de extensie te configureren. Voer de configuratie-id in die u hierboven hebt aangevraagd. De extensie vult automatisch uw organisatie-id in.

Voor meer details over verschillende configuratieopties, zie het [Vormen SDK](../fundamentals/configuring-the-sdk.md).

## Een gebeurtenis verzenden

Nadat de extensie is geïnstalleerd, begint u met het verzenden van gebeurtenissen door de actie &quot;Send Beacon&quot; van de AEP Web SDK-extensie toe te voegen. U wordt aangeraden ten minste één gebeurtenis te verzenden telkens wanneer een pagina wordt geladen met de optie &quot;Komt voor aan het begin van een weergave&quot; ingeschakeld.

Zie Gebeurtenissen [bijhouden voor meer informatie over het bijhouden van gebeurtenissen](../fundamentals/tracking-events.md).

## Gegevens verzenden

U kunt gegevens verzenden die overeenkomen met het schema dat u eerder samen met uw gebeurtenissen hebt gemaakt. Bijvoorbeeld, als u een handelsplaats hebt en de handelsmengeling aan uw schema toevoegde, zou u de volgende structuur verzenden wanneer iemand een product bekijkt.

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
