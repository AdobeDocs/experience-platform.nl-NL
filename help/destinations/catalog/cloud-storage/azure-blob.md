---
keywords: Azure Blob;Blob-bestemming;s3;azure blob-bestemming
title: Azure Blob-verbinding
description: Maak een live uitgaande verbinding met uw Azure Blob-opslag om periodiek door tabs gescheiden of CSV-gegevensbestanden vanuit Adobe Experience Platform te exporteren.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 1%

---

# [!DNL Azure Blob] verbinding

## Overzicht {#overview}

[!DNL Azure Blob] (hierna genoemd  [!DNL Blob]) is de objecten opslagoplossing van Microsoft voor de wolk. Deze zelfstudie bevat stappen voor het maken van een [!DNL Blob]-doel met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldig [!DNL Blob] doel hebt, kunt u de rest van dit document overslaan en aan het leerprogramma op [activerende segmenten aan uw bestemming ](../../ui/activate-destinations.md) te werk gaan.

## Ondersteunde bestandsindelingen {#file-formats}

[!DNL Experience Platform] ondersteunt de volgende bestandsindeling die moet worden geëxporteerd naar  [!DNL Blob]:

* Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot door komma&#39;s gescheiden waarden. Algemene DSV-bestanden worden in de toekomst ondersteund. Lees voor meer informatie over ondersteunde bestanden het gedeelte cloudopslag in de zelfstudie over [het activeren van doelen](../../ui/activate-destinations.md#esp-and-cloud-storage).

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Connection string]**: de verbindingstekenreeks is vereist voor toegang tot gegevens in uw blob-opslag. Het patroon van de [!DNL Blob] verbindingstekenreeks begint met: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Zie [Een verbindingstekenreeks configureren voor een Azure-opslagaccount](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) in de documentatie van Microsoft voor meer informatie over het configureren van uw [!DNL Blob]-verbindingstekenreeks.

* U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.
* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving van deze bestemming in.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL Container]**: Voer de naam in van de  [!DNL Azure Blob Storage] container die door dit doel moet worden gebruikt.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.

## Segmenten naar dit doel activeren {#activate}

Zie [Profielen en segmenten activeren aan een doel](../../ui/activate-destinations.md) voor instructies bij het activeren van publiekssegmenten aan bestemmingen.
