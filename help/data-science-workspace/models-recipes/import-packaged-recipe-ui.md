---
keywords: Experience Platform;in een pakket opgenomen recept importeren;Data Science Workspace;populaire onderwerpen;recepten;ui;engine maken
solution: Experience Platform
title: Een gecomprimeerde ontvanger importeren in de werkruimte voor wetenschap van gegevens
topic: tutorial
type: Tutorial
description: Deze zelfstudie biedt inzicht in het configureren en importeren van een verpakt recept met behulp van het meegeleverde voorbeeld Detailhandel. Aan het einde van deze zelfstudie bent u klaar om een model te maken, te trainen en te evalueren in de Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: 13fa4af388c6f31768a6b7e1da05cb56c5635c9e
workflow-type: tm+mt
source-wordcount: '1740'
ht-degree: 0%

---


# Een verpakt recept importeren in de gebruikersinterface van de Data Science Workspace

Deze zelfstudie biedt inzicht in het configureren en importeren van een verpakt recept met behulp van het meegeleverde voorbeeld Detailhandel. Aan het einde van deze zelfstudie bent u klaar om een model te maken, te trainen en te evalueren in Adobe Experience Platform [!DNL Data Science Workspace].

## Vereisten

Voor deze zelfstudie is een recept in een pakket nodig in de vorm van een URL voor een Docker-afbeelding. Zie de zelfstudie over het [Pakken van bronbestanden in een Recipe](./package-source-files-recipe.md) voor meer informatie.

## UI-workflow

Voor het importeren van een verpakt recept in [!DNL Data Science Workspace] zijn specifieke recept-configuraties vereist, gecompileerd in één JSON-bestand (JavaScript Object Notation). Deze compilatie van recept-configuraties wordt het configuratiebestand genoemd. Een verpakt recept met een bepaalde set configuraties wordt een recept-exemplaar genoemd. Met één recept kunt u veel recept-varianten maken in [!DNL Data Science Workspace].

