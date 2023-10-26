---
title: Een SFTP-bronverbinding maken in de gebruikersinterface
description: Leer hoe u een SFTP-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: e92471b386b857fc21947d352f1c1b88431c68bc
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Een [!DNL SFTP] bronverbinding in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL SFTP] bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

>[!IMPORTANT]
>
>Het wordt aanbevolen nieuwe regels of regeleinden te vermijden bij het innemen van JSON-objecten met een [!DNL SFTP] bronverbinding. Als u de beperking wilt omzeilen, gebruikt u één JSON-object per regel en gebruikt u meerdere regels voor het uitvoeren van bestanden.

Als u al een geldige [!DNL SFTP] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Als u verbinding wilt maken met [!DNL SFTP]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of IP adres verbonden aan uw [!DNL SFTP] server. |
| `port` | De [!DNL SFTP] serverpoort waarmee u verbinding maakt. Indien niet opgegeven, wordt de waarde standaard ingesteld op `22`. |
| `username` | De gebruikersnaam met toegang tot uw [!DNL SFTP] server. |
| `password` | Het wachtwoord voor uw [!DNL SFTP] server. |
| `privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |
| `maxConcurrentConnections` | Met deze parameter kunt u een maximumlimiet opgeven voor het aantal gelijktijdige verbindingen dat Platform maakt wanneer verbinding wordt gemaakt met uw SFTP-server. U moet deze waarde instellen op een waarde die kleiner is dan de limiet die door SFTP is ingesteld. **Opmerking**: Wanneer deze instelling is ingeschakeld voor een bestaande SFTP-account, heeft deze alleen invloed op toekomstige gegevensstromen en niet op bestaande gegevensstromen. |
| Mappad | Het pad naar de map waartoe u toegang wilt verlenen. [!DNL SFTP] bron, kunt u het omslagweg verstrekken om gebruikerstoegang tot de subomslag van uw keus te specificeren. |

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om een nieuwe [!DNL SFTP] account voor verbinding met Platform.

## Verbinding maken met uw [!DNL SFTP] server

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Cloud storage] categorie, selecteert u **[!UICONTROL SFTP]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De Experience Platform bronnen catalogus met de geselecteerde bron SFTP.](../../../../images/tutorials/create/sftp/catalog.png)

De **[!UICONTROL Connect to SFTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP- of SFTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om verder te gaan.

![Een lijst met bestaande SFTP-accounts in de gebruikersinterface van het Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nieuwe account

>[!TIP]
>
>* Nadat u een verificatietype hebt gemaakt, kunt u dit type van een [!DNL SFTP] basisverbinding. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.
>
>* SFTP steunt een RSA of DSA type OpenSSH sleutel. Zorg ervoor dat de inhoud van uw sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"`. Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam en een optionele beschrijving voor uw nieuwe [!DNL SFTP] account.

![Het nieuwe accountscherm voor SFTP](../../../../images/tutorials/create/sftp/new.png)

De [!DNL SFTP] de bron steunt zowel basisauthentificatie als authentificatie via SSH openbare sleutel.

>[!BEGINTABS]

>[!TAB Basisverificatie]

Als u basisverificatie wilt gebruiken, selecteert u **[!UICONTROL Password]** en geef vervolgens de host- en poortwaarden op waarmee u verbinding wilt maken, naast uw gebruikersnaam en wachtwoord. Tijdens deze stap kunt u ook het pad naar de submap aangeven waartoe u toegang wilt verlenen. Selecteer **[!UICONTROL Connect to source]**.

![Het nieuwe accountscherm voor de SFTP-bron met behulp van basisverificatie](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH-verificatie met openbare sleutel]

Als u SSH-gebruikersgegevens op basis van openbare sleutels wilt gebruiken, selecteert u **[!UICONTROL SSH public key]**  en geef vervolgens uw host- en poortwaarden op, evenals de inhoud van de persoonlijke sleutel en de combinatie van passphrase. Tijdens deze stap kunt u ook het pad naar de submap aangeven waartoe u toegang wilt verlenen. Selecteer **[!UICONTROL Connect to source]**.

![Het nieuwe accountscherm voor de SFTP-bron met behulp van SSH public key.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw SFTP-account tot stand gebracht. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar het platform te brengen](../../dataflow/batch/cloud-storage.md).
