---
title: Evolutie van Audience Manager naar Real-Time CDP
description: Begrijp de overwegingen alvorens uw migratie van Audience Manager aan Real-Time CDP te plannen.
exl-id: 83ab9a5d-9abc-4072-b449-e2a9ecd48639
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Evolutie van Audience Manager naar Real-Time CDP

Naarmate uw organisatie zich ontwikkelt om Adobe Real-Time CDP te gebruiken, verkent u deze overwegingen om uw gegevens voor te bereiden en zich bewust te worden van de kritieke verschillen tussen de twee technologieën. Dit artikel is gericht op een beoefenaar van een beroep.

![Audience Manager naar Real-Time CDP-evolutiediagram](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Overweeg gegevensarchitectuur binnen Audience Manager

Als je kijkt naar de evolutie van Audience Manager naar Real-Time CDP, is het nu een cruciaal moment om je [Audience Managers](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html) en bepaalt de [signalen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html), [kenmerken](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html), en [regels](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html#segment-builder-section) zijn die de segmenten vormen.

Overweeg bovendien de gegevensbronnen die u momenteel in de Audience Manager gebruikt.

Adobe raadt u aan de segmenten als volgt te categoriseren:

* Segmenten die via de [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md), aangezien zij geen gegevensgebiedsdelen, geen bestemming of activeringsuitdagingen hebben, en hun segmenteringsregels kunnen tot stand worden gebracht door Real-Time CDP [segmentbuilder](/help/segmentation/ui/segment-builder.md) later.
* Segmenten met regels die kunnen worden ondersteund, maar die gegevens bevatten die niet beschikbaar zijn in Real-Time CDP.
* Segmenten die niet in Real-Time CDP kunnen worden gemaakt en geen functionaliteit hebben.

>[!TIP]
>
>Adobe Real-Time CDP-aanbiedingen [drie soorten segmentbeoordeling](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming], en [!UICONTROL Edge]. Klanten die realtime segmenten in de Audience Manager gebruiken, kunnen worden beperkt door de huidige beperking van 500 streaming segmenten in Real-Time CDP. Meer informatie over [segmentatiegeleidingen](/help/profile/guardrails.md).

## 2. Welke segmenten zijn essentieel om door te sturen via [!UICONTROL Audience Manager Source Connector]?

Gebaseerd op hun evaluatiecriteria, kunnen de segmenten die geen gegevensgebiedsdelen, geen bestemming of activeringsuitdagingen hebben, en hun segmenteringsregels door de gegevensinzameling van Real-Time CDP zoals worden gecreeerd [Adobe Experience Platform Web SDK](/help/web-sdk/faq.md) op een recentere datum zou door de Bron van de Audience Manager Schakelaar moeten worden verzonden.

## 3. Gebruikt u de [!UICONTROL Experience Cloud Audiences] bestemming om gegevens terug naar Audience Manager te brengen?

Segmenten die regels hebben die in Real-Time CDP kunnen worden ondersteund, maar die activeringsafhankelijkheden hebben voor Audience Manager, kunnen via de [Soorten publiek Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) doelkaart.

## 4. Welke bestemmingen hebt u vandaag in Audience Manager die u kunt beginnen naar Real-Time CDP te verhuizen?

Adobe raadt sterk aan dat segmenten die in Audience Manager worden geactiveerd tot [op mensen gebaseerde bestemmingen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=nl) via de [!UICONTROL Audience Manager Source Connector], activeren via Real-Time CDP.

Alle op mensen gebaseerde bestemmingen beschikbaar in Audience Manager - [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google Customer Match]](/help/destinations/catalog/advertising/google-customer-match.md), [LinkedIn](/help/destinations/catalog/social/linkedin.md) - ook beschikbaar zijn in Real-Time CDP.

Extra eersteklas gegevens en media strategiepartners zoals [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Adds](/help/destinations/catalog/advertising/amazon-ads.md), en [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md) zijn beschikbaar.

Real-Time CDP biedt momenteel ondersteuning voor meer dan 60 native bestemmingen in de [catalogus](/help/destinations/catalog/overview.md), waarvan er meer dan 20 reclame- of sociale bestemmingen zijn die ondersteuning bieden voor het afstemmen van de eerste doelgroep.

## Volgende stappen

Na het lezen van deze pagina hebt u nu een eerste reeks overwegingen die u kunt doorlopen wanneer u uw evolutie van Audience Manager naar Real-Time CDP start.
