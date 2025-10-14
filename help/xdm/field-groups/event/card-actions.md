---
title: Groep kaarthandelingen in schema
description: Meer informatie over de veldgroep kaarthandelingen.
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# [!UICONTROL Card Actions] schemaveldgroep

[!UICONTROL Card Actions] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse &#x200B;](../../classes/experienceevent.md). De veldgroep verschaft één `personalFinances.cardActions` -veld voor een schema waarin details worden vastgelegd over een kaartactie, zoals het type kaart, de activeringsstatus en de vergrendelingsstatus.

![](../../images/field-groups/card-actions.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `cardActivated` | Geheel | Tracks wanneer de kaart is geactiveerd. |
| `cardActivationStart` | Geheel | Tracks when the card activation process is started. |
| `cardCancelled` | Geheel | Tracks wanneer een kaart is geannuleerd. |
| `cardControlsLocked` | Geheel | Tracks wanneer de controles van een kaart zijn gesloten. |
| `cardControlsUnlocked` | Geheel | Tracks wanneer de besturingselementen van een kaart zijn ontgrendeld. |
| `cardID` | String | De id van de kaart die wordt geactiveerd. Deze waarde kan verschillen van het kaartnummer. |
| `cardLocked` | Geheel | Tracks wanneer een kaart is vergrendeld. |
| `cardOrderNew` | Geheel | Tracks wanneer een kaart is aangevraagd. |
| `cardOrderType` | String | Het type kaartorder dat aan een kaartordergebeurtenis is gekoppeld. |
| `cardType` | String | Het type kaart. |
| `cardUnlocked` | Geheel | Tracks wanneer een kaart is ontgrendeld. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [&#x200B; openbare bewaarplaats XDM &#x200B;](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
