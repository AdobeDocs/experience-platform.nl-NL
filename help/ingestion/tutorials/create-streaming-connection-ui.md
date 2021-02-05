---
keywords: Experience Platform;home;populaire onderwerpen;streamingverbinding;maak streamingverbinding;ui-handleiding;zelfstudie;maak een streamingverbinding;streaming opname;opname;
solution: Experience Platform
title: Een streamingverbinding maken met de gebruikersinterface
topic: tutorial
type: Tutorial
description: Deze UI-handleiding helpt u bij het maken van een streamingverbinding met Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Een streamingverbinding maken met de gebruikersinterface

Deze UI-handleiding helpt u bij het maken van een streamingverbinding met Adobe Experience Platform.

## Aan de slag

Als u wilt beginnen met het streamen van gegevens naar [!DNL Experience Platform], moet u eerst een streaming HTTP-verbinding maken. Wanneer u een streamingverbinding maakt, moet u belangrijke details opgeven, zoals de bron van streaminggegevens, en of u gegevens wilt verzenden van een vertrouwde (geverifieerde) of niet-vertrouwde (niet-geverifieerde) bron.

Na het registreren van een het stromen verbinding zult u een unieke URL hebben die aan stroom gegevens aan [!DNL Platform] kan worden gebruikt.

Je hebt toegang tot Adobe Experience Platform nodig om deze gids te voltooien. Als u geen toegang tot [!DNL Platform] hebt, gelieve uw systeembeheerder te contacteren alvorens te werk te gaan.

## Een streamingverbinding maken

Nadat u zich hebt aangemeld bij de [!DNL Experience Platform]-interface, klikt u op **[!UICONTROL Bronnen]** om het tabblad **[!UICONTROL Catalogus]** te openen. Deze pagina toont de beschikbare brontypes als individuele kaarten, met elke kaart die een bel bevat die het aantal gegevensstromen toont die van het stromen verbindingen aan datasets zijn gecreeerd.

![](../images/streaming-ingestion/ui/click-sources.png)

Op **[!UICONTROL Bronnen]** pagina, klik **[!UICONTROL HTTP API]**, dan **[!UICONTROL Bron verbinden]**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Het scherm **[!UICONTROL Verbinding maken met HTTP]** wordt weergegeven. Geef onder **[!UICONTROL Servicedetails]** zowel de naam als een beschrijving op voor uw nieuwe streamingverbinding.

Selecteer onder **[!UICONTROL Accountverificatie]** de volgende configuratie-eigenschappen voor uw streamingverbinding:

- **[!UICONTROL Verificatie]:** Of verificatie vereist is voor de streamingverbinding of niet. Verificatie zorgt ervoor dat gegevens worden verzameld van vertrouwde bronnen. Aanbevolen wordt deze optie in te schakelen als het gaat om PII (Personal Identified Information).
- **[!UICONTROL Compatibiliteit] met XDM-schema:** Of deze streamingverbinding gebeurtenissen verzendt die compatibel zijn met XDM-schema&#39;s. Deze eigenschap wordt standaard **on** ingeschakeld.

Nadat u de configuratie-eigenschappen hebt geselecteerd, klikt u op **[!UICONTROL Connect]**. Uw streaming HTTP-verbinding wordt nu gemaakt en kan nu worden weergegeven onder het tabblad **[!UICONTROL Bladeren]** in de werkruimte **[!UICONTROL Bronnen]**.

![](../images/streaming-ingestion/ui/http-sources-details.png)

Vanuit het tabblad **[!UICONTROL Bladeren]** kunt u op de nieuwe streamingverbinding van HTTP klikken en de details van die verbinding bekijken.

![](../images/streaming-ingestion/ui/browse-sources.png)

Door op hyperlink van de verbindingsnaam te klikken, kunt u gegevens selecteren die moeten worden getoond door te vormen welke dataset wordt aangesloten, door **[!UICONTROL Selecteer gegevens]** te klikken.

![](../images/streaming-ingestion/ui/select-data.png)

U kunt of [een nieuwe dataset](#create-a-new-dataset) of [een bestaande dataset](#use-an-existing-dataset) tot stand brengen.

### Een nieuwe gegevensset maken

Om een nieuwe dataset tot stand te brengen, verstrek de naam, de beschrijving, evenals het doelschema voor de dataset.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Nadat u alle details hebt ingevoegd en op **[!UICONTROL Next]** hebt geklikt, kunt u de verschafte details controleren voordat u op **[!UICONTROL Voltooien]** klikt om de dataset te verbinden met uw streaming HTTP-verbinding.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Een bestaande gegevensset gebruiken

Om een bestaande dataset te gebruiken, selecteer **[!UICONTROL de naam van de dataset van de Output]**.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Nadat u op **[!UICONTROL Volgende]** hebt geklikt, kunt u de details controleren voordat u op **[!UICONTROL Voltooien]** klikt om de geselecteerde gegevensset te verbinden met uw streaming HTTP-verbinding.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een het stromen verbinding van HTTP gecreeerd, toelatend u om het het stromen eindpunt te gebruiken om tot een verscheidenheid van [!DNL Data Ingestion] APIs toegang te hebben. Voor instructies voor het maken van een streamingverbinding in de API leest u de [zelfstudie voor het maken van een streamingverbinding](../tutorials/create-streaming-connection.md).
