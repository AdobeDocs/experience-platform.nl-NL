---
title: Een Amazon Kinesis Source Connection maken in de gebruikersinterface
description: Leer hoe u een Amazon Kinesis-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# Een [!DNL Amazon Kinesis] bronverbinding in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Amazon Kinesis] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Amazon Kinesis] (hierna [!DNL "Kinesis"]) bronaansluiting met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geldige [!DNL Kinesis] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/streaming/cloud-storage-streaming.md).

### Vereiste referenties verzamelen

Om uw [!DNL Kinesis] bronaansluiting, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `accessKeyId` | De toegangstoets-id voor uw [!DNL Kinesis] account. |
| `Secret access key` | De geheime toegangstoets voor uw [!DNL Kinesis] account. |
| `region` | Het gebied van uw AWS-server. |

Zie voor meer informatie over deze waarden [dit [!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Verbind uw [!DNL Kinesis] account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Kinesis] account aan [!DNL Platform].

Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de **[!UICONTROL Sources]** werkruimte. De **[!UICONTROL Catalog]** in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Cloud Storage]** categorie, selecteert u **[!UICONTROL Amazon Kinesis]**. Als dit de eerste keer is met deze connector, selecteert u **[!UICONTROL Configure]**. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Kinesis] -aansluiting.

![](../../../../images/tutorials/create/kinesis/catalog.png)

De **[!UICONTROL Connect to Amazon Kinesis]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New Account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Kinesis] referenties. Selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![](../../../../images/tutorials/create/kinesis/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de optie [!DNL Kinesis] account waarmee u verbinding wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u verbinding gemaakt met uw [!DNL Kinesis] account aan [!DNL Platform]. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag over te brengen naar [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
