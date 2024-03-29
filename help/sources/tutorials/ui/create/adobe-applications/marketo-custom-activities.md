---
title: Creeer een Verbinding van de Bron van het Marketo Engage en Dataflow voor de gegevens van de Activiteit van de Douane in UI
description: Deze zelfstudie biedt stappen voor het maken van een Marketo Engage-bronverbinding en gegevensstroom in de gebruikersinterface om gegevens van aangepaste activiteiten over te brengen naar Adobe Experience Platform.
exl-id: 05a7b500-11d2-4d58-be43-a2c4c0ceeb87
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 0%

---

# Een [!DNL Marketo Engage] bronverbinding en gegevensstroom voor gegevens met aangepaste activiteit in de gebruikersinterface

>[!NOTE]
>
>Deze zelfstudie bevat specifieke stappen voor het instellen en leveren van **aangepaste activiteit** gegevens van [!DNL Marketo] naar Experience Platform. Voor stappen over hoe te brengen **standaardactiviteit** gegevens lezen [[!DNL Marketo] UI-hulplijn](./marketo.md).

Naast [standaardactiviteiten](../../../../connectors/adobe-applications/mapping/marketo.md#activities)kunt u ook de opdracht [!DNL Marketo] bron om gegevens over aangepaste activiteiten naar Adobe Experience Platform te verzenden. In dit document worden de volgende stappen beschreven voor het maken van een bronverbinding en gegevensstroom voor aangepaste activiteitengegevens met de opdracht [!DNL Marketo] bron in de UI.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [B2B-naamruimten en hulpprogramma voor automatisch genereren van schema&#39;s](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Het B2B-hulpprogramma voor naamruimten en automatisch genereren van schema maakt het mogelijk om [!DNL Postman] om automatisch waarden te genereren voor uw B2B-naamruimten en -schema&#39;s. U moet eerst uw B2B-naamruimten en -schema&#39;s voltooien voordat u een [!DNL Marketo] bronverbinding en gegevensstroom.
* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Schema&#39;s maken en bewerken in de gebruikersinterface](../../../../../xdm/ui/resources/schemas.md): Leer om schema&#39;s in UI tot stand te brengen en uit te geven.
* [Identiteitsnaamruimten](../../../../../identity-service/features/namespaces.md): Identiteitsnaamruimten zijn een component van [!DNL Identity Service] die dienen als indicatoren van de context waarop een identiteit betrekking heeft. Een volledig gekwalificeerde identiteit omvat een waarde van identiteitskaart en een namespace.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Je aangepaste activiteitengegevens ophalen

De eerste stap om gegevens van de douaneactiviteit van te brengen [!DNL Marketo] aan Experience Platform moet de API-naam en de weergavenaam van uw aangepaste activiteit ophalen.

Meld u aan bij uw account met de [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) interface. In de linkernavigatie, onder [!DNL Database Management], selecteert u **Aangepaste Marketo-activiteiten**.

De interface wordt bijgewerkt met een weergave van uw aangepaste activiteiten, inclusief informatie over de respectievelijke weergavenamen en API-namen. U kunt ook de Right-rail gebruiken om andere aangepaste activiteiten van uw account te selecteren en weer te geven.

![De interface Custom Activity in de gebruikersinterface van Adobe Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

Selecteren **Velden** in de bovenste koptekst om de velden weer te geven die zijn gekoppeld aan uw aangepaste activiteit. Op deze pagina kunt u de namen, API-namen, beschrijvingen en gegevenstypen van de velden in uw aangepaste activiteit weergeven. Details betreffende afzonderlijke velden worden in een latere stap gebruikt wanneer u een schema maakt.

![De pagina met gegevens over aangepaste activiteitsvelden van Marketo in de gebruikersinterface van het Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## Veldgroepen instellen voor aangepaste activiteiten in het B2B-activiteitenschema

In de *[!UICONTROL Schemas]* het dashboard van Experience Platform UI, uitgezocht **[!UICONTROL Browse]** en selecteer vervolgens **[!UICONTROL B2B Activity]** in de lijst van schema&#39;s.

>[!TIP]
>
>Met de zoekbalk kunt u de navigatie versnellen door de lijst met schema&#39;s.

![De schemawerkruimte in het Experience Platform UI met het geselecteerde B2B schema van de Activiteit.](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### Nieuwe veldgroep maken voor aangepaste activiteit

Voeg vervolgens een nieuwe veldgroep toe aan de [!DNL B2B Activity] schema. Deze veldgroep moet overeenkomen met de aangepaste activiteit die u wilt invoeren en moet de weergavenaam van de aangepaste activiteit gebruiken die u eerder hebt opgehaald.

Als u een nieuwe veldgroep wilt toevoegen, selecteert u **[!UICONTROL + Add]** naast de *[!UICONTROL Field groups]* paneel onder *[!UICONTROL Composition]*.

![De schemastructuur.](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

De *[!UICONTROL Add field groups]* wordt weergegeven. Selecteren **[!UICONTROL Create new field group]** en geef vervolgens dezelfde weergavenaam voor de aangepaste activiteit op die u in een eerdere stap hebt opgehaald. Geef een optionele beschrijving voor de nieuwe veldgroep op. Selecteer **[!UICONTROL Add field groups]**.

![Het venster voor labeling en het maken van een nieuwe veldgroep.](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

Als u een nieuwe veldgroep voor aangepaste activiteit hebt gemaakt, wordt deze weergegeven in het dialoogvenster [!UICONTROL Field groups] catalogus.

![De schemastructuur met een nieuwe gebiedsgroep die onder het paneel van de gebiedsgroep wordt toegevoegd.](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### Een nieuw veld toevoegen aan de schemastructuur

Voeg vervolgens een nieuw veld toe aan uw schema. Dit nieuwe veld moet worden ingesteld op `type: object` en bevat de afzonderlijke velden van de aangepaste activiteit.

Als u een nieuw veld wilt toevoegen, selecteert u het plusteken (`+`) naast de naam van het schema. Een vermelding voor *[!UICONTROL Untitled Field | Type]* wordt weergegeven. Configureer vervolgens eigenschappen van uw veld met de *[!UICONTROL Field properties]* deelvenster. Stel de veldnaam in op de API-naam van uw aangepaste activiteit en stel de weergavenaam in op de weergavenaam van uw aangepaste activiteit. Stel vervolgens de tekst in als `object` en wijs de veldgroep toe aan de veldgroep met aangepaste activiteiten die u in de vorige stap hebt gemaakt. Selecteer **[!UICONTROL Apply]**.

![De schemastructuur met plus (`+`) geselecteerd zodat een nieuw veld kan worden toegevoegd.](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

Het nieuwe veld wordt in uw schema weergegeven.

![Een nieuw veld dat aan het schema is toegevoegd.](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### Subvelden toevoegen aan het objectveld {#add-sub-fields-to-the-object-field}

De laatste stap bij het voorbereiden van uw schema is het toevoegen van individuele gebieden binnen het gebied dat u in de vorige stap creeerde.

![Een groep subvelden die wordt toegevoegd aan een veld in het schema.](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## Een gegevensstroom maken

Als de schema-instelling is voltooid, kunt u nu doorgaan met het maken van een gegevensstroom voor uw aangepaste activiteitengegevens.

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Adobe applications] categorie, selecteert u **[!UICONTROL Marketo Engage]**. Selecteer vervolgens **[!UICONTROL Add data]** om een nieuwe [!DNL Marketo] dataflow.

![De broncatalogus op Experience Platform UI met het geselecteerde Marketo Engage bron.](../../../../images/tutorials/create/marketo/catalog.png)

### Gegevens selecteren

Selecteren **[!UICONTROL Activities]** van de lijst van [!DNL Marketo] datasets en selecteer vervolgens **[!UICONTROL Next]**.

![De uitgezochte gegevensstap in het bronwerkschema met de geselecteerde activiteitendataset.](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### Gegevens

Volgende, [Geef informatie voor uw gegevensstroom](./marketo.md#provide-dataflow-details), met inbegrip van namen en beschrijvingen voor uw dataset en dataflow, het schema dat u zult gebruiken, en configuraties voor [!DNL Profile] inname, foutopsporing en gedeeltelijke inname.

![De detailstap voor gegevensstroom.](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### Toewijzing

Toewijzingen voor velden met standaardactiviteit worden automatisch ingevuld, maar aangepaste velden voor activiteit moeten handmatig worden toegewezen aan de desbetreffende doelvelden.

Selecteer **[!UICONTROL New field type]** en selecteer vervolgens **[!UICONTROL Add new field]**.

![De toewijzingsstap met het vervolgkeuzemenu om een nieuw veld toe te voegen.](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

Navigeer door de brongegevensstructuur en zoek het veld voor aangepaste activiteit dat u wilt innemen. Selecteer **[!UICONTROL Select]**.

>[!TIP]
>
>Om verwarring te voorkomen en dubbele veldnamen af te handelen, worden aangepaste activiteitsvelden voorafgegaan door de API-naam.

![De brongegevensstructuur.](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

Selecteer het schemapictogram om een doelveld toe te voegen ![schema-pictogram](../../../../images/tutorials/create/marketo-custom-activities/schema-icon.png) en selecteer vervolgens de velden met aangepaste activiteit in het doelschema.

![De doelschemastructuur.](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

Herhaal de stappen om de rest van uw gebieden van de afbeelding van de douaneactiviteit toe te voegen. Selecteer **[!UICONTROL Next]**.

![Alle toewijzingen voor bron- en doelgegevens.](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### Controleren

De *[!UICONTROL Review]* wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Hiermee geeft u het brontype, het relevante pad van de gekozen bronentiteit en de hoeveelheid kolommen in die bronentiteit weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Save & ingest]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![De laatste revisiestap waarin informatie over de verbinding, gegevensset en toewijzingsvelden wordt samengevat.](../../../../images/tutorials/create/marketo-custom-activities/review.png)

### Aangepaste activiteiten toevoegen aan een bestaande activiteitengegevensstroom {#add-to-existing-dataflows}

Om de gegevens van de douaneactiviteit aan een bestaande gegevensstroom toe te voegen, wijzig de afbeeldingen van een bestaande activiteitendataflow met de gegevens van de douaneactiviteit die u wilt opnemen. Dit staat u toe om douaneactiviteit in de zelfde bestaande activiteitendataset in te voeren. Lees voor meer informatie over het bijwerken van de toewijzingen van een bestaande gegevensstroom de handleiding op [bijwerken, gegevensstromen in UI](../../update-dataflows.md).

### Gebruiken [!DNL Query Service] om activiteiten voor douaneactiviteiten te filtreren {#query-service-filter}

Zodra uw gegevensstroom volledig is, kunt u gebruiken [Query-service](../../../../../query-service/home.md) om activiteiten voor uw gegevens van de douaneactiviteit te filtreren.

Wanneer aangepaste activiteiten worden opgenomen in Platform, wordt de API-naam van de aangepaste activiteit automatisch gewijzigd in `eventType`. Gebruiken `eventType={API_NAME}` om te filteren op aangepaste activiteitsgegevens.

```sql
SELECT * FROM with_custom_activities_ds_today WHERE eventType='aepCustomActivityDemo1' 
```

Gebruik de `IN` clausule om meerdere aangepaste activiteiten te filteren:

```sql
SELECT * FROM $datasetName WHERE eventType='{API_NAME}'
SELECT * FROM $datasetName WHERE eventType IN ('aepCustomActivityDemo1', 'aepCustomActivityDemo2')
```

In de onderstaande afbeelding ziet u een voorbeeld van een SQL-instructie in het dialoogvenster [Query-editor](../../../../../query-service/ui/user-guide.md) dat filters voor de gegevens van de douaneactiviteit.

![Platform UI die een vraagvoorbeeld voor douaneactiviteiten toont.](../../../../images/tutorials/create/marketo-custom-activities/queries.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een platformschema ingesteld voor [!DNL Marketo] gegevens van de douaneactiviteit en creeerde een gegevensstroom om die gegevens aan Platform te brengen. Voor algemene informatie over de [!DNL Marketo] bron, lees de [[!DNL Marketo] bronoverzicht](../../../../connectors/adobe-applications/marketo/marketo.md).
