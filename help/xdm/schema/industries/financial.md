---
solution: Experience Platform
title: Gegevensmodel financiële dienstverlening ERD
description: Bekijk een entiteitsrelatiediagram (ERD) dat een gestandaardiseerd gegevensmodel beschrijft voor de bank-, financiële diensten- en verzekeringssector. Dit gegevensmodel is compatibel met het gegevensmodel van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# [!UICONTROL Financial services] industrie gegevensmodel ERD

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de banksector, de financiële sector en de verzekeringssector (BFSI). De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

>[!NOTE]
>
>De ERD zoals beschreven is een aanbeveling voor hoe u uw gegevens moet modelleren voor deze branche-gebruikscase. Om van dit gegevensmodel in Experience Platform gebruik te maken, moet u de geadviseerde schema&#39;s en hun verhoudingen zelf construeren. Zie de gidsen bij het beheren van [ schema&#39;s ](../../ui/resources/schemas.md) en [ verhoudingen ](../../tutorials/relationship-ui.md) in UI voor meer informatie.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die binnen wordt getoond is gebaseerd op een onderliggende [ Model van de Gegevens van de Ervaring (XDM) klasse ](../composition.md#class).
* Velden die onder een bovenliggend veld zijn ingesprongen, vertegenwoordigen een onderliggend veld, of subveld, dat tot de veldgroep van het bovenliggende veld behoort.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![ Een voorbeeld ERD voor een model van de financiële industrie gegevens ](../../images/industries/financial.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat het unieke id-kenmerk (`_id`) vertegenwoordigt dat door de XDM ExperienceEvent-klasse wordt verschaft. Zie het verwijzingsdocument op [ XDM ExperienceEvent ](../../classes/experienceevent.md) voor meer details over wat voor deze waarde wordt verwacht.

## [!UICONTROL Financial services] gebruik gevallen

In de volgende tabel worden de aanbevolen klassen en schemaveldgroepen voor verschillende algemene gevallen van financieel gebruik beschreven.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| De personalisering van de aandrijving bij schaal voor aangewezen segmenten door omnichannel rapporterend inzicht en automatiseren reizen om inschrijving aan een aangewezen beloningsprogramma te verhogen. | <ul><li>**[[!UICONTROL Product]](../../classes/product.md)** :<ul><li>[[!UICONTROL Product Category]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Card Actions]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Quote Request Details]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Deposit Details]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Channel Details]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Balance Transfers]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Loyalty Details]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Optimaliseer kanaalpersonalisatie over online en off-line kanalen. | <ul><li>**[[!UICONTROL Product]](../../classes/product.md)**:<ul><li>[[!UICONTROL Product Category]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Channel Details]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Loyalty Details]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Nieuwe inkomstenmogelijkheden stimuleren door gebruik te maken van inzichten die zijn opgedaan bij de analyse van gedrag over meerdere kanalen, door patronen van productgebruik te identificeren die tot nieuwe productaanbiedingen kunnen leiden. | <ul><li>**[[!UICONTROL Policy]](../../classes/policy.md)**</li><li>**[[!UICONTROL Product]](../../classes/product.md)**:<ul><li>[[!UICONTROL Product Category]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Card Actions]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Support Site Search]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Deposit Details]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Channel Details]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Demographic Details]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Personal Contact Details]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Loyalty Details]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
