---
title: Balans van groep van het schemaveld
description: Dit document biedt een overzicht van de veldgroep Balansoverdrachten.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '107'
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

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
