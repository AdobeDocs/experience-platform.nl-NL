---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;
solution: Experience Platform
title: Detailsvakgroep handel
description: Leer over de het schemagebiedgroep van de Details van de Handel.
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---

# [!UICONTROL Commerce Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Document weergeven op [veldgroepnaapupdates](../name-updates.md) voor meer informatie .

[!UICONTROL Commerce Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), gebruikt om handelsgegevens te beschrijven zoals productinformatie (SKU, naam, hoeveelheid), en standaard kartverrichtingen (orde, kassa, verlaten).

![](../../images/field-groups/commerce-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Een object dat productretourneert, garantieregistratie en processen voor winkelwagentjes/bestellingen beschrijft. |
| `productListItems` | Array van [Objecten in de productlijst](../../data-types/product-list-item.md) | Een lijst met items die de door een klant geselecteerde producten vertegenwoordigen, met specifieke opties en prijzen op een bepaald tijdstip (die kunnen verschillen van de productregistratie). |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
