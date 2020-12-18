---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: Een SFTP-bronconnector maken in de UI
topic: overview
type: Tutorial
description: Deze zelfstudie biedt stappen voor het maken van een SFTP-bronconnector met behulp van de gebruikersinterface van het Platform.
translation-type: tm+mt
source-git-commit: 0d0d3aa4213f3a8252de82c47eef6e9caa4d3e9e
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---


# Een SFTP-bronconnector maken in de UI

>[!NOTE]
>
>De SFTP-connector bevindt zich in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie biedt stappen voor het maken van een SFTP-bronconnector met behulp van de gebruikersinterface van het Platform.

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
| `privateKeyContent` | De Base64-gecodeerde SSH-inhoud voor persoonlijke sleutels. De OpenSSH-indeling (RSA/DSA) voor de persoonlijke sleutel van SSH. |
| `passPhrase` | De wachtwoordgroep of het wachtwoord voor het decoderen van de persoonlijke sleutel als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe SFTP-account te maken waarmee u verbinding kunt maken met het Platform.

## Verbinding maken met uw SFTP-server

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte [!UICONTROL Bronnen] te openen. Het scherm [!UICONTROL Catalog] toont een verscheidenheid van bronnen waarvoor u een binnenkomende rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL SFTP]** onder de categorie [!UICONTROL Cloudopslag]. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders selecteert u **[!UICONTROL Gegevens toevoegen]** om een nieuwe SFTP-verbinding te maken.

![catalogus](../../../../images/tutorials/create/sftp/catalog.png)

De pagina **[!UICONTROL Verbinding maken met SFTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw referenties in. Selecteer **[!UICONTROL Connect]** als u klaar bent en wacht dan enige tijd tot de nieuwe verbinding tot stand is gebracht.

De schakelaar SFTP verstrekt u verschillende authentificatietypen voor toegang. Selecteer **[!UICONTROL Wachtwoord]** onder **[!UICONTROL Accountverificatie]** om een op een wachtwoord gebaseerde referentie te gebruiken.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Alternatief, kunt u **[SSH openbare sleutel]** selecteren en uw rekening verbinden SFTP gebruikend een combinatie van [!UICONTROL Persoonlijke zeer belangrijke inhoud] en [!UICONTROL Passphrase].

>[!IMPORTANT]
>
>De schakelaar SFTP steunt een sleutel RSA/DSA OpenSSH. Zorg ervoor dat de inhoud van het sleutelbestand begint met `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`. Als het bestand met de persoonlijke sleutel een PPK-bestand is, gebruikt u het gereedschap PuTTY om de PPK-indeling om te zetten in de OpenSSH-indeling.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Credentials | Beschrijving |
| ---------- | ----------- |
| Persoonlijke toetsinhoud | A Base64 encoded SSH private key content. De persoonlijke sleutel van SSH zou OpenSSH formaat moeten zijn. |
| Passphrase | Hiermee geeft u de woordgroep of het wachtwoord op waarmee de persoonlijke sleutel wordt gedecodeerd als het sleutelbestand of de sleutelinhoud wordt beveiligd door een wachtwoordgroep. Als PrivateKeyContent met een wachtwoord beveiligd is, moet deze parameter worden gebruikt met de wachtwoordzin van PrivateKeyContent als waarde. |

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP- of SFTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/sftp/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw FTP- of SFTP-account. U kunt nu verdergaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).