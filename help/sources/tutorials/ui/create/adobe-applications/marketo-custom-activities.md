---
title: Een Marketo Engage maken voor Source Connection en Dataflow voor Custom Activity Data in de gebruikersinterface
description: Deze zelfstudie biedt stappen voor het maken van een Marketo Engage-bronverbinding en gegevensstroom in de gebruikersinterface om gegevens van aangepaste activiteiten over te brengen naar Adobe Experience Platform.
exl-id: 05a7b500-11d2-4d58-be43-a2c4c0ceeb87
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 0%

---

# Een [!DNL Marketo Engage] bronverbinding en gegevensstroom maken voor aangepaste activiteitsgegevens in de gebruikersinterface

>[!NOTE]
>
>Dit leerprogramma verstrekt specifieke stappen op hoe te opstelling en **gegevens van de douaneactiviteit** van [!DNL Marketo] aan Experience Platform te brengen. Voor stappen op hoe te om **standaardactiviteit** gegevens te brengen, lees de [[!DNL Marketo]  gids UI ](./marketo.md).

Naast [ standaardactiviteiten ](../../../../connectors/adobe-applications/mapping/marketo.md#activities), kunt u de [!DNL Marketo] bron ook gebruiken om gegevens van douaneactiviteiten aan Adobe Experience Platform te brengen. Dit document bevat stappen voor het maken van een bronverbinding en gegevensstroom voor aangepaste activiteitengegevens met behulp van de [!DNL Marketo] -bron in de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ B2B namespaces en schema auto-generatienut ](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Het B2B namespaces en schema auto-generatienut staat u toe om [!DNL Postman] te gebruiken om waarden voor uw B2B namespaces en schema&#39;s auto-produceren. U moet eerst de B2B-naamruimten en -schema&#39;s voltooien voordat u een [!DNL Marketo] -bronverbinding en -gegevensstroom maakt.
* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Model van de Gegevens van de Ervaring (XDM) ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ creeer en geef schema&#39;s in UI ](../../../../../xdm/ui/resources/schemas.md) uit: Leer hoe te om schema&#39;s in UI tot stand te brengen en uit te geven.
* [ Identiteitsnaamruimten ](../../../../../identity-service/features/namespaces.md): Identiteitsnaamruimten zijn een component van [!DNL Identity Service] die als indicatoren van de context dienen waarop een identiteit betrekking heeft. Een volledig gekwalificeerde identiteit omvat een waarde van identiteitskaart en een namespace.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Je aangepaste activiteitengegevens ophalen

De eerste stap om aangepaste activiteitsgegevens van [!DNL Marketo] naar het Experience Platform te brengen, is het ophalen van de API-naam en de weergavenaam van uw aangepaste activiteit.

Meld u aan bij uw account met de interface [[!DNL Marketo] ](https://app-sjint.marketo.com/#MM0A1) . In de linkernavigatie, onder [!DNL Database Management], selecteer **de Activiteiten van de Douane van Marketo**.

De interface wordt bijgewerkt met een weergave van uw aangepaste activiteiten, inclusief informatie over de respectievelijke weergavenamen en API-namen. U kunt ook de Right-rail gebruiken om andere aangepaste activiteiten van uw account te selecteren en weer te geven.

![ de interface van de Activiteiten van de Douane in Adobe Marketo Engage UI.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

Selecteer **Gebieden** van de hoogste kopbal om de gebieden te bekijken verbonden aan uw douaneactiviteit. Op deze pagina kunt u de namen, API-namen, beschrijvingen en gegevenstypen van de velden in uw aangepaste activiteit weergeven. Details betreffende afzonderlijke velden worden in een latere stap gebruikt wanneer u een schema maakt.

![ de pagina van de Details van de Gegevens van de Gebieden van de Activiteit van de Douane van Marketo in Marketo Engage UI.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## Veldgroepen instellen voor aangepaste activiteiten in het B2B-activiteitenschema

Selecteer in het *[!UICONTROL Schemas]* dashboard van de gebruikersinterface van het Experience Platform de optie **[!UICONTROL Browse]** en selecteer vervolgens **[!UICONTROL B2B Activity]** in de lijst met schema&#39;s.

>[!TIP]
>
>Met de zoekbalk kunt u de navigatie versnellen door de lijst met schema&#39;s.

![ de schemawerkruimte in het Experience Platform UI met het B2B geselecteerde schema van de Activiteit.](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### Nieuwe veldgroep maken voor aangepaste activiteit

Voeg vervolgens een nieuwe veldgroep toe aan het schema [!DNL B2B Activity] . Deze veldgroep moet overeenkomen met de aangepaste activiteit die u wilt invoeren en moet de weergavenaam van de aangepaste activiteit gebruiken die u eerder hebt opgehaald.

Als u een nieuwe veldgroep wilt toevoegen, selecteert u **[!UICONTROL + Add]** naast het deelvenster *[!UICONTROL Field groups]* onder *[!UICONTROL Composition]* .

![ de schemastructuur.](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

Het venster *[!UICONTROL Add field groups]* wordt weergegeven. Selecteer **[!UICONTROL Create new field group]** en geef dezelfde weergavenaam voor de aangepaste activiteit op die u eerder hebt opgehaald. Geef een optionele beschrijving voor de nieuwe veldgroep op. Selecteer **[!UICONTROL Add field groups]** als u klaar bent.

![ het venster voor het etiketteren en het creëren van een nieuwe gebiedsgroep.](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

Nadat u een nieuwe veldgroep voor aangepaste activiteiten hebt gemaakt, wordt deze weergegeven in de catalogus van [!UICONTROL Field groups] .

![ de schemastructuur met een nieuwe die gebiedsgroep onder het paneel van de gebiedsgroep wordt toegevoegd.](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### Een nieuw veld toevoegen aan de schemastructuur

Voeg vervolgens een nieuw veld toe aan uw schema. Dit nieuwe veld moet worden ingesteld op `type: object` en bevat de afzonderlijke velden van de aangepaste activiteit.

Om een nieuw gebied toe te voegen, selecteer het plusteken (`+`) naast de schemanaam. Er wordt een vermelding voor *[!UICONTROL Untitled Field | Type]* weergegeven. Configureer vervolgens eigenschappen van het veld met behulp van het deelvenster *[!UICONTROL Field properties]* . Stel de veldnaam in op de API-naam van uw aangepaste activiteit en stel de weergavenaam in op de weergavenaam van uw aangepaste activiteit. Vervolgens stelt u het type in als `object` en wijst u de veldgroep toe aan de veldgroep met aangepaste activiteit die u in de vorige stap hebt gemaakt. Selecteer **[!UICONTROL Apply]** als u klaar bent.

![ de schemastructuur met plus (`+`) geselecteerd teken zodat een nieuw gebied kan worden toegevoegd.](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

Het nieuwe veld wordt in uw schema weergegeven.

![ een nieuw gebied dat aan het schema wordt toegevoegd.](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### Subvelden toevoegen aan het objectveld {#add-sub-fields-to-the-object-field}

De laatste stap bij het voorbereiden van uw schema is het toevoegen van individuele gebieden binnen het gebied dat u in de vorige stap creeerde.

![ een groep subfields die aan een gebied binnen het schema worden toegevoegd.](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## Een gegevensstroom maken

Als de schema-instelling is voltooid, kunt u nu doorgaan met het maken van een gegevensstroom voor uw aangepaste activiteitengegevens.

Selecteer in de gebruikersinterface van het platform **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer onder de categorie [!UICONTROL Adobe applications] de optie **[!UICONTROL Marketo Engage]** . Selecteer vervolgens **[!UICONTROL Add data]** om een nieuwe [!DNL Marketo] dataflow te maken.

![ de broncatalogus op Experience Platform UI met de geselecteerde bron van het Marketo Engage.](../../../../images/tutorials/create/marketo/catalog.png)

### Gegevens selecteren

Selecteer **[!UICONTROL Activities]** in de lijst met [!DNL Marketo] gegevenssets en selecteer vervolgens **[!UICONTROL Next]** .

![ de uitgezochte gegevensstap in het bronwerkschema met de geselecteerde activiteitendataset.](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### Gegevens

Daarna, [ verstrekt informatie voor uw dataflow ](./marketo.md#provide-dataflow-details), met inbegrip van namen en beschrijvingen voor uw dataset en dataflow, het schema dat u, en configuraties voor [!DNL Profile] opname, foutendiagnostiek, en gedeeltelijke opname zult gebruiken.

![ de dataflow detailstap.](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### Toewijzing

Toewijzingen voor velden met standaardactiviteit worden automatisch ingevuld, maar aangepaste velden voor activiteit moeten handmatig worden toegewezen aan de desbetreffende doelvelden.

Selecteer **[!UICONTROL New field type]** en selecteer **[!UICONTROL Add new field]** om uw aangepaste activiteitsvelden toe te wijzen.

![ de afbeeldingsstap met het dropdown menu om een nieuw gebied toe te voegen.](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

Navigeer door de brongegevensstructuur en zoek het veld voor aangepaste activiteit dat u wilt innemen. Selecteer **[!UICONTROL Select]** als u klaar bent.

>[!TIP]
>
>Om verwarring te voorkomen en dubbele veldnamen af te handelen, worden aangepaste activiteitsvelden voorafgegaan door de API-naam.

![ de brongegevensstructuur.](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

Om een doelgebied toe te voegen, selecteer het schemapictogram ![ schemapictogram ](/help/images/icons/schema.png) en selecteer dan de gebieden van de douaneactiviteit van het doelschema.

![ de structuur van het doelschema.](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

Herhaal de stappen om de rest van uw gebieden van de afbeelding van de douaneactiviteit toe te voegen. Selecteer **[!UICONTROL Next]** als u klaar bent.

![ Alle afbeeldingen voor bron en doelgegevens.](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### Controleren

De stap *[!UICONTROL Review]* wordt weergegeven, zodat u de nieuwe gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het brontype, het relevante pad van de gekozen bronentiteit en de hoeveelheid kolommen in die bronentiteit weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Save & ingest]** en laat u enige tijd over om de gegevensstroom te maken.

![ de definitieve revisiestap die informatie over de verbinding, dataset, en kaartgebieden samenvat.](../../../../images/tutorials/create/marketo-custom-activities/review.png)

### Aangepaste activiteiten toevoegen aan een bestaande activiteitengegevensstroom {#add-to-existing-dataflows}

Om de gegevens van de douaneactiviteit aan een bestaande gegevensstroom toe te voegen, wijzig de afbeeldingen van een bestaande activiteitendataflow met de gegevens van de douaneactiviteit die u wilt opnemen. Dit staat u toe om douaneactiviteit in de zelfde bestaande activiteitendataset in te voeren. Voor meer informatie over hoe te om de afbeeldingen van een bestaande dataflow bij te werken, lees de gids op [ het bijwerken dataflows in UI ](../../update-dataflows.md).

### Gebruik [!DNL Query Service] om activiteiten voor aangepaste activiteiten te filteren {#query-service-filter}

Zodra uw dataflow volledig is, kunt u [ Dienst van de Vraag ](../../../../../query-service/home.md) gebruiken om activiteiten voor uw gegevens van de douaneactiviteit te filtreren.

Wanneer aangepaste activiteiten in Platform worden opgenomen, wordt de API-naam van de aangepaste activiteit automatisch de `eventType` ervan. Gebruik `eventType={API_NAME}` om te filteren voor aangepaste activiteitsgegevens.

```sql
SELECT * FROM with_custom_activities_ds_today WHERE eventType='aepCustomActivityDemo1' 
```

Gebruik de component `IN` om meerdere aangepaste activiteiten te filteren:

```sql
SELECT * FROM $datasetName WHERE eventType='{API_NAME}'
SELECT * FROM $datasetName WHERE eventType IN ('aepCustomActivityDemo1', 'aepCustomActivityDemo2')
```

Het beeld toont hieronder een voorbeeld SQL verklaring in de [ Redacteur van de Vraag ](../../../../../query-service/ui/user-guide.md) die filters voor de gegevens van de douaneactiviteit.

![ Platform UI die een vraagvoorbeeld voor douaneactiviteiten toont.](../../../../images/tutorials/create/marketo-custom-activities/queries.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een platformschema voor [!DNL Marketo] aangepaste activiteitengegevens ingesteld en een gegevensstroom gemaakt om die gegevens over te brengen naar Platform. Voor algemene informatie over de [!DNL Marketo] bron, lees het [[!DNL Marketo]  bronoverzicht ](../../../../connectors/adobe-applications/marketo/marketo.md).
