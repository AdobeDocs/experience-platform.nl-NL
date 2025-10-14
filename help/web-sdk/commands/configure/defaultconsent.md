---
title: defaultConsent
description: Stel de standaardmethode voor het verzamelen van toestemmingen in voor uw webeigenschap.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---


# `defaultConsent`

De eigenschap `defaultConsent` bepaalt hoe u toestemming voor gegevensverzameling afhandelt voordat u de opdracht [`setConsent`](../setconsent.md) aanroept. Deze eigenschap is nuttig wanneer u niet per ongeluk gegevens wilt verzamelen van personen die zich bevinden in gebieden waar toestemming is vereist voordat gegevens worden verzameld.

Door gebrek, worden de gebruikers binnen aan alle doeleinden gekozen, en SDK van het Web wordt toegestaan om de volgende taken uit te voeren:

* Gegevens verzenden van en naar de servers van de Adobe.
* Cookies of webopslagitems lezen en schrijven.

Als de gebruikers uit alle doeleinden opteren, voert het Web SDK geen van deze taken uit.

De eigenschap `defaultConsent` ondersteunt drie waarden:

* **`in`**: de gegevensverzameling verloopt zoals gewoonlijk totdat de gebruiker de optie Weigeren inschakelt.
* **`out`**: gegevens worden definitief verwijderd totdat de gebruiker het programma inschakelt.
* **`pending`**: De gegevens worden lokaal opgeslagen totdat de gebruiker de opdracht [`setConsent`](../setconsent.md) gebruikt. Wanneer de standaardtoestemming voor het algemene doel is ingesteld op `pending` , wordt bij een poging om opdrachten uit te voeren die afhankelijk zijn van de gebruikersaanmeldingsvoorkeuren (bijvoorbeeld de opdracht [`sendEvent`](../sendevent/overview.md) ) de opdracht in de webSDK in de wachtrij geplaatst. Opdrachten in de wachtrij worden pas verwerkt nadat u de aanmeldingsvoorkeuren van de gebruiker aan de Web SDK hebt doorgegeven.

>[!NOTE]
>
> Er blijven geen gegevens van de toestemming behouden tussen het laden van de pagina.

Als u een bezoeker hebt die niet onder de jurisdictie van Algemene Verordening van de Bescherming van Gegevens (GDPR) valt, zou de standaardtoestemming kunnen worden geplaatst aan `in`. Bezoekers binnen de jurisdictie van GDPR kunnen hun toestemming voor wanbetaling instellen op `pending` . Uw platform van het Beheer van de Toestemming (CMP) kan het gebied van de klant ontdekken en de vlag `gdprApplies` verstrekken aan IAB TCF 2.0. Deze markering kan worden gebruikt om de standaardtoestemming te plaatsen.

Als u geen gebeurtenissen wilt verzamelen die zich hebben voorgedaan voordat de aanmeldingsvoorkeuren van de gebruiker zijn ingesteld, kunt u `"defaultConsent": "out"` tijdens de Web SDK-configuratie doorgeven. Het proberen om het even welke bevelen uit te voeren die van gebruiker afhangen opent voorkeur zal geen effect hebben tot u de opt-in voorkeur van de gebruiker aan het Web SDK hebt meegedeeld.

>[!NOTE]
>
>Momenteel, steunt SDK van het Web slechts één enkel alles-of-niets doel. Hoewel we van plan zijn een robuustere reeks doelen of categorieën te ontwikkelen die zullen overeenkomen met de verschillende mogelijkheden en productaanbiedingen van de Adobe, is de huidige implementatie een allesomvattende benadering van opt-in.  Dit geldt alleen voor [!DNL Web SDK] - en NIET voor andere Adobe JavaScript-bibliotheken.

## `defaultConsent` gebruiken in combinatie met `setConsent` {#using-consent}

De Web SDK biedt twee aanvullende opdrachten voor de configuratie van toestemmingen:

