---
title: Snel aan de slag met plain javascript
seo-title: 'Snelle start voor Adobe Experience Platform Web SDK '
description: Snelle startgids voor het gebruiken van het Web SDK van het Platform van de Ervaring om gegevens te verzamelen
seo-description: Snelle startgids voor het gebruiken van het Web SDK van het Platform van de Ervaring om gegevens te verzamelen
translation-type: tm+mt
source-git-commit: 2d58f7f95c6ad125e66856350aee2f29a0499061
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Welkom

Deze gids leidt u door de verschillende manieren om SDK van het Web van Adobe Experience Platform te plaatsen. Als u deze functie wilt kunnen gebruiken, moet u in de lijst Toestaan staan. Neem contact op met uw CSM als u op de wachtlijst wilt staan.

- Heb een [1st-partijdomein (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) toegelaten. Als u al een CNAME voor Analytics hebt, zou u dat moeten gebruiken. Het testen in ontwikkeling werkt zonder CNAME maar u hebt er een nodig voordat u naar productie gaat
- recht hebben op het Adobe Experience Platform-gegevensplatform.  Als u Platform niet hebt aangeschaft, zullen wij u van de Stichting van de Diensten van de Gegevens van het Platform van de Ervaring voor gebruik op een beperkte manier met SDK zonder extra kosten voorzien.
- Gebruik de nieuwste versie van de service Bezoeker-id

## Een configuratie-id maken

U kunt een configuratie-id maken met het gereedschap [](../fundamentals/edge-configuration.md) Edge-configuratie in Adobe Launch, zelfs als u de functies voor tagbeheer niet gebruikt. Dit staat u toe om het Netwerk van de Rand toe te laten om gegevens naar de diverse oplossingen te verzenden. Nadere informatie over het vinden van elke optie vindt u in de pagina [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>[!NOTE]
>
>Uw organisatie moet in de lijst met toegestane items staan voor de functie. Neem contact op met uw CSM om de lijst voor toestaan weer te geven.

## Een schema voorbereiden

Het Edge Network van het Platform van de Ervaring neemt gegevens als XDM. XDM is een gegevensformaat dat u schema&#39;s laat bepalen. Het schema bepaalt hoe het Netwerk van de Rand verwacht dat de gegevens worden geformatteerd. Om gegevens te verzenden, moet u uw schema bepalen.

- [Een schema maken](../../xdm/tutorials/create-schema-ui.md)
- Voeg de mix van de SDK van Adobe Experience Platform Web toe aan het schema dat u hebt gemaakt

## De SDK installeren

Als u de SDK wilt installeren, kopieert en plakt u de volgende &quot;basiscode&quot; zo hoog mogelijk in de `<head>` tag van de HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Zie [De SDK](../fundamentals/installing-the-sdk.md)installeren voor meer informatie over de verschillende opties om dit te doen.

## De SDK configureren

Geef vervolgens de SDK de configuratie op. Dit wordt gedaan gebruikend het `configure` bevel. Dit zou het eerste bevel moeten zijn dat op elke pagina wordt geroepen.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Hier geeft u de configuratie-id die u hierboven hebt gemaakt op en uw organisatie-id. Dit zijn de enige twee vereiste velden. Er zijn echter veel andere [configuratieopties](../fundamentals/configuring-the-sdk.md).

## Een gebeurtenis verzenden

Nadat u het vormen bevel hebt geroepen, kunt u beginnen gebeurtenissen te volgen.

```javascript
alloy("sendEvent", {});
```

Gewoonlijk verzendt u gebeurtenissen met bepaalde gegevens. U kunt XDM-gegevens op deze manier verzenden. De gegevens die u verzendt, moeten in het schema staan u in XDM creeerde.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

Zie Gebeurtenissen [bijhouden voor meer informatie over het bijhouden van gebeurtenissen](../fundamentals/tracking-events.md).

## Volgende stappen

Nadat u gegevens hebt laten stromen, kunt u het volgende doen:

- [Uw schema samenstellen](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Meer informatie over foutopsporing](../fundamentals/debugging.md)
- Leer hoe u de ervaring kunt [aanpassen](../fundamentals/rendering-personalization-content.md)
- Meer informatie over het verzenden van gegevens naar meerdere oplossingen
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
