---
keywords: personalisatie; doel; bestemming; personalisatiebestemmingen; vormen verpersoonlijkingsbestemmingen; dezelfde pagina; volgende bladzijde;
title: Vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: Leer hoe te om verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking te vormen.
seo-description: Configure personalization destinations for same-page and next-page personalization.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: 851a9598523d26ba52a367f6c03e3c9612f6678b
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# Vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking

Adobe Experience Platform gebruikt [randsegmentatie](../../segmentation/ui/edge-segmentation.md) om klanten toe te laten om publiekssegmenten tot stand te brengen en te richten op hoge schaal, in echt - tijd.

Met deze functie kunt u gebruiksgevallen voor personalisatie op dezelfde pagina en op de volgende pagina configureren.

Dit artikel verstrekt geleidelijke instructies op hoe te om Experience Platform en uw verpersoonlijkingsbestemmingen voor deze gebruiksgevallen te vormen.

## Stap 1: Een gegevensstroom configureren in de gebruikersinterface voor gegevensverzameling {#configure-datastream}

De eerste stap in vestiging moet uw verpersoonlijkingsbestemming een gegevensstroom voor het Web SDK van het Experience Platform vormen. Dit wordt gedaan in de UI van de Inzameling van Gegevens.

Bij het configureren van de gegevensstroom, onder **[!UICONTROL Adobe Experience Platform]** ervoor zorgen dat beide **[!UICONTROL Edge Segmentation]** en **[!UICONTROL Personalization Destinations]** zijn geselecteerd.

![Configuratie DataStream](../assets/ui/configure-personalization-destinations/datastream-config.png)

Voor meer informatie over hoe u een gegevensstroom instelt, volgt u de instructies in het dialoogvenster [Platform Web SDK-documentatie](../../edge/fundamentals/datastreams.md).

## Stap 2: Vorm uw verpersoonlijkingsbestemming {#configure-destination}

Nadat u uw gegevensstroom hebt gevormd, kunt u beginnen uw verpersoonlijkingsbestemming te vormen.

Volg de [zelfstudie over het maken van doelverbinding](../ui/connect-destination.md) voor gedetailleerde instructies op hoe te om een nieuwe bestemmingsverbinding tot stand te brengen.

Afhankelijk van de bestemming u vormt, verwijs naar de volgende artikelen voor bestemmings-specifieke eerste vereisten en verwante informatie:

* [Adobe Target-verbinding](../catalog/personalization/adobe-target-connection.md)
* [Aangepaste aanpassingsverbinding](../catalog/personalization/custom-personalization.md)

## Stap 3: Een [!DNL Active-On-Edge] samenvoegingsbeleid {#create-merge-policy}

Nadat u de doelverbinding hebt gemaakt, moet u een [!DNL Active-On-Edge] samenvoegbeleid.

Volg de instructies op [samenvoegingsbeleid maken](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)en zorgt ervoor dat de **[!UICONTROL Active-On-Edge Merge Policy]** schakelen.

## Stap 4: Nieuw segment maken in Platform {#create-segment}

Nadat u het [!DNL Active-On-Edge] samenvoegbeleid, moet u een nieuw segment in Platform tot stand brengen.

Volg de [segmentbuilder](../../segmentation/ui/segment-builder.md) gids om uw nieuw segment tot stand te brengen, en zorg ervoor [toewijzen](../../segmentation/ui/segment-builder.md#merge-policies) de [!DNL Active-On-Edge] samenvoegbeleid dat u in stap 3 hebt gemaakt.

## Stap 5: Activeer het segment aan uw bestemming

De laatste stap van het configuratieproces is het segment te activeren dat u in stap 4 aan de bestemming creeerde die u in stap 2 creeerde.

Volg deze [activeringszelfstudie](../ui/activate-profile-request-destinations.md).

## De configuratie valideren {#validate-configuration}

Nadat u de bovenstaande stappen met succes hebt uitgevoerd, ziet u de nieuwe segmenten in uw aanpassingsdoel.
