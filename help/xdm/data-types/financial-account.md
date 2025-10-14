---
title: Gegevenstype financiële rekening
description: Meer informatie over het XDM-gegevenstype van de financiële account.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 1%

---

# [!UICONTROL Financial Account] gegevenstype

[!UICONTROL Financial Account] is een standaard XDM gegevenstype dat de details van een financiële rekening met inbegrip van zijn type, eigenaar, en huidig saldo beschrijft.

![](../images/data-types/financial-account.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Currency]](./currency.md) | The current balance of the account. |
| `financialAccountId` | [!UICONTROL String] | Een unieke id voor het account. |
| `financialAccountName` | [!UICONTROL String] | De naam die aan de account is toegewezen. |
| `financialAccountType` | [!UICONTROL String] | Het type financiële rekening, zoals controle, spaargeld of pensionering. |

{style="table-layout:auto"}

Voor meer details op het gegevenstype, verwijs naar de [&#x200B; openbare bewaarplaats XDM &#x200B;](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
