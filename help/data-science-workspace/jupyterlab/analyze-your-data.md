---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;populaire onderwerpen;analyse gegevenslaptops
solution: Experience Platform
title: Uw gegevens analyseren met laptops
type: Tutorial
description: Deze zelfstudie richt zich op het gebruik van Jupyter-laptops, gebouwd in Data Science Workspace, voor toegang tot, verkenning en visualisatie van uw gegevens.
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 0%

---

# Analyseer uw gegevens met behulp van laptops

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Deze zelfstudie richt zich op het gebruik van Jupyter-laptops, gebouwd in Data Science Workspace, voor toegang tot, verkenning en visualisatie van uw gegevens. Tegen het einde van deze zelfstudie hebt u meer inzicht in enkele functies die Jupyter-laptops bieden om uw gegevens beter te begrijpen.

De volgende concepten worden geïntroduceerd:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab] &#x200B;](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) is de volgende-generatie web-based interface voor Project Jupyter, en is strak geïntegreerd in [!DNL Adobe Experience Platform].
- **de Banden:** Datasets worden samengesteld uit partijen. Een batch is een reeks gegevens die over een bepaalde periode worden verzameld en samen als één eenheid worden verwerkt. Nieuwe batches worden gemaakt wanneer gegevens aan een gegevensset worden toegevoegd.
- **SDK van de Toegang van Gegevens (afgekeurd):** De Toegang SDK van Gegevens is nu afgekeurd. Gebruik de handleiding [[!DNL Experience Platform SDK]](../authoring/platform-sdk.md) .

## Ontdek notebooks in Data Science Workspace

In deze sectie, worden de gegevens onderzocht die eerder in het detailhandelschema werden opgenomen.

Met Data Science Workspace kunnen gebruikers [!DNL Jupyter Notebooks] maken via het [!DNL JupyterLab] -platform waar ze werkstromen voor machinaal leren kunnen maken en bewerken. [!DNL JupyterLab] is een hulpmiddel voor samenwerking tussen server en client waarmee gebruikers notitieboekjecten kunnen bewerken via een webbrowser. Deze laptops kunnen zowel uitvoerbare code als tekstelementen bevatten. Voor onze doeleinden gebruiken we Markdown voor analysebeschrijving en uitvoerbare [!DNL Python] code om gegevensexploratie en -analyse uit te voeren.

### Kies uw werkruimte

Bij het starten van [!DNL JupyterLab] krijgen we een webinterface voor Jupyter-laptops te zien. Afhankelijk van welk type laptop we kiezen, wordt een corresponderende kernel gestart.

