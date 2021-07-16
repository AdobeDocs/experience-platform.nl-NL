---
title: Reacties filteren in de Reactor-API
description: Leer hoe u resultaten kunt filteren wanneer u bronnen opsomt in de Reactor-API.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

---

# Reacties filteren in de Reactor-API

Wanneer u eindpunten van lijsten (GET) gebruikt in de Reactor-API, is het mogelijk dat u de geretourneerde resultaten moet beperken tot een subset van records. Hiervoor ondersteunen veel van de eindpunten van de lijst van de API de mogelijkheid om te filteren op specifieke kenmerken. Als u gestructureerde vragen aan API in plaats daarvan wenst te maken, zie de gids op [zoekend](./search.md).

## Filtersyntaxis

In het volgende voorbeeld wordt uitgelegd hoe u filters voor uw GET-aanvragen kunt implementeren.

**API-indeling**

Om de reactie voor een bepaald lijsteindpunt te filtreren, moet u een `filter` vraagparameter in de verzoekweg leveren.

>[!NOTE]
>
>In de onderstaande sjabloon worden vierkante haken (`[]`) en spatietekens gebruikt voor leesbaarheid. In de praktijk, moeten deze karakters URI-gecodeerd zijn, zoals geschetst in [RFC 3986](https://tools.ietf.org/html/rfc3986). Deze handleiding bevat een voorbeeld van een correct gecodeerd aanvraagpad.
>
>Als de structuur van de filters onjuist is, worden geen filters toegepast en wordt de volledige resultaatset geretourneerd.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `{ENDPOINT}` | Een eindpunt in de Reactor-API dat filterparameters ondersteunt. |
| `{ATTRIBUTE_NAME}` | De naam van een specifiek kenmerk waarop filterresultaten moeten worden uitgevoerd. Houd er rekening mee dat verschillende eindpunten verschillende kenmerken voor filteren ondersteunen. Verwijs naar de verwijzingsgids voor het eindpunt u met voor een lijst van beschikbare het filtreren attributen werkt. |
| `{OPERATOR}` | De operator die bepaalt hoe de resultaten worden geëvalueerd op basis van de opgegeven `{VALUE}`. Ondersteunde operatoren worden vermeld in de [bijlage sectie](#supported-operators). |
| `{VALUE}` | De waarde waarmee de geretourneerde resultaten moeten worden vergeleken. Wanneer u vergelijkt voor gelijkheid met de operator `EQ`, moet de waarde een exacte, hoofdlettergevoelige overeenkomst zijn om te worden opgenomen in de reactie. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt een lijst met gepubliceerde bibliotheken opgehaald door een filter toe te passen waarbij het kenmerk `state` van de bibliotheek gelijk moet zijn aan `published`.

Voordat URI-codering wordt uitgevoerd, ziet de syntaxis voor dit filter in het aanvraagpad er ongeveer als volgt uit:

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

Zodra de weg en vraagparameters URI-gecodeerd zijn, kunnen zij in API verzoeken zoals hieronder worden gebruikt:

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

## Filteren op meerdere waarden {#multiple-values}

Als u met meerdere waarden voor één kenmerk wilt filteren, geeft u de waarden op als een lijst met door komma&#39;s gescheiden waarden.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## Meerdere filters gebruiken

Als u filters voor meerdere kenmerken wilt toepassen, voert u voor elk kenmerk een `filter`-parameter in. Parameters moeten worden gescheiden door en-tekens (`&`).

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>Als u hetzelfde kenmerk in meerdere filters opgeeft op dezelfde aanvraag, wordt alleen het laatst opgegeven filter voor dat kenmerk toegepast.

## Aanhangsel

De volgende sectie bevat aanvullende informatie voor het werken met filters in de Reactor-API.

### Ondersteunde filteroperatoren {#operators}

In de volgende tabel worden de ondersteunde operatorwaarden voor filterparameters weergegeven. Houd er rekening mee dat, afhankelijk van het kenmerk waarop u filtert, niet alle beschikbare filteroperatoren van toepassing zijn, zoals het gebruik van de operatoren &quot;kleiner dan&quot; of &quot;groter dan&quot; voor tekenreekskenmerken.

| Operator | Beschrijving |
| --- | --- |
| `EQ` | Het kenmerk moet gelijk zijn aan de opgegeven waarde. |
| `NOT` | Het kenmerk mag niet gelijk zijn aan de opgegeven waarde. |
| `LT` | Het kenmerk moet kleiner zijn dan de opgegeven waarde. |
| `GT` | Het kenmerk moet groter zijn dan de opgegeven waarde. |
| `BETWEEN` | Het kenmerk moet binnen een opgegeven waardenbereik vallen. Wanneer u deze operator gebruikt, moeten [twee waarden](#multiple-values) worden opgegeven om de minimum- en maximumwaarden voor het gewenste bereik aan te geven. |
| `CONTAINS` | Het kenmerk moet de opgegeven waarde bevatten, zoals een set tekens binnen een tekenreekskenmerk. |
