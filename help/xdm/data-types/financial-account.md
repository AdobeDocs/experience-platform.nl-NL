---
title: Gegevenstype financiële rekening
description: Dit document biedt een overzicht van het XDM-gegevenstype van de Financiële Rekening.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '98'
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

{style=&quot;table-layout:auto&quot;}

Voor meer details over het gegevenstype raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
