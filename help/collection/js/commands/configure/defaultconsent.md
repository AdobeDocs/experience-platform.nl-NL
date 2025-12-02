---
title: defaultConsent
description: Stel de standaardmethode voor het verzamelen van toestemmingen in voor uw webeigenschap.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 1e272eb18fac2f59f9737756d48947a25573d772
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# `defaultConsent`

De eigenschap `defaultConsent` bepaalt hoe u toestemming voor gegevensverzameling afhandelt voordat u de opdracht [`setConsent`](../setconsent.md) aanroept. Deze eigenschap is nuttig wanneer u niet per ongeluk gegevens wilt verzamelen van personen die zich bevinden in gebieden waar toestemming is vereist voordat gegevens worden verzameld.

Als u een bezoeker hebt die niet onder de jurisdictie van Algemene Verordening van de Bescherming van Gegevens (GDPR) valt, zou de standaardtoestemming kunnen worden geplaatst aan `in`. Bezoekers binnen de jurisdictie van GDPR kunnen hun toestemming voor wanbetaling instellen op `pending` . Uw platform van het Beheer van de Toestemming (CMP) kan het gebied van de klant ontdekken en de vlag `gdprApplies` verstrekken aan IAB TCF 2.0. Deze markering kan worden gebruikt om de standaardtoestemming te plaatsen.

Stel de tekenreekseigenschap `defaultConsent` in op het gewenste toestemmingsniveau wanneer u de opdracht `configure` uitvoert. Deze eigenschap is hoofdlettergevoelig en ondersteunt alleen de volgende drie waarden: `"in"`, `"out"` en `"pending"` . Als u een andere waarde probeert te gebruiken, genereert de bibliotheek een fout. Als deze niet is ingesteld in de opdracht `configure` , is de standaardwaarde **`in`** .

>[!IMPORTANT]
>
>De waarde `defaultConsent` blijft niet behouden tussen het laden van pagina&#39;s. Controleer of u telkens wanneer u de opdracht `configure` aanroept de gewenste standaardtoestemming hebt ingesteld.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`**: De gegevensverzameling wordt normaal uitgevoerd totdat de gebruiker het programma afsluit.
* **`out`**: gegevens worden definitief verwijderd totdat de gebruiker het programma inschakelt.
* **`pending`**: De gegevens worden lokaal opgeslagen totdat de gebruiker de opdracht [`setConsent`](../setconsent.md) gebruikt.

>[!NOTE]
>
>Hoewel Adobe van plan is een robuustere reeks doelen of categorieën te bouwen die aansluiten bij de mogelijkheden en productaanbiedingen van Adobe, is de huidige implementatie een allesomvattende benadering van opt-in. Deze beperking geldt alleen voor de Web SDK en niet voor andere Adobe JavaScript-bibliotheken.

## `defaultConsent` gebruiken in combinatie met `setConsent` {#using-consent}

De Web SDK biedt twee aanvullende toestemmingsopties:

* `defaultConsent` (deze pagina): hiermee bepaalt u de voorkeuren voor de standaardtoestemming.
* [`setConsent`](../setconsent.md): leg de voorkeuren voor toestemming van bezoekers vast.

Wanneer deze instellingen samen worden gebruikt, kunnen ze leiden tot verschillende resultaten voor gegevensverzameling en cookie-instellingen, afhankelijk van de geconfigureerde waarden.

Zie de onderstaande tabel om te begrijpen wanneer gegevensverzameling plaatsvindt en wanneer cookies worden ingesteld, op basis van toestemmingsinstellingen.

| `defaultConsent` | `setConsent` | Gegevensverzameling vindt plaats | Web SDK stelt browsercookies in |
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

Zie [&#x200B; de koekjes van SDK van het Web van Adobe Experience Platform &#x200B;](https://experienceleague.adobe.com/nl/docs/core-services/interface/data-collection/cookies/web-sdk) voor een lijst van koekjes die de bibliotheekreeksen.

>[!NOTE]
>
>Identiteitscookies en toestemmingscookies worden ingesteld, zelfs als een bezoeker de cookies niet bijhoudt. Deze cookies zijn nodig om de voorkeuren voor gegevensverzameling te respecteren.

## Standaardtoestemming instellen op basis van `gdprApplies`

Sommige CMP&#39;s kunnen bepalen of algemene gegevensbeschermingsverordening (General Data Protection Regulation — GDPR) op de klant van toepassing is. Als u toestemming voor klanten wilt veronderstellen waar GDPR niet van toepassing is, kunt u de `gdprApplies` markering in een vraag TCF API gebruiken. Bijvoorbeeld:

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

In het bovenstaande codeblok wordt de opdracht `configure` aangeroepen nadat `tcData` is verkregen van de TCF API. Als `gdprApplies` true is, wordt de standaardtoestemming ingesteld op `pending` . Als `gdprApplies` false is, wordt de standaardtoestemming ingesteld op `in` . Vul de variabele `alloyConfiguration` met uw configuratie in.

## Standaardtoestemming met de Web SDK-tagextensie

Zie [&#x200B; de montages van de Toestemming &#x200B;](/help/tags/extensions/client/web-sdk/configure/consent.md) in de de markeringsuitbreidingsdocumentatie van SDK van het Web leren hoe te om deze acties uit te voeren gebruikend markeringen.
