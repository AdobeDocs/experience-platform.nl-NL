---
keywords: Experience Platform;thuis;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;schema;schema's;
solution: Experience Platform
title: Schema's maken en bewerken in de gebruikersinterface
description: Leer de grondbeginselen van om schema's in het gebruikersinterface van het Experience Platform tot stand te brengen en uit te geven.
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 90f055f2fbeb7571d2f7c1daf4ea14490069f2eb
workflow-type: tm+mt
source-wordcount: '2817'
ht-degree: 0%

---

# Schema&#39;s maken en bewerken in de gebruikersinterface

Deze handleiding biedt een overzicht van het maken, bewerken en beheren van XDM-schema&#39;s (Experience Data Model) voor uw organisatie in de gebruikersinterface van Adobe Experience Platform.

>[!IMPORTANT]
>
>De schema&#39;s XDM zijn uiterst aanpasbaar, en daarom kunnen de stappen betrokken bij het creëren van een schema variëren afhankelijk van welk soort gegevens u het schema wilt vangen. Dientengevolge, behandelt dit document slechts de basisinteractie u met schema&#39;s in UI kunt maken, en sluit verwante stappen uit zoals het aanpassen van klassen, groepen van het schemagebied, gegevenstypes, en gebieden.
>
>Voor een volledige overzicht van het proces van het schemaontwerp, volg samen met [zelfstudie over het maken van schema&#39;s](../../tutorials/create-schema-ui.md) om een volledig voorbeeldschema tot stand te brengen en met de vele mogelijkheden vertrouwd te maken van [!DNL Schema Editor].

## Vereisten

Deze handleiding vereist een goed begrip van XDM System. Zie de [XDM-overzicht](../../home.md) voor een inleiding op de rol van XDM binnen het ecosysteem van het Experience Platform, en [grondbeginselen van de schemacompositie](../../schema/composition.md) voor een overzicht van hoe schema&#39;s worden gebouwd.

## Een nieuw schema maken {#create}

In de [!UICONTROL Schemas] werkruimte, selecteert u **[!UICONTROL Create schema]** in de rechterbovenhoek. In het vervolgkeuzemenu dat wordt weergegeven, kunt u kiezen tussen **[!UICONTROL XDM Individual Profile]** en **[!UICONTROL XDM ExperienceEvent]** als de basisklasse voor het schema. U kunt ook **[!UICONTROL Browse]** om een keuze te maken uit de volledige lijst van beschikbare klassen, of [een nieuwe aangepaste klasse maken](./classes.md#create) in plaats daarvan.

![](../../images/ui/resources/schemas/create-schema.png)

Wanneer u een klasse selecteert, worden de [!DNL Schema Editor] wordt weergegeven en de basisstructuur van het schema (opgegeven door de klasse) wordt weergegeven op het canvas. Vanaf hier kunt u de juiste rail gebruiken om een **[!UICONTROL Display name]** en **[!UICONTROL Description]** voor het schema.

![](../../images/ui/resources/schemas/schema-details.png)

U kunt nu beginnen de structuur van het schema te bouwen door [groepen met schemavelden toevoegen](#add-field-groups).

## Een bestaand schema bewerken {#edit}

>[!NOTE]
>
>Als een schema eenmaal is opgeslagen en gebruikt in gegevensinvoer, kunnen er alleen additieve wijzigingen in worden aangebracht. Zie de [regels voor schemaontwikkeling](../../schema/composition.md#evolution) voor meer informatie .

Als u een bestaand schema wilt bewerken, selecteert u de optie **[!UICONTROL Browse]** en selecteert u vervolgens de naam van het schema dat u wilt bewerken.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Met de zoek- en filtermogelijkheden van de werkruimte kunt u het schema gemakkelijker vinden. Zie de handleiding op [XDM-bronnen verkennen](../explore.md) voor meer informatie .

Nadat u een schema hebt geselecteerd, [!DNL Schema Editor] wordt weergegeven met de structuur van het schema die op het canvas wordt weergegeven. U kunt nu [veldgroepen toevoegen](#add-field-groups) naar het schema (of [afzonderlijke velden toevoegen](#add-individual-fields) van deze groepen), [weergavenamen van velden bewerken](#display-names), of [bestaande aangepaste veldgroepen bewerken](./field-groups.md#edit) als het schema om het even welk gebruikt.

## Veldgroepen toevoegen aan een schema {#add-field-groups}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u bestaande veldgroepen aan een schema kunt toevoegen. Als u een nieuwe aangepaste veldgroep wilt maken, raadpleegt u de handleiding [maken en bewerken van veldgroepen](./field-groups.md#create) in plaats daarvan.

Als u een schema hebt geopend in het dialoogvenster [!DNL Schema Editor]U kunt velden toevoegen aan het schema door veldgroepen te gebruiken. Selecteer **[!UICONTROL Add]** naast **[!UICONTROL Field groups]** in het linkerspoor.

![](../../images/ui/resources/schemas/add-field-group-button.png)

Er wordt een dialoogvenster weergegeven met een lijst met veldgroepen die u voor het schema kunt selecteren. Aangezien de gebiedsgroepen slechts met één klasse compatibel zijn, slechts die gebiedsgroepen die met de geselecteerde klasse van het schema worden geassocieerd zullen worden vermeld. Standaard worden vermelde veldgroepen gesorteerd op basis van hun populariteit in uw organisatie.

![](../../images/ui/resources/schemas/field-group-popularity.png)

Als u de algemene activiteit of het bedrijfsgebied van de gebieden kent u wilt toevoegen, selecteer één of meerdere industrie-verticale categorieën in de linkerspoorstaaf om de getoonde lijst van gebiedsgroepen te filtreren.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Voor meer informatie over beste praktijken voor industrie-specifieke gegevensmodellering in XDM, zie de documentatie over [bedrijfsgegevensmodellen](../../schema/industries/overview.md).

U kunt de zoekbalk ook gebruiken om de gewenste veldgroep te zoeken. Veldgroepen waarvan de naam overeenkomt met de query, worden boven in de lijst weergegeven. Onder **[!UICONTROL Standard Fields]**, worden veldgroepen weergegeven die velden bevatten die de gewenste gegevenskenmerken beschrijven.

![](../../images/ui/resources/schemas/field-group-search.png)

Schakel het selectievakje in naast de naam van de veldgroep die u aan het schema wilt toevoegen. U kunt meerdere veldgroepen in de lijst selecteren, waarbij elke geselecteerde veldgroep in de rechtertrack verschijnt.

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Voor elke vermelde veldgroep kunt u de muisaanwijzer of focus op het informatiepictogram (![](../../images/ui/resources/schemas/info-icon.png)) om een korte beschrijving weer te geven van het type gegevens dat de veldgroep vastlegt. U kunt ook het voorvertoningspictogram selecteren (![](../../images/ui/resources/schemas/preview-icon.png)) om de structuur van de velden in de veldgroep weer te geven voordat u besluit deze aan het schema toe te voegen.

Nadat u de veldgroepen hebt gekozen, selecteert u **[!UICONTROL Add field groups]** om deze aan het schema toe te voegen.

![](../../images/ui/resources/schemas/add-field-group-finish.png)

De [!DNL Schema Editor] verschijnt weer terwijl de velden die door de veldgroep worden opgegeven, op het canvas worden weergegeven.

![](../../images/ui/resources/schemas/field-groups-added.png)

Nadat u een veldgroep aan een schema hebt toegevoegd, kunt u optioneel [bestaande velden verwijderen](#remove-fields) of [Nieuwe aangepaste velden toevoegen](#add-fields) naar deze groepen, afhankelijk van uw behoeften.

### Velden verwijderen die zijn toegevoegd uit veldgroepen {#remove-fields}

Nadat u een veldgroep aan een schema hebt toegevoegd, kunt u alle velden verwijderen die u niet nodig hebt.

>[!NOTE]
>
>Het verwijderen van velden uit een veldgroep heeft alleen invloed op het schema waaraan wordt gewerkt en heeft geen invloed op de veldgroep zelf. Als u velden in één schema verwijdert, zijn deze velden nog steeds beschikbaar in alle andere schema&#39;s waarin dezelfde veldgroep wordt gebruikt.

In het volgende voorbeeld wordt de standaardveldgroep **[!UICONTROL Demographic Details]** is toegevoegd aan een schema. Eén veld verwijderen, zoals `taxId`selecteert u het veld op het canvas en selecteert u vervolgens **[!UICONTROL Remove]** in het rechterspoor.

![Eén veld verwijderen](../../images/ui/resources/schemas/remove-single-field.png)

Als er meerdere velden zijn die u wilt verwijderen, kunt u de veldgroep als geheel beheren. Selecteer een veld dat tot de groep behoort op het canvas en selecteer vervolgens **[!UICONTROL Manage related fields]** in het rechterspoor.

![Gerelateerde velden beheren](../../images/ui/resources/schemas/manage-related-fields.png)

Er verschijnt een dialoogvenster met de structuur van de veldgroep in kwestie. Hier kunt u de beschikbare selectievakjes gebruiken om de velden die u nodig hebt in of uit te schakelen. Als u tevreden bent, selecteert u **[!UICONTROL Confirm]**.

![Velden selecteren uit veldgroep](../../images/ui/resources/schemas/select-fields.png)

Het canvas verschijnt weer met alleen de geselecteerde velden in de schemastructuur.

![Toegevoegde velden](../../images/ui/resources/schemas/fields-added.png)

### Aangepaste velden toevoegen aan veldgroepen {#add-fields}

Nadat u een veldgroep aan een schema hebt toegevoegd, kunt u aanvullende velden voor die groep definiëren. Om het even welke gebieden die aan een gebiedsgroep in één schema worden toegevoegd zullen ook in alle andere schema&#39;s verschijnen die die zelfde gebiedsgroep gebruiken.

Als een aangepast veld wordt toegevoegd aan een standaardveldgroep, wordt die veldgroep geconverteerd naar een aangepaste veldgroep en is de oorspronkelijke standaardveldgroep niet meer beschikbaar.

Als u een aangepast veld wilt toevoegen aan een standaardveldgroep, raadpleegt u de [sectie hieronder](#custom-fields-for-standard-groups) voor specifieke instructies. Als u velden toevoegt aan een aangepaste veldgroep, raadpleegt u de sectie over [aangepaste veldgroepen bewerken](./field-groups.md) in de UI-gids voor veldgroepen.

Als u geen bestaande veldgroepen wilt wijzigen, kunt u [een nieuwe aangepaste veldgroep maken](./field-groups.md#create) om in plaats daarvan extra velden te definiëren.

## Afzonderlijke velden toevoegen aan een schema {#add-individual-fields}

Met de Schema-editor kunt u afzonderlijke velden rechtstreeks aan een schema toevoegen als u niet een hele veldgroep voor een bepaald gebruiksgeval wilt toevoegen. U kunt [Afzonderlijke velden toevoegen uit standaardveldgroepen](#add-standard-fields) of [uw eigen aangepaste velden toevoegen](#add-custom-fields) in plaats daarvan.

>[!IMPORTANT]
>
>Hoewel de Redacteur van het Schema functioneel u toestaat om individuele gebieden aan een schema direct toe te voegen, verandert dit niet het feit dat alle gebieden in een XDM schema door zijn klasse of een gebiedsgroep moeten worden verstrekt die met die klasse compatibel is. Zoals in de volgende secties wordt uitgelegd, worden alle afzonderlijke velden nog steeds aan een veldgroep gekoppeld als een belangrijke stap wanneer ze aan een schema worden toegevoegd.

### Standaardvelden toevoegen {#add-standard-fields}

U kunt velden van standaardveldgroepen rechtstreeks aan een schema toevoegen zonder dat u eerst de corresponderende veldgroep hoeft te kennen. Als u een standaardveld aan een schema wilt toevoegen, selecteert u de plusknop (**+**) naast de naam van het schema in het canvas. An **[!UICONTROL Untitled Field]** tijdelijke aanduiding wordt weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![Tijdelijke aanduiding voor veld](../../images/ui/resources/schemas/root-custom-field.png)

Onder **[!UICONTROL Field name]** typt u de naam van het veld dat u wilt toevoegen. Het systeem zoekt automatisch naar standaardvelden die overeenkomen met de query en geeft deze onder weer **[!UICONTROL Recommended Standard Fields]**, inclusief de veldgroepen waartoe ze behoren.

![Aanbevolen standaardvelden](../../images/ui/resources/schemas/standard-field-search.png)

Sommige standaardvelden hebben dezelfde naam, maar de structuur van deze velden kan afhankelijk zijn van de veldgroep waaruit ze afkomstig zijn. Als een standaardveld is genest in een bovenliggend object in de veldgroepsstructuur, wordt het bovenliggende veld ook opgenomen in het schema als het onderliggende veld wordt toegevoegd.

Selecteer het voorvertoningspictogram (![Pictogram Voorvertoning](../../images/ui/resources/schemas/preview-icon.png)) naast een standaardveld om de structuur van de veldgroep weer te geven en om beter te begrijpen hoe deze kan worden genest. Als u het standaardveld aan het schema wilt toevoegen, selecteert u het plusteken (![Plus-pictogram](../../images/ui/resources/schemas/add-icon.png)).

![Standaardveld toevoegen](../../images/ui/resources/schemas/add-standard-field.png)

Het canvas wordt bijgewerkt om het standaardveld weer te geven dat aan het schema is toegevoegd, inclusief bovenliggende velden die het is genest onder de veldgroepsstructuur. De naam van de veldgroep wordt ook onder **[!UICONTROL Field groups]** in het linkerspoor. Als u meer velden uit dezelfde veldgroep wilt toevoegen, selecteert u **[!UICONTROL Manage related fields]** in het rechterspoor.

![Standaardveld toegevoegd](../../images/ui/resources/schemas/standard-field-added.png)

### Aangepaste velden toevoegen {#add-custom-fields}

Net als bij de workflow voor standaardvelden kunt u ook uw eigen aangepaste velden rechtstreeks aan een schema toevoegen.

Als u velden wilt toevoegen aan het hoofdniveau van een schema, selecteert u de plusknop (**+**) naast de naam van het schema in het canvas. An **[!UICONTROL Untitled Field]** tijdelijke aanduiding wordt weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![Aangepast basisveld](../../images/ui/resources/schemas/root-custom-field.png)

Typ de naam van het veld dat u wilt toevoegen en het systeem zoekt automatisch naar de desbetreffende standaardvelden. Als u een nieuw aangepast veld wilt maken, selecteert u de bovenste optie die wordt toegevoegd met **([!UICONTROL New Field])**.

![Nieuw veld](../../images/ui/resources/schemas/custom-field-search.png)

Hier geeft u een weergavenaam en gegevenstype op voor het veld. Onder **[!UICONTROL Assign field group]** selecteert u een veldgroep waaraan het nieuwe veld moet worden gekoppeld. Typ de naam van de veldgroep en als u dat eerder hebt gedaan [aangepaste veldgroepen maken](./field-groups.md#create) deze worden weergegeven in de vervolgkeuzelijst. U kunt ook een unieke naam in het veld typen om een nieuwe veldgroep te maken.

![Veldgroep selecteren](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>Als u een bestaande aangepaste veldgroep selecteert, nemen alle andere schema&#39;s die die veldgroep gebruiken ook het nieuwe toegevoegde veld over nadat u de wijzigingen hebt opgeslagen. Om deze reden, slechts selecteer een bestaande gebiedsgroep als u dit type van propagatie wilt. Anders kunt u beter een nieuwe aangepaste veldgroep maken.

Als u klaar bent, selecteert u **[!UICONTROL Apply]**.

![Veld toepassen](../../images/ui/resources/schemas/apply-field.png)

Het nieuwe veld wordt toegevoegd aan het canvas en krijgt een naamruimte onder het canvas [huurder-id](../../api/getting-started.md#know-your-tenant_id) om conflicten met standaard XDM gebieden te vermijden. De veldgroep waaraan u het nieuwe veld hebt gekoppeld, wordt ook weergegeven onder **[!UICONTROL Field groups]** in het linkerspoor.

![Tenant-id](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>De overige velden die door de geselecteerde aangepaste veldgroep worden opgegeven, worden standaard uit het schema verwijderd. Als u enkele van deze velden aan het schema wilt toevoegen, selecteert u een veld dat tot de groep behoort en selecteert u vervolgens **[!UICONTROL Manage related fields]** in het rechterspoor.

#### Aangepaste velden toevoegen aan de structuur van standaardveldgroepen {#custom-fields-for-standard-groups}

Als het schema u werkt een voorwerp-type gebied heeft dat door een standaardgebiedsgroep wordt verstrekt, kunt u uw eigen douanevelden aan dat standaardobject toevoegen.

>[!WARNING]
>
>Om het even welke gebieden die aan een gebiedsgroep in één schema worden toegevoegd zullen ook in alle andere schema&#39;s verschijnen die die zelfde gebiedsgroep gebruiken. Als een aangepast veld wordt toegevoegd aan een standaardveldgroep, wordt die veldgroep geconverteerd naar een aangepaste veldgroep en is de oorspronkelijke standaardveldgroep niet meer beschikbaar.
>
>Als u aan de bètaversie van deze functie hebt deelgenomen, ontvangt u een dialoogvenster met informatie over de standaardveldgroepen die u eerder hebt aangepast. Zodra u **[!UICONTROL Acknowledge]**, worden de weergegeven bronnen geconverteerd naar aangepaste veldgroepen.
>
>![Bevestigingsdialoogvenster voor conversie van standaardveldgroepen](../../images/ui/resources/schemas/beta-extension-confirmation.png)

Selecteer de plusknop (**+**) naast de hoofdmap van het object dat wordt geleverd door de standaardveldgroep.

![Veld toevoegen aan standaardobject](../../images/ui/resources/schemas/add-field-to-standard-object.png)

Er verschijnt een waarschuwingsbericht waarin u wordt gevraagd te bevestigen of u de standaardveldgroep wilt converteren. Selecteren **[!UICONTROL Continue creating field group]** om verder te gaan.

![Conversie van veldgroep bevestigen](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

Het canvas verschijnt opnieuw met een naamloze plaatsaanduiding voor het nieuwe veld. De naam van de standaardveldgroep is toegevoegd met &quot;()[!UICONTROL Extended])&quot; om aan te geven dat deze in de oorspronkelijke versie is gewijzigd. Gebruik vanaf hier de besturingselementen in de rechterspoorstaaf om de eigenschappen van het veld te definiëren.

![Veld toegevoegd aan standaardobject](../../images/ui/resources/schemas/standard-field-group-converted.png)

Nadat u de wijzigingen hebt toegepast, wordt het nieuwe veld onder de naamruimte van de huurder-id weergegeven in het standaardobject. Deze geneste naamruimte voorkomt conflicten met veldnamen binnen de veldgroep zelf om te voorkomen dat wijzigingen worden verbroken in andere schema&#39;s die dezelfde veldgroep gebruiken.

![Veld toegevoegd aan standaardobject](../../images/ui/resources/schemas/added-to-standard-object.png)

## Een schema voor realtime klantprofiel inschakelen {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="Een schema voor profiel inschakelen"
>abstract="Wanneer een schema voor Profiel wordt toegelaten, nemen om het even welke datasets die van dit schema worden gecreeerd aan het Profiel van de Klant in real time deel, dat gegevens uit ongelijksoortige bronnen samenvoegt om een volledige mening van elke klant te construeren. Als een schema eenmaal is gebruikt om gegevens in te voeren in Profiel, kan het niet worden uitgeschakeld."
>text="See the documentation for more information on enabling a schema for Profile."

[Klantprofiel in realtime](../../../profile/home.md) voegt gegevens uit verschillende bronnen samen om een volledige weergave van elke afzonderlijke klant samen te stellen. Als u wilt dat de gegevens die door een schema worden vastgelegd, aan dit proces deelnemen, moet u het schema inschakelen voor gebruik in [!DNL Profile].

>[!IMPORTANT]
>
>Om een schema voor toe te laten [!DNL Profile]moet er een primair identiteitsveld zijn gedefinieerd. Zie de handleiding op [identiteitsvelden definiëren](../fields/identity.md) voor meer informatie .

Als u het schema wilt inschakelen, selecteert u eerst de naam van het schema in de linkertrack en vervolgens de naam van het schema **[!UICONTROL Profile]** schakelen in de rechterspoorstaaf.

![](../../images/ui/resources/schemas/profile-toggle.png)

Er verschijnt een pop-upvenster met de waarschuwing dat een schema dat is ingeschakeld en opgeslagen, niet kan worden uitgeschakeld. Selecteren **[!UICONTROL Enable]** om door te gaan.

![](../../images/ui/resources/schemas/profile-confirm.png)

Het canvas verschijnt weer met de [!UICONTROL Profile] schakelen ingeschakeld.

>[!IMPORTANT]
>
>Aangezien het schema nog niet wordt opgeslagen, is dit het punt van geen terugkeer als u uw mening over het laten van het schema aan het Profiel van de Klant in real time verandert: wanneer u een ingeschakeld schema hebt opgeslagen, kan het niet meer worden uitgeschakeld. Selecteer **[!UICONTROL Profile]** schakelt u het schema opnieuw uit.

Selecteer **[!UICONTROL Save]** om het schema op te slaan.

![](../../images/ui/resources/schemas/profile-enabled.png)

Het schema is nu ingeschakeld voor gebruik in het Real-time profiel van de Klant. Wanneer het Platform gegevens in datasets opneemt die op dit schema worden gebaseerd, zullen die gegevens in uw samengevoegde gegevens van het Profiel worden opgenomen.

## Weergavenamen voor schemavelden bewerken {#display-names}

Nadat u een klasse hebt toegewezen en veldgroepen aan een schema hebt toegevoegd, kunt u de weergavenamen van de velden van een schema bewerken, ongeacht of die velden zijn voorzien door standaard- of aangepaste XDM-bronnen.

>[!NOTE]
>
>Onthoud dat de weergavenamen van velden die tot standaardklassen of -veldgroepen behoren, alleen kunnen worden bewerkt in de context van een specifiek schema. Met andere woorden, het veranderen van de vertoningsnaam van een standaardgebied in één schema beïnvloedt andere schema&#39;s niet die de zelfde bijbehorende klasse of de gebiedsgroep gebruiken.
>
>Zodra u veranderingen de vertoningsnamen voor de gebieden van een schema aanbrengt, worden die veranderingen onmiddellijk weerspiegeld in om het even welke bestaande datasets die op dat schema worden gebaseerd.

Als u de weergavenaam van een schemaveld wilt bewerken, selecteert u het veld op het canvas. Geef de nieuwe naam op in het rechterspoor onder **[!UICONTROL Display name]**.

![](../../images/ui/resources/schemas/display-name.png)

Selecteren **[!UICONTROL Apply]** in het rechterspoor en het canvas wordt bijgewerkt om de nieuwe weergavenaam van het veld te tonen. Selecteren **[!UICONTROL Save]** om de wijzigingen toe te passen op het schema.

![](../../images/ui/resources/schemas/display-name-changed.png)

## De klasse van een schema wijzigen {#change-class}

U kunt de klasse van een schema op om het even welk punt tijdens het aanvankelijke samenstellingsproces veranderen alvorens het schema is bewaard.

>[!WARNING]
>
>Het opnieuw toewijzen van de klasse voor een schema zou met uiterste voorzichtigheid moeten worden gedaan. Veldgroepen zijn alleen compatibel met bepaalde klassen. Als u de klasse wijzigt, worden het canvas en alle velden die u hebt toegevoegd opnieuw ingesteld.

Als u een klasse opnieuw wilt toewijzen, selecteert u **[!UICONTROL Assign]** aan de linkerkant van het canvas.

![](../../images/ui/resources/schemas/assign-class-button.png)

Er wordt een dialoogvenster weergegeven met een lijst met alle beschikbare klassen, inclusief alle klassen die door uw organisatie zijn gedefinieerd (de eigenaar is &quot;[!UICONTROL Customer]&quot;) en door Adobe gedefinieerde standaardklassen.

Selecteer een klasse in de lijst om de beschrijving ervan aan de rechterkant van het dialoogvenster weer te geven. U kunt ook **[!UICONTROL Preview class structure]** om de velden en metagegevens weer te geven die aan de klasse zijn gekoppeld. Selecteren **[!UICONTROL Assign class]** om door te gaan.

![](../../images/ui/resources/schemas/assign-class.png)

Er wordt een nieuw dialoogvenster geopend waarin u wordt gevraagd te bevestigen dat u een nieuwe klasse wilt toewijzen. Selecteren **[!UICONTROL Assign]** ter bevestiging.

![](../../images/ui/resources/schemas/assign-confirm.png)

Nadat de klassewijziging is bevestigd, wordt het canvas opnieuw ingesteld en gaat alle compositievoortgang verloren.

## Volgende stappen

In dit document worden de basisbeginselen van het maken en bewerken van schema&#39;s besproken in de gebruikersinterface van het Platform. U wordt ten zeerste aangeraden de [zelfstudie over het maken van schema&#39;s](../../tutorials/create-schema-ui.md) voor een uitvoerige werkschema voor het bouwen van een volledig schema in UI, met inbegrip van het creëren van de groepen van het douanegebied en gegevenstypes voor unieke gebruiksgevallen.

Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie [[!UICONTROL Schemas] werkruimte - overzicht](../overview.md).

Leren hoe u schema&#39;s kunt beheren in het dialoogvenster [!DNL Schema Registry] API, zie [schema&#39;s eindpuntgids](../../api/schemas.md).
