---
keywords: Experience Platform;home;populaire onderwerpen;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Een Apache HDFS Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Apache Hadoop-bronverbinding voor gedistribueerd bestandssysteem maakt met behulp van de Adobe Experience Platform-gebruikersinterface.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Een [!DNL Apache] HDFS-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Apache] HDFS-connector bevindt zich in bèta. Zie het [&#x200B; Bronoverzicht &#x200B;](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Source-connectors in [!DNL Adobe Experience Platform] bieden de mogelijkheid om volgens schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Apache Hadoop Distributed File System] (hierna &quot;HDFS&quot; genoemd) bronconnector via de [!DNL Experience Platform] -gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van [!DNL Experience Platform] :

- [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   - [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige verbinding van HDFS hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Voor verificatie van de HDFS-bronconnector moet u waarden opgeven voor de volgende eigenschap connection:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De URL definieert de auteparams die vereist zijn om anoniem verbinding te maken met HDFS. Voor meer informatie over hoe te om deze waarde te verkrijgen, verwijs naar het volgende document op [&#x200B; authentificatie HTTPS voor HDFS &#x200B;](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Sluit uw HDFS-account aan

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw HDFS-account te koppelen aan [!DNL Experience Platform] .

Login aan [&#x200B; Adobe Experience Platform &#x200B;](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Cloud storage]** de optie **[!UICONTROL Apache HDFS]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe HDFS-aansluiting te maken.

![&#x200B; catalogus &#x200B;](../../../../images/tutorials/create/hdfs/catalog.png)

De pagina **[!UICONTROL Connect to HDFS]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw HDFS-referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![&#x200B; verbind &#x200B;](../../../../images/tutorials/create/hdfs/new.png)

### Bestaande account

Als u een bestaande account wilt aansluiten, selecteert u de HDFS-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![&#x200B; bestaand &#x200B;](../../../../images/tutorials/create/hdfs/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw HDFS-account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens van uw wolkenopslag in  [!DNL Experience Platform]](../../dataflow/batch/cloud-storage.md) te brengen.
