---
title: defaultConsent
description: Stel de standaardverzamelingsmethode voor toestemming in.
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# `defaultConsent`

De `defaultConsent` eigenschap bepaalt hoe de toestemming voor gegevensverzameling wordt verwerkt voordat u de optie [`setConsent`](../setconsent.md) gebruiken. Deze eigenschap is nuttig wanneer u niet per ongeluk gegevens wilt verzamelen van personen die zich bevinden in gebieden waar toestemming is vereist voordat gegevens worden verzameld.

Deze eigenschap staat drie waarden toe:

* **In**: De verzameling van gegevens verloopt normaal, totdat de gebruiker de functie uitschakelt.
* **Uit**: Gegevens worden definitief verwijderd totdat de gebruiker inklikt.
* **In behandeling**: Gegevens worden lokaal opgeslagen totdat de gebruiker het dialoogvenster [`setConsent`](../setconsent.md) gebruiken. Er blijven geen gegevens behouden tussen het laden van pagina&#39;s.

Als u een bezoeker hebt die niet binnen de jurisdictie van Algemene Verordening van de Bescherming van Gegevens (GDPR) valt, zou de standaardtoestemming kunnen worden geplaatst aan `in`. Bezoekers binnen de jurisdictie van de GDPR zouden hun toestemming voor wanbetaling kunnen instellen op `pending`. Uw CMP (Consent Management Platform) kan het gebied van de klant detecteren en de vlag voorzien `gdprApplies` naar IAB TCF 2.0. Deze markering kan worden gebruikt om de standaardtoestemming te plaatsen.

## Standaardtoestemming instellen met de webSDK-tagextensie

Selecteer het gewenste keuzerondje onder **[!UICONTROL Default consent]** wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Privacy] en selecteert u vervolgens het gewenste **[!UICONTROL Default consent]**.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## Standaardtoestemming instellen met de Web SDK JavaScript-bibliotheek

Stel de `defaultConsent` tekenreeks-eigenschap naar het gewenste toestemmingsniveau wanneer de eigenschap wordt uitgevoerd `configure` gebruiken. Deze eigenschap is hoofdlettergevoelig en ondersteunt alleen de volgende drie waarden: `"in"`, `"out"`, en `"pending"`. Als u een andere waarde probeert te gebruiken, genereert de bibliotheek een fout.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
