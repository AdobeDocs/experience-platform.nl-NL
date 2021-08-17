---
keywords: segment streamingdoelen activeren;segment streamingdoelen activeren;gegevens activeren
title: De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen
type: Tutorial
seo-title: De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen
description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten toe te wijzen aan segmentstreamingdoelen.
seo-description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten toe te wijzen aan segmentstreamingdoelen.
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---


# De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist voor het activeren van publieksgegevens in streaming doelen voor Adobe Experience Platform-segmenten.

## Vereisten {#prerequisites}

Om gegevens aan bestemmingen te activeren, moet u [met succes hebben verbonden met een bestemming](./connect-destination.md). Als u dit niet reeds hebt gedaan, ga naar [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer het tabblad **[!UICONTROL Browse]**.

   ![Tabblad Doelbladeren](../assets/ui/activate-segment-streaming-destinations/browse-tab.png)

1. Selecteer de **[!UICONTROL Add segments]** knoop die aan de bestemming beantwoordt waar u uw segmenten wilt activeren, zoals aangetoond in het hieronder beeld.

   ![Knoppen activeren](../assets/ui/activate-segment-streaming-destinations/activate-buttons-browse.png)

1. Ga naar de volgende sectie naar [selecteer uw segmenten](#select-segments).

## Uw segmenten selecteren {#select-segments}

Gebruik de controledozen links van de segmentnamen om de segmenten te selecteren die u aan de bestemming wilt activeren, dan uitgezocht **[!UICONTROL Next]**.

![Segmenten selecteren](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Kenmerken en identiteiten toewijzen {#mapping}

>[!IMPORTANT]
>
>Deze stap is slechts op sommige segment het stromen bestemmingen van toepassing. Als uw bestemmingen geen **[!UICONTROL Mapping]** stap hebben, overslaan aan [de segmentuitvoer van het Programma](#scheduling).

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

### Voorbeeld van toewijzing: publieksgegevens activeren in [!DNL Facebook Custom Audience] {#example-facebook}

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het activeren van publieksgegevens in [!DNL Facebook Custom Audience].

Bronvelden selecteren:

* Selecteer de naamruimte `Email` als bronidentiteit als de e-mailadressen die u gebruikt geen hashed zijn.
* Selecteer de naamruimte `Email_LC_SHA256` als bronidentiteit als u de e-mailadressen van de klant bij het invoeren van gegevens hebt gewijzigd in [!DNL Platform], volgens [!DNL Facebook] [e-mailhashingvereisten](../catalog/social/facebook.md#email-hashing-requirements).
* Selecteer `PHONE_E.164` namespace als bronidentiteit als uw gegevens uit niet-gehakte telefoonaantallen bestaan. [!DNL Platform] hash de telefoonnummers om aan de  [!DNL Facebook] vereisten te voldoen.
* Selecteer `Phone_SHA256` namespace als bronidentiteit als u telefoonaantallen op gegevensinvoer in [!DNL Platform], volgens [!DNL Facebook] [de vereisten van de het hakken van het telefoonaantal ](../catalog/social/facebook.md#phone-number-hashing-requirements) hakt.
* Selecteer `IDFA` namespace als bronidentiteit als uw gegevens uit [!DNL Apple] apparaat IDs bestaan.
* Selecteer `GAID` namespace als bronidentiteit als uw gegevens uit [!DNL Android] apparaat IDs bestaan.
* Selecteer `Custom` namespace als bronidentiteit als uw gegevens uit ander type herkenningstekens bestaan.

Doelvelden selecteren:

* Selecteer `Email_LC_SHA256` namespace als doelidentiteit wanneer uw bronnamespaces of `Email` of `Email_LC_SHA256` zijn.
* Selecteer `Phone_SHA256` namespace als doelidentiteit wanneer uw bronnamespaces of `PHONE_E.164` of `Phone_SHA256` zijn.
* Selecteer `IDFA` of `GAID` namespaces als doelidentiteit wanneer uw bronnamespaces `IDFA` of `GAID` zijn.
* Selecteer de naamruimte `Extern_ID` als doelidentiteit wanneer uw bronnaamruimte een aangepaste naamruimte is.

>[!IMPORTANT]
>
>Gegevens uit naamruimten zonder hashing worden na activering automatisch gehasht door [!DNL Platform].
> 
>Kenmerkbrongegevens worden niet automatisch gehasht. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om [!DNL Platform] de gegevens automatisch te laten hashen bij activering.

![Identiteitskaart](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

### Voorbeeld van toewijzing: publieksgegevens activeren in [!DNL Google Customer Match] {#example-gcm}

Dit is een voorbeeld van correcte identiteitstoewijzing wanneer het activeren van publieksgegevens in [!DNL Google Customer Match].

Bronvelden selecteren:

* Selecteer de naamruimte `Email` als bronidentiteit als de e-mailadressen die u gebruikt geen hashed zijn.
* Selecteer de naamruimte `Email_LC_SHA256` als bronidentiteit als u de e-mailadressen van de klant bij het invoeren van gegevens hebt gewijzigd in [!DNL Platform], volgens [!DNL Google Customer Match] [e-mailhashingvereisten](../catalog/social/../advertising/google-customer-match.md).
* Selecteer `PHONE_E.164` namespace als bronidentiteit als uw gegevens uit niet-gehakte telefoonaantallen bestaan. [!DNL Platform] hash de telefoonnummers om aan de  [!DNL Google Customer Match] vereisten te voldoen.
* Selecteer `Phone_SHA256_E.164` namespace als bronidentiteit als u telefoonaantallen op gegevensinvoer in [!DNL Platform], volgens [!DNL Facebook] [de vereisten van de het hakken van het telefoonaantal ](../catalog/social/../advertising/google-customer-match.md) hakt.
* Selecteer `IDFA` namespace als bronidentiteit als uw gegevens uit [!DNL Apple] apparaat IDs bestaan.
* Selecteer `GAID` namespace als bronidentiteit als uw gegevens uit [!DNL Android] apparaat IDs bestaan.
* Selecteer `Custom` namespace als bronidentiteit als uw gegevens uit ander type herkenningstekens bestaan.

Doelvelden selecteren:

* Selecteer `Email_LC_SHA256` namespace als doelidentiteit wanneer uw bronnamespaces of `Email` of `Email_LC_SHA256` zijn.
* Selecteer `Phone_SHA256_E.164` namespace als doelidentiteit wanneer uw bronnamespaces of `PHONE_E.164` of `Phone_SHA256_E.164` zijn.
* Selecteer `IDFA` of `GAID` namespaces als doelidentiteit wanneer uw bronnamespaces `IDFA` of `GAID` zijn.
* Selecteer de naamruimte `User_ID` als doelidentiteit wanneer uw bronnaamruimte een aangepaste naamruimte is.

![Identiteitskaart](../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Gegevens uit naamruimten zonder hashing worden na activering automatisch gehasht door [!DNL Platform].

Kenmerkbrongegevens worden niet automatisch gehasht. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om [!DNL Platform] de gegevens automatisch te laten hashen bij activering.

![Transformatie identiteitstoewijzing](../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Segmentexport plannen {#scheduling}

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

Controleer uw doelaccount. Als de activering is gelukt, worden de doelgroepen ingevuld in het doelplatform.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
