---
keywords: Experience Platform;huis;populaire onderwerpen;de bronschakelaar van de manager van het publiek;Audience Manager;de schakelaar van de publieksmanager
title: Een Adobe Audience Manager Source Connection maken in de gebruikersinterface
description: Deze zelfstudie begeleidt u door de stappen om een bronverbinding voor Adobe Audience Manager tot stand te brengen om de gegevens van de Gebeurtenis van de Consumentenervaring in Platform in te brengen gebruikend het gebruikersinterface.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Een Adobe Audience Manager-bronverbinding maken in de gebruikersinterface

Deze zelfstudie begeleidt u door de stappen om een bronschakelaar voor Adobe Audience Manager tot stand te brengen om de gegevens van de Gebeurtenis van de Consumentenervaring in Platform in te brengen gebruikend het gebruikersinterface.

## Een bronverbinding maken met Adobe Audience Manager

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer onder [!UICONTROL Adobe Application] de optie **[!UICONTROL Adobe Audience Manager]** en selecteer vervolgens **[!UICONTROL Set up]** .

![ catalogus ](../../../../images/tutorials/create/aam/catalog.png)

### Kenmerken en segmenten selecteren

>[!NOTE]
>
>U kunt geen regionale gegevens van de bron van de Audience Manager aan Experience Platform opnemen. Als u Analytics gebruiksgevallen hebt die regionale gegevens vereisen, dan gelieve te gebruiken de [ bron van Analytics schakelaar ](../adobe-applications/analytics.md).

De stap [!UICONTROL Select traits and segments] verschijnt, die u van een interactieve interface voorzien om uw eigenschappen, segmenten, en gegevens te onderzoeken en te selecteren.

* Het linkerdeelvenster van de interface bevat de [!UICONTROL Select traits and segments] -opties en een hiërarchische map met alle segmenten die voor u beschikbaar zijn.
* De juiste helft van de interface staat u toe om met geselecteerde segmenten in wisselwerking te staan en door specifieke gegevens te kiezen u wilt gebruiken.

![ toe:voegen-gegevens ](../../../../images/tutorials/create/aam/add-data.png)

Als u door beschikbare segmenten wilt navigeren, selecteert u in het deelvenster [!UICONTROL All Segments] de map die u wilt openen. Als u een map selecteert, kunt u de hiërarchie van een map doorlopen en krijgt u een lijst met segmenten om door te filteren.

![ segment-omslag ](../../../../images/tutorials/create/aam/segment-folder.png)

Nadat u de gewenste segmenten hebt geïdentificeerd en geselecteerd, wordt aan de rechterkant een nieuw deelvenster weergegeven met de lijst met geselecteerde items. U kunt tot verschillende omslagen blijven toegang hebben en verschillende segmenten voor uw verbinding selecteren. Als u meer segmenten selecteert, wordt het deelvenster aan de rechterkant bijgewerkt.

![ selecteren-gegevens ](../../../../images/tutorials/create/aam/select-data.png)

U kunt ook de vakken **[!UICONTROL Select all segments]** en **[!UICONTROL Select all traits]** selecteren. Het selecteren van alle segmenten zal de segmenten van de Audience Manager aan Platform brengen, terwijl het selecteren van alle eigenschappen alle eerste partijsporen van Audience Manager toelaat.

>[!WARNING]
>
>De inname van grote populaties van het segment van de Audience Manager heeft een directe invloed op uw totale profieltelling wanneer u eerst een segment van de Audience Manager naar Platform verzendt gebruikend de bron van de Audience Manager. Dit betekent dat het selecteren van alle segmenten kan leiden tot een aantal profielen dat groter is dan uw gebruiksrechten voor licenties. Gelieve te herzien uw [ gebruikstoelage van de vergunning ](../../../../../dashboards/guides/license-usage.md) alvorens te werk te gaan.

Selecteer **[!UICONTROL Next]** wanneer u klaar bent

![ alle-segmenten ](../../../../images/tutorials/create/aam/all-segments.png)

De stap [!UICONTROL Review] wordt weergegeven, zodat u de geselecteerde kenmerken en segmenten kunt bekijken voordat ze worden verbonden met Platform. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het bronplatform en de status van de verbinding weer.
* **[!UICONTROL Selected data]** - Geeft het aantal geselecteerde segmenten en de ingeschakelde kenmerken weer.

![ overzicht ](../../../../images/tutorials/create/aam/review.png)

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over om de gegevensstroom te maken.

## Volgende stappen

Terwijl een gegevensstroom van de Audience Manager actief is, worden de inkomende gegevens automatisch opgenomen in de Profielen van de Klant in real time. U kunt deze inkomende gegevens nu gebruiken en publiekssegmenten maken met de Platform Segmentation Service. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../../profile/home.md)
* [Overzicht van segmentatieservice](../../../../../segmentation/home.md)
