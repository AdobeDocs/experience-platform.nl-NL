---
title: XDM Business Campagne Details Schema Field Group
description: Meer informatie over de XDM Business Campagne Details schema veldgroep.
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# [!UICONTROL XDM Business Campaign Details] schemaveldgroep

[!UICONTROL XDM Business Campaign Details] is een standaardgroep van het schemagebied voor de [[!UICONTROL XDM Business Campaign] klasse &#x200B;](../../classes/b2b/business-campaign.md), die gedetailleerde informatie over een bedrijfscampagne vangt.

![&#x200B; de structuur van de XDM het gebiedsgroep van Details Bedrijfs van de Campagne aangezien het in UI &#x200B;](../../images/field-groups/b2b/business-campaign-details.png) verschijnt

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
| `isDeleted` | [!UICONTROL Boolean] | Geeft aan of deze campagne is verwijderd uit het Marketo Engage.<br><br> wanneer het gebruiken van de [&#x200B; Marketo bronschakelaar &#x200B;](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden om het even welke verslagen die in Marketo worden geschrapt automatisch weerspiegeld in Real-Time Profiel van de Klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door `isDeleted` in te stellen op `true` , kunt u het veld gebruiken om uit te filteren welke records uit uw bronnen zijn verwijderd wanneer u een query uitvoert op het gegevensmeer. |
| `lastActivityDate` | [!UICONTROL DateTime] | Een ISO 8601-tijdstempel van de laatste activiteit die aan de campagne is gekoppeld. |
| `timeZone` | [!UICONTROL String] | De tijdzone waarin de campagne wordt uitgevoerd. |
| `timeZoneDelivery` | [!UICONTROL String] | De tijdzone van de levering waarin de campagne werkt. |
| `timeZoneName` | [!UICONTROL String] | De naam van de tijdzone waarin de campagne wordt uitgevoerd. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Een tijdstempel van ISO 8601 van de laatste webinar historiesynchronisatie voor deze campagne. |
| `webinarHistorySyncStatus` | [!UICONTROL String] | De status van de webinar historiesynchronisatie voor deze campagne. |
| `webinarSessionDescription` | [!UICONTROL String] | Een beschrijving van de webinar zitting verbonden aan deze campagne. |
| `webinarSessionName` | [!UICONTROL String] | Een naam van de webinar zitting verbonden aan deze campagne. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [&#x200B; openbare bewaarplaats XDM &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
