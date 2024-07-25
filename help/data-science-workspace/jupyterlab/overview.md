---
keywords: Experience Platform;JupyterLab;laptops;Data Science Workspace;populaire onderwerpen;jupyterlab
solution: Experience Platform
title: Overzicht van de gebruikersinterface van JupyterLab
description: JupyterLab is een webgebaseerde gebruikersinterface voor Project Jupyter en is nauw geïntegreerd in Adobe Experience Platform. Het verstrekt een interactieve ontwikkelomgeving voor gegevenswetenschappers om met Notities Jupyter, code, en gegevens te werken. Dit document biedt een overzicht van JupyterLab en de bijbehorende functies, evenals instructies om algemene handelingen uit te voeren.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 0%

---

# Overzicht van de gebruikersinterface [!DNL JupyterLab]

[!DNL JupyterLab] is een web-based gebruikersinterface voor [ Jupyter van het Project ](https://jupyter.org/) en is strak geïntegreerd in Adobe Experience Platform. Het verstrekt een interactieve ontwikkelomgeving voor gegevenswetenschappers om met Notities Jupyter, code, en gegevens te werken.

Dit document biedt een overzicht van [!DNL JupyterLab] en de bijbehorende functies, evenals instructies om algemene handelingen uit te voeren.

## [!DNL JupyterLab] on [!DNL Experience Platform]

De JupyterLab-integratie van Experience Platform gaat gepaard met architectuurwijzigingen, ontwerpoverwegingen, aangepaste laptopextensies, vooraf geïnstalleerde bibliotheken en een interface op basis van Adoben.

In de volgende lijst worden enkele functies beschreven die uniek zijn voor JupyterLab op Platform:

| Functie | Beschrijving |
| --- | --- |
| **Kernels** | Kernels bieden laptop en andere [!DNL JupyterLab] front-ends de mogelijkheid om code in verschillende programmeertalen uit te voeren en te introspecteren. [!DNL Experience Platform] bevat aanvullende kernels die de ontwikkeling in [!DNL Python] , R, PySpark en [!DNL Spark] ondersteunen. Zie de [ kernels ](#kernels) sectie voor meer details. |
| **Toegang van Gegevens** | U hebt vanuit [!DNL JupyterLab] rechtstreeks toegang tot bestaande gegevenssets met volledige ondersteuning voor lees- en schrijfmogelijkheden. |
| **[!DNL Platform]service integration** | Dankzij de ingebouwde integratie kunt u andere [!DNL Platform] -services rechtstreeks vanuit [!DNL JupyterLab] gebruiken. Een volledige lijst van gesteunde integratie wordt verstrekt in de sectie over [ Integratie met andere diensten van het Platform ](#service-integration). |
| **Verificatie** | Naast <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank"> JupyterLab&#39;s ingebouwde veiligheidsmodel </a>, wordt elke interactie tussen uw toepassing en Experience Platform, met inbegrip van de dienst-aan-dienst van het Platform mededeling gecodeerd en voor authentiek verklaard door <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS) </a>. |
| **de bibliotheken van de Ontwikkeling** | In [!DNL Experience Platform] biedt [!DNL JupyterLab] vooraf geïnstalleerde bibliotheken voor [!DNL Python] , R en PySpark. Zie [ bijlage ](#supported-libraries) voor een volledige lijst van gesteunde bibliotheken. |
| **controlemechanisme van de Bibliotheek** | Wanneer de vooraf geïnstalleerde bibliotheken niet geschikt zijn voor uw behoeften, kunnen extra bibliotheken voor Python en R worden geïnstalleerd en tijdelijk in geïsoleerde containers worden opgeslagen om de integriteit van [!DNL Platform] te handhaven en uw gegevens veilig te houden. Zie de [ kernels ](#kernels) sectie voor meer details. |

>[!NOTE]
>
>Aanvullende bibliotheken zijn alleen beschikbaar voor de sessie waarin ze zijn geïnstalleerd. Wanneer u nieuwe sessies start, moet u alle extra bibliotheken die u nodig hebt opnieuw installeren.

## Integratie met andere [!DNL Platform] -services {#service-integration}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform] . Dankzij de integratie van [!DNL JupyterLab] on [!DNL Platform] als een ingesloten IDE kunt u communiceren met andere [!DNL Platform] -services, zodat u [!DNL Platform] optimaal kunt gebruiken. De volgende [!DNL Platform] -services zijn beschikbaar in [!DNL JupyterLab] :

* **[!DNL Catalog Service]:** open en verken datasets met lees- en schrijffunctionaliteit.
* **[!DNL Query Service]:** heb toegang tot en verken datasets gebruikend SQL, die lagere gegevenstoegang overheadkosten verstrekken wanneer het behandelen van grote hoeveelheden gegevens.
* **[!DNL Sensei ML Framework]:** Modelontwikkeling met de mogelijkheid om gegevens te trainen en te scoren, en het maken van recept met één klik.
* **[!DNL Experience Data Model (XDM)]:** Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. [ Model van de Gegevens van de Ervaring (XDM) ](https://www.adobe.com/go/xdm-home-en), die door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

>[!NOTE]
>
>Sommige [!DNL Platform] -service-integratie op [!DNL JupyterLab] is beperkt tot specifieke kernels. Verwijs naar de sectie op [ kernels ](#kernels) voor meer details.

## Belangrijke functies en veelvoorkomende bewerkingen

In de volgende secties vindt u informatie over de belangrijkste functies van [!DNL JupyterLab] en instructies voor het uitvoeren van veelvoorkomende bewerkingen:

* [Access JupyterLab](#access-jupyterlab)
* [JupyterLab-interface](#jupyterlab-interface)
* [Codecellen](#code-cells)
* [Kernels](#kernels)
* [Kernel-sessies](#kernel-sessions)
* [Launcher](#launcher)

### Toegang [!DNL JupyterLab] {#access-jupyterlab}

In [ Adobe Experience Platform ](https://platform.adobe.com), selecteer **[!UICONTROL Notebooks]** van de linkernavigatiekolom. Laat [!DNL JupyterLab] enige tijd volledig initialiseren.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interface {#jupyterlab-interface}

De interface [!DNL JupyterLab] bestaat uit een menubalk, een opvouwbare linkerzijbalk en het hoofdwerkgebied met tabbladen met documenten en activiteiten.

**bar van het Menu**

De menubalk boven aan de interface heeft menu&#39;s op hoofdniveau die acties beschikbaar maken in [!DNL JupyterLab] met hun sneltoetsen:

* **Dossier:** Acties met betrekking tot dossiers en folders
* **geef uit:** Acties met betrekking tot het uitgeven van documenten en andere activiteiten
* **Mening:** Acties die de verschijning van [!DNL JupyterLab] veranderen
* **Looppas:** Acties voor het runnen van code in verschillende activiteiten zoals laptops en codeconsoles
* **Kernel:** Acties voor het beheren van kernels
* **Lusjes:** een lijst van open documenten en activiteiten
* **Montages:** Gemeenschappelijke montages en een geavanceerde montagesredacteur
* **Hulp:** een lijst van [!DNL JupyterLab] en kernel hulpverbindingen

**Linkerzijbalk**

De linkerzijbalk bevat klikbare tabbladen die toegang bieden tot de volgende functies:

* **browser van het Dossier:** een lijst van opgeslagen notitiedocumenten en folders
* **ontdekkingsreiziger van Gegevens:** doorblader, toegang, en onderzoek datasets en schema&#39;s
* **lopende kernels en terminals:** Een lijst van actieve kernel en eindzittingen met de capaciteit om te eindigen
* **Bevelen:** een lijst van nuttige bevelen
* **de inspecteur van het Cel:** de celredacteur van A die toegang tot hulpmiddelen en meta-gegevens nuttig verleent voor vestiging een notitieboekje voor presentatiedoeleinden
* **lusjes:** een lijst van open lusjes

Selecteer een tab om de bijbehorende functies weer te geven of selecteer een uitgevouwen tab om de linkerzijbalk samen te vouwen, zoals hieronder wordt getoond:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Belangrijkste het werkgebied**

In het hoofdwerkgebied van [!DNL JupyterLab] kunt u documenten en andere activiteiten rangschikken in tabbladen waarvan u de grootte kunt wijzigen of die u kunt onderverdelen. Sleep een tab naar het midden van een tabdeelvenster om de tab te migreren. Verdeel een deelvenster door een tab naar links, rechts, boven of onder in het deelvenster te slepen:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### GPU- en geheugenserverconfiguratie in [!DNL Python]/R

In [!DNL JupyterLab] selecteer het tandwielpictogram in de hoogste juiste hoek om *de serverconfiguratie van het Notitieboekje* te openen. Met de schuifregelaar kunt u de GPU in- en uitschakelen en de benodigde hoeveelheid geheugen toewijzen. De hoeveelheid geheugen die u kunt toewijzen, is afhankelijk van de hoeveelheid geheugen die uw organisatie heeft ingericht. Selecteer **[!UICONTROL Update configs]** voor opslaan.

>[!NOTE]
>
>Per organisatie is slechts één GPU beschikbaar voor laptops. Als de GPU in gebruik is, moet u wachten op de gebruiker die momenteel de GPU heeft gereserveerd om deze vrij te geven. Dit kan worden gedaan door uit te loggen of GPU in een nutteloze staat voor vier of meer uren te verlaten.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Beëindigen en opnieuw starten [!DNL JupyterLab]

In [!DNL JupyterLab] kunt u uw sessie beëindigen om te voorkomen dat meer bronnen worden gebruikt. Begin door het **machtspictogram** ![ machtspictogram ](/help/images/icons/power.png) te selecteren, dan uitgezocht **[!UICONTROL Shut Down]** van popover die lijkt om uw zitting te eindigen. Laptopsessies worden automatisch beëindigd na 12 uur geen activiteit.

Om [!DNL JupyterLab] opnieuw te beginnen, selecteer het **pictogram van het nieuwe begin** ![ herstart pictogram ](/help/images/icons/restart.png) dat direct aan de linkerzijde van het machtspictogram wordt gevestigd, dan uitgezocht **[!UICONTROL Restart]** van popover die verschijnt.

![ beëindigt jupyterlab ](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Codecellen {#code-cells}

Codecellen zijn de belangrijkste inhoud van laptops. Ze bevatten broncode in de taal van de bijbehorende kernel van de laptop en de uitvoer als gevolg van het uitvoeren van de codecel. Rechts van elke codecel wordt een aantal uitvoeringen weergegeven die de volgorde van uitvoering ervan aangeven.

![](../images/jupyterlab/user-guide/code_cell.png)

Vaak voorkomende celhandelingen worden hieronder beschreven:

* **voeg een cel toe:** klik het plus symbool (**+**) van het notitieboekjecomenu om een lege cel toe te voegen. Nieuwe cellen worden onder de cel geplaatst waarmee momenteel wordt gewerkt, of aan het einde van de laptop als geen bepaalde cel de focus heeft.

* **Beweeg een cel:** Plaats uw curseur rechts van de cel u wenst te bewegen, dan klik en sleep de cel aan een nieuwe plaats. Als u bovendien een cel van het ene notebook naar het andere verplaatst, wordt de cel met de inhoud gerepliceerd.

* **voert een cel uit:** klik op het lichaam van de cel u wenst uit te voeren en dan het **spel** pictogram (**▶**) van het notitieboekjecomenu te klikken. Een asterisk (**\***) wordt getoond in de uitvoerteller van de cel wanneer de kernel de uitvoering verwerkt, en met een geheel na voltooiing vervangen.

* **Schrap een cel:** klik op het lichaam van de cel u wenst om dan het **schaar** pictogram te schrappen en te klikken.

### Kernels {#kernels}

Notebookkernels zijn de taalspecifieke computerengines voor de verwerking van notebookcellen. Naast [!DNL Python] biedt [!DNL JupyterLab] extra taalondersteuning in R, PySpark en [!DNL Spark] (Scala). Wanneer u een notitieboekjectdocument opent, wordt de bijbehorende kernel gestart. Wanneer een laptopcel wordt uitgevoerd, voert de kernel de berekening uit en levert dit resultaten op die aanzienlijke CPU- en geheugenbronnen verbruiken. Let op: toegewezen geheugen wordt pas vrijgemaakt wanneer de kernel wordt afgesloten.

Bepaalde kenmerken en functies zijn beperkt tot bepaalde kernels zoals beschreven in de onderstaande tabel:

| Kernel | Ondersteuning voor bibliotheekinstallatie | [!DNL Platform] integraties |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Nee | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Kernel-sessies {#kernel-sessions}

Elke actieve laptop of activiteit op [!DNL JupyterLab] maakt gebruik van een kernel-sessie. Alle actieve zittingen kunnen worden gevonden door de **Lopende terminals en kernels** tabel van linkerzijbalk uit te breiden. Het type en de toestand van de kernel voor een laptop kunnen worden geïdentificeerd door de laptop rechtsboven te volgen. In het onderstaande diagram is de bijbehorende kernel van de laptop **[!DNL Python]3** en wordt de huidige toestand weergegeven door een grijze cirkel naar rechts. Een holle cirkel impliceert een nutteloze kernel en een stevige cirkel impliceert een bezige kernel.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Als de kernel voor een lange periode wordt gesloten of inactief, dan **Geen Kernel!** met een effen cirkel wordt weergegeven. Activeer een kernel door op de kernel-status te klikken en het juiste kernel-type te selecteren, zoals hieronder wordt getoond:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Launcher {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

De aangepaste *Lanceerinrichting* voorziet u van nuttige notitieboekjecalplaatjes voor hun gesteunde kernels om u te helpen uw taak beginnen, die omvat:

| Sjabloon | Beschrijving |
| --- | --- |
| Leeg | Een leeg laptopbestand. |
| Starter | Een voorgevulde laptop die de gegevensexploratie aantoont met behulp van voorbeeldgegevens. |
| Detailhandel | Een voorgevuld notitieboekje dat het [ detailhandelrecept ](../pre-built-recipes/retail-sales.md) kenmerkt gebruikend steekproefgegevens. |
| Recipe Builder | Een laptopsjabloon voor het maken van een recept in [!DNL JupyterLab] . De voorgevulde code en opmerkingen tonen en beschrijven het proces voor het maken van recept. Verwijs naar de [ notitieboekje aan recept zelfstudie ](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) voor een gedetailleerde analyse. |
| [!DNL Query Service] | Een voorgevulde laptop die het gebruik van [!DNL Query Service] rechtstreeks in [!DNL JupyterLab] aantoont, beschikt over voorbeeldworkflows waarmee gegevens op schaal worden geanalyseerd. |
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

Om een nieuwe *Lanceerinrichting* te openen, klik **Dossier > Nieuwe Lanceerinrichting**. Alternatief, breid browser van het **Dossier** van linkerzijbalk uit en klik het plus symbool (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Volgende stappen

Om meer over elk van de gesteunde laptops te leren en hoe te om hen te gebruiken, bezoek de [ toegang van de documentengegevens van Jupyterlab ](./access-notebook-data.md) ontwikkelaarsgids. Deze handleiding is gericht op het gebruik van JupyterLab-laptops voor toegang tot uw gegevens, zoals lezen, schrijven en vragen om gegevens. De gids voor gegevenstoegang bevat ook informatie over de maximale hoeveelheid gegevens die kan worden gelezen door elke ondersteunde laptop.

## Ondersteunde bibliotheken {#supported-libraries}

Kopieer en plak `!conda list` in een nieuwe cel voor een lijst met ondersteunde pakketten in Python, R en PySpark en voer vervolgens de cel uit. Een lijst met ondersteunde pakketten wordt in alfabetische volgorde gevuld.

![ voorbeeld ](../images/jupyterlab/user-guide/libraries.PNG)

Bovendien worden de volgende gebiedsdelen gebruikt maar niet vermeld:
* CUDA 11.2
* CUDNN 8.1

