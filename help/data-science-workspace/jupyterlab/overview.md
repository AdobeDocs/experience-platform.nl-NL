---
keywords: Experience Platform;JupyterLab;laptops;Data Science Workspace;populaire onderwerpen;jupyterlab
solution: Experience Platform
title: Overzicht van de gebruikersinterface van JupyterLab
topic: Overzicht
description: JupyterLab is een webgebaseerde gebruikersinterface voor Project Jupyter en is nauw geïntegreerd in Adobe Experience Platform. Het verstrekt een interactieve ontwikkelomgeving voor gegevenswetenschappers om met Notities Jupyter, code, en gegevens te werken. Dit document biedt een overzicht van JupyterLab en de bijbehorende functies, evenals instructies om algemene handelingen uit te voeren.
translation-type: tm+mt
source-git-commit: 9d84fc1eb898020ed4b154c091fcc9fc4933c7de
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---


# [!DNL JupyterLab] Overzicht van gebruikersinterface

[!DNL JupyterLab] is een webgebaseerde gebruikersinterface voor  [Project ](https://jupyter.org/) Jupyterand en is nauw geïntegreerd in Adobe Experience Platform. Het verstrekt een interactieve ontwikkelomgeving voor gegevenswetenschappers om met Notities Jupyter, code, en gegevens te werken.

Dit document biedt een overzicht van [!DNL JupyterLab] en de bijbehorende functies, evenals instructies om algemene handelingen uit te voeren.

## [!DNL JupyterLab] op  [!DNL Experience Platform]

De JupyterLab-integratie van Experience Platform gaat gepaard met architectuurwijzigingen, ontwerpoverwegingen, aangepaste laptopextensies, vooraf geïnstalleerde bibliotheken en een Adobe-interface.

In de volgende lijst worden enkele functies beschreven die uniek zijn voor JupyterLab op Platform:

| Functie | Beschrijving |
| --- | --- |
| **Kernels** | Kernels bieden laptop en andere [!DNL JupyterLab] front-ends de mogelijkheid om code in verschillende programmeertalen uit te voeren en in te voeren. [!DNL Experience Platform] verstrekt extra kernels om ontwikkeling in  [!DNL Python], R, PySpark, en  [!DNL Spark]. te steunen. Zie de sectie [kernels](#kernels) voor meer informatie. |
| **Toegang tot gegevens** | Toegang tot bestaande datasets rechtstreeks vanuit [!DNL JupyterLab] met volledige ondersteuning voor lees- en schrijfmogelijkheden. |
| **[!DNL Platform]serviceintegratie** | Dankzij de ingebouwde integratie kunt u andere [!DNL Platform] services rechtstreeks vanuit [!DNL JupyterLab] gebruiken. Een volledige lijst van gesteunde integraties wordt verstrekt in de sectie over [Integratie met andere diensten van de Platform](#service-integration). |
| **Verificatie** | Naast <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">ingebouwde veiligheidsmodel van JupyterLab</a>, wordt elke interactie tussen uw toepassing en Experience Platform, met inbegrip van de dienst-aan-dienst van het Platform mededeling gecodeerd en door <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a> voor authentiek verklaard. |
| **Ontwikkelingsbibliotheken** | In [!DNL Experience Platform], [!DNL JupyterLab] verstrekt vooraf geïnstalleerde bibliotheken voor [!DNL Python], R, en PySpark. Zie [appendix](#supported-libraries) voor een volledige lijst van gesteunde bibliotheken. |
| **Bibliotheekcontroller** | Wanneer de vooraf geïnstalleerde bibliotheken niet aan uw behoeften voldoen, kunnen extra bibliotheken voor Python en R worden geïnstalleerd en tijdelijk in geïsoleerde containers worden opgeslagen om de integriteit van [!DNL Platform] te handhaven en uw gegevens veilig te houden. Zie de sectie [kernels](#kernels) voor meer informatie. |

>[!NOTE]
>
>Aanvullende bibliotheken zijn alleen beschikbaar voor de sessie waarin ze zijn geïnstalleerd. Wanneer u nieuwe sessies start, moet u alle extra bibliotheken die u nodig hebt opnieuw installeren.

## Integratie met andere [!DNL Platform] services {#service-integration}

Standaardisering en interoperabiliteit zijn belangrijke concepten achter [!DNL Experience Platform]. Dankzij de integratie van [!DNL JupyterLab] op [!DNL Platform] als een ingesloten IDE kan de toepassing communiceren met andere [!DNL Platform]-services, zodat u [!DNL Platform] volledig kunt benutten. De volgende [!DNL Platform] services zijn beschikbaar in [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Toegang tot en verken gegevenssets met lees- en schrijffuncties.
* **[!DNL Query Service]:** Open en verken datasets gebruikend SQL, die lagere gegevenstoegang overheadkosten verstrekken wanneer het behandelen van grote hoeveelheden gegevens.
* **[!DNL Sensei ML Framework]:** Modelontwikkeling met de mogelijkheid om gegevens op te leiden en te scoren en het maken van recept met één klik.
* **[!DNL Experience Data Model (XDM)]:** Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. [Het Model van Gegevens van de ervaring (XDM)](https://www.adobe.com/go/xdm-home-en), die door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

>[!NOTE]
>
>Sommige [!DNL Platform] service-integraties op [!DNL JupyterLab] zijn beperkt tot specifieke kernels. Raadpleeg de sectie over [kernels](#kernels) voor meer informatie.

## Belangrijke functies en veelvoorkomende bewerkingen

In de volgende secties wordt informatie gegeven over de belangrijkste kenmerken van [!DNL JupyterLab] en instructies voor het uitvoeren van gemeenschappelijke bewerkingen:

* [Access JupyterLab](#access-jupyterlab)
* [JupyterLab-interface](#jupyterlab-interface)
* [Codecellen](#code-cells)
* [Kernels](#kernels)
* [Kernel-sessies](#kernel-sessions)
* [Launcher](#launcher)

### Ga naar [!DNL JupyterLab] {#access-jupyterlab}

Selecteer **[!UICONTROL Laptops]** in [Adobe Experience Platform](https://platform.adobe.com) in de linkernavigatiekolom. Sta wat tijd voor [!DNL JupyterLab] toe om volledig te initialiseren.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interface  {#jupyterlab-interface}

De interface [!DNL JupyterLab] bestaat uit een menubalk, een doen ineenstorten linkerzijbalk, en het belangrijkste het werkgebied dat lusjes van documenten en activiteiten bevat.

**Menubalk**

De menubalk bij de bovenkant van de interface heeft menu&#39;s op hoofdniveau die acties beschikbaar in [!DNL JupyterLab] met hun toetsenbordkortere weg blootstellen:

* **Bestand:** handelingen met betrekking tot bestanden en mappen
* **Bewerken:** handelingen met betrekking tot het bewerken van documenten en andere activiteiten
* **Weergeven:** Handelingen die de weergave van  [!DNL JupyterLab]
* **Uitvoeren:** handelingen voor het uitvoeren van code in verschillende activiteiten, zoals notebooks en codeconsoles
* **kernen:** handelingen voor het beheren van kernels
* **tabbladen:** een lijst met geopende documenten en activiteiten
* **Instellingen:** algemene instellingen en een geavanceerde instellingeneditor
* **Help:** een lijst met Help-koppelingen  [!DNL JupyterLab] en kernel-koppelingen

**Linkerzijbalk**

De linkerzijbalk bevat klikbare tabbladen die toegang bieden tot de volgende functies:

* **Bestandenbrowser:** een lijst met opgeslagen laptopdocumenten en -mappen
* **Gegevensverkenner:** doorbladeren, toegang, en onderzoeken datasets en schema&#39;s
* **Running kerels en terminals:** Een lijst van actieve kernel en eindzittingen met de capaciteit om te eindigen
* **Opdrachten:** een lijst met nuttige opdrachten
* **Celcontrole:** een celeditor die toegang biedt tot gereedschappen en metagegevens die nuttig zijn voor het instellen van een laptop voor presentatiedoeleinden
* **tabs:** een lijst met geopende tabbladen

Selecteer een tab om de bijbehorende functies weer te geven of selecteer een uitgevouwen tab om de linkerzijbalk samen te vouwen, zoals hieronder wordt getoond:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Belangrijkste werkterrein**

Met het belangrijkste werkgebied in [!DNL JupyterLab] kunt u documenten en andere activiteiten rangschikken in tabbladen waarvan u de grootte kunt wijzigen of kunt onderverdelen. Sleep een tab naar het midden van een deelvenster met tabbladen om de tab te migreren. Verdeel een deelvenster door een tab naar links, rechts, boven of onder in het deelvenster te slepen:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### GPU- en geheugenserverconfiguratie in [!DNL Python]/R

Selecteer in [!DNL JupyterLab] het tandwielpictogram in de rechterbovenhoek om *Configuratie notebookserver* te openen. Met de schuifregelaar kunt u de GPU in- en uitschakelen en de benodigde hoeveelheid geheugen toewijzen. De hoeveelheid geheugen die u kunt toewijzen, is afhankelijk van de hoeveelheid geheugen die uw organisatie heeft ingericht. Selecteer **[!UICONTROL Configuraties bijwerken]** om op te slaan.

>[!NOTE]
>
>Per organisatie is slechts één GPU beschikbaar voor laptops. Als de GPU in gebruik is, moet u wachten op de gebruiker die momenteel de GPU heeft gereserveerd om deze vrij te geven. Dit kan worden gedaan door uit te loggen of GPU in een nutteloze staat voor vier of meer uren te verlaten.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### [!DNL JupyterLab] beëindigen en opnieuw starten

In [!DNL JupyterLab], kunt u uw zitting eindigen om verdere middelen te verhinderen worden gebruikt. Begin door **machtspictogram** ![machtspictogram](../images/jupyterlab/user-guide/power_button.png) te selecteren, dan uitgezocht **[!UICONTROL Sluit]** van popover die uw zitting lijkt te eindigen. Laptopsessies worden automatisch beëindigd na twaalf uur geen activiteit.

Als u [!DNL JupyterLab] opnieuw wilt starten, selecteert u het **pictogram voor opnieuw opstarten** ![pictogram voor opnieuw opstarten](../images/jupyterlab/user-guide/restart_button.png) dat zich direct links van het energiepictogram bevindt en selecteert u **[!UICONTROL Opnieuw starten]** in de pop-up die wordt weergegeven.

![jupyterlab beëindigen](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Codecellen {#code-cells}

Codecellen zijn de belangrijkste inhoud van laptops. Ze bevatten broncode in de taal van de bijbehorende kernel van de laptop en de uitvoer als gevolg van het uitvoeren van de codecel. Rechts van elke codecel wordt een aantal uitvoeringen weergegeven die de volgorde van uitvoering ervan aangeven.

![](../images/jupyterlab/user-guide/code_cell.png)

Vaak voorkomende celhandelingen worden hieronder beschreven:

* **Voeg een cel toe:** Klik op het plusteken (**+**) in het notitieboekje om een lege cel toe te voegen. Nieuwe cellen worden onder de cel geplaatst waarmee momenteel wordt gewerkt, of aan het einde van de laptop als geen bepaalde cel de focus heeft.

* **Een cel verplaatsen:** Plaats de cursor rechts van de cel die u wilt verplaatsen, klik en sleep de cel naar een nieuwe locatie. Als u bovendien een cel van het ene notebook naar het andere verplaatst, wordt de cel met de inhoud gerepliceerd.

* **Een cel uitvoeren:** Klik op de hoofdtekst van de cel die u wilt uitvoeren en klik vervolgens op het  **** afspeelpictogram (**▶**) in het notitieboekje. Een asterisk (**\***) wordt getoond in de uitvoerteller van de cel wanneer de kernel de uitvoering verwerkt, en wordt vervangen met een geheel na voltooiing.

* **Een cel verwijderen:** Klik op de hoofdtekst van de cel die u wilt verwijderen en klik vervolgens op het  **** schaarpictogram.

### Kernels {#kernels}

Notebookkernels zijn de taalspecifieke computerengines voor de verwerking van notebookcellen. Naast [!DNL Python] biedt [!DNL JupyterLab] extra taalondersteuning in R, PySpark en [!DNL Spark] (Scala). Wanneer u een notitieboekjectdocument opent, wordt de bijbehorende kernel gestart. Wanneer een laptopcel wordt uitgevoerd, voert de kernel de berekening uit en levert dit resultaten op die aanzienlijke CPU- en geheugenbronnen verbruiken. Let op: toegewezen geheugen wordt pas vrijgemaakt wanneer de kernel wordt afgesloten.

Bepaalde kenmerken en functies zijn beperkt tot bepaalde kernels zoals beschreven in de onderstaande tabel:

| Kernel | Ondersteuning voor bibliotheekinstallatie | [!DNL Platform] integratie |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Nee | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Kernelsessies {#kernel-sessions}

Elke actieve laptop of activiteit op [!DNL JupyterLab] gebruikt een kernel-sessie. Alle actieve sessies kunt u vinden door het tabblad **Doorlopende terminals en kernels** vanuit de linkerzijbalk uit te vouwen. Het type en de toestand van de kernel voor een laptop kunnen worden geïdentificeerd door de laptop rechtsboven te volgen. In het onderstaande diagram is de bijbehorende kernel van de laptop **[!DNL Python]3** en de huidige toestand wordt weergegeven door een grijze cirkel naar rechts. Een holle cirkel impliceert een nutteloze kernel en een stevige cirkel impliceert een bezige kernel.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Als de kernel gedurende langere tijd wordt afgesloten of niet actief is, dan **Geen kernel!** met een effen cirkel. Activeer een kernel door op de kernel-status te klikken en het juiste kernel-type te selecteren, zoals hieronder wordt getoond:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Starten {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

De aangepaste *Launcher* biedt u nuttige laptopsjablonen voor hun ondersteunde kernels om u te helpen uw taak te starten, zoals:

| Sjabloon | Beschrijving |
| --- | --- |
| Leeg | Een leeg laptopbestand. |
| Starter | Een voorgevulde laptop die de gegevensexploratie aantoont met behulp van voorbeeldgegevens. |
| Detailhandel | Een voorgevulde laptop met het [recept voor detailhandel](https://adobe.ly/2wOgO3L) aan de hand van voorbeeldgegevens. |
| Recipe Builder | Een laptopsjabloon voor het maken van een recept in [!DNL JupyterLab]. De voorgevulde code en opmerkingen tonen en beschrijven het proces voor het maken van recept. Raadpleeg het [notebook to recipe tutorial](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) voor een gedetailleerde analyse. |
| [!DNL Query Service] | Een voorgevulde laptop die het gebruik van [!DNL Query Service] direct in [!DNL JupyterLab] aantoont met meegeleverde voorbeeldworkflows die gegevens op schaal analyseren. |
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

Als u een nieuwe *Launcher* wilt openen, klikt u op **Bestand > Nieuwe Launcher**. U kunt ook de **Bestandbrowser** vanuit de linkerzijbalk uitvouwen en op het plusteken (**+**) klikken:

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Volgende stappen

Voor meer informatie over elk van de ondersteunde laptops en hoe deze te gebruiken, raadpleegt u de [Jupyterlab-handleiding voor toegang tot gegevens van laptops](./access-notebook-data.md). In deze handleiding wordt vooral uitgelegd hoe u JupyterLab-laptops kunt gebruiken om toegang te krijgen tot uw gegevens, zoals lezen, schrijven en vragen om gegevens. De gids voor gegevenstoegang bevat ook informatie over de maximale hoeveelheid gegevens die kan worden gelezen door elke ondersteunde laptop.

## Ondersteunde bibliotheken {#supported-libraries}

Voor een lijst van gesteunde pakketten in Python, R, en PySpark, kopieer en deeg `!pip list --format=columns` in een nieuwe cel, dan stel de cel in werking. Een lijst met ondersteunde pakketten wordt in alfabetische volgorde gevuld.

![voorbeeld](../images/jupyterlab/user-guide/libraries.PNG)