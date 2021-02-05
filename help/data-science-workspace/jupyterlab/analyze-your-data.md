---
keywords: Experience Platform;JupyterLab;laptops;Data Science Workspace;populaire onderwerpen;analyseren gegevenslaptops
solution: Experience Platform
title: Uw gegevens analyseren met laptops
topic: tutorial
type: Tutorial
description: Deze zelfstudie richt zich op het gebruik van Jupyter-laptops, gebouwd in de Data Science Workspace, voor toegang tot, verkenning en visualisatie van uw gegevens.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---


# Analyseer uw gegevens met notebooks

Deze zelfstudie richt zich op het gebruik van Jupyter-laptops, gebouwd in de Data Science Workspace, voor toegang tot, verkenning en visualisatie van uw gegevens. Tegen het einde van deze zelfstudie hebt u meer inzicht in enkele functies die Jupyter-laptops bieden om uw gegevens beter te begrijpen.

De volgende concepten worden geïntroduceerd:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) is de volgende-generatie web-based interface voor Project Jupyter, en is strak geïntegreerd in  [!DNL Adobe Experience Platform].
- **Batches:** Datasets bestaan uit batches. Een batch is een reeks gegevens die over een bepaalde periode worden verzameld en samen als één eenheid worden verwerkt. Nieuwe batches worden gemaakt wanneer gegevens aan een gegevensset worden toegevoegd.
- **SDK voor gegevenstoegang (afgekeurd):** De SDK voor gegevenstoegang is nu afgekeurd. Gebruik de [[!DNL Platform SDK]](../authoring/platform-sdk.md)-handleiding.

## Laptops verkennen in de werkruimte voor wetenschap van gegevens

In deze sectie, worden de gegevens onderzocht die eerder in het detailhandelschema werden opgenomen.

Met de werkruimte voor gegevenswetenschap kunnen gebruikers [!DNL Jupyter Notebooks] maken via het [!DNL JupyterLab]-platform waar ze werkstromen voor machinaal leren kunnen maken en bewerken. [!DNL JupyterLab] is een hulpmiddel voor samenwerking tussen server en client waarmee gebruikers notitieboekjecten kunnen bewerken via een webbrowser. Deze laptops kunnen zowel uitvoerbare code als tekstelementen bevatten. Voor onze doeleinden, zullen wij Markdown voor analysebeschrijving en uitvoerbare [!DNL Python] code gebruiken om gegevensonderzoek en analyse uit te voeren.

### Kies uw werkruimte

Bij het starten van [!DNL JupyterLab] wordt een webinterface voor Jupyter-laptops weergegeven. Afhankelijk van welk type laptop we kiezen, wordt een corresponderende kernel gestart.

Bij het vergelijken van welke omgeving we moeten gebruiken, moeten we rekening houden met de beperkingen van elke service. Als we bijvoorbeeld de [pandas](https://pandas.pydata.org/)-bibliotheek gebruiken met [!DNL Python], is de RAM-limiet voor gewone gebruikers 2 GB. Zelfs als energiegebruiker zouden we beperkt zijn tot 20 GB RAM. Als u werkt met grotere berekeningen, is het verstandig om [!DNL Spark] te gebruiken, die 1,5 TB biedt, dat wordt gedeeld met alle laptopexemplaren.

Standaard werkt Tensorflow-recept in een GPU-cluster en Python in een CPU-cluster.

### Een nieuw notebook maken

In [!DNL Adobe Experience Platform] UI, klik op het lusje van de Wetenschap van Gegevens in het hoogste menu om u aan de Werkruimte van de Wetenschap van Gegevens te nemen. Klik op het tabblad [!DNL JupyterLab] van deze pagina om de [!DNL JupyterLab]-startprogramma te openen. U zou een pagina moeten zien gelijkend op dit.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher.png)

