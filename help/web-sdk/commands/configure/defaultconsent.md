---
title: defaultConsent
description: Stel de standaardmethode voor het verzamelen van toestemmingen in voor uw webeigenschap.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---


# `defaultConsent`

De `defaultConsent` eigenschap bepaalt hoe de toestemming voor gegevensverzameling wordt verwerkt voordat u de optie [`setConsent`](../setconsent.md) gebruiken. Deze eigenschap is nuttig wanneer u niet per ongeluk gegevens wilt verzamelen van personen die zich bevinden in gebieden waar toestemming is vereist voordat gegevens worden verzameld.

Door gebrek, worden de gebruikers binnen aan alle doeleinden gekozen, en SDK van het Web wordt toegestaan om de volgende taken uit te voeren:

* Gegevens verzenden van en naar de servers van de Adobe.
* Cookies of webopslagitems lezen en schrijven.

Als de gebruikers uit alle doeleinden opteren, voert het Web SDK geen van deze taken uit.

De `defaultConsent` eigenschap ondersteunt drie waarden:

* **`in`**: De verzameling van gegevens verloopt normaal, totdat de gebruiker de functie uitschakelt.
* **`out`**: Gegevens worden definitief verwijderd totdat de gebruiker inklikt.
* **`pending`**: Gegevens worden lokaal opgeslagen totdat de gebruiker het dialoogvenster [`setConsent`](../setconsent.md) gebruiken. Wanneer de standaardtoestemming voor het algemene doel is ingesteld op `pending`, waarbij wordt geprobeerd opdrachten uit te voeren die afhankelijk zijn van de gebruikersvoorkeuren (bijvoorbeeld [`sendEvent`](../sendevent/overview.md) bevel) resulteert in het bevel dat in het Web SDK een rij wordt gevormd. Opdrachten in de wachtrij worden pas verwerkt nadat u de aanmeldingsvoorkeuren van de gebruiker aan de Web SDK hebt doorgegeven.

>[!NOTE]
>
> Er blijven geen gegevens van de toestemming behouden tussen het laden van de pagina.

Als u een bezoeker hebt die niet binnen de jurisdictie van Algemene Verordening van de Bescherming van Gegevens (GDPR) valt, zou de standaardtoestemming kunnen worden geplaatst aan `in`. Bezoekers binnen de jurisdictie van de GDPR zouden hun toestemming voor wanbetaling kunnen instellen op `pending`. Uw CMP (Consent Management Platform) kan het gebied van de klant detecteren en de vlag voorzien `gdprApplies` naar IAB TCF 2.0. Deze markering kan worden gebruikt om de standaardtoestemming te plaatsen.

Als u geen gebeurtenissen wilt verzamelen die zijn opgetreden voordat de aanmeldingsvoorkeuren van de gebruiker zijn ingesteld, kunt u `"defaultConsent": "out"` tijdens Web SDK-configuratie. Het proberen om het even welke bevelen uit te voeren die van gebruiker afhangen opent voorkeur zal geen effect hebben tot u de opt-in voorkeur van de gebruiker aan het Web SDK hebt meegedeeld.

>[!NOTE]
>
>Momenteel, steunt SDK van het Web slechts één enkel alles-of-niets doel. Hoewel we van plan zijn een robuustere reeks doelen of categorieën te ontwikkelen die zullen overeenkomen met de verschillende mogelijkheden en productaanbiedingen van de Adobe, is de huidige implementatie een allesomvattende benadering van opt-in.  Dit geldt alleen voor [!DNL Web SDK] en NIET andere Adobe JavaScript bibliotheken.

## Gebruiken `defaultConsent` samen met `setConsent` {#using-consent}

De Web SDK biedt twee aanvullende opdrachten voor de configuratie van toestemmingen:

* [`defaultConsent`](defaultconsent.md): Dit bevel wordt bedoeld om de toestemmingsvoorkeur van de klanten van de Adobe te vangen gebruikend Web SDK.
* [`setConsent`](../setconsent.md): Deze opdracht is bedoeld om de voorkeuren voor toestemming van uw sitebezoekers vast te leggen.

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
| **AMCV_##@AdobeOrg** | 34128000 (395 dagen) | Presenteren wanneer [`idMigrationEnabled`](../configure/idmigrationenabled.md) is ingeschakeld. Het helpt wanneer het overgaan naar Web SDK terwijl sommige delen van de plaats nog gebruiken `visitor.js`. |
| **Demdex cookie** | 15552000 (180 dagen) | Presenteren als id-synchronisatie is ingeschakeld. Audience Manager stelt dit cookie zo in dat een unieke id wordt toegewezen aan een sitebezoeker. Het demdex-cookie helpt Audience Manager basisfuncties uit te voeren, zoals bezoekersidentificatie, id-synchronisatie, segmentatie, modellering, rapportage, enzovoort. |
| **kndctr_orgid_cluster** | 1800 (30 minuten) | Hiermee slaat u het gebied Edge Network op dat de verzoeken van de huidige gebruiker dient. Het gebied wordt gebruikt in de weg URL zodat de Edge Network het verzoek aan het correcte gebied kan leiden. Als een gebruiker met een verschillend IP adres of in een verschillende zitting verbindt, wordt het verzoek opnieuw verpletterd aan het dichtstbijzijnde gebied. |
| **kndct_orgid_identity** | 34128000 (395 dagen) | Hiermee slaat u de ECID op, evenals andere informatie over de ECID. |
| **kndctr_orgid_permission** | 15552000 (180 dagen) | Hiermee slaat u de voorkeur van de gebruikers voor toestemming voor de website op. |
| **s_ecid** | 63115200 (2 jaar) | Bevat een kopie van de Experience Cloud-id ([!DNL ECID]) of MID. MID wordt opgeslagen in een zeer belangrijk-waardepaar dat deze syntaxis volgt, `s_ecid=MCMID\|<ECID>`. |

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
