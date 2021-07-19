---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schemas;baken;interactiedetails;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype baken
topic-legacy: overview
description: Dit document biedt een overzicht van de klasse Individueel profiel XDM.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# [!UICONTROL Beacon] gegevenstype

[!UICONTROL Beacon] is een standaard XDM gegevenstype dat het draadloze apparaat beschrijft dat identiteitsinformatie aan mobiele toepassingen meedeelt aangezien de mobiele apparaten binnen waaier vallen.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `beaconMajor` | Dubbel | De belangrijkste waarden identificeren en onderscheiden een groep en unsigned geheelwaarden tussen 1 en 65.535. |
| `beaconMinor` | Dubbel | Kleine waarden identificeren en onderscheiden een individueel geheel getal en waarden zonder teken tussen 1 en 65.535. |
| `proximity` | Tekenreeks | Geschatte afstand tot het baken. Zie [appendix](#proximity) voor geaccepteerde waarden en definities. |
| `proximityUUID` | Tekenreeks | Een nabijheid UUID (Universally Unique Identifier) is een speciaal type herkenningsteken dat wordt gebruikt om bakens in uw netwerk van alle andere bakens in netwerken buiten uw controle te onderscheiden. De nabijheid UUID wordt gevormd in een baken, dat aan mobiele apparaten in waaier moet worden overgebracht om de bakens van een organisatie te identificeren. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Aanhangsel

De volgende sectie bevat aanvullende informatie over het gegevenstype [!UICONTROL Beacon].

## Geaccepteerde waarden voor nabijheid {#proximity}

In de volgende tabel worden de geaccepteerde waarden voor `proximity` en de bijbehorende betekenissen weergegeven:

| Waarde | Beschrijving |
| --- | --- |
| `immediate` | Binnen enkele centimeter. |
| `near` | Op minder dan 10 meter afstand. |
| `far` | Op meer dan 10 meter afstand. |
| `unknown` | De afstand kon niet worden vastgesteld, waarschijnlijk als gevolg van een zwak signaal. |
