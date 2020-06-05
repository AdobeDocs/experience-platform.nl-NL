---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Azure Blob- of Amazon S3-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 9fd00ec198f61843bb9a395103215e5441b23745
workflow-type: tm+mt
source-wordcount: '644'
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

Als u toegang wilt tot uw blob-opslag op Platform, moet u een geldige waarde opgeven voor de volgende referentie:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die is vereist voor toegang tot gegevens in de blob-opslag. Het patroon van de Blob-verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Voor meer informatie over aan de slag gaan, bezoek [dit Azure Blob-document](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

Op dezelfde manier vereist de toegang tot van uw S3 emmertje op Platform u om uw geldige waarden voor de volgende geloofsbrieven te verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `s3AccessKey` | De toegangs belangrijkste identiteitskaart voor uw S3 opslag. |
| `s3SecretKey` | De geheime zeer belangrijke identiteitskaart voor uw S3 opslag. |

Ga naar [dit AWS-document](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/)voor meer informatie over aan de slag gaan.

## Sluit uw Blob- of S3-account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe Blob- of S3-account te maken voor verbinding met Platform.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *[!UICONTROL Bronnen]* . In het scherm *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven waarmee u een binnenkomende account kunt maken. Elke bron toont het aantal bestaande accounts en gegevensstromen dat aan deze accounts is gekoppeld.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie *[!UICONTROL Databases]* de optie **[!UICONTROL Azure Blob Storage]** of **[!UICONTROL Amazon S3]** en klik **op het +-pictogram (+)** om een nieuwe Blob- of S3-connector te maken.

![catalogus](../../../../images/tutorials/create/blob/catalog.png)

De pagina *[!UICONTROL Connect to Azure Blob Storage]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef op het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw Blob- of S3-referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/blob/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Blob- of S3-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/blob/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw Blob- of S3-account. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag over te brengen naar Platform](../../dataflow/batch/cloud-storage.md).