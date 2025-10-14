---
title: Health Care Plan Details Schema Veld Groep
description: Leer over de het schemagebiedgroep van Details van het Plan van de Gezondheid.
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# [!UICONTROL Healthcare Plan Details] schemaveldgroep

[!UICONTROL Healthcare Plan Details] is een standaardgroep van het schemagebied voor de [[!UICONTROL Plan] klasse &#x200B;](../../classes/plan.md). Het verstrekt één enkel voorwerp-type gebied `healthcarePlanDetails` dat eigenschappen met betrekking tot een medisch plan vangt.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `networkDetails` | Array van objecten | Vermeldt de gegevens van het (de) door de verzekeraar gedefinieerde netwerk(en) van dienstverrichters waaraan de begunstigde een behandeling kan aanvragen, en zal worden gedekt tegen het &quot;in-network&quot;-tarief. Elk object bevat de volgende eigenschappen: <ul><li>`networkID`: (Tekenreeks) De verzekeraar-specifieke id voor het netwerk.</li><li>`networkName`: (String) De verzekeraarspecifieke naam voor het netwerk.</li></ul> |
| `affiliations` | Array van tekenreeksen | Een lijst van met de regeling verbonden bedrijfsentiteiten. |
| `coverageType` | String | Het type van de plandekking. Accepteerde waarden zijn:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Boolean | Geeft aan of het abonnement actief is. |
| `lastVerificationDate` | DateTime | De datum waarop het plan voor het laatst is geverifieerd. |
| `payerID` | String | De unieke identificatiecode voor de betaler (met andere woorden de verzekeringsaanbieder voor de regeling). |
| `planLevel` | String | Geeft het planniveau aan. Accepteerde waarden zijn:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | String | Geeft het overzichtstype aan. Accepteerde waarden zijn:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | String | Het type eigenaar waarvoor een abonnement is bedoeld. Voorbeelden zijn individu, groep, organisatie, enzovoort. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [&#x200B; openbare bewaarplaats XDM &#x200B;](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
