---
keywords: Experience Platform;huis;populaire onderwerpen;de bronschakelaar van de manager van het publiek;Audience Manager;de schakelaar van de publieksmanager
solution: Experience Platform
title: Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Deze zelfstudie begeleidt u door de stappen om een bronschakelaars voor Adobe Audience Manager tot stand te brengen om de gegevens van de Gebeurtenis van de Consumentenervaring in Platform te brengen gebruikend het gebruikersinterface.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface

Deze zelfstudie begeleidt u door de stappen om een bronschakelaar voor Adobe Audience Manager tot stand te brengen om de gegevens van de Gebeurtenis van de Consumentenervaring in Platform te brengen gebruikend het gebruikersinterface.

## Een bronverbinding maken met Adobe Audience Manager

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte [!UICONTROL Sources] te openen. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

Selecteer [!UICONTROL Adobe applications] onder de categorie **[!UICONTROL Adobe Audience Manager]** en selecteer **[!UICONTROL Configure]**.

![catalogus](../../../../images/tutorials/create/aam/catalog.png)

De stap [!UICONTROL Select traits and segments] verschijnt, die u van een interactieve interface voorzien om uw eigenschappen, segmenten, en gegevens te onderzoeken en te selecteren.

* Het linkerpaneel van de interface bevat de [!UICONTROL Select traits and segments] opties, evenals een hiërarchische folder van alle segmenten beschikbaar aan u.
* De juiste helft van de interface staat u toe om met geselecteerde segmenten in wisselwerking te staan en door specifieke gegevens te kiezen u wilt gebruiken.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Om door beschikbare segmenten te navigeren, selecteer de omslag u van het [!UICONTROL All Segments] paneel wilt toegang hebben. Als u een map selecteert, kunt u de hiërarchie van een map doorlopen en krijgt u een lijst met segmenten om door te filteren.

![segmentmap](../../../../images/tutorials/create/aam/segment-folder.png)

Nadat u de gewenste segmenten hebt geïdentificeerd en geselecteerd, wordt aan de rechterkant een nieuw deelvenster weergegeven met de lijst met geselecteerde items. U kunt tot verschillende omslagen blijven toegang hebben en verschillende segmenten voor uw verbinding selecteren. Als u meer segmenten selecteert, wordt het deelvenster aan de rechterkant bijgewerkt.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

U kunt ook de vakken **[!UICONTROL Select all segments]** en **[!UICONTROL Select all traits]** selecteren. Het selecteren van alle segmenten zal de segmenten van de Audience Manager aan Platform brengen, terwijl het selecteren van alle eigenschappen alle eerste partijsporen van Audience Manager toelaat.

Als u klaar bent, selecteert u **[!UICONTROL Next]**

![alle segmenten](../../../../images/tutorials/create/aam/all-segments.png)

De stap [!UICONTROL Review] wordt weergegeven, zodat u de geselecteerde kenmerken en segmenten kunt bekijken voordat ze met het Platform worden verbonden. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Toont het bronplatform en de status van de verbinding.
* **[!UICONTROL Selected data]**: Hiermee geeft u het aantal geselecteerde segmenten en de ingeschakelde kenmerken weer.

![revisie](../../../../images/tutorials/create/aam/review.png)

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over om de gegevensstroom te maken.

## Volgende stappen

Terwijl een gegevensstroom van de Audience Manager actief is, worden de inkomende gegevens automatisch opgenomen in de Profielen van de Klant in real time. U kunt deze inkomende gegevens nu gebruiken en publiekssegmenten maken met de Dienst van de Segmentatie van het Platform. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../../profile/home.md)
* [Overzicht van segmentatieservice](../../../../../segmentation/home.md)
