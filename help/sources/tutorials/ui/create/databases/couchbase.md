---
keywords: Experience Platform;home;populaire onderwerpen;Couchbase;couchbase
solution: Experience Platform
title: Een Couchbase Source-verbinding maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Couchbase-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
source-git-commit: a32d0d7ed7d18454099d2b55b3f6809cfbcd9b62
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Een [!DNL Couchbase] bronverbinding maken in de gebruikersinterface

>[!IMPORTANT]
>
>De bron [!DNL Couchbase] wordt eind mei 2025 vervangen.

Source-connectors in [!DNL Adobe Experience Platform] bieden de mogelijkheid om volgens schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Couchbase] bronaansluiting met behulp van de gebruikersinterface van [!DNL Platform] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van [!DNL Platform] :

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Couchbase] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u de [!DNL Couchbase] bronconnector wilt verifiëren, moet u waarden opgeven voor de volgende verbindingseigenschap:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie [!DNL Couchbase] . Het patroon van de verbindingstekenreeks voor [!DNL Couchbase] is `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];` . Voor meer informatie bij het verwerven van een verbindingskoord, verwijs naar de documentatie over [[!DNL Couchbase]  verbinding ](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Sluit uw [!DNL Couchbase] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Couchbase] -account te koppelen aan [!DNL Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL Couchbase]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Couchbase] -connector te maken.

![ catalogus ](../../../../images/tutorials/create/couchbase/catalog.png)

De pagina **[!UICONTROL Connect to Couchbase]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Couchbase] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/couchbase/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Couchbase] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan.

![ bestaand ](../../../../images/tutorials/create/couchbase/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Couchbase] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Platform]](../../dataflow/databases.md) te brengen.
