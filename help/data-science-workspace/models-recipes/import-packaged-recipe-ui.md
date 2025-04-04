---
keywords: Experience Platform;import verpakt recept;Data Science Workspace;populaire onderwerpen;recepten;ui;create engine
solution: Experience Platform
title: Een gecomprimeerde ontvanger importeren in de gebruikersinterface van Data Science Workspace
type: Tutorial
description: Deze zelfstudie biedt insight informatie over het configureren en importeren van een verpakt recept met behulp van het opgegeven voorbeeld Detailhandel. Aan het einde van deze zelfstudie bent u klaar om een model te maken, te trainen en te evalueren in Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 0%

---

# Een verpakt recept importeren in de gebruikersinterface van Data Science Workspace

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Deze zelfstudie biedt insight informatie over het configureren en importeren van een verpakt recept met behulp van het opgegeven voorbeeld Detailhandel. Aan het einde van deze zelfstudie bent u klaar om een model te maken, te trainen en te evalueren in Adobe Experience Platform [!DNL Data Science Workspace] .

## Vereisten

Voor deze zelfstudie is een recept in een pakket nodig in de vorm van een URL voor een Docker-afbeelding. Zie het leerprogramma op hoe te [ brondossiers van het Pakket in Ontvanger ](./package-source-files-recipe.md) voor meer informatie.

## UI-workflow

Voor het importeren van een verpakt recept in [!DNL Data Science Workspace] zijn specifieke recept-configuraties nodig, gecompileerd in één JSON-bestand (JavaScript Object Notation). Deze compilatie van recept-configuraties wordt het configuratiebestand genoemd. Een verpakt recept met een bepaalde set configuraties wordt een recept-exemplaar genoemd. Met één recept kunt u veel recept-instanties maken in [!DNL Data Science Workspace] .

