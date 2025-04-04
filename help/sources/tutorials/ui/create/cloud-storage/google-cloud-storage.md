---
title: Google Cloud Storage Source Connection maken in de gebruikersinterface
description: Leer hoe u een Google Cloud Storage-bronverbinding maakt met de Adobe Experience Platform-interface.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# Een [!DNL Google Cloud Storage] bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Google Cloud Storage] -bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Google Cloud Storage] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

[!DNL Experience Platform] ondersteunt de volgende bestandsindelingen die door externe opslagmedia moeten worden ingevoerd:

* DSV (Delimiter-separated-separated values, gescheiden waarden): elke waarde van één teken kan worden gebruikt als scheidingsteken voor gegevensbestanden met DSV-indeling.
* JavaScript Object Notation (JSON): gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Google Cloud Storage] -gegevens op Experience Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Toegangstoets-id | Een alfanumerieke tekenreeks van 61 tekens die wordt gebruikt om uw [!DNL Google Cloud Storage] -account te verifiëren bij Experience Platform. |
| Geheim toegangssleutel | Een tekenreeks van 40 tekens met een basiscodering van 64 tekens die wordt gebruikt om uw [!DNL Google Cloud Storage] -account te verifiëren bij Experience Platform. |
| Naam van emmertje | De naam van uw [!DNL Google Cloud Storage] emmertje. U moet een emmernaam specificeren als u toegang tot specifieke subfolder in uw wolkenopslag wilt verlenen. |
| Mappad | Het pad naar de map waartoe u toegang wilt verlenen. |

Voor meer informatie over deze waarden, zie de [ de sleutels van HMAC van de Opslag van de Wolk van Google HMAC ](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) gids. Voor stappen op hoe te om uw eigen toegangs zeer belangrijke identiteitskaart en geheime toegangssleutel te produceren, verwijs naar het [[!DNL Google Cloud Storage]  overzicht ](../../../../connectors/cloud-storage/google-cloud-storage.md).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Google Cloud Storage] -account te koppelen aan Experience Platform.

## Sluit uw [!DNL Google Cloud Storage] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL Cloud storage] de optie **[!UICONTROL Google Cloud Storage]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ het scherm van Experience Platform UI die de pagina van de broncatalogus toont.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

De pagina **[!UICONTROL Connect to Google Cloud Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Google Cloud Storage] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ het scherm UI van Experience Platform die de bestaande rekeningspagina voor een bron van de Opslag van de Wolk van Google toont ](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Google Cloud Storage] -gegevens op. Tijdens deze stap kunt u ook de submappen aangeven waartoe uw account toegang heeft door de naam van het pad naar de submap te definiëren.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ het scherm van UI van Experience Platform die de nieuwe rekeningspagina voor een bron van de Opslag van de Wolk van Google toont.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Google Cloud Storage] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens van uw wolkenopslag in Experience Platform ](../../dataflow/batch/cloud-storage.md) te brengen.
