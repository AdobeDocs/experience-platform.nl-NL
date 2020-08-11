---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een ServiceNow bronschakelaar in UI
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# Creeer een [!DNL ServiceNow] bronschakelaar in UI

>[!NOTE]
>De [!DNL ServiceNow] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL ServiceNow] bronaansluiting met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een [!DNL ServiceNow] verbinding hebt, kunt u de rest van dit document overslaan en naar de zelfstudie gaan over het [configureren van een gegevensstroom](../../dataflow/customer-success.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL ServiceNow] [!DNL Platform]account op, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `endpoint` | Het eindpunt van de [!DNL ServiceNow] server. |
| `username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de [!DNL ServiceNow] server voor verificatie. |
| `password` | Het wachtwoord om verbinding te maken met de [!DNL ServiceNow] server voor verificatie. |

Voor meer informatie over begonnen worden, verwijs naar [dit document](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)ServiceNow.

## Uw [!DNL ServiceNow] account verbinden

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuw [!DNL ServiceNow] account te maken waarmee u verbinding kunt maken [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *[!UICONTROL Bronnen]* . Het scherm van de *[!UICONTROL Catalogus]* toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de categorie *[!UICONTROL Klantsucces]* selecteert u **[!UICONTROL ServiceNow]** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **[!UICONTROL Connect-bron]** als u een nieuwe account wilt maken.

![](../../../../images/tutorials/create/servicenow/catalog.png)

De pagina *[!UICONTROL Verbinding maken met ServiceNow]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw [!DNL ServiceNow] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe account enige tijd beginnen.

![](../../../../images/tutorials/create/servicenow/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL ServiceNow] account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw [!DNL ServiceNow] account tot stand gebracht. U kunt nu verdergaan aan het volgende leerprogramma en een dataflow [vormen om gegevens in Platform](../../dataflow/customer-success.md)te brengen.
