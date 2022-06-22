---
keywords: Experience Platform;JupyterLab;laptops;Data Science Workspace;populaire onderwerpen;analyseren gegevenslaptops
solution: Experience Platform
title: Uw gegevens analyseren met laptops
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie richt zich op het gebruik van Jupyter-laptops, gebouwd in de Data Science Workspace, voor toegang tot, verkenning en visualisatie van uw gegevens.
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 1e240c710da3fa7ae863377d044308b0bca47c7f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Analyseer uw gegevens met notebooks

Deze zelfstudie richt zich op het gebruik van Jupyter-laptops, gebouwd in de Data Science Workspace, voor toegang tot, verkenning en visualisatie van uw gegevens. Tegen het einde van deze zelfstudie hebt u meer inzicht in enkele functies die Jupyter-laptops bieden om uw gegevens beter te begrijpen.

De volgende concepten worden geïntroduceerd:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) is de volgende generatie web-based interface voor Project Jupyter, en is strak geïntegreerd in [!DNL Adobe Experience Platform].
- **Batches:** Datasets bestaan uit batches. Een batch is een reeks gegevens die over een bepaalde periode worden verzameld en samen als één eenheid worden verwerkt. Nieuwe batches worden gemaakt wanneer gegevens aan een gegevensset worden toegevoegd.
- **SDK voor gegevenstoegang (afgekeurd):** De SDK voor gegevenstoegang is nu afgekeurd. Gebruik de [[!DNL Platform SDK]](../authoring/platform-sdk.md) hulplijn.

## Laptops verkennen in de werkruimte voor wetenschap van gegevens

In deze sectie, worden de gegevens onderzocht die eerder in het detailhandelschema werden opgenomen.

Met de werkruimte voor gegevenswetenschap kunnen gebruikers [!DNL Jupyter Notebooks] via de [!DNL JupyterLab] platform waar ze werkstromen voor machinaal leren kunnen maken en bewerken. [!DNL JupyterLab] is een hulpmiddel voor samenwerking tussen server en client waarmee gebruikers notitieboekjecten kunnen bewerken via een webbrowser. Deze laptops kunnen zowel uitvoerbare code als tekstelementen bevatten. Voor onze doeleinden gebruiken wij Markdown voor analysebeschrijving en uitvoerbaar [!DNL Python] code voor het onderzoeken en analyseren van gegevens.

### Kies uw werkruimte

Bij starten [!DNL JupyterLab]We krijgen een webinterface voor Jupyter-laptops te zien. Afhankelijk van welk type laptop we kiezen, wordt een corresponderende kernel gestart.

