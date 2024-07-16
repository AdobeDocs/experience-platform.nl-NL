---
keywords: Experience Platform;home;populaire onderwerpen;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Een Apache HDFS Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Apache Hadoop Distributed File System-bronverbinding maakt met de Adobe Experience Platform-interface.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Een [!DNL Apache] HDFS-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Apache] HDFS-connector bevindt zich in bèta. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Source-connectors in [!DNL Adobe Experience Platform] bieden de mogelijkheid om volgens schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Apache Hadoop Distributed File System] (hierna &quot;HDFS&quot; genoemd) bronconnector via de [!DNL Platform] -gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van [!DNL Platform] :

- [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   - [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige verbinding van HDFS hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Voor verificatie van de HDFS-bronconnector moet u waarden opgeven voor de volgende eigenschap connection:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De URL definieert de auteparams die vereist zijn om anoniem verbinding te maken met HDFS. Voor meer informatie over hoe te om deze waarde te verkrijgen, verwijs naar het volgende document op [ authentificatie HTTPS voor HDFS ](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Sluit uw HDFS-account aan

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw HDFS-account te koppelen aan [!DNL Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Cloud storage]** de optie **[!UICONTROL Apache HDFS]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe HDFS-aansluiting te maken.

![ catalogus ](../../../../images/tutorials/create/hdfs/catalog.png)

De pagina **[!UICONTROL Connect to HDFS]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw HDFS-referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/hdfs/new.png)

### Bestaande account

Als u een bestaande account wilt aansluiten, selecteert u de HDFS-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/hdfs/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw HDFS-account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens van uw wolkenopslag in  [!DNL Platform]](../../dataflow/batch/cloud-storage.md) te brengen.
