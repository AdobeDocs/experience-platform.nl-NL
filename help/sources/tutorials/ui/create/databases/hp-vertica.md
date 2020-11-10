---
keywords: Experience Platform;home;popular topics;HP Vertica
solution: Experience Platform
title: Creeer HP Vertica bronschakelaar in UI
topic: overview
type: Tutorial
description: Dit leerprogramma verstrekt stappen voor het creëren van een HP Vertica bronschakelaar gebruikend het gebruikersinterface van het Platform.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# Creeer een [!DNL Vertica] bronschakelaar van HP in UI

>[!NOTE]
>
> De [!DNL Vertica] schakelaar van HP is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Dit leerprogramma verstrekt stappen voor het creëren van een [!DNL Vertica] bronschakelaar van HP gebruikend het [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige [!DNL Vertica] verbinding van HP hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een dataflow](../../dataflow/databases.md).

### Vereiste referenties verzamelen

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met HP te verbinden [!DNL Vertica] gebruikend [!DNL Flow Service] API.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | Het verbindingskoord dat wordt gebruikt om met uw [!DNL Vertica] instantie van HP te verbinden. Het patroon van het verbindingskoord voor HP [!DNL Vertica] is `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Voor meer informatie over begonnen worden, verwijs naar [dit [!DNL Vertica] document](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)van HP.

## Sluit uw [!DNL Vertica] rekening van HP aan

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen hieronder volgen om uw rekening van HP aan te verbinden [!DNL Vertica] [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Bronnen]** . In het scherm **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de categorie **[!UICONTROL Databases]** selecteert u **[!UICONTROL HP Vertica]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders, uitgezochte **[!UICONTROL voeg gegevens]** toe om een nieuwe [!DNL Vertica] schakelaar van HP tot stand te brengen.

![catalogus](../../../../images/tutorials/create/hp-vertica/catalog.png)

De pagina **[!UICONTROL Verbinding maken met HP Vertica]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Voor de inputvorm die verschijnt, verstrek een naam, een facultatieve beschrijving, en uw geloofsbrieven van HP [!DNL Vertica] . Wanneer u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![verbinden](../../../../images/tutorials/create/hp-vertica/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de HP- [!DNL Vertica] account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** in de rechterbovenhoek om door te gaan.

![bestaand](../../../../images/tutorials/create/hp-vertica/existing.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u een verbinding aan uw [!DNL Vertica] rekening van HP gevestigd. U kunt nu verdergaan naar de volgende zelfstudie en een gegevensstroom [configureren om gegevens in te voeren [!DNL Platform]](../../dataflow/databases.md).