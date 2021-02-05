---
keywords: Experience Platform;home;populaire onderwerpen;Google Cloud Storage;Google Cloud-opslag;Google Cloud-opslag;GCS;gcs
solution: Experience Platform
title: Een Google Cloud Storage Source Connection maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Leer hoe u een Google Cloud Storage-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---


# Een [!DNL Google Cloud Storage]-bronverbinding maken in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een [!DNL Google Cloud Storage] (hierna &quot;GCS&quot; genoemd) bronconnector met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding GCS hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

[!DNL Experience Platform] ondersteunt de volgende bestandsindelingen die door externe opslagmedia moeten worden ingevoerd:

* Door scheidingstekens gescheiden waarden (DSV): De ondersteuning voor gegevensbestanden met DSV-indeling is momenteel beperkt tot door komma&#39;s gescheiden waarden. De waarde van veldkoppen in bestanden met DSV-indeling mag alleen bestaan uit alfanumerieke tekens en onderstrepingstekens. Algemene DSV-bestanden worden in de toekomst ondersteund.
* JavaScript Object Notation (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: Gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw GCS-gegevens op [!DNL Platform], moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Toegangstoets-id | De toegangs belangrijkste identiteitskaart van [!DNL Google Cloud Storage] rekening. |
| Geheime toegangstoets | Het clientgeheim van de [!DNL Google Cloud Storage]-account. |

Raadpleeg [Server-naar-server verificatiegids](https://cloud.google.com/docs/authentication/production) voor [!DNL Google Cloud Storage] voor meer informatie over aan de slag gaan.

## Uw [!DNL Google Cloud Storage]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw GCS-account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Bronnen]** te openen. Het scherm **[!UICONTROL Catalog]** toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Google Cloud Storage]** onder de categorie **[!UICONTROL Databases]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders selecteert u **[!UICONTROL Gegevens toevoegen]** om een nieuwe GCS-connector te maken.

![catalogus](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

De pagina **[!UICONTROL Verbinding maken met Google Cloud Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw GCS-referenties op. Selecteer **[!UICONTROL Connect]** als u klaar bent en wacht dan enige tijd tot de nieuwe verbinding tot stand is gebracht.

![verbinden](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de GCS-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw GCS-account tot stand gebracht. U kunt nu verdergaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag over te brengen naar [!DNL Platform]](../../dataflow/batch/cloud-storage.md).