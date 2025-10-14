---
title: Klasse Provider
description: Leer over de klasse van de Leverancier in het Model van de Gegevens van de Ervaring (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# [!UICONTROL Provider] -klasse

In het Model van de Gegevens van de Ervaring (XDM), vangt de [!UICONTROL Provider] klasse de minimumreeks eigenschappen die een dienstverlener bedrijfsentiteit (zoals een gezondheidszorgleverancier of een verzekeringsleverancier) bepalen.

![&#x200B; structuur van de Klasse &#x200B;](../images/classes/provider.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Person name]](../data-types/person-name.md) | De naam van de provider. |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br> Aangezien dit gebied systeem-geproduceerd is, wordt het geen expliciete waarde geleverd tijdens gegevensopname. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `providerId` | [!UICONTROL String] | Een unieke id voor de provider. |

{style="table-layout:auto"}

De klasse kan met de [[!UICONTROL Healthcare Provider] gebiedsgroep &#x200B;](../field-groups/provider/healthcare-provider.md) worden uitgebreid om verdere details over een gezondheidszorgleverancier te beschrijven.
