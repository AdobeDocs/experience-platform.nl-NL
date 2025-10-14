---
title: Gegevenstype voor Media-gebeurtenis
description: Meer informatie over het gegevenstype Data Model (XDM) van het Media Event Information Experience.
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 1%

---

# [!UICONTROL Media Event Information] gegevenstype

[!UICONTROL Media Event Information] is een standaard XDM-gegevenstype (Experience Data Model) waarmee mediadetails-informatie over de ervaringsgebeurtenis worden beschreven.

![&#x200B; een diagram van het gegevenstype van de Informatie van de Gebeurtenis van Media.](../images/data-types/media-event-information.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | Informatie over mediagegevens met betrekking tot de ervaringsgebeurtenis. Dit gegevenstype wordt gebruikt voor zowel [&#x200B; media gegevensinzameling &#x200B;](./media-collection-details.md) als [&#x200B; media gegevens die &#x200B;](./media-reporting-details.md) melden. |
| `mediaEventTimestamp` | [!UICONTROL String] | Het tijdstip waarop een mediagebeurtenis heeft plaatsgevonden. |
| `mediaEventType` | [!UICONTROL String] | Het type media-gebeurtenis. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [&#x200B; openbare bewaarplaats XDM &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
