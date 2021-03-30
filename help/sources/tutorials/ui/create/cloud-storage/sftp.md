---
keywords: Experience Platform;home;populaire onderwerpen;SFTP;sftp
solution: Experience Platform
title: Een SFTP-bronverbinding maken in de gebruikersinterface
topic: overzicht
type: Tutorial
description: Leer hoe u een SFTP-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
translation-type: tm+mt
source-git-commit: 0e11acc4a599d360cb3048445003f61848ad23d3
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---


# Een SFTP-bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een SFTP-bronverbinding met de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

>[!IMPORTANT]
>
>Het wordt aanbevolen nieuwe regels of regeleinden te vermijden bij het opnemen van JSON-objecten met een SFTP-bronverbinding. Als u de beperking wilt omzeilen, gebruikt u één JSON-object per regel en gebruikt u meerdere regels voor het uitvoeren van bestanden.

Als u reeds een geldige verbinding SFTP hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Als u verbinding wilt maken met SFTP, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP-adres dat aan uw SFTP-server is gekoppeld. |
| `username` | De gebruikersnaam met toegang tot uw SFTP-server. |
| `password` | Het wachtwoord voor uw SFTP-server. |
| `privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe SFTP-account te maken waarmee u verbinding kunt maken met het Platform.

## Verbinding maken met uw SFTP-server

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte [!UICONTROL Sources] te openen. Het scherm [!UICONTROL Catalog] toont een verscheidenheid van bronnen waarvoor u een binnenkomende rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL SFTP]** onder de categorie [!UICONTROL Cloud storage]. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL Configure]**. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe SFTP-verbinding te maken.

![catalogus](../../../../images/tutorials/create/sftp/catalog.png)

De pagina **[!UICONTROL Connect to SFTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw referenties in. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

De schakelaar SFTP verstrekt u verschillende authentificatietypen voor toegang. Selecteer **[!UICONTROL Account authentication]** onder **[!UICONTROL Password]** om een op een wachtwoord gebaseerde referentie te gebruiken.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

U kunt ook **[SSH public key]** selecteren en uw SFTP-account aansluiten met een combinatie van [!UICONTROL Private key content] en [!UICONTROL Passphrase].

>[!IMPORTANT]
>
>De schakelaar SFTP steunt een sleutel van RSA of van het type DSA OpenSSH. Zorg ervoor dat de inhoud van het sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` en eindigt met `"-----END [RSA/DSA] PRIVATE KEY-----"`. Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Credentials | Beschrijving |
| ---------- | ----------- |
| Persoonlijke toetsinhoud | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. Het type van sleutel OpenSSH moet als of RSA of DSA worden geclassificeerd. |
| Passphrase | Hiermee geeft u de woordgroep of het wachtwoord op waarmee de persoonlijke sleutel wordt gedecodeerd als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP- of SFTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/sftp/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw FTP- of SFTP-account. U kunt nu verdergaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).