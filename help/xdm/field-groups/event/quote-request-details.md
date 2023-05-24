---
title: Veld groep velden wijzigingsverzoek
description: Dit document verstrekt een overzicht van de het schemagebiedgroep van de Details van het Verzoek van het Citaat.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# [!UICONTROL Quote Request Details] schemaveldgroep

[!UICONTROL Quote Request Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). De veldgroep bevat één `quotes` bezwaar aan een schema, dat de details van het verzoekproces voor diverse types van citaten, met inbegrip van verzekeringspolissen, gezondheidszorg, productiebevelen, en high-tech orden vangt.

![](../../images/field-groups/quote-request-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `discount` | [[!UICONTROL Currency]](../../data-types/currency.md) | Het kortingsbedrag voor een prijsopgave dat aan een bezoeker wordt weergegeven. |
| `premium` | [[!UICONTROL Currency]](../../data-types/currency.md) | Het premiebedrag voor een citaat dat aan een bezoeker wordt getoond. |
| `location` | [!UICONTROL String] | De postcode die wordt gebruikt voor het zoeken van detailhandelaren in de buurt van de locatie van de bezoeker. |
| `requestID` | [!UICONTROL String] | Een unieke id voor de aanhalingsaanvraag. |
| `selectedRetailer` | [!UICONTROL String] | De geselecteerde detailhandelaar voor het citaatverzoek, indien van toepassing. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
