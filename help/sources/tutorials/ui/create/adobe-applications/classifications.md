---
keywords: Experience Platform;home;populaire onderwerpen; analyses;classificaties
description: Leer hoe u een Adobe Analytics-bronaansluiting voor de gebruikersinterface maakt om classificatiegegevens over te brengen naar Adobe Experience Platform.
solution: Experience Platform
title: Een Adobe Analytics Source Connection maken voor classificatiegegevens in de gebruikersinterface
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Een Adobe Analytics-bronverbinding maken voor classificatiegegevens in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een gegevensbronverbinding voor classificaties van Adobe Analytics in de gebruikersinterface voor het verzenden van classificatiegegevens naar Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaring te ontwikkelen en te ontwikkelen.

Voor de gegevensverbinding Analytics Classifications moeten uw gegevens zijn gemigreerd naar de nieuwe [!DNL Classifications] -infrastructuur van Adobe Analytics voordat ze kunnen worden gebruikt. Neem contact op met het accountteam van de Adobe om de migratiestatus van uw gegevens te bevestigen.

## Uw classificaties selecteren

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de bronwerkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden beschikbare bronnen weergegeven om binnenkomende verbindingen met te maken. Elke bronkaart bevat een optie waarmee u een nieuw account kunt configureren of gegevens kunt toevoegen aan een bestaand account.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Adobe applications]** de **[!UICONTROL Adobe Analytics]** -kaart en selecteer vervolgens **[!UICONTROL Add data]** om te gaan werken met Classificatiegegevens van Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

De stap **[!UICONTROL Analytics source add data]** wordt weergegeven. Selecteer **[!UICONTROL Classifications]** in de bovenste koptekst om een lijst met [!DNL Classifications] -gegevenssets weer te geven, inclusief informatie over de dimensie-id, de naam van de rapportsuite en de id van de rapportsuite.

Elke pagina bevat maximaal tien verschillende [!DNL Classifications] datasets waaruit u kunt kiezen. Selecteer **[!UICONTROL Next]** onder aan de pagina om naar meer opties te bladeren. In het rechterdeelvenster ziet u het totale aantal [!DNL Classifications] gegevenssets dat u hebt geselecteerd en hun namen. In dit deelvenster kunt u ook [!DNL Classifications] -gegevenssets verwijderen die u per ongeluk hebt geselecteerd of alle selecties wissen met één actie.

U kunt maximaal 30 verschillende [!DNL Classifications] datasets selecteren om in [!DNL Platform] over te brengen.

Nadat u de [!DNL Classifications] -gegevenssets hebt geselecteerd, selecteert u **[!UICONTROL Next]** rechtsboven op de pagina.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Uw classificaties bekijken

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de geselecteerde [!DNL Classifications] -gegevenssets kunt bekijken voordat deze worden gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het bronplatform en de status van de verbinding weer.
* **[!UICONTROL Data type]** - Geeft het aantal geselecteerde [!DNL Classifications] weer.
* **[!UICONTROL Scheduling]**: geeft de synchronisatiefrequentie voor [!DNL Classifications] -gegevens weer.

Nadat u de gegevensstroom hebt gereviseerd, klikt u op **[!UICONTROL Finish]** en laat u enige tijd over tot de gegevensstroom.

![](../../../../images/tutorials/create/classifications/review.png)

## Uw classificatiegegevens controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen. Selecteer in het scherm **[!UICONTROL Catalog]** de optie **[!UICONTROL Dataflows]** om een lijst weer te geven met bestaande stromen die zijn gekoppeld aan uw [!DNL Classifications] -account.

![](../../../../images/tutorials/create/classifications/dataflows.png)

Het scherm **[!UICONTROL Dataflows]** wordt weergegeven. Op deze pagina vindt u een lijst met gegevensstromen, inclusief informatie over hun naam, brongegevens en status van de gegevensstroom. Rechts is dit het deelvenster **[!UICONTROL Properties]** dat metagegevens bevat over de [!DNL Classifications] -gegevensstroom.

Selecteer de **[!UICONTROL Target dataset]** die u wilt openen.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

De **[!UICONTROL Dataset activity]** pagina toont informatie over de doeldataset u selecteerde, met inbegrip van details over zijn partijstatus, dataset identiteitskaart, en schema.

![](../../../../images/tutorials/create/classifications/dataset.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een connector voor gegevens van analytische classificaties gemaakt die [!DNL Classifications] gegevens in [!DNL Platform] plaatst. Zie de volgende documenten voor meer informatie over [!DNL Analytics] en [!DNL Classifications] gegevens:

* [Overzicht van de gegevensconnector Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Verbinding met analysegegevens maken in de gebruikersinterface](./analytics.md)
* [ Ongeveer classificaties ](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
