---
title: Evolutie van Audience Manager naar Real-Time CDP
description: Begrijp de overwegingen alvorens uw migratie van Audience Manager aan Real-Time CDP te plannen.
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Evolutie van Audience Manager naar Real-Time CDP

Naarmate uw organisatie zich ontwikkelt om Adobe Real-Time CDP te gebruiken, verkent u deze overwegingen om uw gegevens voor te bereiden en zich bewust te worden van de kritieke verschillen tussen de twee technologieën. Dit artikel is gericht op een beoefenaar van een beroep.

![Audience Manager naar Real-Time CDP-evolutiediagram](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Overweeg gegevensarchitectuur binnen Audience Manager

Als je kijkt naar de evolutie van Audience Manager naar Real-Time CDP, is het nu een cruciaal moment om je [Audience Manager-segmenten](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=en) en bepaalt de [signalen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=en), [kenmerken](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=en), en [regels](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=en#segment-builder-section) zijn die de segmenten vormen.

Overweeg bovendien de gegevensbronnen die u momenteel in de Audience Manager gebruikt.

Adobe raadt u aan de segmenten als volgt te categoriseren:

* Segmenten die via de [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md), aangezien zij geen gegevensgebiedsdelen, geen bestemming of activeringsuitdagingen hebben, en hun segmenteringsregels kunnen door Real-time CDP worden gecreeerd [segmentbuilder](/help/segmentation/ui/segment-builder.md) later.
* Segmenten met regels die kunnen worden ondersteund, maar die gegevens bevatten die niet beschikbaar zijn in Real-Time CDP.
* Segmenten die niet in real time CDP kunnen worden gecreeerd en functionaliteit missen.

>[!TIP]
>
>Adobe Real-Time CDP-aanbiedingen [drie soorten segmentbeoordeling](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming], en [!UICONTROL Edge]. Klanten die realtime segmenten in de Audience Manager gebruiken, kunnen worden beperkt door de huidige beperking van 500 streaming segmenten in Real-Time CDP. Meer informatie over [segmentatiegeleidingen](/help/profile/guardrails.md).

## 2. Welke segmenten zijn kritiek om door via te verzenden [!UICONTROL Audience Manager Source Connector]?

Gebaseerd op hun evaluatiecriteria, kunnen de segmenten die geen gegevensgebiedsdelen, geen bestemming of activeringsuitdagingen hebben, en hun segmenteringsregels door de gegevensinzameling van Real-Time CDP zoals worden gecreeerd [Adobe Experience Platform Web SDK](/help/edge/web-sdk-faq.md) op een recentere datum zou door de Bron van de Audience Manager Schakelaar moeten worden verzonden.

## 3. Gebruikt u de [!UICONTROL Experience Cloud Audiences] bestemming om gegevens terug naar Audience Manager te brengen?

Segmenten die regels hebben die in Real-Time CDP kunnen worden ondersteund, maar die activeringsafhankelijkheden hebben voor Audience Manager, kunnen via het dialoogvenster naar de Audience Manager worden verzonden [Experience Cloud publiek](/help/destinations/catalog/adobe/experience-cloud-audiences.md) doelkaart.

## 4. Welke bestemmingen hebt u op zijn plaats in Audience Manager vandaag dat u aan Real-Time CDP kunt beginnen te bewegen?

Adobe raadt u ten zeerste aan om segmenten die in Audience Manager zijn geactiveerd, aan te passen aan [op mensen gebaseerde bestemmingen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=en) via de [!UICONTROL Audience Manager Source Connector], om vervolgens te activeren via Real-Time CDP.

Alle op mensen gebaseerde bestemmingen beschikbaar in Audience Manager - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [linkedIn](/help/destinations/catalog/social/linkedin.md) - ook beschikbaar zijn in Real-Time CDP.

Extra eersteklas gegevens en media strategiepartners zoals [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon-advertenties](/help/destinations/catalog/advertising/amazon-ads.md), en [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) zijn beschikbaar.

Real-Time CDP biedt momenteel ondersteuning voor meer dan 60 native bestemmingen in de [catalogus](/help/destinations/catalog/overview.md), waarvan er meer dan 20 reclame- of sociale bestemmingen zijn die ondersteuning bieden voor het afstemmen van de eerste doelgroep.

## Volgende stappen

Na het lezen van deze pagina hebt u nu een eerste reeks overwegingen die u kunt doorlopen wanneer u uw evolutie van Audience Manager naar Real-Time CDP start.
