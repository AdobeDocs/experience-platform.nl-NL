---
keywords: Experience Platform;home;populaire onderwerpen;Greenplum;greenplum
solution: Experience Platform
title: Een GreenPlum Source-verbinding maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een GreenPlum-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Een [!DNL GreenPlum] bronverbinding maken in de gebruikersinterface

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL GreenPlum] bronaansluiting met behulp van de gebruikersinterface van [!DNL Experience Platform] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL GreenPlum] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL GreenPlum] via de [!DNL Flow Service] API.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie [!DNL GreenPlum] . Het patroon van de verbindingstekenreeks voor [!DNL GreenPlum] is `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Voor meer informatie over begonnen worden, verwijs naar [ dit document GreenPlum ](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## Sluit uw [!DNL GreenPlum] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL GreenPlum] -account te koppelen aan [!DNL Experience Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL GreenPlum]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL GreenPlum] -connector te maken.

![ catalogus ](../../../../images/tutorials/create/greenplum/catalog.png)

De pagina **[!UICONTROL Connect to GreenPlum]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL GreenPlum] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/greenplum/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL GreenPlum] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan.

![ bestaand ](../../../../images/tutorials/create/greenplum/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL GreenPlum] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Experience Platform]](../../dataflow/databases.md) te brengen.
