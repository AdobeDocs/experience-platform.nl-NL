---
keywords: Experience Platform;home;populaire onderwerpen;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: IBM DB2 Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een IBM DB2-bronverbinding maakt met de Adobe Experience Platform-interface.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# Een IBM DB2-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De IBM DB2-connector is in bèta. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een IBM DB2-bronconnector (hierna &quot;DB2&quot; genoemd) via de gebruikersinterface van [!DNL Experience Platform] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige verbinding DB2 hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met DB2 tot stand te kunnen brengen met de API [!DNL Flow Service] .

| Credentials | Beschrijving |
| ---------- | ----------- |
| `server` | De naam van de DB2-server. U kunt het poortnummer opgeven na de servernaam die is gescheiden door een dubbele punt. Bijvoorbeeld: server:poort. |
| `database` | De naam van de database DB2. |
| `username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de database DB2. |
| `password` | Het wachtwoord voor de gebruikersaccount die u voor de gebruikersnaam hebt opgegeven. |

Voor meer informatie over begonnen worden, verwijs naar [ dit document DB2 ](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## IBM DB2-account verbinden

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw DB2-account te koppelen aan [!DNL Experience Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL IBM DB2]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe DB2-connector te maken.

![ catalogus ](../../../../images/tutorials/create/ibm-db2/catalog.png)

De pagina **[!UICONTROL Connect to IBM DB2]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw DB2-referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/ibm-db2/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de DB2-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/ibm-db2/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw DB2-account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Experience Platform]](../../dataflow/databases.md) te brengen.
