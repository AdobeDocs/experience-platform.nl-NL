---
title: Klasse Provider
description: Dit document biedt een overzicht van de klasse Provider in het XDM (Experience Data Model).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# [!UICONTROL Provider] class

In het Model van de Gegevens van de Ervaring (XDM), [!UICONTROL Provider] klasse legt de minimumreeks eigenschappen vast die een dienstverlener bedrijfsentiteit (zoals een zorgleverancier of verzekeringsleverancier) bepalen.

![Klassenstructuur](../images/classes/provider.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Person name]](../data-types/person-name.md) | De naam van de provider. |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, wordt er geen expliciete waarde opgegeven tijdens het invoeren van gegevens. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `providerId` | [!UICONTROL String] | Een unieke id voor de provider. |

{style="table-layout:auto"}

De klasse kan worden uitgebreid met de [[!UICONTROL Healthcare Provider] veldgroep](../field-groups/provider/healthcare-provider.md) voor nadere informatie over een zorgleverancier.
