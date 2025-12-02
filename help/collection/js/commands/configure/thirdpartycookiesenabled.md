---
title: thirdPartyCookiesEnabled
description: Het gebruik van cookies van derden toestaan om bezoekers te identificeren.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

De eigenschap `thirdPartyCookiesEnabled` is een Booleaanse waarde die bepaalt of de Web SDK cookies instelt in een context van derden. Het inschakelen van deze optie is handig als u bezoekers wilt identificeren tussen subdomeinen of domeinen die eigendom zijn van uw organisatie. Veel moderne browsers beperken echter de instelling en vervaldatum van cookies van derden. Als de browser van een bezoeker geen cookies van derden ondersteunt, doet deze eigenschap niets.

De eigenschap `thirdPartyCookiesEnabled` bepaalt ook of een [`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk) kan worden opgevraagd voor [`getIdentity`](../getidentity.md) -aanroepen.

Als deze optie is ingeschakeld, gebruikt de Web SDK Adobe Audience Manager om een bezoeker te identificeren. Wanneer deze optie is uitgeschakeld, wordt de aanroep naar Audience Manager uitgeschakeld. Zie [ Begrip vraag aan het domein van de Index ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html) in de gebruikersgids van Audience Manager voor meer informatie.

Stel de Booleaanse waarde `thirdPartyCookiesEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `true` gebruikt. Stel deze waarde in op `false` als u niet wilt dat de Web SDK Audience Manager gebruikt om bezoekers te identificeren.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## Cookies van derden inschakelen met de extensie Web SDK

Dit plaatsen kan in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [ de configuratiemontages van de Identiteit ](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies).
