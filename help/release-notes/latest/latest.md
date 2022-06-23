---
title: Opmerkingen bij de release van Adobe Experience Platform juni 2022
description: In de release van juni 2022 staat Adobe Experience Platform vermeld.
source-git-commit: 4edd2042234149ab8836da4fc58eb4d6084ae205
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 22 juni 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [Query-service](#query-service)
- [Bronnen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen voor [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations is nu slimmer en sneller. De nieuwe bevestigingscontroles verminderen beduidend de gemeenschappelijkste afbeeldingsfouten, zo verminderend tijd-aan-Waarde. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## [!DNL Data Science Workspace] {#dsw}

De Werkruimte van de Wetenschap van gegevens gebruikt machine het leren en kunstmatige intelligentie om inzichten van uw gegevens te ontketenen. De Data Science Workspace is geïntegreerd in Adobe Experience Platform en helpt u om voorspellingen te maken met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen. Een van de manieren waarop de Werkruimte van de Wetenschap van Gegevens dit verwezenlijkt is door het gebruik van JupyterLab. JupyterLab is een webgebaseerde gebruikersinterface voor <a href="https://jupyter.org/" target="_blank">Jupyter-project</a> en is nauw geïntegreerd in Adobe Experience Platform. Het biedt een interactieve ontwikkelomgeving voor gegevenswetenschappers die werken met Jupyter-laptops, -code en -gegevens.

| Functie | Beschrijving |
| --- | --- |
| JupyterLab Launcher | De JupyterLab Launcher bevat nu startteksten voor Spark 3.2-laptops. Starters voor Spark 2.4-laptops worden nu vervangen door Spark 3.2-laptops en maken deel uit van deze release. |
| Vonk 3.2 | Nieuwe Scala (Vonk) en PySpark recepten gebruiken nu Vonk 3.2 |
| Kernels | Scala-laptops (Spark) zijn nu ontworpen via de Scala-kernel. PySpark laptops zijn nu ontworpen via de Python Kernel. De kernel van de Vonk en van PySpark wordt afgekeurd en geplaatst om in een verdere versie worden verwijderd. |
| Ontvangers | Nieuwe PySpark- en Spark-recepten volgen nu de Docker-workflow, vergelijkbaar met Python- en R-recepten. |

{style=&quot;table-layout:auto&quot;}

Voor meer algemene informatie over de Werkruimte van de Wetenschap van Gegevens, zie [overzichtsdocumentatie](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| (bèta) Destination SDK-ondersteuning voor [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) bestandsgebaseerde doelen en [configureerbare bestandsnamen](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | U kunt de Destination SDK nu gebruiken om Google Cloud Storage-doelen te maken en aangepaste bestandsnamen voor geëxporteerde bestanden te definiëren via bestandsnaammacro&#39;s. <br><br> Bestandsgebaseerde doelondersteuning in Adobe Experience Platform Destination SDK staat momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd. |

{style=&quot;table-layout:auto&quot;}

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [(bèta) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | De [!DNL Google Ad Manager 360] verbinding maakt batch-upload mogelijk voor [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage] <br><br>Deze bestemming is momenteel in Bèta en is slechts beschikbaar aan een beperkt aantal klanten. Om toegang tot [!DNL Google Ad Manager 360] verbinding, neem contact op met uw Adobe-vertegenwoordiger en geef uw [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Activeer profielen voor gerichte Media enquêtes en koppel inzameling terug om klantenbehoeften en verwachtingen beter te begrijpen. |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | De Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) de bestemming staat u toe om voor authentiek verklaarde eerste-partijsegmenten met goedgekeurde adverteerders en gebruikers voor campagneactivering met DSP te delen. |

{style=&quot;table-layout:auto&quot;}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL Data Lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL Data Lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ad-hocschema-labeling | Beheer toegang tot gevoelige gegevens door etiketten op gegevensgebieden van ad hoc regelingen toe te passen die automatisch door de vraag van de Dienst CTAS van de Vraag worden geproduceerd. U kunt het gebruik van bepaalde gebieden, of datasets, van ad hoc regelingen beperken om toegang tot zowel gevoelige persoonlijke gegevens als persoonlijk identificeerbare informatie te controleren. Door op attribuut-gebaseerde toegangsbeheercapaciteit te gebruiken kunt u ad hoc schemagebieden door de UI van het Platform etiketteren. |
| `FLATTEN` instellen | Wanneer het verbinden met een gegevensbestand door derdehulpmiddelen van BI, `FLATTEN` bij het instellen worden geneste gegevensstructuren afgevlakt in afzonderlijke kolommen, waarbij de kenmerknaam de kolomnaam wordt die de rijwaarden bevat. Dit verbetert de bruikbaarheid van ad-hocschema&#39;s en vermindert de vereiste werkbelasting om gegevens op te halen, te analyseren, om te zetten en te melden in BI hulpmiddelen die geen genestelde gegevensstructuren steunen. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de Diensten van de Vraag, verwijs naar [Overzicht van Query Service](../../query-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Bètaversie van [!DNL Mixpanel] bron | U kunt nu de opdracht [!DNL Mixpanel] bron voor het opnemen van analysegegevens uit uw [!DNL Mixpanel] aan Experience Platform. Zie de [[!DNL Mixpanel] brondocumentatie](../../sources/connectors/analytics/mixpanel.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
