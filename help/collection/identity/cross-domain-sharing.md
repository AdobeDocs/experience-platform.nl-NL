---
title: Identiteit delen over domeinen
description: Handhaaf identiteitscontinuïteit over domeinen die uw organisatie bezit om verpersoonlijking en rapportering te verbeteren.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Identiteit delen over domeinen

Wanneer bezoekers schakelen tussen domeinen die eigendom zijn van uw organisatie, behoudt elk domein standaard zijn eigen bezoekersidentiteit. Zonder expliciete overdracht wordt een bezoeker die van één van uw domeinen aan een andere klikt behandeld als nieuwe, onbekende persoon op de bestemmingsplaats. Dit type implementatiefragmenten rapporteert en start personalisatie opnieuw.

Met het delen van domeinidentiteit lost u dit probleem op door een parameter `adobe_mc` voor query-tekenreeksen aan de doel-URL toe te voegen wanneer een bezoeker op een koppeling klikt of opnieuw wordt omgeleid. Deze parameter draagt identiteitskaart van Experience Cloud van de bezoeker [&#x200B; (ECID) &#x200B;](./overview.md), uw organisatie identiteitskaart, en timestamp. Wanneer de bestemmingspagina met een geldige `adobe_mc` parameter laadt, leest het Web SDK automatisch het en past de uitgaande identiteit op zijn eerste Edge Network- verzoek toe, zodat delen beide domeinen de zelfde bezoeker. De parameter `adobe_mc` verloopt na vijf minuten, zodat moet de bestemmingspagina onmiddellijk na omleiding laden.

In dit geval wordt het delen van identiteiten tussen websites op verschillende domeinen besproken. Als u identiteit van een mobiele toepassing in een WebView of mobiele Web-pagina wilt overgaan, gebruik [&#x200B; mobiel-aan-Web identiteit het delen &#x200B;](./mobile-to-web.md) in plaats daarvan.

## Vereisten

Voordat u begint, moet u ervoor zorgen dat uw implementatie aan de volgende vereisten voldoet:

* **SDK van het Web**: [&#x200B; SDK van het Web &#x200B;](/help/collection/js/js-overview.md) versie **2.11.0 of later**, of de de markeringsuitbreiding van SDK van het Web, wordt geïnstalleerd op zowel de bron als bestemmingsdomeinen.
* **het Aanpassen configuratie**: Alle deelnemende domeinen gebruiken het zelfde [`orgId`](../js/commands/configure/orgid.md) wanneer het vormen van het Web SDK.
* **controle URL**: Uw code controleert de verbindingen of richt tussen domeinen opnieuw zodat u vraag-koord parameters aan de bestemming URL kunt toevoegen.

## Interdomeindeling implementeren

U moet identiteit het delen op elk domein vormen dat als bron in een dwars-domeinoverdracht dienst doet. Als bezoekers in beide richtingen tussen twee domeinen kunnen navigeren, vorm beide domeinen als bronnen.

>[!BEGINTABS]

>[!TAB  de bibliotheek van JavaScript ]

Gebruik de opdracht [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) om de parameter `adobe_mc` toe te voegen aan uitgaande koppelingen. In het volgende voorbeeld wordt geluisterd naar klikken op ankerelementen en wordt een identiteit toegevoegd aan elke koppeling die naar een gewenst domein wijst:

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB  de markeringsuitbreiding van SDK van het Web ]

Gebruik de handeling [**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) om de parameter `adobe_mc` toe te voegen aan uitgaande koppelingen. U kunt een regel met de volgende voorwaarden tot stand brengen om het gewenste gedrag te bereiken:

1. **Gebeurtenis**: Plaats de uitbreiding aan **[!UICONTROL Core]** en het gebeurtenistype aan **[!UICONTROL Click]**. Voer onder **[!UICONTROL Elements matching the CSS selector]** `a[href]` in.
2. **Voorwaarde**: Plaats de uitbreiding aan **[!UICONTROL Core]** en het voorwaardetype aan **[!UICONTROL Value Comparison]**. Stel **[!UICONTROL Left Operand]** in op `%this.hostname%` , **[!UICONTROL Operator]** op **[!UICONTROL Matches Regex]** en **[!UICONTROL Right Operand]** op een reguliere expressie die overeenkomt met uw doeldomeinen (bijvoorbeeld `example\.com$|example\.org$` ).
3. **Actie**: Plaats de uitbreiding aan **[!UICONTROL Adobe Experience Platform Web SDK]** en het actietype aan **[!UICONTROL Redirect with identity]**.

>[!ENDTABS]

## Identiteit ontvangen op het doeldomein

Er is geen aanvullende code vereist voor het doeldomein. Wanneer de SDK Web aanwezig is op de pagina en de URL een geldige `adobe_mc` -parameter bevat, extraheert de SDK automatisch de ECID en past deze toe op de identiteitskaart van de bezoeker op de eerste Edge Network-aanvraag.

Zorg ervoor dat het bestemmingsdomein aan de volgende voorwaarden voldoet:

* De Web SDK- of Web SDK-tagextensie wordt geïnstalleerd en geconfigureerd met dezelfde [`orgId`](../js/commands/configure/orgid.md) als het brondomein. U kunt de JavaScript-bibliotheek en de Web SDK-tagextensie onderling uitwisselen tussen domeinen, mits deze dezelfde domeinen delen `orgId` .
* De pagina laadt en verzendt zijn eerste verzoek van Edge Network binnen **vijf minuten** van redirect, alvorens de `adobe_mc` parameter verloopt.
