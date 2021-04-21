---
keywords: Experience Platform;home;populaire onderwerpen;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Een Amazon Kinesis Source Connection maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Amazon Kinesis-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---

# Een [!DNL Amazon Kinesis]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Amazon Kinesis] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Amazon Kinesis] (hierna [!DNL "Kinesis"] genoemd) bronconnector met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Kinesis] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [vormend een dataflow](../../dataflow/streaming/cloud-storage-streaming.md).

### Vereiste referenties verzamelen

Om uw [!DNL Kinesis] bronschakelaar voor authentiek te verklaren, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `accessKeyId` | De toegangs belangrijkste identiteitskaart voor uw [!DNL Kinesis] rekening. |
| `Secret access key` | De geheime toegangssleutel voor uw [!DNL Kinesis] rekening. |
| `region` | Het gebied van uw AWS-server. |

Raadpleeg [this [!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html) voor meer informatie over deze waarden.

## Uw [!DNL Kinesis]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Kinesis]-account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Sources]** te openen. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Amazon Kinesis]** onder de categorie **[!UICONTROL Cloud Storage]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL Configure]**. Anders, selecteer **[!UICONTROL Add data]** om een nieuwe [!DNL Kinesis] schakelaar tot stand te brengen.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Het dialoogvenster **[!UICONTROL Connect to Amazon Kinesis]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New Account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Kinesis]-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![](../../../../images/tutorials/create/kinesis/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Kinesis]-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u verbinding gemaakt met uw [!DNL Kinesis]-account met [!DNL Platform]. U kunt nu verdergaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag over te brengen naar [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
