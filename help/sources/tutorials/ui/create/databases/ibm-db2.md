---
keywords: Experience Platform;home;populaire onderwerpen;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Een IBM DB2-bronverbinding maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een IBM DB2-bronverbinding maakt met de Adobe Experience Platform-interface.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Een IBM DB2-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De IBM DB2-connector is in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een IBM DB2-bronconnector (hierna &quot;DB2&quot; genoemd) met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige DB2-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met DB2 te verbinden gebruikend [!DNL Flow Service] API.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `server` | De naam van de DB2-server. U kunt het poortnummer opgeven na de servernaam die is gescheiden door een dubbele punt. Bijvoorbeeld: server:poort. |
| `database` | De naam van de database DB2. |
| `username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de database DB2. |
| `password` | Het wachtwoord voor de gebruikersaccount die u voor de gebruikersnaam hebt opgegeven. |

Raadpleeg voor meer informatie over aan de slag gaan [dit DB2-document](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## IBM DB2-account verbinden

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw DB2-account te koppelen aan [!DNL Platform].

Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de **[!UICONTROL Sources]** werkruimte. De **[!UICONTROL Catalog]** in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Databases]** categorie, selecteert u **[!UICONTROL IBM DB2]**. Als dit de eerste keer is met deze connector, selecteert u **[!UICONTROL Configure]**. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe schakelaar te creëren DB2.

![catalogus](../../../../images/tutorials/create/ibm-db2/catalog.png)

De **[!UICONTROL Connect to IBM DB2]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw DB2-referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![verbinden](../../../../images/tutorials/create/ibm-db2/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de DB2-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/ibm-db2/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw DB2-account tot stand gebracht. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).
