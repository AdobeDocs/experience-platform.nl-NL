---
keywords: Experience Platform;in een pakket opgenomen recept importeren;Data Science Workspace;populaire onderwerpen;recepten;ui;engine maken
solution: Experience Platform
title: Een gecomprimeerde ontvanger importeren in de werkruimte voor wetenschap van gegevens
type: Tutorial
description: Deze zelfstudie biedt inzicht in het configureren en importeren van een verpakt recept met behulp van het meegeleverde voorbeeld Detailhandel. Aan het einde van deze zelfstudie bent u klaar om een model te maken, te trainen en te evalueren in de Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 0%

---

# Een verpakt recept importeren in de gebruikersinterface van de Data Science Workspace

Deze zelfstudie biedt inzicht in het configureren en importeren van een verpakt recept met behulp van het meegeleverde voorbeeld Detailhandel. Aan het einde van deze zelfstudie bent u klaar om een model te maken, te trainen en te evalueren in Adobe Experience Platform [!DNL Data Science Workspace].

## Vereisten

Voor deze zelfstudie is een recept in een pakket nodig in de vorm van een URL voor een Docker-afbeelding. Bekijk de zelfstudie over hoe u [Bronbestanden in een pakket plaatsen in een ontvanger](./package-source-files-recipe.md) voor meer informatie .

## UI-workflow

Een verpakt recept importeren in [!DNL Data Science Workspace] vereist specifieke receptconfiguraties, gecompileerd in één JSON-bestand (JavaScript Object Notation). Deze compilatie van recept-configuraties wordt het configuratiebestand genoemd. Een verpakt recept met een bepaalde set configuraties wordt een recept-exemplaar genoemd. Met één recept kunt u veel recept-varianten maken in [!DNL Data Science Workspace].

