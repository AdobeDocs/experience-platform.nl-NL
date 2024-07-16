---
title: Een SFTP Source-verbinding maken in de gebruikersinterface
description: Leer hoe u een SFTP-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Een [!DNL SFTP] bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL SFTP] -bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

>[!IMPORTANT]
>
>Het wordt aangeraden nieuwe regels of regeleinden te vermijden bij het invoeren van JSON-objecten met een [!DNL SFTP] -bronverbinding. Als u de beperking wilt omzeilen, gebruikt u één JSON-object per regel en gebruikt u meerdere regels voor het uitvoeren van bestanden.

Als u reeds een geldige [!DNL SFTP] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Als u verbinding wilt maken met [!DNL SFTP] , moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP-adres dat aan de [!DNL SFTP] -server is gekoppeld. |
| `port` | De [!DNL SFTP] serverpoort waarmee u verbinding maakt. Als deze waarde niet wordt opgegeven, wordt deze standaard ingesteld op `22` . |
| `username` | De gebruikersnaam met toegang tot de [!DNL SFTP] -server. |
| `password` | Het wachtwoord voor uw [!DNL SFTP] -server. |
| `privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |
| `maxConcurrentConnections` | Met deze parameter kunt u een maximumlimiet opgeven voor het aantal gelijktijdige verbindingen dat Platform maakt wanneer verbinding wordt gemaakt met uw SFTP-server. U moet deze waarde instellen op een waarde die kleiner is dan de limiet die door SFTP is ingesteld. **Nota**: Wanneer dit het plaatsen voor een bestaande rekening van SFTP wordt toegelaten, zal het slechts toekomstige dataflows en niet bestaande dataflows beïnvloeden. |
| Mappad | Het pad naar de map waartoe u toegang wilt verlenen. [!DNL SFTP] -bron, kunt u het mappad opgeven waarmee u gebruikerstoegang tot de submap van uw keuze kunt opgeven. |

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe [!DNL SFTP] -account te maken voor verbinding met Platform.

## Verbinding maken met uw [!DNL SFTP] -server

Selecteer in de gebruikersinterface van het platform **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL Cloud storage] de optie **[!UICONTROL SFTP]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ de Experience Platform broncatalogus met geselecteerde bron SFTP.](../../../../images/tutorials/create/sftp/catalog.png)

De pagina **[!UICONTROL Connect to SFTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP- of SFTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ een lijst van bestaande rekeningen SFTP op het Experience Platform UI.](../../../../images/tutorials/create/sftp/existing.png)

### Nieuwe account

>[!TIP]
>
>* Nadat u een [!DNL SFTP] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.
>
>* SFTP steunt een RSA of DSA type OpenSSH sleutel. Zorg ervoor dat de inhoud van het sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"` . Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam en een optionele beschrijving voor uw nieuwe [!DNL SFTP] -account.

![ het nieuwe rekeningsscherm voor SFTP ](../../../../images/tutorials/create/sftp/new.png)

De [!DNL SFTP] -bron ondersteunt zowel basisverificatie als verificatie via de openbare SSH-sleutel.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Als u basisverificatie wilt gebruiken, selecteert u **[!UICONTROL Password]** en geeft u de host- en poortwaarden op waarmee u verbinding wilt maken, naast uw gebruikersnaam en wachtwoord. Tijdens deze stap kunt u ook het pad naar de submap aangeven waartoe u toegang wilt verlenen. Selecteer **[!UICONTROL Connect to source]** als u klaar bent.

![ het nieuwe rekeningsscherm voor de bron SFTP die basisauthentificatie gebruiken ](../../../../images/tutorials/create/sftp/password.png)

>[!TAB  SSH openbare zeer belangrijke authentificatie ]

Als u SSH-gebruikersgegevens op basis van openbare sleutels wilt gebruiken, selecteert u **[!UICONTROL SSH public key]** en geeft u vervolgens uw host- en poortwaarden op, evenals de inhoud en wachtwoordgroep van uw persoonlijke sleutel. Tijdens deze stap kunt u ook het pad naar de submap aangeven waartoe u toegang wilt verlenen. Selecteer **[!UICONTROL Connect to source]** als u klaar bent.

![ het nieuwe rekeningsscherm voor de bron SFTP die SSH openbare sleutel gebruikt.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw SFTP-account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens van uw wolkenopslag in Platform ](../../dataflow/batch/cloud-storage.md) te brengen.
