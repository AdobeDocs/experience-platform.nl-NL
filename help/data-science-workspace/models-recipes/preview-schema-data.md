---
keywords: Experience Platform;voorbeeldschemagegevens;Data Science Workspace;populaire onderwerpen
solution: Experience Platform
title: Een voorvertoning weergeven van het detailhandelsschema en de gegevensset
type: Tutorial
description: Het volgende document schetst het voorvertonen van schema's en datasets op Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Een voorvertoning weergeven van het detailhandelsschema en de dataset

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Op succesvolle voltooiing van het laarzentrekkermanuscript van het [ detailhandelschema en dataset ](./create-retails-sales-dataset.md) leerprogramma. Uitvoerschema&#39;s en gegevenssets kunnen worden weergegeven op [!DNL Experience Platform] . Volg onderstaande stappen om de schema&#39;s en datasets weer te geven:

Selecteer het tabblad **[!UICONTROL Schemas]** in de linkernavigatie en zoek het invoerschema dat door het bootstrap-script is gemaakt. De naam van het schema komt overeen met de naam die in `config.yaml` van de vorige stap is gedefinieerd. Bekijk de schemadetails en het is samenstelling door in het te klikken.

![](../images/models-recipes/access-data/schema.PNG)

Selecteer het tabblad **[!UICONTROL Datasets]** in de linkernavigatie en open de gegevensset die is gemaakt door de naam van de gegevensset te selecteren. De naam van de gegevensset komt overeen met de naam die is gedefinieerd in `config.yaml` van de vorige stap.

![](../images/models-recipes/access-data/dataset.PNG)

Selecteer **[!UICONTROL Preview Dataset]** in de rechterbovenhoek om een voorvertoning weer te geven van een subset van de gegevensset.

![](../images/models-recipes/access-data/preview.PNG)

## Volgende stappen

U hebt nu met succes de gegevens van de steekproef van de Verkoop van de Handel in [!DNL Experience Platform] gegeconsumeerd gebruikend het verstrekte laarzentrekwescript.

U kunt als volgt met de opgenomen gegevens blijven werken:
- [Uw gegevens analyseren met Jupyter-laptops](../jupyterlab/analyze-your-data.md)
   - Gebruik Jupyter-laptops in [!DNL Data Science Workspace] om toegang te krijgen tot uw gegevens, deze te verkennen, te visualiseren en inzicht in uw gegevens te krijgen.
- [Bronbestanden in een pakket plaatsen in een ontvanger](./package-source-files-recipe.md)
   - Volg deze zelfstudie om te leren hoe u uw eigen model in [!DNL Data Science Workspace] kunt plaatsen door bronbestanden in een importeerbaar Recipe-bestand te verpakken.
