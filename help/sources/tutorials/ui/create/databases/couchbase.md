---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Couchbase-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# Een Couchbase-bronconnector maken in de gebruikersinterface

> [!NOTE]
> De Couchbase-connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in [!DNL Adobe Experience Platform] verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een Couchbase-bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van [!DNL Platform]:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding van de Couchbase hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Om uw Couchbase bronschakelaar voor authentiek te verklaren, moet u waarden voor het volgende verbindingsbezit verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie Couchbase. Het patroon van de verbindingstekenreeks voor Couchbase is `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Raadpleeg de documentatie bij [Couchbase-verbinding](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)voor meer informatie over het verkrijgen van een verbindingstekenreeks. |

## Verbinding maken met uw Couchbase-account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om een nieuwe account voor Couchbase te maken waarmee u verbinding kunt maken [!DNL Platform].

Login aan [Adobe Experience Platform](https://platform.adobe.com) en selecteer dan **[!UICONTROL Bronnen]** van de linkernavigatiebar om tot de werkruimte van *[!UICONTROL Bronnen]* toegang te hebben. Het scherm van de *[!UICONTROL Catalogus]* toont een verscheidenheid van bronnen waarvoor u een binnenkomende rekening met kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de categorie *[!UICONTROL Databases]* selecteert u **[!UICONTROL Couchbase]** en klikt u **op het pictogram + (+)** om een nieuwe Couchbase-connector te maken.

![catalogus](../../../../images/tutorials/create/couchbase/catalog.png)

De pagina *[!UICONTROL Verbinden met Couchbase]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw gegevens voor de Couchbase. Als u klaar bent, selecteert u **[!UICONTROL Verbinding maken met bron]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/couchbase/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Couchbase-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** in de rechterbovenhoek om door te gaan.

![bestaand](../../../../images/tutorials/create/couchbase/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw account Couchbase. U kunt nu verdergaan aan het volgende leerprogramma en een dataflow [vormen om gegevens in Platform](../../dataflow/databases.md)te brengen.