---
title: Google Cloud Platform Event Forwarding Extension
description: Deze Adobe Experience Platform-extensie voor het doorsturen van gebeurtenissen verzendt Adobe Experience Edge Network-gebeurtenissen naar Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: d1a34a98efd24a20dc53544eeb0d79490aaf31e7
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# [!DNL Google Cloud Platform] extensie voor doorsturen van gebeurtenissen

[[!DNL Google Cloud Platform]](https://cloud.google.com/) is een platform voor cloud computing dat een groot aantal verschillende services biedt, zoals gedistribueerde computers, databaseopslag, levering van inhoud en SAA-integratieservices (software-as-a-service) voor relatiebeheer voor klanten (CRM) en planning van bedrijfsmiddelen (ERP).

De [!DNL Google Cloud Platform] [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) extensiefuncties [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) om gebeurtenissen vanaf Adobe Experience Platform Edge Network naar de [!DNL Google Cloud Platform] voor verdere verwerking. Deze gids behandelt hoe te om de uitbreiding te installeren en zijn mogelijkheden in een gebeurtenis aan te wenden die regel door:sturen.

## Vereisten

Als u deze extensie wilt gebruiken, moet u beschikken over een [!DNL Google Cloud Platform] met een bestaande [!DNL Cloud Pub/Sub] onderwerp. Als u geen reeds bestaande gegevensstroom hebt, zie [!DNL AWS] documentatie over [een nieuwe gegevensstroom maken met de [!DNL AWS] Beheerconsole](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

### Een geheim en een gegevenselement maken

Maak eerst een nieuwe `Google OAuth 2` [gebeurtenis die geheim door:sturen](../../../ui/event-forwarding/secrets.md), die wordt gebruikt om de verbinding met uw account te verifiëren en de waarde veilig te houden.

Volgende, [een gegevenselement maken](../../../ui/managing-resources/data-elements.md#create-a-data-element) met de **[!UICONTROL Core]** en **[!UICONTROL Secret]** het elementtype van gegevens om naar `Google OAuth 2` geheim dat je zojuist hebt gemaakt.

## Installeer en configureer de [!DNL Google Cloud Platform] extension {#install}

Als u de extensie wilt installeren, [een eigenschap voor het doorsturen van gebeurtenissen maken](../../../ui/event-forwarding/overview.md#properties) of kies een bestaande eigenschap die u wilt bewerken.

Selecteren **[!UICONTROL Extensions]** in de linkernavigatie. In de **[!UICONTROL Catalog]** tab, selecteert u **[!UICONTROL Install]** op de kaart voor de [!DNL Google Cloud Platform] extensie.

![De catalogus [!DNL Google Cloud Platform] installatie van markering voor extensie.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Voor het configuratiescherm, ga het geheim van het gegevenselement in dat u vroeger in het **[!UICONTROL Access Token]** veld. Het gegevenselementgeheim bevat uw [!DNL Google Cloud Platform] OAuth 2 token. Selecteren **[!UICONTROL Save]** wanneer gereed.

![De [!DNL Google Cloud Platform] extensieconfiguratiepagina.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Een [!DNL Send Data to Cloud Pub/Sub] regel {#tracking-rule}

Zodra de uitbreiding wordt geïnstalleerd, creeer een nieuwe gebeurtenis door:sturen [regel](../../../ui/managing-resources/rules.md) en configureer de voorwaarden naar wens. Wanneer het vormen van de acties voor de regel, selecteer **[!UICONTROL Google Cloud Platform]** extensie selecteert u vervolgens **[!UICONTROL Send Data to Cloud Pub/Sub]** voor het actietype.

![De mening van de actieconfiguratie voor [!UICONTROL Google Cloud Platform], met de actie gemarkeerd en [!UICONTROL Send Data to Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Topic] | Het onderwerp dat de gebeurtenissen van Gebeurtenis door:sturen zal ontvangen. De waarde moet de notatie hebben `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Data] | Dit veld bevat de gegevens die naar de [!DNL Cloud Pub/Sub] in JSON-indeling.<br><br>Onder de **[!UICONTROL Raw]** kunt u het JSON-object rechtstreeks in het opgegeven tekstveld plakken of het pictogram voor het gegevenselement selecteren (![Dataset-pictogram](../../../images/extensions/server/aws/data-element-icon.png)) om de gegevens te selecteren in een lijst met bestaande gegevenselementen.<br><br>U kunt ook de opdracht **[!UICONTROL JSON Key-Value Pairs Editor]** optie om elk zeer belangrijk-waardepaar door een redacteur manueel toe te voegen UI. Elke waarde kan worden vertegenwoordigd door een onbewerkte invoer, maar er kan ook een gegevenselement worden geselecteerd. |
| [!UICONTROL Attributes] | Dit veld bevat het JSON-object met extra kenmerken die samen met het bericht moeten worden verzonden.<br><br>Onder de **[!UICONTROL Raw]** kunt u het JSON-object rechtstreeks in het opgegeven tekstveld plakken of het pictogram voor het gegevenselement selecteren (![Dataset-pictogram](../../../images/extensions/server/aws/data-element-icon.png)) om de gegevens te selecteren in een lijst met bestaande gegevenselementen.<br><br>U kunt ook de opdracht **[!UICONTROL JSON Key-Value Pairs Editor]** optie om elk zeer belangrijk-waardepaar door een redacteur manueel toe te voegen UI. Elke waarde kan worden vertegenwoordigd door een onbewerkte invoer, maar er kan ook een gegevenselement worden geselecteerd. |

{style="table-layout:auto"}

## Volgende stappen

In deze handleiding wordt uitgelegd hoe u gegevens kunt verzenden naar [!DNL Cloud Pub/Sub] met de [!DNL Google Cloud Platform] gebeurtenis die uitbreiding door:sturen. Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar [overzicht van gebeurtenissen doorsturen](../../../ui/event-forwarding/overview.md).