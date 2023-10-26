---
title: Creeer een Azure van de BronVerbinding van de Gebeurtenis Hubs in UI
description: Leer hoe u een Azure Event Hubs-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 1680cc4e1d5c1576767053a74e560bc2eb8c24cb
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Een [!DNL Azure Event Hubs] bronverbinding in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Azure Event Hubs] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Deze zelfstudie bevat stappen om een [!DNL Azure Event Hubs] -account die de gebruikersinterface van Adobe Experience Platform gebruikt.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geldige [!DNL Event Hubs] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/streaming/cloud-storage-streaming.md).

### Vereiste referenties verzamelen

Om uw [!DNL Event Hubs] bronaansluiting, moet u waarden opgeven voor de volgende verbindingseigenschappen:

>[!BEGINTABS]

>[!TAB Standaardverificatie]

| Credentials | Beschrijving |
| --- | --- |
| SAS-sleutelnaam | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| SAS-sleutel | De primaire sleutel van de [!DNL Event Hubs] naamruimte. De `sasPolicy` dat de `sasKey` komt overeen met `manage` rechten geconfigureerd voor de [!DNL Event Hubs] in te vullen lijst. |
| Naamruimte | De naamruimte van de [!DNL Event Hubs] u hebt toegang. An [!DNL Event Hubs] namespace verstrekt een unieke bereikcontainer, waarin u één of meerdere kunt creëren [!DNL Event Hubs]. |

>[!TAB SAS-verificatie]

| Credentials | Beschrijving |
| --- | --- |
| SAS-sleutelnaam | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| SAS-sleutel | De primaire sleutel van de [!DNL Event Hubs] naamruimte. De `sasPolicy` dat de `sasKey` komt overeen met `manage` rechten geconfigureerd voor de [!DNL Event Hubs] in te vullen lijst. |
| Naamruimte | De naamruimte van de [!DNL Event Hubs] u hebt toegang. An [!DNL Event Hubs] namespace verstrekt een unieke bereikcontainer, waarin u één of meerdere kunt creëren [!DNL Event Hubs]. |
| Naam van gebeurtenishub | De naam voor uw [!DNL Event Hubs] bron. |

>[!ENDTABS]

Zie voor meer informatie over deze waarden [this Event Hubs document](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Event Hubs] aan Experience Platform.

## Verbind uw [!DNL Event Hubs] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden verschillende bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Cloud storage] categorie, selecteert u **[!UICONTROL Azure Event Hubs]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De broncatalogus met Azure Event Hubs geselecteerd.](../../../../images/tutorials/create/eventhub/catalog.png)

De **[!UICONTROL Connect to Azure Event Hubs]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL Event Hubs] account dat u wilt gebruiken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![Een lijst met bestaande Azure Event Hubs-bronaccounts.](../../../../images/tutorials/create/eventhub/existing.png)

### Nieuwe account

>[!TIP]
>
>Nadat u een verificatietype hebt gemaakt, kunt u dit type van een [!DNL Event Hubs] basisverbinding. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam en een optionele beschrijving voor uw nieuwe [!DNL Event Hubs] account.

![De nieuwe interface van de rekeningsverwezenlijking voor Azure Event Hubs.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Standaardverificatie]

Om een [!DNL Event Hubs] account met standaardverificatie, selecteer **[!UICONTROL Standard authentication]** en geef vervolgens waarden op voor uw [!UICONTROL SAS key name], [!UICONTROL SAS key], en [!UICONTROL Namespace].

Nadat u de verificatiegegevens hebt ingevoerd, selecteert u **[!UICONTROL Connect to source]**.

![De standaardverificatieinterface voor Azure Event Hubs.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB SAS-verificatie]

Om een [!DNL Event Hubs] account met SAS-verificatie, selecteer **[!UICONTROL SAS authentication]** en geef vervolgens waarden op voor uw [!UICONTROL SAS key name], [!UICONTROL SAS key], [!UICONTROL Namespace], en [!UICONTROL Event Hubs name].

Nadat u de verificatiegegevens hebt ingevoerd, selecteert u **[!UICONTROL Connect to source]**.

![De SAS-verificatieinterface voor Azure Event Hubs.](../../../../images/tutorials/create/eventhub/sas.png)

>[!ENDTABS]


## Volgende stappen

Door deze zelfstudie te volgen, hebt u verbinding gemaakt met uw [!DNL Event Hubs] aan Experience Platform. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Experience Platform te brengen](../../dataflow/streaming/cloud-storage-streaming.md).