In onze zelfstudie gebruiken we [!DNL Python] 3 in het Jupyter-notebook om te tonen hoe we de gegevens kunnen openen en verkennen. Op de pagina Launcher staan voorbeelden van laptops. We gebruiken het winkelrecept voor [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

Het recept van de Verkoop van de Detailhandel is een standalone voorbeeld dat de zelfde detailhandel dataset van de Verkoop gebruikt om te tonen hoe de gegevens in de Notitie van Jupyter kunnen worden onderzocht en worden visualiseerd. Bovendien gaat de laptop dieper in met training en verificatie. Meer informatie over deze specifieke laptop vindt u in deze [doorhaling](../walkthrough.md).

### Toegangsgegevens

>[!NOTE]
>
>De instructie `data_access_sdk_python` is afgekeurd en wordt niet langer aanbevolen. Raadpleeg de zelfstudie [SDK voor gegevenstoegang converteren naar SDK van Platform](../authoring/platform-sdk.md) voor het converteren van uw code. Voor deze zelfstudie gelden nog dezelfde stappen.

We gaan intern gegevens van [!DNL Adobe Experience Platform] en externe gegevens gebruiken. Wij zullen `data_access_sdk_python` bibliotheek gebruiken om tot interne gegevens zoals datasets en schema&#39;s toegang te hebben XDM. Voor externe gegevens gebruiken we de [!DNL Python]-bibliotheek voor panda&#39;s.

#### Externe gegevens

Open de Retail Sales-laptop en zoek de header &quot;Load Data&quot;. De volgende [!DNL Python]-code gebruikt pandas&#39; `DataFrame`-gegevensstructuur en de functie [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) om de CSV te lezen die op [!DNL Github] wordt gehost in het DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

De gegevensstructuur van Pandas&#39; DataFrame is een tweedimensionale gelabelde gegevensstructuur. Om snel de afmetingen van onze gegevens te zien, kunnen wij `df.shape` gebruiken. Dit keert een tegel terug die de dimensionaliteit van DataFrame vertegenwoordigt:

![](../images/jupyterlab/analyze-data/df_shape.png)

Tot slot kunnen we eens bekijken hoe onze gegevens eruit zien. Met `df.head(n)` kunt u de eerste `n` rijen van het DataFrame weergeven:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] data

We gaan nu verder met het openen van [!DNL Experience Platform]-gegevens.

##### Op gegevensset-id

Voor deze sectie, gebruiken wij de Detailhandel dataset van de Verkoop die de zelfde dataset is die in de de steekproefnotitie van de Verkoop wordt gebruikt.

In ons Jupyter-notebook hebben we toegang tot onze gegevens via het tabblad **Gegevens** links. Als u op het tabblad klikt, wordt een lijst met gegevenssets weergegeven.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Nu in de folder van Datasets, zullen wij alle ingebedde datasets kunnen zien. Merk op dat het een minuut kan nemen om alle ingangen te laden als uw folder met datasets zwaar bevolkt is.

Aangezien de dataset het zelfde is, willen wij de ladingsgegevens van de vorige sectie vervangen die externe gegevens gebruikt. Selecteer het codeblok onder **Gegevens laden** en druk tweemaal op **&#39;d&#39;** op uw toetsenbord. Zorg ervoor dat de focus zich op het blok bevindt en niet in de tekst. U kunt **&#39;esc&#39;** drukken om de tekstnadruk te ontsnappen alvorens **&#39;d&#39;** tweemaal te drukken.

Nu, kunnen wij op de `Retail-Training-<your-alias>` dataset met de rechtermuisknop klikken en de &quot;Onderzoek Gegevens in Notitieboekje&quot;optie in dropdown selecteren. Er wordt een uitvoerbaar code-item in uw notitieboekje weergegeven.

>[!TIP]
>
>Raadpleeg de handleiding [[!DNL Platform SDK]](../authoring/platform-sdk.md) om uw code om te zetten.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Als u aan andere kernels dan [!DNL Python] werkt, te verwijzen gelieve [deze pagina](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) om tot gegevens op [!DNL Adobe Experience Platform] toegang te hebben.

Als u de cel van het uitvoerbare bestand selecteert en vervolgens op de afspeelknop op de werkbalk drukt, wordt de uitvoerbare code uitgevoerd. De output voor `head()` zal een lijst met de sleutels van uw dataset als kolommen en eerste n rijen in de dataset zijn. `head()` Accepteert een geheel argument om te specificeren hoeveel lijnen aan output. Standaard is dit 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Als u de kernel opnieuw opstart en alle cellen opnieuw uitvoert, krijgt u dezelfde uitvoer als voorheen.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Uw gegevens verkennen

Nu wij tot uw gegevens kunnen toegang hebben, laten wij nadruk op de gegevens zelf door statistieken en visualisatie te gebruiken. De dataset die wij gebruiken is een detailgegevensset die diverse informatie over 45 verschillende opslag op een bepaalde dag geeft. Enkele kenmerken voor een gegeven `date` en `store` omvatten het volgende:
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

