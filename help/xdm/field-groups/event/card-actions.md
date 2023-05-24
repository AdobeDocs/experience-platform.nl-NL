---
title: Groep kaarthandelingen
description: Dit document biedt een overzicht van de veldgroep met het schema Kaarthandelingen.
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 2%

---

# [!UICONTROL Card Actions] schemaveldgroep

[!UICONTROL Card Actions] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). De veldgroep bevat één `personalFinances.cardActions` veld naar een schema, waarin details worden vastgelegd over een kaartactie, zoals het type kaart, de activeringsstatus en de vergrendelingsstatus.

![](../../images/field-groups/card-actions.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `cardActivated` | Geheel | Tracks wanneer de kaart is geactiveerd. |
| `cardActivationStart` | Geheel | Tracks when the card activation process is started. |
| `cardCancelled` | Geheel | Tracks wanneer een kaart is geannuleerd. |
| `cardControlsLocked` | Geheel | Tracks wanneer de besturingselementen van een kaart zijn vergrendeld. |
| `cardControlsUnlocked` | Geheel | Tracks wanneer de besturingselementen van een kaart zijn ontgrendeld. |
| `cardID` | Tekenreeks | De id van de kaart die wordt geactiveerd. Deze waarde kan verschillen van het kaartnummer. |
| `cardLocked` | Geheel | Tracks wanneer een kaart is vergrendeld. |
| `cardOrderNew` | Geheel | Tracks wanneer een kaart is aangevraagd. |
| `cardOrderType` | Tekenreeks | Het type kaartorder dat aan een kaartordergebeurtenis is gekoppeld. |
| `cardType` | Tekenreeks | Het type kaart. |
| `cardUnlocked` | Geheel | Tracks wanneer een kaart is ontgrendeld. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