De workflow voor het importeren van een pakketrecept bestaat uit de volgende stappen:
- [Een recept configureren](#configure)
- [Op docker gebaseerd recept importeren - Python](#python)
- [Op Docker gebaseerde recept importeren - R](#r)
- [Op docker gebaseerde recept importeren - PySpark](#pyspark)
- [Op Docker gebaseerde recept importeren - Scala](#scala)

### Een recept {#configure} configureren

Elk recept-exemplaar in [!DNL Data Science Workspace] gaat vergezeld van een set configuraties die het recept-exemplaar aanpassen aan een bepaald gebruiksgeval. De dossiers van de configuratie bepalen het standaardopleiding en het scoren gedrag van een Model dat gebruikend dit recept geval wordt gecreeerd.

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
| `tenantId` | Tekenreeks | Deze id zorgt ervoor dat bronnen die u maakt, op de juiste wijze worden benoemd en zich in uw IMS-organisatie bevinden. [Volg de stappen ](../../xdm/api/getting-started.md#know-your-tenant_id) hier om je huurder-id te vinden. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Tekenreeks | Het invoerschema dat wordt gebruikt voor het trainen van een model. Laat dit leeg wanneer u importeert in de gebruikersinterface, vervang deze door de trainingsschema-id wanneer u importeert met behulp van de API. |
| `evaluation.labelColumn` | Tekenreeks | Kolomlabel voor evaluatievisualisaties. |
| `evaluation.metrics` | Tekenreeks | Door komma&#39;s gescheiden lijst met evaluatiemetriek die moet worden gebruikt voor de evaluatie van een model. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Tekenreeks | Het uitvoerschema dat voor het scoren van een model wordt gebruikt. Laat dit leeg wanneer u importeert in de gebruikersinterface, vervang het bestand door een SchemaID wanneer u importeert met behulp van de API. |

Voor dit leerprogramma, kunt u de standaardconfiguratiedossiers voor het Recept van de Verkoop van de Detailhandel in [!DNL Data Science Workspace] Verwijzing de manier verlaten zij zijn.

### Op docker gebaseerd recept importeren - [!DNL Python] {#python}

Begin door **[!UICONTROL Workflows]** te navigeren en te selecteren die in de bovenkant-linkerzijde van [!DNL Platform] UI wordt gevestigd. Selecteer vervolgens **Opbrengst importeren** en selecteer **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

De pagina **Configure** voor **Import recipe** werkschema verschijnt. Voer een naam en beschrijving voor het recept in en selecteer **[!UICONTROL Next]** in de rechterbovenhoek.

![workflow configureren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In [De brondossiers van het Pakket in een Recipe](./package-source-files-recipe.md) leerprogramma, werd een Docker URL verstrekt aan het eind van de bouw van het Retailrecept van de Verkoop gebruikend de brondossiers van Python.

Als u op de pagina **Source** selecteert, plakt u de URL van Docker die overeenkomt met het verpakte recept dat is samengesteld met behulp van [!DNL Python] bronbestanden in het veld **[!UICONTROL Source URL]**. Importeer vervolgens het opgegeven configuratiebestand door te slepen en neer te zetten of gebruik het bestandssysteem **Browser**. Het meegeleverde configuratiebestand vindt u op `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Selecteer **[!UICONTROL Python]** in **Runtime** drop down en **[!UICONTROL Classification]** in **Type** drop down. Als alles is ingevuld, selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan naar **Schema&#39;s beheren**.

>[!NOTE]
>
> Type ondersteunt **[!UICONTROL Classification]** en **[!UICONTROL Regression]**. Selecteer **[!UICONTROL Custom]** als uw model niet onder een van deze typen valt.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Vervolgens selecteert u de invoer- en uitvoerschema&#39;s voor de detailhandel onder de sectie **Schema&#39;s beheren**. Deze schema&#39;s zijn gemaakt met het opgegeven opstartscript in de zelfstudie [Maak het handelsschema en de dataset](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Onder **Het Beheer van de Eigenschap** sectie, selecteer op uw huurdersidentificatie in de schemakijker om het Retailschema van de input van de Verkoop uit te breiden. Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en selecteer **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** in het rechtervenster **[!UICONTROL Field Properties]**. Voor deze zelfstudie stelt u **[!UICONTROL weeklySales]** in als de **[!UICONTROL Target Feature]** en alles als **[!UICONTROL Input Feature]**. Selecteer **[!UICONTROL Next]** om uw nieuw gevormd recept te herzien.

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteer **[!UICONTROL Finish]** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga aan [volgende stappen](#next-steps) te werk om te weten te komen hoe te om een Model in [!DNL Data Science Workspace] tot stand te brengen gebruikend het pas gecreëerde Retailrecept van de Verkoop.

### Op docker gebaseerd recept importeren - R {#r}

Begin door **[!UICONTROL Workflows]** te navigeren en te selecteren die in de bovenkant-linkerzijde van [!DNL Platform] UI wordt gevestigd. Selecteer vervolgens **Opbrengst importeren** en selecteer **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

De pagina **Configure** voor **Import recipe** werkschema verschijnt. Voer een naam en beschrijving voor het recept in en selecteer **[!UICONTROL Next]** in de rechterbovenhoek.

![workflow configureren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In [De brondossiers van het Pakket in een Recipe](./package-source-files-recipe.md) leerprogramma, werd een Docker URL verstrekt aan het eind van de bouw van het Retailrecept van de Verkoop gebruikend de brondossiers van R.

Als u op de pagina **Source** selecteert, plakt u de URL van Docker die overeenkomt met het verpakte recept dat is samengesteld met R-bronbestanden in het veld **[!UICONTROL Source URL]**. Importeer vervolgens het opgegeven configuratiebestand door te slepen en neer te zetten of gebruik het bestandssysteem **Browser**. Het meegeleverde configuratiebestand vindt u op `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Selecteer **[!UICONTROL R]** in **Runtime** drop down en **[!UICONTROL Classification]** in **Type** drop down. Als alles is ingevuld, selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan naar **Schema&#39;s beheren**.

>[!NOTE]
>
> ** Typesupports  **[!UICONTROL Classification]** en  **[!UICONTROL Regression]**. Selecteer **[!UICONTROL Custom]** als uw model niet onder een van deze typen valt.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Vervolgens selecteert u de invoer- en uitvoerschema&#39;s voor de detailhandel onder de sectie **Schema&#39;s beheren**. Deze schema&#39;s zijn gemaakt met het opgegeven opstartscript in de zelfstudie [Maak het handelsschema en de dataset](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Onder *het Beheer van de Eigenschap* sectie, selecteer op uw huurdersidentificatie in de schemakijker om het Retailschema van de input van de Verkoop uit te breiden. Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en selecteer **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** in het rechtervenster **[!UICONTROL Field Properties]**. Voor deze zelfstudie stelt u **[!UICONTROL weeklySales]** in als de **[!UICONTROL Target Feature]** en alles als **[!UICONTROL Input Feature]**. Selecteer **[!UICONTROL Next]** om uw nieuwe Gevormde recept te herzien.

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteer **Voltooien** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga aan [volgende stappen](#next-steps) te werk om te weten te komen hoe te om een Model in [!DNL Data Science Workspace] tot stand te brengen gebruikend het pas gecreëerde Retailrecept van de Verkoop.

### Op docker gebaseerde recept importeren - PySpark {#pyspark}

Begin door **[!UICONTROL Workflows]** te navigeren en te selecteren die in de bovenkant-linkerzijde van [!DNL Platform] UI wordt gevestigd. Selecteer vervolgens **Opbrengst importeren** en selecteer **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

De pagina **Configure** voor **Import recipe** werkschema verschijnt. Voer een naam en beschrijving voor het recept in en selecteer **[!UICONTROL Next]** in de rechterbovenhoek om verder te gaan.

![workflow configureren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In [De brondossiers van het Pakket in een Recipe](./package-source-files-recipe.md) leerprogramma, werd een Docker URL verstrekt aan het eind van de bouw van het Retailrecept van de Verkoop gebruikend PySpark brondossiers.

Zodra u op **Select bron** pagina bent, kleef de Dok URL die aan het verpakte recept beantwoordt dat met PySpark brondossiers in het **[!UICONTROL Source URL]** gebied wordt gebouwd. Importeer vervolgens het opgegeven configuratiebestand door te slepen en neer te zetten of gebruik het bestandssysteem **Browser**. Het meegeleverde configuratiebestand vindt u op `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Selecteer **[!UICONTROL PySpark]** in **Runtime** drop down. Nadat de PySpark-runtime is geselecteerd, wordt het standaardartefact automatisch gevuld tot **[!UICONTROL Docker]**. Selecteer vervolgens **[!UICONTROL Classification]** in de vervolgkeuzelijst **Type**. Als alles is ingevuld, selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan naar **Schema&#39;s beheren**.

>[!NOTE]
>
> ** Typesupports  **[!UICONTROL Classification]** en  **[!UICONTROL Regression]**. Selecteer **[!UICONTROL Custom]** als uw model niet onder een van deze typen valt.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Vervolgens selecteert u de invoer- en uitvoerschema&#39;s voor de detailhandel met behulp van de kiezer **Schema&#39;s beheren**. De schema&#39;s zijn gemaakt met behulp van het opgegeven opstartscript in de zelfstudie [Maak het handelsschema en de dataset](../models-recipes/create-retails-sales-dataset.md).

![schema&#39;s beheren](../images/models-recipes/import-package-ui/manage-schemas.png)

Onder **Het Beheer van de Eigenschap** sectie, selecteer op uw huurdersidentificatie in de schemakijker om het Retailschema van de input van de Verkoop uit te breiden. Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en selecteer **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** in het rechtervenster **[!UICONTROL Field Properties]**. Voor deze zelfstudie stelt u **[!UICONTROL weeklySales]** in als de **[!UICONTROL Target Feature]** en alles als **[!UICONTROL Input Feature]**. Selecteer **[!UICONTROL Next]** om uw nieuw gevormd recept te herzien.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteer **[!UICONTROL Finish]** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga aan [volgende stappen](#next-steps) te werk om te weten te komen hoe te om een Model in [!DNL Data Science Workspace] tot stand te brengen gebruikend het pas gecreëerde Retailrecept van de Verkoop.

### Op docker gebaseerde recept importeren - Scala {#scala}

Begin door **[!UICONTROL Workflows]** te navigeren en te selecteren die in de bovenkant-linkerzijde van [!DNL Platform] UI wordt gevestigd. Selecteer vervolgens **Opbrengst importeren** en selecteer **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

De pagina **Configure** voor **Import recipe** werkschema verschijnt. Voer een naam en beschrijving voor het recept in en selecteer **[!UICONTROL Next]** in de rechterbovenhoek om verder te gaan.

![workflow configureren](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In [De brondossiers van het Pakket in een Recipe](./package-source-files-recipe.md) leerprogramma, werd een Docker URL verstrekt aan het eind van de bouw van het Retailrecept van de Verkoop gebruikend Scala ([!DNL Spark]) brondossiers.

Zodra u op **Select bron** pagina bent, kleef de Dok URL die aan het verpakte recept beantwoordt dat gebruikend Scala brondossiers op het BronURL gebied wordt gebouwd. Importeer vervolgens het opgegeven configuratiebestand door te slepen en neer te zetten of gebruik de bestandssysteembrowser. Het meegeleverde configuratiebestand vindt u op `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Selecteer **[!UICONTROL Spark]** in **Runtime** drop down. Wanneer de runtime [!DNL Spark] is geselecteerd, wordt het standaardartefact automatisch gevuld tot **[!UICONTROL Docker]**. Selecteer vervolgens **[!UICONTROL Regression]** in de vervolgkeuzelijst **Type**. Als alles is ingevuld, selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan naar **Schema&#39;s beheren**.

>[!NOTE]
>
> Type ondersteunt **[!UICONTROL Classification]** en **[!UICONTROL Regression]**. Selecteer **[!UICONTROL Custom]** als uw model niet onder een van deze typen valt.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Vervolgens selecteert u de invoer- en uitvoerschema&#39;s voor de detailhandel met behulp van de kiezer **Schema&#39;s beheren**. De schema&#39;s zijn gemaakt met behulp van het opgegeven opstartscript in de zelfstudie [Maak het handelsschema en de dataset](../models-recipes/create-retails-sales-dataset.md).

![schema&#39;s beheren](../images/models-recipes/import-package-ui/manage-schemas.png)

Onder **Het Beheer van de Eigenschap** sectie, selecteer op uw huurdersidentificatie in de schemakijker om het Retailschema van de input van de Verkoop uit te breiden. Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en selecteer **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** in het rechtervenster **[!UICONTROL Field Properties]**. Voor deze zelfstudie stelt u &quot;[!UICONTROL weeklySales]&quot; in als de **[!UICONTROL Target Feature]** en alle andere elementen als **[!UICONTROL Input Feature]**. Selecteer **[!UICONTROL Next]** om uw nieuw gevormd recept te herzien.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteer **[!UICONTROL Finish]** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga aan [volgende stappen](#next-steps) te werk om te weten te komen hoe te om een Model in [!DNL Data Science Workspace] tot stand te brengen gebruikend het pas gecreëerde Retailrecept van de Verkoop.

## Volgende stappen {#next-steps}

Deze zelfstudie gaf inzicht in het configureren en importeren van een recept in [!DNL Data Science Workspace]. U kunt nu een model maken, trainen en evalueren met het nieuwe recept.

- [Een model trainen en evalueren in de gebruikersinterface](./train-evaluate-model-ui.md)
- [Een model trainen en evalueren met behulp van de API](./train-evaluate-model-api.md)