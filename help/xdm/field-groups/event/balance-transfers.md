---
title: Balans van groep van het schemaveld
description: Leer over de het schemagebiedgroep van de Overdracht van het Saldo.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# [!UICONTROL Balance Transfers] schemaveldgroep

[!UICONTROL Balance Transfers] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse &#x200B;](../../classes/experienceevent.md). De veldgroep biedt één `personalFinances.balanceTransfers` -object aan een schema, waarin details worden vastgelegd over een overdracht van een financiële balans tussen accounts.

![](../../images/field-groups/balance-transfers.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beschrijft de financiële rekening die het saldo van wordt overgebracht. |
| `accountTo` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beschrijft de financiële rekening die het saldo aan wordt overgebracht. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Beschrijft de financiële transactie die aan de saldooverdracht is gekoppeld. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [&#x200B; openbare bewaarplaats XDM &#x200B;](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
