---
solution: Experience Platform
title: Gegevensmodel telecommunicatiesector ERD
description: Bekijk een diagram van de entiteitverhouding (ERD) dat een gestandaardiseerd gegevensmodel voor de telecommunicatiesector beschrijft, compatibel met het Model van de Gegevens van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# [!UICONTROL Telecommunications] bedrijfsgegevensmodel ERD

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de telecomindustrie. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

>[!NOTE]
>
>De ERD zoals beschreven is een aanbeveling voor hoe u uw gegevens moet modelleren voor deze branche-gebruikscase. Om van dit gegevensmodel in Platform gebruik te maken, moet u de geadviseerde schema&#39;s en hun verhoudingen zelf construeren. Zie de handleidingen over het beheer [schema&#39;s](../../ui/resources/schemas.md) en [relaties](../../tutorials/relationship-ui.md) in UI voor meer informatie.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die wordt vermeld in is gebaseerd op een onderliggende waarde [Experience Data Model (XDM)-klasse](../composition.md#class).
* Voor een bepaalde entiteit wordt elke in **vet** vertegenwoordigt een veldgroep of een gegevenstype, waarvan de relevante velden hieronder in onbolde tekst worden vermeld.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat de unieke id vertegenwoordigt (`_id`), opgegeven door de klasse XDM ExperienceEvent. Zie het referentiedocument op [XDM ExperienceEvent](../../classes/experienceevent.md) voor meer informatie over wat er voor deze waarde wordt verwacht.

## [!UICONTROL Telecommunications] use cases

De volgende lijst schetst de geadviseerde klassen en groepen van het schemagebied voor verscheidene gemeenschappelijke gebruiksgevallen voor de telecomindustrie.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| Begrijp klanten die goede kandidaten voor upsell of cross-sell kansen zijn die op hun huidige bezit en hun het browsen gedrag worden gebaseerd. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Upsell Details]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Upgrade Details]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telecom Subscription]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Retarget winkelwagentje verlaat de betreffende advertenties en geautomatiseerde persoonlijke e-mails. Advertenties onderdrukken wanneer ze worden omgezet. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Commerce Details]](../../field-groups/event/upsell-details.md) (Ophalen van winkels met winkelwagentjes)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Telecom Subscription]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Wanneer een klant is gemarkeerd als een klant die waarschijnlijk zal klappen (op basis van een werknemersinteractie of een geautomatiseerd machine-learningalgoritme), stuurt u de klantgegevens naar digitale en niet-digitale kanalen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Campaign Marketing Details]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Channel Details]](../../field-groups/event/channel-details.md)</li><li>Een aangepaste veldgroep met gepersonaliseerde inhoud</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
