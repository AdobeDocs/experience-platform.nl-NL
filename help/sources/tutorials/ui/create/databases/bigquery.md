---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Google Big Query-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Een Google Big Query-bronconnector maken in de gebruikersinterface

> [!NOTE]
> De Google BigQuery-connector is in bèta. De functies en documentatie kunnen worden gewijzigd.

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een Google Big Query-bronconnector (hierna &quot;GBQ&quot; genoemd) via de gebruikersinterface van Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een basisverbinding GBQ hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Om tot uw rekening GBQ op Platform toegang te hebben, moet u de volgende waarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `project` | Projectidentiteitskaart van het standaard project BigQuery aan vraag tegen. |
| `clientID` | De waarde van identiteitskaart die wordt gebruikt om het vernieuwingstoken te produceren. |
| `clientSecret` | De geheime waarde die wordt gebruikt om het te produceren vernieuwt teken. |
| `refreshToken` | Het vernieuwingstoken dat bij Google wordt verkregen en waarmee toegang tot BigQuery wordt toegestaan. |

Raadpleeg [dit GBQ-document](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)voor meer informatie over deze waarden.

## Uw GBQ-account verbinden

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuwe binnenkomende basisverbinding tot stand te brengen om uw rekening GBQ aan Platform te verbinden.

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . In het scherm *Catalogus* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Selecteer onder de categorie *Databases* de optie **Google Big Query** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **Connect-bron** als u een nieuwe binnenkomende basisverbinding wilt maken.

![](../../../../images/tutorials/create/google-big-query/sources-catalog.png)

De pagina *Verbinding maken met Google Big Query* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **Nieuw account** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, aan de basisverbinding een naam, een optionele beschrijving en uw GBQ-gegevens. Als u klaar bent, selecteert u **Connect** en laat u de nieuwe basisverbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/google-big-query/gbq-new-credentials.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de GBQ-account waarmee u verbinding wilt maken en selecteert u **Volgende** om door te gaan.

![](../../../../images/tutorials/create/google-big-query/gbq-existing-credentials.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een basisverbinding aan uw rekening GBQ gevestigd. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/databases.md).