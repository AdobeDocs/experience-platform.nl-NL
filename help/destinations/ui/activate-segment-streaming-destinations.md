---
title: De publieksgegevens van de activering aan het stromen bestemmingen
type: Tutorial
description: Leer hoe u het publiek in Adobe Experience Platform activeert door het toe te wijzen aan streamingdoelen.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 0%

---


# Stimulansen voor het publiek naar streamingdoelen activeren

>[!IMPORTANT]
> 
> * Om het publiek te activeren en het [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
> * Om het publiek te activeren zonder door [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}
> 
> Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist om het publiek in Adobe Experience Platform-streaming doelen te activeren.

## Vereisten {#prerequisites}

Als u een publiek naar een bestemming wilt activeren, moet u [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Tabblad Doelcatalogus met verschillende streamingdoelen.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate audiences]** op de kaart die overeenkomt met de bestemming waar u uw publiek wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Activeer controle die in de catalogus van bestemmingen wordt benadrukt.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw publiek te activeren en selecteer vervolgens **[!UICONTROL Next]**.

   ![Een doelverbinding die in Uitgezochte bestemmingsstap wordt benadrukt.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Naar de volgende sectie gaan [uw publiek selecteren](#select-audiences).

## Uw publiek selecteren {#select-audiences}

Als u het publiek dat u wilt activeren naar het doel wilt selecteren, schakelt u het selectievakje links van de publieksnamen in en selecteert u **[!UICONTROL Next]**.

U kunt kiezen uit meerdere soorten publiek, afhankelijk van de oorsprong:

* **[!UICONTROL Segmentation Service]**: publiek dat binnen Experience Platform door de Dienst van de Segmentatie wordt geproduceerd. Zie de [segmentatiedocumentatie](../../segmentation/ui/overview.md) voor meer informatie .
* **[!UICONTROL Custom upload]**: Soorten publiek dat buiten het Experience Platform is gegenereerd en als CSV-bestanden naar Platform is geüpload. Raadpleeg de documentatie over [een publiek importeren](../../segmentation/ui/audience-portal.md#import-audience).
* Andere soorten soorten publiek, afkomstig van andere oplossingen voor Adobe, zoals [!DNL Audience Manager].

![Verschillende soorten publiek gemarkeerd in de stap Soorten publiek selecteren.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Kenmerken en identiteiten toewijzen {#mapping}

>[!IMPORTANT]
>
>Deze stap is alleen van toepassing op bepaalde streamingdoelen voor het publiek. Als uw doel geen **[!UICONTROL Mapping]** stap, overslaan naar [publieksplanning](#scheduling).
>
>Wanneer u een publiek activeert naar streaming doelen, moet u ook een toewijzing maken *ten minste één naamruimte voor doelidentiteit*, naast de kenmerken van het doelprofiel. Anders wordt het publiek niet geactiveerd naar het doelplatform.
> ![Afbeelding van toewijzingsstap met een verplichte naamruimtetoewijzing.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


Voor sommige doelstreamingdoelen voor het publiek moet u bronkenmerken of naamruimten selecteren om toe te wijzen als doelidentiteiten in de bestemming.

1. In de **[!UICONTROL Mapping]** pagina, selecteert u **[!UICONTROL Add new mapping]**.

   ![Nieuwe gemarkeerde toewijzingsbesturingselement toevoegen.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Selecteer de pijl rechts van de knop **[!UICONTROL Source field]** vermelding.

   ![Selecteer het besturingselement voor het bronveld gemarkeerd.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. In de **[!UICONTROL Select source field]** pagina gebruiken **[!UICONTROL Select attributes]** of de **[!UICONTROL Select identity namespace]** opties voor het schakelen tussen de twee categorieën beschikbare bronvelden. Via de beschikbare [!DNL XDM] profielkenmerken en naamruimten, selecteer de kenmerken die u wilt toewijzen aan het doel en kies vervolgens **[!UICONTROL Select]**.

   Gebruik de **[!UICONTROL Show only fields with data]** schakelen om alleen schemavelden weer te geven die zijn gevuld met waarden. Standaard worden alleen gevulde schemavelden weergegeven.

   ![Selecteer de pagina met bronvelden waarop verschillende beschikbare bronvelden worden weergegeven.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. Selecteer de knop rechts van de knop **[!UICONTROL Target field]** vermelding.

   ![Selecteer gemarkeerd doelveld.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. In de **[!UICONTROL Select target field]** pagina, selecteert u de naamruimte van de doelidentiteit waaraan u het bronveld wilt toewijzen en kiest u **[!UICONTROL Select]**.

   ![Selecteer de pagina met doelvelden met de beschikbare opties voor de toewijzingen van doelvelden.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Herhaal stap 1 tot en met 5 om meer toewijzingen toe te voegen.

### Transformatie toepassen {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Transformatie toepassen"
>abstract="Schakel deze optie in als u niet-gehashte bronvelden gebruikt, zodat Adobe Experience Platform deze automatisch verbergt bij activering."

Wanneer u ongehashte bronkenmerken toewijst aan doelkenmerken die de bestemming verwacht te worden gehasht (bijvoorbeeld: `email_lc_sha256` of `phone_sha256`), controleert u **Transformatie toepassen** als u wilt dat Adobe Experience Platform de bronkenmerken bij activering automatisch hasht.

![Transformatiebeheer toepassen dat is gemarkeerd in de stap Identiteitstoewijzing.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Het exporteren van publiek plannen {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Einddatum"
>abstract="Het toevoegen van een einddatum voor het publieksprogramma is niet beschikbaar."

Standaard worden de **[!UICONTROL Audience schedule]** op de pagina worden alleen de onlangs geselecteerde doelgroepen weergegeven die u in de huidige activeringsstroom hebt gekozen.

Als u alle soorten publiek wilt zien die op uw doel worden geactiveerd, gebruikt u de filteroptie en schakelt u de optie **[!UICONTROL Show new audiences only]** filter.

![Alle soorten publiek](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. Op de **[!UICONTROL Audience schedule]** pagina, selecteert u elk publiek en gebruikt u vervolgens de **[!UICONTROL Start date]** en **[!UICONTROL End date]** selecteurs om het tijdinterval voor het verzenden van gegevens naar uw bestemming te vormen.

   ![Het filter Audience-schema is gemarkeerd.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Voor sommige doelen moet u de **[!UICONTROL Origin of audience]** voor elk publiek, gebruikend het drop-down menu onder de kalenderselecteurs. Als deze kiezer niet in uw doel is opgenomen, slaat u deze stap over.

     ![Vervolgkeuzelijst Toewijzings-id gemarkeerd.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Voor sommige doelen moet u handmatig een toewijzing maken [!DNL Platform] publiek naar zijn tegenhanger in de doelbestemming. Om dit te doen, selecteer elk publiek, dan ga overeenkomstige publiekidentiteitskaart van het bestemmingsplatform in **[!UICONTROL Mapping ID]** veld. Sla deze stap over als dit veld niet in uw bestemming is opgenomen.

     ![Oorsprong van vervolgkeuzelijst voor publiek gemarkeerd.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Voor sommige doelen moet u een **[!UICONTROL App ID]** bij activering [!DNL IDFA] of [!DNL GAID] publiek. Sla deze stap over als dit veld niet in uw bestemming is opgenomen.

     ![Toepassings-id-vervolgkeuzelijst gemarkeerd.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Selecteren **[!UICONTROL Next]** om naar de [!UICONTROL Review] pagina.

## Controleren {#review}

Op de **[!UICONTROL Review]** , kunt u een overzicht van uw selectie zien. Selecteren **[!UICONTROL Cancel]** om de stroom op te delen, **[!UICONTROL Back]** om uw instellingen te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

![Selectieoverzicht in de revisiestap.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Goedkeuring van het beleid {#consent-policy-evaluation}

Als uw organisatie is aangeschaft **Adobe Gezondheidsschild** of **Privacy- en beveiligingsschild van Adobe**, selecteert u **[!UICONTROL View applicable consent policies]** na te gaan welk toestemmingsbeleid wordt toegepast en hoeveel profielen als gevolg daarvan in de activering worden opgenomen. Meer informatie [goedkeuring beleidsevaluatie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) voor meer informatie .

### Controle van het gegevensgebruiksbeleid {#data-usage-policy-checks}

In de **[!UICONTROL Review]** stap, controleert het Experience Platform ook om het even welke schendingen van het beleid van het gegevensgebruik. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor publieksactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe u beleidsovertredingen kunt oplossen, leest u informatie over [beleidsovertredingen voor gegevensgebruik](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) in de sectie Documentatie inzake gegevensbeheer.

![Een voorbeeld van een schending van een gegevensbeleid die in het activeringswerkschema wordt getoond.](../assets/common/data-policy-violation.png)

### Filter publiek {#filter-audiences}

In deze stap kunt u ook de beschikbare filters op de pagina gebruiken om alleen de doelgroepen weer te geven waarvan het schema of de toewijzing is bijgewerkt als onderdeel van deze workflow. U kunt ook schakelen welke tabelkolommen u wilt zien.

![De opname van het scherm die de beschikbare publieksfilters in de overzichtsstap toont.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Als u tevreden bent met de selectie en er zijn geen beleidsovertredingen vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

## Activering van publiek controleren {#verify}

Controleer de [doelcontroledocumentatie](../../dataflows/ui/monitor-destinations.md) voor gedetailleerde informatie over hoe te om de stroom van gegevens aan uw bestemmingen te controleren.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
