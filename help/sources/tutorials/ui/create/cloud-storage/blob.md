---
title: Een Azure Blob Source Connection maken in de gebruikersinterface
description: Leer hoe u een Azure Blob-bronconnector kunt maken via de Experience Platform-gebruikersinterface.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Een [!DNL Azure Blob] bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Azure Blob] (hierna &quot;[!DNL Blob]&quot; genoemd) bronverbinding met de Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader voor het organiseren van de gegevens van de klantenervaring in Experience Platform.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Blob] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

Experience Platform ondersteunt de volgende bestandsindelingen die door externe opslagmedia moeten worden ingevoerd:

* DSV (Delimiter-separated values, door scheidingstekens gescheiden waarden): u kunt elke scheidingsteken voor één kolom gebruiken, zoals een tab, komma, pipe, puntkomma of hash, om platte bestanden in elke gewenste indeling te verzamelen.
* JavaScript Object Notation (JSON): gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Als u toegang wilt tot [!DNL Blob] -opslag op Experience Platform, moet u geldige waarden opgeven voor de volgende referenties:

>[!BEGINTABS]

>[!TAB  het koordauthentificatie van de Verbinding ]

| Credentials | Beschrijving |
| --- | --- |
| Verbindingstekenreeks | Een tekenreeks die de machtigingsgegevens bevat die nodig zijn voor verificatie van [!DNL Blob] naar Experience Platform. Het patroon van de [!DNL Blob] verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}` . Voor meer informatie over verbindingskoorden, zie dit [!DNL Blob] document op [ vormend verbindingskoorden ](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |

>[!TAB  de authentificatie van SAS URI ]

| Credentials | Beschrijving |
| --- | --- |
| SAS-URI | De URI van de handtekening voor gedeelde toegang die u kunt gebruiken als alternatief verificatietype om uw [!DNL Blob] -account te verbinden. Het [!DNL Blob] patroon van SAS URI is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` voor meer informatie, zie dit [!DNL Blob] document op [ gedeelde toegangshandtekening URIs ](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Container | De naam van de container die u toegang tot wilt aanwijzen. Wanneer u een nieuw account maakt met de [!DNL Blob] -bron, kunt u een containernaam opgeven om gebruikerstoegang tot de submap van uw keuze op te geven. |
| Mappad | Het pad naar de map waartoe u toegang wilt verlenen. |

>[!ENDTABS]

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Blob] -opslaggegevens te verbinden met Experience Platform

## Sluit uw [!DNL Blob] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer onder de categorie [!UICONTROL Cloud storage] de optie **[!UICONTROL Azure Blob Storage]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ de de broncatalogus van Experience Platform met de Azure Blob geselecteerde bron van de Opslag.](../../../../images/tutorials/create/blob/catalog.png)

De pagina **[!UICONTROL Connect to Azure Blob Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Blob] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/blob/existing.png)

### Nieuwe account

>[!TIP]
>
>Nadat u een [!DNL Blob] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam en een optionele beschrijving voor uw nieuwe [!DNL Blob] -account.

![ het nieuwe rekeningsscherm voor de bron van de Opslag van Azure Blob.](../../../../images/tutorials/create/blob/new.png)

De [!DNL Blob] -bron ondersteunt zowel verificatie met accountsleutels als verificatie met gedeelde toegangshandtekeningen (SAS). Voor verificatie is een verbindingstekenreeks vereist voor verificatie op basis van een account, terwijl een SAS-verificatie gebruikmaakt van een URI die veilige gedelegeerde autorisatie van uw account toestaat.

Tijdens deze stap kunt u ook de submappen aangeven waartoe uw account toegang heeft door de naam van de container en het pad naar de submap te definiëren.

>[!BEGINTABS]

>[!TAB  Koord van de Verbinding ]

Selecteer **[!UICONTROL Account key authentication]** en geef uw verbindingstekenreeks op om verificatie met een accountsleutel uit te voeren. Tijdens deze stap kunt u ook de containernaam en het pad naar de submap aangeven waartoe u toegang wilt. Selecteer **[!UICONTROL Connect to source]** als u klaar bent.

![ verbindingskoord ](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB  SAS URI ]

Met SAS kunt u verificatiereferenties maken met verschillende toegangsgraden, aangezien een SAS-gebaseerde verificatie u in staat stelt machtigingen, begin- en vervaldatums en bepalingen voor specifieke bronnen in te stellen.

Als u wilt verifiëren met een handtekening voor gedeelde toegang, selecteert u **[!UICONTROL Shared access signature authentication]** en geeft u uw SAS-URI op. Tijdens deze stap kunt u ook de containernaam en het pad naar de submap aangeven waartoe u toegang wilt. Selecteer **[!UICONTROL Connect to source]** als u klaar bent.

![ sas-uri ](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Blob] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens van uw wolkenopslag in Experience Platform ](../../dataflow/batch/cloud-storage.md) te brengen.
