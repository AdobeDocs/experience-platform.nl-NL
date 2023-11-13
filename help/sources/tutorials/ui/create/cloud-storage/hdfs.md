---
keywords: Experience Platform;home;populaire onderwerpen;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Een Apache HDFS-bronverbinding maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Apache Hadoop Distributed File System-bronverbinding maakt met de Adobe Experience Platform-interface.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Een [!DNL Apache] HDFS-bronverbinding in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Apache] De HDFS-aansluiting is in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Bronaansluitingen in [!DNL Adobe Experience Platform] de mogelijkheid bieden om op een geplande basis extern verkregen gegevens in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Apache Hadoop Distributed File System] (hierna &quot;HDFS&quot; genoemd) bronaansluiting met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geldige HDFS-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Voor verificatie van de HDFS-bronconnector moet u waarden opgeven voor de volgende eigenschap connection:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De URL definieert de auteparams die vereist zijn om anoniem verbinding te maken met HDFS. Raadpleeg voor meer informatie over het verkrijgen van deze waarde het volgende document op [HTTPS-verificatie voor HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Sluit uw HDFS-account aan

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw HDFS-account te koppelen aan [!DNL Platform].

Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de **[!UICONTROL Sources]** werkruimte. De **[!UICONTROL Catalog]** in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Cloud storage]** categorie, selecteert u **[!UICONTROL Apache HDFS]**. Als dit de eerste keer is met deze connector, selecteert u **[!UICONTROL Configure]**. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe HDFS-aansluiting te maken.

![catalogus](../../../../images/tutorials/create/hdfs/catalog.png)

De **[!UICONTROL Connect to HDFS]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw HDFS-referenties op. Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![verbinden](../../../../images/tutorials/create/hdfs/new.png)

### Bestaande account

Als u een bestaande account wilt aansluiten, selecteert u de HDFS-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/hdfs/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw HDFS-account tot stand gebracht. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag over te brengen naar [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
