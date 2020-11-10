---
keywords: Experience Platform;home;popular topics;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Een Apache HDFS-bronaansluiting maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Deze zelfstudie bevat stappen voor het verifiëren van een Apache Hadoop Distributed File System (hierna "HDFS" genoemd)-bronconnector via de gebruikersinterface van het Platform.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# Een [!DNL Apache] HDFS-bronaansluiting maken in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Apache] HDFS-aansluiting is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in [!DNL Adobe Experience Platform] verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Apache Hadoop Distributed File System] (hierna &quot;HDFS&quot; genoemd) bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige HDFS-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Voor verificatie van de HDFS-bronconnector moet u waarden opgeven voor de volgende eigenschap connection:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De URL definieert de auteparams die vereist zijn om anoniem verbinding te maken met HDFS. Raadpleeg het volgende document over [HTTPS-verificatie voor HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)voor meer informatie over hoe u deze waarde kunt verkrijgen. |

## Sluit uw HDFS-account aan

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw HDFS-account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Bronnen]** . In het scherm **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Apache HDFS onder de opslagcategorie]** Cloud ****. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders selecteert u Gegevens **** toevoegen om een nieuwe HDFS-aansluiting te maken.

![catalogus](../../../../images/tutorials/create/hdfs/catalog.png)

De pagina **[!UICONTROL Verbinding maken met HDFS]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw HDFS-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL verbind met bron]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![verbinden](../../../../images/tutorials/create/hdfs/new.png)

### Bestaande account

Als u een bestaande account wilt aansluiten, selecteert u de HDFS-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/hdfs/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw HDFS-account tot stand gebracht. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag naar [!DNL Platform]](../../dataflow/batch/cloud-storage.md)te brengen.