---
keywords: Experience Platform;home;popular topics;SFTP;FTP;ftp;sftp
solution: Experience Platform
title: Een FTP- of SFTP-bronconnector maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Deze zelfstudie biedt stappen voor het maken van een FTP- of SFTP-bronconnector met behulp van de gebruikersinterface van het Platform.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---


# Een FTP- of SFTP-bronconnector maken in de gebruikersinterface

>[!NOTE]
>
>De FTP- en SFTP-connectors bevinden zich in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een FTP- of SFTP-bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige FTP- of SFTP-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

[!DNL Experience Platform] ondersteunt de volgende bestandsindelingen die van externe bronnen moeten worden ingevoerd:

* Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot CSV-bestanden (comma-separated values, door komma&#39;s gescheiden waarden). De waarde van veldkoppen in bestanden met DSV-indeling mag alleen bestaan uit alfanumerieke tekens en onderstrepingstekens. In de toekomst zal steun voor algemene DSV worden verleend.
* JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Als u toegang wilt tot uw FTP- of SFTP-server, moet u de hostnaam, een gebruikersnaam en een wachtwoord van de server opgeven. [!DNL Platform]

## Verbinding maken met uw FTP- of SFTP-server

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe FTP- of SFTP-account te maken waarmee u verbinding kunt maken [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Bronnen]** . In het scherm **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarmee u een binnenkomende account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL SFTP]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders selecteert u Gegevens **** toevoegen om een nieuwe FTP- of SFTP-connector te maken.

![catalogus](../../../../images/tutorials/create/sftp/catalog.png)

De pagina **[!UICONTROL Verbinding maken met SFTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw referenties in. Wanneer u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

De schakelaar SFTP verstrekt u verschillende authentificatietypen voor toegang. Selecteer onder **[!UICONTROL Accountverificatie]** de optie **[!UICONTROL Wachtwoord]** om een op een wachtwoord gebaseerde referentie te gebruiken.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Alternatief, kunt u openbare sleutel **[van]** SSH selecteren en uw rekening verbinden SFTP gebruikend een combinatie **[!UICONTROL Persoonlijke zeer belangrijke inhoud]** en **[!UICONTROL Passphrase]**.

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

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw FTP- of SFTP-account. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag naar [!DNL Platform]](../../dataflow/batch/cloud-storage.md)te brengen.