Bij het vergelijken van welke omgeving we moeten gebruiken, moeten we rekening houden met de beperkingen van elke service. Als we bijvoorbeeld de opdracht [pandas](https://pandas.pydata.org/) bibliotheek met [!DNL Python]Als normale gebruiker is de maximale RAM-geheugen 2 GB. Zelfs als energiegebruiker zouden we beperkt zijn tot 20 GB RAM. Als het om grotere berekeningen gaat, zou het zinvol zijn om te gebruiken [!DNL Spark] die 1,5 TB biedt en die met alle laptopexemplaren wordt gedeeld.

Standaard werkt Tensorflow-recept in een GPU-cluster en Python in een CPU-cluster.

### Een nieuw notebook maken

In de [!DNL Adobe Experience Platform] UI, selecteer [!UICONTROL Data Science] in het bovenste menu om naar de werkruimte voor wetenschap van gegevens te gaan. Selecteer op deze pagina [!DNL JupyterLab] om de [!DNL JupyterLab] lanceerinrichting. U zou een pagina moeten zien gelijkend op dit.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

In onze zelfstudie gebruiken we [!DNL Python] 3 in het Notitieboekje van de Jupyter om te tonen hoe te om tot de gegevens toegang te hebben en te onderzoeken. Op de pagina Launcher staan voorbeelden van laptops. We gebruiken het winkelrecept voor [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

Het recept van de Verkoop van de Detailhandel is een standalone voorbeeld dat de zelfde detailhandel dataset van de Verkoop gebruikt om te tonen hoe de gegevens in de Notitie van Jupyter kunnen worden onderzocht en worden visualiseerd. Bovendien gaat de laptop dieper in met training en verificatie. Meer informatie over deze specifieke laptop vindt u in deze [wandelpad](../walkthrough.md).

### Toegangsgegevens

>[!NOTE]
>
>De `data_access_sdk_python` is vervangen en niet meer aanbevolen. Raadpleeg de [het omzetten van gegevens toegang SDK in Platform SDK](../authoring/platform-sdk.md) zelfstudie voor het converteren van uw code. Voor deze zelfstudie gelden nog dezelfde stappen.

We gaan over tot interne toegang tot gegevens van [!DNL Adobe Experience Platform] en gegevens extern. We zullen de `data_access_sdk_python` bibliotheek om tot interne gegevens zoals datasets en schema&#39;s toegang te hebben XDM. Voor externe gegevens gebruiken we de panda&#39;s [!DNL Python] bibliotheek.

#### Externe gegevens

Open de Retail Sales-laptop en zoek de header &quot;Load Data&quot;. Het volgende [!DNL Python] code gebruikt pandas `DataFrame` de gegevensstructuur en de [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) functie voor het lezen van de CSV-host op [!DNL Github] in het DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

De gegevensstructuur van Pandas&#39; DataFrame is een tweedimensionale gelabelde gegevensstructuur. Om snel de afmetingen van onze gegevens te zien, kunnen wij gebruiken `df.shape`. Dit keert een tegel terug die de dimensionaliteit van DataFrame vertegenwoordigt:

![](../images/jupyterlab/analyze-data/df_shape.png)

Tot slot kunnen we eens bekijken hoe onze gegevens eruit zien. We kunnen `df.head(n)` om de eerste `n` rijen van het DataFrame:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] data

We gaan nu verder met toegang [!DNL Experience Platform] gegevens.

##### Op gegevensset-id

Voor deze sectie, gebruiken wij de Detailhandel dataset van de Verkoop die de zelfde dataset is die in de de steekproefnotitie van de Verkoop wordt gebruikt.

In Jupyter-laptop hebt u toegang tot uw gegevens via de **Gegevens** tab ![tabblad Gegevens](../images/jupyterlab/analyze-data/dataset-tab.png) links. Als u het tabblad selecteert, worden er twee mappen weergegeven. Selecteer **[!UICONTROL Datasets]** map.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Nu in de folder van Datasets, kunt u alle ingebedde datasets zien. Merk op dat het een minuut kan nemen om alle ingangen te laden als uw folder met datasets zwaar bevolkt is.

Aangezien de dataset het zelfde is, willen wij de ladingsgegevens van de vorige sectie vervangen die externe gegevens gebruikt. Selecteer het codeblok onder **Gegevens laden** en druk op **&quot;d&quot;** tweemaal op het toetsenbord. Zorg ervoor dat de focus zich op het blok bevindt en niet in de tekst. U kunt op **&quot;esc&quot;** om de tekstfocus te verlaten voordat u op **&quot;d&quot;** twee keer.

Nu kunnen we met de rechtermuisknop op de knop `Retail-Training-<your-alias>` dataset en selecteer de optie &quot;Onderzoek Gegevens in Notitieboekje&quot;in dropdown. Er wordt een uitvoerbaar code-item in uw notitieboekje weergegeven.

>[!TIP]
>
>Zie de [[!DNL Platform SDK]](../authoring/platform-sdk.md) handleiding voor het converteren van code.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Als u met andere kernels werkt dan [!DNL Python], raadpleeg [deze pagina](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) voor toegang tot gegevens over de [!DNL Adobe Experience Platform].

Als u de cel van het uitvoerbare bestand selecteert en vervolgens op de afspeelknop op de werkbalk drukt, wordt de uitvoerbare code uitgevoerd. De uitvoer voor `head()` zal een lijst met de sleutels van uw dataset als kolommen en eerste n rijen in de dataset zijn. `head()` Accepteert een geheel argument om te specificeren hoeveel lijnen aan output. Standaard is dit 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Als u de kernel opnieuw opstart en alle cellen opnieuw uitvoert, krijgt u dezelfde uitvoer als voorheen.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Uw gegevens verkennen

Nu wij tot uw gegevens kunnen toegang hebben, laten wij nadruk op de gegevens zelf door statistieken en visualisatie te gebruiken. De dataset die wij gebruiken is een detailgegevensset die diverse informatie over 45 verschillende opslag op een bepaalde dag geeft. Sommige kenmerken van een bepaalde `date` en `store` het volgende opnemen:
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

We kunnen gebruikmaken van [!DNL Python's] pandabibliotheek om het gegevenstype van elk kenmerk op te halen. De output van de volgende vraag zal ons informatie over het aantal ingangen en het gegevenstype voor elk van de kolommen geven:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Deze informatie is nuttig aangezien het weten van het gegevenstype voor elke kolom ons zal toelaten om te weten hoe te om de gegevens te behandelen.

Laten we nu eens kijken naar de statistische samenvatting. Alleen de numerieke gegevenstypen worden weergegeven, dus `date`, `storeType`, en `isHoliday` wordt niet uitgevoerd:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

We zien dat er 6435 gevallen zijn voor elk kenmerk. Daarnaast worden statistische informatie gegeven zoals gemiddelde, standaardafwijking (std), min, max en interkwartielen. Dit geeft ons informatie over de afwijking voor de gegevens. In de volgende sectie gaan we over tot visualisatie die samen met deze informatie werkt om ons een goed inzicht te geven in onze gegevens.

De minimum- en maximumwaarden voor `store`We kunnen zien dat er 45 unieke opslagplaatsen zijn die de gegevens vertegenwoordigen. Er zijn ook `storeTypes` die onderscheid maken tussen wat een winkel is. We zien de verdeling van `storeTypes` door het volgende te doen:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Dit betekent dat 22 opslagplaatsen `storeType` `A`, zijn 17 `storeType` `B`, en 6 `storeType` `C`.

#### Gegevensvisualisatie

Nu we onze gegevenskaderwaarden kennen, willen we dit aanvullen met visualisaties om de dingen duidelijker en makkelijker te maken om patronen te identificeren. Grafieken zijn ook handig wanneer u resultaten naar een publiek verzendt. Sommige [!DNL Python] bibliotheken die nuttig zijn voor visualisatie zijn onder meer:
- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [gumpje](https://ggplot2.tidyverse.org/)

In deze sectie gaan we snel over enkele voordelen voor het gebruik van elke bibliotheek.

[Matplotlib](https://matplotlib.org/) is de oudste [!DNL Python] visualisatiepakket. Hun doel is om &quot;gemakkelijke en moeilijke dingen mogelijk te maken&quot;. Dit is meestal het geval omdat het pakket uiterst krachtig is, maar ook ingewikkeld. Het is niet altijd gemakkelijk om een redelijke grafiek te krijgen zonder veel tijd en moeite te nemen.

[Pandas](https://pandas.pydata.org/) wordt voornamelijk gebruikt voor het DataFrame-object dat gegevensmanipulatie met geïntegreerde indexering mogelijk maakt. Panda&#39;s bevatten echter ook een ingebouwde functie voor het uitzetten van beelden die is gebaseerd op matplotlib.

[seaborn](https://seaborn.pydata.org/) is een pakket dat bovenop matplotlib wordt gebouwd. Het hoofddoel is standaardgrafieken visueel aantrekkelijker te maken en het maken van gecompliceerde grafieken te vereenvoudigen.

[gumpje](https://ggplot2.tidyverse.org/) is een pakket dat ook boven op matplotlib is gebouwd. Nochtans is het belangrijkste verschil dat het hulpmiddel een haven van gplot2 voor R is. Net als bij seaborn is het doel om matplotlib beter te krijgen. De gebruikers die met gplot2 voor R vertrouwd zijn zouden deze bibliotheek moeten overwegen.


##### Grafieken gelijktrekken

Univariate grafieken zijn percelen van een individuele variabele. Een uniforme grafiek wordt gebruikt om uw gegevens te visualiseren is de doos en de whiskergrafiek.

Met behulp van onze detailhandelsdataset van voordien, kunnen wij de doos en de whiskerperceel voor elk van 45 winkels en hun wekelijkse verkoop produceren. Het perceel wordt geproduceerd gebruikend `seaborn.boxplot` functie.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Een doos en een whiskerplot worden gebruikt om de verspreiding van gegevens te tonen. De buitenlijnen van het waarnemingspunt tonen de bovenste en onderste kwartiel, terwijl de doos het interkwartielbereik beslaat. De regel in het vak markeert de mediaan. Alle gegevenspunten die meer dan 1,5 keer het bovenste of onderste kwartiel bedragen, worden als een cirkel gemarkeerd. Deze punten worden beschouwd als uitschieters.

##### Meerdere grafieken

Meerdere percelen worden gebruikt om de interactie tussen variabelen te zien. Met de visualisatie kunnen wetenschappers van data zien of er correlaties of patronen zijn tussen de variabelen. Een veelgebruikte multivariate grafiek is een correlatiematrix. Met een correlatiematrix worden de afhankelijkheden tussen meerdere variabelen gekwantificeerd aan de hand van de correlatiecoëfficiënt.

Gebruikend de zelfde kleinhandelsdataset, kunnen wij de correlatiematrix produceren.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Merk op dat 1 diagonaal naar beneden is. Dit toont aan dat wanneer het vergelijken van een variabele aan zich, het volledige positieve correlatie heeft. Sterke positieve correlatie zal een grootte dichter bij 1 hebben, terwijl zwakke correlaties dichter bij 0 liggen. Een negatieve correlatie wordt aangetoond met een negatieve coëfficiënt die een omgekeerde trend laat zien.


## Volgende stappen

In deze zelfstudie wordt uitgelegd hoe u een nieuw Jupyter-notebook maakt in de Data Science Workspace en hoe u toegang krijgt tot gegevens van buitenaf en van [!DNL Adobe Experience Platform]. We hebben met name de volgende stappen doorlopen:
- Een nieuwe jupyter-laptop maken
- Gegevensbestanden en schema&#39;s voor toegang
- Gegevenssets verkennen

Nu ben je klaar om door te gaan naar de [volgende sectie](../models-recipes/package-source-files-recipe.md) om een recept te verpakken en in de Werkruimte van de Wetenschap van Gegevens te importeren.
