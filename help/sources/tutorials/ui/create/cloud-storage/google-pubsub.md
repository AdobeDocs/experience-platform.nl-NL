---
keywords: Experience Platform;home;populaire onderwerpen;Google PubSub;Google pubsub
solution: Experience Platform
title: Een Google PubSub-bronverbinding maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Leer hoe u een Google PubSub-bronconnector maakt via de gebruikersinterface van het Platform.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Een [!DNL Google PubSub]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Google PubSub] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Google PubSub] (hierna &quot;[!DNL PubSub]&quot; genoemd) met behulp van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Als u al een geldige [!DNL PubSub] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [vormend een dataflow](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Als u [!DNL PubSub] wilt verbinden met Platform, moet u een geldige waarde opgeven voor de volgende referenties:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `projectId` | De project-id die is vereist voor verificatie [!DNL PubSub]. |
| `credentials` | De referentie- of persoonlijke sleutel-id die is vereist voor verificatie [!DNL PubSub]. |

Zie het volgende [PubSub-verificatie](https://cloud.google.com/pubsub/docs/authentication)-document voor meer informatie over deze waarden. Als u de op rekening-gebaseerde authentificatie van de dienst gebruikt, zie [PubSub gids](https://cloud.google.com/docs/authentication/production#create_service_account) voor stappen op hoe te om uw geloofsbrieven te produceren.

>[!TIP]
>
>Als u de op rekening-gebaseerde authentificatie van de dienst gebruikt, zorg ervoor dat u voldoende gebruikerstoegang tot uw de dienstrekening hebt verleend en dat er geen extra witte ruimten in JSON zijn, wanneer het kopiëren en het kleven van uw geloofsbrieven.

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL PubSub]-account te koppelen aan het Platform.

## Uw [!DNL PubSub]-account aansluiten

In [Platform UI](https://platform.adobe.com), selecteer **[!UICONTROL Sources]** van de linkernavigatiebar om tot de [!UICONTROL Sources] werkruimte toegang te hebben. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer [!UICONTROL Cloud storage] onder de categorie **[!UICONTROL Google PubSub]** en selecteer **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/google-pubsub/catalog.png)

De pagina **[!UICONTROL Connect to Google PubSub]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL PubSub]-account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een naam, een optionele beschrijving en uw [!DNL PubSub] verificatiegegevens op het invoerformulier. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding gemaakt tussen uw [!DNL PubSub]-account en Platform. U kunt nu verdergaan naar de volgende zelfstudie en [een gegevensstroom configureren om streaminggegevens van uw cloudopslag naar Platform te brengen](../../dataflow/streaming/cloud-storage-streaming.md).
