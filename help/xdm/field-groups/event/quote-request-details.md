---
title: Veld groep veld Aanvraag details offerte
description: Leer over de het schemagebiedgroep van de Details van het Verzoek van het Citaat.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# [!UICONTROL Quote Request Details] schemaveldgroep

[!UICONTROL Quote Request Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). De veldgroep bevat één `quotes` bezwaar aan een schema, dat de details van het verzoekproces voor diverse types van citaten, met inbegrip van verzekeringspolissen, gezondheidszorg, productiebevelen, en high-tech orden vangt.

![](../../images/field-groups/quote-request-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `discount` | [[!UICONTROL Currency]](../../data-types/currency.md) | Het kortingsbedrag voor een prijsopgave dat aan een bezoeker wordt weergegeven. |
| `premium` | [[!UICONTROL Currency]](../../data-types/currency.md) | Het premiebedrag voor een citaat dat aan een bezoeker wordt getoond. |
| `location` | [!UICONTROL String] | De postcode die wordt gebruikt voor het zoeken van detailhandelaren bij de locatie van de bezoeker. |
| `requestID` | [!UICONTROL String] | Een unieke id voor de aanhalingsaanvraag. |
| `selectedRetailer` | [!UICONTROL String] | De geselecteerde detailhandelaar voor het citaatverzoek, indien van toepassing. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
