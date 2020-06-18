---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Gebruikershandleiding voor JupyterLab
topic: Overview
translation-type: tm+mt
source-git-commit: 49f0678cf8bf4349d0b63f3525a1f707f725ede9
workflow-type: tm+mt
source-wordcount: '3782'
ht-degree: 9%

---


# Gebruikershandleiding voor JupyterLab

JupyterLab is een webgebaseerde gebruikersinterface voor <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> en is nauw geïntegreerd in [!DNL Adobe Experience Platform]. Het biedt een interactieve ontwikkelomgeving voor gegevenswetenschappers die werken met Jupyter-laptops, -code en -gegevens.

Dit document biedt een overzicht van JupyterLab en de bijbehorende functies, evenals instructies om algemene handelingen uit te voeren.

## JupyterLab op Experience Platform

De JupyterLab-integratie van Experience Platform gaat gepaard met architectuurwijzigingen, ontwerpoverwegingen, aangepaste laptopextensies, vooraf geïnstalleerde bibliotheken en een Adobe-interface.

In de volgende lijst worden enkele functies beschreven die uniek zijn voor JupyterLab op Platform:

| Functie | Beschrijving |
| --- | --- |
| **Kernels** | Kernels bieden laptop en andere voorkant van JupyterLab de mogelijkheid om code in verschillende programmeertalen uit te voeren en in te voeren. Experience Platform verstrekt extra kernels om ontwikkeling in Python, R, PySpark, en Vonk te steunen. Zie de sectie [Korrels](#kernels) voor meer informatie. |
| **Toegang tot gegevens** | Toegang tot bestaande datasets rechtstreeks vanuit JupyterLab met volledige ondersteuning voor lees- en schrijfmogelijkheden. |
| **Integratie van Platform-services** | Dankzij de ingebouwde integratie kunt u rechtstreeks vanuit JupyterLab andere services voor Platforms gebruiken. Een volledige lijst van gesteunde integratie wordt verstrekt in de sectie over [Integratie met andere diensten](#service-integration)van de Platform. |
| **Verificatie** | Naast het ingebouwde veiligheidsmodel <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">van</a>JupyterLab, wordt elke interactie tussen uw toepassing en Experience Platform, met inbegrip van de dienst-aan-dienst van het Platform mededeling gecodeerd en voor authentiek verklaard door <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Ontwikkelingsbibliotheken** | In Experience Platform biedt JupyterLab vooraf geïnstalleerde bibliotheken voor Python, R en PySpark. Zie de [bijlage](#supported-libraries) voor een volledige lijst met ondersteunde bibliotheken. |
| **Bibliotheekcontroller** | Wanneer de vooraf geïnstalleerde bibliotheken niet geschikt zijn voor uw behoeften, kunnen extra bibliotheken voor Python en R worden geïnstalleerd en tijdelijk in geïsoleerde containers worden opgeslagen om de integriteit van het Platform te handhaven en uw gegevens veilig te houden. Zie de sectie [Korrels](#kernels) voor meer informatie. |

>[!NOTE] Aanvullende bibliotheken zijn alleen beschikbaar voor de sessie waarin ze zijn geïnstalleerd. Wanneer u nieuwe sessies start, moet u alle extra bibliotheken die u nodig hebt opnieuw installeren.

## Integratie met andere diensten van de Platform {#service-integration}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform]. De integratie van JupyterLab op [!DNL Platform] als ingebedde winde staat het toe om met andere [!DNL Platform] diensten in wisselwerking te staan, toelatend u om aan zijn volledig potentieel [!DNL Platform] te gebruiken. De volgende [!DNL Platform] services zijn beschikbaar in JupyterLab:

* **Catalogusservice:** Toegang tot en verken gegevenssets met lees- en schrijffuncties.
* **Query-service:** Toegang tot en verken gegevenssets met SQL, waardoor u lagere gegevenstoegangsoverheadkosten krijgt wanneer u met grote hoeveelheden gegevens werkt.
* **Sensei ML Framework:** Modelontwikkeling met de mogelijkheid om gegevens op te leiden en te scoren, en het maken van recept met één klik.
* **Experience Data Model (XDM):** Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter het Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), aangestuurd door Adobe, is een poging om de gegevens van de klantervaring te standaardiseren en schema&#39;s voor het beheer van de klantervaring te definiëren.

>[!NOTE] Sommige [!DNL Platform] service-integratie op JupyterLab is beperkt tot specifieke kernels. Raadpleeg de sectie over [korrels](#kernels) voor meer informatie.

## Belangrijke functies en veelvoorkomende bewerkingen

In de volgende secties wordt informatie gegeven over de belangrijkste kenmerken van JupyterLab en instructies voor het uitvoeren van veelvoorkomende bewerkingen:

* [Access JupyterLab](#access-jupyterlab)
* [JupyterLab-interface](#jupyterlab-interface)
* [Codecellen](#code-cells)
* [Kernels](#kernels)
* [Kernel-sessies](#kernel-sessions)
* [PySpark/Spark-uitvoeringsbron](#execution-resource)
* [Launcher](#launcher)

### Access JupyterLab {#access-jupyterlab}

In [Adobe Experience Platform](https://platform.adobe.com), uitgezochte **Notities** van de linkernavigatiekolom. Laat JupyterLab enige tijd volledig initialiseren.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### JupyterLab-interface {#jupyterlab-interface}

De interface JupyterLab bestaat uit een menubalk, een opvouwbare linkerzijbalk en het hoofdwerkgebied met tabbladen met documenten en activiteiten.

**Menubalk**

De menubalk boven aan de interface heeft menu&#39;s op hoofdniveau die acties beschikbaar in JupyterLab met hun toetsenbordkortere weg blootstellen:

* **Bestand:** Acties in verband met bestanden en mappen
* **Bewerken:** Acties in verband met het bewerken van documenten en andere activiteiten
* **Weergave:** Handelingen die de weergave van JupyterLab wijzigen
* **Uitvoeren:** Handelingen voor het uitvoeren van code in verschillende activiteiten, zoals notebooks en codeconsoles
* **Kernel:** Handelingen voor het beheren van kernels
* **Tabs:** Een lijst van geopende documenten en activiteiten
* **Instellingen:** Algemene instellingen en een geavanceerde instellingeneditor
* **Help:** Een lijst met JupyterLab- en kernel Help-koppelingen

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

Met het hoofdwerkgebied in JupyterLab kunt u documenten en andere activiteiten rangschikken in tabbladen waarvan u de grootte kunt wijzigen of waarin u de documenten kunt onderverdelen. Sleep een tab naar het midden van een deelvenster met tabbladen om de tab te migreren. Verdeel een deelvenster door een tab naar links, rechts, boven of onder in het deelvenster te slepen:

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

Notebookkernels zijn de taalspecifieke computerengines voor de verwerking van notebookcellen. Naast Python biedt JupyterLab extra taalondersteuning in R, PySpark en Spark (Scala). Wanneer u een notitieboekjectdocument opent, wordt de bijbehorende kernel gestart. Wanneer een laptopcel wordt uitgevoerd, voert de kernel de berekening uit en levert dit resultaten op die aanzienlijke CPU- en geheugenbronnen verbruiken. Let op: toegewezen geheugen wordt pas vrijgegeven wanneer de kernel wordt afgesloten.

Bepaalde kenmerken en functies zijn beperkt tot bepaalde kernels zoals beschreven in de onderstaande tabel:

| Kernel | Ondersteuning voor bibliotheekinstallatie | Integratie van Platforms |
| :----: | :--------------------------: | :-------------------- |
| **Python** | Ja | <ul><li>Sensei ML Framework</li><li>Catalogusservice</li><li>Query-service</li></ul> |
| **R** | Ja | <ul><li>Sensei ML Framework</li><li>Catalogusservice</li></ul> |
| **Scala** | Nee | <ul><li>Sensei ML Framework</li><li>Catalogusservice</li></ul> |

### Kernel-sessies {#kernel-sessions}

Elke actieve laptop of activiteit op JupyterLab maakt gebruik van een kernel-sessie. Alle actieve sessies kunt u vinden door het tabblad **Doorlopende terminals en kernels** vanuit de linkerzijbalk uit te vouwen. Het type en de toestand van de kernel voor een laptop kunnen worden geïdentificeerd door de laptop rechtsboven te volgen. In het onderstaande diagram is de bijbehorende kernel van de laptop **Python 3** en de huidige toestand wordt weergegeven door een grijze cirkel naar rechts. Een holle cirkel impliceert een nutteloze kernel en een stevige cirkel impliceert een bezige kernel.

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
| Detailhandel | Een voorgevulde laptop met de <a href="https://adobe.ly/2wOgO3L" target="_blank">Retail Sales Recipe</a> met voorbeeldgegevens. |
| Recipe Builder | Een laptopsjabloon voor het maken van een recept in JupyterLab. De voorgevulde code en opmerkingen tonen en beschrijven het proces voor het maken van recept. Raadpleeg de <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">zelfstudie</a> over het recept voor een gedetailleerde analyse. |
| Query-service | Een voorgevulde laptop die het gebruik van Query Service rechtstreeks in JupyterLab aantoont met voorbeeldworkflows die gegevens op schaal analyseren. |
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
        <th><strong>Query-service</strong></th>
        <th><strong>XDM-gebeurtenissen</strong></th>
        <th><strong>XDM-query's</strong></th>
        <th><strong>Samenvoeging</strong></th>
        <th><strong>Clustering</strong></th>
    </tr>
    <tr>
        <th><strong>Python</strong></th>
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
        <th  ><strong>PySpark 3 (Spark 2.4)</strong></th>
        <td >nee</td>
        <td >ja</td>
        <td >nee</td>
        <td >nee</td>
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

### GPU- en geheugenserverconfiguratie in Python/R

Selecteer in de [!DNL JupyterLab] rechterbovenhoek het tandwielpictogram om de configuratie *van de* notebookserver te openen. Met de schuifregelaar kunt u de GPU in- en uitschakelen en de benodigde hoeveelheid geheugen toewijzen. De hoeveelheid geheugen die u kunt toewijzen, is afhankelijk van de hoeveelheid geheugen die uw organisatie heeft ingericht. Selecteer Configs **[!UICONTROL bijwerken]** om op te slaan.

>[!NOTE]
>Per organisatie is slechts één GPU beschikbaar voor laptops. Als de GPU in gebruik is, moet u wachten op de gebruiker die momenteel de GPU heeft gereserveerd om deze vrij te geven. Dit kan worden gedaan door uit te loggen of GPU in een nutteloze staat voor vier of meer uren te verlaten.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Toegang tot Platform-gegevens met laptops

Elke ondersteunde kernel biedt ingebouwde functies waarmee u gegevens van een Platform in een notitieboekje kunt lezen. De ondersteuning voor pagineringsgegevens is echter beperkt tot Python- en R-laptops.

### Gegevenslimieten voor laptops

De volgende informatie definieert de maximale hoeveelheid gegevens die kan worden gelezen, het type gegevens dat is gebruikt en het geschatte tijdsbestek waarin de gegevens worden gelezen. Voor Python en R werd een notebookserver met een RAM van 40 GB gebruikt voor de benchmarks. Voor PySpark en Scala, werd een gegevensbestandcluster gevormd bij 64GB RAM, 8 kernen, 2 DBU met een maximum van 4 arbeiders gebruikt voor de hieronder vermelde benchmarks.

De gegevens in het ExperienceEvent-schema die werden gebruikt, varieerden van 100 (1K) rijen die oplopen tot 1 miljard (1B) rijen. Merk op dat voor de metriek PySpark en van de Vonk, een datumspanwijdte van 10 dagen werd gebruikt voor de gegevens XDM.

De ad-hocschemagegevens zijn vooraf verwerkt gebruikend de Dienst van de Vraag leidt Lijst zoals Uitgezochte (CTAS). Deze gegevens varieerden ook in grootte die van duizend (1K) rijen die zich tot één miljard (1B) rijen uitstrekten.

#### Gegevenslimieten Python-laptop

**XDM ExperienceEvent-schema:** U moet maximaal 2 miljoen rijen (~6.1 GB gegevens op schijf) XDM-gegevens in minder dan 22 minuten kunnen lezen. Als u extra rijen toevoegt, kunnen er fouten optreden.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Grootte op schijf (MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (in seconden) | 20.3 | 86.8 | 63 | 659 | 1315 |

**ad-hocschema:** U moet maximaal 5 miljoen rijen (~5,6 GB gegevens op schijf) niet-XDM (ad-hocgegevens) in minder dan 14 minuten kunnen lezen. Als u extra rijen toevoegt, kunnen er fouten optreden.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Grootte op schijf (in MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in seconden) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### R-laptopgegevenslimieten

**XDM ExperienceEvent-schema:** U moet maximaal 1 miljoen rijen XDM-gegevens (3 GB gegevens op schijf) kunnen lezen in minder dan 13 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Grootte op schijf (MB) | 18.73 | 187.5 | 308 | 3000 |
| R Kernel (in seconden) | 14.03 | 69.6 | 86.8 | 775 |

**ad-hocschema:** U moet maximaal 3 miljoen rijen ad-hocgegevens (293 MB gegevens op schijf) kunnen lezen in ongeveer 10 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Grootte op schijf (in MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK (in sec) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### PySpark-laptopgegevenslimieten (Python kernel):

**XDM ExperienceEvent-schema:** In de interactieve modus kunt u maximaal 5 miljoen rijen (~13,42 GB gegevens op schijf) XDM-gegevens lezen in ongeveer 20 minuten. De interactieve wijze steunt slechts tot 5 miljoen rijen. Als u wenst om grotere datasets te lezen, wordt het geadviseerd u op de wijze van de Partij over te schakelen. In de Batchmodus kunt u maximaal 500 miljoen rijen (~1,31 TB gegevens op schijf) met XDM-gegevens lezen in ongeveer 14 uur.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Grootte op schijf | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK (interactieve modus) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (batchmodus) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**ad-hocschema:** In de interactieve modus kunt u maximaal 1 miljard rijen (~1,05 TB gegevens op schijf) niet-XDM-gegevens lezen in minder dan 3 minuten. In de modus Batch kunt u maximaal 1 miljard rijen (ongeveer 1,05 TB gegevens op schijf) niet-XDM-gegevens lezen in ongeveer 18 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Grootte op schijf | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Interactieve SDK-modus (in seconden) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | 22s | 28.4s | 40s | 97.4s | 154.5s |
| SDK-batchmodus (in seconden) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

#### Grenswaarden voor Spark-laptops (Scala kernel):

**XDM ExperienceEvent-schema:** In de interactieve modus kunt u maximaal 5 miljoen rijen (~13,42 GB gegevens op schijf) met XDM-gegevens lezen in ongeveer 18 minuten. De interactieve wijze steunt slechts tot 5 miljoen rijen. Als u wenst om grotere datasets te lezen, wordt het geadviseerd u op de wijze van de Partij over te schakelen. In de Batchmodus kunt u maximaal 500 miljoen rijen (~1,31 TB gegevens op schijf) met XDM-gegevens lezen in ongeveer 14 uur.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Grootte op schijf | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| Interactieve SDK-modus (in seconden) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK-batchmodus (in seconden) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**ad-hocschema:** In de interactieve modus kunt u maximaal 1 miljard rijen (~1,05 TB gegevens op schijf) niet-XDM-gegevens lezen in minder dan 3 minuten. In de modus Batch kunt u maximaal 1 miljard rijen (ongeveer 1,05 TB gegevens op schijf) niet-XDM-gegevens lezen in ongeveer 16 minuten.

| Aantal rijen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Grootte op schijf | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Interactieve SDK-modus (in seconden) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | 29.2s | 29.7s | 36.9s | 83.5s | 139s |
| SDK-batchmodus (in seconden) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

### Lezen uit een gegevensset in Python/R

Met Python- en R-laptops kunt u gegevens pagineren wanneer u gegevenssets opent. De voorbeeldcode voor het lezen van gegevens met en zonder paginering wordt hieronder getoond.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Lezen uit een gegevensset in Python/R zonder paginering

Het uitvoeren van de volgende code zal de volledige dataset lezen. Als de uitvoering is gelukt, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele wordt verwezen `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`: De unieke identiteit van de gegevensset waartoe toegang moet worden verkregen

#### Lezen uit een gegevensset in Python/R met paginering

Het uitvoeren van de volgende code zal gegevens van de gespecificeerde dataset lezen. Paginering wordt bereikt door de gegevens te beperken en te verschuiven via de functies `limit()` en `offset()` . Het beperken van gegevens heeft betrekking op het maximumaantal gegevenspunten dat moet worden gelezen, terwijl het compenseren verwijst naar het aantal gegevenspunten dat vóór het lezen van gegevens moet worden overgeslagen. Als de leesbewerking met succes wordt uitgevoerd, worden de gegevens opgeslagen als een Pandas-dataframe waarnaar door de variabele wordt verwezen `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`: De unieke identiteit van de gegevensset waartoe toegang moet worden verkregen

### Lees van een dataset in PySpark/Spark/Scala

Met een actieve PySpark of Opgezette Boek Scala, breid het lusje van de Ontdekkingsreiziger **van** Gegevens van linkerzijbalk uit en klik **Datasets** tweemaal om een lijst van beschikbare datasets te bekijken. Klik met de rechtermuisknop op de gegevensset die u wilt openen en klik op Gegevens **zoeken in laptop**. De volgende codecellen worden gegenereerd:

#### PySpark (Spark 2.4) {#pyspark2.4}

Met de introductie van Spark 2.4 wordt [`%dataset`](#magic) aangepaste magie geleverd.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala (park 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>In Scala, kunt u gebruiken `sys.env()` om een waarde van binnen te verklaren en terug te keren `option`.

### Het gebruiken van de magie van %dataset in PySpark 3 (Vonk 2.4) laptops {#magic}

Met de introductie van Spark 2.4 wordt `%dataset` aangepaste magie geleverd voor gebruik in nieuwe PySpark 3 (Spark 2.4) notebooks (Python 3 kernel).

**Gebruik**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Beschrijving**

Een toveropdracht voor aangepaste Data Science Workspace voor het lezen of schrijven van een gegevensset van een Python-laptop (Python 3-kernel).

* **{action}**: Het type van actie op de dataset uit te voeren. Er zijn twee handelingen beschikbaar: &quot;read&quot; of &quot;write&quot;.
* **—datasetId {id}**: Gebruikt om identiteitskaart van de dataset te leveren om te lezen of te schrijven. Dit is een verplicht argument.
* **—dataFrame {df}**: Het dataframe van de pandas. Dit is een verplicht argument.
   * Wanneer de handeling &quot;read&quot; is, is {df} de variabele waar de resultaten van de bewerking voor het lezen van de gegevensset beschikbaar zijn.
   * Wanneer de actie &quot;schrijven&quot;is, wordt dit dataframe {df} geschreven aan de dataset.
* **—modus (optioneel)**: Toegestane parameters zijn &quot;batch&quot; en &quot;interactief&quot;. De modus is standaard ingesteld op &quot;interactief&quot;. Het wordt aanbevolen de modus &quot;batch&quot; te gebruiken bij het lezen van grote hoeveelheden gegevens.

**Voorbeelden**

* **Voorbeeld** lezen: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Voorbeeld** schrijven: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### De gegevens van de vraag gebruikend de Dienst van de Vraag in Python

Met JupyterLab op Platform kunt u SQL in een Python-laptop gebruiken om toegang te krijgen tot gegevens via <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">Adobe Experience Platform Query Service</a>. De toegang tot van gegevens door de Dienst van de Vraag kan nuttig zijn om grote datasets wegens zijn superieure lopende tijden te behandelen. Houd er rekening mee dat het opvragen van gegevens met behulp van Query Service een verwerkingstijdslimiet van tien minuten heeft.

Alvorens u de Dienst van de Vraag in JupyterLab gebruikt, zorg ervoor u een werkend inzicht in de SQL syntaxis <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">van de Dienst van de</a>Vraag hebt.

Het vragen van gegevens die de Dienst van de Vraag gebruiken vereist u om de naam van de doeldataset te verstrekken. U kunt de noodzakelijke codecellen produceren door de gewenste dataset te vinden gebruikend de ontdekkingsreiziger **van** Gegevens. Klik met de rechtermuisknop op de gegevenssetlijst en klik op **Query-gegevens in laptop** om de volgende twee codecellen in uw laptop te genereren:


Om de Dienst van de Vraag in JupyterLab te gebruiken, moet u eerst een verbinding tussen uw werkende Notitieboekje Python en de Dienst van de Vraag tot stand brengen. Dit kan worden bereikt door de eerste gegenereerde cel uit te voeren.

```python
qs_connect()
```

In de tweede gegenereerde cel moet de eerste regel worden gedefinieerd vóór de SQL-query. Door gebrek, bepaalt de geproduceerde cel een facultatieve variabele (`df0`) die de vraagresultaten als dataframe van de Pandas bewaart. <br>Het `-c QS_CONNECTION` argument is verplicht en vertelt de kernel om de SQL vraag tegen de Dienst van de Vraag uit te voeren. Zie de [bijlage](#optional-sql-flags-for-query-service) voor een lijst van extra argumenten.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Er kan rechtstreeks naar Python-variabelen worden verwezen binnen een SQL-query met behulp van een syntaxis met tekenreeksindeling en de variabelen tussen accolades (`{}`), zoals in het volgende voorbeeld wordt getoond:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filter ExperienceEvent-gegevens in Python/R

Om tot een dataset ExperienceEvent in een notitieboekje van Python of van R toegang te hebben en te filtreren, moet u identiteitskaart van de dataset (`{DATASET_ID}`) samen met de filterregels verstrekken die een specifieke tijdwaaier gebruikend logische exploitanten bepalen. Wanneer een tijdwaaier wordt bepaald, wordt om het even welke gespecificeerde paginering genegeerd en de volledige dataset wordt overwogen.

Een lijst met filteroperatoren wordt hieronder beschreven:

* `eq()`: Gelijk aan
* `gt()`: Groter dan
* `ge()`: Groter dan of gelijk aan
* `lt()`: Minder dan
* `le()`: Kleiner dan of gelijk aan
* `And()`: Logische operator AND
* `Or()`: Logische operator OR

De volgende cellen filteren een dataset ExperienceEvent op gegevens die uitsluitend tussen 1 januari 2019 en eind december 2019 bestonden.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### Filter ExperienceEvent-gegevens in PySpark/Spark

Als u toegang krijgt tot en filtert op een dataset ExperienceEvent in een PySpark- of Scala-laptop, moet u de gegevenssetidentiteit (`{DATASET_ID}`), de IMS-identiteit van uw organisatie en de filterregels die een specifieke tijdreeks definiëren, opgeven. Een het Filtreren tijdwaaier wordt bepaald door de functie te gebruiken `spark.sql()`, waar de functieparameter een SQL vraagkoord is.

De volgende cellen filteren een dataset ExperienceEvent op gegevens die uitsluitend tussen 1 januari 2019 en eind december 2019 bestonden.

#### PySpark 3 (Spark 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Scala (park 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>In Scala, kunt u gebruiken `sys.env()` om een waarde van binnen te verklaren en terug te keren `option`. Dit elimineert de behoefte om variabelen te bepalen als u weet zij slechts één keer zullen worden gebruikt. In het volgende voorbeeld wordt uit het bovenstaande voorbeeld `val userToken` het voorbeeld opgehaald en inline gedeclareerd `option` als alternatief:
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## Ondersteunde bibliotheken {#supported-libraries}

### Python/R

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
| jupyterlab | 1.0.4 |
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
| python | 3.6.7 |
| mkl-rt | 11.1 |

## Optionele SQL-vlaggen voor Query Service {#optional-sql-flags-for-query-service}

Deze lijst schetst de facultatieve SQL vlaggen die voor de Dienst van de Vraag kunnen worden gebruikt.

| **Markering** | **Beschrijving** |
| --- | --- |
| `-h`, `--help` | Help-bericht weergeven en afsluiten. |
| `-n`, `--notify` | Optie in-/uitschakelen voor het melden van queryresultaten. |
| `-a`, `--async` | Als u deze markering gebruikt, wordt de query asynchroon uitgevoerd en kan de kernel vrijkomen terwijl de query wordt uitgevoerd. Wees voorzichtig wanneer u queryresultaten toewijst aan variabelen, omdat deze mogelijk niet gedefinieerd zijn als de query niet volledig is. |
| `-d`, `--display` | Met deze markering voorkomt u dat resultaten worden weergegeven. |

