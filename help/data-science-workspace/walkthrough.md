---
keywords: Experience Platform;analyse;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen
solution: Experience Platform
title: Analyse van werkruimte voor gegevenswetenschap
topic: Walkthrough
description: Dit document biedt een analyse voor de Adobe Experience Platform Data Science Workspace. Specifiek de algemene werkstroom zou een gegevenswetenschapper een probleem oplossen gebruikend machine het leren.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 0%

---


# [!DNL Data Science Workspace] wandelpad

Dit document biedt een doorhaling voor Adobe Experience Platform [!DNL Data Science Workspace]. Deze zelfstudie schetst een algemene werkstroom van gegevenswetenschappers en hoe ze een probleem kunnen benaderen en oplossen met behulp van computerleren.

## Vereisten

- Een geregistreerde Adobe ID-account
   - De Adobe ID-account moet zijn toegevoegd aan een organisatie met toegang tot Adobe Experience Platform en [!DNL Data Science Workspace].

## Handelsversie

Een detailhandelaar staat voor vele uitdagingen om concurrerend te blijven op de huidige markt. Een van de belangrijkste punten van zorg van de detailhandelaar is het bepalen van de optimale prijsstelling van een product en het voorspellen van verkooptrends. Met een accuraat voorspellingsmodel zou een detailhandelaar de relatie tussen vraag en prijsbeleid kunnen vinden en geoptimaliseerde prijsbeslissingen kunnen nemen om verkoop en inkomsten te maximaliseren.

## Oplossing van de wetenschapper

De oplossing van een wetenschapper op het gebied van gegevens is gebruik te maken van de rijkdom aan historische informatie die door een detailhandelaar wordt verstrekt, toekomstige trends te voorspellen en prijsbeslissingen te optimaliseren. Deze analyse gebruikt vroegere verkoopgegevens om een machine het leren model op te leiden en gebruikt het model om toekomstige verkooptendensen te voorspellen. Met dit, kunt u inzichten produceren helpen optimale prijsveranderingen aanbrengen.

Dit overzicht weerspiegelt de stappen die een gegevenswetenschapper zou doorlopen om een dataset te nemen en een model te creëren om wekelijkse verkoop te voorspellen. Deze zelfstudie behandelt de volgende secties in het voorbeeldnotebook voor detailhandel op Adobe Experience Platform [!DNL Data Science Workspace]:

