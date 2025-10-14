---
title: Aangepaste metagegevens met gegevenrapportage gegevenstype
description: Meer informatie over het gegevenstype Custom Metadata Details Reporting Experience Data Model (XDM).
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# [!UICONTROL Custom Metadata Details] Gegevenstype rapporteren

[!UICONTROL Custom Metadata Details] Rapportering is een standaard XDM-gegevenstype (Experience Data Model) waarmee een structuur wordt gedefinieerd voor het opslaan van aangepaste metagegevens. In het gegevenstype [!UICONTROL Custom Metadata Details] Reporting worden gegevens vastgelegd, zoals de naam en waarde van aangepaste metagegevens die zijn gekoppeld aan inhoud of interacties. Media-rapportvelden worden door Adobe-services gebruikt voor het analyseren van de velden voor de verzameling van media die door gebruikers worden verzonden. Deze gegevens worden, samen met andere specifieke maatstaven voor gebruikers, berekend en gerapporteerd.

![&#x200B; A diagram van de Details die van Meta-gegevens van de Douane gegevenstype melden.](../images/data-types/the-custom-metadata-reporting.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Custom Metadata Field Name] | `name` | string | De naam van het aangepaste veld. |
| [!UICONTROL Custom Metadata Field Value] | `value` | string | De waarde van het aangepaste veld. |

{style="table-layout:auto"}
