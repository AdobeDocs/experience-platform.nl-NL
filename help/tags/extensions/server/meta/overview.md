---
title: Overzicht van Meta Conversions API
description: Meer informatie over de Meta Conversions API extensie voor het doorsturen van gebeurtenissen in Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2437'
ht-degree: 0%

---

# [!DNL Meta Conversions API] overzicht van extensies

Met [[!DNL Meta Conversions API] ](https://developers.facebook.com/docs/marketing-api/conversions-api/) kunt u uw marketinggegevens aan de serverzijde verbinden met [!DNL Meta] -technologieën om uw advertentie te optimaliseren, de kosten per actie te verlagen en de resultaten te meten. Gebeurtenissen zijn gekoppeld aan een [[!DNL Meta Pixel] ](https://developers.facebook.com/docs/meta-pixel/) -id en worden op dezelfde manier verwerkt als gebeurtenissen aan de clientzijde.

Gebruikend de [!DNL Meta Conversions API] uitbreiding, kunt u hefboomwerking de mogelijkheden van API in uw [ gebeurtenis door:sturen ](../../../ui/event-forwarding/overview.md) regels om gegevens naar [!DNL Meta] van Adobe Experience Platform Edge Network te verzenden. Dit document behandelt hoe te om de uitbreiding te installeren en zijn mogelijkheden in een gebeurtenis te gebruiken die [ regel ](../../../ui/managing-resources/rules.md) door:sturen.

## Demo

De volgende video is bedoeld om uw begrip van [!DNL Meta Conversions API] te steunen.

>[!VIDEO](https://unlockmarketingdata.com/video-meta-conversions-api)

## Vereisten

Het wordt ten zeerste aanbevolen om [!DNL Meta Pixel] en [!DNL Conversions API] te gebruiken om dezelfde gebeurtenissen te delen en te verzenden vanaf respectievelijk de client en de server, aangezien dit ertoe kan bijdragen dat gebeurtenissen worden hersteld die niet door [!DNL Meta Pixel] zijn opgehaald. Alvorens de [!DNL Conversions API] uitbreiding te installeren, zie de gids op de [[!DNL Meta Pixel]  uitbreiding ](../../client/meta/overview.md) voor stappen op hoe te om het in uw cliënt-zijmarkeringsimplementaties te integreren.

>[!NOTE]
>
>De sectie op [ gebeurtenisdeduplicatie ](#deduplication) later in dit document behandelt de stappen om de zelfde gebeurtenis te verzekeren niet tweemaal wordt gebruikt, aangezien het van zowel browser als de server kan worden ontvangen.

Als u de extensie [!DNL Conversions API] wilt gebruiken, hebt u toegang tot het doorsturen van gebeurtenissen en hebt u een geldige [!DNL Meta] -account met toegang tot [!DNL Ad Manager] en [!DNL Event Manager] . Specifiek, moet u identiteitskaart van bestaande [[!DNL Meta Pixel] kopiëren ](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (of [ creeer een nieuw  [!DNL Pixel] ](https://www.facebook.com/business/help/952192354843755) in plaats daarvan) zodat kan de uitbreiding aan uw rekening worden gevormd.

>[!INFO]
>
>Als u van plan bent om deze uitbreiding met mobiele toepassingsgegevens te gebruiken, of als u ook met off-line gebeurtenisgegevens in uw [!DNL Meta] campagnes werkt, zult u uw dataset door bestaande app moeten creëren en **selecteren creeert van een pixelidentiteitskaart** wanneer ertoe aangezet. Zie artikel [ beslissen welke optie van de datasetverwezenlijking juist voor uw zaken ](https://www.facebook.com/business/help/5270377362999582?id=490360542427371) voor details is. Verwijs naar [ Conversies API voor de Gebeurtenissen van de App ](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) document voor alle vereiste en facultatieve app het volgen parameters.

## De extensie installeren

Als u de extensie [!DNL Meta Conversions API] wilt installeren, navigeert u naar de gebruikersinterface van de gegevensverzameling of de gebruikersinterface van Experience Platform en selecteert u **[!UICONTROL Event Forwarding]** in de linkernavigatie. Selecteer van hieruit een eigenschap waaraan u de extensie wilt toevoegen of maak een nieuwe eigenschap.

Wanneer u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie en selecteert u vervolgens de tab **[!UICONTROL Catalog]** . Zoek de [!UICONTROL Meta Conversions API] -kaart en selecteer vervolgens **[!UICONTROL Install]** .

![ de [!UICONTROL Install] optie die voor de [!UICONTROL Meta Conversions API] uitbreiding in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/meta/install.png)

In de configuratieweergave die wordt weergegeven, moet u de [!DNL Pixel] id opgeven die u eerder hebt gekopieerd om de extensie te koppelen aan uw account. U kunt de id rechtstreeks in de invoer plakken, maar u kunt ook een gegevenselement gebruiken.

U moet ook een toegangstoken verstrekken om [!DNL Conversions API] specifiek te gebruiken. Verwijs naar de [!DNL Conversions API] documentatie over [ het produceren van een toegangstoken ](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) voor stappen op hoe te om deze waarde te verkrijgen.

Selecteer **[!UICONTROL Save]** wanneer u klaar bent

![ identiteitskaart [!DNL Pixel] als gegevenselement in de mening van de uitbreidingsconfiguratie wordt verstrekt die.](../../../images/extensions/server/meta/configure.png)

De uitbreiding is geïnstalleerd en u kunt zijn mogelijkheden in uw gebeurtenis nu gebruiken die regels door:sturen.

## Integratie met de extensie Facebook en Instagram {#facebook}

Dankzij de integratie met de extensie Facebook en Instagram kunt u snel verifiëren bij uw Meta Business Account. Vervolgens worden de [!UICONTROL Pixel ID] en de Meta Conversions API [!UICONTROL Access Token] automatisch ingevuld, zodat de Meta Conversions API eenvoudiger kan worden geïnstalleerd en geconfigureerd.

Wanneer u de extensie [!UICONTROL Meta Conversions API] installeert, wordt er een dialoogvenster weergegeven waarin u wordt gevraagd om verificatie op Facebook en Instagram uit te voeren.

![ de [!UICONTROL Meta Conversions API Extension] installatiepagina die [!UICONTROL Connect to Meta] benadrukt.](../../../images/extensions/server/meta/mbe-extension-install.png)

Er wordt ook een dialoogvenster weergegeven met de vraag of verificatie op Facebook en Instagram moet worden uitgevoerd. Dit wordt ook weergegeven in de gebruikersinterface van de snelstartworkflow wanneer gebeurtenissen worden doorgestuurd.

![ Snelle het begin werkschema UI die [!UICONTROL Connect to Meta] benadrukt.](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## Integratie met Event Quality Match Score (EMQ) {#emq}

Dankzij de integratie met de Event Quality Match Score (EMQ) kunt u de doeltreffendheid van uw implementatie eenvoudig bekijken door de EMQ-scores weer te geven. Deze integratie minimaliseert contextomschakeling en helpt u het succes van uw Meta Conversions API implementaties te verbeteren. Deze gebeurtenissencores worden weergegeven in het configuratiescherm van [!UICONTROL Meta Conversions API extension] .

![ de [!UICONTROL Meta Conversions API Extension] configuratiepagina die [!UICONTROL View EMQ Score] benadrukt.](../../../images/extensions/server/meta/emq-score.png)

## Integratie met LiveRamp (Alpha) {#alpha}

[!DNL LiveRamp] klanten die [!DNL LiveRamp] voor authentiek verklaarde Oplossing van het Verkeer (ATS) op hun plaatsen hebben opgesteld kunnen verkiezen om RampIDs als parameter van de klanteninformatie te delen. Werk samen met uw [!DNL Meta] -accountteam om deel te nemen aan het Alpha-programma voor deze functie.

![ de gebeurtenis die van Meta [!UICONTROL Rule] configuratiepagina [!UICONTROL Partner Name (alpha)] en [!UICONTROL Partner ID (alpha)] door:sturen.](../../../images/extensions/server/meta/live-ramp.png)

## Vorm een gebeurtenis door:sturen regel {#rule}

Deze sectie behandelt hoe te om de [!DNL Conversions API] uitbreiding in een generische gebeurtenis te gebruiken die regel door:sturen. In praktijk, zou u verscheidene regels moeten vormen om alle toegelaten [ standaardgebeurtenissen ](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] en [!DNL Conversions API] te verzenden. Voor mobiele toepassingsgegevens, gelieve te zien de vereiste gebieden, de gebieden van toepassingsgegevens, de parameters van de klanteninformatie, en de details van douanegegevens [ hier ](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events).

>[!NOTE]
>
>De gebeurtenissen zouden [ moeten worden verzonden in echt - tijd ](https://www.facebook.com/business/help/379226453470947?id=818859032317965) of zo dicht bij echt - tijd zoals mogelijk voor betere en campagneroptimalisering.

Begin creërend een nieuwe gebeurtenis door:sturen regel en vorm zijn voorwaarden zoals gewenst. Wanneer u de handelingen voor de regel selecteert, selecteert u **[!UICONTROL Meta Conversions API Extension]** voor de extensie en selecteert u **[!UICONTROL Send Conversions API Event]** voor het actietype.

![ het [!UICONTROL Send Page View] actietype dat voor een regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/meta/select-action.png)

Er worden besturingselementen weergegeven waarmee u de gebeurtenisgegevens kunt configureren die via [!DNL Meta] naar [!DNL Conversions API] worden verzonden. Deze opties kunnen rechtstreeks in de verstrekte input worden ingevoerd, of u kunt bestaande gegevenselementen selecteren om de waarden te vertegenwoordigen. De configuratieopties worden verdeeld in vier hoofdsecties, zoals hieronder beschreven.

| Config-sectie | Beschrijving |
| --- | --- |
| [!UICONTROL Server Event Parameters] | Algemene informatie over de gebeurtenis, waaronder de tijd dat deze heeft plaatsgevonden en de bronactie die deze heeft geactiveerd. Verwijs naar de [!DNL Meta] ontwikkelaarsdocumentatie voor meer informatie over de [ standaardgebeurtenisparameters ](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) die door [!DNL Conversions API] worden goedgekeurd.<br><br> als u zowel [!DNL Meta Pixel] als [!DNL Conversions API] gebruikt om gebeurtenissen te verzenden, zorg ervoor om zowel **[!UICONTROL Event Name]** (`event_name`) als **[!UICONTROL Event ID]** (`event_id`) met elke gebeurtenis te omvatten, aangezien deze waarden voor [ gebeurtenisdeduplicatie ](#deduplication) worden gebruikt.<br><br> u hebt ook de optie aan **[!UICONTROL Enable Limited Data Use]** om te helpen aan klant opt-outs voldoen. Zie de [!DNL Conversions API] documentatie over [ gegevens verwerkend opties ](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) voor details op deze eigenschap. |
| [!UICONTROL Customer Information Parameters] | De identiteitsgegevens van de gebruiker die worden gebruikt om de gebeurtenis aan een klant toe te schrijven. Sommige van deze waarden moeten worden gehasht voordat ze naar de API kunnen worden verzonden.<br><br> om een goede gemeenschappelijke API verbinding en de hoge kwaliteit van de gebeurtenisgelijke (EMQ) te verzekeren, wordt het geadviseerd dat u alle [ toegelaten parameters van de klanteninformatie ](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) naast servergebeurtenissen verzendt. Deze parameters zouden ook [ moeten worden geprioriteerd gebaseerd op hun belang en effect op EMQ ](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Custom Data] | Aanvullende gegevens die moeten worden gebruikt voor optimalisatie van levering voor advertenties, opgegeven in de vorm van een JSON-object. Verwijs naar de [[!DNL Conversions API]  documentatie ](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) voor meer informatie over de toegelaten eigenschappen voor dit voorwerp.<br><br> Als u een aankoopgebeurtenis verzendt, moet u deze sectie gebruiken om de vereiste attributen `currency` en `value` te verstrekken. |
| [!UICONTROL Test Event] | Deze optie wordt gebruikt om te controleren of uw configuratie ertoe leidt dat servergebeurtenissen door [!DNL Meta] worden ontvangen zoals verwacht. Als u deze functie wilt gebruiken, schakelt u het selectievakje **[!UICONTROL Send as Test Event]** in en geeft u een gewenste testgebeurteniscode op in de onderstaande invoer. Zodra de gebeurtenis door:sturen regel wordt opgesteld, als u de uitbreiding en de actie correct vormde zou u activiteiten moeten zien die binnen de **[!DNL Test Events]** mening in [!DNL Meta Events Manager] verschijnen. |

{style="table-layout:auto"}

Als u klaar bent, selecteert u **[!UICONTROL Keep Changes]** om de handeling aan de regelconfiguratie toe te voegen.

![[!UICONTROL Keep Changes] die voor de actieconfiguratie worden geselecteerd.](../../../images/extensions/server/meta/keep-changes.png)

Selecteer **[!UICONTROL Save to Library]** als u tevreden bent met de regel. Tot slot publiceer een nieuwe gebeurtenis door:sturen [ bouwt ](../../../ui/publishing/builds.md) om de veranderingen toe te laten die aan de bibliotheek worden aangebracht.

## Gebeurtenisdeduplicatie {#deduplication}

Zoals vermeld in de [ eerste vereisten sectie ](#prerequisites), adviseert men dat u zowel de [!DNL Meta Pixel] markeringsuitbreiding als [!DNL Conversions API] gebeurtenis gebruikt die uitbreiding door:sturen om de zelfde gebeurtenissen van de cliënt en de server in een overtollige opstelling te verzenden. Dit kan helpen gebeurtenissen herstellen die niet door één of andere uitbreiding werden opgepikt.

Als u verschillende gebeurtenistypen verzendt van de client en de server zonder overlapping tussen beide, is deduplicatie niet nodig. Als echter één gebeurtenis wordt gedeeld door zowel [!DNL Meta Pixel] als [!DNL Conversions API] , moet u ervoor zorgen dat deze overbodige gebeurtenissen worden gededupliceerd, zodat de rapportage niet wordt beïnvloed.

Wanneer u gedeelde gebeurtenissen verzendt, moet u een gebeurtenis-id en een naam opnemen voor elke gebeurtenis die u verzendt van zowel de client als de server. Wanneer meerdere gebeurtenissen met dezelfde id en naam worden ontvangen, gebruikt [!DNL Meta] automatisch verschillende strategieën om deze te dedupliceren en de meest relevante gegevens te behouden. Zie de [!DNL Meta] documentatie over [ deduplicatie voor  [!DNL Meta Pixel]  en  [!DNL Conversions API]  gebeurtenissen ](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) voor details op dit proces.

## Snelle startworkflow: Meta Conversions API Extension (Beta) {#quick-start}

>[!IMPORTANT]
>
>* De functie Snel starten is beschikbaar voor klanten die het pakket Real-Time CDP Prime en Ultimate hebben aangeschaft. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie.
>* Deze eigenschap is voor netto nieuwe implementaties en steunt momenteel niet auto installerende uitbreidingen en configuraties op bestaande markeringen en gebeurtenis die eigenschappen door:sturen.

>[!NOTE]
>
>Om het even welke bestaande cliënt kan de snelstartwerkschema&#39;s gebruiken om een verwijzings implementatie tot stand te brengen die voor het volgende kan worden gebruikt:
>
>* Gebruik dit als het begin van een gloednieuwe implementatie.
>* Haal voordeel uit het als verwijzingsimplementatie die u kunt onderzoeken om te zien hoe het is gevormd en dan in uw huidige productieimplementaties repliceert.

Met de functie Snel starten kunt u eenvoudig en efficiënt werken met de Meta Conversies API en de Meta Pixel-extensies. Met dit gereedschap worden meerdere stappen geautomatiseerd die worden uitgevoerd in Adobe-tags en het doorsturen van gebeurtenissen, waardoor de installatietijd aanzienlijk korter wordt.

Deze functie installeert en configureert automatisch de Meta Conversies API en de Meta Pixel-extensies op een nieuw automatisch gegenereerde tag en eigenschap voor het doorsturen van gebeurtenissen met de vereiste regels en gegevenselementen. Bovendien installeert en configureert het automatisch de Experience Platform Web SDK en DataStream. Tot slot publiceert de functie Snel starten de bibliotheek automatisch naar de opgegeven URL in een ontwikkelomgeving, waardoor gegevensverzameling aan de clientzijde en gebeurtenisdoorsturen aan de serverzijde in real-time mogelijk zijn via Event Forwarding en Experience Platform Edge Network.

In de volgende video wordt een inleiding gegeven op de functie Snel starten.

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### Snelstartfunctie installeren

>[!NOTE]
>
>Deze eigenschap wordt ontworpen om u te helpen begonnen met een gebeurtenis door:sturen implementatie. Het zal geen eind-aan-eind, volledig functionele implementatie leveren die alle gebruiksgevallen aanpast.

Deze setup wordt automatisch uitgevoerd om zowel de Meta Conversies-API als de Meta Pixel-extensies te installeren. Deze hybride implementatie wordt door Meta aanbevolen voor het verzamelen en doorsturen van de serverzijde van conversies van gebeurtenissen.
De snelle opstellingseigenschap wordt ontworpen om klanten te helpen met een gebeurtenis beginnen die implementatie door:sturen en is niet bedoeld om een eind aan eind te leveren, volledig functionele implementatie die alle gebruiksgevallen aanpast.

Selecteer **[!UICONTROL Get Started]** voor **[!DNL Send Conversions Data to Meta]** op de pagina Adobe Experience Platform Data Collection **[!UICONTROL Home]** om de functie te installeren.

![ de homepage van de inzameling van Gegevens die omzettingsgegevens in meta tonen ](../../../images/extensions/server/meta/conversion-data-to-meta.png)

Voer uw **[!UICONTROL Domain]** in en selecteer vervolgens **[!UICONTROL Next]** . Dit domein zal als noemende overeenkomst voor uw auto geproduceerde Markeringen en Gebeurtenis worden gebruikt die eigenschappen, regels, gegevenselementen, gegevensstromen, etc. door:sturen.

![ Welkome scherm die domeinnaam verzoeken ](../../../images/extensions/server/meta/welcome.png)

Voer in het dialoogvenster **[!UICONTROL Initial Setup]** de opties **[!UICONTROL Meta Pixel ID]** , **[!UICONTROL Meta Conversion API Access Token]** en **[!UICONTROL Data Layer Path]** in en selecteer vervolgens **[!UICONTROL Next]** .

![ Aanvankelijke opstellingsdialoog ](../../../images/extensions/server/meta/initial-setup.png)

Wacht enkele minuten tot het initiële installatieproces is voltooid en selecteer vervolgens **[!UICONTROL Next]** .

![ Aanvankelijke opstelling voltooide bevestigingsscherm ](../../../images/extensions/server/meta/setup-complete.png)

Van de **[!UICONTROL Add Code on Your Site]** dialoog kopieert de code die wordt verstrekt gebruikend de functie van het exemplaar ![ Exemplaar ](/help/images/icons/copy.png) en kleeft dit in `<head>` van uw bronwebsite. Selecteer na implementatie **[!UICONTROL Start Validation]**

![ voeg code op uw plaatsdialoog toe ](../../../images/extensions/server/meta/add-code-on-your-site.png)

Het dialoogvenster [!UICONTROL Validation Results] geeft de resultaten van de Meta-extensie-implementatie weer. Selecteer **[!UICONTROL Next]**. U kunt ook aanvullende validatieresultaten zien door de koppeling **[!UICONTROL Assurance]** te selecteren.

![ de resultatendialoog van de Test tonend implementatieresultaten ](../../../images/extensions/server/meta/test-results.png)

De schermweergave van **[!UICONTROL Next Steps]** bevestigt de voltooiing van de installatie. Van hieruit hebt u de optie om uw implementatie te optimaliseren door nieuwe gebeurtenissen toe te voegen, die in de volgende sectie worden getoond.

Selecteer **[!UICONTROL Close]** als u geen aanvullende gebeurtenissen wilt toevoegen.

![ Volgende stappen dialoog ](../../../images/extensions/server/meta/next-steps.png)

#### Extra gebeurtenissen toevoegen

Selecteer **[!UICONTROL Edit Your Tags Web Property]** als u nieuwe gebeurtenissen wilt toevoegen.

![ Volgende stappen dialoog tonen uitgeeft uw bezit van het markeringenWeb ](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

Selecteer de regel die overeenkomt met de meta-gebeurtenis die u wilt bewerken. Bijvoorbeeld, **MetaConversion_AddToCart**.

>[!NOTE]
>
>Als er geen gebeurtenis is, zal deze regel niet lopen. Dit is waar voor alle regels, met **MetaConversion_PageView** regel die de uitzondering is.

Als u een gebeurtenis wilt toevoegen, selecteert u **[!UICONTROL Add]** onder de kop [!UICONTROL Events] .

![ de eigenschappenpagina die van de Markering geen gebeurtenissen toont ](../../../images/extensions/server/meta/edit-rule.png)

Selecteer het [!UICONTROL Event Type]. In dit voorbeeld, hebben wij de [!UICONTROL Click] gebeurtenis geselecteerd en het gevormd om te teweegbrengen wanneer **.add-to-cart-button** wordt geselecteerd. Selecteer **[!UICONTROL Keep Changes]**.

![ het configuratiescherm dat van de Gebeurtenis toont gebeurtenis ](../../../images/extensions/server/meta/event-configuration.png)

De nieuwe gebeurtenis is opgeslagen. Selecteer **[!UICONTROL Select a working library]** en selecteer de bibliotheek die u wilt maken.

![ Uitgezocht een werkende bibliotheekdaling onderaan ](../../../images/extensions/server/meta/working-library.png)

Selecteer vervolgens de vervolgkeuzelijst naast **[!UICONTROL Save to Library]** en selecteer **[!UICONTROL Save to Library and Build]** . Hiermee wordt de wijziging in de bibliotheek gepubliceerd.

![ Uitgezocht sparen aan bibliotheek en bouwt ](../../../images/extensions/server/meta/save-and-build.png)

Herhaal deze stappen voor elke andere meta-omzettingsgebeurtenis u zou willen vormen.

#### Configuratie van gegevenslaag {#configuration}

>[!IMPORTANT]
>
>De manier waarop u deze algemene gegevenslaag bijwerkt, is afhankelijk van uw websitearchitectuur. Een toepassing op één pagina verschilt van een renderingtoepassing op de server. Het is ook mogelijk dat u volledig verantwoordelijk bent voor het maken en bijwerken van deze gegevens in het product Tags. In alle gevallen moet de gegevenslaag worden bijgewerkt tussen het uitvoeren van elk van de `MetaConversion_* rules` . Als u de gegevens niet bijwerkt tussen regels, kunt u ook in een geval lopen waarin u gegevens van de laatste `MetaConversion_* rule` in de huidige `MetaConversion_* rule` verzendt.

Tijdens de configuratie, werd u gevraagd waar uw gegevenslaag leeft. Standaard is dit `window.dataLayer.meta` en binnen het `meta` -object worden uw gegevens verwacht zoals hieronder wordt weergegeven.

![ de meta-informatie van de laag van Gegevens ](../../../images/extensions/server/meta/data-layer-meta.png)

Dit is belangrijk om te begrijpen, aangezien elke `MetaConversion_*` -regel deze gegevensstructuur gebruikt om de relevante gegevens door te geven aan de [!DNL Meta Pixel] -extensie en aan [!DNL Meta Conversions API] . Verwijs naar de documentatie over [ standaardgebeurtenissen ](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) voor meer informatie over welke gegevens de verschillende meta gebeurtenissen vereisen.

Bijvoorbeeld, als u de `MetaConversion_Subscribe` regel wilde gebruiken, zou u `window.dataLayer.meta.currency` moeten bijwerken, `window.dataLayer.meta.predicted_ltv`, en `window.dataLayer.meta.value` volgens de objecten eigenschappen die in de documentatie over [ worden beschreven standaardgebeurtenissen ](https://developers.facebook.com/docs/meta-pixel/reference#standard-events).

Hieronder ziet u een voorbeeld van wat er op een website moet worden uitgevoerd om de gegevenslaag bij te werken voordat de regel wordt uitgevoerd.

![ de meta-informatie van de de gegevenslaag van de Update ](../../../images/extensions/server/meta/update-data-layer-meta.png)

Standaard wordt de `<datalayerpath>.conversionData.eventId` willekeurig gegenereerd door de actie Nieuwe gebeurtenis-id genereren voor een van de `MetaConversion_* rules` .

Voor een lokale verwijzing naar hoe de gegevenslaag eruit zou moeten zien, kunt u de redacteur van de douanecode op het `MetaConversion_DataLayer` gegevenselement op uw bezit openen.

## Volgende stappen

In deze handleiding wordt beschreven hoe u gebeurtenisgegevens aan de serverzijde naar [!DNL Meta] kunt verzenden met de extensie [!DNL Meta Conversions API] . Het wordt aanbevolen om vanaf hier uw integratie uit te breiden door meer [!DNL Pixels] aan te sluiten en meer gebeurtenissen te delen, indien van toepassing. Voer een van de volgende twee handelingen uit om uw advertentieprestaties verder te verbeteren:

* Sluit andere [!DNL Pixels] -bestanden aan die nog niet zijn verbonden met een [!DNL Conversions API] -integratie.
* Als u bepaalde gebeurtenissen uitsluitend via [!DNL Meta Pixel] op de client verzendt, moet u deze gebeurtenissen ook vanaf de server naar [!DNL Conversions API] verzenden.

Zie de [!DNL Meta] documentatie over [ beste praktijken voor  [!DNL Conversions API] ](https://www.facebook.com/business/help/308855623839366?id=818859032317965) voor meer begeleiding op hoe te om uw integratie effectief uit te voeren. Voor meer algemene informatie over markeringen en gebeurtenis die in Adobe Experience Cloud door:sturen, verwijs naar het [ overzicht van markeringen ](../../../home.md).
