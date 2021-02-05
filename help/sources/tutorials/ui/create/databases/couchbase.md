---
keywords: Experience Platform;home;populaire onderwerpen;Couchbase;couchbase
solution: Experience Platform
title: Een Couchbase-bronverbinding maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Leer hoe u een Couchbase-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---


# Een [!DNL Couchbase]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Couchbase] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in [!DNL Adobe Experience Platform] verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Couchbase]-bronconnector met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van [!DNL Platform]:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Couchbase] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [vormend een dataflow](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Om uw [!DNL Couchbase] bronschakelaar voor authentiek te verklaren, moet u waarden voor het volgende verbindingsbezit verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met uw [!DNL Couchbase]-instantie. Het patroon van de verbindingstekenreeks voor [!DNL Couchbase] is `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Raadpleeg de documentatie bij [[!DNL Couchbase] connection](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview) voor meer informatie over het ophalen van een verbindingstekenreeks. |

## Uw [!DNL Couchbase]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Couchbase]-account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Bronnen]** te openen. Het scherm **[!UICONTROL Catalog]** toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Couchbase]** onder de categorie **[!UICONTROL Databases]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders, uitgezocht **[!UICONTROL voeg gegevens]** toe om een nieuwe [!DNL Couchbase] schakelaar tot stand te brengen.

![catalogus](../../../../images/tutorials/create/couchbase/catalog.png)

De pagina **[!UICONTROL Verbinding maken met Couchbase]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Couchbase]-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL verbind met bron]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![verbinden](../../../../images/tutorials/create/couchbase/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Couchbase]-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** in de rechterbovenhoek om door te gaan.

![bestaand](../../../../images/tutorials/create/couchbase/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Couchbase]-account. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).