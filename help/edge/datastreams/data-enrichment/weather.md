---
title: Weergavegegevens van DNL gebruiken
description: De weergegevens van het gebruik van DNL het Weather Kanaal om de gegevens te verbeteren u door gegevensstromen verzamelt.
source-git-commit: b53be9f2f2d55d5f9e8081fb0ca6732dcc2a8c11
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 1%

---


# Weer gegevens gebruiken uit [!DNL The Weather Channel]

Adobe heeft een partnerschap met [!DNL [The Weather Company]](https://www.ibm.com/weather) om de extra context van het weer in de Verenigde Staten te brengen aan de gegevens die via gegevensstromen worden verzameld. U kunt deze gegevens gebruiken voor analyses, het richten van en het segmentverwezenlijking in Experience Platform.

Er zijn 3 soorten gegevens beschikbaar van [!DNL The Weather Channel]:

* **[!UICONTROL Current Weather]**: De huidige weersomstandigheden van de gebruiker, op basis van hun locatie. Dit omvat de huidige temperatuur, neerslag, wolkendekking en meer.
* **[!UICONTROL Forecasted Weather]**: De prognose omvat de prognose van 1,2,3,5,7 en 10 dagen voor de locatie van de gebruiker.
* **[!UICONTROL Triggers]**: Triggers zijn specifieke combinaties die aan verschillende semantische weersomstandigheden in kaart brengen. Er zijn drie verschillende soorten weertriggers:

   * **[!UICONTROL Weather Triggers]**: Halfzinvolle omstandigheden, zoals koud of regenachtig weer. Deze kunnen in de definities verschillen tussen de verschillende klimatologische omstandigheden.
   * **[!UICONTROL Product Triggers]**: Voorwaarden die tot de aankoop van verschillende soorten producten zouden leiden. Bijvoorbeeld: de weerprognoses zouden kunnen betekenen dat de aankoop van regenjassen waarschijnlijker is .
   * **[!UICONTROL Severe Weather Triggers]**: Ernstige weerswaarschuwingen, zoals winterstorm of orkaanwaarschuwingen.

## Vereisten {#prerequisites}

Voordat u weergegevens gebruikt, moet u controleren of aan de volgende voorwaarden is voldaan:

* U moet een licentie geven voor de weergegevens die u gebruikt, van [!DNL The Weather Channel]. Ze zullen het dan inschakelen op je account.
* Weer-gegevens zijn alleen beschikbaar via gegevensstreams. Als u weergegevens wilt gebruiken, moet u [!DNL Web SDK], [!DNL Mobile Edge Extension] of de [Server-API](../../../server-api/overview.md) om deze gegevens te gebruiken.
* Uw gegevensstroom moet [[!UICONTROL Geo Location]](../configure.md#advanced-options) ingeschakeld.
* Voeg de [weerveldgroep](#schema-configuration) aan het schema u gebruikt.

## Inrichting {#provisioning}

Nadat u de gegevens van [!DNL The Weather Channel], zullen uw account toegang krijgen tot de gegevens. Vervolgens moet u contact opnemen met de klantenservice van Adobe om de gegevens op uw gegevensstroom in te schakelen. Als deze optie is ingeschakeld, worden de gegevens automatisch toegevoegd.

U kunt bevestigen dat het door een randspoor met debugger in werking te stellen of door Verzekering te gebruiken wordt toegevoegd om een slag door te vinden [!DNL Edge Network].

### Schema-configuratie {#schema-configuration}

U moet de groepen van het weergebied aan uw Experience Platform toevoegen die aan de gebeurtenisdataset beantwoorden u in uw gegevensstroom gebruikt. Er zijn vijf veldgroepen beschikbaar:

* [!UICONTROL Forecasted Weather]
* [!UICONTROL Current Weather]
* [!UICONTROL Product Triggers]
* [!UICONTROL Relative Triggers]
* [!UICONTROL Severe Weather Triggers]

## Toegang tot de weergegevens {#access-weather-data}

Zodra u een licentie hebt en de gegevens beschikbaar zijn, kunt u deze op verschillende manieren openen in de Adobe-services.

### Adobe Analytics {#analytics}

In [!DNL Adobe Analytics], zijn de weergegevens beschikbaar om te worden toegewezen via verwerkingsregels, samen met de rest van uw [!DNL XDM] schema.

U kunt de lijst met velden vinden die u kunt toewijzen in het dialoogvenster [weerreferentie](weather-reference.md) pagina. Zoals bij alles [!DNL XDM] schema&#39;s, de sleutels worden vooraf bepaald met `a.x`. Een veld met de naam `weather.current.temperature.farenheit` zou verschijnen binnen [!DNL Analytics] als `a.x.weather.current.temperature.farenheit`.

![Interface van verwerkingsregel](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

In [!DNL Adobe Customer Journey Analytics], zijn de weergegevens beschikbaar in de dataset die in de gegevensstroom wordt gespecificeerd. Zolang de weerkenmerken [toegevoegd aan uw schema](#prerequisites-prerequisites), zullen zij beschikbaar zijn aan [toevoegen aan een gegevensweergave](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html) in [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

Weezelgegevens zijn beschikbaar in het dialoogvenster [Real-time Customer Data Platform](../../../rtcdp/overview.md), voor gebruik in segmenten. Weezelgegevens worden gekoppeld aan gebeurtenissen.

![Segement Builder met weersomstandigheden](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

Aangezien de weersomstandigheden vaak veranderen, adviseert Adobe dat u tijdbeperkingen op de segmenten, zoals aangetoond in het bovenstaande voorbeeld plaatst. Een koude dag in de laatste twee is veel impacter dan een koude dag zes maanden geleden.

Zie de [weerreferentie](weather-reference.md) voor de beschikbare velden.

### Adobe Target {#target}

In [!DNL Adobe Target], kunt u weergegevens gebruiken om personalisatie in real time te bevorderen. Weezelgegevens worden doorgegeven aan [!DNL Target] als [!UICONTROL mBox] parameters en u kunt deze openen via een aangepaste [!UICONTROL mBox] parameter.

![Doelpubliek Builder](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

De parameter is [!DNL XDM] pad naar een specifiek veld. Zie de [weerreferentie](weather-reference.md) voor de beschikbare velden en de bijbehorende paden.

## Volgende stappen {#next-steps}

Na het lezen van dit document hebt u nu een beter inzicht in hoe u weergegevens kunt gebruiken voor verschillende Adobe-oplossingen. Als u meer wilt weten over de toewijzing van weersgegevens, raadpleegt u de [veldtoewijzingsverwijzing](weather-reference.md).