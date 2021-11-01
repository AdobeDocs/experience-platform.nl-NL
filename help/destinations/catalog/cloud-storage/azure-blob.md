---
keywords: Azure Blob;Blob-bestemming;s3;azure blob-bestemming
title: Azure Blob-verbinding
description: Maak een live uitgaande verbinding met uw Azure Blob-opslag om regelmatig CSV-gegevensbestanden uit Adobe Experience Platform te exporteren.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---

# [!DNL Azure Blob] verbinding

## Overzicht {#overview}

[!DNL Azure Blob] (hierna [!DNL Blob]) is Microsoft-oplossing voor objectopslag voor de cloud. Deze zelfstudie bevat stappen voor het maken van een [!DNL Blob] bestemming die het [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Blob] doel, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [segmenten activeren op uw doel](../../ui/activate-batch-profile-destinations.md).

## Ondersteunde bestandsindelingen {#file-formats}

[!DNL Experience Platform] ondersteunt de volgende bestandsindeling waarnaar geëxporteerd moet worden [!DNL Blob]:

* Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot door komma&#39;s gescheiden waarden. Algemene DSV-bestanden worden in de toekomst ondersteund.

## Verbinden met de bestemming {#connect}

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Connection string]**: de verbindingstekenreeks is vereist voor toegang tot gegevens in uw blob-opslag. De [!DNL Blob] patroon verbindingstekenreeks begint met: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Voor meer informatie over het configureren van uw [!DNL Blob] verbindingstekenreeks, zie [Een verbindingstekenreeks configureren voor een Azure-opslagaccount](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) in de documentatie van Microsoft.

* U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet worden geschreven als een [!DNL Base64] gecodeerde tekenreeks.
* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving van deze bestemming in.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL Container]**: Voer de naam in van de [!DNL Azure Blob Storage] container die door deze bestemming moet worden gebruikt.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet worden geschreven als een [!DNL Base64] gecodeerde tekenreeks.

## Segmenten naar dit doel activeren {#activate}

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.
