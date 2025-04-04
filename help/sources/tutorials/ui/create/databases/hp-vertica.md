---
keywords: Experience Platform;home;populaire onderwerpen;HP Vertica
solution: Experience Platform
title: Creeer een Verbinding van HP Vertica Source in UI
type: Tutorial
description: Leer hoe te om een HP Vertica bronverbinding tot stand te brengen gebruikend Adobe Experience Platform UI.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Creeer een HP [!DNL Vertica] bronverbinding in UI

>[!NOTE]
>
> De HP [!DNL Vertica] -connector bevindt zich in bèta. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een HP [!DNL Vertica] -bronconnector met behulp van de [!DNL Experience Platform] -gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige verbinding van HP [!DNL Vertica] hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met HP [!DNL Vertica] te verbinden gebruikend [!DNL Flow Service] API.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met uw HP [!DNL Vertica] -instantie. Het patroon van de verbindingstekenreeks voor HP [!DNL Vertica] is `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Voor meer informatie over begonnen worden, verwijs naar [ dit document van HP  [!DNL Vertica]  ](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## Sluit uw HP [!DNL Vertica] -account aan

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen hieronder volgen om uw rekening van HP [!DNL Vertica] aan [!DNL Experience Platform] te verbinden.

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL HP Vertica]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders, uitgezochte **[!UICONTROL Add data]** om een nieuwe schakelaar van HP [!DNL Vertica] tot stand te brengen.

![ catalogus ](../../../../images/tutorials/create/hp-vertica/catalog.png)

De pagina **[!UICONTROL Connect to HP Vertica]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Voor de inputvorm die verschijnt, verstrek een naam, een facultatieve beschrijving, en uw geloofsbrieven van HP [!DNL Vertica]. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/hp-vertica/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de HP [!DNL Vertica] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan.

![ bestaand ](../../../../images/tutorials/create/hp-vertica/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding aan uw rekening van HP [!DNL Vertica] gevestigd. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Experience Platform]](../../dataflow/databases.md) te brengen.
