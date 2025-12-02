---
title: edgeBasePath
description: Het basispad van het eindpunt dat wordt gebruikt voor interactie met Adobe-services.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

De eigenschap `edgeBasePath` wijzigt het doelpad wanneer u werkt met Adobe-services. Adobe kan vragen dat u deze variabele wijzigt als u deelneemt aan alfa- of bètaprogramma&#39;s voor gegevensverzameling. De meeste organisaties hoeven deze eigenschap niet in te stellen of te wijzigen.

Stel het tekstveld `edgeBasePath` in wanneer u de opdracht `configure` uitvoert. Wanneer u deze eigenschap weglaat, krijgt deze standaard de waarde `ee` . Adobe raadt aan deze eigenschap uit de meeste configuraties weg te laten.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## Edge-basispad met de webtagextensie SDK

Het de markeringsuitbreidingsequivalent van SDK van het Web van dit gebied is onder [&#x200B; Geavanceerde configuratiemontages &#x200B;](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md) wanneer het vormen van de markeringsuitbreiding.
