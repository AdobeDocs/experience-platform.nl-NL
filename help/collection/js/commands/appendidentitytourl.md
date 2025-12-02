---
title: appendIdentityToUrl
description: Lever persoonlijke ervaringen nauwkeuriger tussen apps, het Web, en over domeinen.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

Met de opdracht `appendIdentityToUrl` kunt u een gebruiker-id aan de URL toevoegen als een queryreeks. Met deze actie kunt u de identiteit van een bezoeker tussen domeinen dragen, waardoor dubbele bezoekersaantallen voor datasets met zowel domeinen als kanalen worden voorkomen. Het is beschikbaar op het Web SDK versie 2.11.0 of later.

De querytekenreeks die wordt gegenereerd en aan de URL wordt toegevoegd, is `adobe_mc` . Als het Web SDK geen ECID kan vinden, roept het het `/acquire` eindpunt om te produceren.

>[!NOTE]
>
>Als er geen toestemming is gegeven, wordt de URL van deze methode ongewijzigd geretourneerd. Deze opdracht wordt onmiddellijk uitgevoerd; er wordt niet gewacht op een toestemmingsupdate.

Voer de opdracht `appendIdentityToUrl` uit met een URL als parameter. De methode retourneert een URL waarvan de id als queryreeks is toegevoegd.

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

U kunt een gebeurtenislistener toevoegen voor alle klikken die op de pagina worden ontvangen en controleren of de URL overeenkomt met de gewenste domeinen. Als dit het geval is, voegt u de identiteit toe aan de URL en leidt u de gebruiker om.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

Deze opdracht ondersteunt het object [`edgeConfigOverrides`](configure/edgeconfigoverrides.md) .

## Object Response

Wanneer [ behandelende reacties ](command-responses.md) met dit bevel, bevat het reactievoorwerp **`url`**, nieuwe URL met identiteitsinformatie die als parameter van het vraagkoord wordt toegevoegd.

## Identiteit toevoegen aan URL met de extensie Web SDK

De de markeringsuitbreiding van SDK van het Web gelijkwaardig aan dit bevel is [ opnieuw richt met identiteit ](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) actie.
