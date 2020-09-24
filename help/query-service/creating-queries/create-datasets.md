---
keywords: Experience Platform;home;popular topics;query service;Query service;generate datasets;generate dataset;create dataset;
solution: Experience Platform
title: Gegevenssets genereren op basis van queryresultaten
topic: queries
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Gegevenssets genereren op basis van queryresultaten

De ware macht van [!DNL Query Service] wordt onthuld wanneer de vragen worden gebruikt om datasets in te produceren [!DNL Data Lake] die als input in meer vragen of in andere diensten zoals [!DNL Data Science Workspace], [!DNL Real-time Customer Profile], of [!DNL Analysis Workspace]worden gebruikt.

[!DNL Query Service] staat de verwezenlijking van datasets van UI toe. Voer de volgende stappen uit:

1. Schrijf uw vraag gebruikend een verbonden cliënt en bevestig de output.
2. Meld u aan bij de [!DNL Platform] UI en ga naar Query&#39;s.
3. Zoek de query in de lijst en houd de muisaanwijzer boven de rij.
4. Klik op Gegevensset **[!UICONTROL maken]**. ![Image](../images/queries/create-datasets/click-create-dataset.png)
5. Voer een naam voor een gegevensset in, voorafgegaan door uw LDAP-id (hoeft niet uniek of SQL-veilig te zijn). het systeem genereert een &quot;tabelnaam&quot; op basis van de hier gegeven naam).
6. Voer een beschrijving van een gegevensset in en klik op **[!UICONTROL Query]** uitvoeren.![Image](../images/queries/create-datasets/run-query.png)
7. Bekijk de vraag volledig, en ga dan naar de pagina van de datasetlijst om de dataset te zien u enkel creeerde.

Nadat een dataset wordt gecreeerd, kan het als een andere dataset in worden betreden [!DNL Data Lake] en voor een verscheidenheid van gebruiksgevallen worden gebruikt.

>[!NOTE]
>
>In een levende implementatie, moet u [!DNL Data Governance] etiketten toepassen nadat de dataset wordt gecreeerd.

## Gegevenssets genereren met een vooraf gedefinieerd [!DNL Experience Data Model] schema

Om een dataset met een vooraf bepaald [!DNL Experience Data Model] (XDM) schema te produceren, zult u de SQL syntaxis moeten gebruiken. Lees voor meer informatie over de syntaxis die u moet gebruiken de handleiding [SQL Syntax](../sql/syntax.md#create-table-as-select).

## Uitvoergegevenssets

Datasets die met deze functie worden gemaakt, worden gegenereerd met een ad-hocschema dat overeenkomt met de structuur van de uitvoergegevens zoals gedefinieerd in de SQL-instructie. Sommige downstream diensten vereisen datasets met bepaalde [!DNL Experience Data Model] (XDM) schema&#39;s. Verifieer de gegevens het formatteren vereisten voor de stroomafwaartse diensten alvorens uw vragen te schrijven.