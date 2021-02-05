---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schemas;baken;interactiedetails;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype baken
topic: overview
description: Dit document biedt een overzicht van de klasse Individueel profiel XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# [!UICONTROL Het type ] Beacondata

 Beaconis een standaard XDM gegevenstype dat het draadloze apparaat beschrijft dat identiteitsinformatie aan mobiele toepassingen meedeelt aangezien de mobiele apparaten binnen waaier vallen.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `beaconMajor` | Dubbel | De belangrijkste waarden identificeren en onderscheiden een groep en unsigned geheelwaarden tussen 1 en 65.535. |
| `beaconMinor` | Dubbel | Kleine waarden identificeren en onderscheiden een individueel geheel getal en waarden zonder teken tussen 1 en 65.535. |
| `proximity` | Tekenreeks | Geschatte afstand tot het baken. Zie [appendix](#proximity) voor geaccepteerde waarden en definities. |
| `proximityUUID` | Tekenreeks | Een nabijheid UUID (Universally Unique Identifier) is een speciaal type herkenningsteken dat wordt gebruikt om bakens in uw netwerk van alle andere bakens in netwerken buiten uw controle te onderscheiden. De nabijheid UUID wordt gevormd in een baken, dat aan mobiele apparaten in waaier moet worden overgebracht om de bakens van een organisatie te identificeren. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## Aanhangsel

De volgende sectie bevat extra informatie over het [!UICONTROL gegevenstype Beacon].

## Geaccepteerde waarden voor nabijheid {#proximity}

In de volgende tabel worden de geaccepteerde waarden voor `proximity` en de bijbehorende betekenissen weergegeven:

| Value | Beschrijving |
| --- | --- |
| `immediate` | Binnen enkele centimeter. |
| `near` | Op minder dan 10 meter afstand. |
| `far` | Op meer dan 10 meter afstand. |
| `unknown` | De afstand kon niet worden vastgesteld, waarschijnlijk als gevolg van een zwak signaal. |