---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Azure Blob- of Amazon S3-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 799445eca080175e2bffc49c6714f0c812b9bbea
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# Een Azure Blob- of Amazon S3-bronconnector maken in de gebruikersinterface

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een Azure Blob (hierna &quot;Blob&quot; genoemd)- of Amazon S3-bronconnector (hierna &quot;S3&quot; genoemd) via de gebruikersinterface van Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

- [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een Blob of S3 basisverbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

Het Experience Platform ondersteunt de volgende bestandsindelingen die in externe opslagruimten kunnen worden opgenomen:

- Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot door komma&#39;s gescheiden waarden. De waarde van veldkoppen in bestanden met DSV-indeling mag alleen bestaan uit alfanumerieke tekens en onderstrepingstekens. Algemene DSV-bestanden worden in de toekomst ondersteund.
- JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
- Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Als u toegang wilt tot uw blob-opslag op Platform, moet u een geldige **Azure Storage-verbindingstekenreeks** opgeven. U kunt meer over verbindingskoorden leren met inbegrip van manieren om hen door <a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string" target="_blank">dit document</a>van Microsoft Azure te verkrijgen.

Op dezelfde manier vereist de toegang tot van uw S3 emmertje op Platform u uw Sleutel **van de Toegang** S3 en **S3 Geheime Sleutel** te verstrekken. Raadpleeg <a href="https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/" target="_blank">dit AWS-document</a>voor meer informatie.

## Sluit uw Blob- of S3-account aan

Met de gegevens voor uw cloudopslag kunt u de onderstaande stappen volgen om een nieuwe binnenkomende basisverbinding te maken waarmee uw Blob- of S3-account aan Platform wordt gekoppeld.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte Bronnen. In het scherm *Catalogus* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Selecteer onder de categorie *Cloud Storage* de optie **Azure Blob Storage** of **Amazon S3** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het weergeven van de documentatie of het maken van een verbinding met de bron. Klik op **Verbindingsbron** om een nieuwe binnenkomende basisverbinding te maken.

![](../../../../images/tutorials/create/s3/s3_sources_catalog.png)

Geef in het invoerformulier een naam, een optionele beschrijving en uw Blob- of S3-referenties op voor de basisverbinding. Klik ten slotte op **Verbinden** en laat enige tijd de nieuwe basisverbinding tot stand brengen.

![](../../../../images/tutorials/create/s3/s3_credentials.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een basisverbinding tot stand gebracht met uw Azure Blob- of Amazon S3-account. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/batch/cloud-storage.md).