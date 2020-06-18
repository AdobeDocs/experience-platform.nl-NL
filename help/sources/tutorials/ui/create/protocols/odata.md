---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Generic OData-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Een Generic OData-bronconnector maken in de gebruikersinterface

> [!NOTE]
> De Generic OData-connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een algemene bronconnector van het Open Data Protocol (hierna &quot;OData&quot; genoemd) met behulp van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding OData hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een stroom van de protocoldataset](../../dataflow/protocols.md)

### Vereiste referenties verzamelen

Om tot uw rekening OData in Platform toegang te hebben, moet u de volgende waarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De basis-URL van de OData-service. |

Raadpleeg [dit OData-document](https://www.odata.org/getting-started/basic-tutorial/)voor meer informatie over aan de slag gaan.

## Sluit uw OData-account aan

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuwe rekening te creëren OData om met Platform te verbinden.

Login aan <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer dan **Bronnen** van de linkernavigatiebar om tot de werkruimte van *Bronnen* toegang te hebben. In het scherm *Catalogus* worden diverse bronnen weergegeven waarvoor u een binnenkomende account kunt maken. Elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie *Protocollen* de optie **Generic OData** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **Connect-bron** als u een nieuwe binnenkomende verbinding wilt maken.

![catalogus](../../../../images/tutorials/create/odata/catalog.png)

De pagina *Verbinden met Generic OData* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, aan de verbinding een naam, een optionele beschrijving en uw OData-gegevens. Als u klaar bent, selecteert u **Connect** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/odata/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de OData-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![bestaand](../../../../images/tutorials/create/odata/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw OData-account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en een datasetstroom [vormen om protocolgegevens in Platform](../../dataflow/protocols.md)te brengen.