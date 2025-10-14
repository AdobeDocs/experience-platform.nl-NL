---
title: Gegevensmodel ERD in de gezondheidszorg
description: Bekijk een entiteitrelatiediagram (ERD) dat een gestandaardiseerd gegevensmodel voor de gezondheidszorgindustrie beschrijft. Dit gegevensmodel is compatibel met het gegevensmodel van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# [!UICONTROL Healthcare] industrie gegevensmodel ERD

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de gezondheidszorgindustrie. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

>[!NOTE]
>
>De ERD zoals beschreven is een aanbeveling voor hoe u uw gegevens moet modelleren voor deze branche-gebruikscase. Om van dit gegevensmodel in Experience Platform gebruik te maken, moet u de geadviseerde schema&#39;s en hun verhoudingen zelf construeren. Zie de gidsen bij het beheren van [&#x200B; schema&#39;s &#x200B;](../../ui/resources/schemas.md) en [&#x200B; verhoudingen &#x200B;](../../tutorials/relationship-ui.md) in UI voor meer informatie.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die binnen wordt getoond is gebaseerd op een onderliggende [&#x200B; Model van de Gegevens van de Ervaring (XDM) klasse &#x200B;](../composition.md#class).
* Velden die onder een bovenliggend veld zijn ingesprongen, vertegenwoordigen een onderliggend veld, of subveld, dat tot de veldgroep van het bovenliggende veld behoort.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![&#x200B; Een voorbeeld ERD voor een model van de de gezondheidszorgindustrie gegevens &#x200B;](../../images/industries/healthcare.png)

>[!NOTE]
>
>Elke entiteit bevat een veld &quot;_ID&quot;, dat het unieke tekenreekskenmerk (`_id`) voor de desbetreffende record of gebeurtenis vertegenwoordigt. Dit veld wordt gebruikt om de uniciteit van de afzonderlijke record of gebeurtenis te volgen, om te voorkomen dat gegevens worden herhaald en om die gegevens in downstreamdiensten op te zoeken. In sommige gevallen, `_id` kan a [&#x200B; Universally Unique Identifier (UUID) &#x200B;](https://tools.ietf.org/html/rfc4122) of [&#x200B; globally Unieke Identifier (GUID) &#x200B;](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0) zijn.<br><br> het is belangrijk om te onderscheiden dat **dit gebied geen identiteit met betrekking tot een individuele persoon** vertegenwoordigt, maar eerder het verslag van gegevens zelf. De gegevens van de identiteit met betrekking tot een persoon, een gebeurtenis, of een bedrijfsentiteit zouden aan [&#x200B; identiteitsgebieden &#x200B;](../composition.md#identity) moeten worden beperkt die door compatibele gebiedsgroepen in plaats daarvan worden verstrekt.

## [!UICONTROL Healthcare] gebruik gevallen

De volgende lijst schetst de geadviseerde klassen en de groepen van het schemagebied voor verscheidene gemeenschappelijke gevallen van het gezondheidszorggebruik.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| Verbeter de digitale verwerving en ervaring bij consumenten die op zoek zijn naar een verzekering. Voorbeelden zijn: <ul><li>Wanneer mensen tot een pagina toegang hebben die algemene informatie (zoals plannen, plannamen/rijen, medicaid, welzijnsprogramma&#39;s, etc.) bevat, begrijpen zij hun gedrag en wat zij zoeken om promotionele e-mails te verzenden of hen op derdeplatforms met advertenties te richten.</li><li>Wanneer mensen op zoek zijn naar hartgezondheid en vaccininformatie, sturen ze hun vaccingerelateerde informatie over hartgezondheid om merkbewustzijn te creëren of ze te vragen vaccins te plannen.</li></ul> | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li><li>Relatievatievelden zijn gemaakt tussen `planID` -kenmerken en -schema&#39;s die gebruikmaken van de [!UICONTROL Plan] -klasse.</li></ul></li><li>**[[!UICONTROL Payer]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Healthcare Plan Details]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Application Details]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Sitetool Details]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL &#x200B; Campaign Marketing Details]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Verhoog de digitale verwerving van patiënten door middel van gerichte advertenties op basis van eerdere online gedragsgegevens en gezondheidsgegevens. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provider]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Healthcare Provider]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Verbeteren van de inschrijving en het aanmaken van accounts in gezondheidsplannen door het volgen van de marketing van verzekeringen via verschillende kanalen, om te begrijpen hoe een klant informatie over een verzekeringsmaatschappij heeft gevonden. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Payer]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Healthcare Plan Details]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Vermijd het wegvallen van ziektekostenverzekeringen. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Healthcare Plan Details]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Verhoging van drugsinformatie aan aanbieders met DTC-advertenties (direct-to-customer). | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medication]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Healthcare medication]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |

