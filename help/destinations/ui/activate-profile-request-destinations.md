---
keywords: activeer profiel verzoek bestemmingen;activeer gegevens;profiel verzoek bestemmingen
title: De publieksgegevens van de activering aan de bestemmingen van het profielverzoek
type: Tutorial
description: Leer hoe te om de publieksgegevens te activeren u in Adobe Experience Platform hebt door segmenten aan de bestemmingen van het profielverzoek in kaart te brengen.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 26e7a3e78a4513aa69cdfbed7902509609e114cc
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# De publieksgegevens van de activering aan de bestemmingen van het profielverzoek

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist voor het activeren van publieksgegevens in Adobe Experience Platform-profielen voor aanvraagdoelen. Indien samen gebruikt met [randsegmentatie](../../segmentation/ui/edge-segmentation.md), laten deze bestemmingen zelfde-pagina en volgende-pagina het gebruiksgevallen van de verpersoonlijking op uw Web-eigenschappen toe. Meer informatie over [het toelaten van zelfde pagina en volgende-pagina verpersoonlijkingsgebruiksgevallen](/help/destinations/ui/configure-personalization-destinations.md).

De voorbeelden van de bestemmingen van het profielverzoek zijn [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) en de [Aangepaste personalisatie](../../destinations/catalog/personalization/custom-personalization.md) verbindingen.

## Vereisten {#prerequisites}

Als u gegevens naar doelen wilt activeren, moet u [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde verpersoonlijkingsbestemmingen, en vorm de bestemming die u wilt gebruiken.

### Samenvoegingsbeleid segment {#merge-policy}

Momenteel, steunen de bestemmingen van het profielverzoek slechts de activering van segmenten die gebruiken [Samenvoegingsbeleid actief op rand](../../segmentation/ui/segment-builder.md#merge-policies) ingesteld als standaard.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Tabblad Doelcatalogus](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate segments]** op de kaart die overeenkomt met de aanpassingsbestemming waar u de segmenten wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Knoppen activeren](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw segmenten te activeren en selecteer vervolgens **[!UICONTROL Next]**.

   ![Doel selecteren](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Naar de volgende sectie gaan [uw segmenten selecteren](#select-segments).

## Uw segmenten selecteren {#select-segments}

Gebruik de selectievakjes links van de segmentnamen om de segmenten te selecteren die u wilt activeren naar het doel en selecteer vervolgens **[!UICONTROL Next]**.

![Segmenten selecteren](../assets/ui/activate-profile-request-destinations/select-segments.png)

## (bèta) Kaartkenmerken {#map-attributes}

>[!IMPORTANT]
>
>De afbeeldingsstap, die op attributen-gebaseerde verpersoonlijking voor toelaat [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) en [algemene verpersoonlijkingsbestemmingen](/help/destinations/catalog/personalization/custom-personalization.md), is momenteel in bèta en uw organisatie heeft er wellicht nog geen toegang tot. Deze documentatie kan worden gewijzigd.

Selecteer de kenmerken op basis waarvan u gebruiksgevallen voor personalisatie voor uw gebruikers wilt inschakelen. Dit betekent dat als de waarde van een attribuut verandert of als een attribuut aan een profiel wordt toegevoegd, dat profiel een lid van het segment zal worden en aan de verpersoonlijkingsbestemming zal worden geactiveerd.

Het toevoegen van kenmerken is optioneel en u kunt doorgaan naar de volgende stap en personalisatie op dezelfde pagina en op de volgende pagina inschakelen zonder kenmerken te selecteren. Als u geen attributen in deze stap toevoegt, zal de verpersoonlijking nog voorkomen gebaseerd op het segmentlidmaatschap en de kwalificaties van de identiteitskaart voor profielen.

![Afbeelding waarin de toewijzingsstap wordt weergegeven terwijl een kenmerk is geselecteerd](../assets/ui/activate-profile-request-destinations/mapping-step.png)

Als u kenmerken wilt toevoegen, selecteert u de optie **[!UICONTROL Add new field]** besturing en zoek of navigeer naar het gewenste XDM-kenmerkveld, zoals hieronder wordt weergegeven.

![Schermopname die laat zien hoe een XDM-kenmerk in de toewijzingsstap moet worden geselecteerd](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

## Segmentexport plannen {#scheduling}

Standaard worden de [!UICONTROL Segment schedule] op de pagina worden alleen de nieuw geselecteerde segmenten weergegeven die u hebt gekozen in de huidige activeringsstroom.

![Nieuwe segmenten](../assets/ui/activate-profile-request-destinations/new-segments.png)

Om alle segmenten te zien die aan uw bestemming worden geactiveerd, gebruik de het filtreren optie en maak onbruikbaar **[!UICONTROL Show new segments only]** filter.

![Alle segmenten](../assets/ui/activate-profile-request-destinations/all-segments.png)

Op de **[!UICONTROL Segment schedule]** pagina, selecteer elk segment, dan gebruik **[!UICONTROL Start date]** en **[!UICONTROL End date]** selecteurs om het tijdinterval voor het verzenden van gegevens naar uw bestemming te vormen.

![Segmentatieschema](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Selecteren **[!UICONTROL Next]** om naar de [!UICONTROL Review] pagina.

## Controleren {#review}

Op de **[!UICONTROL Review]** , kunt u een overzicht van uw selectie zien. Selecteren **[!UICONTROL Cancel]** om de stroom op te delen, **[!UICONTROL Back]** om uw instellingen te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe u beleidsovertredingen kunt oplossen, raadpleegt u [Beleidshandhaving](../../rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie Documentatie inzake gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

![Controleren](../assets/ui/activate-profile-request-destinations/review.png)

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->