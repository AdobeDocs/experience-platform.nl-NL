---
title: Gegevenstype voor zoeken interne site
description: Dit document biedt een overzicht van het XDM-gegevenstype voor zoeken op interne site.
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# [!UICONTROL Internal Site Search] gegevenstype

[!UICONTROL Internal Site Search] is een standaard XDM gegevenstype dat een interne plaatsonderzoek, met inbegrip van alle verwante onderzoeksgedrag en details beschrijft.

![](../images/data-types/internal-site-search.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Boolean] | Geeft aan of een bezoeker een voorgestelde of automatisch voltooide zoekwaarde heeft gebruikt om de zoekopdracht uit te voeren. |
| `autoCompleteTypedValue` | [!UICONTROL String] | Voor scenario&#39;s autocomplete, verlaten de gebruikers soms hun onderzoek en selecteren een specifieke termijn van dropdown. Deze waarde houdt bij wat de gebruiker begon te typen om de specifieke reeks voorgestelde zoektermen te genereren. |
| `autoCompleteValue` | [!UICONTROL String] | Voor scenario&#39;s autocomplete, verlaten de gebruikers soms hun onderzoek en selecteren een specifieke termijn van dropdown menu. Deze waarde wordt gebruikt om de specifieke geselecteerde termen bij te houden. |
| `instances` | [!UICONTROL Integer] | Het aantal keren dat de interne sitezoekopdracht is uitgevoerd. |
| `locationInPage` | [!UICONTROL String] | Wanneer de pagina meerdere zoekvakken bevat, moet u deze waarde gebruiken om de specifieke locatie aan te duiden die de gebruiker heeft gebruikt om te zoeken. |
| `nullInstances` | [!UICONTROL Integer] | Het aantal keren dat de interne sitezoekopdracht is uitgevoerd en dat er geen resultaten zijn geboekt. |
| `numberOfResults` | [!UICONTROL Integer] | Het totale aantal geretourneerde zoekresultaten. |
| `postalCode` | [!UICONTROL String] | De postcode die voor de zoekopdracht wordt gebruikt, indien van toepassing. |
| `productFindingMethods` | [!UICONTROL String] | De interne waarde van de het vraagtermijn van het plaatsenonderzoek met handelaardiserende band. Deze waarde geeft aan naar welke term is gezocht vlak voordat een product werd bekeken. |
| `radiusDistance` | [!UICONTROL Integer] | Gecombineerd met `radiusType`, geeft de geselecteerde afstand van de zoekstraal aan. |
| `radiusType` | [!UICONTROL Integer] | Het geselecteerde afstandstype `radiusDistance`, hetzij kilometers of kilometers. |
| `refinementInstances` | [!UICONTROL Integer] | Het aantal keren dat de interne sitezoekopdracht is verfijnd. |
| `refinementType` | Array van tekenreeksen | Hier worden de verfijningstypen weergegeven die op de zoekresultaten worden toegepast. Voorbeelden zijn afdeling, merk, prijs, in-store, beoordeling, kleur, materiaal, enzovoort. |
| `refinementValue` | [!UICONTROL String] | De waarde waarnaar de zoekopdracht is verfijnd. |
| `resultsPageNumber` | [!UICONTROL Integer] | Voor gepagineerde zoekresultaten volgt deze waarde de pagina met resultaten die de bezoeker bekijkt. |
| `resultsPerPage` | [!UICONTROL Integer] | Voor gepagineerde zoekresultaten houdt deze waarde bij hoeveel zoekresultaten per pagina worden weergegeven. |
| `searchType` | [!UICONTROL String] | Vangt de methode van onderzoek die, indien toepasselijk wordt uitgevoerd. Voorbeelden zijn een &#39;type-ahead&#39;-zoekopdracht, een rechtstreeks getypte zoekopdracht of een ander type aangepaste zoekfunctionaliteit die een site mogelijk heeft. |
| `sortOrder` | [!UICONTROL String] | Gecombineerd met `sortType`, geeft de sorteervolgorde van de zoekresultaten aan, in oplopende of aflopende volgorde. |
| `term` | [!UICONTROL String] | De interne zoekterm voor de site die door de bezoeker is ingevoerd. |

{style=&quot;table-layout:auto&quot;}

Voor meer details over het gegevenstype raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
