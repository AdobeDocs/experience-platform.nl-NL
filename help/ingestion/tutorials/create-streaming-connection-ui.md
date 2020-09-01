---
keywords: Experience Platform;home;popular topics;streaming connection;create streaming connection;ui guide;tutorial;create a streaming connection;streaming ingestion;ingestion;
solution: Experience Platform
title: Een streamingverbinding maken met de gebruikersinterface
topic: tutorial
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---


# Een streamingverbinding maken met de gebruikersinterface

Deze UI-handleiding helpt u bij het maken van een streamingverbinding met Adobe Experience Platform.

## Aan de slag

Als u wilt beginnen met het streamen van gegevens naar, moet u eerst een streaming HTTP-verbinding maken. [!DNL Experience Platform] Wanneer u een streamingverbinding maakt, moet u belangrijke details opgeven, zoals de bron van streaminggegevens, en of u gegevens wilt verzenden van een vertrouwde (geverifieerde) of niet-vertrouwde (niet-geverifieerde) bron.

Nadat u een streamingverbinding hebt geregistreerd, hebt u een unieke URL die kan worden gebruikt om gegevens naar te streamen [!DNL Platform].

Je hebt toegang tot Adobe Experience Platform nodig om deze gids te voltooien. Als u geen toegang tot hebt, gelieve uw systeembeheerder te contacteren alvorens te werk te gaan. [!DNL Platform]

## Een streamingverbinding maken

Nadat u zich hebt aangemeld bij de [!DNL Experience Platform] UI, klikt u op **[!UICONTROL Bronnen]** om het tabblad **[!UICONTROL Catalogus]** te openen. Deze pagina toont de beschikbare brontypes als individuele kaarten, met elke kaart die een bel bevat die het aantal gegevensstromen toont die van het stromen verbindingen aan datasets zijn gecreeerd.

![](../images/streaming-ingestion/ui/click-sources.png)

Klik op de pagina **[!UICONTROL Bronnen]** op **[!UICONTROL HTTP API]** en vervolgens op **[!UICONTROL Connect-bron]**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Het scherm **[!UICONTROL Verbinding maken met HTTP]** wordt weergegeven. Geef onder **[!UICONTROL Servicedetails]** zowel de **[!UICONTROL naam]** als een **[!UICONTROL beschrijving]** voor de nieuwe streamingverbinding op.

Selecteer onder **[!UICONTROL Accountverificatie]** de volgende configuratie-eigenschappen voor uw streamingverbinding:

- **[!UICONTROL Verificatie]:** Of verificatie vereist is voor de streamingverbinding. Verificatie zorgt ervoor dat gegevens worden verzameld van vertrouwde bronnen. Aanbevolen wordt deze optie in te schakelen als het gaat om PII (Personal Identified Information).
- **[!UICONTROL Compatibiliteit met]XDM-schema:** Of deze streamingverbinding gebeurtenissen verzendt die compatibel zijn met XDM-schema&#39;s. Deze eigenschap is standaard **ingeschakeld**.

Nadat u de configuratie-eigenschappen hebt geselecteerd, klikt u op **[!UICONTROL Verbinden]**. Uw streaming HTTP-verbinding wordt nu gemaakt en kan nu worden weergegeven onder het tabblad **[!UICONTROL Bladeren]** in de werkruimte **[!UICONTROL Bronnen]** .

![](../images/streaming-ingestion/ui/http-sources-details.png)

Via het tabblad **[!UICONTROL Bladeren]** kunt u op de nieuwe streamingverbinding van HTTP klikken en de details van die verbinding weergeven.

![](../images/streaming-ingestion/ui/browse-sources.png)

Door op hyperlink van de verbindingsnaam te klikken, kunt u gegevens selecteren die moeten worden getoond door te vormen welke dataset wordt aangesloten, door **[!UICONTROL Uitgezochte gegevens]** te klikken.

![](../images/streaming-ingestion/ui/select-data.png)

U kunt of een nieuwe dataset [](#create-a-new-dataset) creëren of een bestaande dataset [](#use-an-existing-dataset)gebruiken.

### Een nieuwe gegevensset maken

Om een nieuwe dataset tot stand te brengen, verstrek de **[!UICONTROL Naam]**, de **[!UICONTROL Beschrijving]**, evenals het doel **[!UICONTROL Schema]** voor de dataset.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Nadat u alle details hebt ingevoegd en op **[!UICONTROL Volgende]** hebt geklikt, kunt u de verschafte details controleren voordat u op **[!UICONTROL Voltooien]** klikt om de gegevensset te verbinden met uw streaming HTTP-verbinding.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Een bestaande gegevensset gebruiken

Als u een bestaande gegevensset wilt gebruiken, selecteert u de naam **[!UICONTROL van de]** uitvoergegevensset.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Nadat u op **[!UICONTROL Volgende]** hebt geklikt, kunt u de details controleren voordat u op **[!UICONTROL Voltooien]** klikt om de geselecteerde dataset te verbinden met uw streaming HTTP-verbinding.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een streaming HTTP-verbinding gemaakt, waarmee u het streaming eindpunt kunt gebruiken voor toegang tot verschillende API&#39; [!DNL Data Ingestion] s. Voor instructies voor het maken van een streamingverbinding in de API leest u de zelfstudie voor het [maken van een streamingverbinding](../tutorials/create-streaming-connection.md).
