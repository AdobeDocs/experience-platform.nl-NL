---
keywords: Azure Blob;Blob-bestemming;s3;azure blob-bestemming
title: Azure Blob-verbinding
description: Maak een live uitgaande verbinding met uw Azure Blob-opslag om periodiek door tabs gescheiden of CSV-gegevensbestanden vanuit Adobe Experience Platform te exporteren.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '579'
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

## Ondersteunde bestandsindelingen {#file-formats}

[!DNL Experience Platform] ondersteunt de volgende bestandsindeling die moet worden geëxporteerd naar  [!DNL Blob]:

- Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot door komma&#39;s gescheiden waarden. Algemene DSV-bestanden worden in de toekomst ondersteund. Lees voor meer informatie over ondersteunde bestanden het gedeelte cloudopslag in de zelfstudie over [het activeren van doelen](../../ui/activate-destinations.md#esp-and-cloud-storage).

## Sluit uw Blob-account {#connect-destination} aan

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Destinations]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Destinations]** te openen. In het scherm **[!UICONTROL Catalog]** worden verschillende doelen weergegeven waarvoor u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bestemming vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Cloud Storage]** onder de categorie **[!UICONTROL Azure Blob Storage]**, gevolgd door **[!UICONTROL Configure]**.

![Catalogus](../../assets/catalog/cloud-storage/blob/catalog.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

De pagina **[!UICONTROL Connect to Azure Blob Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

## Nieuwe account {#new-account}

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven de verbindingstekenreeks op. De verbindingstekenreeks is vereist voor toegang tot gegevens in de blob-opslag. Het patroon van de [!DNL Blob] verbindingstekenreeks begint met: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.

Zie [Een verbindingstekenreeks configureren voor een Azure-opslagaccount](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) in de documentatie van Microsoft voor meer informatie over het configureren van uw [!DNL Blob]-verbindingstekenreeks.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Merk op dat deze openbare sleutel **must** als Base64 wordt geschreven gecodeerd koord.

![Nieuwe account](../../assets/catalog/cloud-storage/blob/new.png)

## Bestaande account {#existing-account}

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Blob]-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![Bestaande account](../../assets/catalog/cloud-storage/blob/existing.png)

## Verificatie {#authentication}

De pagina **Authentication** wordt weergegeven. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving, het mappad en de container voor uw bestanden op.

In deze stap kunt u ook elke **[!UICONTROL Marketing actions]** selecteren die op dit doel moet worden toegepast. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

Selecteer **[!UICONTROL Create destination]** als u klaar bent.

![Verificatie](../../assets/catalog/cloud-storage/blob/authentication.png)

## Volgende stappen {#activate-segments}

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Blob]-account. U kunt nu naar het volgende leerprogramma verdergaan en segmenten [activeren aan uw bestemming](../../ui/activate-destinations.md).
