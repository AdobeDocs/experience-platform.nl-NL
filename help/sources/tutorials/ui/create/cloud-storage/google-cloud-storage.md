---
title: Een Google Cloud Storage Source Connection maken in de gebruikersinterface
description: Leer hoe u een Google Cloud Storage-bronverbinding maakt met de Adobe Experience Platform-interface.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---

# Een [!DNL Google Cloud Storage] bronverbinding in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Google Cloud Storage] bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Google Cloud Storage] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

[!DNL Experience Platform] ondersteunt de volgende bestandsindelingen die door externe opslagmedia moeten worden ingevoerd:

* Door scheidingstekens gescheiden waarden (DSV): Elke waarde van één teken kan worden gebruikt als scheidingsteken voor gegevensbestanden met DSV-indeling.
* JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Google Cloud Storage] gegevens over Platform, moet u de volgende waarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Toegangstoets-id | Een alfanumerieke tekenreeks van 61 tekens die wordt gebruikt voor het verifiëren van uw [!DNL Google Cloud Storage] aan Platform. |
| Geheime toegangstoets | Een tekenreeks van 40 tekens met een basiscodering van 64 tekens die wordt gebruikt voor de verificatie van uw [!DNL Google Cloud Storage] aan Platform. |
| Naam van emmertje | De naam van uw [!DNL Google Cloud Storage] emmertje. U moet een emmernaam specificeren als u toegang tot specifieke subfolder in uw wolkenopslag wilt verlenen. |
| Mappad | Het pad naar de map waartoe u toegang wilt verlenen. |

Voor meer informatie over deze waarden raadpleegt u de [HMAC-sleutels voor Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) hulplijn. Raadpleeg voor meer informatie over het genereren van uw eigen toegangstoets-id en geheime toegangstoets de [[!DNL Google Cloud Storage] overzicht](../../../../connectors/cloud-storage/google-cloud-storage.md).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Google Cloud Storage] aan Platform.

## Verbind uw [!DNL Google Cloud Storage] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Cloud storage] categorie, selecteert u **[!UICONTROL Google Cloud Storage]** en selecteer vervolgens **[!UICONTROL Add data]**.

![Het scherm UI van het Platform dat de pagina van de broncatalogus toont.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

De **[!UICONTROL Connect to Google Cloud Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de optie [!DNL Google Cloud Storage] account waarmee u verbinding wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![Het scherm met de gebruikersinterface van het Platform met de bestaande accountpagina voor een Google Cloud Storage-bron](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Google Cloud Storage] referenties. Tijdens deze stap kunt u ook de submappen aangeven waartoe uw account toegang heeft door de naam van het pad naar de submap te definiëren.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![Het scherm met de gebruikersinterface van het Platform met de nieuwe accountpagina voor een Google Cloud Storage-bron.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Google Cloud Storage] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).
