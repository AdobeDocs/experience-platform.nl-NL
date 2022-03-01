---
keywords: Experience Platform;home;populaire onderwerpen;Google PubSub;Google pubsub
solution: Experience Platform
title: Een Google PubSub-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Google PubSub-bronconnector maakt via de gebruikersinterface van het Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: da7b6fe8f9d274b8e5f27138a1baf8caf63a0c01
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# Een [!DNL Google PubSub] bronverbinding in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Google PubSub] (hierna &quot;[!DNL PubSub]&quot;) gebruiken van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Als u al een geldige [!DNL PubSub] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Om verbinding te maken [!DNL PubSub] aan Platform, moet u een geldige waarde voor de volgende geloofsbrieven verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `projectId` | De project-id die is vereist voor verificatie [!DNL PubSub]. |
| `credentials` | De referentie- of persoonlijke sleutel-id die is vereist voor verificatie [!DNL PubSub]. |

Raadpleeg de volgende secties voor meer informatie over deze waarden [PubSub-verificatie](https://cloud.google.com/pubsub/docs/authentication) document. Als u de dienst op rekening-gebaseerde authentificatie gebruikt, zie het volgende [PubSub-hulplijn](https://cloud.google.com/docs/authentication/production#create_service_account) voor stappen over hoe te om uw geloofsbrieven te produceren.

>[!TIP]
>
>Als u de op rekening-gebaseerde authentificatie van de dienst gebruikt, zorg ervoor dat u voldoende gebruikerstoegang tot uw de dienstrekening hebt verleend en dat er geen extra witte ruimten in JSON zijn, wanneer het kopiëren en het kleven van uw geloofsbrieven.

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL PubSub] aan Platform.

## Verbind uw [!DNL PubSub] account

In de [UI Platform](https://platform.adobe.com), selecteert u **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Cloud storage] categorie, selecteert u **[!UICONTROL Google PubSub]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/google-pubsub/catalog.png)

De **[!UICONTROL Connect to Google PubSub]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL PubSub] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam, een optionele beschrijving en uw [!DNL PubSub] verificatiereferenties op het invoerformulier. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding gemaakt tussen uw [!DNL PubSub] account en Platform. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om streaminggegevens van uw cloudopslag naar Platform te brengen](../../dataflow/streaming/cloud-storage-streaming.md).
