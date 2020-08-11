---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Generic OData-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# Creeer een [!DNL Generic OData] bronschakelaar in UI

>[!NOTE]
> De [!DNL Generic OData] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een algemene bronconnector van het Open Data Protocol (hierna &quot;OData&quot; genoemd) met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding OData hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een stroom van de protocoldataset](../../dataflow/protocols.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL OData] [!DNL Platform]account in, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De basis-URL van de [!DNL OData] service. |

Raadpleeg [dit OData-document](https://www.odata.org/getting-started/basic-tutorial/)voor meer informatie over aan de slag gaan.

## Uw [!DNL OData] account verbinden

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuw [!DNL OData] account te maken waarmee u verbinding kunt maken [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *[!UICONTROL Bronnen]* . In het scherm *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven waarvoor u een binnenkomende account kunt maken. Elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie *[!UICONTROL Protocollen]* de optie **[!UICONTROL Generic OData]** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Als u een nieuwe binnenkomende verbinding wilt maken, selecteert u Gegevens **** toevoegen.

![catalogus](../../../../images/tutorials/create/odata/catalog.png)

De pagina *[!UICONTROL Verbinden met Generic OData]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw [!DNL OData] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/odata/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL OData] account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/odata/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw [!DNL OData] account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en een datasetstroom [vormen om protocolgegevens in Platform](../../dataflow/protocols.md)te brengen.