---
title: Gegevenstype financiële rekening
description: Dit document biedt een overzicht van het XDM-gegevenstype van de Financiële Rekening.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '95'
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

Voor meer details over het gegevenstype raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
