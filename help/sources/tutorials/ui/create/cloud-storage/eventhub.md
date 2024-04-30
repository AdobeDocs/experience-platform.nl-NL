---
title: Creeer een Azure van de BronVerbinding van de Gebeurtenis Hubs in UI
description: Leer hoe u een Azure Event Hubs-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: e4ea21af3f0d9e810959330488dc06bc559cf72c
workflow-type: tm+mt
source-wordcount: '1013'
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

Voor meer informatie over verificatie met gedeelde toegang (SAS) voor [!DNL Event Hubs], lees de [[!DNL Azure] handleiding voor het gebruik van SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Event Hub Azure Active Directory Auth]

| Credentials | Beschrijving |
| --- | --- |
| Tenant-id | De huurder-id waarvan u toestemming wilt vragen. Uw huurder identiteitskaart kan als GUID of als vriendschappelijke naam worden geformatteerd. **Opmerking**: De huurdersidentiteitskaart wordt bedoeld als &quot;identiteitskaart van de Folder&quot;in [!DNL Microsoft Azure] interface. |
| Client-id | De toepassings-id die aan uw app is toegewezen. U kunt deze id ophalen vanuit het dialoogvenster [!DNL Microsoft Entra ID] portal waar u uw [!DNL Azure Active Directory]. |
| Geheime waarde client | Het clientgeheim dat naast de client-id wordt gebruikt om uw app te verifiëren. U kunt uw clientgeheim ophalen via het dialoogvenster [!DNL Microsoft Entra ID] portal waar u uw [!DNL Azure Active Directory]. |
| Naamruimte | De naamruimte van de [!DNL Event Hubs] u hebt toegang. An [!DNL Event Hubs] namespace verstrekt een unieke bereikcontainer, waarin u één of meerdere kunt creëren [!DNL Event Hubs]. |

Voor meer informatie over [!DNL Azure Active Directory], lees de [Azure-gids bij het gebruik van Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB De Hub Scoped Azure Active Directory Auth van de gebeurtenis]

| Credentials | Beschrijving |
| --- | --- |
| Tenant-id | De huurder-id waarvan u toestemming wilt vragen. Uw huurder identiteitskaart kan als GUID of als vriendschappelijke naam worden geformatteerd. **Opmerking**: De huurdersidentiteitskaart wordt bedoeld als &quot;identiteitskaart van de Folder&quot;in [!DNL Microsoft Azure] interface. |
| Client-id | De toepassings-id die aan uw app is toegewezen. U kunt deze id ophalen vanuit het dialoogvenster [!DNL Microsoft Entra ID] portal waar u uw [!DNL Azure Active Directory]. |
| Geheime waarde client | Het clientgeheim dat naast de client-id wordt gebruikt om uw app te verifiëren. U kunt uw clientgeheim ophalen via het dialoogvenster [!DNL Microsoft Entra ID] portal waar u uw [!DNL Azure Active Directory]. |
| Naamruimte | De naamruimte van de [!DNL Event Hubs] u hebt toegang. An [!DNL Event Hubs] namespace verstrekt een unieke bereikcontainer, waarin u één of meerdere kunt creëren [!DNL Event Hubs]. |
| Naam van gebeurtenishub | De naam voor uw [!DNL Event Hubs] bron. |

Voor meer informatie over [!DNL Azure Active Directory], lees de [Azure-gids bij het gebruik van Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

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

Om een [!DNL Event Hubs] -account met standaardverificatie, gebruik de [!UICONTROL Account authentication] vervolgkeuzemenu en selecteer vervolgens **[!UICONTROL Standard authentication]**. Geef vervolgens waarden op voor uw [!UICONTROL SAS key name], [!UICONTROL SAS key], en [!UICONTROL Namespace].

Nadat u de verificatiegegevens hebt ingevoerd, selecteert u **[!UICONTROL Connect to source]**.

![De standaardverificatieinterface voor Azure Event Hubs.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB SAS-verificatie]

Om een [!DNL Event Hubs] account met SAS-verificatie, gebruik de [!UICONTROL Account authentication] vervolgkeuzemenu en selecteer vervolgens **[!UICONTROL SAS authentication]**. Geef vervolgens waarden op voor uw [!UICONTROL SAS key name], [!UICONTROL SAS key], [!UICONTROL Namespace], en [!UICONTROL Event Hubs name].

Nadat u de verificatiegegevens hebt ingevoerd, selecteert u **[!UICONTROL Connect to source]**.

![De SAS-verificatieinterface voor Azure Event Hubs.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB Event Hub Azure Active Directory Auth]

Om een [!DNL Event Hubs] de rekening met de authentificatie van de Folder van de Hub van de Gebeurtenis Azure Actieve [!UICONTROL Account authentication] vervolgkeuzemenu en selecteer vervolgens **[!UICONTROL Event Hub Azure Active Directory]**. Geef vervolgens waarden op voor uw [!UICONTROL Tenant ID], [!UICONTROL Client ID], [!UICONTROL Client Secret Value], en [!UICONTROL Namespace].

![Azure Event Hub Azure Active Directory Authentication](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB De Hub Scoped Azure Active Directory Auth van de gebeurtenis]

Om een [!DNL Event Hubs] account met verificatie van Active Directory van gebeurtenishub Scoped Azure Active Directory, gebruik de [!UICONTROL Account authentication] vervolgkeuzemenu en selecteer vervolgens **[!UICONTROL Event Hub Scoped Azure Active Directory]**. Geef vervolgens waarden op voor uw [!UICONTROL Tenant ID], [!UICONTROL Client ID], [!UICONTROL Client Secret Value], [!UICONTROL Namespace], en [!UICONTROL Event Hub Name].

![Azure Event Hub Scoped Azure Activity Directory Authentication](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Volgende stappen

Door deze zelfstudie te volgen, hebt u verbinding gemaakt met uw [!DNL Event Hubs] aan Experience Platform. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Experience Platform te brengen](../../dataflow/streaming/cloud-storage-streaming.md).
