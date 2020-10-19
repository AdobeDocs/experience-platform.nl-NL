---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;identity;datatype;data-type;data type;
solution: Experience Platform
title: Gegevenstype Identiteit
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype Identity.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 1%

---


# [!UICONTROL Gegevenstype Identiteit]

[!UICONTROL Identiteit] is een standaard XDM gegevenstype dat wordt gebruikt om mensen duidelijk te onderscheiden die met digitale ervaringen in wisselwerking staan. De identiteit wordt gevestigd door een identiteitsleverancier, die zelf in een `namespace` attribuut van verwijzingen wordt voorzien. Binnen elke `namespace`is de identiteit uniek.

<img src="../images/data-types/identity.png" width="550" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `namespace` | Object | Een object dat één tekenreeksveld (`code`) bevat, dat de naamruimte aangeeft die aan het opgegeven `id` kenmerk is gekoppeld. |
| `authenticatedState` | Tekenreeks | De voor authentiek verklaarde staat voor deze identiteit op het tijdstip van de waargenomen Gebeurtenis van de Ervaring. Zie de [bijlage](#authenticatedState) voor toegestane waarden en definities. |
| `id` | Tekenreeks | De identiteit van de consument in de verwante naamruimte. |
| `primary` | Boolean | Geeft aan of dit de primaire identiteit voor het individu is. Elke persoon kan slechts één primaire identiteit hebben. |
| `xid` | Tekenreeks | Wanneer deze waarde aanwezig is, vertegenwoordigt deze een naamruimte-id die uniek is voor alle naamruimte-bereikid&#39;s in alle naamruimten. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Aanhangsel

De volgende sectie bevat aanvullende informatie over het gegevenstype [!UICONTROL Identity] .

## Geaccepteerde waarden voor authenticatedState {#authenticatedState}

In de volgende tabel worden de geaccepteerde waarden voor `authenticatedState` en de bijbehorende betekenis weergegeven:

| Waarde | Beschrijving |
| --- | --- |
| `ambiguous` | De voor authentiek verklaarde staat is dubbelzinnig. |
| `authenticated` | De gebruiker werd geïdentificeerd door een login of een gelijkaardige actie die op het tijdstip van de gebeurtenisobservatie geldig was. |
| `loggedOut` | De gebruiker werd geïdentificeerd door een login actie op één of ander vorig punt in tijd, maar niet het programma geopend op het tijdstip van de gebeurtenisobservatie. |