---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;
solution: Experience Platform
title: Detailsvakgroep handel
topic-legacy: overview
description: Dit document verstrekt een overzicht van de het schemagebiedgroep van de Details van de Handel.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---


# [!UICONTROL Commerce Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL Commerce Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM ExperienceEvent] klasse](../../classes/experienceevent.md), die wordt gebruikt om handelsgegevens zoals productinformatie (SKU, naam, hoeveelheid), en standaardkartverrichtingen (orde, checkout, verlaten) te beschrijven.

![](../../images/field-groups/commerce-details.png)

| Eigenschap | Data type | Beschrijving |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Een object dat productretourneert, garantieregistratie en processen voor winkelwagentjes/bestellingen beschrijft. |
| `productListItems` | Array of [Product list items](../../data-types/product-list-item.md) | Een lijst met items die de door een klant geselecteerde producten vertegenwoordigen, met specifieke opties en prijzen op een bepaald tijdstip (die kunnen verschillen van de productregistratie). |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
