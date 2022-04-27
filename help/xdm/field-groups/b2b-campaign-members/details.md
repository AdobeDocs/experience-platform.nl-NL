---
title: XDM Business Campaign Member Details Schema Field Group
description: Dit document verstrekt een overzicht van de XDM Business Campagne het schemagebiedgroep van de Gegevens van het Lid van de Campagne.
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# [!UICONTROL XDM Business Campaign Member Details] schemaveldgroep

[!UICONTROL XDM Business Campaign Member Details] is een standaardschemagebiedgroep voor [[!UICONTROL XDM Business Campaign Members] class](../../classes/b2b/business-campaign-members.md), waarin gedetailleerde informatie over een zakelijke campagne wordt vastgelegd.

![De structuur van de XDM Business Campaign Member Details gebiedsgroep zoals deze in UI wordt weergegeven](../../images/field-groups/b2b/business-campaign-member-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | De samengestelde id van de campagne die dit campagnerelid heeft aangeschaft. |
| `acquiredByCampaignID` | [!UICONTROL String] | Een tekenreeks-id voor de campagne die dit campagnerelid heeft opgehaald. |
| `firstRespondedDate` | [!UICONTROL DateTime] | Een tijdstempel van ISO 8601 van wanneer de persoon voor het eerst op de campagne heeft gereageerd. |
| `hasReachedSuccess` | [!UICONTROL Boolean] | Geeft aan of dit campagnerelid heeft geresulteerd in een geslaagde conversie. |
| `hasResponded` | [!UICONTROL Boolean] | Geeft aan of dit campagnerelid op de campagne heeft gereageerd. |
| `isDeleted` | [!UICONTROL Boolean] | Geeft aan of dit campagnerelid is verwijderd in Marketo Engage.<br><br>Wanneer u de [Marketo-bronaansluiting](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden alle records die in Marketo worden verwijderd, automatisch weergegeven in het realtime profiel van de klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door in te stellen `isDeleted` tot `true`, kunt u het gebied gebruiken om uit te filteren welke verslagen uit uw bronnen zijn geschrapt wanneer het vragen van het meer van Gegevens. |
| `isExhausted` | [!UICONTROL Boolean] | Geeft aan of dit campagnerelid alle campagneinteracties heeft voltooid. |
| `lastStatus` | [!UICONTROL String] | De laatste status voor het campagnelid. |
| `memberStatus` | [!UICONTROL String] | De huidige status voor het campagnelid. |
| `memberStatusReason` | [!UICONTROL String] | De reden achter de huidige status voor het campagnelid. |
| `membershipDate` | [!UICONTROL DateTime] | De reden achter de huidige status voor het campagnelid. |
| `nurtureCadence` | [!UICONTROL String] | De tijdsduur voor campagnegerelateerde informatie die aan het campagnelid moet worden voorgelegd. |
| `nurtureTrackName` | [!UICONTROL String] | De naam van het programma voor de verzorging waaraan dit campagnelid is onderworpen. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | Een tijdstempel van ISO 8601 voor het tijdstip waarop de conversie is gelukt voor het campagelid. |
| `webinarConfirmationUrl` | [!UICONTROL String] | De URL voor bevestiging via het webinar voor het lid van de campagne. |
| `webinarRegistrationID` | [!UICONTROL String] | De webinar-registratie-id voor het campagnetelid. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
