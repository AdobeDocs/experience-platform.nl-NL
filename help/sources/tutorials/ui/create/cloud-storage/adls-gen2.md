---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Maak een Azure Data Lake Storage Gen2-bronconnector in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# Creeer een [!DNL Azure Data Lake Storage Gen2] bronschakelaar in UI

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om extern gesourceerde gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het verifiëren van een [!DNL Azure Data Lake Storage Gen2] (hierna &quot;ADLS Gen2&quot; genoemd) bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

- [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een ADLS Gen2 basisverbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Om uw ADLS Gen2-bronconnector te verifiëren, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | Het eindpunt voor ADLS Gen2. |
| `servicePrincipalId` | De client-id van de toepassing. |
| `servicePrincipalKey` | De sleutel van de toepassing. |
| `tenant` | De huurdersinformatie die uw toepassing bevat. |

Raadpleeg [dit ADLS Gen2-document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)voor meer informatie over deze waarden.

## Sluit uw ADLS Gen2-account aan

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuwe binnenkomende basisverbinding tot stand te brengen om uw rekening van ADLS Gen2 aan te verbinden [!DNL Platform].

Login aan <a href="https://platform.adobe.com" target="_blank">Adobe [!DNL Experience Platform]</a> en selecteer dan **[!UICONTROL Bronnen]** van de linkernavigatiebar om tot de werkruimte van *[!UICONTROL Bronnen]* toegang te hebben. Op het tabblad *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven die kunnen worden gebruikt om binnenkomende basisverbindingen te maken. Elke bron toont het aantal bestaande basisverbindingen verbonden aan hen.

Selecteer onder de categorie *[!UICONTROL Cloud Storage]* de optie **[!UICONTROL Azure Data Lake Gen2]** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van een verbinding met de bronweergave in de bijbehorende documentatie. Klik op **[!UICONTROL Verbindingsbron]** om een nieuwe binnenkomende basisverbinding te maken.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Het dialoogvenster *[!UICONTROL Verbinden met Azure Data Lake Gen2]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, aan de basisverbinding een naam, een optionele beschrijving en uw ADLS Gen2-referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe basisverbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de ADLS Gen2-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een basisverbinding tot stand gebracht met uw account van ADLS Gen2. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag naar het Platform](../../dataflow/batch/cloud-storage.md)te brengen.