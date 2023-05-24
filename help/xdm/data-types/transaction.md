---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;transactie;datatype;data-type;data-type;
title: Gegevenstype transactie
description: Dit document verstrekt een overzicht van het gegevenstype van het Model van de Gegevens van de Ervaring van de Transactie (XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 1%

---

# [!UICONTROL Transaction] gegevenstype

[!UICONTROL Transaction] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat de details van een monetaire transactie beschrijft.

![Transactiestructuur](../images/data-types/transaction.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Currency]](./currency.md) | Beschrijft het bedrag van de omgewisselde valuta als onderdeel van de transactie. |
| `transactionDate` | [!UICONTROL DateTime] | Een tijdstempel van wanneer de transactie heeft plaatsgevonden. |
| `transactionId` | [!UICONTROL String] | Een unieke id voor de transactie. |
| `transactionType` | [!UICONTROL String] | Het type transactie dat door de bezoeker wordt gebruikt. |

{style="table-layout:auto"}
