---
title: Balans van groep van het schemaveld
description: Dit document biedt een overzicht van de veldgroep Balansoverdrachten.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# [!UICONTROL Balance Transfers] schemaveldgroep

[!UICONTROL Balance Transfers] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). De veldgroep bevat één `personalFinances.balanceTransfers` object maken naar een schema dat details vastlegt over een overdracht van een financieel saldo tussen rekeningen.

![](../../images/field-groups/balance-transfers.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beschrijft de financiële rekening die het saldo van wordt overgebracht. |
| `accountTo` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beschrijft de financiële rekening die het saldo aan wordt overgebracht. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Beschrijft de financiële transactie die aan de saldooverdracht is gekoppeld. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
