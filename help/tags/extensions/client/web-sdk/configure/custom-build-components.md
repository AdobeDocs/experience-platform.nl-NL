---
title: Opties voor samenstellen
description: Maak een aangepaste Web SDK-build die functies uitschakelt om de buildgrootte te verlagen.
exl-id: 853e0a6c-0953-4e08-9a7d-334aab022583
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 1%

---

# Opties voor samenstellen {#build-options}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_buildoptions"
>title="Opties voor samenstellen"
>abstract="U kunt modules selectief opnemen in of uitsluiten van de JavaScript-bibliotheek, waardoor de bibliotheekgrootte afneemt en de prestaties verbeteren."

De bibliotheek van SDK van het Web omvat veelvoudige modules voor diverse eigenschappen zoals verpersoonlijking, identiteit, verbinding het volgen, en meer. Afhankelijk van uw gebruiksgevallen hebt u wellicht alleen specifieke functies nodig in plaats van de volledige bibliotheek. Als u de build-componenten uitschakelt, kunt u alleen de modules gebruiken die u nodig hebt, waardoor de bibliotheekgrootte afneemt en de prestaties verbeteren.

Wanneer u een component uitschakelt, kunt u de instellingen van die component niet meer bewerken. Als u veelvoudige instanties van SDK van het Web gebruikt, zijn de geselecteerde bouwstijlcomponenten op alle instanties van toepassing.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Vouw de accordeon **[!UICONTROL Custom build components]** bovenaan uit.

>[!WARNING]
>
>Onjuiste wijzigingen in deze instellingen kunnen ongewenste resultaten tot gevolg hebben, waaronder gegevensverlies. Test uw implementatie grondig in een ontwikkelomgeving voordat u deze wijzigingen in de productie publiceert.

Adobe biedt de mogelijkheid om de volgende Web SDK-bouwstijlcomponenten uit te schakelen:

| Component samenstellen | Beschrijving | Afhankelijke functies |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | Staat automatische verbindingsinzameling en het volgen van Activity Map toe. | |
| **[!UICONTROL Advertising]** | Maakt Adobe Advertising-integratie met Customer Journey Analytics mogelijk. | |
| **[!UICONTROL Audiences]** | Ondersteunt de integratie met Adobe Audience Manager, zoals ID-syncs. | |
| **[!UICONTROL Brand concierge]** | Maakt integratie met Brand concierge mogelijk. |
| **[!UICONTROL Consent]** | Hiermee kunt u toestemmingskenmerken gebruiken. | [[!UICONTROL Set consent]](../actions/set-consent.md) handeling |
| **[!UICONTROL Event merge]** | Vervangen. | [[!UICONTROL Event merge ID]](../data-element-types.md) data element (afgekeurd) <br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md) action (afgekeurd) |
| **[!UICONTROL Media Analytics bridge]** | Ondersteunt de integratie met verouderde Media Analytics. | [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md) handeling |
| **[!UICONTROL Personalization]** | Ondersteunt integratie met Adobe Target en Adobe Journey Optimizer. | [[!UICONTROL Apply propositions]](../actions/apply-propositions.md) handeling |
| **[!UICONTROL Push notifications]** | Hiermee schakelt u webpushberichten voor Adobe Journey Optimizer in. | [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md) handeling |
| **[!UICONTROL Rules engine]** | Maakt apparaatbeslissingen mogelijk met Adobe Journey Optimizer. | [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md) action <br> [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items) -gebeurtenis |
| **[!UICONTROL Streaming media]** | Ondersteunt de integratie met streaming media collection. | [[!UICONTROL Send media event]](../actions/send-media-event.md) handeling |
