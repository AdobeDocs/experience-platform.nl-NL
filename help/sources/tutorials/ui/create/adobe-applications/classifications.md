---
keywords: Experience Platform;thuis;populaire onderwerpen; analyses;classificaties
description: Leer hoe u een Adobe Analytics-bronaansluiting voor de gebruikersinterface maakt om classificatiegegevens over te brengen naar Adobe Experience Platform.
solution: Experience Platform
title: Een Adobe Analytics-bronverbinding maken voor classificatiegegevens in de gebruikersinterface
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Een Adobe Analytics-bronverbinding maken voor classificatiegegevens in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een gegevensbronverbinding voor classificaties van Adobe Analytics in de gebruikersinterface voor het verzenden van classificatiegegevens naar Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Voor de gegevensverbinding Analytics Classifications moeten uw gegevens zijn gemigreerd naar de nieuwe [!DNL Classifications] infrastructuur van Adobe Analytics vóór gebruik. Neem contact op met uw Adobe-accountteam om de migratiestatus van uw gegevens te bevestigen.

## Uw classificaties selecteren

Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte Bronnen te openen. De **[!UICONTROL Catalog]** het scherm toont beschikbare bronnen om binnenkomende verbindingen met tot stand te brengen. Elke bronkaart bevat een optie waarmee u een nieuw account kunt configureren of gegevens kunt toevoegen aan een bestaand account.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Adobe applications]** categorie selecteert u de categorie **[!UICONTROL Adobe Analytics]** en selecteer vervolgens **[!UICONTROL Add data]** om te gaan werken met gegevens van analytische classificaties.

![](../../../../images/tutorials/create/classifications/catalog.png)

De **[!UICONTROL Analytics source add data]** wordt weergegeven. Selecteren **[!UICONTROL Classifications]** in de bovenste koptekst om een lijst met [!DNL Classifications] datasets, met inbegrip van informatie over hun afmeting ID, de naam van de rapportreeks, en identiteitskaart van de rapportreeks.

Elke pagina wordt weergegeven met tien verschillende [!DNL Classifications] gegevenssets waaruit u kunt kiezen. Selecteren **[!UICONTROL Next]** onder aan de pagina om naar meer opties te bladeren. In het rechterdeelvenster wordt het totale aantal [!DNL Classifications] datasets die u hebt geselecteerd, en hun namen. In dit deelvenster kunt u ook [!DNL Classifications] de datasets u door fout hebt geselecteerd of alle selecties met één actie ontruimen.

U kunt maximaal 30 verschillende opties selecteren [!DNL Classifications] gegevenssets die moeten worden ingevoerd [!DNL Platform].

Als u eenmaal uw [!DNL Classifications] datasets, selecteren **[!UICONTROL Next]** rechtsboven op de pagina.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Uw classificaties bekijken

De **[!UICONTROL Review]** wordt weergegeven, zodat u de geselecteerde [!DNL Classifications] datasets alvorens het wordt gecreeerd. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Toont het bronplatform en de status van de verbinding.
* **[!UICONTROL Data type]**: Hiermee geeft u het aantal geselecteerde items weer [!DNL Classifications].
* **[!UICONTROL Scheduling]**: Geeft de synchronisatiefrequentie voor [!DNL Classifications] gegevens.

Nadat u de gegevensstroom hebt gecontroleerd, klikt u op **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![](../../../../images/tutorials/create/classifications/review.png)

## Uw classificatiegegevens controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen. Van de **[!UICONTROL Catalog]** scherm, selecteren **[!UICONTROL Dataflows]** om een lijst weer te geven met bestaande stromen die zijn gekoppeld aan uw [!DNL Classifications] account.

![](../../../../images/tutorials/create/classifications/dataflows.png)

De **[!UICONTROL Dataflows]** wordt weergegeven. Op deze pagina vindt u een lijst met gegevensstromen, inclusief informatie over hun naam, brongegevens en status van de gegevensstroom. Rechts is het **[!UICONTROL Properties]** deelvenster dat metagegevens bevat voor uw [!DNL Classifications] dataflow.

Selecteer **[!UICONTROL Target dataset]** u wenst toegang te hebben.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

De **[!UICONTROL Dataset activity]** De pagina toont informatie over de doeldataset u selecteerde, met inbegrip van details over zijn partijstatus, dataset identiteitskaart, en schema.

>[!IMPORTANT]
>
>Terwijl het schrappen van datasets voor andere bronschakelaars mogelijk is, wordt het momenteel niet gesteund voor de schakelaar van Gegevens van de Classificaties van Analytics. Neem contact op met de klantenservice van Adobe als u per ongeluk een gegevensset verwijdert.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Volgende stappen

Door deze zelfstudie te volgen hebt u een gegevensconnector voor Analytics Classifications gemaakt die [!DNL Classifications] gegevens in [!DNL Platform]. Zie de volgende documenten voor meer informatie over [!DNL Analytics] en [!DNL Classifications] gegevens:

* [Overzicht gegevensconnector Analyse](../../../../connectors/adobe-applications/analytics.md)
* [Verbinding met analysegegevens maken in de gebruikersinterface](./analytics.md)
* [Informatie over classificaties](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
