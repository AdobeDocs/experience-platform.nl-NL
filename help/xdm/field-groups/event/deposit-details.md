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

[!UICONTROL Deposit Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse &#x200B;](../../classes/experienceevent.md). De veldgroep verschaft één `personalFinances.deposits` -veld voor een schema waarin details over een financiële aanbetaling worden vastgelegd.

![](../../images/field-groups/deposit-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `account` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beschrijft de financiële rekening verbonden aan het deposito. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Beschrijft de financiële transactie verbonden aan het deposito. |
| `mobileDeposit` | [!UICONTROL Boolean] | Geeft aan of de aanbetaling is uitgevoerd via een mobiel platform. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [&#x200B; openbare bewaarplaats XDM &#x200B;](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
