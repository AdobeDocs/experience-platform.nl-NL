---
keywords: activeer profiel verzoek bestemmingen;activeer gegevens;profiel verzoek bestemmingen
title: De publieksgegevens van de activering aan de bestemmingen van het profielverzoek
type: Tutorial
description: Leer hoe te om de publieksgegevens te activeren u in Adobe Experience Platform hebt door segmenten aan de bestemmingen van het profielverzoek in kaart te brengen.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 811aba50fb4509e77910499f8d01c4bc13d06841
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# De publieksgegevens van de activering aan de bestemmingen van het profielverzoek

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist voor het activeren van publieksgegevens in Adobe Experience Platform-profielen voor aanvraagdoelen. Indien samen gebruikt met [randsegmentatie](../../segmentation/ui/edge-segmentation.md)Met deze doelen kunnen gebruikers van dezelfde pagina en van de volgende pagina gebruikmaken van hoofdlettergebruik op uw web- en mobiele eigenschappen. Meer informatie over [het toelaten van zelfde pagina en volgende-pagina verpersoonlijkingsgebruiksgevallen](/help/destinations/ui/configure-personalization-destinations.md).

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

### Bronkenmerken selecteren {#select-source-attributes}

Als u bronkenmerken wilt toevoegen, selecteert u de optie **[!UICONTROL Add new field]** controle op de **[!UICONTROL Source field]** kolom en zoek of navigeer naar het gewenste XDM-kenmerkveld, zoals hieronder wordt weergegeven.

![Schermopname die laat zien hoe u een doelkenmerk in de toewijzingsstap selecteert](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

### Doelkenmerken selecteren {#select-target-attributes}

>[!NOTE]
>
>Sommige bestemmingen vereisen u om bronattributen slechts te selecteren, terwijl anderen zowel bron als doelattributen vereisen.
>
>Op dit moment worden de [Adobe Target V2](../catalog/personalization/adobe-target-connection.md) doel vereist alleen bronkenmerken, terwijl [Aangepaste aanpassing met kenmerken](../catalog/personalization/custom-personalization.md) vereist zowel bron- als doelkenmerken.

Als u doelkenmerken wilt toevoegen, selecteert u de optie **[!UICONTROL Add new field]** controle op de **[!UICONTROL Target field]** kolom en typ in de naam van het aangepaste kenmerk waaraan u het bronkenmerk wilt toewijzen.

![Schermopname die laat zien hoe een XDM-kenmerk in de toewijzingsstap moet worden geselecteerd](../assets/ui/activate-profile-request-destinations/mapping-step-select-target-attribute.gif)

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

![Selectieoverzicht in de revisiestap.](../assets/ui/activate-profile-request-destinations/review.png)

### Goedkeuring van het beleid {#consent-policy-evaluation}

Als uw organisatie is aangeschaft **Adobe Healthcare Shield** of **Adobe Privacy- en beveiligingsschild**, selecteert u **[!UICONTROL View applicable consent policies]** na te gaan welk toestemmingsbeleid wordt toegepast en hoeveel profielen als gevolg daarvan in de activering worden opgenomen. Meer informatie [goedkeuring beleidsevaluatie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) voor meer informatie .

### Controle van het gegevensgebruiksbeleid {#data-usage-policy-checks}

In de **[!UICONTROL Review]** stap, controleert het Experience Platform ook om het even welke schendingen van het beleid van het gegevensgebruik. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe u beleidsovertredingen kunt oplossen, raadpleegt u [beleidsovertredingen voor gegevensgebruik](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) in de sectie Documentatie inzake gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

### Segmenten filteren {#filter-segments}

In deze stap kunt u ook de beschikbare filters op de pagina gebruiken om alleen de segmenten weer te geven waarvan het schema of de toewijzing is bijgewerkt als onderdeel van deze workflow. U kunt ook schakelen welke tabelkolommen u wilt zien.

![De opname van het scherm die de beschikbare segmentfilters in de overzichtsstap toont.](/help/destinations/assets/ui/activate-profile-request-destinations/filter-segments-review-step.gif)

Als u tevreden bent met de selectie en er zijn geen beleidsovertredingen vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->