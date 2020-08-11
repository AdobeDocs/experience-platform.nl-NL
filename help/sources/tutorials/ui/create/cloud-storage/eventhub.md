---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een Azure de bronschakelaar van de Hubs van de Gebeurtenis in UI
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---


# Creeer een [!DNL Azure Event Hubs] bronschakelaar in UI

>[!NOTE]
> De [!DNL Azure Event Hubs] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Azure Event Hubs] (hierna &quot;[!DNL Event Hubs]&quot; genoemd) bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een [!DNL Event Hubs] account hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/streaming/cloud-storage.md).

### Vereiste referenties verzamelen

Om uw [!DNL Event Hubs] bronschakelaar voor authentiek te verklaren, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `sasKey` | De gegenereerde handtekening voor gedeelde toegang. |
| `namespace` | De naamruimte van het object [!DNL Event Hubs] dat u opent. |

Raadpleeg [dit Event Hubs-document](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)voor meer informatie over deze waarden.

## Uw [!DNL Event Hubs] account verbinden

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Event Hubs] account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . Op het tabblad *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven waarmee u verbinding kunt maken [!DNL Platform]. Elke bron toont het aantal bestaande rekeningen verbonden aan hen.

Selecteer onder de categorie *[!UICONTROL Cloud Storage]* de optie **[!UICONTROL Azure Event Hubs]** gevolgd door gegevens **** toevoegen om een nieuwe Event Hubs-connector te maken.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Het dialoogvenster *[!UICONTROL Connect to Azure Event Hubs]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Voor de inputvorm die verschijnt, verstrek een naam, een facultatieve beschrijving, en uw geloofsbrieven van de Hubs van de Gebeurtenis. Wanneer u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/eventhub/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Event Hubs-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u uw rekening van de Hubs van de Gebeurtenis met verbonden [!DNL Platform]. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag naar het Platform](../../dataflow/streaming/cloud-storage.md)te brengen.