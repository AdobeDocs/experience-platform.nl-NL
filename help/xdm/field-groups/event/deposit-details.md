---
title: Veldgroep aanbetalingsgegevens
description: Dit document bevat een overzicht van de veldgroep van het schema Aanbetalingsgegevens.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# [!UICONTROL Deposit Details] schemaveldgroep

[!UICONTROL Deposit Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). De veldgroep bevat één `personalFinances.deposits` veld naar een schema waarin details over een financiële aanbetaling worden vastgelegd.

![](../../images/field-groups/deposit-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `account` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beschrijft de financiële rekening verbonden aan het deposito. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Beschrijft de financiële transactie verbonden aan het deposito. |
| `mobileDeposit` | [!UICONTROL Boolean] | Geeft aan of de aanbetaling is uitgevoerd via een mobiel platform. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
