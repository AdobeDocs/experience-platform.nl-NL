---
keywords: Experience Platform;thuis;populaire onderwerpen; analyses;classificaties
description: Leer hoe u een Adobe Analytics-bronaansluiting voor de gebruikersinterface maakt om classificatiegegevens over te brengen naar Adobe Experience Platform.
solution: Experience Platform
title: Een Adobe Analytics-bronverbinding maken voor classificatiegegevens in de gebruikersinterface
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---


# Een Adobe Analytics-bronverbinding maken voor classificatiegegevens in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een gegevensbronverbinding voor classificaties van Adobe Analytics in de gebruikersinterface voor het verzenden van classificatiegegevens naar Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Voor de gegevensverbinding Analytics Classifications moeten uw gegevens zijn gemigreerd naar de nieuwe [!DNL Classifications]-infrastructuur van Adobe Analytics voordat ze kunnen worden gebruikt. Neem contact op met uw Adobe Customer Success Manager om de migratiestatus van uw gegevens te bevestigen.

## Uw classificaties selecteren

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte Bronnen te openen. In het scherm **[!UICONTROL Catalog]** worden beschikbare bronnen weergegeven om binnenkomende verbindingen met te maken. Elke bronkaart bevat een optie waarmee u een nieuw account kunt configureren of gegevens kunt toevoegen aan een bestaand account.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Adobe toepassingen]** de **[!UICONTROL Adobe Analytics]**-kaart en selecteer vervolgens **[!UICONTROL Gegevens toevoegen]** om te gaan werken met Gegevens uit analytische classificaties.

![](../../../../images/tutorials/create/classifications/catalog.png)

De stap **[!UICONTROL Analytische bron voegt gegevens toe]** wordt weergegeven. Selecteer **[!UICONTROL Classifications]** van de hoogste kopbal om een lijst van [!DNL Classifications] datasets, met inbegrip van informatie over hun afmeting ID, de naam van de rapportreeks, en rapportsuite ID te zien.

Elke pagina toont tot tien verschillende [!DNL Classifications] datasets u van kunt kiezen. Selecteer **[!UICONTROL Volgende]** onder aan de pagina om naar meer opties te bladeren. Het paneel op het recht toont het totale aantal [!DNL Classifications] datasets u selecteerde, evenals hun namen. In dit deelvenster kunt u ook [!DNL Classifications]-gegevenssets verwijderen die u per ongeluk hebt geselecteerd of alle selecties met één actie wissen.

U kunt tot 30 verschillende [!DNL Classifications] datasets selecteren om in [!DNL Platform] te brengen.

Nadat u uw [!DNL Classifications] datasets hebt geselecteerd, selecteert u **[!UICONTROL Next]** rechtsboven op de pagina.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Uw classificaties bekijken

De stap **[!UICONTROL Review]** verschijnt, toestaand u om uw geselecteerde [!DNL Classifications] datasets te herzien alvorens het wordt gecreeerd. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Verbinding]**: Toont het bronplatform en de status van de verbinding.
* **[!UICONTROL Gegevenstype]**: Hier wordt het aantal geselecteerde items weergegeven  [!DNL Classifications].
* **[!UICONTROL Planning]**: Hiermee geeft u de synchronisatiefrequentie voor  [!DNL Classifications] gegevens weer.

Zodra u uw gegevensstroom hebt herzien, klik **[!UICONTROL Afwerking]** en laat wat tijd voor dataflow toe om worden gecreeerd.

![](../../../../images/tutorials/create/classifications/review.png)

## Uw classificatiegegevens controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen. Selecteer **[!UICONTROL Gegevensstromen]** in het scherm **[!UICONTROL Catalogus]** om een lijst weer te geven met bestaande stromen die zijn gekoppeld aan uw [!DNL Classifications]-account.

![](../../../../images/tutorials/create/classifications/dataflows.png)

Het scherm **[!UICONTROL Dataflows]** wordt weergegeven. Op deze pagina vindt u een lijst met gegevensstromen, inclusief informatie over hun naam, brongegevens en status van de gegevensstroom. Rechts is het deelvenster **[!UICONTROL Eigenschappen]** dat metagegevens bevat met betrekking tot de [!DNL Classifications]-gegevensstroom.

Selecteer **[!UICONTROL Doel dataset]** u wenst om toegang te hebben.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

De **[!UICONTROL Dataset activity]** pagina toont informatie over de doeldataset u selecteerde, met inbegrip van details over zijn partijstatus, dataset identiteitskaart, en schema.

>[!IMPORTANT]
>
>Terwijl het schrappen van datasets voor andere bronschakelaars mogelijk is, wordt het momenteel niet gesteund voor de schakelaar van Gegevens van de Classificaties van Analytics. Neem contact op met de klantenservice van Adobe als u per ongeluk een gegevensset verwijdert.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensschakelaar van de Classificaties van Analytics gecreeerd die [!DNL Classifications] gegevens in [!DNL Platform] brengt. Zie de volgende documenten voor meer informatie over [!DNL Analytics] en [!DNL Classifications] gegevens:

* [Overzicht gegevensconnector Analyse](../../../../connectors/adobe-applications/analytics.md)
* [Verbinding met analysegegevens maken in de gebruikersinterface](./analytics.md)
* [Informatie over classificaties](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)