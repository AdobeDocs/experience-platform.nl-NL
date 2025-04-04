---
keywords: Experience Platform;home;populaire onderwerpen;query-service;Query-service;genereren datasets;genereren gegevensset;maken gegevensset;
solution: Experience Platform
title: Uitvoergegevens genereren op basis van zoekresultaten
type: Tutorial
description: Met Adobe Experience Platform Query Service kunt u gegevenssets maken vanuit de gebruikersinterface. Nadat een dataset wordt gecreeerd, kan het als een andere dataset in het meer van Gegevens worden betreden en voor een verscheidenheid van gebruiksgevallen worden gebruikt.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Uitvoerdatasets genereren op basis van queryresultaten

Met [!DNL Query Service] kunt u query&#39;s gebruiken om gegevenssets te genereren in de [!DNL Data Lake] . Deze datasets kunnen dan als input voor meer vragen of in andere diensten zoals [!DNL Data Science Workspace], het Profiel van de Klant in real time, of [!DNL Analysis Workspace] worden gebruikt.

## Gegevenssets genereren vanuit de gebruikersinterface van Adobe Experience Platform

Ga als volgt te werk om gegevenssets te maken van de gebruikersinterface van Adobe Experience Platform (UI):

1. Maak een query met een verbonden client en valideer de uitvoer. Leren hoe te om vragen te schrijven gebruikend [!DNL Query Editor], lees de [!DNL Query Editor] gids UI [ bij het schrijven van vragen ](./user-guide.md#writing-queries).

2. Navigeer in de gebruikersinterface van Experience Platform naar **[!UICONTROL Queries]** , gevolgd door het tabblad **[!UICONTROL Templates]** en selecteer de query die u hebt gemaakt. Voor meer details op hoe te om vragen te bekijken die voor uw organisatie binnen Experience Platform UI werden gecreeerd en werden bewaard, lees het [[!DNL Query Service]  overzicht ](./overview.md#browse).

3. Selecteer **[!UICONTROL Run as CTAS]** in het deelvenster Query-details.

   ![ het lusje van de werkruimte van Vragen [!UICONTROL Templates] met Uitgezochte [!UICONTROL Run as CTAS] benadrukte.](../images/ui/create-datasets/run-as-ctas.png)

4. Voer in het dialoogvenster dat wordt weergegeven een naam in voor de gegevensset die is toegevoegd met uw LDAP-id. De naam van de gegevensset hoeft niet uniek of SQL-veilig te zijn. Merk op dat de lijstnaam voor uw dataset zal worden geproduceerd gebaseerd op de datasetnaam u hier creeert.

5. Voer vervolgens een beschrijving voor uw gegevensset in het veld [!UICONTROL Description] in en selecteer **[!UICONTROL Run as CTAS]** .

   ![ de dialoog van de dataset van de Output met de datasetdetails en [!UICONTROL Run as CTAS] benadrukte ](../images/ui/create-datasets/run-query.png)

6. Wanneer de query is uitgevoerd, navigeert u naar **[!UICONTROL Datasets]** om de gegevensset weer te geven die u hebt gemaakt. Meer over leren hoe te om gemeenschappelijke acties uit te voeren wanneer het werken met datasets binnen Experience Platform UI, zie de [ gids UI van Datasets ](../../catalog/datasets/user-guide.md).

Nadat een dataset wordt gecreeerd, kan het als een andere dataset in [!DNL Data Lake] worden betreden en voor een verscheidenheid van gebruiksgevallen worden gebruikt.

>[!NOTE]
>
>In een levende implementatie, moet u de etiketten van de Governance van Gegevens toepassen nadat de dataset wordt gecreeerd. Meer over leren hoe te om de etiketten van het gegevensgebruik op datasets toe te passen, zie het [ overzicht van de gebruiksetiketten van Gegevens ](../../data-governance/labels/overview.md).

## Gegevenssets genereren met een vooraf gedefinieerd [!DNL Experience Data Model] -schema

Gebruik de SQL-syntaxis om een gegevensset te genereren met een vooraf gedefinieerd [!DNL Experience Data Model] (XDM) schema. Voor meer informatie over de syntaxis die door [!DNL Query Service] wordt gesteund, te lezen gelieve de [ SQL gids van de Syntaxis ](../sql/syntax.md#create-table-as-select).

## Uitvoergegevenssets

Datasets die met deze functie worden gemaakt, worden gegenereerd met een ad-hocschema dat overeenkomt met de structuur van de uitvoergegevens zoals gedefinieerd in de SQL-instructie. Sommige downstream diensten vereisen datasets met bepaalde schema&#39;s XDM. Verifieer de gegevens het formatteren vereisten voor de stroomafwaartse diensten alvorens uw vragen te schrijven.

## Volgende stappen

Nadat u dit document hebt gelezen, moet u nu begrijpen hoe u [!DNL Query Service] kunt gebruiken om gegevenssets te genereren via de gebruikersinterface van Experience Platform. Voor meer informatie over hoe te om tot, schrijven, en uit te voeren vragen binnen Experience Platform UI, zie het [[!DNL Query Service]  overzicht UI ](./overview.md).