De workflow voor het importeren van een pakketrecept bestaat uit de volgende stappen:
- [Een recept configureren](#configure)
- [Op docker gebaseerd recept importeren - Python](#python)
- [Op Docker gebaseerde recept importeren - R](#r)
- [Op docker gebaseerde recept importeren - PySpark](#pyspark)
- [Op Docker gebaseerde recept importeren - Scala](#scala)

### Een recept configureren {#configure}

Elk recept-exemplaar in [!DNL Data Science Workspace] gaat vergezeld van een reeks configuraties die het recept-exemplaar aanpassen aan een bepaald gebruiksgeval. De dossiers van de configuratie bepalen het standaardopleiding en het scoren gedrag van een Model dat gebruikend dit recept geval wordt gecreeerd.

>[!NOTE]
>
>De dossiers van de configuratie zijn recept en geval-specifiek.

Hieronder ziet u een voorbeeldconfiguratiebestand met standaardtraining en scoring voor het detailhandelsverkooprecept.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| Parametersleutel | Type | Beschrijving |
| ----- | ----- | ----- |
| `learning_rate` | Getal | Schaalbaar voor verloopvermenigvuldiging. |
| `n_estimators` | Getal | Aantal bomen in het bos voor Random Forest Classifier. |
| `max_depth` | Getal | Maximale diepte van een boom in Random Forest Classifier. |
| `ACP_DSW_INPUT_FEATURES` | Tekenreeks | Lijst met door komma&#39;s gescheiden invoerschemakenmerken. |
| `ACP_DSW_TARGET_FEATURES` | Tekenreeks | Lijst met door komma&#39;s gescheiden kenmerken van het uitvoerschema. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolean | Hiermee wordt bepaald of invoer- en uitvoerfuncties kunnen worden gewijzigd |
| `tenantId` | Tekenreeks | Deze id zorgt ervoor dat bronnen die u maakt, op de juiste wijze worden benoemd en zich binnen uw organisatie bevinden. [Voer hier de stappen uit](../../xdm/api/getting-started.md#know-your-tenant_id) om je huurder-id te vinden. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Tekenreeks | Het invoerschema dat wordt gebruikt voor het trainen van een model. Laat dit leeg wanneer u importeert in de gebruikersinterface, vervang deze door de trainingsschema-id wanneer u importeert met behulp van de API. |
| `evaluation.labelColumn` | Tekenreeks | Kolomlabel voor evaluatievisualisaties. |
| `evaluation.metrics` | Tekenreeks | Door komma&#39;s gescheiden lijst met evaluatiemetriek die moet worden gebruikt voor de evaluatie van een model. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Tekenreeks | Het uitvoerschema dat voor het scoren van een model wordt gebruikt. Laat dit leeg wanneer u importeert in de gebruikersinterface, vervang het bestand door een SchemaID wanneer u importeert met behulp van de API. |

Voor deze zelfstudie kunt u de standaardconfiguratiebestanden voor het recept voor detailhandel in het dialoogvenster [!DNL Data Science Workspace] Verwijs naar de manier waarop ze zijn.

### Op Docker gebaseerde recept importeren - [!DNL Python] {#python}

Begin door te navigeren en te selecteren **[!UICONTROL Workflows]** in de linkerbovenhoek van het [!DNL Platform] UI. Selecteer vervolgens **Importeerrecept** en selecteert u **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

De **Configureren** pagina voor de **Importeerrecept** wordt weergegeven. Voer een naam en beschrijving in voor het recept en selecteer **[!UICONTROL Next]** in de rechterbovenhoek.

![workflow configureren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In de [Bronbestanden in een pakket plaatsen in een ontvanger](./package-source-files-recipe.md) Een zelfstudie, een Docker URL werd verstrekt aan het eind van de bouw van het Recept van de Verkoop van de Detailhandel gebruikend de brondossiers van Python.

Zodra u op **Bron selecteren** pagina, plakt u de URL van Docker die overeenkomt met het verpakte recept dat is gemaakt met [!DNL Python] bronbestanden in het dialoogvenster **[!UICONTROL Source URL]** veld. Importeer vervolgens het configuratiebestand door te slepen en neer te zetten of gebruik het bestandssysteem **Browser**. Het opgegeven configuratiebestand is te vinden op `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Selecteren **[!UICONTROL Python]** in de **Runtime** vervolgkeuzelijst en **[!UICONTROL Classification]** in de **Type** vervolgkeuzelijst. Als alles is ingevuld, selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan naar **Schema&#39;s beheren**.

>[!NOTE]
>
> Type ondersteunt **[!UICONTROL Classification]** en **[!UICONTROL Regression]**. Als uw model niet onder een van deze typen valt, selecteert u **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Selecteer vervolgens de invoer- en uitvoerschema&#39;s voor detailhandel onder de sectie **Schema&#39;s beheren**, zijn ze gemaakt met het opgegeven laarstaarscript in het dialoogvenster [het detailhandelschema en de dataset creëren](../models-recipes/create-retails-sales-dataset.md) zelfstudie.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Onder de **Functiebeheer** de sectie, selecteert op uw huurdersidentificatie in de schemakijker om het de inputschema van de Verkoop van de Detailhandel uit te breiden. Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en kies een van de volgende opties **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** rechts **[!UICONTROL Field Properties]** venster. Voor deze zelfstudie stelt u **[!UICONTROL weeklySales]** als de  **[!UICONTROL Target Feature]** en alle andere **[!UICONTROL Input Feature]**. Selecteren **[!UICONTROL Next]** om uw nieuwe gevormde recept te herzien.

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteren **[!UICONTROL Finish]** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga door naar de [volgende stappen](#next-steps) om te weten te komen hoe te om een Model tot stand te brengen in [!DNL Data Science Workspace] met behulp van het nieuwe detailhandelsrecept.

### Op Docker gebaseerde recept importeren - R {#r}

Begin door te navigeren en te selecteren **[!UICONTROL Workflows]** in de linkerbovenhoek van het [!DNL Platform] UI. Selecteer vervolgens **Importeerrecept** en selecteert u **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

De **Configureren** pagina voor de **Importeerrecept** wordt weergegeven. Voer een naam en beschrijving in voor het recept en selecteer **[!UICONTROL Next]** in de rechterbovenhoek.

![workflow configureren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In de [Bronbestanden in een pakket plaatsen in een ontvanger](./package-source-files-recipe.md) Een zelfstudie, een Docker URL werd verstrekt aan het eind van de bouw van het Recept van de Verkoop van de Detailhandel gebruikend de brondossiers van R.

Zodra u op **Bron selecteren** pagina, plakt u de URL van Docker die overeenkomt met het verpakte recept dat is gemaakt met R-bronbestanden in het dialoogvenster **[!UICONTROL Source URL]** veld. Importeer vervolgens het configuratiebestand door te slepen en neer te zetten of gebruik het bestandssysteem **Browser**. Het opgegeven configuratiebestand is te vinden op `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Selecteren **[!UICONTROL R]** in de **Runtime** vervolgkeuzelijst en **[!UICONTROL Classification]** in de **Type** vervolgkeuzelijst. Als alles is ingevuld, selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan naar **Schema&#39;s beheren**.

>[!NOTE]
>
> *Type* supports **[!UICONTROL Classification]** en **[!UICONTROL Regression]**. Als uw model niet onder een van deze typen valt, selecteert u **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Selecteer vervolgens de invoer- en uitvoerschema&#39;s voor detailhandel onder de sectie **Schema&#39;s beheren**, zijn ze gemaakt met het opgegeven laarstaarscript in het dialoogvenster [het detailhandelschema en de dataset creëren](../models-recipes/create-retails-sales-dataset.md) zelfstudie.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Onder de *Functiebeheer* de sectie, selecteert op uw huurdersidentificatie in de schemakijker om het de inputschema van de Verkoop van de Detailhandel uit te breiden. Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en kies een van de volgende opties **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** rechts **[!UICONTROL Field Properties]** venster. Voor deze zelfstudie stelt u **[!UICONTROL weeklySales]** als de  **[!UICONTROL Target Feature]** en alle andere **[!UICONTROL Input Feature]**. Selecteren **[!UICONTROL Next]** om uw nieuwe Gevormde recept te herzien.

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteren **Voltooien** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga door naar de [volgende stappen](#next-steps) om te weten te komen hoe te om een Model tot stand te brengen in [!DNL Data Science Workspace] met behulp van het nieuwe detailhandelsrecept.

### Op docker gebaseerde recept importeren - PySpark {#pyspark}

Begin door te navigeren en te selecteren **[!UICONTROL Workflows]** in de linkerbovenhoek van het [!DNL Platform] UI. Selecteer vervolgens **Importeerrecept** en selecteert u **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

De **Configureren** pagina voor de **Importeerrecept** wordt weergegeven. Voer een naam en beschrijving in voor het recept en selecteer **[!UICONTROL Next]** in de rechterbovenhoek om verder te gaan.

![workflow configureren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In de [Bronbestanden in een pakket plaatsen in een ontvanger](./package-source-files-recipe.md) zelfstudie, werd een Docker URL verstrekt aan het eind van de bouw van het Recept van de Verkoop van de Detailhandel gebruikend PySpark brondossiers.

Zodra u op **Bron selecteren** pagina, plakt u de URL van Docker die overeenkomt met het verpakte recept dat is samengesteld met PySpark-bronbestanden in het dialoogvenster **[!UICONTROL Source URL]** veld. Importeer vervolgens het configuratiebestand door te slepen en neer te zetten of gebruik het bestandssysteem **Browser**. Het opgegeven configuratiebestand is te vinden op `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Selecteren **[!UICONTROL PySpark]** in de **Runtime** vervolgkeuzelijst. Als de PySpark-runtime is geselecteerd, wordt het standaardartefact automatisch gevuld tot **[!UICONTROL Docker]**. Selecteer vervolgens **[!UICONTROL Classification]** in de **Type** vervolgkeuzelijst. Als alles is ingevuld, selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan naar **Schema&#39;s beheren**.

>[!NOTE]
>
> *Type* supports **[!UICONTROL Classification]** en **[!UICONTROL Regression]**. Als uw model niet onder een van deze typen valt, selecteert u **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Selecteer vervolgens de invoer- en uitvoerschema&#39;s voor de detailhandel met de **Schema&#39;s beheren** selector, werden de schema&#39;s gecreeerd gebruikend het verstrekte laarsmanuscript in [het detailhandelschema en de dataset creëren](../models-recipes/create-retails-sales-dataset.md) zelfstudie.

![schema&#39;s beheren](../images/models-recipes/import-package-ui/manage-schemas.png)

Onder de **Functiebeheer** de sectie, selecteert op uw huurdersidentificatie in de schemakijker om het de inputschema van de Verkoop van de Detailhandel uit te breiden. Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en kies een van de volgende opties **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** rechts **[!UICONTROL Field Properties]** venster. Voor deze zelfstudie stelt u **[!UICONTROL weeklySales]** als de  **[!UICONTROL Target Feature]** en alle andere **[!UICONTROL Input Feature]**. Selecteren **[!UICONTROL Next]** om uw nieuwe gevormde recept te herzien.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteren **[!UICONTROL Finish]** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga door naar de [volgende stappen](#next-steps) om te weten te komen hoe te om een Model tot stand te brengen in [!DNL Data Science Workspace] met behulp van het nieuwe detailhandelsrecept.

### Op Docker gebaseerde recept importeren - Scala {#scala}

Begin door te navigeren en te selecteren **[!UICONTROL Workflows]** in de linkerbovenhoek van het [!DNL Platform] UI. Selecteer vervolgens **Importeerrecept** en selecteert u **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

De **Configureren** pagina voor de **Importeerrecept** wordt weergegeven. Voer een naam en beschrijving in voor het recept en selecteer **[!UICONTROL Next]** in de rechterbovenhoek om verder te gaan.

![workflow configureren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In de [Bronbestanden in een pakket plaatsen in een ontvanger](./package-source-files-recipe.md) zelfstudie, werd een Docker URL verstrekt aan het eind van de bouw van het Detailhandelrecept gebruikend Scala ([!DNL Spark]).

Zodra u op **Bron selecteren** plakken, plakt u de URL van Docker die overeenkomt met het verpakte recept dat is samengesteld met Scala-bronbestanden in het veld Bron-URL. Importeer vervolgens het opgegeven configuratiebestand door te slepen en neer te zetten of gebruik de bestandssysteembrowser. Het opgegeven configuratiebestand is te vinden op `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Selecteren **[!UICONTROL Spark]** in de **Runtime** vervolgkeuzelijst. Wanneer de [!DNL Spark] runtime wordt geselecteerd als standaardartefact dat automatisch wordt gevuld **[!UICONTROL Docker]**. Selecteer vervolgens **[!UICONTROL Regression]** van de **Type** vervolgkeuzelijst. Als alles is ingevuld, selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan naar **Schema&#39;s beheren**.

>[!NOTE]
>
> Type ondersteunt **[!UICONTROL Classification]** en **[!UICONTROL Regression]**. Als uw model niet onder een van deze typen valt, selecteert u **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Selecteer vervolgens de invoer- en uitvoerschema&#39;s voor de detailhandel met de **Schema&#39;s beheren** selector, werden de schema&#39;s gecreeerd gebruikend het verstrekte laarsmanuscript in [het detailhandelschema en de dataset creëren](../models-recipes/create-retails-sales-dataset.md) zelfstudie.

![schema&#39;s beheren](../images/models-recipes/import-package-ui/manage-schemas.png)

Onder de **Functiebeheer** de sectie, selecteert op uw huurdersidentificatie in de schemakijker om het de inputschema van de Verkoop van de Detailhandel uit te breiden. Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en kies een van de volgende opties **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** rechts **[!UICONTROL Field Properties]** venster. Voor deze zelfstudie stelt u &quot;[!UICONTROL weeklySales]&quot; als de  **[!UICONTROL Target Feature]** en alle andere **[!UICONTROL Input Feature]**. Selecteren **[!UICONTROL Next]** om uw nieuwe gevormde recept te herzien.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteren **[!UICONTROL Finish]** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga door naar de [volgende stappen](#next-steps) om te weten te komen hoe te om een Model tot stand te brengen in [!DNL Data Science Workspace] met behulp van het nieuwe detailhandelsrecept.

## Volgende stappen {#next-steps}

Deze zelfstudie gaf inzicht in het configureren en importeren van een recept in [!DNL Data Science Workspace]. U kunt nu een model maken, trainen en evalueren met het nieuwe recept.

- [Een model trainen en evalueren in de gebruikersinterface](./train-evaluate-model-ui.md)
- [Een model trainen en evalueren met behulp van de API](./train-evaluate-model-api.md)
