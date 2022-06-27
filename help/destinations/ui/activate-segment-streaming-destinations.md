---
keywords: segment streamingdoelen activeren;segment streamingdoelen activeren;gegevens activeren
title: De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen
type: Tutorial
description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten toe te wijzen aan segmentstreamingdoelen.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist voor het activeren van publieksgegevens in streaming doelen voor Adobe Experience Platform-segmenten.

## Vereisten {#prerequisites}

Als u gegevens naar doelen wilt activeren, moet u [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Tabblad Doelcatalogus](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate segments]** op de kaart die overeenkomt met de bestemming waar u de segmenten wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Knoppen activeren](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw segmenten te activeren en selecteer vervolgens **[!UICONTROL Next]**.

   ![Doel selecteren](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Naar de volgende sectie gaan [uw segmenten selecteren](#select-segments).

## Uw segmenten selecteren {#select-segments}

Gebruik de selectievakjes links van de segmentnamen om de segmenten te selecteren die u wilt activeren naar het doel en selecteer vervolgens **[!UICONTROL Next]**.

![Segmenten selecteren](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Kenmerken en identiteiten toewijzen {#mapping}

>[!IMPORTANT]
>
>Deze stap is slechts op sommige segment het stromen bestemmingen van toepassing. Als uw doel geen **[!UICONTROL Mapping]** stap, overslaan naar [Segmentexport plannen](#scheduling).

Voor sommige segment streamingdoelen moet u bronkenmerken of naamruimten selecteren om toe te wijzen als doelidentiteiten in de bestemming.

1. In de **[!UICONTROL Mapping]** pagina, selecteert u **[!UICONTROL Add new mapping]**.

   ![Nieuwe toewijzing toevoegen](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Selecteer de pijl rechts van de knop **[!UICONTROL Source field]** vermelding.

   ![Bronveld selecteren](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. In de **[!UICONTROL Select source field]** pagina gebruiken **[!UICONTROL Select attributes]** of de **[!UICONTROL Select identity namespace]** opties voor het schakelen tussen de twee categorieën beschikbare bronvelden. Via de beschikbare [!DNL XDM] profielkenmerken en naamruimten, selecteer de kenmerken die u wilt toewijzen aan het doel en kies vervolgens **[!UICONTROL Select]**.

   ![Bronveldpagina selecteren](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Selecteer de knop rechts van de knop **[!UICONTROL Target field]** vermelding.

   ![Doelveld selecteren](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. In de **[!UICONTROL Select target field]** pagina, selecteert u de naamruimte van de doelidentiteit waaraan u het bronveld wilt toewijzen en kiest u **[!UICONTROL Select]**.

   ![Doelveldpagina selecteren](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Herhaal stap 1 tot en met 5 om meer toewijzingen toe te voegen.

### Transformatie toepassen {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Transformatie toepassen"
>abstract="Schakel deze optie in als u niet-gehashte bronvelden gebruikt, zodat Adobe Experience Platform deze automatisch verbergt bij activering."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html#apply-transformation" text="Meer informatie in documentatie"

Wanneer u ongehashte bronkenmerken toewijst aan doelkenmerken die de bestemming verwacht te worden gehasht (bijvoorbeeld: `email_lc_sha256` of `phone_sha256`), controleert u de **Transformatie toepassen** als u wilt dat Adobe Experience Platform de bronkenmerken bij activering automatisch hasht.

![Identiteitskaart](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Segmentexport plannen {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Einddatum"
>abstract="Het toevoegen van een einddatum voor segmentprogramma is niet beschikbaar."
>additional-url="https://www.adobe.com/go/destinations-activate-segment-scheduling-en" text="Meer informatie in documentatie"

Standaard worden de [!UICONTROL Segment schedule] op de pagina worden alleen de nieuw geselecteerde segmenten weergegeven die u hebt gekozen in de huidige activeringsstroom.

![Nieuwe segmenten](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

Om alle segmenten te zien die aan uw bestemming worden geactiveerd, gebruik de het filtreren optie en maak onbruikbaar **[!UICONTROL Show new segments only]** filter.

![Alle segmenten](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. Op de **[!UICONTROL Segment schedule]** pagina, selecteer elk segment, dan gebruik **[!UICONTROL Start date]** en **[!UICONTROL End date]** selecteurs om het tijdinterval voor het verzenden van gegevens naar uw bestemming te vormen.

   ![Segmentatieschema](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Voor sommige doelen moet u de **[!UICONTROL Origin of audience]** voor elk segment, gebruikend het drop-down menu onder de kalenderselecteurs. Sla deze stap over als uw doel deze kiezer niet bevat.

      ![Toewijzing-id](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Voor sommige doelen moet u handmatig een toewijzing maken [!DNL Platform] segmenten aan hun tegenhanger in de doelbestemming. Om dit te doen, selecteer elk segment, dan ga overeenkomstige segmentidentiteitskaart van het bestemmingsplatform in **[!UICONTROL Mapping ID]** veld. Sla deze stap over als dit veld niet in uw bestemming is opgenomen.

      ![Toewijzing-id](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Voor sommige doelen moet u een **[!UICONTROL App ID]** bij activering [!DNL IDFA] of [!DNL GAID] segmenten. Sla deze stap over als dit veld niet in uw bestemming is opgenomen.

      ![Toepassings-id](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Selecteren **[!UICONTROL Next]** om naar de [!UICONTROL Review] pagina.

## Controleren {#review}

Op de **[!UICONTROL Review]** , kunt u een overzicht van uw selectie zien. Selecteren **[!UICONTROL Cancel]** om de stroom op te delen, **[!UICONTROL Back]** om uw instellingen te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe u beleidsovertredingen kunt oplossen, raadpleegt u [Beleidshandhaving](../../rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie Documentatie inzake gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

![Controleren](../assets/ui/activate-segment-streaming-destinations/review.png)

## Segmentactivering verifiëren {#verify}

Controleer de [doelcontroledocumentatie](../../dataflows/ui/monitor-destinations.md) voor gedetailleerde informatie over hoe te om de stroom van gegevens aan uw bestemmingen te controleren.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
