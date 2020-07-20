---
title: Snel aan de slag met plain javascript
seo-title: 'Snelle start voor Web SDK van Adobe Experience Platform '
description: Snelle startgids voor het gebruiken van het Web SDK van het Experience Platform om gegevens te verzamelen
seo-description: Snelle startgids voor het gebruiken van het Web SDK van het Experience Platform om gegevens te verzamelen
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---


# Welkom

Deze handleiding leidt u door de verschillende manieren om het Adobe Experience Platform in te stellen [!DNL Web SDK]. Als u deze functie wilt kunnen gebruiken, moet u op de lijst van gewenste personen staan. Neem contact op met uw CSM als u op de wachtlijst wilt staan.

- Heb een [1st-partijdomein (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) toegelaten. Als u al een CNAME voor hebt, [!DNL Analytics]zou u dat moeten gebruiken. Het testen in ontwikkeling werkt zonder CNAME maar u hebt er een nodig voordat u naar productie gaat
- Het recht hebben op Adobe Experience Platform [!DNL Data Platform].  Als u geen Platform hebt aangeschaft, ontvangen wij u gratis [!DNL Experience Platform Data Services Foundation] een beperkte gebruiksmogelijkheid met de SDK.
- Gebruik de nieuwste versie van de service Bezoeker-id

## Een configuratie-id maken

U kunt een configuratie-id maken met het gereedschap [](../fundamentals/edge-configuration.md) Edge-configuratie in Adobe Launch, zelfs als u de functies voor tagbeheer niet gebruikt. Dit staat u toe om toe te laten [!DNL Edge Network] om gegevens naar de diverse oplossingen te verzenden. Nadere informatie over het vinden van elke optie vindt u in de pagina [Edge Configuration Tool](../fundamentals/edge-configuration.md) .

>[!NOTE]
>
>Uw organisatie moet op de lijst van gewenste personen voor de eigenschap zijn. Neem contact op met uw CSM om de lijst van gewenste personen te openen.

## Een schema voorbereiden

De [!DNL Experience Platform Edge Network] gegevens worden als XDM gebruikt. XDM is een gegevensformaat dat u schema&#39;s laat bepalen. Het schema bepaalt hoe de gegevens [!DNL Edge Network] verwacht worden geformatteerd. Om gegevens te verzenden, moet u uw schema bepalen.

- [Een schema maken](../../xdm/tutorials/create-schema-ui.md)
- Voeg de Adobe Experience Platform- [!DNL Web SDK] mix toe aan het schema dat u hebt gemaakt

De volgende video is bedoeld om u in het creëren van een schema, dataset, en het stromen bronschakelaar voor uw [!DNL Web SDK] gegevens te steunen.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
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
