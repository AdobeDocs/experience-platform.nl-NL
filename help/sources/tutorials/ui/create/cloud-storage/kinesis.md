---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Amazon Kinesis-bronaansluiting maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# Creeer een [!DNL Amazon Kinesis] bronschakelaar in UI

>[!NOTE]
>De [!DNL Amazon Kinesis] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om extern gesourceerde gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het verifiëren van een [!DNL Amazon Kinesis] (hierna [!DNL "Kinesis"]) bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

- [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een [!DNL Kinesis] account hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/streaming/cloud-storage.md).

### Vereiste referenties verzamelen

Om uw [!DNL Kinesis] bronschakelaar voor authentiek te verklaren, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `accessKeyId` | De toegangssleutel-id voor uw [!DNL Kinesis] account. |
| `Secret access key` | De geheime toegangssleutel voor uw [!DNL Kinesis] account. |
| `region` | Het gebied van uw AWS-server. |

Raadpleeg [dit Kinesis-document](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)voor meer informatie over deze waarden.

## Uw [!DNL Kinesis] account verbinden

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Kinesis] account te koppelen aan [!DNL Platform].

Login aan [Adobe Experience Platform](https://platform.adobe.com) en selecteer dan **[!UICONTROL Bronnen]** van de linkernavigatiebar om tot de werkruimte van *Bronnen* toegang te hebben. Op het tabblad *Catalogus* worden diverse bronnen weergegeven waarmee u verbinding kunt maken [!DNL Platform]. Elke bron toont het aantal bestaande rekeningen verbonden aan hen.

Selecteer in de categorie *[!UICONTROL Cloud Storage]* de optie **[!UICONTROL Amazon Kinesis]** en klik **op + (+)** om een nieuwe [!DNL Kinesis] aansluiting te maken.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Het dialoogvenster *[!UICONTROL Verbinding maken met Amazon Kinesis]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Kinesis] referenties in. Wanneer u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/kinesis/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Kinesis] account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u verbinding met uw [!DNL Kinesis] account gemaakt [!DNL Platform]. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag naar het Platform](../../dataflow/streaming/cloud-storage.md)te brengen.