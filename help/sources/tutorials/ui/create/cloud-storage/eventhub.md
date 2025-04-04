---
title: Een Azure Event Hubs Source Connection maken in de gebruikersinterface
description: Leer hoe u een Azure Event Hubs-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# Een [!DNL Azure Event Hubs] bronverbinding maken in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Azure Event Hubs] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Lees deze zelfstudie om te leren hoe u een [!DNL Azure Event Hubs] -account kunt maken via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Event Hubs] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/streaming/cloud-storage-streaming.md).

### Vereiste referenties verzamelen

Als u de [!DNL Event Hubs] bronconnector wilt verifiëren, moet u waarden opgeven voor de volgende verbindingseigenschappen:

>[!BEGINTABS]

>[!TAB  Standaard authentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| SAS-sleutelnaam | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| SAS-sleutel | De primaire sleutel van de naamruimte [!DNL Event Hubs] . De `sasPolicy` die `sasKey` aansluit bij `manage` , moet rechten hebben geconfigureerd om de [!DNL Event Hubs] -lijst te vullen. |
| Naamruimte | De naamruimte van de [!DNL Event Hub] die u opent. Een naamruimte [!DNL Event Hub] biedt een unieke container voor het bereik, waarin u een of meer naamruimten kunt maken [!DNL Event Hubs] . |

>[!TAB  SAS authentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| SAS-sleutelnaam | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| SAS-sleutel | De primaire sleutel van de naamruimte [!DNL Event Hub] . De `sasPolicy` die `sasKey` aansluit bij `manage` , moet rechten hebben geconfigureerd om de [!DNL Event Hubs] -lijst te vullen. |
| Naamruimte | De naamruimte van de [!DNL Event Hub] die u opent. Een naamruimte [!DNL Event Hub] biedt een unieke container voor het bereik, waarin u een of meer naamruimten kunt maken [!DNL Event Hubs] . |
| Naam van gebeurtenishub | Vul de naam [!DNL Azure Event Hub] in. Lees de [ documentatie van Microsoft ](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) voor meer informatie over [!DNL Event Hub] namen. |

>[!TAB  Hub van de Gebeurtenis Azure Actieve Auth van de Folder ]

| Credentials | Beschrijving |
| --- | --- |
| Tenant-id | De huurder-id waarvan u toestemming wilt vragen. Uw huurder identiteitskaart kan als GUID of als vriendschappelijke naam worden geformatteerd. **Nota**: De huurder identiteitskaart wordt bedoeld als &quot;identiteitskaart van de Folder&quot;in de [!DNL Microsoft Azure] interface. |
| Client-id | De toepassings-id die aan uw app is toegewezen. U kunt deze id ophalen via de portal [!DNL Microsoft Entra ID] waar u uw [!DNL Azure Active Directory] hebt geregistreerd. |
| Geheime waarde client | Het clientgeheim dat naast de client-id wordt gebruikt om uw app te verifiëren. U kunt uw clientgeheim ophalen via de [!DNL Microsoft Entra ID] -portal waar u uw [!DNL Azure Active Directory] hebt geregistreerd. |
| Naamruimte | De naamruimte van de [!DNL Event Hub] die u opent. Een naamruimte [!DNL Event Hub] biedt een unieke container voor het bereik, waarin u een of meer naamruimten kunt maken [!DNL Event Hubs] . |

Voor meer informatie over [!DNL Azure Active Directory], lees de [ Azure gids bij het gebruiken van identiteitskaart van Microsoft Entra ](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB  Hub Scoped Azure Actieve Auth van de Folder van de Gebeurtenis ]

| Credentials | Beschrijving |
| --- | --- |
| Tenant-id | De huurder-id waarvan u toestemming wilt vragen. Uw huurder identiteitskaart kan als GUID of als vriendschappelijke naam worden geformatteerd. **Nota**: De huurder identiteitskaart wordt bedoeld als &quot;identiteitskaart van de Folder&quot;in de [!DNL Microsoft Azure] interface. |
| Client-id | De toepassings-id die aan uw app is toegewezen. U kunt deze id ophalen via de portal [!DNL Microsoft Entra ID] waar u uw [!DNL Azure Active Directory] hebt geregistreerd. |
| Geheime waarde client | Het clientgeheim dat naast de client-id wordt gebruikt om uw app te verifiëren. U kunt uw clientgeheim ophalen via de [!DNL Microsoft Entra ID] -portal waar u uw [!DNL Azure Active Directory] hebt geregistreerd. |
| Naamruimte | De naamruimte van de [!DNL Event Hub] die u opent. Een naamruimte [!DNL Event Hub] biedt een unieke container voor het bereik, waarin u een of meer naamruimten kunt maken [!DNL Event Hubs] . |
| Naam van gebeurtenishub | Vul de naam [!DNL Azure Event Hub] in. Lees de [ documentatie van Microsoft ](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) voor meer informatie over [!DNL Event Hub] namen. |

Voor meer informatie over [!DNL Azure Active Directory], lees de [ Azure gids bij het gebruiken van identiteitskaart van Microsoft Entra ](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Event Hubs] -account te koppelen aan Experience Platform.

## Sluit uw [!DNL Event Hubs] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL Cloud storage] de optie **[!UICONTROL Azure Event Hubs]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ de broncatalogus met de Azure Geselecteerde Hubs van de Gebeurtenis.](../../../../images/tutorials/create/eventhub/catalog.png)

Het dialoogvenster **[!UICONTROL Connect to Azure Event Hubs]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Event Hubs] -account die u wilt gebruiken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ een lijst van bestaande Azure van de Bron van de Gebeurtenis Hubs rekeningen.](../../../../images/tutorials/create/eventhub/existing.png)

