---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: Een AI-instantie van de klant configureren
topic: Instance creation
translation-type: tm+mt
source-git-commit: ec0de4c8775367be9e6016529471254ad9f8f453

---


# Een AI-instantie van de klant configureren

De AI van de klant, als deel van de Intelligente Diensten staat u toe om de scores van de douanedichtheid te produceren zonder het moeten zich over machine het leren ongerust maken.

Intelligente services bieden de AI van de Klant als een eenvoudig te gebruiken Adobe Sensei-service die voor verschillende gebruiksgevallen kan worden geconfigureerd. De volgende secties bevatten stappen voor het configureren van een exemplaar van Customer AI.

## Instellen van instantie {#set-up-your-instance}

Klik in de interface Platform op **[!UICONTROL Services]** de linkernavigatie. De **[!UICONTROL Services]** browser wordt weergegeven en geeft alle beschikbare services weer. Klik in de container voor Customer AI **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

In het *AI* -scherm van de Klant worden alle bestaande AI-exemplaren van de Klant weergegeven. Klik op **[!UICONTROL Create instance]**.

![](../images/user-guide/dashboard.png)

De workflow voor het maken van instanties wordt weergegeven, te beginnen bij de stap *Setup* .

Hieronder vindt u belangrijke informatie over waarden die u aan het exemplaar moet doorgeven:

* De naam van het exemplaar wordt gebruikt op alle plaatsen waar de AI-score van de Klant wordt weergegeven. Daarom moeten namen beschrijven wat de voorspellingsscores bijvoorbeeld vertegenwoordigen, &quot;Likeliability to cancel magazine subscription&quot;.

* Het type van aandrijving bepaalt de intentie van de score en metrische polariteit. U kunt kiezen **[!UICONTROL Churn]** of **[!UICONTROL Conversion]**. Zie de notitie onder [scoresamenvatting](./discover-insights.md#scoring-summary) in het document met ontdekkingsinzichten voor meer informatie over hoe het type neiging uw instantie beïnvloedt.

* De gegevensbron is waar het gegeven wordt gevestigd. Dataset is de gegevensset die wordt gebruikt om scores te voorspellen. Door ontwerp gebruikt de AI van de Klant gegevens van de Gebeurtenis van de Ervaring van de Consumenten om volheidsscores te berekenen. Wanneer u een gegevensset selecteert in de keuzelijst, worden alleen gegevenssets weergegeven die compatibel zijn met AI van de klant.

* Standaard worden voor alle profielen densiteitsscores gegenereerd, tenzij een in aanmerking komende populatie is opgegeven. U kunt een in aanmerking komende populatie opgeven door voorwaarden te definiëren voor het opnemen of uitsluiten van profielen op basis van gebeurtenissen.

Geef de vereiste waarden op en klik op **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### Een doel definiëren {#define-a-goal}

De stap *Definiëren van doel* verschijnt en biedt een interactieve omgeving waarin u visueel een doel kunt definiëren. Een doel bestaat uit een of meer gebeurtenissen, waarbij het voorkomen van elke gebeurtenis is gebaseerd op de voorwaarde die deze bevat. Het doel van een AI-instantie van een klant is na te gaan of het waarschijnlijk is dat het doel binnen een bepaald tijdsbestek wordt bereikt.

Klik op een veld in de vervolgkeuzelijst **[!UICONTROL Enter Field Name]** en selecteer dit. Klik op de tweede invoer en selecteer een component voor de voorwaarde van de gebeurtenis. Geef vervolgens de doelwaarde op om de gebeurtenis te voltooien. Aanvullende gebeurtenissen kunnen worden geconfigureerd door te klikken **[!UICONTROL Add event]**. Voltooi ten slotte het doel door een voorspelling in een aantal dagen toe te passen en klik vervolgens **[!UICONTROL Next]**.

![](../images/user-guide/goal.png)

### Een schema configureren *(optioneel)* {#configure-a-schedule}

De *geavanceerde* stap wordt weergegeven. Deze facultatieve stap staat u toe om een programma te vormen om voorspellingslooppas te automatiseren, voorspellingsuitsluitingen te bepalen om bepaalde gebeurtenissen te filtreren, of te klikken **[!UICONTROL Finish]** als niets nodig is.

Opstelling een het scoren programma door de het *Scoreren Frequentie* te vormen. De geautomatiseerde predikings kunnen worden gepland om of wekelijks of maandelijks te lopen.

![](../images/user-guide/schedule.png)

Onder de planningsconfiguratie, hebt u de capaciteit om voorspellingsuitsluitingen te bepalen om gebeurtenissen te verhinderen die aan bepaalde voorwaarden worden geëvalueerd wanneer het produceren van scores. Deze functie kan worden gebruikt om irrelevante gegevensinvoer uit te filteren.

Om bepaalde gebeurtenissen uit te sluiten, klik **[!UICONTROL Add exclusion]** en bepaal de gebeurtenis op de zelfde manier zoals aan hoe het doel wordt bepaald. Als u een uitsluiting wilt verwijderen, klikt u op de ovalen (**[!UICONTROL ...]**) rechtsboven in de gebeurteniscontainer en klikt u op **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

Sluit gebeurtenissen waar nodig uit en klik vervolgens om de instantie **[!UICONTROL Finish]** te maken.

![](../images/user-guide/advanced.png)

Als de instantie met succes wordt gecreeerd, wordt een voorspelling onmiddellijk teweeggebracht en de verdere looppas volgens uw bepaald programma uitvoeren.

>[!NOTE] Afhankelijk van de grootte van de invoergegevens kan het voltooien van de voorspelling 24 uur duren.

Door deze sectie te volgen, hebt u een geval van AI van de Klant gevormd en een voorspellingslooppas werd uitgevoerd. Als de uitvoering is voltooid, worden profielen met scorelijsten automatisch met voorspelde scores gevuld. Wacht tot 24 uur voordat u doorgaat naar de volgende sectie van deze zelfstudie.

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u met succes een exemplaar van de AI van de Klant en geproduceerde bezitsscores gevormd. U kunt er nu voor kiezen om de Segment Builder te gebruiken om klantsegmenten met voorspelde scores [te](./create-segment.md) maken of om inzichten met Customer AI [te](./discover-insights.md)ontdekken.

## Aanvullende bronnen

De volgende video is ontworpen ter ondersteuning van uw begrip van de configuratieworkflow voor AI van de klant. Daarnaast worden aanbevolen procedures en praktijkvoorbeelden gegeven.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

