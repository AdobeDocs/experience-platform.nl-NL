---
keywords: activeer profiel verzoek bestemmingen;activeer gegevens;profiel verzoek bestemmingen
title: De publieksgegevens van de activering aan de bestemmingen van het profielverzoek (Bèta)
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Leer hoe te om de publieksgegevens te activeren u in Adobe Experience Platform hebt door segmenten aan de bestemmingen van het profielverzoek in kaart te brengen.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# De publieksgegevens van de activering aan de bestemmingen van het profielverzoek (Bèta)

## Overzicht {#overview}

>[!IMPORTANT]
>
>De de verzoekbestemmingen van het profiel in Adobe Experience Platform zijn momenteel in Bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

In dit artikel wordt uitgelegd welke workflow is vereist voor het activeren van publieksgegevens in Adobe Experience Platform-profielen voor aanvraagdoelen. Voorbeelden van bestemmingen van profielverzoeken zijn [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) en [Aangepaste verpersoonlijking](../../destinations/catalog/personalization/custom-personalization.md) verbindingen.

## Vereisten {#prerequisites}

Om gegevens aan bestemmingen te activeren, moet u [met succes hebben verbonden met een bestemming](./connect-destination.md). Als u dit niet reeds hebt gedaan, ga naar [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

### Samenvoegingsbeleid segment {#merge-policy}

Momenteel, steunen de bestemmingen van het profielverzoek slechts de activering van segmenten die [standaardsamenvoegbeleid](../../segmentation/ui/segment-builder.md#merge-policies) gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer het tabblad **[!UICONTROL Catalog]**.

   ![Tabblad Doelcatalogus](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecteer **[!UICONTROL Activate segments]** op de kaart die overeenkomt met de bestemming waar u de segmenten wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Knoppen activeren](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw segmenten te activeren en selecteer **[!UICONTROL Next]**.

   ![Doel selecteren](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Ga naar de volgende sectie naar [selecteer uw segmenten](#select-segments).

## Uw segmenten selecteren {#select-segments}

Gebruik de controledozen links van de segmentnamen om de segmenten te selecteren die u aan de bestemming wilt activeren, dan uitgezocht **[!UICONTROL Next]**.

![Segmenten selecteren](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Segmentexport plannen {#scheduling}

Standaard worden op de pagina [!UICONTROL Segment schedule] alleen de zojuist geselecteerde segmenten weergegeven die u hebt gekozen in de huidige activeringsstroom.

![Nieuwe segmenten](../assets/ui/activate-profile-request-destinations/new-segments.png)

Om alle segmenten te zien die aan uw bestemming worden geactiveerd, gebruik de het filtreren optie en maak **[!UICONTROL Show new segments only]** filter onbruikbaar.

![Alle segmenten](../assets/ui/activate-profile-request-destinations/all-segments.png)

Selecteer elk segment op de pagina **[!UICONTROL Segment schedule]** en gebruik vervolgens de kiezers **[!UICONTROL Start date]** en **[!UICONTROL End date]** om het tijdsinterval voor het verzenden van gegevens naar uw bestemming te configureren.

![Segmentatieschema](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Selecteer **[!UICONTROL Next]** om naar de [!UICONTROL Review] pagina te gaan.

## Controleren {#review}

Op de **[!UICONTROL Review]** pagina, kunt u een samenvatting van uw selectie zien. Selecteer **[!UICONTROL Cancel]** om de stroom te verbreken, **[!UICONTROL Back]** om uw montages te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](../../rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie van de documentatie van het gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![Controleren](../assets/ui/activate-profile-request-destinations/review.png)

## Segmentactivering verifiëren {#verify}

Raadpleeg de [documentatie voor doelbewaking](../../dataflows/ui/monitor-destinations.md) voor gedetailleerde informatie over hoe u de gegevensstroom naar uw doelen kunt controleren.