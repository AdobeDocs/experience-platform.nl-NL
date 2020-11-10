---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;Event Hubs;azure event hubs
solution: Experience Platform
title: Creeer een Azure de bronschakelaar van de Hubs van de Gebeurtenis in UI
topic: overview
type: Tutorial
description: Deze zelfstudie biedt stappen voor het verifiëren van een Azure Event Hubs-bronconnector (hierna "Event Hubs" genoemd) die de gebruikersinterface van het Platform gebruikt.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---


# Creeer een [!DNL Azure Event Hubs] bronschakelaar in UI

>[!NOTE]
>
> De [!DNL Azure Event Hubs] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Azure Event Hubs] (hierna &quot;[!DNL Event Hubs]&quot; genoemd) bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Event Hubs] verbinding hebt, kunt u de rest van dit document overslaan en verdergaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/streaming/cloud-storage-streaming.md).

### Vereiste referenties verzamelen

Om uw [!DNL Event Hubs] bronschakelaar voor authentiek te verklaren, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `sasKey` | De gegenereerde handtekening voor gedeelde toegang. |
| `namespace` | De naamruimte van het object [!DNL Event Hubs] dat u opent. |

Raadpleeg dit document voor meer informatie over deze waarden [ [!DNL Event Hubs] ](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Uw [!DNL Event Hubs] account verbinden

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Event Hubs] account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Bronnen]** . Op het tabblad **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Cloud Storage]** de optie **[!UICONTROL Azure Event Hubs]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders, uitgezochte **[!UICONTROL voeg gegevens]** toe om een nieuwe schakelaar van de Hubs van de Gebeurtenis tot stand te brengen.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Het dialoogvenster **[!UICONTROL Connect to Azure Event Hubs]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Event Hubs] referenties in. Wanneer u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/eventhub/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Event Hubs] account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u verbinding met uw [!DNL Event Hubs] account [!DNL Platform]. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag naar [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md)te brengen.