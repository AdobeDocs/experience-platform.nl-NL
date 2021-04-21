---
keywords: Experience Platform;home;populaire onderwerpen;Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: Een Google Big Query Source Connection maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Google Big Query-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Een [!DNL Google Big Query]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Google BigQuery] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een [!DNL Google Big Query]-bronconnector (hierna &quot;BigQuery&quot; genoemd) met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding BigQuery hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw BigQuery-account op [!DNL Platform], moet u de volgende OAuth 2.0-verificatiewaarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `project` | Projectidentiteitskaart van het gebrek [!DNL BigQuery] project om tegen te vragen. |
| `clientID` | De waarde van identiteitskaart die wordt gebruikt om het vernieuwingstoken te produceren. |
| `clientSecret` | De geheime waarde die wordt gebruikt om het te produceren vernieuwt teken. |
| `refreshToken` | Het vernieuwingstoken dat wordt verkregen van [!DNL Google] wordt gebruikt om toegang tot [!DNL BigQuery] toe te staan. |

Voor meer informatie over deze waarden, verwijs naar [dit document BigQuery](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Maak verbinding met uw Google BigQuery-account

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om uw rekening BigQuery aan [!DNL Platform] te verbinden.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Sources]** te openen. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Google Big Query]** onder de categorie **[!UICONTROL Databases]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL Configure]**. Anders, selecteer **[!UICONTROL Add data]** om een nieuwe schakelaar te creëren BigQuery.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

De pagina **[!UICONTROL Connect to Google Big Query]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw BigQuery-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de BigQuery-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw account GBQ tot stand gebracht. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).