- [Instellen](#setup)
- [Gegevens verkennen](#exploring-data)
- [Functietechniek](#feature-engineering)
- [Training en verificatie](#training-and-verification)

### Laptops in [!DNL Data Science Workspace]

Selecteer **[!UICONTROL Laptops]** in de gebruikersinterface van Adobe Experience Platform op het tabblad **[!UICONTROL Gegevenswetenschap]** om naar de overzichtspagina [!UICONTROL Laptops] te gaan. Selecteer op deze pagina het tabblad [!DNL JupyterLab] om de [!DNL JupyterLab]-omgeving te starten. De standaardlandingspagina voor [!DNL JupyterLab] is **[!UICONTROL Launcher]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

In deze zelfstudie wordt [!DNL Python] 3 in [!DNL JupyterLab Notebooks] gebruikt om te tonen hoe u de gegevens kunt openen en verkennen. Op de pagina Launcher staan voorbeelden van laptops. De voorbeeldlaptop **[!UICONTROL Retail Sales]** wordt gebruikt in de onderstaande voorbeelden.

### {#setup} instellen

Als de Retail Sales-laptop is geopend, moet u eerst de bibliotheken laden die nodig zijn voor uw workflow. De volgende lijst bevat een korte beschrijving van alle bibliotheken die in de voorbeelden in latere stappen worden gebruikt.

- **getal**: Wetenschappelijke computerbibliotheek die ondersteuning biedt voor grote, multidimensionale arrays en matrixen
- **pandas**: Bibliotheek die gegevensstructuren en verrichtingen aanbiedt die voor gegevensmanipulatie en analyse worden gebruikt
- **matplotlib.pyplot**: Bibliotheek plaatsen die een MATLAB-achtige ervaring biedt bij het tekenen
- **afgebroken** : De bibliotheek van de interfacegegevensvisualisatie op hoog niveau die op matplotlib wordt gebaseerd
- **klearn**: Machine Learning-bibliotheek met classificatie, regressie, ondersteuning voor vector- en clusteralgoritmen
- **waarschuwingen**: Bibliotheek die waarschuwingsberichten beheert

### Gegevens {#exploring-data} verkennen

#### Gegevens laden

Nadat de bibliotheken zijn geladen, kunt u de gegevens bekijken. De volgende [!DNL Python]-code gebruikt pandas&#39; `DataFrame`-gegevensstructuur en de functie [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) om de CSV te lezen die op [!DNL Github] wordt gehost in het DataFrame van pandas:

![](./images/walkthrough/read_csv.png)

De gegevensstructuur van Pandas&#39; DataFrame is een tweedimensionale gelabelde gegevensstructuur. Als u de afmetingen van uw gegevens snel wilt zien, kunt u `df.shape` gebruiken. Dit keert een tegel terug die de dimensionaliteit van DataFrame vertegenwoordigt:

![](./images/walkthrough/df_shape.png)

Tot slot kunt u een voorvertoning weergeven van hoe uw gegevens eruitzien. U kunt `df.head(n)` gebruiken om de eerste `n` rijen van DataFrame te bekijken:

![](./images/walkthrough/df_head.png)

#### Statistisch overzicht

We kunnen de pandabibliotheek [!DNL Python's] gebruiken om het gegevenstype van elk kenmerk op te halen. De output van de volgende vraag zal ons informatie over het aantal ingangen en het gegevenstype voor elk van de kolommen geven:

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Deze informatie is nuttig aangezien het weten van het gegevenstype voor elke kolom ons zal toelaten om te weten hoe te om de gegevens te behandelen.

Laten we nu eens kijken naar de statistische samenvatting. Alleen de numerieke gegevenstypen worden weergegeven als `date`, `storeType` en `isHoliday` worden niet uitgevoerd:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Hier zie je 6435 varianten voor elk kenmerk. Daarnaast worden statistische informatie zoals gemiddelde, standaardafwijking (std), min, max en interkwartielen gegeven. Dit geeft ons informatie over de afwijking voor de gegevens. In de volgende sectie gaat u over visualisatie die samen met deze informatie werkt om ons een volledig inzicht in uw gegevens te geven.

Wanneer u de minimum- en maximumwaarden voor `store` bekijkt, ziet u dat er 45 unieke opslagruimten zijn waarin de gegevens staan. Er zijn ook `storeTypes` die onderscheiden wat een opslag is. U kunt de distributie van `storeTypes` door het volgende zien:

![](./images/walkthrough/df_groupby.png)

Dit betekent dat 22 opslagruimten van `storeType A` zijn, 17 `storeType B` zijn, en 6 zijn `storeType C`.

#### Gegevens visualiseren

Nu u de gegevenskaderwaarden kent, wilt u dit met visualisaties aanvullen om dingen helderder en gemakkelijker te maken om patronen te identificeren. Deze grafieken zijn ook handig wanneer u resultaten naar een publiek stuurt.

#### Grafieken gelijktrekken

Univariate grafieken zijn percelen van een individuele variabele. Een uniforme grafiek die wordt gebruikt om uw gegevens te visualiseren is box en whiskerpercelen.

Gebruikend uw detailhandelsdataset van voordien, kunt u de doos en de whiskerplot voor elk van de 45 opslag en hun wekelijkse verkoop produceren. Het plot wordt geproduceerd gebruikend de functie `seaborn.boxplot`.

![](./images/walkthrough/box_whisker.png)

Een doos en een whiskerplot worden gebruikt om de verspreiding van gegevens te tonen. De buitenlijnen van het waarnemingspunt tonen de bovenste en onderste kwartiel, terwijl de doos het interkwartielbereik beslaat. De regel in het vak markeert de mediaan. Alle gegevenspunten die meer dan 1,5 keer het bovenste of onderste kwartiel bedragen, worden als een cirkel gemarkeerd. Deze punten worden beschouwd als uitschieters.

Vervolgens kunt u de wekelijkse verkoop met de tijd uitzetten. U zult slechts de output van de eerste opslag tonen. De code in de laptop genereert 6 percelen die overeenkomen met 6 van de 45 winkels in onze dataset.

![](./images/walkthrough/weekly_sales.png)

Met dit diagram kunt u de wekelijkse verkoop over een periode van 2 jaar vergelijken. Het is gemakkelijk om verkooppieken en dalpatronen in tijd te zien.

#### Meerdere grafieken

Meerdere percelen worden gebruikt om de interactie tussen variabelen te zien. Met de visualisatie kunnen wetenschappers van data zien of er correlaties of patronen zijn tussen de variabelen. Een veelgebruikte multivariate grafiek is een correlatiematrix. Met een correlatiematrix worden de afhankelijkheden tussen meerdere variabelen gekwantificeerd aan de hand van de correlatiecoëfficiënt.

Gebruikend de zelfde kleinhandelsdataset, kunt u de correlatiematrix produceren.

![](./images/walkthrough/correlation_1.png)

Let op de diagonaal van de diagonalen in het midden. Dit toont aan dat wanneer het vergelijken van een variabele aan zich, het volledige positieve correlatie heeft. Sterke positieve correlatie zal een grootte dichter bij 1 hebben, terwijl zwakke correlaties dichter bij 0 liggen. Een negatieve correlatie wordt aangetoond met een negatieve coëfficiënt die een omgekeerde trend laat zien.

### Functietechniek {#feature-engineering}

In deze sectie, wordt de eigenschaptechniek gebruikt om wijzigingen in uw Retaildataset door de volgende verrichtingen uit te voeren te maken:

- Week- en jaarkolommen toevoegen
- StoreType omzetten in een indicatorvariabele
- IsHoliday omzetten in een numerieke variabele
- wekelijkseVerkoop van volgende week voorspellen

#### Week- en jaarkolommen toevoegen

De huidige notatie voor datum (`2010-02-05`) kan het moeilijk maken om te onderscheiden dat de gegevens voor elke week zijn. Daarom dient u de datum om te zetten in week en jaar.

![](./images/walkthrough/date_to_week_year.png)

Nu zijn de week en de datum als volgt:

![](./images/walkthrough/date_week_year.png)

#### StoreType omzetten in indicatorvariabele

Daarna, wilt u de storeType kolom in kolommen omzetten die elk `storeType` vertegenwoordigen. Er zijn 3 opslagtypes, (`A`, `B`, `C`), waarvan u 3 nieuwe kolommen creeert. De waarde die in elke eigenschap wordt ingesteld, is een booleaanse waarde waarbij &#39;1&#39; is ingesteld, afhankelijk van wat de `storeType` was en `0` voor de andere twee kolommen.

![](./images/walkthrough/storeType.png)

De huidige `storeType` kolom wordt gelaten vallen.

#### IsHoliday omzetten in numeriek type

De volgende wijziging bestaat uit het wijzigen van de booleaanse waarde `isHoliday` in een numerieke weergave.

![](./images/walkthrough/isHoliday.png)

#### wekelijkseVerkoop van volgende week voorspellen

Nu wilt u vorige en toekomstige wekelijkse verkoop aan elk van uw datasets toevoegen. U kunt dit doen door uw `weeklySales` te compenseren. Daarnaast wordt het verschil `weeklySales` berekend. Dit wordt gedaan door `weeklySales` met `weeklySales` van vorige week af te trekken.

![](./images/walkthrough/weekly_past_future.png)

Aangezien u `weeklySales` gegevens 45 datasets door:sturen en 45 datasets achterwaarts compenseert om nieuwe kolommen tot stand te brengen, hebben de eerste en laatste 45 gegevenspunten waarden NaN. U kunt deze punten uit uw dataset verwijderen door de `df.dropna()` functie te gebruiken die alle rijen verwijdert die waarden NaN hebben.

![](./images/walkthrough/dropna.png)

Een samenvatting van de dataset nadat uw wijzigingen hieronder wordt getoond:

![](./images/walkthrough/df_info_new.png)

### Training en verificatie {#training-and-verification}

Nu is het tijd om een aantal modellen van de gegevens te maken en te selecteren welk model de best presterende is voor het voorspellen van toekomstige verkopen. U evalueert de volgende vijf algoritmen:

- Lineaire regressie
- Beslissingsboom
- Willekeurig bos
- Verloop verhogen
- K-buren

#### Gegevensset splitsen naar subsets voor training en tests

U hebt een manier nodig om te weten hoe nauwkeurig uw model waarden kan voorspellen. Deze evaluatie kan worden uitgevoerd door een deel van de gegevensset toe te wijzen aan gebruik als validatie en de rest als trainingsgegevens. Aangezien `weeklySalesAhead` de daadwerkelijke toekomstige waarden van `weeklySales` is, kunt u dit gebruiken om te evalueren hoe nauwkeurig het model in het voorspellen van de waarde is. De splitsing vindt hieronder plaats:

![](./images/walkthrough/split_data.png)

U hebt nu `X_train` en `y_train` voor het voorbereiden van de modellen en `X_test` en `y_test` voor evaluatie later.

#### Spotcontrolealgoritmen

In deze sectie declareert u alle algoritmen in een array met de naam `model`. Vervolgens doorloopt u deze array en voert u voor elk algoritme uw trainingsgegevens in met `model.fit()` dat een model `mdl` maakt. Met dit model kunt u `weeklySalesAhead` voorspellen met uw `X_test` gegevens.

![](./images/walkthrough/training_scoring.png)

Voor het scoren gebruikt u het gemiddelde percentageverschil tussen de voorspelde `weeklySalesAhead` en de werkelijke waarden in de `y_test` gegevens. Aangezien u het verschil tussen uw voorspelling en het daadwerkelijke resultaat wilt minimaliseren, is de het best presterende model dat van de Verhoging van Regressor het.

#### Voorspellingen visualiseren

Tot slot visualiseert u uw voorspellingsmodel met de daadwerkelijke wekelijkse verkoopwaarden. De blauwe lijn geeft de werkelijke getallen aan, terwijl de groene lijn uw voorspelling vertegenwoordigt met Verloop verhogen. De volgende code produceert 6 percelen die 6 van de 45 opslag in uw dataset vertegenwoordigen. Alleen `Store 1` wordt hier weergegeven:

![](./images/walkthrough/visualize_prediction.png)

## Volgende stappen

In dit document wordt een algemene workflow voor gegevenswetenschappers besproken om een probleem met de detailhandel op te lossen. Samenvatten:

- Laad de bibliotheken die nodig zijn voor de workflow.
- Nadat de bibliotheken zijn geladen, kunt u de gegevens bekijken met statistische overzichten, visualisaties en grafieken.
- Daarna, wordt de eigenschaptechniek gebruikt om wijzigingen in uw detailhandelsdataset te maken.
- Ten slotte maakt u modellen van de gegevens en selecteert u het model dat de beste prestaties levert voor het voorspellen van toekomstige verkopen.

Als u klaar bent, leest u eerst de [JupyterLab-gebruikershandleiding](./jupyterlab/overview.md) voor een kort overzicht van laptops in de Adobe Experience Platform Data Science Workspace. Bovendien, als u in het leren over Modellen en Ontvangt geinteresseerd bent, begin door het [kleinhandelsverkoopschema en dataset](./models-recipes/create-retails-sales-dataset.md) leerprogramma te lezen. Deze zelfstudie bereidt u voor op volgende zelfstudies voor de werkruimte voor wetenschap van gegevens die kunnen worden weergegeven in de werkruimte voor wetenschap van gegevens [zelfstudies op pagina](../tutorials/data-science-workspace.md).