Bij het vergelijken van welke omgeving we moeten gebruiken, moeten we rekening houden met de beperkingen van elke service. Bijvoorbeeld, als wij de [&#x200B; pandas &#x200B;](https://pandas.pydata.org/) bibliotheek met [!DNL Python] gebruiken, als regelmatige gebruiker is de grens van RAM 2 GB. Zelfs als energiegebruiker zouden we beperkt zijn tot 20 GB RAM. Als u werkt met grotere berekeningen, is het handig om [!DNL Spark] te gebruiken, dat 1,5 TB biedt dat wordt gedeeld met alle laptopexemplaren.

Standaard werkt Tensorflow-recept in een GPU-cluster en Python in een CPU-cluster.

### Een nieuw notebook maken

Selecteer in de gebruikersinterface van [!DNL Adobe Experience Platform] de optie [!UICONTROL Data Science] in het bovenste menu om naar de Data Science Workspace te gaan. Selecteer op deze pagina [!DNL JupyterLab] om de [!DNL JupyterLab] launcher te openen. U zou een pagina moeten zien gelijkend op dit.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

In onze zelfstudie gebruiken we [!DNL Python] 3 in het Jupyter-notebook om te tonen hoe we de gegevens kunnen openen en verkennen. Op de pagina Launcher staan voorbeelden van laptops. We gebruiken het winkelrecept voor [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

Het recept van de Verkoop van de Detailhandel is een standalone voorbeeld dat de zelfde Detailhandel dataset van de Verkoop gebruikt om te tonen hoe de gegevens in de Notitie van Jupyter kunnen worden onderzocht en worden visualiseerd. Bovendien gaat de laptop dieper in met training en verificatie. Meer informatie over dit specifieke notitieboekje kan in deze [&#x200B; analyse &#x200B;](../walkthrough.md) worden gevonden.

### Toegangsgegevens

>[!NOTE]
>
>`data_access_sdk_python` is afgekeurd en wordt niet meer aanbevolen. Gelieve te verwijzen naar het [&#x200B; omzetten van gegevenstoegang SDK in Experience Platform SDK &#x200B;](../authoring/platform-sdk.md) leerprogramma om uw code om te zetten. Voor deze zelfstudie gelden nog dezelfde stappen.

We gaan over tot interne toegang tot gegevens van [!DNL Adobe Experience Platform] en externe gegevens. We gebruiken de `data_access_sdk_python` -bibliotheek voor toegang tot interne gegevens, zoals gegevenssets en XDM-schema&#39;s. Voor externe gegevens gebruiken we de bibliotheek met panda&#39;s [!DNL Python] .

#### Externe gegevens

Open de Retail Sales-laptop en zoek de header &quot;Load Data&quot;. De volgende [!DNL Python] code gebruikt pandas&#39; `DataFrame` gegevensstructuur en [&#x200B; read_csv () &#x200B;](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) functie om CSV te lezen die op [!DNL Github] in DataFrame wordt ontvangen:

![](../images/jupyterlab/analyze-data/read_csv.png)

De gegevensstructuur van Pandas&#39; DataFrame is een tweedimensionale gelabelde gegevensstructuur. We kunnen de `df.shape` gebruiken om snel de afmetingen van onze gegevens te zien. Dit keert een tegel terug die de dimensionaliteit van DataFrame vertegenwoordigt:

![](../images/jupyterlab/analyze-data/df_shape.png)

Tot slot kunnen we eens bekijken hoe onze gegevens eruit zien. Met `df.head(n)` kunt u de eerste `n` rijen van het DataFrame weergeven:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] gegevens

Nu gaan we verder met het benaderen van [!DNL Experience Platform] -gegevens.

##### Op gegevensset-id

Voor deze sectie, gebruiken wij de Detailhandel dataset van de Verkoop die de zelfde dataset is in de de steekproefnotitie van de Verkoop wordt gebruikt.

In Jupyter Notitieboekje, kunt u tot uw gegevens van het **lusje van Gegevens** toegang hebben ![&#x200B; op de linkerzijde. &#x200B;](../images/jupyterlab/analyze-data/dataset-tab.png) Als u het tabblad selecteert, worden er twee mappen weergegeven. Selecteer de map **[!UICONTROL Datasets]** .

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Nu in de folder van Datasets, kunt u alle ingebedde datasets zien. Merk op dat het een minuut kan nemen om alle ingangen te laden als uw folder met datasets zwaar bevolkt is.

Aangezien de dataset het zelfde is, willen wij de ladingsgegevens van de vorige sectie vervangen die externe gegevens gebruikt. Selecteer het codeblok onder **Gegevens van de Lading** en druk tweemaal **&quot;d&#39;** sleutel op uw toetsenbord. Zorg ervoor dat de focus zich op het blok bevindt en niet in de tekst. U kunt **&quot;esc&quot;drukken** om de tekstnadruk te ontsnappen alvorens **te drukken &quot;d&quot;** tweemaal.

Nu, kunnen wij op de `Retail-Training-<your-alias>` dataset met de rechtermuisknop klikken en de &quot;Onderzoek Gegevens in Notitieboekje&quot;optie in dropdown selecteren. Er wordt een uitvoerbaar code-item in uw notitieboekje weergegeven.

>[!TIP]
>
>Raadpleeg de handleiding van [[!DNL Experience Platform SDK]](../authoring/platform-sdk.md) voor het converteren van uw code.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Als u aan andere kernels buiten [!DNL Python] werkt, gelieve te verwijzen naar [&#x200B; deze pagina &#x200B;](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) om tot gegevens op [!DNL Adobe Experience Platform] toegang te hebben.

Als u de cel van het uitvoerbare bestand selecteert en vervolgens op de afspeelknop op de werkbalk drukt, wordt de uitvoerbare code uitgevoerd. De uitvoer voor `head()` zal een lijst met de sleutels van uw dataset als kolommen en eerste n rijen in de dataset zijn. `head()` accepteert een argument van het type integer om op te geven hoeveel regels moeten worden uitgevoerd. Standaard is dit 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Als u de kernel opnieuw opstart en alle cellen opnieuw uitvoert, krijgt u dezelfde uitvoer als voorheen.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Uw gegevens verkennen

Nu wij tot uw gegevens kunnen toegang hebben, laten wij nadruk op de gegevens zelf door statistieken en visualisatie te gebruiken. De dataset die wij gebruiken is een detailgegevensset die diverse informatie over 45 verschillende opslag op een bepaalde dag geeft. Enkele kenmerken voor een bepaalde `date` en `store` zijn:

- `storeType`
- `weeklySales`
- `storeSize`
- `temperature`
- `regionalFuelPrice`
- `markDown`
- `cpi`
- `unemployment`
- `isHoliday`

#### Statistisch overzicht

Met [!DNL Python's] pandas-bibliotheek kunnen we het gegevenstype van elk kenmerk ophalen. De output van de volgende vraag zal ons informatie over het aantal ingangen en het gegevenstype voor elk van de kolommen geven:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Deze informatie is nuttig aangezien het weten van het gegevenstype voor elke kolom ons zal toelaten om te weten hoe te om de gegevens te behandelen.

Laten we nu eens kijken naar de statistische samenvatting. Alleen de numerieke gegevenstypen worden weergegeven, dus `date` , `storeType` en `isHoliday` worden niet uitgevoerd:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

We zien dat er 6435 gevallen zijn voor elk kenmerk. Daarnaast worden statistische informatie gegeven zoals gemiddelde, standaardafwijking (std), min, max en interkwartielen. Dit geeft ons informatie over de afwijking voor de gegevens. In de volgende sectie gaan we over tot visualisatie die samen met deze informatie werkt om ons een goed inzicht te geven in onze gegevens.

Als u de minimum- en maximumwaarden voor `store` bekijkt, ziet u dat er 45 unieke opslagruimten zijn waarin de gegevens staan. Er zijn ook `storeTypes` die onderscheid maken tussen wat een winkel is. U kunt de verdeling van `storeTypes` als volgt zien:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Dit betekent dat er 22 winkels zijn van `storeType` `A` , 17 van `storeType` `B` en 6 van `storeType` `C` .

#### Gegevensvisualisatie

Nu we onze gegevenskaderwaarden kennen, willen we dit aanvullen met visualisaties om de dingen duidelijker en makkelijker te maken om patronen te identificeren. Grafieken zijn ook handig wanneer u resultaten naar een publiek verzendt. Enkele [!DNL Python] -bibliotheken die nuttig zijn voor visualisatie zijn onder andere:

- [&#x200B; Matplotlib &#x200B;](https://matplotlib.org/)
- [&#x200B; pandas &#x200B;](https://pandas.pydata.org/)
- [&#x200B; seaborn &#x200B;](https://seaborn.pydata.org/)
- [&#x200B; gplot &#x200B;](https://ggplot2.tidyverse.org/)

In deze sectie gaan we snel over enkele voordelen voor het gebruik van elke bibliotheek.

[&#x200B; Matplotlib &#x200B;](https://matplotlib.org/) is het oudste [!DNL Python] visualisatiepakket. Hun doel is om &quot;gemakkelijke en moeilijke dingen mogelijk te maken&quot;. Dit is meestal het geval omdat het pakket uiterst krachtig is, maar ook ingewikkeld. Het is niet altijd gemakkelijk om een redelijke grafiek te krijgen zonder veel tijd en moeite te nemen.

[&#x200B; Pandas &#x200B;](https://pandas.pydata.org/) wordt hoofdzakelijk gebruikt voor zijn voorwerp DataFrame dat voor gegevensmanipulatie met geïntegreerde indexering toestaat. Panda&#39;s bevatten echter ook een ingebouwde functie voor het uitzetten van beelden die is gebaseerd op matplotlib.

[&#x200B; seaborn &#x200B;](https://seaborn.pydata.org/) is een pakket bouwt bovenop matplotlib. Het hoofddoel is standaardgrafieken visueel aantrekkelijker te maken en het maken van gecompliceerde grafieken te vereenvoudigen.

[&#x200B; gplot &#x200B;](https://ggplot2.tidyverse.org/) is een pakket dat ook bovenop matplotlib wordt gebouwd. Het belangrijkste verschil is echter dat het gereedschap een haven is van ggplot2 voor R. Net als voor Seaborn, is het doel om matplotlib beter te maken. De gebruikers die met gplot2 voor R vertrouwd zijn zouden deze bibliotheek moeten overwegen.


##### Grafieken gelijktrekken

Univariate grafieken zijn percelen van een individuele variabele. Een uniforme grafiek wordt gebruikt om uw gegevens te visualiseren is de doos en de whiskergrafiek.

Met behulp van onze detailhandelsdataset van voordien, kunnen wij de doos en de whiskerperceel voor elk van 45 winkels en hun wekelijkse verkoop produceren. Het waarnemingspunt wordt geproduceerd gebruikend de `seaborn.boxplot` functie.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Een doos en een whiskerplot worden gebruikt om de verspreiding van gegevens te tonen. De buitenlijnen van het waarnemingspunt tonen de bovenste en onderste kwartiel, terwijl de doos het interkwartielbereik beslaat. De regel in het vak markeert de mediaan. Alle gegevenspunten die meer dan 1,5 keer het bovenste of onderste kwartiel bedragen, worden als een cirkel gemarkeerd. Deze punten worden beschouwd als uitschieters.

##### Meerdere grafieken

Meerdere percelen worden gebruikt om de interactie tussen variabelen te zien. Met de visualisatie kunnen wetenschappers van data zien of er correlaties of patronen zijn tussen de variabelen. Een veelgebruikte multivariate grafiek is een correlatiematrix. Met een correlatiematrix worden de afhankelijkheden tussen meerdere variabelen gekwantificeerd aan de hand van de correlatiecoëfficiënt.

Gebruikend de zelfde kleinhandelsdataset, kunnen wij de correlatiematrix produceren.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Merk op dat 1 diagonaal naar beneden is. Dit toont aan dat wanneer het vergelijken van een variabele aan zich, het volledige positieve correlatie heeft. Sterke positieve correlatie zal een grootte dichter bij 1 hebben, terwijl zwakke correlaties dichter bij 0 liggen. Een negatieve correlatie wordt aangetoond met een negatieve coëfficiënt die een omgekeerde trend laat zien.


## Volgende stappen

In deze zelfstudie wordt uitgelegd hoe u een nieuw Jupyter-notebook kunt maken in de Data Science Workspace en hoe u toegang kunt krijgen tot gegevens zowel extern als vanuit [!DNL Adobe Experience Platform] . We hebben met name de volgende stappen doorlopen:

- Een nieuwe jupyter-laptop maken
- Gegevensbestanden en schema&#39;s voor toegang
- Gegevenssets verkennen

Nu bent u bereid om naar de [&#x200B; volgende sectie &#x200B;](../models-recipes/package-source-files-recipe.md) te gaan om een recept te verpakken en in de Wetenschap van Gegevens Workspace in te voeren.
