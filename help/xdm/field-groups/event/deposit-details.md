---
title: Veldgroep aanbetalingsgegevens
description: Meer informatie over de veldgroep van het schema voor aanbetalingsgegevens.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 1%

---

# [!UICONTROL Deposit Details] schemaveldgroep

[!UICONTROL Deposit Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). De veldgroep bevat één `personalFinances.deposits` veld naar een schema waarin details over een financiële aanbetaling worden vastgelegd.

![](../../images/field-groups/deposit-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `account` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beschrijft de financiële rekening verbonden aan het deposito. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Beschrijft de financiële transactie verbonden aan het deposito. |
| `mobileDeposit` | [!UICONTROL Boolean] | Geeft aan of de aanbetaling is uitgevoerd via een mobiel platform. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