### Nieuwe account

>[!TIP]
>
>Nadat u een [!DNL Event Hubs] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en een optionele beschrijving voor uw nieuwe [!DNL Event Hubs] -account.

![ de nieuwe interface van de rekeningsverwezenlijking voor de Hubs van de Gebeurtenis van Azure.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB  Standaard authentificatie ]

Als u een [!DNL Event Hubs] -account met standaardverificatie wilt maken, gebruikt u het vervolgkeuzemenu [!UICONTROL Account authentication] en selecteert u **[!UICONTROL Standard authentication]** . Geef vervolgens waarden op voor de [!UICONTROL SAS key name] , [!UICONTROL SAS key] en [!UICONTROL Namespace] .

Nadat u de verificatiegegevens hebt ingevoerd, selecteert u **[!UICONTROL Connect to source]** .

![ de standaardauthentificatieinterface voor Azure Event Hubs.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB  SAS authentificatie ]

Als u een [!DNL Event Hubs] -account met SAS-verificatie wilt maken, gebruikt u het vervolgkeuzemenu [!UICONTROL Account authentication] en selecteert u vervolgens **[!UICONTROL SAS authentication]** . Geef vervolgens waarden op voor de [!UICONTROL SAS key name] , [!UICONTROL SAS key] , [!UICONTROL Namespace] en [!UICONTROL Event Hubs name] .

Nadat u de verificatiegegevens hebt ingevoerd, selecteert u **[!UICONTROL Connect to source]** .

![ de SAS authentificatieinterface voor Azure Event Hubs.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB  Hub van de Gebeurtenis Azure Actieve Auth van de Folder ]

Als u een [!DNL Event Hubs] -account wilt maken met Active Directory-verificatie van de gebeurtenishub Azure, gebruikt u het vervolgkeuzemenu [!UICONTROL Account authentication] en selecteert u **[!UICONTROL Event Hub Azure Active Directory]** . Geef vervolgens waarden op voor de [!UICONTROL Tenant ID] , [!UICONTROL Client ID] , [!UICONTROL Client Secret Value] en [!UICONTROL Namespace] .

![ Azure de Hub van de Gebeurtenis Azure Actieve Authentificatie van de Folder ](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB  Hub Scoped Azure Actieve Auth van de Folder van de Gebeurtenis ]

Als u een [!DNL Event Hubs] -account wilt maken met de verificatie van Active Directory van de gebeurtenishub Scoped Azure, gebruikt u het vervolgkeuzemenu [!UICONTROL Account authentication] en selecteert u **[!UICONTROL Event Hub Scoped Azure Active Directory]** . Geef vervolgens waarden op voor de [!UICONTROL Tenant ID] , [!UICONTROL Client ID] , [!UICONTROL Client Secret Value] , [!UICONTROL Namespace] en [!UICONTROL Event Hub Name] .

![ Azure de Hub Scoped Azure van de Gebeurtenis de Authentificatie van de Folder van de Activiteit ](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Volgende stappen

Door deze zelfstudie te volgen, hebt u uw [!DNL Event Hubs] -account verbonden met Experience Platform. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens van uw wolkenopslag in Experience Platform ](../../dataflow/streaming/cloud-storage-streaming.md) te brengen.
