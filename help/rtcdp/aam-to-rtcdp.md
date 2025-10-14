---
title: Evolutie van Audience Manager naar Real-Time CDP
description: Begrijp de overwegingen alvorens uw migratie van Audience Manager aan Adobe Real-Time CDP te plannen.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# Evolutie van Audience Manager naar Real-Time CDP

Naarmate uw organisatie zich ontwikkelt om Adobe Real-Time CDP te gebruiken, verkent u deze overwegingen om uw gegevens voor te bereiden en zich bewust te worden van de kritieke verschillen tussen de twee technologieën. Dit artikel is gericht op een beoefenaar van een beroep.

![&#x200B; Audience Manager aan Real-Time CDP evolutiediagram &#x200B;](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Overweeg gegevensarchitectuur binnen Audience Manager

Aangezien u de evolutie van Audience Manager aan Real-Time CDP overweegt, is nu een kritieke tijd om uw [&#x200B; segmenten van de Audience Manager &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=nl-NL) te analyseren en te bepalen wat de [&#x200B; signalen &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=nl-NL), [&#x200B; trekken &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=nl-NL), en [&#x200B; regels &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=nl-NL#segment-builder-section) zijn die omhoog die segmenten maken.

Overweeg bovendien de gegevensbronnen die u momenteel in de Audience Manager gebruikt.

Adobe raadt u aan de segmenten als volgt te categoriseren:

* De segmenten die via [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md) naar Experience Platform kunnen worden verzonden, aangezien zij geen gegevensgebiedsdelen, geen bestemming of activeringsuitdagingen hebben, en hun segmenteringsregels kunnen door Real-Time CDP [&#x200B; segmentbouwer &#x200B;](/help/segmentation/ui/segment-builder.md) later worden gecreeerd.
* Segmenten met regels die kunnen worden ondersteund, maar die gegevens bevatten die niet beschikbaar zijn in Real-Time CDP.
* Segmenten die niet in Real-Time CDP kunnen worden gemaakt en geen functionaliteit hebben.

>[!TIP]
>
>Adobe Real-Time CDP biedt [&#x200B; drie soorten segmentevaluatie &#x200B;](/help/segmentation/home.md#evaluate-segments) aan: [!UICONTROL Batch], [!UICONTROL Streaming], en [!UICONTROL Edge]. Klanten die realtime segmenten in de Audience Manager gebruiken, kunnen worden beperkt door de huidige beperking van 500 streaming segmenten in Real-Time CDP. Lees meer over [&#x200B; segmentatiegeleidingen &#x200B;](/help/profile/guardrails.md).

## 2. Welke segmenten zijn van essentieel belang om door te sturen via [!UICONTROL Audience Manager Source Connector]?

Gebaseerd op hun evaluatiecriteria, zouden de segmenten die geen gegevensgebiedsdelen, geen bestemming of activeringsuitdagingen hebben, en hun segmentatieregels door de gegevensinzameling van Real-Time CDP zoals [&#128279;](/help/web-sdk/faq.md) kunnen worden gecreeerd van het Web SDK van 0&rbrace; Adobe Experience Platform op een recentere datum door de Schakelaar van Source van de Audience Manager zouden moeten worden verzonden.

## 3. Gebruikt u het doel [!UICONTROL Experience Cloud Audiences] om gegevens terug te brengen naar de Audience Manager?

De segmenten die regels hebben die in Real-Time CDP kunnen worden gesteund maar activeringsgebiedsdelen aan Audience Manager kunnen worden verzonden naar Audience Manager via de [&#128279;](/help/destinations/catalog/adobe/experience-cloud-audiences.md) bestemmingskaart van het publiek 0&rbrace; van het Experience Cloud &lbrace;.

## 4. Welke bestemmingen hebt u vandaag in Audience Manager die u kunt beginnen naar Real-Time CDP te verhuizen?

De Adobe adviseert sterk dat de segmenten die in Audience Manager aan [&#x200B; op mensen-gebaseerde bestemmingen &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=nl) worden geactiveerd aan Real-Time CDP via [!UICONTROL Audience Manager Source Connector], dan door Real-Time CDP te activeren.

Alle op mensen-gebaseerde bestemmingen beschikbaar in Audience Manager - [&#x200B; Facebook &#x200B;](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [&#x200B; LinkedIn &#x200B;](/help/destinations/catalog/social/linkedin.md) - zijn ook beschikbaar in Real-Time CDP.

De extra gegevens van de eerste partij en media strategiepartners zoals [&#x200B; Pinterest &#x200B;](/help/destinations/catalog/advertising/pinterest.md), [&#x200B; Snapchat &#x200B;](/help/destinations/catalog/advertising/snap-inc.md), [&#x200B; TikTok &#x200B;](/help/destinations/catalog/social/tiktok.md), [&#x200B; Advertentie van Amazon &#x200B;](/help/destinations/catalog/advertising/amazon-ads.md), en [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) zijn beschikbaar.

Real-Time CDP steunt momenteel meer dan 60 bestemmingen binnen in de [&#x200B; catalogus &#x200B;](/help/destinations/catalog/overview.md), meer dan 20 waarvan reclame of sociale bestemmingen zijn die de aanpassing van het eerste partijpubliek steunen.

## Volgende stappen

Na het lezen van deze pagina hebt u nu een eerste reeks overwegingen die u kunt doorlopen wanneer u uw evolutie van Audience Manager naar Real-Time CDP start.
