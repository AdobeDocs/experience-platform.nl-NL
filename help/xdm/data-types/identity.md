---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;identiteit;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype identiteit
description: Leer over het Identiteit XDM gegevenstype.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# [!UICONTROL Identity] gegevenstype

[!UICONTROL Identity] is een standaard XDM gegevenstype dat wordt gebruikt om mensen duidelijk te onderscheiden die met digitale ervaringen in wisselwerking staan. De identiteit wordt vastgesteld door een identiteitsprovider, waarnaar zelf wordt verwezen in een `namespace` -kenmerk. Binnen elke `namespace` is de identiteit uniek.

![](../images/data-types/identity.png){width=550}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `namespace` | Object | Een object dat één tekenreeksveld bevat (`code`). Dit geeft de naamruimte aan die is gekoppeld aan het opgegeven `id` -kenmerk. |
| `authenticatedState` | String | De geverifieerde status voor deze identiteit op het moment van de waargenomen Experience Event. Zie [&#x200B; bijlage &#x200B;](#authenticatedState) voor erkende waarden en definities. |
| `id` | String | De identiteit van de consument in de verwante naamruimte. |
| `primary` | Boolean | Geeft aan of dit de primaire identiteit voor het individu is. Elke persoon kan slechts één primaire identiteit hebben. |
| `xid` | String | Wanneer deze waarde aanwezig is, vertegenwoordigt deze een naamruimte-id die uniek is voor alle naamruimte-bereikid&#39;s in alle naamruimten. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Bijlage

De volgende sectie bevat aanvullende informatie over het gegevenstype [!UICONTROL Identity] .

## Geaccepteerde waarden voor authenticatedState {#authenticatedState}

In de volgende tabel worden de geaccepteerde waarden voor `authenticatedState` en de bijbehorende betekenissen weergegeven:

| Waarde | Beschrijving |
| --- | --- |
| `ambiguous` | De voor authentiek verklaarde staat is dubbelzinnig. |
| `authenticated` | De gebruiker werd geïdentificeerd door een login of een gelijkaardige actie die op het tijdstip van de gebeurtenisobservatie geldig was. |
| `loggedOut` | De gebruiker werd geïdentificeerd door een login actie op één of ander vorig punt in tijd, maar niet het programma geopend op het tijdstip van de gebeurtenisobservatie. |
