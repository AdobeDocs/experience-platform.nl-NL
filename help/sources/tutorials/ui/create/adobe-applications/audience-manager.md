---
keywords: Experience Platform;huis;populaire onderwerpen;de bronschakelaar van de manager van het publiek;Audience Manager;de schakelaar van de publieksmanager
title: Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface
description: Deze zelfstudie begeleidt u door de stappen om een bronverbinding voor Adobe Audience Manager tot stand te brengen om de gegevens van de Gebeurtenis van de Consumentenervaring in Platform te brengen gebruikend het gebruikersinterface.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 90a917ea2b623079f26c67b776dd46b62531c7da
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface

Deze zelfstudie begeleidt u door de stappen om een bronschakelaar voor Adobe Audience Manager tot stand te brengen om de gegevens van de Gebeurtenis van de Consumentenervaring in Platform te brengen gebruikend het gebruikersinterface.

## Een bronverbinding maken met Adobe Audience Manager

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder [!UICONTROL Adobe Application], selecteert u **[!UICONTROL Adobe Audience Manager]** en selecteer vervolgens **[!UICONTROL Set up]**.

![catalogus](../../../../images/tutorials/create/aam/catalog.png)

### Kenmerken en segmenten selecteren

>[!NOTE]
>
>U kunt geen regionale gegevens van de bron van de Audience Manager aan Experience Platform opnemen. Als u beschikt over gevallen waarin Analytics regionale gegevens vereist, gebruikt u de [Bronconnector voor analyse](../adobe-applications/analytics.md).

De [!UICONTROL Select traits and segments] de stap verschijnt, die u van een interactieve interface voorzien om uw eigenschappen, segmenten, en gegevens te onderzoeken en te selecteren.

* Het linkerpaneel van de interface bevat het [!UICONTROL Select traits and segments] en een hiërarchische map met alle segmenten die voor u beschikbaar zijn.
* De juiste helft van de interface staat u toe om met geselecteerde segmenten in wisselwerking te staan en door specifieke gegevens te kiezen u wilt gebruiken.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Als u door beschikbare segmenten wilt navigeren, selecteert u de map die u wilt openen in het dialoogvenster [!UICONTROL All Segments] deelvenster. Als u een map selecteert, kunt u de hiërarchie van een map doorlopen en krijgt u een lijst met segmenten om door te filteren.

![segmentmap](../../../../images/tutorials/create/aam/segment-folder.png)

Nadat u de gewenste segmenten hebt geïdentificeerd en geselecteerd, wordt aan de rechterkant een nieuw deelvenster weergegeven met de lijst met geselecteerde items. U kunt tot verschillende omslagen blijven toegang hebben en verschillende segmenten voor uw verbinding selecteren. Als u meer segmenten selecteert, wordt het deelvenster aan de rechterkant bijgewerkt.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

U kunt ook de **[!UICONTROL Select all segments]** en **[!UICONTROL Select all traits]** vakken. Het selecteren van alle segmenten zal de segmenten van de Audience Manager aan Platform brengen, terwijl het selecteren van alle eigenschappen alle eerste partijsporen van Audience Manager toelaat.

Als u klaar bent, selecteert u **[!UICONTROL Next]**

![alle segmenten](../../../../images/tutorials/create/aam/all-segments.png)

De [!UICONTROL Review] wordt weergegeven, zodat u de geselecteerde kenmerken en segmenten kunt bekijken voordat ze met het Platform worden verbonden. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Toont het bronplatform en de status van de verbinding.
* **[!UICONTROL Selected data]**: Hiermee geeft u het aantal geselecteerde segmenten en de ingeschakelde kenmerken weer.

![revisie](../../../../images/tutorials/create/aam/review.png)

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

## Volgende stappen

Terwijl een gegevensstroom van de Audience Manager actief is, worden de inkomende gegevens automatisch opgenomen in de Profielen van de Klant in real time. U kunt deze inkomende gegevens nu gebruiken en publiekssegmenten maken met de Dienst van de Segmentatie van het Platform. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../../profile/home.md)
* [Overzicht van segmentatieservice](../../../../../segmentation/home.md)
