---
keywords: Azure Blob;Blob-bestemming;s3;azure blob-bestemming
title: Azure Blob Connection Destination
description: Maak een live uitgaande verbinding met uw Azure Blob-opslag om periodiek door tabs gescheiden of CSV-gegevensbestanden vanuit Adobe Experience Platform te exporteren.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# [!DNL Azure Blob] verbinding

[!DNL Azure Blob] (hierna &quot;[!DNL Blob]&quot; genoemd) is de oplossing van de objecten van Microsoft voor de wolk. Deze zelfstudie bevat stappen voor het maken van een [!DNL Blob]-doel met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige Klodderbestemming hebt, kunt u de rest van dit document overslaan en aan het leerprogramma op [activerende segmenten aan uw bestemming ](../../ui/activate-destinations.md) te werk gaan.

### Ondersteunde bestandsindelingen

[!DNL Experience Platform] ondersteunt de volgende bestandsindeling die moet worden geëxporteerd naar  [!DNL Blob]:

- Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot door komma&#39;s gescheiden waarden. Algemene DSV-bestanden worden in de toekomst ondersteund. Lees voor meer informatie over ondersteunde bestanden het gedeelte cloudopslag in de zelfstudie over [het activeren van doelen](../../ui/activate-destinations.md#esp-and-cloud-storage)

## Sluit uw Blob-account {#connect-destination} aan

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Doelen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Doelen]** te openen. Het scherm **[!UICONTROL Catalog]** toont een verscheidenheid van bestemmingen waarvoor u een rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bestemming vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Azure Blob Storage]** onder de categorie **[!UICONTROL Cloud Storage]**, gevolgd door **[!UICONTROL Activate]**.

![Catalogus](../../assets/catalog/cloud-storage/blob/catalog.png)

De pagina **[!UICONTROL Verbinding maken met Azure Blob Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account {#new-account}

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Geef op het invoerformulier dat wordt weergegeven de verbindingstekenreeks op. De verbindingstekenreeks die is vereist voor toegang tot gegevens in de blob-opslag. Het patroon van de [!DNL Blob] verbindingstekenreeks begint met: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Merk op dat deze openbare sleutel **must** als Base64 wordt geschreven gecodeerd koord.

![Nieuwe account](../../assets/catalog/cloud-storage/blob/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Blob]-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![Bestaande account](../../assets/catalog/cloud-storage/blob/existing.png)

## Verificatie {#authentication}

De pagina **Authentication** wordt weergegeven. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving, het mappad en de container voor uw bestanden op. Als u klaar bent, selecteert u **[!UICONTROL Doel maken]**.

![Verificatie](../../assets/catalog/cloud-storage/blob/authentication.png)

## Volgende stappen {#activate-segments}

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Blob]-account. U kunt nu naar het volgende leerprogramma verdergaan en segmenten [activeren aan uw bestemming](../../ui/activate-destinations.md).
