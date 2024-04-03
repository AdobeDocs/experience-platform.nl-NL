---
title: Aangepaste metagegevens met gegevenrapportage gegevenstype
description: Meer informatie over het gegevenstype Custom Metadata Details Reporting Experience Data Model (XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# [!UICONTROL Custom Metadata Details] Gegevenstype rapporteren

[!UICONTROL Custom Metadata Details] Rapportering is een standaard XDM-gegevenstype (Experience Data Model) dat een structuur definieert voor het opslaan van aangepaste metagegevens. De [!UICONTROL Custom Metadata Details] Bij het rapporteren van het gegevenstype worden details vastgelegd, zoals de naam en waarde van aangepaste metagegevens die zijn gekoppeld aan inhoud of interacties. Media-rapportvelden worden door Adobe-services gebruikt voor het analyseren van de velden voor de verzameling van media die door gebruikers worden verzonden. Deze gegevens worden, samen met andere specifieke maatstaven voor gebruikers, berekend en gerapporteerd.

![Een diagram van het gegevenstype Custom Metadata Details Reporting.](../images/data-types/the-custom-metadata-reporting.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Custom Metadata Field Name] | `name` | string | De naam van het aangepaste veld. |
| [!UICONTROL Custom Metadata Field Value] | `value` | string | De waarde van het aangepaste veld. |

{style="table-layout:auto"}
