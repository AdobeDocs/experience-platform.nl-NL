---
title: Een Google PubSub-bronverbinding maken in de gebruikersinterface
description: Leer hoe u een Google PubSub-bronconnector maakt via de gebruikersinterface van Platform.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: b157b9147d8ea8100bcaedca272b303a3c04e71a
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# Een [!DNL Google PubSub] bronverbinding in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Google PubSub] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Google PubSub] (hierna &quot;[!DNL PubSub]&quot;) gebruiken van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Als u al een geldige [!DNL PubSub] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Om verbinding te maken [!DNL PubSub] aan Platform, moet u een geldige waarde voor de volgende geloofsbrieven verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Project-id | De project-id die is vereist voor verificatie [!DNL PubSub]. |
| Credentials | De referentie die vereist is voor verificatie [!DNL PubSub]. U moet ervoor zorgen dat u het volledige JSON-bestand plaatst nadat u de witruimten uit uw referenties hebt verwijderd. |
| Onderwerpnaam | De naam van uw [!DNL PubSub] abonnement. In [!DNL PubSub], staan de abonnementen u toe om berichten te ontvangen, door aan het onderwerp in te tekenen waarin de berichten zijn gepubliceerd aan. **Opmerking**: Eén [!DNL PubSub] abonnement kan slechts voor één dataflow worden gebruikt. Als u meerdere gegevensstromen wilt maken, hebt u meerdere abonnementen nodig. |
| Abonnementsnaam | De naam van uw [!DNL PubSub] abonnement. In [!DNL PubSub], staan de abonnementen u toe om berichten te ontvangen, door aan het onderwerp in te tekenen waarin de berichten zijn gepubliceerd aan. |

Raadpleeg de volgende secties voor meer informatie over deze waarden [PubSub-verificatie](https://cloud.google.com/pubsub/docs/authentication) document. Als u de dienst op rekening-gebaseerde authentificatie gebruikt, zie het volgende [PubSub-hulplijn](https://cloud.google.com/docs/authentication/production#create_service_account) voor stappen over hoe te om uw geloofsbrieven te produceren.

>[!TIP]
>
>Als u de op rekening-gebaseerde authentificatie van de dienst gebruikt, zorg ervoor dat u voldoende gebruikerstoegang tot uw de dienstrekening hebt verleend en dat er geen extra witte ruimten in JSON zijn, wanneer het kopiëren en het kleven van uw geloofsbrieven.

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL PubSub] account aan Platform.

## Verbind uw [!DNL PubSub] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden verschillende bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Cloud storage] categorie, selecteert u **[!UICONTROL Google PubSub]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De broncatalogus op Experience Platform UI.](../../../../images/tutorials/create/google-pubsub/catalog.png)

De **[!UICONTROL Connect to Google PubSub]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL PubSub] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![De bestaande accountselectie in de workflow voor bronnen.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nieuwe account

>[!TIP]
>
>Wanneer u een account met beperkte toegang maakt, moet u ten minste een van uw onderwerpnaam of abonnementsnaam opgeven. Verificatie mislukt als beide waarden ontbreken.

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam en een optionele beschrijving voor uw nieuwe [!DNL PubSub] account.

![De nieuwe accountinterface voor de Google PubSub-bron in de workflow voor bronnen](../../../../images/tutorials/create/google-pubsub/new.png)

De [!DNL PubSub] bron staat u toe om het type van toegang te specificeren dat u tijdens authentificatie wilt toestaan. U kunt opstelling uw rekening om of op project-gebaseerde authentificatie of onderwerp en op abonnement-gebaseerde authentificatie te hebben. De op project-gebaseerde authentificatie staat u toe om toegang tot het wortel-vlakke project in uw rekening te verlenen, terwijl het onderwerp en op abonnement-gebaseerde authentificatie u toestaat om toegang tot een bepaald te beperken [!DNL PubSub] onderwerp en abonnement.

>[!BEGINTABS]

>[!TAB Op projecten gebaseerde verificatie]

Een account maken met toegang tot de hoofdmap [!DNL PubSub] projectmap. Selecteren **[!UICONTROL Google PubSub authentication credentials]** als uw authentificatietype en verstrek uw project identiteitskaart en geloofsbrieven. Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![De nieuwe accountinterface voor de Google PubSub-bron waarbij toegang tot de hoofdmap is geselecteerd.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Onderwerp en op abonnement gebaseerde authentificatie]

Een account maken met alleen beperkte toegang tot een bepaalde [!DNL PubSub] onderwerp en abonnement, uitgezocht **[!UICONTROL Google PubSub Scoped authentication credentials]** en geef vervolgens uw referenties, onderwerpnaam en/of abonnementsnaam op. Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![De nieuwe accountinterface voor de Google PubSub-bron met geselecteerde bereiktoegang.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Hoofd (rollen) toegewezen aan een [!DNL PubSub] het project wordt geërft in alle onderwerpen en abonnementen binnen gecreeerd [!DNL PubSub] project. Als u een hoofd (rol) toegang tot een specifiek onderwerp wilt hebben, dan moet dat hoofd (rol) ook aan het overeenkomstige abonnement van het onderwerp worden toegevoegd. Lees voor meer informatie de [[!DNL PubSub] documentatie over toegangscontrole](<https://cloud.google.com/pubsub/docs/access-control>).

## Gegevens selecteren

Een succesvolle authentificatie brengt u aan [!UICONTROL Select data] stap, waar u door uw [!DNL PubSub] de gegevenshiërarchie en selecteert de gegevens die u aan Experience Platform wilt brengen.

>[!BEGINTABS]

>[!TAB Op projecten gebaseerde verificatie]

Als u met op project-gebaseerde toegang voor authentiek hebt verklaard, [!UICONTROL Select data] de interface zal alle abonnementen binnen uw project tonen dat een onderwerp in bijlage aan hen heeft.

![De uitgezochte gegevensstap van het bronwerkschema met op project-gebaseerde authentificatie.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Onderwerp en op abonnement gebaseerde authentificatie]

Als u met een onderwerp en op abonnement-gebaseerde toegang voor authentiek hebt verklaard, [!UICONTROL Select data] de interfacevertoning kan variëren afhankelijk van de informatie die u verstrekte.

* Als u slechts de onderwerpnaam verstrekt, dan toont de interface alle onderwerp-abonnement paren die aan het verstrekte onderwerp beantwoorden.
* Als u slechts de abonnementsnaam verstrekt, dan toont de interface alle onderwerp-abonnement paren die aan de verstrekte abonnementsnaam beantwoorden.
* Als zowel het onderwerp als de abonnementsnamen worden verstrekt, dan toont de interface het onderwerp-abonnement paar dat met beide verstrekte waarden beantwoordt.

![De uitgezochte gegevensstap van het bronwerkschema met onderwerp en op abonnement-gebaseerde authentificatie.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding gemaakt tussen uw [!DNL PubSub] account en platform. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om streaminggegevens van uw cloudopslag over te brengen naar Platform](../../dataflow/streaming/cloud-storage-streaming.md).
