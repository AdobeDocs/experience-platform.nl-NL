---
title: Een SFTP Source-verbinding maken in de gebruikersinterface
description: Leer hoe u een SFTP-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Een [!DNL SFTP] bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL SFTP] -bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

>[!IMPORTANT]
>
>Het wordt aangeraden nieuwe regels of regeleinden te vermijden bij het invoeren van JSON-objecten met een [!DNL SFTP] -bronverbinding. Als u de beperking wilt omzeilen, gebruikt u één JSON-object per regel en gebruikt u meerdere regels voor het uitvoeren van bestanden.

Als u reeds een geldige [!DNL SFTP] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Lees de [[!DNL SFTP]  authentificatiegids &#x200B;](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) voor gedetailleerde stappen op hoe te om uw authentificatiegeloofsbrieven terug te winnen.

## Verbinding maken met uw [!DNL SFTP] -server

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL Cloud storage] de optie **[!UICONTROL SFTP]** en selecteer vervolgens **[!UICONTROL Add data]** .

![&#x200B; de de broncatalogus van Experience Platform met geselecteerde bron SFTP.](../../../../images/tutorials/create/sftp/catalog.png)

De pagina **[!UICONTROL Connect to SFTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP- of SFTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![&#x200B; een lijst van bestaande rekeningen SFTP op Experience Platform UI.](../../../../images/tutorials/create/sftp/existing.png)

### Nieuwe account

>[!TIP]
>
>* Nadat u een [!DNL SFTP] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.
>
>* SFTP biedt ondersteuning voor het type `ed25519` , `RSA` of `DSA` OpenSSH-toets. Zorg ervoor dat de inhoud van het sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"` . Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam en een optionele beschrijving voor uw nieuwe [!DNL SFTP] -account.

![&#x200B; het nieuwe rekeningsscherm voor SFTP &#x200B;](../../../../images/tutorials/create/sftp/new.png)

De [!DNL SFTP] -bron ondersteunt zowel basisverificatie als verificatie via de openbare SSH-sleutel.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Als u basisverificatie wilt gebruiken, selecteert u **[!UICONTROL Password]** en geeft u de juiste waarden op voor de volgende referenties:

* host
* poort
* gebruikersnaam
* password

Tijdens deze stap kunt u ook uw maximale gelijktijdige verbindingen configureren, het mappad definiëren en het koppelen voor uw [!DNL SFTP] -server in- of uitschakelen. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

Voor meer informatie over authentificatie, lees de gids over [&#x200B; het verzamelen vereiste geloofsbrieven voor  [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![&#x200B; het nieuwe rekeningsscherm voor de bron SFTP die basisauthentificatie gebruiken &#x200B;](../../../../images/tutorials/create/sftp/password.png)

>[!TAB  SSH openbare zeer belangrijke authentificatie ]

Als u SSH-gebruikersgegevens op basis van openbare sleutels wilt gebruiken, selecteert u **[!UICONTROL SSH public key]** en geeft u de juiste waarden op voor de volgende referenties:

* host
* poort
* gebruikersnaam
* inhoud van persoonlijke sleutel
* passphrase

Tijdens deze stap kunt u ook uw maximale gelijktijdige verbindingen configureren, het mappad definiëren en het koppelen voor uw [!DNL SFTP] -server in- of uitschakelen. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

Voor meer informatie over authentificatie, lees de gids over [&#x200B; het verzamelen vereiste geloofsbrieven voor  [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![&#x200B; het nieuwe rekeningsscherm voor de bron SFTP die SSH openbare sleutel gebruikt.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw SFTP-account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens van uw wolkenopslag in Experience Platform &#x200B;](../../dataflow/batch/cloud-storage.md) te brengen.
