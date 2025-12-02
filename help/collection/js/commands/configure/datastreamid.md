---
title: datastreamId
description: Bepaal de gegevensstroom-id waarnaar u gegevens wilt verzenden.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---

# `datastreamId`

Het `datastreamId` bezit is een koord dat bepaalt welke [ datastream ](/help/datastreams/overview.md) in Adobe Experience Platform u gegevens naar wilt verzenden. Deze eigenschap is vereist wanneer gegevens naar Adobe worden verzonden. Web SDK versie 2.20.0 of eerder gebruikt `edgeConfigId` .

Een gegevensstroom-id zoeken:

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Gebruik het onderzoeksgebied om van de gewenste gegevensstroom de plaats te bepalen, dan selecteren **[!UICONTROL Copy]** ![ Exemplaar ](../../assets/copy.png) naast gegevensstroom identiteitskaart

U kunt ook de gewenste gegevensstroomnaam selecteren en de gegevensstroom-id verschijnt in de rechterkolom voor kopiëren.

## Codevoorbeeld

Stel de eigenschap `datastreamID` string in wanneer u de opdracht `configure` uitvoert. Dit bezit wordt vereist voor alle implementaties van SDK van het Web. Als u deze eigenschap weglaat, weet de SDK van het Web niet naar welke gegevensstroom gegevens moeten worden verzonden, waardoor die gegevens permanent verloren gaan.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>Als u veelvoudige instanties van het Web SDK op één enkele pagina vormt, moet u verschillende `datastreamId` voor elke instantie vormen.

## Selecteer de gegevensstroom-id met de Web SDK-tagextensie

Zie [ de configuratiemontages van de Gegevensstroom ](/help/tags/extensions/client/web-sdk/configure/datastreams.md) in de de markeringsuitbreidingsdocumentatie van SDK van het Web leren hoe te om de gewenste gegevensstroom voor elk milieu te plaatsen gebruikend markeringen. U kunt gegevens naar verschillende gegevensstromen voor productie, het opvoeren, en milieu&#39;s van ontwikkelingsmarkeringen verzenden.
