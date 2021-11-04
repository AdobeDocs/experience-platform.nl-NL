---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;produceert datasets;produceert dataset;creeer dataset;
solution: Experience Platform
title: Gegevensbestanden genereren op basis van resultaten in Query-service
topic-legacy: queries
type: Tutorial
description: Met Adobe Experience Platform Query Service kunt u gegevenssets maken vanuit de gebruikersinterface. Nadat een dataset wordt gecreeerd, kan het als een andere dataset in het meer van Gegevens worden betreden en voor een verscheidenheid van gebruiksgevallen worden gebruikt.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Gegevenssets genereren op basis van resultaten in Query Service

De ware kracht van [!DNL Query Service] wordt onthuld wanneer de vragen worden gebruikt om datasets in te produceren [!DNL Data Lake] om als input in meer vragen of in andere diensten zoals [!DNL Data Science Workspace], [!DNL Real-time Customer Profile], of [!DNL Analysis Workspace].

[!DNL Query Service] staat de verwezenlijking van datasets van UI toe. Voer de volgende stappen uit:

1. Schrijf uw vraag gebruikend een verbonden cliënt en bevestig de output.
2. Aanmelden bij de [!DNL Platform] UI en ga naar Vragen.
3. Zoek de query in de lijst en houd de muisaanwijzer boven de rij.
4. Selecteer **[!UICONTROL Create Dataset]**. ![Image](../images/ui/create-datasets/output-dataset.png)
5. Voer een naam voor een gegevensset in, voorafgegaan door uw LDAP-id (hoeft niet uniek of SQL-veilig te zijn). het systeem genereert een &quot;tabelnaam&quot; op basis van de hier gegeven naam).
6. Voer een beschrijving van een gegevensset in en selecteer **[!UICONTROL Run Query]**.![Afbeelding](../images/ui/create-datasets/run-query.png)
7. Bekijk de vraag volledig, en ga dan naar de pagina van de datasetlijst om de dataset te zien u enkel creeerde.

Nadat een dataset wordt gecreeerd, kan het als een andere dataset in worden betreden [!DNL Data Lake] en worden gebruikt voor diverse gebruiksgevallen.

>[!NOTE]
>
>In een levende implementatie, moet u de etiketten van de Governance van Gegevens toepassen nadat de dataset wordt gecreeerd.

## Gegevenssets genereren met een vooraf gedefinieerde [!DNL Experience Data Model] schema

Om een dataset met vooraf bepaald te produceren [!DNL Experience Data Model] (XDM) schema, zult u de SQL syntaxis moeten gebruiken. Voor meer informatie over welke syntaxis u moet gebruiken, gelieve te lezen [SQL-syntaxishandleiding](../sql/syntax.md#create-table-as-select).

## Uitvoergegevenssets

Datasets die met deze functie worden gemaakt, worden gegenereerd met een ad-hocschema dat overeenkomt met de structuur van de uitvoergegevens zoals gedefinieerd in de SQL-instructie. Voor sommige downstreamdiensten zijn gegevensbestanden met name vereist [!DNL Experience Data Model] (XDM) schema&#39;s. Verifieer de gegevens het formatteren vereisten voor de stroomafwaartse diensten alvorens uw vragen te schrijven.
