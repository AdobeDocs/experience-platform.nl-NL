---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;
solution: Experience Platform
title: Commerce Details-schema-veldgroep
description: Meer informatie over de veldgroep Commerce Details-schema.
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# [!UICONTROL Commerce Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [ de naamupdates van de gebiedsgroep ](../name-updates.md) voor meer informatie.

[!UICONTROL Commerce Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md), die wordt gebruikt om handelsgegevens zoals productinformatie (SKU, naam, hoeveelheid), en standaardkartverrichtingen (orde, controle, verlaten) te beschrijven.

![](../../images/field-groups/commerce-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `commerce` | [ Commerce ](../../data-types/commerce.md) | Een object dat productretourneert, garantieregistratie en processen voor winkelwagentjes/bestellingen beschrijft. |
| `productListItems` | Serie van [ de lijstpunten van het Product ](../../data-types/product-list-item.md) | Een lijst met items die de door een klant geselecteerde producten vertegenwoordigen, met specifieke opties en prijzen op een bepaald tijdstip (die kunnen verschillen van de productregistratie). |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
