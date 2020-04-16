---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een FTP- of SFTP-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Een FTP- of SFTP-bronconnector maken in de gebruikersinterface

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een FTP- of SFTP-bronconnector met behulp van de gebruikersinterface van het platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige FTP- of SFTP-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/cloud-storage.md).

### Ondersteunde bestandsindelingen

Het Experience Platform ondersteunt de volgende bestandsindelingen die uit externe bronnen kunnen worden ingevoerd:

* Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot CSV-bestanden (comma-separated values, door komma&#39;s gescheiden waarden). De waarde van veldkoppen in bestanden met DSV-indeling mag alleen bestaan uit alfanumerieke tekens en onderstrepingstekens. In de toekomst zal steun voor algemene DSV worden verleend.
* JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Als u toegang wilt tot uw FTP- of SFTP-server op Platform, moet u de **hostnaam** van de server, een **gebruikersnaam** en een **wachtwoord** opgeven.

## Verbinding maken met uw server

Als de referenties van uw server klaar zijn, kunt u de onderstaande stappen volgen om een nieuwe binnenkomende basisverbinding te maken om uw FTP- of SFTP-server te koppelen aan Platform.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte Bronnen. In het scherm *Catalogus* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Selecteer onder de categorie *Cloud Storage* de optie **FTP** of **SFTP** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het weergeven van de documentatie of het maken van een verbinding met de bron. Klik op **Verbindingsbron** om een nieuwe binnenkomende basisverbinding te maken.

![](../../../../images/tutorials/create/sftp/sftp_sources_catalog.png)

Geef in het invoerformulier een naam, een optionele beschrijving en uw FTP- of SFTP-referenties op voor de basisverbinding. Klik ten slotte op **Verbinden** en laat enige tijd de nieuwe basisverbinding tot stand brengen.

![](../../../../images/tutorials/create/sftp/sftp_credentials.png)

Zodra een basisverbinding met uw FTP of server SFTP wordt gevestigd, kunt u op de volgende sectie verdergaan en een dataflow vormen om gegevens in Platform te brengen.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw FTP- of SFTP-server. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/cloud-storage.md).
