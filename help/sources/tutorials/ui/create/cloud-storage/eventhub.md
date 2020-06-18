---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een Azure de bronschakelaar van de Hubs van de Gebeurtenis in UI
topic: overview
translation-type: tm+mt
source-git-commit: 855f543a1cef394d121502f03471a60b97eae256
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Creeer een Azure de bronschakelaar van de Hubs van de Gebeurtenis in UI

>[!NOTE]
> De Azure Event Hubs-connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het verifiëren van een Azure Event Hubs-bronconnector (hierna &quot;Event Hubs&quot; genoemd) die de gebruikersinterface van het Platform gebruikt.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

- [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een rekening van de Hubs van de Gebeurtenis hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een dataflow](../../dataflow/streaming/cloud-storage.md).

### Vereiste referenties verzamelen

Om uw bronschakelaar van de Hubs van de Gebeurtenis voor authentiek te verklaren, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `sasKey` | De gegenereerde handtekening voor gedeelde toegang. |
| `namespace` | De naamruimte van de gebeurtenishubs waartoe u toegang hebt. |

Raadpleeg [dit Event Hubs-document](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)voor meer informatie over deze waarden.

## Connect your Event Hubs account

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen hieronder volgen om uw rekening van de Hubs van de Gebeurtenis aan Platform te verbinden.

Login aan [Adobe Experience Platform](https://platform.adobe.com) en selecteer dan **Bronnen** van de linkernavigatiebar om tot de werkruimte van *Bronnen* toegang te hebben. Op het tabblad *Catalogus* worden diverse bronnen weergegeven die met het Platform kunnen worden verbonden. Elke bron toont het aantal bestaande rekeningen verbonden aan hen.

Selecteer onder de categorie *Cloud Storage* de optie **Azure Event Hubs** en klik **op het plusteken (+)** om een nieuwe Event Hubs-connector te maken.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Het dialoogvenster *Connect to Azure Event Hubs* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Voor de inputvorm die verschijnt, verstrek een naam, een facultatieve beschrijving, en uw geloofsbrieven van de Hubs van de Gebeurtenis. Wanneer u klaar bent, selecteert u **Connect** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/eventhub/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Event Hubs-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u uw rekening van de Hubs van de Gebeurtenis met Platform verbonden. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag naar het Platform](../../dataflow/streaming/cloud-storage.md)te brengen.