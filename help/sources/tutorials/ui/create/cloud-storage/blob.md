---
keywords: Experience Platform;home;populaire onderwerpen;Azure Blob;azure blob;Azure blob-connector
solution: Experience Platform
title: Een Azure Blob Source Connection maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Azure Blob-bronconnector kunt maken via de gebruikersinterface van het Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Een [!DNL Azure Blob]-bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Azure Blob] (hierna &quot;[!DNL Blob]&quot; genoemd) met behulp van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Blob] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [vormend een dataflow](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

[!DNL Experience Platform] ondersteunt de volgende bestandsindelingen die door externe opslagmedia moeten worden ingevoerd:

- Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot door komma&#39;s gescheiden waarden. De waarde van veldkoppen in bestanden met DSV-indeling mag alleen bestaan uit alfanumerieke tekens en onderstrepingstekens. Algemene DSV-bestanden worden in de toekomst ondersteund.
- JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
- Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Blob]-opslagruimte op het Platform, moet u een geldige waarde opgeven voor de volgende referentie:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | Een tekenreeks die de machtigingsgegevens bevat die nodig zijn om [!DNL Blob] te verifiëren bij Experience Platform. Het patroon van de [!DNL Blob] verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Voor meer informatie over verbindingskoorden, zie dit [!DNL Blob] document op [vormend verbindingskoorden](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | De URI van de handtekening voor gedeelde toegang die u kunt gebruiken als alternatief verificatietype om uw [!DNL Blob]-account aan te sluiten. Het [!DNL Blob] SAS URI-patroon is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Voor meer informatie, zie dit [!DNL Blob] document op [gedeelde toegangshandtekening URIs](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Uw [!DNL Blob]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Blob]-account te koppelen aan het Platform.

In [Platform UI](https://platform.adobe.com), selecteer **[!UICONTROL Sources]** van de linkernavigatiebar om tot de [!UICONTROL Sources] werkruimte toegang te hebben. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer [!UICONTROL Cloud storage] onder de categorie **[!UICONTROL Azure Blob Storage]** en selecteer **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/blob/catalog.png)

De pagina **[!UICONTROL Connect to Azure Blob Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Blob]-account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/blob/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een naam en een optiebeschrijving voor uw nieuwe [!DNL Blob]-account.

**Verifiëren met een verbindingstekenreeks**

De [!DNL Blob] schakelaar voorziet u van verschillende authentificatietypen voor toegang. Selecteer [!UICONTROL Account authentication] onder **[!UICONTROL ConnectionString]** om referenties te gebruiken die zijn gebaseerd op een verbindingstekenreeks.

![verbindingstekenreeks](../../../../images/tutorials/create/blob/connectionstring.png)

**Verifiëren met URI voor een handtekening voor gedeelde toegang**

Een gedeelde toegangshandtekening (SAS) URI staat veilige gedelegeerde autorisatie toe aan uw [!DNL Blob]-account. Met SAS kunt u verificatiereferenties maken met verschillende toegangsgraden, aangezien een SAS-gebaseerde verificatie u in staat stelt machtigingen, begin- en vervaldatums en bepalingen voor specifieke bronnen in te stellen.

Selecteer **[!UICONTROL SasURIAuthentication]** en geef vervolgens uw [!DNL Blob] SAS-URI op. Selecteer **[!UICONTROL Connect to source]** om door te gaan.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Blob]-account. U kunt nu verdergaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).
