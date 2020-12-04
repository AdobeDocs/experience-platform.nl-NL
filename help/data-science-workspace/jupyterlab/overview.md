---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: Gebruikershandleiding voor JupyterLab
topic: Overview
description: JupyterLab is een webgebaseerde gebruikersinterface voor Project Jupyter en is nauw geïntegreerd in Adobe Experience Platform. Het biedt een interactieve ontwikkelomgeving voor gegevenswetenschappers die werken met Jupyter-laptops, -code en -gegevens. Dit document biedt een overzicht van JupyterLab en de bijbehorende functies, evenals instructies voor het uitvoeren van veelvoorkomende handelingen.
translation-type: tm+mt
source-git-commit: d5e7679ac41fd476c77a98920d7f7aeaefacec6d
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 6%

---


# [!DNL JupyterLab] gebruikershandleiding

[!DNL JupyterLab] is een webgebaseerde gebruikersinterface voor [Project Jupyter](https://jupyter.org/) en is nauw geïntegreerd in Adobe Experience Platform. Het biedt een interactieve ontwikkelomgeving voor gegevenswetenschappers die werken met Jupyter-laptops, -code en -gegevens.

Dit document biedt een overzicht van [!DNL JupyterLab] en de bijbehorende functies en instructies voor het uitvoeren van algemene handelingen.

## [!DNL JupyterLab] op [!DNL Experience Platform]

De JupyterLab-integratie van Experience Platform gaat gepaard met architectuurwijzigingen, ontwerpoverwegingen, aangepaste laptopextensies, vooraf geïnstalleerde bibliotheken en een Adobe-interface.

In de volgende lijst worden enkele functies beschreven die uniek zijn voor JupyterLab op Platform:

| Functie | Beschrijving |
| --- | --- |
| **Kernels** | Kernels bieden laptop en andere [!DNL JupyterLab] front-ends de mogelijkheid om code in verschillende programmeertalen uit te voeren en in te voeren. [!DNL Experience Platform] verstrekt extra kernels om ontwikkeling in [!DNL Python], R, PySpark, en [!DNL Spark]. te steunen. Zie de sectie [Korrels](#kernels) voor meer informatie. |
| **Toegang tot gegevens** | Toegang tot bestaande datasets rechtstreeks vanuit [!DNL JupyterLab] de volledige ondersteuning voor lees- en schrijfmogelijkheden. |
| **[!DNL Platform]serviceintegratie** | Dankzij de ingebouwde integratie kunt u rechtstreeks vanuit de toepassing andere [!DNL Platform] services gebruiken [!DNL JupyterLab]. Een volledige lijst van gesteunde integratie wordt verstrekt in de sectie over [Integratie met andere diensten](#service-integration)van de Platform. |
| **Verificatie** | Naast het ingebouwde veiligheidsmodel <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">van</a>JupyterLab, wordt elke interactie tussen uw toepassing en Experience Platform, met inbegrip van de dienst-aan-dienst van het Platform mededeling gecodeerd en voor authentiek verklaard door <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Ontwikkelingsbibliotheken** | In [!DNL Experience Platform], verstrekt [!DNL JupyterLab] vooraf geïnstalleerde bibliotheken voor [!DNL Python], R, en PySpark. Zie de [bijlage](#supported-libraries) voor een volledige lijst met ondersteunde bibliotheken. |
| **Bibliotheekcontroller** | Wanneer de vooraf geïnstalleerde bibliotheken niet aan uw behoeften voldoen, kunnen extra bibliotheken voor Python en R worden geïnstalleerd en tijdelijk in geïsoleerde containers worden opgeslagen om de integriteit van uw gegevens te handhaven [!DNL Platform] en uw gegevens veilig te houden. Zie de sectie [Korrels](#kernels) voor meer informatie. |

>[!NOTE]
>
>Aanvullende bibliotheken zijn alleen beschikbaar voor de sessie waarin ze zijn geïnstalleerd. Wanneer u nieuwe sessies start, moet u alle extra bibliotheken die u nodig hebt opnieuw installeren.

## Integratie met andere [!DNL Platform] services {#service-integration}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform]. De integratie van [!DNL JupyterLab] op [!DNL Platform] als ingebedde winde staat het toe om met andere [!DNL Platform] diensten in wisselwerking te staan, toelatend u om [!DNL Platform] aan zijn volledig potentieel te gebruiken. De volgende [!DNL Platform] services zijn beschikbaar in [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Toegang tot en verken gegevenssets met lees- en schrijffuncties.
* **[!DNL Query Service]:** Toegang tot en verken gegevenssets met SQL, waardoor u lagere gegevenstoegangsoverheadkosten krijgt wanneer u te maken hebt met grote hoeveelheden gegevens.
* **[!DNL Sensei ML Framework]:** Modelontwikkeling met de mogelijkheid om gegevens op te leiden en te scoren, en het maken van recept met één klik.
* **[!DNL Experience Data Model (XDM)]:** Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. [Het Model van Gegevens van de ervaring (XDM)](https://www.adobe.com/go/xdm-home-en), die door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

>[!NOTE]
>
>Sommige [!DNL Platform] de dienstintegratie op [!DNL JupyterLab] zijn beperkt tot specifieke kernels. Raadpleeg de sectie over [korrels](#kernels) voor meer informatie.

## Belangrijke functies en veelvoorkomende bewerkingen

In de volgende secties wordt informatie gegeven over de belangrijkste kenmerken van [!DNL JupyterLab] en instructies voor het uitvoeren van gemeenschappelijke operaties:

* [Access JupyterLab](#access-jupyterlab)
* [JupyterLab-interface](#jupyterlab-interface)
* [Codecellen](#code-cells)
* [Kernels](#kernels)
* [Kernel-sessies](#kernel-sessions)
* [Launcher](#launcher)

### Ga naar [!DNL JupyterLab] {#access-jupyterlab}

Selecteer in [Adobe Experience Platform](https://platform.adobe.com)de optie **Laptops** in de navigatiekolom links. Laat enige tijd over [!DNL JupyterLab] om volledig te initialiseren.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interface {#jupyterlab-interface}

De [!DNL JupyterLab] interface bestaat uit een menubalk, een opvouwbare linkerzijbalk en het hoofdwerkgebied met tabbladen met documenten en activiteiten.

**Menubalk**

De menubalk boven aan de interface heeft menu&#39;s op hoofdniveau die acties beschikbaar maken in [!DNL JupyterLab] de sneltoetsen:

* **Bestand:** Acties in verband met bestanden en mappen
* **Bewerken:** Acties in verband met het bewerken van documenten en andere activiteiten
* **Weergave:** Handelingen die de weergave van [!DNL JupyterLab]
* **Uitvoeren:** Handelingen voor het uitvoeren van code in verschillende activiteiten, zoals notebooks en codeconsoles
* **Kernel:** Handelingen voor het beheren van kernels
* **Tabs:** Een lijst van geopende documenten en activiteiten
* **Instellingen:** Algemene instellingen en een geavanceerde instellingeneditor
* **Help:** Een lijst met Help-koppelingen voor [!DNL JupyterLab] en kernel-koppelingen

**Linkerzijbalk**

De linkerzijbalk bevat klikbare tabbladen die toegang bieden tot de volgende functies:

* **Bestandenbrowser:** Een lijst met opgeslagen laptopdocumenten en -mappen
* **Gegevensverkenner:** Doorblader, toegang, en onderzoek datasets en schema&#39;s
* **Lopende kernels en terminals:** Een lijst van actieve kernel en eindzittingen met de capaciteit om te eindigen
* **Opdrachten:** Een lijst met nuttige opdrachten
* **Celcontrole:** Een celeditor die toegang biedt tot gereedschappen en metagegevens die nuttig zijn voor het instellen van een laptop voor presentatiedoeleinden
* **tabs:** Een lijst met geopende tabbladen

Klik op een tab om de bijbehorende functies weer te geven of klik op een uitgevouwen tab om de linkerzijbalk samen te vouwen, zoals hieronder wordt getoond:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Belangrijkste werkterrein**

In het belangrijkste werkgebied in [!DNL JupyterLab] kunt u documenten en andere activiteiten rangschikken in tabbladen waarvan u de grootte kunt wijzigen of die u kunt onderverdelen. Sleep een tab naar het midden van een deelvenster met tabbladen om de tab te migreren. Verdeel een deelvenster door een tab naar links, rechts, boven of onder in het deelvenster te slepen:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Codecellen {#code-cells}

Codecellen zijn de belangrijkste inhoud van laptops. Ze bevatten broncode in de taal van de bijbehorende kernel van de laptop en de uitvoer als gevolg van het uitvoeren van de codecel. Rechts van elke codecel wordt een aantal uitvoeringen weergegeven die de volgorde van uitvoering ervan aangeven.

![](../images/jupyterlab/user-guide/code_cell.png)

Vaak voorkomende celhandelingen worden hieronder beschreven:

* **Een cel toevoegen:** Klik op het plusteken (**+**) in het notitieboekje om een lege cel toe te voegen. Nieuwe cellen worden onder de cel geplaatst waarmee momenteel wordt gewerkt, of aan het einde van de laptop als geen bepaalde cel de focus heeft.

* **Een cel verplaatsen:** Plaats de cursor rechts van de cel die u wilt verplaatsen, klik en sleep de cel naar een nieuwe locatie. Als u bovendien een cel van het ene notebook naar het andere verplaatst, wordt de cel met de inhoud gerepliceerd.

* **Een cel uitvoeren:** Klik op de hoofdtekst van de cel die u wilt uitvoeren en klik vervolgens op het **afspeelpictogram** (**▶**) in het notitieboekje. Een asterisk (**\***) wordt getoond in de uitvoerteller van de cel wanneer de kernel de uitvoering verwerkt, en wordt vervangen met een geheel na voltooiing.

* **Een cel verwijderen:** Klik op de hoofdtekst van de cel die u wilt verwijderen en klik vervolgens op het **schaarpictogram** .

### Kernels {#kernels}

Notebookkernels zijn de taalspecifieke computerengines voor de verwerking van notebookcellen. Naast [!DNL Python], [!DNL JupyterLab] verleent extra taalsteun in R, PySpark, en [!DNL Spark] (Scala). Wanneer u een notitieboekjectdocument opent, wordt de bijbehorende kernel gestart. Wanneer een laptopcel wordt uitgevoerd, voert de kernel de berekening uit en levert dit resultaten op die aanzienlijke CPU- en geheugenbronnen verbruiken. Let op: toegewezen geheugen wordt pas vrijgegeven wanneer de kernel wordt afgesloten.

Bepaalde kenmerken en functies zijn beperkt tot bepaalde kernels zoals beschreven in de onderstaande tabel:

| Kernel | Ondersteuning voor bibliotheekinstallatie | [!DNL Platform] integratie |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Nee | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Kernel-sessies {#kernel-sessions}

Elke actieve laptop of activiteit op [!DNL JupyterLab] gebruikt een kernel-sessie. Alle actieve sessies kunt u vinden door het tabblad **Doorlopende terminals en kernels** vanuit de linkerzijbalk uit te vouwen. Het type en de toestand van de kernel voor een laptop kunnen worden geïdentificeerd door de laptop rechtsboven te volgen. In het onderstaande diagram is de bijbehorende kernel van de laptop **[!DNL Python]3** en de huidige toestand wordt weergegeven door een grijze cirkel naar rechts. Een holle cirkel impliceert een nutteloze kernel en een stevige cirkel impliceert een bezige kernel.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Als de kernel gedurende langere tijd wordt afgesloten of inactief is, dan **Geen Kernel!** met een effen cirkel. Activeer een kernel door op de kernel-status te klikken en het juiste kernel-type te selecteren, zoals hieronder wordt getoond:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Launcher {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

De aangepaste *Launcher* biedt u nuttige laptopsjablonen voor hun ondersteunde kernels om u te helpen uw taak snel te starten, zoals:

| Sjabloon | Beschrijving |
| --- | --- |
| Leeg | Een leeg laptopbestand. |
| Starter | Een voorgevulde laptop die de gegevensexploratie aantoont met behulp van voorbeeldgegevens. |
| Detailhandel | Een voorgevulde laptop met het recept [voor de](https://adobe.ly/2wOgO3L) detailhandel aan de hand van voorbeeldgegevens. |
| Recipe Builder | Een laptopsjabloon voor het maken van een recept in [!DNL JupyterLab]. De voorgevulde code en opmerkingen tonen en beschrijven het proces voor het maken van recept. Raadpleeg de [zelfstudie](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) over het recept voor een gedetailleerde analyse. |
| [!DNL Query Service] | Een voorgevulde laptop die het gebruik aantoont van [!DNL Query Service] rechtstreeks in [!DNL JupyterLab] de meegeleverde workflows met voorbeelden die gegevens op schaal analyseren. |
| XDM-gebeurtenissen | Een voorgevulde laptop waarin de gegevensverkenning op postvalue Experience-gebeurtenisgegevens wordt gedemonstreerd, waarbij de nadruk ligt op functies die gemeenschappelijk zijn in de gegevensstructuur. |
| XDM-query&#39;s | Een voorgevulde laptop met voorbeelden van zakelijke vragen over Experience Event-gegevens. |
| Samenvoeging | Een voorgevulde laptop met voorbeelden van workflows om grote hoeveelheden gegevens samen te voegen tot kleinere, beheerbare blokken. |
| Clustering | Een voorgevulde laptop die het end-to-end computerleermodelleringsproces aantoont met behulp van clusteringsalgoritmen. |

Sommige laptopsjablonen zijn beperkt tot bepaalde kernels. De beschikbaarheid van het malplaatje voor elke pit wordt in de volgende lijst in kaart gebracht:

<table>
    <tr>
        <td></td>
        <th><strong>Leeg</strong></th>
        <th><strong>Starter</strong></th>
        <th><strong>Detailhandel</strong></th>
        <th><strong>Recipe Builder</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>XDM-gebeurtenissen</strong></th>
        <th><strong>XDM-query's</strong></th>
        <th><strong>Samenvoeging</strong></th>
        <th><strong>Clustering</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >nee</td>
        <td >nee</td>
        <td >nee</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >nee</td>
        <td >nee</td>
        <td >nee</td>
        <td >nee</td>
        <td >nee</td>
        <td >nee</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
        <td >nee</td>
        <td >ja</td>
        <td >nee</td>
        <td >no</td>
        <td >nee</td>
        <td >nee</td>
        <td >ja</td>
        <td >ja</td>
        <td >nee</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >ja</td>
        <td >ja</td>
        <td >nee</td>
        <td >nee</td>
        <td >nee</td>
        <td >nee</td>
        <td >nee</td>
        <td >nee</td>
        <td >ja</td>
    </tr>
</table>

Als u een nieuwe *Launcher* wilt openen, klikt u op **Bestand > Nieuwe startpagina**. U kunt ook de **bestandsbrowser** uitvouwen vanuit de linkerzijbalk en op het plusteken klikken (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

### GPU- en geheugenserverconfiguratie in [!DNL Python]/R

Selecteer in de [!DNL JupyterLab] rechterbovenhoek het tandwielpictogram om de configuratie *van de* notebookserver te openen. Met de schuifregelaar kunt u de GPU in- en uitschakelen en de benodigde hoeveelheid geheugen toewijzen. De hoeveelheid geheugen die u kunt toewijzen, is afhankelijk van de hoeveelheid geheugen die uw organisatie heeft ingericht. Selecteer Configs **[!UICONTROL bijwerken]** om op te slaan.

>[!NOTE]
>
>Per organisatie is slechts één GPU beschikbaar voor laptops. Als de GPU in gebruik is, moet u wachten op de gebruiker die momenteel de GPU heeft gereserveerd om deze vrij te geven. Dit kan worden gedaan door uit te loggen of GPU in een nutteloze staat voor vier of meer uren te verlaten.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Volgende stappen

Ga voor meer informatie over elk van de ondersteunde laptops en hoe u deze kunt gebruiken naar de [Jupyterlab-handleiding voor gegevenstoegang tot](./access-notebook-data.md) ontwikkelaars van laptops. In deze handleiding wordt vooral uitgelegd hoe u JupyterLab-laptops kunt gebruiken om toegang te krijgen tot uw gegevens, zoals lezen, schrijven en vragen om gegevens. De gids voor gegevenstoegang bevat ook informatie over de maximale hoeveelheid gegevens die kan worden gelezen door elke ondersteunde laptop.

## Ondersteunde bibliotheken {#supported-libraries}

### [!DNL Python] / R

| Bibliotheek | Versie |
| :------ | :------ |
| notebook | 6.0.0 |
| verzoeken | 2.22.0 |
| plots | 4.0.0 |
| folium | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokee | 1.3.1 |
| gensim | 3.7.3 |
| ipyparallel | 0.5.2 |
| jq | 1.6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| pandas | 0.22.0 |
| pandasql | 0.7.3 |
| kussen | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| slordig | 1.3.0 |
| slordig | 1.3.0 |
| seaborn | 0.9.0 |
| statsmodellen | 0.10.1 |
| elastisch | 5.1.0.17 |
| gumpje | 0.11.5 |
| py-xgboost | 0.90 |
| opencv | 3.4.1 |
| pyspark | 2.4.3 |
| pytorch | 1.0.1 |
| wxpython | 4.0.6 |
| kleurovergang | 0.3.0 |
| geopanda | 0.5.1 |
| peper | 2.1.0 |
| vormig | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentiële | 3.6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| rggthemes | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| r-leaps | 3.0 |
| r-manipuleert | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-overleving | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| r-prognose | 8.7 |
| r-rsolnp | 1.16 |
| herticuleren | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corplot | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-randomforest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pymongo | 3.8.0 |
| pijltje | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| fastparket | 0.3.2 |
| python-snappy | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| woordwolk | 1.5.0 |
| grafiet | 2.40.1 |
| python-graphviz | 0.11.1 |
| azuuropslag | 0.36.0 |
| [!DNL jupyterlab] | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| molen | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| neus | 1.3.7 |
| autovizwidget | 0.12.9 |
| altair | 3.1.0 |
| vega_datasets | 0.7.0 |
| papiermolen | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimporter | 0.3.1 |

### PySpark

| Bibliotheek | Versie |
| :------ | :------ |
| verzoeken | 2.18.4 |
| gensim | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| pandas | 0.20.1 |
| pandasql | 0.7.3 |
| kussen | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| slordig | 0.19.1 |
| slordig | 1.3.3 |
| statsmodellen | 0.8.0 |
| elastisch | 4.0.30.44 |
| py-xgboost | 0.60 |
| opencv | 3.1.0 |
| pijltje | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |