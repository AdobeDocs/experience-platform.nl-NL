---
keywords: Experience Platform;home;popular topics;Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: Een Google Big Query-bronconnector maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Deze zelfstudie bevat stappen voor het maken van een Google Big Query-bronconnector (hierna "GBQ" genoemd) via de gebruikersinterface van het Platform.
translation-type: tm+mt
source-git-commit: 74fbf388cf645c89f9f6d00a5ae2e59ba94041b9
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# Een [!DNL Google Big Query]-bronconnector maken in de gebruikersinterface

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
| `clientSecret` | De geheime waarde die wordt gebruikt om het vernieuwingstoken te genereren. |
| `refreshToken` | Het vernieuwingstoken dat wordt verkregen van [!DNL Google] en dat wordt gebruikt om toegang tot [!DNL BigQuery] toe te staan. |

Raadpleeg [dit BigQuery-document](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing) voor meer informatie over deze waarden.

## Verbind uw Google BigQuery-account

Nadat u uw vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw BigQuery-account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Bronnen]** te openen. In het scherm **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Google Big Query]** onder de categorie **[!UICONTROL Databases]**. Als u deze connector voor het eerst gebruikt, selecteert u **[!UICONTROL Configureren]**. Selecteer anders **[!UICONTROL Gegevens toevoegen]** om een nieuwe BigQuery-connector te maken.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

De pagina **[!UICONTROL Verbinding maken met Google Big Query]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuw account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL Nieuw account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw BigQuery-referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Bestaande account

Als u een bestaande account wilt koppelen, selecteert u het BigQuery-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw GBQ-account tot stand gebracht. U kunt nu doorgaan naar de volgende zelfstudie en [een dataflow configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).