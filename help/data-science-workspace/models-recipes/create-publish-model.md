---
keywords: Experience Platform;machine het leren model;Gegevens Wetenschap Workspace;populaire onderwerpen;creeer en publiceer een model
solution: Experience Platform
title: Een model voor machinaal leren maken en Publish
type: Tutorial
description: In de volgende handleiding worden de stappen beschreven die nodig zijn om een model voor machinaal leren te maken en te publiceren.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---


# Een machine-learningmodel maken en publiceren

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

In de volgende handleiding worden de stappen beschreven die nodig zijn om een model voor machinaal leren te maken en te publiceren. Elke sectie bevat een beschrijving van wat u gaat doen en een verbinding aan de documentatie UI en API om de beschreven stap uit te voeren.

## Aan de slag

Voordat u deze zelfstudie kunt starten, moet u aan de volgende voorwaarden voldoen:

- Toegang tot [!DNL Adobe Experience Platform] . Als u geen toegang hebt tot een organisatie in [!DNL Experience Platform] , neemt u contact op met uw systeembeheerder voordat u verdergaat.

- Alle zelfstudies van Workspace voor gegevenswetenschap gebruiken het Luminantiemodel. Om langs te volgen, moet u de [&#x200B; het voorloodsmodel van de Luma schema&#39;s en datasets &#x200B;](./create-luma-data.md) hebben gecreeerd.

### Ontdek de gegevens en begrijp de schema&#39;s

Login aan [&#x200B; Adobe Experience Platform &#x200B;](https://platform.adobe.com/) en selecteert **[!UICONTROL Datasets]** om van alle bestaande datasets een lijst te maken en de dataset te selecteren die u zou willen onderzoeken. In dit geval, zou u de **het Webgegevens van de Luma** dataset moeten selecteren.

![&#x200B; uitgezochte het Webdataset van de Luma &#x200B;](../images/models-recipes/model-walkthrough/luma-dataset.png)

De activiteitenpagina van de gegevensset wordt geopend en bevat informatie over uw gegevensset. U kunt **[!UICONTROL Preview Dataset]** in de buurt van de rechterbovenhoek selecteren om voorbeeldrecords te bekijken. U kunt het schema voor de geselecteerde dataset ook bekijken.

![&#x200B; voorvertoning het Webgegevens van de Luma &#x200B;](../images/models-recipes/model-walkthrough/preview-dataset.png)

Selecteer de schemakoppeling in het rechterdeelvenster. Als u een pop-up selecteert onder **[!UICONTROL schema name]** , wordt het schema op een nieuw tabblad geopend.

![&#x200B; voorproef het luma schema van Webgegevens &#x200B;](../images/models-recipes/model-walkthrough/preview-schema.png)

U kunt de gegevens verder verkennen met de geleverde EDA-laptop (Exploratory Data Analysis). Deze laptop kan worden gebruikt om inzicht te krijgen in de patronen in de Luminantiemaatgegevens, de gegevenshygiëne te controleren en een overzicht te maken van de relevante gegevens voor het voorspellende-nevenmodel. Meer over de Verkennende Analyse van Gegevens leren, bezoek de [&#x200B; documentatie EDA &#x200B;](../jupyterlab/eda-notebook.md).

## Maak het veelvuldigheidsrecept voor Luma {#author-your-model}

Een belangrijk onderdeel van de levenscyclus van [!DNL Data Science Workspace] is het ontwerpen van Recipes en Modellen. Het nevelingsmodel van Luma is ontworpen om een voorspelling te genereren over de vraag of klanten een hoge neiging hebben om een product van Luma aan te schaffen.

Voor het maken van het model Luma-eigenschappen wordt de sjabloon voor het maken van het recept gebruikt. Ontvangers vormen de basis voor een model, aangezien zij machine het leren algoritmen en logica bevatten die worden ontworpen om specifieke problemen op te lossen. Nog belangrijker is dat met behulp van Ontvangers u het leren van machines in uw organisatie kunt democratiseren, zodat andere gebruikers toegang hebben tot een model voor verschillende gebruiksgevallen zonder dat er code hoeft te worden geschreven.

Volg [&#x200B; creeer een model gebruikend JupyterLab Notitieboekjes &#x200B;](../jupyterlab/create-a-model.md) leerprogramma om het het modelrecept van de Bevolheid van de Luma tot stand te brengen dat in verdere leerprogramma&#39;s wordt gebruikt.

## De invoer en verpakt een recept van externe bronnen (*facultatief*)

Als u een recept wilt importeren en verpakken voor gebruik in Data Science Workspace, moet u de bronbestanden in een archiefbestand plaatsen. Volg het [&#x200B; pakket brondossiers in een recept &#x200B;](./package-source-files-recipe.md) leerprogramma. Deze zelfstudie laat u zien hoe u bronbestanden in een recept kunt plaatsen. Dit is de eerste vereiste stap voor het importeren van een recept naar Data Science Workspace. Zodra de zelfstudie is voltooid, krijgt u een Docker-afbeelding in een Azure Container-register, samen met de bijbehorende afbeelding-URL, met andere woorden een archiefbestand.

Dit archiefdossier kan worden gebruikt om een recept in de Wetenschap van Gegevens te creëren Workspace door het recept te volgen invoerwerkschema gebruikend het [&#x200B; werkschema UI &#x200B;](./import-packaged-recipe-ui.md) of het [&#x200B; API werkschema &#x200B;](./import-packaged-recipe-api.md).

## Een model trainen en evalueren {#train-and-evaluate-your-model}

Nu uw gegevens zijn voorbereid en een recept klaar is, hebt u de mogelijkheid om uw model voor het leren van machines verder te maken, te trainen en te evalueren. Terwijl u de Recipe Builder gebruikt, had u uw model al moeten opleiden, scoren en evalueren voordat u het in een recept hebt verpakt.

Met de gebruikersinterface van Data Science Workspace en de API kunt u uw recept publiceren als een model. Bovendien kunt u specifieke aspecten van uw model verder aanpassen, zoals het toevoegen, verwijderen en wijzigen van hyperparameters.

### Een model maken

Om meer te leren over het creëren van een model gebruikend UI, bezoek de trein en evalueer een model in de Werkruimte van de Wetenschap van Gegevens [&#x200B; UI leerprogramma &#x200B;](./train-evaluate-model-ui.md) of [&#x200B; API leerprogramma &#x200B;](./train-evaluate-model-api.md). In deze zelfstudie wordt een voorbeeld gegeven van het maken, trainen en bijwerken van hyperparameters om uw model verder aan te passen.

>[!NOTE]
>
> Hyperparameters kunnen niet worden geleerd, daarom moeten zij worden toegewezen alvorens de opleidingslooppas voorkomt. Het aanpassen van hyperparameters kan de nauwkeurigheid van uw getrainde model veranderen. Aangezien het optimaliseren van een model een herhalend proces is, kunnen meerdere trainingen nodig zijn voordat een bevredigende evaluatie wordt uitgevoerd.

## Score een model {#score-a-model}

De volgende stap bij het maken en publiceren van een model is het operationeel maken van uw model om inzichten van het datumpeer en het Real-Time Profiel van de Klant te scoren en te verbruiken.

Scores in Data Science Workspace kunnen worden bereikt door invoergegevens in te voeren in een bestaand getraind model. De resultaten van het scoren worden dan opgeslagen en viewable in een gespecificeerde outputdataset als nieuwe partij.

Leren hoe te om uw model te scoren, bezoek de score een model [&#x200B; UI leerprogramma &#x200B;](./score-model-ui.md) of [&#x200B; API leerprogramma &#x200B;](./score-model-api.md).

## Publish a scored model as a service

Met Data Science Workspace kunt u uw getrainde model publiceren als service. Dit laat gebruikers binnen uw organisatie toe om gegevens te scoren zonder de behoefte om hun eigen modellen tot stand te brengen.

Leren hoe te om een model als dienst te publiceren, bezoek het [&#x200B; leerprogramma UI &#x200B;](./publish-model-service-ui.md) of [&#x200B; API leerprogramma &#x200B;](./publish-model-service-api.md).

### Geautomatiseerde training voor een service plannen

Als u een model eenmaal als service hebt gepubliceerd, kunt u geplande scoring- en trainingsprogramma&#39;s voor de leerservice voor uw computer instellen. Het automatiseren van het trainings- en scoringsproces kan de efficiëntie van een service helpen behouden en verbeteren door patronen in uw gegevens bij te houden. Bezoek het [&#x200B; programma een model in de Wetenschap van Gegevens Workspace UI &#x200B;](./schedule-models-ui.md) leerprogramma.

>[!NOTE]
>
> U kunt een model voor geautomatiseerde training en scores alleen plannen vanuit de gebruikersinterface.

## Volgende stappen {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] biedt de tools en resources waarmee je machine-learningmodellen kunt maken, evalueren en gebruiken om data-voorspellingen en -inzichten te genereren. Wanneer inzichten in machine learning worden opgenomen in een [!DNL Profile] -dataset, worden dezelfde gegevens ook ingevoegd als [!DNL Profile] -records die vervolgens kunnen worden gesegmenteerd met [!DNL Adobe Experience Platform Segmentation Service] .

Als profiel- en tijdreeksdata worden opgenomen, besluit Real-Time Customer Profile automatisch om die data uit segmenten op te nemen of uit te sluiten via een doorlopend proces dat streaming segmentatie wordt genoemd, voordat de data worden samengevoegd met bestaande data en de union view wordt bijgewerkt. Hierdoor kun je onmiddellijk berekeningen uitvoeren en beslissingen nemen om klanten verbeterde, geïndividualiseerde ervaringen te bieden terwijl ze interactie hebben met je merk.

Bezoek het leerprogramma voor [&#x200B; verrijkend Real-Time Profiel van de Klant met machine het leren inzichten &#x200B;](./enrich-profile.md) om meer over te leren hoe u machine het leren inzichten kunt gebruiken.