* [`defaultConsent`](defaultconsent.md): deze opdracht is bedoeld om de voorkeuren voor toestemming van Adobe klanten vast te leggen met gebruik van Web SDK.
* [`setConsent`](../setconsent.md): deze opdracht is bedoeld om de voorkeuren voor toestemming van uw sitebezoekers vast te leggen.

Wanneer deze instellingen samen worden gebruikt, kunnen ze leiden tot verschillende resultaten voor gegevensverzameling en cookie-instellingen, afhankelijk van de geconfigureerde waarden.

Zie de onderstaande tabel om te begrijpen wanneer gegevensverzameling plaatsvindt en wanneer cookies worden ingesteld, op basis van toestemmingsinstellingen.

| defaultConsent | setConsent | Gegevensverzameling vindt plaats | Web SDK stelt browsercookies in |
|---------|----------|---------|---------|
| `in` | `in` | Ja | Ja |
| `in` | `out` | Nee | Ja |
| `in` | Niet ingesteld | Ja | Ja |
| `pending` | `in` | Ja | Ja |
| `pending` | `out` | Nee | Ja |
| `pending` | Niet ingesteld | Nee | Nee |
| `out` | `in` | Ja | Ja |
| `out` | `out` | Nee | Ja |
| `out` | Niet ingesteld | Nee | Nee |

De volgende cookies worden ingesteld wanneer de configuratie van de toestemming dit toestaat:

| Naam | Max. leeftijd | Beschrijving |
|---|---|---|
| **AMCV_##@AdobeOrg** | 34128000 (395 dagen) | Wordt weergegeven wanneer [`idMigrationEnabled`](../configure/idmigrationenabled.md) is ingeschakeld. Het helpt bij het overschakelen naar Web SDK terwijl sommige delen van de site nog steeds `visitor.js` gebruiken. |
| **het koekje van de Index** | 15552000 (180 dagen) | Presenteren als id-synchronisatie is ingeschakeld. Audience Manager stelt dit cookie zo in dat een unieke id wordt toegewezen aan een sitebezoeker. Het demdex-cookie helpt Audience Manager basisfuncties uit te voeren, zoals bezoekersidentificatie, id-synchronisatie, segmentatie, modellering, rapportage, enzovoort. |
| **kndctr_orgid_cluster** | 1800 (30 minuten) | Hiermee slaat u het gebied Edge Network op dat de verzoeken van de huidige gebruiker dient. Het gebied wordt gebruikt in de weg URL zodat de Edge Network het verzoek aan het correcte gebied kan leiden. Als een gebruiker met een verschillend IP adres of in een verschillende zitting verbindt, wordt het verzoek opnieuw verpletterd aan het dichtstbijzijnde gebied. |
| **kCt_orgid_identity** | 34128000 (395 dagen) | Hiermee slaat u de ECID op, evenals andere informatie over de ECID. |
| **kndctr_orgid_permission** | 15552000 (180 dagen) | Hiermee slaat u de voorkeur van de gebruikers voor toestemming voor de website op. |
| **s_ecid** | 63115200 (2 jaar) | Bevat een exemplaar van Experience Cloud identiteitskaart ([!DNL ECID]) of MID. MID wordt opgeslagen in een sleutelwaardepaar dat deze syntaxis volgt, `s_ecid=MCMID\|<ECID>`. |

## Standaardtoestemming instellen met de webSDK-tagextensie

Selecteer het gewenste radioknoop onder **[!UICONTROL Default consent]** wanneer [&#x200B; het vormen van de markeringsuitbreiding &#x200B;](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie [!UICONTROL Privacy] en selecteer vervolgens de gewenste sectie **[!UICONTROL Default consent]** .
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## Standaardtoestemming instellen met de Web SDK JavaScript-bibliotheek

Stel de tekenreekseigenschap `defaultConsent` in op het gewenste toestemmingsniveau wanneer u de opdracht `configure` uitvoert. Deze eigenschap is hoofdlettergevoelig en ondersteunt alleen de volgende drie waarden: `"in"`, `"out"` en `"pending"` . Als u een andere waarde probeert te gebruiken, genereert de bibliotheek een fout.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```
