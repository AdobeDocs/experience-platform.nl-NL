---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;produceert datasets;produceert dataset;creeer dataset;
solution: Experience Platform
title: Gegevensbestanden genereren op basis van resultaten in Query-service
topic-legacy: queries
type: Tutorial
description: Met Adobe Experience Platform Query Service kunt u gegevenssets maken vanuit de gebruikersinterface. Nadat een dataset wordt gecreeerd, kan het als een andere dataset in het meer van Gegevens worden betreden en voor een verscheidenheid van gebruiksgevallen worden gebruikt.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Gegevenssets genereren op basis van resultaten in Query Service

De ware macht van [!DNL Query Service] wordt onthuld wanneer de vragen worden gebruikt om datasets in [!DNL Data Lake] te produceren die als input in meer vragen of in andere diensten zoals [!DNL Data Science Workspace], [!DNL Real-time Customer Profile], of [!DNL Analysis Workspace] worden gebruikt.

[!DNL Query Service] staat de verwezenlijking van datasets van UI toe. Voer de volgende stappen uit:

1. Schrijf uw vraag gebruikend een verbonden cliënt en bevestig de output.
2. Meld u aan bij de gebruikersinterface [!DNL Platform] en ga naar Vragen.
3. Zoek de query in de lijst en houd de muisaanwijzer boven de rij.
4. Klik op **[!UICONTROL Create Dataset]**. ![Image](../images/ui/output-dataset.png)
5. Voer een naam voor een gegevensset in, voorafgegaan door uw LDAP-id (hoeft niet uniek of SQL-veilig te zijn). het systeem genereert een &quot;tabelnaam&quot; op basis van de hier gegeven naam).
6. Voer een beschrijving van een gegevensset in en klik op **[!UICONTROL Run Query]**.![Afbeelding](../images/ui/run-query.png)
7. Bekijk de vraag volledig, en ga dan naar de pagina van de datasetlijst om de dataset te zien u enkel creeerde.

Nadat een dataset wordt gecreeerd, kan het als een andere dataset in [!DNL Data Lake] worden betreden en voor een verscheidenheid van gebruiksgevallen worden gebruikt.

>[!NOTE]
>
>In een levende implementatie, moet u [!DNL Data Governance] etiketten toepassen nadat de dataset wordt gecreeerd.

## Gegevenssets genereren met een vooraf gedefinieerd [!DNL Experience Data Model]-schema

Om een dataset met een vooraf bepaald [!DNL Experience Data Model] (XDM) schema te produceren, zult u de SQL syntaxis moeten gebruiken. Lees voor meer informatie over de syntaxis die u moet gebruiken de [SQL-syntaxishandleiding](../sql/syntax.md#create-table-as-select).

## Uitvoergegevenssets

Datasets die met deze functie worden gemaakt, worden gegenereerd met een ad-hocschema dat overeenkomt met de structuur van de uitvoergegevens zoals gedefinieerd in de SQL-instructie. Voor sommige downstreamservices zijn gegevenssets met bepaalde XDM-schema&#39;s ([!DNL Experience Data Model]) vereist. Verifieer de gegevens het formatteren vereisten voor de stroomafwaartse diensten alvorens uw vragen te schrijven.