We kunnen de pandabibliotheek [!DNL Python's] gebruiken om het gegevenstype van elk kenmerk op te halen. De output van de volgende vraag zal ons informatie over het aantal ingangen en het gegevenstype voor elk van de kolommen geven:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Deze informatie is nuttig aangezien het weten van het gegevenstype voor elke kolom ons zal toelaten om te weten hoe te om de gegevens te behandelen.

Laten we nu eens kijken naar de statistische samenvatting. Alleen de numerieke gegevenstypen worden weergegeven, zodat `date`, `storeType` en `isHoliday` niet worden uitgevoerd:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

We zien dat er 6435 gevallen zijn voor elk kenmerk. Daarnaast worden statistische informatie gegeven zoals gemiddelde, standaardafwijking (std), min, max en interkwartielen. Dit geeft ons informatie over de afwijking voor de gegevens. In de volgende sectie gaan we over tot visualisatie die samen met deze informatie werkt om ons een goed inzicht te geven in onze gegevens.

Als u de minimum- en maximumwaarden voor `store` bekijkt, kunt u zien dat er 45 unieke opslagruimten zijn waarin de gegevens zich bevinden. Er zijn ook `storeTypes` die onderscheiden wat een opslag is. We kunnen de distributie van `storeTypes` als volgt zien:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Dit betekent dat er 22 opslagruimten zijn van `storeType` `A`, 17 zijn `storeType` `B` en 6 zijn `storeType` `C`.

#### Gegevensvisualisatie

Nu we onze gegevenskaderwaarden kennen, willen we dit aanvullen met visualisaties om de dingen duidelijker en makkelijker te maken om patronen te identificeren. Grafieken zijn ook handig wanneer u resultaten naar een publiek verzendt. Enkele [!DNL Python]-bibliotheken zijn handig voor visualisatie:
- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [gumpje](https://ggplot2.tidyverse.org/)

In deze sectie gaan we snel over enkele voordelen voor het gebruik van elke bibliotheek.

[](https://matplotlib.org/) Matplotlibis is het oudste  [!DNL Python] visualisatiepakket. Hun doel is om &quot;gemakkelijke en moeilijke dingen mogelijk te maken&quot;. Dit is meestal het geval omdat het pakket uiterst krachtig is, maar ook ingewikkeld. Het is niet altijd gemakkelijk om een redelijke grafiek te krijgen zonder veel tijd en moeite te nemen.

[De ](https://pandas.pydata.org/) Pandasis wordt hoofdzakelijk gebruikt voor zijn voorwerp DataFrame dat voor gegevensmanipulatie met geïntegreerde indexering toestaat. Panda&#39;s bevatten echter ook een ingebouwde functie voor het uitzetten van beelden die is gebaseerd op matplotlib.

[](https://seaborn.pydata.org/) seabornis een pakket bouwt voort op matplotlib . Het hoofddoel is standaardgrafieken visueel aantrekkelijker te maken en het maken van gecompliceerde grafieken te vereenvoudigen.

[gplotis ](https://ggplot2.tidyverse.org/) is een pakket dat ook boven op matplotlib is gebouwd . Nochtans is het belangrijkste verschil dat het hulpmiddel een haven van gplot2 voor R is. Net als bij seaborn is het doel om matplotlib beter te krijgen. De gebruikers die met gplot2 voor R vertrouwd zijn zouden deze bibliotheek moeten overwegen.


##### Grafieken gelijktrekken

Univariate grafieken zijn percelen van een individuele variabele. Een uniforme grafiek wordt gebruikt om uw gegevens te visualiseren is de doos en de whiskergrafiek.

Met behulp van onze detailhandelsdataset van voordien, kunnen wij de doos en de whiskerperceel voor elk van 45 winkels en hun wekelijkse verkoop produceren. Het plot wordt geproduceerd gebruikend de functie `seaborn.boxplot`.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Een doos en een whiskerplot worden gebruikt om de verspreiding van gegevens te tonen. De buitenlijnen van het waarnemingspunt tonen de bovenste en onderste kwartiel, terwijl de doos het interkwartielbereik beslaat. De regel in het vak markeert de mediaan. Alle gegevenspunten die meer dan 1,5 keer het bovenste of onderste kwartiel bedragen, worden als een cirkel gemarkeerd. Deze punten worden beschouwd als uitschieters.

##### Meerdere grafieken

Meerdere percelen worden gebruikt om de interactie tussen variabelen te zien. Met de visualisatie kunnen wetenschappers van data zien of er correlaties of patronen zijn tussen de variabelen. Een veelgebruikte multivariate grafiek is een correlatiematrix. Met een correlatiematrix worden de afhankelijkheden tussen meerdere variabelen gekwantificeerd aan de hand van de correlatiecoëfficiënt.

Gebruikend de zelfde kleinhandelsdataset, kunnen wij de correlatiematrix produceren.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Merk op dat 1 diagonaal naar beneden is. Dit toont aan dat wanneer het vergelijken van een variabele aan zich, het volledige positieve correlatie heeft. Sterke positieve correlatie zal een grootte dichter bij 1 hebben, terwijl zwakke correlaties dichter bij 0 liggen. Een negatieve correlatie wordt aangetoond met een negatieve coëfficiënt die een omgekeerde trend laat zien.


## Volgende stappen

In deze zelfstudie wordt uitgelegd hoe u een nieuw Jupyter-notebook maakt in de Data Science Workspace en hoe u toegang krijgt tot externe gegevens en van [!DNL Adobe Experience Platform]. We hebben met name de volgende stappen doorlopen:
- Een nieuwe jupyter-laptop maken
- Gegevensbestanden en schema&#39;s voor toegang
- Gegevenssets verkennen

Nu bent u klaar om naar [volgende sectie ](../models-recipes/package-source-files-recipe.md) te gaan om een recept te verpakken en in de Werkruimte van de Wetenschap van Gegevens te importeren.