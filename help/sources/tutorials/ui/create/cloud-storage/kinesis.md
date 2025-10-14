---
title: Een Amazon Kinesis Source Connection maken in de gebruikersinterface
description: Leer hoe u een Amazon Kinesis-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Een [!DNL Amazon Kinesis] bronverbinding maken in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Amazon Kinesis] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Amazon Kinesis] (hierna [!DNL "Kinesis"] genoemd) bronconnector met behulp van de [!DNL Experience Platform] -gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   - [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Kinesis] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/streaming/cloud-storage-streaming.md).

### Vereiste referenties verzamelen

Als u de [!DNL Kinesis] bronconnector wilt verifiëren, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `accessKeyId` | De toegangstoets-id voor uw [!DNL Kinesis] -account. |
| `Secret access key` | De geheime toegangssleutel voor uw [!DNL Kinesis] account. |
| `region` | Het gebied van uw AWS-server. |

Voor meer informatie over deze waarden, verwijs naar [&#x200B; dit  [!DNL Kinesis]  document &#x200B;](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Sluit uw [!DNL Kinesis] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Kinesis] -account te koppelen aan [!DNL Experience Platform] .

Login aan [&#x200B; Adobe Experience Platform &#x200B;](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Cloud Storage]** de optie **[!UICONTROL Amazon Kinesis]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Kinesis] -connector te maken.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Het dialoogvenster **[!UICONTROL Connect to Amazon Kinesis]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New Account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Kinesis] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/kinesis/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Kinesis] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u verbinding gemaakt met uw [!DNL Kinesis] -account met [!DNL Experience Platform] . U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens van uw wolkenopslag in  [!DNL Experience Platform]](../../dataflow/streaming/cloud-storage-streaming.md) te brengen.
