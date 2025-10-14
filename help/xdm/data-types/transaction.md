---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;transactie;datatype;data-type;data-type;
title: Gegevenstype transactie
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Transactie (XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 1%

---

# [!UICONTROL Transaction] gegevenstype

[!UICONTROL Transaction] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat de details van een monetaire transactie beschrijft.

![&#x200B; structuur van de Transactie &#x200B;](../images/data-types/transaction.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Currency]](./currency.md) | Beschrijft het bedrag van valuta die als onderdeel van de transactie wordt geruild. |
| `transactionDate` | [!UICONTROL DateTime] | Een tijdstempel van wanneer de transactie heeft plaatsgevonden. |
| `transactionId` | [!UICONTROL String] | Een unieke id voor de transactie. |
| `transactionType` | [!UICONTROL String] | Het type transactie dat door de bezoeker wordt gebruikt. |

{style="table-layout:auto"}
