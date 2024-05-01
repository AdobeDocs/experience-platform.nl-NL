---
title: Het publiek activeren voor verpersoonlijkingsdoelen van randen
description: Leer hoe u het publiek activeert van Adobe Experience Platform naar Edge-verpersoonlijkingsbestemmingen voor gebruiksgevallen van verpersoonlijking op dezelfde pagina en op de volgende pagina.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: c113d9615a276af67714f38b8325e69737b23964
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---


# Het publiek activeren voor verpersoonlijkingsdoelen van randen

## Overzicht {#overview}

Adobe Experience Platform gebruikt [randsegmentatie](../../segmentation/ui/edge-segmentation.md) samen met [Edge-doelen](/help/destinations/destination-types.md#edge-personalization-destinations) om klanten in staat te stellen om op grote schaal, in real time, publiek te maken en te richten. Met deze functie kunt u gebruiksgevallen voor personalisatie op dezelfde pagina en op de volgende pagina configureren.

Voorbeelden van randbestemmingen zijn de [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) en de [Aangepaste personalisatie](../../destinations/catalog/personalization/custom-personalization.md) verbindingen.

>[!NOTE]
>
>Wanneer [configureren van Adobe Target-verbinding](../catalog/personalization/adobe-target-connection.md) *zonder* wanneer u een gegevensstroom-id gebruikt, worden de in dit artikel beschreven gebruiksgevallen niet ondersteund. Alleen de volgende-sessiegebruikstoepassingen worden ondersteund bij gebrek aan een gegevensstroom.

>[!IMPORTANT]
> 
> * Om gegevens te activeren en de [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
> * Gegevens activeren zonder de opdracht [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}
> 
> Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

In dit artikel wordt uitgelegd welke workflow is vereist om het publiek naar Adobe Experience Platform Edge-doelen te activeren. Indien samen gebruikt met [randsegmentatie](../../segmentation/ui/edge-segmentation.md) en de facultatieve [profielkenmerken toewijzen](#mapping)Met deze doelen kunnen gebruikers van dezelfde pagina en van de volgende pagina gebruikmaken van hoofdlettergebruik op uw web- en mobiele eigenschappen.

Bekijk de onderstaande video voor een kort overzicht van het configureren van de Adobe Target-verbinding voor &#39;edge personalization&#39;.

>[!NOTE]
>
>De gebruikersinterface van het Experience Platform wordt vaak bijgewerkt en kan sinds de opname van deze video zijn veranderd. Raadpleeg de configuratiestappen in de onderstaande secties voor de meest actuele informatie.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

Bekijk de onderstaande video voor een kort overzicht van hoe u doelgroepen en profielkenmerken kunt delen met Adobe Target en aangepaste verpersoonlijkingsdoelen.

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## Gebruiksscenario’s {#use-cases}

De oplossingen van de verpersoonlijking van de Adobe, zoals Adobe Target, of uw eigen platforms van de verpersoonlijkingspartner van het gebruik (bijvoorbeeld [!DNL Optimizely], [!DNL Pega]), en bedrijfseigen systemen (bijvoorbeeld in-house CMS) om een diepere klanterlokalisatie via de [Aangepaste personalisatie](../catalog/personalization/custom-personalization.md) bestemming. Dit alles terwijl ook de gegevensverzameling en segmenteringsmogelijkheden van de Edge Network van het Experience Platform worden gebruikt.

De hieronder beschreven gebruiksgevallen omvatten zowel personalisatie van de site als gerichte on-site reclame.

Om deze gebruiksgevallen mogelijk te maken, hebben klanten een snelle, gestroomlijnde manier nodig om zowel het publiek als de profielkenmerkinformatie van het Experience Platform op te halen, en deze informatie naar of [Adobe Target](../catalog/personalization/adobe-target-connection.md) of de [Aangepaste personalisatie](../catalog/personalization/custom-personalization.md) in de gebruikersinterface van het Experience Platform.

### Zelfde paginagrootte {#same-page}

Een gebruiker bezoekt een pagina van uw website. U kunt de huidige informatie van het paginabezoek (bijvoorbeeld verwijzend URL, browser taal, ingebedde productinfo) gebruiken om de volgende actie of de beslissing (bijvoorbeeld, verpersoonlijking) te selecteren, gebruikend [Aangepaste personalisatie](../catalog/personalization/custom-personalization.md) verbinding voor niet-Adobe platforms (bijvoorbeeld [!DNL Pega], [!DNL Optimizely] of andere.).

### Aanpassing van volgende pagina {#next-page}

Een gebruiker bezoekt pagina A op uw website. Gebaseerd op deze interactie, heeft de gebruiker voor een reeks publiek gekwalificeerd. De gebruiker klikt vervolgens op een koppeling die deze van pagina A naar pagina B verplaatst. Het publiek waarvoor de gebruiker tijdens de vorige interactie op pagina A in aanmerking was gekomen, samen met de profielupdates die door het huidige websitebezoek werden bepaald, zal worden gebruikt om de volgende actie of beslissing aan te sturen (bijvoorbeeld welke advertentiebanner aan de bezoeker moet worden getoond, of, in het geval van A/B-tests, welke versie van de pagina aan vertoning).

### Aanpassing van volgende sessie {#next-session}

Een gebruiker bezoekt verschillende pagina&#39;s op uw website. Op basis van deze interacties heeft de gebruiker zich gekwalificeerd voor een aantal soorten publiek. De gebruiker beëindigt dan de huidige het doorbladeren zitting.

De volgende dag keert de gebruiker terug naar dezelfde klantenwebsite. Het publiek waarvoor zij tijdens de vorige interactie met alle bezochte websitepagina&#39;s in aanmerking kwamen, samen met de profielupdates die door het huidige websitebezoek werden bepaald, zal worden gebruikt om de volgende actie/beslissing te selecteren (bijvoorbeeld welke advertentiebanner aan de bezoeker moet worden getoond, of, in het geval van A/B-tests, welke versie van de pagina moet worden getoond).

### Een banner voor een homepage aanpassen {#home-page-banner}

Een huisverhuurbedrijf en verkoopbedrijf willen hun homepage met een banner personaliseren, op basis van publiekskwalificaties in Adobe Experience Platform. Het bedrijf kan selecteren welk publiek een persoonlijke ervaring zou moeten krijgen en deze doelgroepen naar Adobe Target sturen als criteria voor hun Target-aanbieding.

## Vereisten {#prerequisites}

### Een gegevensstroom configureren in de gebruikersinterface voor gegevensverzameling {#configure-datastream}

De eerste stap in vestiging moet uw verpersoonlijkingsbestemming een gegevensstroom voor het Web SDK van het Experience Platform vormen. Dit wordt gedaan in de Inzameling UI van Gegevens.

Bij het configureren van de gegevensstroom, onder **[!UICONTROL Adobe Experience Platform]** ervoor zorgen dat beide **[!UICONTROL Edge Segmentation]** en **[!UICONTROL Personalization Destinations]** zijn geselecteerd.

>[!TIP]
>
>Vanaf de release van april 2024 hoeft u het selectievakje Edge Segmentation niet in te schakelen als [configureren van verbinding met Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md). In dit geval: [verpersoonlijking volgende sessie](#next-session) is het enige beschikbare geval van het verpersoonlijkingsgebruik.

![De configuratie van de datastream met de Onderverdeling van de Rand en Gemarkeerde Doelen van de Aanpassing!](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

Voor meer informatie over hoe u een gegevensstroom instelt, volgt u de instructies in het dialoogvenster [Platform Web SDK-documentatie](../../datastreams/configure.md#aep).

### Een [!DNL Active-On-Edge] samenvoegingsbeleid {#create-merge-policy}

Nadat u de doelverbinding hebt gemaakt, moet u een [!DNL Active-On-Edge] samenvoegbeleid. De [!DNL Active-On-Edge] samenvoegingsbeleid zorgt ervoor dat het publiek constant wordt geëvalueerd [op de rand](../../segmentation/ui/edge-segmentation.md) en zijn beschikbaar voor het gebruiksgeval van de verpersoonlijking in real time en volgende pagina.

>[!IMPORTANT]
>
>Op dit moment ondersteunen Edge-doelen alleen de activering van soorten publiek die gebruikmaken van de [Samenvoegingsbeleid actief op rand](../../segmentation/ui/segment-builder.md#merge-policies) ingesteld als standaard. Als u publiek in kaart brengt die een verschillend samenvoegbeleid aan randbestemmingen gebruiken, zullen die publiek niet worden geëvalueerd.

Volg de instructies op [samenvoegingsbeleid maken](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)en zorgt ervoor dat de **[!UICONTROL Active-On-Edge Merge Policy]** schakelen.

### Nieuw publiek maken in platform {#create-audience}

Nadat u het [!DNL Active-On-Edge] Samenvoegbeleid, moet u een nieuw publiek in Platform tot stand brengen.

Volg de [toeschouwers](../../segmentation/ui/segment-builder.md) gids om uw nieuw publiek te creëren, en zorg ervoor [toewijzen](../../segmentation/ui/segment-builder.md#merge-policies) de [!DNL Active-On-Edge] samenvoegbeleid dat u in de vorige stap hebt gemaakt.

### Een doelverbinding maken {#connect-destination}

Nadat u uw gegevensstroom hebt gevormd, kunt u beginnen uw verpersoonlijkingsbestemming te vormen.

Volg de [zelfstudie over het maken van doelverbinding](../ui/connect-destination.md) voor gedetailleerde instructies op hoe te om een nieuwe bestemmingsverbinding tot stand te brengen.

Afhankelijk van de bestemming die u vormt, verwijs naar de volgende artikelen voor bestemmings-specifieke eerste vereisten en verwante informatie:

* [Adobe Target-verbinding](../catalog/personalization/adobe-target-connection.md#parameters)
* [Aangepaste verpersoonlijkingsverbinding](../catalog/personalization/custom-personalization.md##parameters)

## Kies uw bestemming {#select-destination}

Nadat u de eerste vereisten hebt voltooid, kunt u nu de verpersoonlijkingsbestemming voor de aanpassing van dezelfde pagina en van de volgende pagina selecteren.

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Tabblad Doelcatalogus wordt gemarkeerd in de gebruikersinterface van het Experience Platform.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate audiences]** op de kaart die overeenkomt met de personalisatiebestemming waar u uw publiek wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Activeer de publiekscontrole die op een doelkaart in de catalogus wordt gemarkeerd.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw publiek te activeren en selecteer vervolgens **[!UICONTROL Next]**.

   ![Selecteer een doelstap in de activeringsworkflow.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Naar de volgende sectie gaan [uw publiek selecteren](#select-audiences).

## Uw publiek selecteren {#select-audiences}

Gebruik de selectievakjes links van de publieksnamen om het publiek te selecteren dat u wilt activeren naar het doel en selecteer vervolgens **[!UICONTROL Next]**.

Als u het publiek dat u wilt activeren naar het doel wilt selecteren, schakelt u het selectievakje links van de publieksnamen in en selecteert u **[!UICONTROL Next]**.

U kunt kiezen uit meerdere soorten publiek, afhankelijk van de oorsprong:

* **[!UICONTROL Segmentation Service]**: publiek dat binnen Experience Platform door de Dienst van de Segmentatie wordt geproduceerd. Zie de [segmentatiedocumentatie](../../segmentation/ui/overview.md) voor meer informatie .
* **[!UICONTROL Custom upload]**: Soorten publiek dat buiten het Experience Platform is gegenereerd en als CSV-bestanden naar Platform is geüpload. Raadpleeg de documentatie over [een publiek importeren](../../segmentation/ui/overview.md#import-audience).
* Andere soorten soorten publiek, afkomstig van andere oplossingen voor Adobe, zoals [!DNL Audience Manager].

![Selecteer de stap voor het publiek van de activeringsworkflow met een aantal gemarkeerde soorten publiek.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## Kenmerken Kaart {#mapping}

>[!IMPORTANT]
>
>Profielkenmerken kunnen vertrouwelijke gegevens bevatten. Om deze gegevens te beschermen, **[!UICONTROL Custom Personalization]** doel vereist dat u de [Edge Network Server-API](../../server-api/overview.md) wanneer het vormen van de bestemming voor op attribuut-gebaseerde verpersoonlijking. Alle API-aanroepen van de server moeten in een [geverifieerde context](../../server-api/authentication.md).
>
><br>Als u reeds SDK van het Web of Mobiele SDK voor uw integratie gebruikt, kunt u attributen via de Server API terugwinnen door een server-zijintegratie toe te voegen.
>
><br>Als u de bovenstaande vereisten niet opvolgt, wordt de personalisatie alleen gebaseerd op het lidmaatschap van het publiek.

Selecteer de kenmerken op basis waarvan u gebruiksgevallen voor personalisatie voor uw gebruikers wilt inschakelen. Dit betekent dat als de waarde van een attribuut verandert of als een attribuut aan een profiel wordt toegevoegd, dat profiel een lid van het publiek zal worden en aan de verpersoonlijkingsbestemming zal worden geactiveerd.

Het toevoegen van kenmerken is optioneel en u kunt doorgaan naar de volgende stap en personalisatie op dezelfde pagina en op de volgende pagina inschakelen zonder kenmerken te selecteren. Als u in deze stap geen kenmerken toevoegt, vindt er nog steeds personalisatie plaats op basis van het lidmaatschap van het publiek en de kwalificaties van het identiteitsoverzicht voor profielen.

![Afbeelding waarin de toewijzingsstap wordt weergegeven terwijl een kenmerk is geselecteerd.](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### Bronkenmerken selecteren {#select-source-attributes}

Als u bronkenmerken wilt toevoegen, selecteert u de **[!UICONTROL Add new field]** controle op de **[!UICONTROL Source field]** kolom en zoek of navigeer naar het gewenste XDM-kenmerkveld, zoals hieronder wordt weergegeven.

![Schermopname die laat zien hoe u een doelkenmerk in de toewijzingsstap selecteert.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### Doelkenmerken selecteren {#select-target-attributes}

Als u doelkenmerken wilt toevoegen, selecteert u de **[!UICONTROL Add new field]** controle op de **[!UICONTROL Target field]** kolom en typ in de naam van het aangepaste kenmerk waaraan u het bronkenmerk wilt toewijzen.

>[!NOTE]
>
>De selectie van doelkenmerken is alleen van toepassing op [Aangepaste personalisatie](../catalog/personalization/custom-personalization.md) activeringswerkstroom, voor ondersteuning van veldtoewijzing met vriendelijke namen op het doelplatform.

![Schermopname die laat zien hoe een XDM-kenmerk in de toewijzingsstap moet worden geselecteerd](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## Het exporteren van publiek plannen {#scheduling}

Standaard worden de [!UICONTROL Audience schedule] op de pagina worden alleen de onlangs geselecteerde doelgroepen weergegeven die u in de huidige activeringsstroom hebt gekozen.

Als u alle soorten publiek wilt zien die op uw doel worden geactiveerd, gebruikt u de filteroptie en schakelt u de optie **[!UICONTROL Show new audiences only]** filter.

![Alle doelfilters zijn gemarkeerd.](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

Op de **[!UICONTROL Audience schedule]** pagina, selecteert u elk publiek en gebruikt u vervolgens de **[!UICONTROL Start date]** en **[!UICONTROL End date]** selecteurs om het tijdinterval voor het verzenden van gegevens naar uw bestemming te vormen.

![Stap in het schema voor het publiek van de activeringsworkflow met de begin- en einddatum gemarkeerd.](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

Selecteren **[!UICONTROL Next]** om naar de [!UICONTROL Review] pagina.

## Controleren {#review}

Op de **[!UICONTROL Review]** , kunt u een overzicht van uw selectie zien. Selecteren **[!UICONTROL Cancel]** om de stroom op te delen, **[!UICONTROL Back]** om uw instellingen te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

![Selectieoverzicht in de revisiestap.](../assets/ui/activate-edge-personalization-destinations/review.png)

### Goedkeuring van het beleid {#consent-policy-evaluation}

Als uw organisatie is aangeschaft **Adobe Gezondheidsschild** of **Privacy- en beveiligingsschild van Adobe**, selecteert u **[!UICONTROL View applicable consent policies]** na te gaan welk toestemmingsbeleid wordt toegepast en hoeveel profielen als gevolg daarvan in de activering worden opgenomen. Meer informatie [goedkeuring beleidsevaluatie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) voor meer informatie .

### Controle van het gegevensgebruiksbeleid {#data-usage-policy-checks}

In de **[!UICONTROL Review]** stap, controleert het Experience Platform ook om het even welke schendingen van het beleid van het gegevensgebruik. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor publieksactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe u beleidsovertredingen kunt oplossen, leest u informatie over [beleidsovertredingen voor gegevensgebruik](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) in de sectie Documentatie inzake gegevensbeheer.

![Een voorbeeld van een schending van een gegevensbeleid.](../assets/common/data-policy-violation.png)

### Filter publiek {#filter-audiences}

In deze stap kunt u de beschikbare filters op de pagina gebruiken om alleen de doelgroepen weer te geven waarvan het schema of de toewijzing is bijgewerkt als onderdeel van deze workflow. U kunt ook schakelen welke tabelkolommen u wilt zien.

![De opname van het scherm die de beschikbare publieksfilters in de overzichtsstap toont.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

Als u tevreden bent met de selectie en er zijn geen beleidsovertredingen vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
