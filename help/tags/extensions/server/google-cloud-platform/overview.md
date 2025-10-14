---
title: Google Cloud Platform Event Forwarding Extension
description: Deze Adobe Experience Platform-gebeurtenis die een extensie doorstuurt, verzendt Edge Network-gebeurtenissen naar het Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# [!DNL Google Cloud Platform] -gebeurtenis, extensie doorsturen

[[!DNL Google Cloud Platform] &#x200B;](https://cloud.google.com/) is een platform van de cloud gegevensverwerking dat een grote verscheidenheid van de diensten zoals gedistribueerde gegevensverwerking, gegevensbestandopslag, inhoudslevering, en software-as-a-dienst (SaaS) integratieservices voor het beheer van de klantenverhouding (CRM) en bedrijfs middelplanning (ERP) aanbiedt.

De [!DNL Google Cloud Platform] [&#x200B; gebeurtenis die &#x200B;](../../../ui/event-forwarding/overview.md) uitbreidingshefboomwerkingen [[!DNL Cloud Pub/Sub] &#x200B;](https://cloud.google.com/pubsub) door:sturen om gebeurtenissen van de Edge Network van Adobe Experience Platform naar [!DNL Google Cloud Platform] voor verdere verwerking te verzenden. Deze gids behandelt hoe te om de uitbreiding te installeren en zijn mogelijkheden in een gebeurtenis aan te wenden die regel door:sturen.

## Vereisten

Als u deze extensie wilt gebruiken, moet u een [!DNL Google Cloud Platform] -account hebben met een bestaand [!DNL Cloud Pub/Sub] -onderwerp. Als u geen reeds bestaand onderwerp hebt, zie de [[!DNL Google Cloud Platform] &#x200B;](https://cloud.google.com/pubsub/docs/create-topic) documentatie over het creëren van en het leiden van onderwerpen.

### Een geheim en een gegevenselement maken

Eerst, creeer een nieuwe `Google OAuth 2` [&#x200B; gebeurtenis door:sturen geheim &#x200B;](../../../ui/event-forwarding/secrets.md), die zal worden gebruikt om de verbinding aan uw rekening voor authentiek te verklaren terwijl het houden van de waarde veilig.

Daarna, [&#x200B; creeer een gegevenselement &#x200B;](../../../ui/managing-resources/data-elements.md#create-a-data-element) gebruikend de **[!UICONTROL Core]** uitbreiding en een **[!UICONTROL Secret]** type van gegevenselement om naar het `Google OAuth 2` geheim te verwijzen u enkel creeerde.

## De extensie [!DNL Google Cloud Platform] installeren en configureren {#install}

Om de uitbreiding te installeren, [&#x200B; creeer een gebeurtenis door:sturen bezit &#x200B;](../../../ui/event-forwarding/overview.md#properties) of kies een bestaand bezit in plaats daarvan uit te geven.

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie. Selecteer op het tabblad **[!UICONTROL Catalog]** **[!UICONTROL Install]** op de kaart voor de extensie [!DNL Google Cloud Platform] .

![&#x200B; de catalogus [!DNL Google Cloud Platform] uitbreiding het benadrukken installeert.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Voer in het configuratiescherm het geheim voor het gegevenselement dat u eerder hebt gemaakt in het veld **[!UICONTROL Access Token]** in. Het gegevenselement-geheim bevat uw [!DNL Google Cloud Platform] OAuth 2-token. Selecteer **[!UICONTROL Save]** wanneer u klaar bent.

![&#x200B; de [!DNL Google Cloud Platform] pagina van de uitbreidingsconfiguratie.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Een [!DNL Send Data to Cloud Pub/Sub] -regel maken {#tracking-rule}

Zodra de uitbreiding wordt geïnstalleerd, creeer een nieuwe gebeurtenis door:sturen [&#x200B; regel &#x200B;](../../../ui/managing-resources/rules.md) en vorm zijn voorwaarden zoals gewenst. Wanneer u de handelingen voor de regel configureert, selecteert u de extensie **[!UICONTROL Google Cloud Platform]** en vervolgens **[!UICONTROL Send Data to Cloud Pub/Sub]** voor het actietype.

![&#x200B; de mening van de actieconfiguratie voor [!UICONTROL Google Cloud Platform], met de benadrukte actie en [!UICONTROL Send Data to Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Topic] | Het onderwerp dat de gebeurtenissen van Gebeurtenis door:sturen zal ontvangen. De waarde moet de notatie `projects/{projectName}/topics/{topicName}` hebben. |
| [!UICONTROL Data] | Dit veld bevat de gegevens die in JSON-indeling naar het [!DNL Cloud Pub/Sub] -onderwerp moeten worden doorgestuurd.<br><br> onder de **[!UICONTROL Raw]** optie, kunt u het voorwerp JSON in het verstrekte tekstgebied direct kleven, of u kunt het pictogram van het gegevenselement (![&#x200B; pictogram Dataset &#x200B;](/help/images/icons/database.png)) selecteren uit een lijst van bestaande gegevenselementen om de gegevens te vertegenwoordigen.<br><br> u kunt de **[!UICONTROL JSON Key-Value Pairs Editor]** optie ook gebruiken om elk zeer belangrijk-waardepaar door een redacteur manueel toe te voegen UI. Elke waarde kan worden vertegenwoordigd door een onbewerkte invoer, maar in plaats daarvan kan ook een gegevenselement worden geselecteerd. |
| [!UICONTROL Attributes] | Dit veld bevat het JSON-object met extra kenmerken die samen met het bericht moeten worden verzonden.<br><br> onder de **[!UICONTROL Raw]** optie, kunt u het voorwerp JSON in het verstrekte tekstgebied direct kleven, of u kunt het pictogram van het gegevenselement (![&#x200B; pictogram Dataset &#x200B;](/help/images/icons/database.png)) selecteren uit een lijst van bestaande gegevenselementen om de gegevens te vertegenwoordigen.<br><br> u kunt de **[!UICONTROL JSON Key-Value Pairs Editor]** optie ook gebruiken om elk zeer belangrijk-waardepaar door een redacteur manueel toe te voegen UI. Elke waarde kan worden vertegenwoordigd door een onbewerkte invoer, maar in plaats daarvan kan ook een gegevenselement worden geselecteerd. |

{style="table-layout:auto"}

## Volgende stappen

In deze handleiding wordt uitgelegd hoe u gegevens naar [!DNL Cloud Pub/Sub] kunt verzenden met behulp van de [!DNL Google Cloud Platform] -extensie voor het doorsturen van gebeurtenissen. Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar de [&#x200B; gebeurtenis die overzicht &#x200B;](../../../ui/event-forwarding/overview.md) door:sturen.