De workflow voor het importeren van een pakketrecept bestaat uit de volgende stappen:
- [Een recept configureren](#configure)
- [Op docker gebaseerd recept importeren - Python](#python)
- [Op Docker gebaseerde recept importeren - R](#r)
- [Op docker gebaseerde recept importeren - PySpark](#pyspark)
- [Op Docker gebaseerde recept importeren - Scala](#scala)

### Een recept configureren {#configure}

Elk recept-exemplaar in [!DNL Data Science Workspace] gaat vergezeld van een set configuraties die het recept-exemplaar aanpassen aan een bepaalde gebruikscase. De dossiers van de configuratie bepalen het standaardopleiding en het scoren gedrag van een Model dat gebruikend dit recept geval wordt gecreeerd.

>[!NOTE]
>
>Configuratiebestanden zijn specifiek voor recept en hoofdletters en kleine letters.

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
| `ACP_DSW_INPUT_FEATURES` | String | Lijst met door komma&#39;s gescheiden invoerschemakenmerken. |
| `ACP_DSW_TARGET_FEATURES` | String | Lijst met door komma&#39;s gescheiden kenmerken van het uitvoerschema. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolean | Hiermee wordt bepaald of invoer- en uitvoerfuncties kunnen worden gewijzigd |
| `tenantId` | String | Deze id zorgt ervoor dat bronnen die u maakt, op de juiste wijze worden benoemd en zich binnen uw organisatie bevinden. [ volg hier de stappen ](../../xdm/api/getting-started.md#know-your-tenant_id) om uw huurdersidentiteitskaart te vinden. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | String | Het invoerschema dat wordt gebruikt voor het trainen van een model. Laat dit leeg wanneer u importeert in de gebruikersinterface, vervang deze door de trainingsschema-id wanneer u importeert met behulp van de API. |
| `evaluation.labelColumn` | String | Kolomlabel voor evaluatievisualisaties. |
| `evaluation.metrics` | String | Door komma&#39;s gescheiden lijst met evaluatiemetriek die moet worden gebruikt voor de evaluatie van een model. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | String | Het uitvoerschema dat voor het scoren van een model wordt gebruikt. Laat dit leeg wanneer u importeert in de gebruikersinterface, vervang het bestand door een SchemaID wanneer u importeert met behulp van de API. |

Voor deze zelfstudie kunt u de standaardconfiguratiebestanden voor het recept voor detailhandel in de [!DNL Data Science Workspace] Referentie opgeven zoals ze zijn.

### Op Docker gebaseerde recept importeren - [!DNL Python] {#python}

Begin door te navigeren en **[!UICONTROL Workflows]** te selecteren in de linkerbovenhoek van de gebruikersinterface van [!DNL Experience Platform] . Daarna, selecteer **het recept van de Invoer** en selecteer **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

**vormt** pagina voor het **recept van de Invoer** werkschema verschijnt. Voer een naam en beschrijving voor het recept in en selecteer vervolgens **[!UICONTROL Next]** in de rechterbovenhoek.

![ vorm werkschema ](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In de [ brondossiers van het Pakket in een Recipe ](./package-source-files-recipe.md) leerprogramma, werd een Docker URL verstrekt aan het eind van de bouw van het Retailrecept van de Verkoop gebruikend Python brondossiers.

Zodra u op de **Uitgezochte bron** pagina bent, kleef het Dok URL die aan het verpakte recept beantwoordt dat gebruikend [!DNL Python] brondossiers in het **[!UICONTROL Source URL]** gebied wordt gebouwd. Daarna, voer het verstrekte configuratiedossier door te slepen en te laten vallen in, of gebruik Browser van het dossiersysteem ****. Het opgegeven configuratiebestand is te vinden op `experience-platform-dsw-reference/recipes/python/retail/retail.config.json` . Selecteer **[!UICONTROL Python]** in de **Runtime** daling neer en **[!UICONTROL Classification]** in de **Type** daling. Zodra alles is ingevuld, uitgezochte **[!UICONTROL Next]** in de hoger-juiste hoek om aan **te werk te gaan leidt schema&#39;s**.

>[!NOTE]
>
> Type ondersteunt **[!UICONTROL Classification]** en **[!UICONTROL Regression]** . Selecteer **[!UICONTROL Custom]** als het model niet onder een van deze typen valt.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Daarna, selecteer de de input en outputschema&#39;s van de Verkoop van de Detailhandel onder de sectie **leiden Schema&#39;s**, werden zij gecreeerd gebruikend het verstrekte laarzentrekkermanuscript in [ creeer het detailhandelschema en dataset ](../models-recipes/create-retails-sales-dataset.md) leerprogramma.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Onder de **sectie van het Beheer van de Eigenschap 0} {, selecteer op uw huurdersidentificatie in de schemakijker om het de inputschema van de Verkoop van de Detailhandel uit te breiden.** Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en selecteer **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** in het rechtervenster **[!UICONTROL Field Properties]** . In deze zelfstudie stelt u **[!UICONTROL weeklySales]** in als de **[!UICONTROL Target Feature]** en alles als **[!UICONTROL Input Feature]** . Selecteer **[!UICONTROL Next]** om uw nieuwe geconfigureerde recept te bekijken.

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteer **[!UICONTROL Finish]** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga aan de [ volgende stappen ](#next-steps) te werk om te weten te komen hoe te om een Model in [!DNL Data Science Workspace] tot stand te brengen gebruikend het pas gecreëerde Commerciële recept van de Verkoop.

### Op Docker gebaseerde recept importeren - R {#r}

Begin door te navigeren en **[!UICONTROL Workflows]** te selecteren in de linkerbovenhoek van de gebruikersinterface van [!DNL Experience Platform] . Daarna, selecteer **het recept van de Invoer** en selecteer **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

**vormt** pagina voor het **recept van de Invoer** werkschema verschijnt. Voer een naam en beschrijving voor het recept in en selecteer vervolgens **[!UICONTROL Next]** in de rechterbovenhoek.

![ vorm werkschema ](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In de [ brondossiers van het Pakket in een Recipe ](./package-source-files-recipe.md) leerprogramma, werd een Docker URL verstrekt aan het eind van de bouw van het Retailrecept van de Verkoop gebruikend R brondossiers.

Zodra u op de **Uitgezochte bron** pagina bent, kleef het Docker URL die aan het verpakte recept beantwoordt dat gebruikend R brondossiers in het **[!UICONTROL Source URL]** gebied wordt gebouwd. Daarna, voer het verstrekte configuratiedossier door te slepen en te laten vallen in, of gebruik Browser van het dossiersysteem ****. Het opgegeven configuratiebestand is te vinden op `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json` . Selecteer **[!UICONTROL R]** in de **Runtime** daling neer en **[!UICONTROL Classification]** in de **Type** daling. Zodra alles is ingevuld, uitgezochte **[!UICONTROL Next]** in de hoger-juiste hoek om aan **te werk te gaan leidt schema&#39;s**.

>[!NOTE]
>
> *Type* steunt **[!UICONTROL Classification]** en **[!UICONTROL Regression]**. Selecteer **[!UICONTROL Custom]** als het model niet onder een van deze typen valt.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Daarna, selecteer de de input en outputschema&#39;s van de Verkoop van de Detailhandel onder de sectie **leiden Schema&#39;s**, werden zij gecreeerd gebruikend het verstrekte laarzentrekkermanuscript in [ creeer het detailhandelschema en dataset ](../models-recipes/create-retails-sales-dataset.md) leerprogramma.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Onder de *sectie van het Beheer van de Eigenschap 0} {, selecteer op uw huurdersidentificatie in de schemakijker om het de inputschema van de Verkoop van de Detailhandel uit te breiden.* Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en selecteer **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** in het rechtervenster **[!UICONTROL Field Properties]** . In deze zelfstudie stelt u **[!UICONTROL weeklySales]** in als de **[!UICONTROL Target Feature]** en alles als **[!UICONTROL Input Feature]** . Selecteer **[!UICONTROL Next]** om uw nieuwe gevormde recept te herzien.

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteer **Afwerking** om het recept tot stand te brengen.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga aan de [ volgende stappen ](#next-steps) te werk om te weten te komen hoe te om een Model in [!DNL Data Science Workspace] tot stand te brengen gebruikend het pas gecreëerde Commerciële recept van de Verkoop.

### Op docker gebaseerde recept importeren - PySpark {#pyspark}

Begin door te navigeren en **[!UICONTROL Workflows]** te selecteren in de linkerbovenhoek van de gebruikersinterface van [!DNL Experience Platform] . Daarna, selecteer **het recept van de Invoer** en selecteer **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

**vormt** pagina voor het **recept van de Invoer** werkschema verschijnt. Voer een naam en beschrijving voor het recept in en selecteer vervolgens **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan.

![ vorm werkschema ](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In de [ brondossiers van het Pakket in een Recipe ](./package-source-files-recipe.md) leerprogramma, werd een Docker URL verstrekt aan het eind van de bouw van het Retailrecept van de Verkoop gebruikend PySpark brondossiers.

Zodra u op de **Uitgezochte bron** pagina bent, kleef het Docker URL die aan het verpakte recept beantwoordt dat gebruikend PySpark brondossiers in het **[!UICONTROL Source URL]** gebied wordt gebouwd. Daarna, voer het verstrekte configuratiedossier door te slepen en te laten vallen in, of gebruik Browser van het dossiersysteem ****. Het opgegeven configuratiebestand is te vinden op `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json` . Selecteer **[!UICONTROL PySpark]** in de **Runtime** daling neer. Wanneer de PySpark-runtime is geselecteerd, wordt het standaardartefact automatisch gevuld tot **[!UICONTROL Docker]** . Daarna, selecteer **[!UICONTROL Classification]** in de **Type** daling neer. Zodra alles is ingevuld, uitgezochte **[!UICONTROL Next]** in de hoger-juiste hoek om aan **te werk te gaan leidt schema&#39;s**.

>[!NOTE]
>
> *Type* steunt **[!UICONTROL Classification]** en **[!UICONTROL Regression]**. Selecteer **[!UICONTROL Custom]** als het model niet onder een van deze typen valt.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Daarna, selecteer de de input en outputschema&#39;s van de Verkoop van de Detailhandel gebruikend **beheert Schema&#39;s** selecteur, werden de schema&#39;s gecreeerd gebruikend het verstrekte laarzentrekkermanuscript in [ creeer het detailhandelschema en de dataset ](../models-recipes/create-retails-sales-dataset.md) leerprogramma.

![ beheert schema&#39;s ](../images/models-recipes/import-package-ui/manage-schemas.png)

Onder de **sectie van het Beheer van de Eigenschap 0} {, selecteer op uw huurdersidentificatie in de schemakijker om het de inputschema van de Verkoop van de Detailhandel uit te breiden.** Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en selecteer **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** in het rechtervenster **[!UICONTROL Field Properties]** . In deze zelfstudie stelt u **[!UICONTROL weeklySales]** in als de **[!UICONTROL Target Feature]** en alles als **[!UICONTROL Input Feature]** . Selecteer **[!UICONTROL Next]** om uw nieuwe geconfigureerde recept te bekijken.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteer **[!UICONTROL Finish]** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga aan de [ volgende stappen ](#next-steps) te werk om te weten te komen hoe te om een Model in [!DNL Data Science Workspace] tot stand te brengen gebruikend het pas gecreëerde Commerciële recept van de Verkoop.

### Op Docker gebaseerde recept importeren - Scala {#scala}

Begin door te navigeren en **[!UICONTROL Workflows]** te selecteren in de linkerbovenhoek van de gebruikersinterface van [!DNL Experience Platform] . Daarna, selecteer **het recept van de Invoer** en selecteer **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

**vormt** pagina voor het **recept van de Invoer** werkschema verschijnt. Voer een naam en beschrijving voor het recept in en selecteer vervolgens **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan.

![ vorm werkschema ](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> In de [ brondossiers van het Pakket in een Recipe ](./package-source-files-recipe.md) leerprogramma, werd een Docker URL verstrekt aan het eind van de bouw van het Retailrecept van de Verkoop gebruikend Scala ([!DNL Spark]) brondossiers.

Zodra u op de **Uitgezochte bron** pagina bent, kleef het Dok URL die aan het verpakte recept beantwoordt dat gebruikend Scala brondossiers in het gebied van Source URL wordt gebouwd. Importeer vervolgens het opgegeven configuratiebestand door te slepen en neer te zetten of gebruik de bestandssysteembrowser. Het opgegeven configuratiebestand is te vinden op `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json` . Selecteer **[!UICONTROL Spark]** in de **Runtime** daling neer. Wanneer de [!DNL Spark] -runtime is geselecteerd, wordt het standaardartefact automatisch gevuld tot **[!UICONTROL Docker]** . Daarna, selecteer **[!UICONTROL Regression]** van het **Type** drop down. Zodra alles is ingevuld, uitgezochte **[!UICONTROL Next]** in de hoger-juiste hoek om aan **te werk te gaan leidt schema&#39;s**.

>[!NOTE]
>
> Type ondersteunt **[!UICONTROL Classification]** en **[!UICONTROL Regression]** . Selecteer **[!UICONTROL Custom]** als het model niet onder een van deze typen valt.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Daarna, selecteer de de input en outputschema&#39;s van de Verkoop van de Detailhandel gebruikend **beheert Schema&#39;s** selecteur, werden de schema&#39;s gecreeerd gebruikend het verstrekte laarzentrekkermanuscript in [ creeer het detailhandelschema en de dataset ](../models-recipes/create-retails-sales-dataset.md) leerprogramma.

![ beheert schema&#39;s ](../images/models-recipes/import-package-ui/manage-schemas.png)

Onder de **sectie van het Beheer van de Eigenschap 0} {, selecteer op uw huurdersidentificatie in de schemakijker om het de inputschema van de Verkoop van de Detailhandel uit te breiden.** Selecteer de invoer- en uitvoerfuncties door de gewenste functie te markeren en selecteer **[!UICONTROL Input Feature]** of **[!UICONTROL Target Feature]** in het rechtervenster **[!UICONTROL Field Properties]** . Voor deze zelfstudie stelt u &quot;[!UICONTROL weeklySales]&quot; in als de **[!UICONTROL Target Feature]** en alles als **[!UICONTROL Input Feature]** . Selecteer **[!UICONTROL Next]** om uw nieuwe geconfigureerde recept te bekijken.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Bekijk het recept, voeg configuraties toe, wijzig of verwijder configuraties zoals nodig. Selecteer **[!UICONTROL Finish]** om het recept te maken.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Ga aan de [ volgende stappen ](#next-steps) te werk om te weten te komen hoe te om een Model in [!DNL Data Science Workspace] tot stand te brengen gebruikend het pas gecreëerde Commerciële recept van de Verkoop.

## Volgende stappen {#next-steps}

Deze zelfstudie biedt insight informatie over het configureren en importeren van een recept in [!DNL Data Science Workspace] . U kunt nu een model maken, trainen en evalueren met het nieuwe recept.

- [Een model trainen en evalueren in de gebruikersinterface](./train-evaluate-model-ui.md)
- [Een model trainen en evalueren met de API](./train-evaluate-model-api.md)
