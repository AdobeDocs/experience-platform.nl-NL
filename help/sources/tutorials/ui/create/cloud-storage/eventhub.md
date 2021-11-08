---
keywords: Experience Platform;home;populaire onderwerpen;Azure Event Hubs;Event Hubs;azure-gebeurtenishubs
solution: Experience Platform
title: Een Azure Event Hubs Source Connection in de UI maken
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Azure Event Hubs-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 855b6414981c6d7ee79bc674e5a4087dd79dde5b
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Een [!DNL Azure Event Hubs] bronverbinding in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Azure Event Hubs] (hierna &quot;[!DNL Event Hubs]&quot;) bronaansluiting met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Event Hubs] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/streaming/cloud-storage-streaming.md).

### Vereiste referenties verzamelen

Om uw [!DNL Event Hubs] bronaansluiting, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `sasKey` | De primaire sleutel van de [!DNL Event Hubs] naamruimte. De `sasPolicy` de `sasKey` komt overeen met `manage` rechten die zijn geconfigureerd voor de [!DNL Event Hubs] in te vullen lijst. |
| `namespace` | De naamruimte van de [!DNL Event Hubs] u hebt toegang. |

Zie voor meer informatie over deze waarden [dit [!DNL Event Hubs] document](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Verbind uw [!DNL Event Hubs] account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Event Hubs] account aan [!DNL Platform].

Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de **[!UICONTROL Sources]** werkruimte. De **[!UICONTROL Catalog]** bevat diverse bronnen waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Cloud Storage]** categorie, selecteert u **[!UICONTROL Azure Event Hubs]**. Als dit de eerste keer is met deze connector, selecteert u **[!UICONTROL Configure]**. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe schakelaar van de Hubs van de Gebeurtenis tot stand te brengen.

![](../../../../images/tutorials/create/eventhub/catalog.png)

De **[!UICONTROL Connect to Azure Event Hubs]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New Account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Event Hubs] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![](../../../../images/tutorials/create/eventhub/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de optie [!DNL Event Hubs] account waarmee u verbinding wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u verbinding gemaakt met uw [!DNL Event Hubs] account aan [!DNL Platform]. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag over te brengen naar [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
