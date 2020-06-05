---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een FTP- of SFTP-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 46b57900d9323cffeb59a0a6250bf5a9f4ac64ab
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---


# Een FTP- of SFTP-bronconnector maken in de gebruikersinterface

>[!NOTE]
>De FTP- en SFTP-connectors bevinden zich in bèta. De functies en documentatie kunnen worden gewijzigd.

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een FTP- of SFTP-bronconnector met behulp van de gebruikersinterface van het platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige FTP- of SFTP-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

Het Experience Platform ondersteunt de volgende bestandsindelingen die uit externe bronnen kunnen worden ingevoerd:

* Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot CSV-bestanden (comma-separated values, door komma&#39;s gescheiden waarden). De waarde van veldkoppen in bestanden met DSV-indeling mag alleen bestaan uit alfanumerieke tekens en onderstrepingstekens. In de toekomst zal steun voor algemene DSV worden verleend.
* JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Als u toegang wilt tot uw FTP- of SFTP-server op Platform, moet u de **hostnaam** van de server, een **gebruikersnaam** en een **wachtwoord** opgeven.

## Verbinding maken met uw FTP- of SFTP-server

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe FTP- of SFTP-account te maken waarmee u verbinding kunt maken met Platform.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *[!UICONTROL Bronnen]* . In het scherm *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven waarmee u een binnenkomende account kunt maken. Elke bron toont het aantal bestaande accounts en gegevensstromen dat aan deze accounts is gekoppeld.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie *[!UICONTROL Databases]* de optie **[!UICONTROL SFTP]** en klik **op het pictogram + (+)** om een nieuwe FTP- of SFTP-connector te maken.

![catalogus](../../../../images/tutorials/create/sftp/catalog.png)

De pagina *[!UICONTROL Verbinding maken met SFTP]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw FTP- of SFTP-referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/sftp/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP- of SFTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/sftp/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw FTP- of SFTP-account. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag over te brengen naar Platform](../../dataflow/batch/cloud-storage.md).