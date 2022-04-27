---
title: XDM Business Campagne Details Schema Field Group
description: Dit document biedt een overzicht van de XDM Business Campagne Details schema veldgroep.
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# [!UICONTROL XDM Business Campaign Details] schemaveldgroep

[!UICONTROL XDM Business Campaign Details] is een standaardschemagebiedgroep voor [[!UICONTROL XDM Business Campaign] class](../../classes/b2b/business-campaign.md), waarin gedetailleerde informatie over een zakelijke campagne wordt vastgelegd.

![De structuur van de XDM Business Campagne Details gebiedsgroep zoals het in UI verschijnt](../../images/field-groups/b2b/business-campaign-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Currency]](../../data-types/currency.md) | Vertegenwoordigt de echte kosten van de bedrijfscampagne. |
| `budgetedCost` | [[!UICONTROL Currency]](../../data-types/currency.md) | Vertegenwoordigt de begrote kosten van de bedrijfscampagne. |
| `expectedRevenue` | [[!UICONTROL Currency]](../../data-types/currency.md) | Vertegenwoordigt de inkomsten die de bedrijfscampagne naar verwachting zal produceren. |
| `parentCampaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | De samengestelde id voor een bovenliggende campagne, indien van toepassing. |
| `campaignEndDate` | [!UICONTROL DateTime] | Een tijdstempel van ISO 8601 van wanneer de campagne is afgelopen of zal eindigen. |
| `campaignProgressionName` | [!UICONTROL String] | De naam van de campagneprogressie. |
| `campaignStartDate` | [!UICONTROL DateTime] | Een tijdstempel van ISO 8601 van wanneer de campagne is gestart of zal worden gestart. |
| `campaignStatus` | [!UICONTROL String] | De huidige status van de campagne. |
| `channelName` | [!UICONTROL String] | De naam van het kanaal dat aan deze campagne is gekoppeld. |
| `expectedResponse` | [!UICONTROL String] | De verwachte reactie voor de campagne. |
| `integrationPartnerName` | [!UICONTROL String] | De naam van de partner die met deze campagne is geïntegreerd. |
| `isActive` | [!UICONTROL Boolean] | Geeft aan of deze campagne actief is. |
| `isDeleted` | [!UICONTROL Boolean] | Geeft aan of deze campagne is verwijderd in Marketo Engage.<br><br>Wanneer u de [Marketo-bronaansluiting](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden alle records die in Marketo worden verwijderd, automatisch weergegeven in het realtime profiel van de klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door in te stellen `isDeleted` tot `true`, kunt u het gebied gebruiken om uit te filteren welke verslagen uit uw bronnen zijn geschrapt wanneer het vragen van het meer van Gegevens. |
| `lastActivityDate` | [!UICONTROL DateTime] | Een ISO 8601-tijdstempel van de laatste activiteit die aan de campagne is gekoppeld. |
| `timeZone` | [!UICONTROL String] | De tijdzone waarin de campagne wordt uitgevoerd. |
| `timeZoneDelivery` | [!UICONTROL String] | De tijdzone van de levering waarin de campagne werkt. |
| `timeZoneName` | [!UICONTROL String] | De naam van de tijdzone waarin de campagne wordt uitgevoerd. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Een tijdstempel van ISO 8601 van de laatste webinar historiesynchronisatie voor deze campagne. |
| `webinarHistorySyncStatus` | [!UICONTROL String] | De status van de webinar historiesynchronisatie voor deze campagne. |
| `webinarSessionDescription` | [!UICONTROL String] | Een beschrijving van de webinar zitting verbonden aan deze campagne. |
| `webinarSessionName` | [!UICONTROL String] | Een naam van de webinar zitting verbonden aan deze campagne. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
