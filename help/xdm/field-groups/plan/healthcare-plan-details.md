---
title: Health Care Plan Details Schema Veld Groep
description: Dit document biedt een overzicht van de veldgroep Details schema van het zorgplan.
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---

# [!UICONTROL Healthcare Plan Details] schemaveldgroep

[!UICONTROL Healthcare Plan Details] is een standaardschemagebiedgroep voor [[!UICONTROL Plan] class](../../classes/plan.md). Het biedt één veld van het objecttype `healthcarePlanDetails` die eigenschappen met betrekking tot een medisch plan vastleggen.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `networkDetails` | Array van objecten | Vermeldt de gegevens van het (de) door de verzekeraar gedefinieerde netwerk(en) van dienstverrichters waaraan de begunstigde een behandeling kan aanvragen, en zal worden gedekt tegen het &quot;in-network&quot;-tarief. Elk object bevat de volgende eigenschappen: <ul><li>`networkID`: (Tekenreeks) De verzekeraar-specifieke id voor het netwerk.</li><li>`networkName`: (Tekenreeks) De verzekeraarspecifieke naam voor het netwerk.</li></ul> |
| `affiliations` | Array van tekenreeksen | Een lijst van met de regeling verbonden bedrijfsentiteiten. |
| `coverageType` | Tekenreeks | Het type van de plandekking. Accepteerde waarden zijn:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Boolean | Geeft aan of het abonnement actief is. |
| `lastVerificationDate` | DateTime | De datum waarop het plan voor het laatst is geverifieerd. |
| `payerID` | Tekenreeks | De unieke identificatiecode voor de betaler (met andere woorden de verzekeringsaanbieder voor de regeling). |
| `planLevel` | Tekenreeks | Geeft het planniveau aan. Accepteerde waarden zijn:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | Tekenreeks | Geeft het overzichtstype aan. Accepteerde waarden zijn:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | Tekenreeks | Het type eigenaar waarvoor een abonnement is bedoeld. Voorbeelden zijn individu, groep, organisatie, enzovoort. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
