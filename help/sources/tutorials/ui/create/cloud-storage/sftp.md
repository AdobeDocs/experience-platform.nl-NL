---
keywords: Experience Platform;home;populaire onderwerpen;SFTP;sftp
solution: Experience Platform
title: Een SFTP-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een SFTP-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: bf665a0041db8a44c39c787bb1f0f1100f61e135
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 0%

---

# Een [!DNL SFTP] bronverbinding in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL SFTP] bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

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
| `maxConcurrentConnections` | Met deze parameter kunt u een maximumlimiet opgeven voor het aantal gelijktijdige verbindingen dat Platform maakt wanneer verbinding wordt gemaakt met uw SFTP-server. U moet deze waarde instellen op een waarde die kleiner is dan de limiet die door SFTP is ingesteld. **Opmerking**: Als deze instelling is ingeschakeld voor een bestaande SFTP-account, heeft dit alleen invloed op toekomstige gegevensstromen en niet op bestaande gegevensstromen. |

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om een nieuwe [!DNL SFTP] account om verbinding te maken met Platform.

## Verbinding maken met uw [!DNL SFTP] server

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] het scherm toont een verscheidenheid van bronnen waarvoor u een binnenkomende rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Cloud storage] categorie, selecteert u **[!UICONTROL SFTP]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De Experience Platform bronnen catalogus met de geselecteerde bron SFTP.](../../../../images/tutorials/create/sftp/catalog.png)

De **[!UICONTROL Connect to SFTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP- of SFTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om verder te gaan.

![Een lijst met bestaande SFTP-accounts in de gebruikersinterface van het Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam en een optionele beschrijving voor uw nieuwe [!DNL SFTP] account.

![Het nieuwe accountscherm voor SFTP](../../../../images/tutorials/create/sftp/new.png)

#### Verifiëren met wachtwoord

[!DNL SFTP] ondersteunt verschillende verificatietypen voor toegang. Onder **[!UICONTROL Account authentication]** selecteren **[!UICONTROL Password]** en geef vervolgens de host- en poortwaarden op waarmee u verbinding wilt maken, naast uw gebruikersnaam en wachtwoord.

![Het nieuwe accountscherm voor de SFTP-bron met behulp van basisverificatie](../../../../images/tutorials/create/sftp/password.png)

#### Verifiëren met SSH-openbare sleutel

Als u SSH-gebruikersgegevens op basis van openbare sleutels wilt gebruiken, selecteert u **[!UICONTROL SSH public key]**  en geef vervolgens uw host- en poortwaarden op, evenals de inhoud van de persoonlijke sleutel en de combinatie van passphrase.

>[!IMPORTANT]
>
>SFTP steunt een RSA of DSA type OpenSSH sleutel. Zorg ervoor dat de inhoud van uw sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"`. Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

![Het nieuwe accountscherm voor de SFTP-bron met behulp van SSH public key.](../../../../images/tutorials/create/sftp/ssh.png)

| Credentials | Beschrijving |
| ---------- | ----------- |
| Persoonlijke toetsinhoud | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| Passphrase | Hiermee geeft u de woordgroep of het wachtwoord op waarmee de persoonlijke sleutel wordt gedecodeerd als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw SFTP-account tot stand gebracht. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).
