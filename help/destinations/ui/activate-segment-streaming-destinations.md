---
keywords: segment streamingdoelen activeren;segment streamingdoelen activeren;gegevens activeren
title: De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen
type: Tutorial
seo-title: Activate audience data to streaming segment export destinations
description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten toe te wijzen aan segmentstreamingdoelen.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to segment streaming destinations.
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---


# De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist voor het activeren van publieksgegevens in streaming doelen voor Adobe Experience Platform-segmenten.

## Vereisten {#prerequisites}

Om gegevens aan bestemmingen te activeren, moet u [met succes hebben verbonden met een bestemming](./connect-destination.md). Als u dit niet reeds hebt gedaan, ga naar [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer het tabblad **[!UICONTROL Catalog]**.

   ![Tabblad Doelcatalogus](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecteer **[!UICONTROL Activate segments]** op de kaart die overeenkomt met de bestemming waar u de segmenten wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Knoppen activeren](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw segmenten te activeren en selecteer **[!UICONTROL Next]**.

   ![Doel selecteren](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Ga naar de volgende sectie naar [selecteer uw segmenten](#select-segments).

## Uw segmenten selecteren {#select-segments}

Gebruik de controledozen links van de segmentnamen om de segmenten te selecteren die u aan de bestemming wilt activeren, dan uitgezocht **[!UICONTROL Next]**.

![Segmenten selecteren](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Kenmerken en identiteiten toewijzen {#mapping}

>[!IMPORTANT]
>
>Deze stap is slechts op sommige segment het stromen bestemmingen van toepassing. Als uw bestemming geen **[!UICONTROL Mapping]** stap heeft, overslaan aan [de segmentuitvoer van het Programma](#scheduling).

Voor sommige segment streamingdoelen moet u bronkenmerken of naamruimten selecteren om toe te wijzen als doelidentiteiten in de bestemming.

1. Selecteer **[!UICONTROL Add new mapping]** op de pagina **[!UICONTROL Mapping]**.

   ![Nieuwe toewijzing toevoegen](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Selecteer de pijl rechts van de **[!UICONTROL Source field]** ingang.

   ![Bronveld selecteren](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Gebruik op de pagina **[!UICONTROL Select source field]** de opties **[!UICONTROL Select attributes]** of **[!UICONTROL Select identity namespace]** om te schakelen tussen de twee categorieën van beschikbare bronvelden. Van beschikbare [!DNL XDM] profielattributen en identiteitsnamespaces, selecteer degenen die u aan de bestemming wilt in kaart brengen, dan kiezen **[!UICONTROL Select]**.

   ![Bronveldpagina selecteren](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Selecteer de knoop rechts van de **[!UICONTROL Target field]** ingang.

   ![Doelveld selecteren](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Selecteer op de pagina **[!UICONTROL Select target field]** de naamruimte van de doelidentiteit waaraan u het bronveld wilt toewijzen en kies **[!UICONTROL Select]**.

   ![Doelveldpagina selecteren](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Herhaal stap 1 tot en met 5 om meer toewijzingen toe te voegen.

### Transformatie toepassen {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Transformatie toepassen"
>abstract="Schakel deze optie in als u niet-gehashte bronvelden gebruikt, zodat Adobe Experience Platform deze automatisch verbergt bij activering."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#apply-transformation" text="Meer informatie in documentatie"

Wanneer u ongehashte bronkenmerken toewijst aan doelkenmerken die de bestemming verwacht te worden gehasht (bijvoorbeeld: `email_lc_sha256` of `phone_sha256`), controleer **Transformatie** toepassen optie om Adobe Experience Platform automatisch te hebben de bronattributen bij activering hakken.

![Identiteitskaart](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Segmentexport plannen {#scheduling}

Standaard worden op de pagina [!UICONTROL Segment schedule] alleen de zojuist geselecteerde segmenten weergegeven die u hebt gekozen in de huidige activeringsstroom.

![Nieuwe segmenten](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

Om alle segmenten te zien die aan uw bestemming worden geactiveerd, gebruik de het filtreren optie en maak **[!UICONTROL Show new segments only]** filter onbruikbaar.

![Alle segmenten](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. Selecteer elk segment op de pagina **[!UICONTROL Segment schedule]** en gebruik vervolgens de kiezers **[!UICONTROL Start date]** en **[!UICONTROL End date]** om het tijdsinterval voor het verzenden van gegevens naar uw bestemming te configureren.

   ![Segmentatieschema](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Sommige bestemmingen vereisen u om **[!UICONTROL Origin of audience]** voor elk segment te selecteren, gebruikend het drop-down menu onder de kalenderselecteurs. Sla deze stap over als uw doel deze kiezer niet bevat.

      ![Toewijzing-id](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Sommige bestemmingen vereisen u om segmenten [!DNL Platform] aan hun tegenhanger in de doelbestemming manueel in kaart te brengen. Om dit te doen, selecteer elk segment, dan ga overeenkomstige segmentidentiteitskaart van het bestemmingsplatform op het **[!UICONTROL Mapping ID]** gebied in. Sla deze stap over als dit veld niet in uw bestemming is opgenomen.

      ![Toewijzing-id](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Voor sommige doelen moet u een **[!UICONTROL App ID]** invoeren wanneer u segmenten [!DNL IDFA] of [!DNL GAID] activeert. Sla deze stap over als dit veld niet in uw bestemming is opgenomen.

      ![Toepassings-id](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Selecteer **[!UICONTROL Next]** om naar de [!UICONTROL Review] pagina te gaan.

## Controleren {#review}

Op de **[!UICONTROL Review]** pagina, kunt u een samenvatting van uw selectie zien. Selecteer **[!UICONTROL Cancel]** om de stroom te verbreken, **[!UICONTROL Back]** om uw montages te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](../../rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie van de documentatie van het gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![Controleren](../assets/ui/activate-segment-streaming-destinations/review.png)

## Segmentactivering verifiëren {#verify}

Raadpleeg de [documentatie voor doelbewaking](../../dataflows/ui/monitor-destinations.md) voor gedetailleerde informatie over hoe u de gegevensstroom naar uw doelen kunt controleren.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
