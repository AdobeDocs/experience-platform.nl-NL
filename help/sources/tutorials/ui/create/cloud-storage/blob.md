---
title: Een Azure Blob Source Connection maken in de gebruikersinterface
description: Leer hoe u een Azure Blob-bronconnector kunt maken via de gebruikersinterface van het Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 1%

---

# Een [!DNL Azure Blob] bronverbinding in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Azure Blob] (hierna &quot;[!DNL Blob]&quot;) bronverbinding via de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader voor het organiseren van de gegevens van de klantenervaring in Experience Platform.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Blob] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

Experience Platform ondersteunt de volgende bestandsindelingen die door externe opslagmedia moeten worden ingevoerd:

* Door scheidingstekens gescheiden waarden (DSV): U kunt elk scheidingsteken voor één kolom gebruiken, zoals een tab, komma, pipe, puntkomma of hash, om platte bestanden in elke gewenste indeling te verzamelen.
* JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Blob] opslag op Platform, moet u een geldige waarde voor de volgende referentie verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Verbindingstekenreeks | Een tekenreeks die de verificatiegegevens bevat die nodig zijn voor verificatie [!DNL Blob] naar Experience Platform. De [!DNL Blob] patroon verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Zie deze voor meer informatie over verbindingstekenreeksen [!DNL Blob] document op [verbindingstekenreeksen configureren](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| SAS-URI | De URI van de handtekening voor gedeelde toegang die u kunt gebruiken als alternatief verificatietype om uw [!DNL Blob] account. De [!DNL Blob] SAS URI-patroon is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Zie deze voor meer informatie [!DNL Blob] document op [handtekening-URI&#39;s voor gedeelde toegang](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Container | De naam van de container waartoe u toegang wilt toewijzen. Wanneer u een nieuwe account maakt met de [!DNL Blob] bron, kunt u een containernaam verstrekken om gebruikerstoegang tot subomslag van uw keus te specificeren. |
| Mappad | Het pad naar de map waartoe u toegang wilt verlenen. |

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Blob] aan Platform.

## Verbind uw [!DNL Blob] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Cloud storage] categorie, selecteert u **[!UICONTROL Azure Blob Storage]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De catalogus met bronnen van het Experience Platform waarbij de Azure Blob Storage-bron is geselecteerd.](../../../../images/tutorials/create/blob/catalog.png)

De **[!UICONTROL Connect to Azure Blob Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL Blob] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/blob/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam en een optionele beschrijving voor uw nieuwe [!DNL Blob] account.

![Het nieuwe accountscherm voor de Azure Blob Storage-bron.](../../../../images/tutorials/create/blob/new.png)

De [!DNL Blob] De bron ondersteunt zowel accountverificatie als verificatie met gedeelde toegangshandtekeningen (SAS). Voor verificatie is een verbindingstekenreeks vereist voor verificatie op basis van een account, terwijl een SAS-verificatie gebruikmaakt van een URI die veilige gedelegeerde autorisatie van uw account toestaat.

Tijdens deze stap kunt u ook de submappen aangeven waartoe uw account toegang heeft door de naam van de container en het pad naar de submap te definiëren.

>[!BEGINTABS]

>[!TAB Verbindingstekenreeks]

Selecteer **[!UICONTROL Account key authentication]** en geef uw verbindingstekenreeks op. Tijdens deze stap kunt u ook de containernaam en het pad naar de submap aangeven waartoe u toegang wilt. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]**.

![verbindingstekenreeks](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS-URI]

Met SAS kunt u verificatiereferenties maken met verschillende toegangsgraden, aangezien een SAS-gebaseerde verificatie u in staat stelt machtigingen, begin- en vervaldatums en bepalingen voor specifieke bronnen in te stellen.

Als u wilt verifiëren met een handtekening voor gedeelde toegang, selecteert u **[!UICONTROL Shared access signature authentication]** en geef vervolgens uw SAS-URI op. Tijdens deze stap kunt u ook de containernaam en het pad naar de submap aangeven waartoe u toegang wilt. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Blob] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).
