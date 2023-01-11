---
keywords: Experience Platform;home;populaire onderwerpen;Azure Blob;azure blob;Azure blob-connector
solution: Experience Platform
title: Een Azure Blob Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Azure Blob-bronconnector kunt maken via de gebruikersinterface van het Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Een [!DNL Azure Blob] bronverbinding in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Azure Blob] (hierna &quot;[!DNL Blob]&quot;) gebruiken van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Blob] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

[!DNL Experience Platform] ondersteunt de volgende bestandsindelingen die door externe opslagmedia moeten worden ingevoerd:

- Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot door komma&#39;s gescheiden waarden. De waarde van veldkoppen in bestanden met DSV-indeling mag alleen bestaan uit alfanumerieke tekens en onderstrepingstekens. Algemene DSV-bestanden worden in de toekomst ondersteund.
- JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
- Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Blob] opslag op Platform, moet u een geldige waarde voor de volgende referentie verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | Een tekenreeks die de verificatiegegevens bevat die nodig zijn voor verificatie [!DNL Blob] naar Experience Platform. De [!DNL Blob] patroon verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Zie deze voor meer informatie over verbindingstekenreeksen [!DNL Blob] document op [verbindingstekenreeksen configureren](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | De URI van de handtekening voor gedeelde toegang die u kunt gebruiken als alternatief verificatietype om uw [!DNL Blob] account. De [!DNL Blob] SAS URI-patroon is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Zie deze voor meer informatie [!DNL Blob] document op [handtekening-URI&#39;s voor gedeelde toegang](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Verbind uw [!DNL Blob] account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Blob] aan Platform.

In de [UI Platform](https://platform.adobe.com), selecteert u **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Cloud storage] categorie, selecteert u **[!UICONTROL Azure Blob Storage]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/blob/catalog.png)

De **[!UICONTROL Connect to Azure Blob Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL Blob] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/blob/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam en een beschrijving van de optie voor uw nieuwe [!DNL Blob] account.

**Verifiëren met een verbindingstekenreeks**

De [!DNL Blob] de schakelaar voorziet u van verschillende authentificatietypen voor toegang. Onder [!UICONTROL Account authentication] selecteren **[!UICONTROL ConnectionString]** als u referenties wilt gebruiken die zijn gebaseerd op een verbindingstekenreeks.

![verbindingstekenreeks](../../../../images/tutorials/create/blob/connectionstring.png)

**Verifiëren met URI voor een handtekening voor gedeelde toegang**

Een gedeelde toegangshandtekening (SAS) URI staat veilige gedelegeerde toestemming aan uw toe [!DNL Blob] account. Met SAS kunt u verificatiereferenties maken met verschillende toegangsgraden, aangezien een SAS-gebaseerde verificatie u in staat stelt machtigingen, begin- en vervaldatums en bepalingen voor specifieke bronnen in te stellen.

Selecteren **[!UICONTROL SasURIAuthentication]** en vervolgens uw [!DNL Blob] SAS-URI. Selecteren **[!UICONTROL Connect to source]** om verder te gaan.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Blob] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).
