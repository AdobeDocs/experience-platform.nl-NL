---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een MySQL bronschakelaar in UI
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Creeer een MySQL bronschakelaar in UI

> [!NOTE]
> De MySQL-connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om extern gesourceerde gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een MySQL-bronconnector met behulp van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een MySQL basisverbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw MySQL-account op Platform, moet u de volgende waarde opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De MySQL-verbindingstekenreeks die aan uw account is gekoppeld. Het MySQL patroon van de verbindingstekenreeks is: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

U kunt meer leren over verbindingskoorden en hoe te om hen te verkrijgen door het document [te lezen](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)MySQL.

## Verbinding maken met uw MySQL-account

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuwe binnenkomende basisverbinding tot stand te brengen om uw rekening MySQL aan Platform te verbinden.

Login aan <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer dan **Bronnen** van de linkernavigatiebar om tot de werkruimte van *Bronnen* toegang te hebben. In het scherm *Catalogus* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Onder de categorie *Databases* selecteert u **MySQL** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **Connect-bron** als u een nieuwe binnenkomende basisverbinding wilt maken.

![](../../../../images/tutorials/create/my-sql/catalog.png)

De pagina *Verbinding maken met MySQL* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Geef op het invoerformulier dat wordt weergegeven, de basisverbinding een naam, een optionele beschrijving en uw MySQL-referenties. Als u klaar bent, selecteert u **Connect** en laat u de nieuwe basisverbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/my-sql/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de MySQL-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een basisverbinding met uw MySQL-account tot stand gebracht. U kunt nu verdergaan aan het volgende leerprogramma en een dataflow [vormen om gegevens in Platform](../../dataflow/databases.md)te brengen.