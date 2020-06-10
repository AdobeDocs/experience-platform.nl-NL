---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Apache HDFS-bronaansluiting maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: adb9c46e7337897e2336971e58ebc90b0e497ea0
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# Een Apache HDFS-bronaansluiting maken in de gebruikersinterface

>[!NOTE]
>Apache HDFS is in bèta. De functies en documentatie kunnen worden gewijzigd.

De bronschakelaars in [!DNL Adobe Experience Platform] verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een Apache Hadoop Distributed File System (hierna &quot;HDFS&quot; genoemd)-bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van [!DNL Platform]:

- [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een HDFS-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Voor verificatie van de HDFS-bronconnector moet u waarden opgeven voor de volgende eigenschap connection:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De URL definieert de auteparams die vereist zijn om anoniem verbinding te maken met HDFS. Raadpleeg het volgende document over [HTTPS-verificatie voor HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)voor meer informatie over hoe u deze waarde kunt verkrijgen. |

## Sluit uw HDFS-account aan

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om een nieuwe HDFS-account te maken waarmee u verbinding kunt maken [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *[!UICONTROL Bronnen]* . In het scherm *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven waarmee u een binnenkomende account kunt maken. Elke bron toont het aantal bestaande accounts en gegevensstromen dat aan deze accounts is gekoppeld.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer in de *[!UICONTROL opslagcategorie]* van Cloud de optie **[!UICONTROL Apache HDFS]** en klik **op het plus-pictogram (+)** om een nieuwe HDFS-aansluiting te maken.

![catalogus](../../../../images/tutorials/create/hdfs/catalog.png)

De pagina *[!UICONTROL Verbinding maken met HDFS]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en de gegevens voor de bestandsopslag op. Als u klaar bent, selecteert u **[!UICONTROL Verbinding maken met bron]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/hdfs/new.png)

### Bestaande account

Als u een bestaande account wilt aansluiten, selecteert u de HDFS-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/hdfs/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw HDFS-account tot stand gebracht. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag over te brengen naar Platform](../../dataflow/batch/cloud-storage.md).