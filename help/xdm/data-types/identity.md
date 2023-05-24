---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;identiteit;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype identiteit
description: Dit document biedt een overzicht van het XDM-gegevenstype Identity.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 2%

---

# [!UICONTROL Identity] gegevenstype

[!UICONTROL Identity] is een standaard XDM gegevenstype dat wordt gebruikt om mensen duidelijk te onderscheiden die met digitale ervaringen in wisselwerking staan. De identiteit wordt vastgesteld door een identiteitsprovider, waarnaar zelf wordt verwezen in een `namespace` kenmerk. Binnen elke `namespace`, is de identiteit uniek.

<img src="../images/data-types/identity.png" width="550" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `namespace` | Object | Een object dat één tekenreeksveld bevat (`code`), die de naamruimte aangeeft die is gekoppeld aan de opgegeven `id` kenmerk. |
| `authenticatedState` | Tekenreeks | De voor authentiek verklaarde staat voor deze identiteit op het tijdstip van de waargenomen Gebeurtenis van de Ervaring. Zie de [aanhangsel](#authenticatedState) voor aanvaarde waarden en definities. |
| `id` | Tekenreeks | De identiteit van de consument in de verwante naamruimte. |
| `primary` | Boolean | Geeft aan of dit de primaire identiteit voor het individu is. Elke persoon kan slechts één primaire identiteit hebben. |
| `xid` | Tekenreeks | Wanneer deze waarde aanwezig is, vertegenwoordigt deze een naamruimte-id die uniek is voor alle naamruimte-bereikid&#39;s in alle naamruimten. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Aanhangsel

De volgende sectie bevat aanvullende informatie over de [!UICONTROL Identity] gegevenstype.

## Geaccepteerde waarden voor authenticatedState {#authenticatedState}

In de volgende tabel worden de toegestane waarden voor `authenticatedState` en de betekenis ervan:

| Waarde | Beschrijving |
| --- | --- |
| `ambiguous` | De voor authentiek verklaarde staat is dubbelzinnig. |
| `authenticated` | De gebruiker werd geïdentificeerd door een login of een gelijkaardige actie die op het tijdstip van de gebeurtenisobservatie geldig was. |
| `loggedOut` | De gebruiker werd geïdentificeerd door een login actie op één of ander vorig punt in tijd, maar niet het programma geopend op het tijdstip van de gebeurtenisobservatie. |
