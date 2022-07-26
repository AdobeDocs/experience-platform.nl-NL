---
title: Gegevensmodel ERD in de gezondheidszorg
description: Bekijk een entiteitrelatiediagram (ERD) dat een gestandaardiseerd gegevensmodel voor de gezondheidszorgindustrie beschrijft. Dit gegevensmodel is compatibel met Experience Data Model (XDM) voor gebruik in Adobe Experience Platform.
source-git-commit: 721059a87347e371228d00edeac141afa894af47
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# [!UICONTROL Healthcare] bedrijfsgegevensmodel ERD

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de gezondheidszorgindustrie. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

>[!NOTE]
>
>De ERD zoals beschreven is een aanbeveling voor hoe u uw gegevens moet modelleren voor deze branche-gebruikscase. Om van dit gegevensmodel in Platform gebruik te maken, moet u de geadviseerde schema&#39;s en hun verhoudingen zelf construeren. Zie de handleidingen over het beheer [schema&#39;s](../../ui/resources/schemas.md) en [relaties](../../tutorials/relationship-ui.md) in UI voor meer informatie.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die wordt vermeld in is gebaseerd op een onderliggende waarde [Experience Data Model (XDM)-klasse](../composition.md#class).
* Voor een bepaalde entiteit wordt elke in **vet** vertegenwoordigt een veldgroep of een gegevenstype, waarvan de relevante velden hieronder in onbolde tekst worden vermeld.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![Afbeelding die het entiteitrelatiediagram voor het gegevensmodel van de gezondheidszorgindustrie weergeeft](../../images/industries/healthcare.png)

>[!NOTE]
>
>Elke entiteit bevat een veld &quot;_ID&quot; dat de unieke tekenreeks-id vertegenwoordigt (`_id`) voor de betreffende record of gebeurtenis. Dit veld wordt gebruikt om de uniciteit van de afzonderlijke record of gebeurtenis te volgen, om te voorkomen dat gegevens worden herhaald en om die gegevens in downstreamdiensten op te zoeken. In sommige gevallen `_id` kan [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) of [Globally Unique Identifier (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Het is van belang te onderscheiden dat **dit veld vertegenwoordigt geen identiteit die betrekking heeft op een individuele persoon**, maar eerder de gegevensregistratie zelf. Identiteitsgegevens met betrekking tot een persoon, een gebeurtenis of een bedrijfsentiteit moeten worden beperkt tot [identiteitsvelden](../composition.md#identity) in plaats daarvan worden verstrekt door compatibele veldgroepen.

## [!UICONTROL Healthcare] use cases

De volgende lijst schetst de geadviseerde klassen en de groepen van het schemagebied voor verscheidene gemeenschappelijke gevallen van het gezondheidszorggebruik.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| Verbeter de digitale verwerving en ervaring bij consumenten die op zoek zijn naar een verzekering. Voorbeelden zijn: <ul><li>Wanneer mensen tot een pagina toegang hebben die algemene informatie (zoals plannen, plannamen/rijen, medicaid, welzijnsprogramma&#39;s, etc.) bevat, begrijpen zij hun gedrag en wat zij zoeken om promotionele e-mails te verzenden of hen op derdeplatforms met advertenties te richten.</li><li>Wanneer mensen op zoek zijn naar hartgezondheid en vaccininformatie, sturen ze hun vaccingerelateerde informatie over hartgezondheid om merkbewustzijn te creëren of ze te vragen vaccins te plannen.</li></ul> | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li><li>Relatie-veld(en) vastgesteld tussen `planID` kenmerken en schema&#39;s die gebruikmaken van de [!UICONTROL Plan] klasse.</li></ul></li><li>**[[!UICONTROL Payer]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Healthcare Plan Details]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Application Details]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Sitetool Details]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  Campaign Marketing Details]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Verhoog de digitale verwerving van patiënten door middel van gerichte advertenties op basis van eerdere online gedragsgegevens en gezondheidsgegevens. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provider]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Healthcare Provider]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Verbeteren van de inschrijving en het aanmaken van accounts in gezondheidsplannen door het volgen van de marketing van verzekeringen via verschillende kanalen, om te begrijpen hoe een klant informatie over een verzekeringsmaatschappij heeft gevonden. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Payer]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Healthcare Plan Details]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Vermijd het wegvallen van ziektekostenverzekeringen. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plan]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Healthcare Plan Details]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Verhoging van drugsinformatie aan aanbieders met DTC-advertenties (direct-to-customer). | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Healthcare Member Details]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medication]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Healthcare medication]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web Details]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Advertising Details]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
