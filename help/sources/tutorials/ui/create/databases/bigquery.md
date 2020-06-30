---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Google Big Query-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# Creeer een [!DNL Google Big Query] bronschakelaar in UI

> [!NOTE]
> De [!DNL Google BigQuery] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een [!DNL Google Big Query] (hierna &quot;GBQ&quot; genoemd) bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een basisverbinding GBQ hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw GBQ-account op [!DNL Platform], moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `project` | Projectidentiteitskaart van het standaardproject [!DNL BigQuery] aan vraag tegen. |
| `clientID` | De waarde van identiteitskaart die wordt gebruikt om het vernieuwingstoken te produceren. |
| `clientSecret` | De geheime waarde die wordt gebruikt om het te produceren vernieuwt teken. |
| `refreshToken` | Het vernieuwingstoken dat wordt verkregen van [!DNL Google] wordt gebruikt om toegang tot te verlenen [!DNL BigQuery]. |

Raadpleeg [dit GBQ-document](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)voor meer informatie over deze waarden.

## Uw GBQ-account verbinden

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuwe binnenkomende basisverbinding tot stand te brengen om uw rekening GBQ aan te verbinden [!DNL Platform].

Login aan <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer dan **[!UICONTROL Bronnen]** van de linkernavigatiebar om tot de werkruimte van *[!UICONTROL Bronnen]* toegang te hebben. In het scherm *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Selecteer onder de categorie *[!UICONTROL Databases]* de optie **[!UICONTROL Google Big Query]** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **[!UICONTROL Connect-bron]** als u een nieuwe binnenkomende basisverbinding wilt maken.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

De pagina *[!UICONTROL Verbinding maken met Google Big Query]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, aan de basisverbinding een naam, een optionele beschrijving en uw GBQ-gegevens. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe basisverbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de GBQ-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een basisverbinding aan uw rekening GBQ gevestigd. U kunt nu verdergaan aan het volgende leerprogramma en een dataflow [vormen om gegevens in Platform](../../dataflow/databases.md)te brengen.