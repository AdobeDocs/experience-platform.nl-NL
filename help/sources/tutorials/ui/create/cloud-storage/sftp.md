---
keywords: Experience Platform;home;populaire onderwerpen;SFTP;sftp
solution: Experience Platform
title: Een SFTP-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een SFTP-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ade0da445b18108a7f8720404cc7a65139ed42b1
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Een [!DNL SFTP]-bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL SFTP]-bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

>[!IMPORTANT]
>
>Het wordt aanbevolen nieuwe regels of regeleinden te vermijden bij het opnemen van JSON-objecten met een [!DNL SFTP]-bronverbinding. Als u de beperking wilt omzeilen, gebruikt u één JSON-object per regel en gebruikt u meerdere regels voor het uitvoeren van bestanden.

Als u al een geldige [!DNL SFTP] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [vormend een dataflow](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Als u verbinding wilt maken met [!DNL SFTP], moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP adres verbonden aan uw [!DNL SFTP] server. |
| `port` | De [!DNL SFTP] serverpoort waarmee u verbinding maakt. Als deze waarde niet wordt opgegeven, wordt de standaardwaarde `22` gebruikt. |
| `username` | De gebruikersnaam met toegang tot uw [!DNL SFTP]-server. |
| `password` | Het wachtwoord voor uw [!DNL SFTP]-server. |
| `privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om een nieuwe [!DNL SFTP]-account te maken waarmee u verbinding kunt maken met het Platform.

## Verbinding maken met uw [!DNL SFTP]-server

Selecteer **[!UICONTROL Sources]** in de gebruikersinterface van het Platform in de linkernavigatiebalk voor toegang tot de werkruimte [!UICONTROL Sources]. Het scherm [!UICONTROL Catalog] toont een verscheidenheid van bronnen waarvoor u een binnenkomende rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer [!UICONTROL Cloud storage] onder de categorie **[!UICONTROL SFTP]** en selecteer **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/sftp/catalog.png)

De pagina **[!UICONTROL Connect to SFTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP- of SFTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/sftp/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam en een optionele beschrijving voor uw nieuwe [!DNL SFTP]-account.

#### Verifiëren met wachtwoord

[!DNL SFTP] ondersteunt verschillende verificatietypen voor toegang. Selecteer **[!UICONTROL Account authentication]** onder **[!UICONTROL Password]** en geef de host- en poortwaarden op waarmee u verbinding wilt maken, naast uw gebruikersnaam en wachtwoord.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

#### Verifiëren met SSH-openbare sleutel

Om openbare op sleutel-gebaseerde geloofsbrieven van SSH te gebruiken, selecteer **[!UICONTROL SSH public key]** en verstrek dan uw gastheer en havenwaarden, evenals uw privé zeer belangrijke inhoud en passphrase combinatie.

>[!IMPORTANT]
>
>SFTP steunt een RSA of DSA type OpenSSH sleutel. Zorg ervoor dat de inhoud van het sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"`. Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh-public-key.png)

| Credentials | Beschrijving |
| ---------- | ----------- |
| Persoonlijke toetsinhoud | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| Passphrase | Hiermee geeft u de woordgroep of het wachtwoord op waarmee de persoonlijke sleutel wordt gedecodeerd als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw SFTP-account tot stand gebracht. U kunt nu verdergaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).
