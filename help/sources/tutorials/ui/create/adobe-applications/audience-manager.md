---
keywords: Experience Platform;huis;populaire onderwerpen;de bronschakelaar van de manager van het publiek;Audience Manager;de schakelaar van de publieksmanager
solution: Experience Platform
title: Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Deze zelfstudie begeleidt u door de stappen om een bronschakelaars voor Adobe Audience Manager tot stand te brengen om de gegevens van de Gebeurtenis van de Consumentenervaring in Platform te brengen gebruikend het gebruikersinterface.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface

Deze zelfstudie begeleidt u door de stappen om een bronschakelaar voor Adobe Audience Manager tot stand te brengen om de gegevens van de Gebeurtenis van de Consumentenervaring in Platform te brengen gebruikend het gebruikersinterface.

## Een bronverbinding maken met Adobe Audience Manager

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte [!UICONTROL Bronnen] te openen. Het scherm [!UICONTROL Catalog] toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen met.

Selecteer **[!UICONTROL Adobe Audience Manager]** onder de categorie [!UICONTROL Adobe toepassingen] en selecteer **[!UICONTROL Configure]**.

![catalogus](../../../../images/tutorials/create/aam/catalog.png)

De stap [!UICONTROL Selecteer kenmerken en segmenten] verschijnt, die u van een interactieve interface voorzien om uw eigenschappen, segmenten, en gegevens te onderzoeken en te selecteren.

* Het linkerpaneel van de interface bevat [!UICONTROL Uitgezochte eigenschappen en segmenten] opties, evenals een hiërarchische folder van alle segmenten beschikbaar aan u.
* De juiste helft van de interface staat u toe om met geselecteerde segmenten in wisselwerking te staan en door specifieke gegevens te kiezen u wilt gebruiken.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Als u door beschikbare segmenten wilt navigeren, selecteert u de map die u wilt openen in het deelvenster [!UICONTROL Alle segmenten]. Als u een map selecteert, kunt u de hiërarchie van een map doorlopen en krijgt u een lijst met segmenten om door te filteren.

![segmentmap](../../../../images/tutorials/create/aam/segment-folder.png)

Nadat u de gewenste segmenten hebt geïdentificeerd en geselecteerd, wordt aan de rechterkant een nieuw deelvenster weergegeven met de lijst met geselecteerde items. U kunt tot verschillende omslagen blijven toegang hebben en verschillende segmenten voor uw verbinding selecteren. Als u meer segmenten selecteert, wordt het deelvenster aan de rechterkant bijgewerkt.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

U kunt ook de vakken **[!UICONTROL Alle segmenten]** en **[!UICONTROL Alle kenmerken selecteren]** selecteren. Het selecteren van alle segmenten zal de segmenten van de Audience Manager aan Platform brengen, terwijl het selecteren van alle eigenschappen alle eerste partijsporen van Audience Manager toelaat.

Als u klaar bent, selecteert u **[!UICONTROL Volgende]**

![alle segmenten](../../../../images/tutorials/create/aam/all-segments.png)

De stap [!UICONTROL Revisie] wordt weergegeven, zodat u de geselecteerde kenmerken en segmenten kunt bekijken voordat ze met het Platform worden verbonden. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Verbinding]**: Toont het bronplatform en de status van de verbinding.
* **[!UICONTROL Geselecteerde gegevens]**: Hiermee geeft u het aantal geselecteerde segmenten en de ingeschakelde kenmerken weer.

![revisie](../../../../images/tutorials/create/aam/review.png)

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Voltooien]** en laat u enige tijd over tot de gegevensstroom.

## Volgende stappen

Terwijl een gegevensstroom van de Audience Manager actief is, worden de inkomende gegevens automatisch opgenomen in de Profielen van de Klant in real time. U kunt deze inkomende gegevens nu gebruiken en publiekssegmenten maken met de Dienst van de Segmentatie van het Platform. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../../profile/home.md)
* [Overzicht van segmentatieservice](../../../../../segmentation/home.md)