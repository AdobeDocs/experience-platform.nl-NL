---
keywords: Experience Platform;thuis;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;schema;schema's;
solution: Experience Platform
title: Schema's maken en bewerken in de gebruikersinterface
description: Leer de grondbeginselen van om schema's in het gebruikersinterface van het Experience Platform tot stand te brengen en uit te geven.
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 5e57df3fbc22baa1c7abbb02a003ad8663aad040
workflow-type: tm+mt
source-wordcount: '3523'
ht-degree: 0%

---

# Schema&#39;s maken en bewerken in de gebruikersinterface

Deze handleiding biedt een overzicht van het maken, bewerken en beheren van XDM-schema&#39;s (Experience Data Model) voor uw organisatie in de gebruikersinterface van Adobe Experience Platform.

>[!IMPORTANT]
>
>De schema&#39;s XDM zijn uiterst aanpasbaar, en daarom kunnen de stappen betrokken bij het creëren van een schema variëren afhankelijk van welk soort gegevens u het schema wilt vangen. Dientengevolge, behandelt dit document slechts de basisinteractie u met schema&#39;s in UI kunt maken, en sluit verwante stappen uit zoals het aanpassen van klassen, groepen van het schemagebied, gegevenstypes, en gebieden.
>
>Voor een volledige overzicht van het proces van het schemaontwerp, volg samen met [zelfstudie Schema maken](../../tutorials/create-schema-ui.md) om een volledig voorbeeldschema tot stand te brengen en met de vele mogelijkheden vertrouwd te maken van [!DNL Schema Editor].

## Vereisten

Deze handleiding vereist een goed begrip van XDM System. Zie de [XDM-overzicht](../../home.md) voor een inleiding op de rol van XDM binnen het ecosysteem van het Experience Platform, en [grondbeginselen van de schemacompositie](../../schema/composition.md) voor een overzicht van hoe schema&#39;s worden gebouwd.

## Een nieuw schema maken {#create}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u handmatig een nieuw schema maakt in de gebruikersinterface. Als u CSV-gegevens opneemt in Platform, kunt u ervoor kiezen [kaart die gegevens aan een schema XDM dat door AI-Gegenereerde aanbevelingen wordt gecreeerd](../../../ingestion/tutorials/map-csv/recommendations.md) (momenteel in bèta) zonder het schema zelf manueel te moeten creëren.

In de [!UICONTROL Schemas] werkruimte, selecteert u **[!UICONTROL Create schema]** in de rechterbovenhoek.

![De werkruimte Schemas met [!UICONTROL Create Schema] gemarkeerd.](../../images/ui/resources/schemas/create-schema.png)

De [!UICONTROL Create schema] wordt weergegeven. U kunt een basisklasse voor het schema kiezen door een van **[!UICONTROL Individual Profile]**, **[!UICONTROL Experience Event]**, of **[!UICONTROL Other]**, gevolgd door **[!UICONTROL Next]** om uw keuze te bevestigen. Zie de [Afzonderlijk XDM-profiel](../../classes/individual-profile.md) en [XDM ExperienceEvent](../../classes/experienceevent.md) documentatie voor meer informatie over deze klassen.

![De [!UICONTROL Create schema] workflow met de drie klasseopties en [!UICONTROL Next] gemarkeerd.](../../images/ui/resources/schemas/schema-class-options.png)

Nadat u een klasse hebt geselecteerd, [!UICONTROL Name and review] wordt weergegeven. In deze sectie geeft u een naam en beschrijving op om uw schema te identificeren. &#x200B;De basisstructuur van het schema (verstrekt door de klasse) wordt getoond in het canvas voor u om uw geselecteerde klasse en schemastructuur te herzien en te verifiëren.

Ga een mensvriendelijk [!UICONTROL Schema display name] in het tekstveld. Voer vervolgens een geschikte beschrijving in om uw schema te identificeren. Wanneer u de schemastructuur hebt herzien en met uw montages gelukkig bent **[!UICONTROL Finish]** om uw schema te maken.

![De [!UICONTROL Name and review] van de [!UICONTROL Create schema] met de [!UICONTROL Schema display name], [!UICONTROL Description], en [!UICONTROL Finish] gemarkeerd.](../../images/ui/resources/schemas/name-and-review.png)

De [!UICONTROL Schema] [!UICONTROL Browse] wordt weergegeven. Uw onlangs gemaakte schema wordt nu vermeld in de Schemabibliotheek en kan worden bewerkt in het dialoogvenster [!DNL Schema Editor].

![Het tabblad Bladeren van de werkruimte Schema&#39;s geeft het onlangs gemaakte schema weer.](../../images/ui/resources/schemas/example-schema.png)

## Een bestaand schema bewerken {#edit}

>[!NOTE]
>
>Als een schema eenmaal is opgeslagen en gebruikt in gegevensinvoer, kunnen er alleen additieve wijzigingen in worden aangebracht. Zie de [regels voor schemaontwikkeling](../../schema/composition.md#evolution) voor meer informatie .

Als u een bestaand schema wilt bewerken, selecteert u de optie **[!UICONTROL Browse]** en selecteert u vervolgens de naam van het schema dat u wilt bewerken. U kunt de zoekbalk ook gebruiken om de lijst met beschikbare opties te verfijnen.

![De werkruimte Schema met een gemarkeerd schema.](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Met de zoek- en filtermogelijkheden van de werkruimte kunt u het schema gemakkelijker vinden. Zie de handleiding op [XDM-bronnen verkennen](../explore.md) voor meer informatie .

Nadat u een schema hebt geselecteerd, [!DNL Schema Editor] wordt weergegeven met de structuur van het schema die op het canvas wordt weergegeven. U kunt nu [veldgroepen toevoegen](#add-field-groups) naar het schema (of [afzonderlijke velden toevoegen](#add-individual-fields) van deze groepen), [weergavenamen van velden bewerken](#display-names), of [bestaande aangepaste veldgroepen bewerken](./field-groups.md#edit) als het schema om het even welk gebruikt.

## Meer handelingen {#more}

Binnen de Redacteur van het Schema kunt u snelle acties ook voeren om de structuur JSON van het schema te kopiëren of het schema te schrappen als het niet voor het Profiel van de Klant in real time of bijbehorende datasets is toegelaten. Selecteren [!UICONTROL More] boven aan de weergave om een vervolgkeuzelijst met snelle acties weer te geven.

Met de functie voor JSON-structuur kopiëren kunt u zien hoe een voorbeeldlading eruit zou zien terwijl u nog steeds het schema en uw gegevenspipetten maakt. Dit is vooral handig voor situaties waarin het schema complexe structuren voor objecttoewijzingen bevat, zoals een identiteitskaart.

![De Schema-editor met de knop Meer gemarkeerd en de vervolgkeuzemogelijkheden weergegeven.](../../images/tutorials/create-schema/more-actions.png)

## Schakelen tussen weergavenamen {#display-name-toggle}

Voor uw gemak, verstrekt de Redacteur van het Schema een knevel om tussen de originele gebiedsnamen en de meer leesbare vertoningsnamen te veranderen. Dankzij deze flexibiliteit is het mogelijk uw schema&#39;s beter te detecteren en te bewerken. De knevel wordt gevonden bij het hoogste recht van de mening van de Redacteur van het Schema.

>[!NOTE]
>
>De overgang van veldnamen naar weergavenamen is puur cosmetisch en verandert geen downstreambronnen.

![De Schema-editor met [!UICONTROL Show display names for fields] gemarkeerd.](../../images/ui/resources/schemas/display-name-toggle.png)

De weergavenamen voor standaardveldgroepen worden gegenereerd door het systeem, maar kunnen worden aangepast, zoals beschreven in het dialoogvenster [weergavenamen](#display-names) sectie. De namen van de vertoning worden weerspiegeld over veelvoudige meningen UI, met inbegrip van afbeelding en datasetvoorproeven. De standaardinstelling is uitgeschakeld en geeft de oorspronkelijke waarden van veldnamen weer.

## Veldgroepen toevoegen aan een schema {#add-field-groups}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u bestaande veldgroepen aan een schema kunt toevoegen. Zie de handleiding voor een nieuwe aangepaste veldgroep [maken en bewerken van veldgroepen](./field-groups.md#create) in plaats daarvan.

Als u een schema hebt geopend in het dialoogvenster [!DNL Schema Editor]U kunt velden toevoegen aan het schema door veldgroepen te gebruiken. Selecteer **[!UICONTROL Add]** naast **[!UICONTROL Field groups]** in het linkerspoor.

![De Schema-editor met de [!UICONTROL Add] van de [!UICONTROL Field groups] gemarkeerd.](../../images/ui/resources/schemas/add-field-group-button.png)

Er wordt een dialoogvenster weergegeven met een lijst met veldgroepen die u voor het schema kunt selecteren. Aangezien de gebiedsgroepen slechts met één klasse compatibel zijn, slechts die gebiedsgroepen die met de geselecteerde klasse van het schema worden geassocieerd zullen worden vermeld. Standaard worden vermelde veldgroepen gesorteerd op basis van hun populariteit in uw organisatie.

![De [!UICONTROL Add field groups] wordt gemarkeerd met de [!UICONTROL Popularity] gemarkeerde kolom.](../../images/ui/resources/schemas/field-group-popularity.png)

Als u de algemene activiteit of het bedrijfsgebied van de gebieden kent u wilt toevoegen, selecteer één of meerdere industrie-verticale categorieën in de linkerspoorstaaf om de getoonde lijst van gebiedsgroepen te filtreren.

![De [!UICONTROL Add field groups] wordt gemarkeerd met de [!UICONTROL Industry] en de [!UICONTROL Industry] gemarkeerde kolom.](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Voor meer informatie over beste praktijken voor industrie-specifieke gegevensmodellering in XDM, zie de documentatie over [bedrijfsgegevensmodellen](../../schema/industries/overview.md).

U kunt de zoekbalk ook gebruiken om de gewenste veldgroep te zoeken. Veldgroepen waarvan de naam overeenkomt met de query, worden boven in de lijst weergegeven. Onder **[!UICONTROL Standard Fields]**, worden veldgroepen weergegeven die velden bevatten die de gewenste gegevenskenmerken beschrijven.

![De [!UICONTROL Add field groups] met de [!UICONTROL Standard fields] zoekfunctie gemarkeerd.](../../images/ui/resources/schemas/field-group-search.png)

Schakel het selectievakje in naast de naam van de veldgroep die u aan het schema wilt toevoegen. U kunt meerdere veldgroepen in de lijst selecteren, waarbij elke geselecteerde veldgroep in de rechtertrack verschijnt.

![De [!UICONTROL Add field groups] met de selectiefunctie gemarkeerd.](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Voor elke vermelde veldgroep kunt u de muisaanwijzer of focus op het informatiepictogram (![](../../images/ui/resources/schemas/info-icon.png)) om een korte beschrijving weer te geven van het type gegevens dat de veldgroep vastlegt. U kunt ook het voorvertoningspictogram (![](../../images/ui/resources/schemas/preview-icon.png)) om de structuur van de velden in de veldgroep weer te geven voordat u besluit deze aan het schema toe te voegen.

Nadat u de veldgroepen hebt gekozen, selecteert u **[!UICONTROL Add field groups]** om deze aan het schema toe te voegen.

![De [!UICONTROL Add field groups] dialoog met geselecteerde veldgroepen en [!UICONTROL Add field groups] gemarkeerd.](../../images/ui/resources/schemas/add-field-group-finish.png)

De [!DNL Schema Editor] verschijnt weer terwijl de velden die door de veldgroep worden opgegeven, op het canvas worden weergegeven.

![De [!DNL Schema Editor] met een voorbeeldschema weergegeven.](../../images/ui/resources/schemas/field-groups-added.png)

Nadat u een veldgroep aan een schema hebt toegevoegd, kunt u optioneel [bestaande velden verwijderen](#remove-fields) of [Nieuwe aangepaste velden toevoegen](#add-fields) naar deze groepen, afhankelijk van uw behoeften.

### Velden verwijderen die zijn toegevoegd uit veldgroepen {#remove-fields}

Nadat u een veldgroep aan een schema hebt toegevoegd, kunt u alle velden verwijderen die u niet nodig hebt.

>[!NOTE]
>
>Het verwijderen van velden uit een veldgroep heeft alleen invloed op het schema waaraan wordt gewerkt en heeft geen invloed op de veldgroep zelf. Als u velden in één schema verwijdert, zijn deze velden nog steeds beschikbaar in alle andere schema&#39;s waarin dezelfde veldgroep wordt gebruikt.

In het volgende voorbeeld wordt de standaardveldgroep **[!UICONTROL Demographic Details]** is toegevoegd aan een schema. Eén veld verwijderen, zoals `taxId`selecteert u het veld op het canvas en selecteert u vervolgens **[!UICONTROL Remove]** in het rechterspoor.

![De [!DNL Schema Editor] with [!UICONTROL Remove] gemarkeerd. Met deze handeling wordt één veld verwijderd.](../../images/ui/resources/schemas/remove-single-field.png)

Als er meerdere velden zijn die u wilt verwijderen, kunt u de veldgroep als geheel beheren. Selecteer een veld dat tot de groep behoort op het canvas en selecteer vervolgens **[!UICONTROL Manage related fields]** in het rechterspoor.

![De [!DNL Schema Editor] with [!UICONTROL Manage related fields] gemarkeerd.](../../images/ui/resources/schemas/manage-related-fields.png)

Er verschijnt een dialoogvenster met de structuur van de veldgroep in kwestie. Hier kunt u de beschikbare selectievakjes gebruiken om de velden die u nodig hebt in of uit te schakelen. Als u tevreden bent, selecteert u **[!UICONTROL Confirm]**.

![De [!UICONTROL Manage related fields] met geselecteerde velden en [!UICONTROL Confirm] gemarkeerd.](../../images/ui/resources/schemas/select-fields.png)

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
>Hoewel de Redacteur van het Schema functioneel u toestaat om individuele gebieden aan een schema direct toe te voegen, verandert dit niet het feit dat alle gebieden in een XDM schema door zijn klasse of een gebiedsgroep moeten worden verstrekt die met die klasse compatibel is. Zoals in de volgende secties wordt uitgelegd, worden alle afzonderlijke velden nog steeds gekoppeld aan een klasse of veldgroep als een belangrijke stap wanneer ze aan een schema worden toegevoegd.

### Standaardvelden toevoegen {#add-standard-fields}

U kunt velden van standaardveldgroepen rechtstreeks aan een schema toevoegen zonder dat u eerst de corresponderende veldgroep hoeft te kennen. Als u een standaardveld aan een schema wilt toevoegen, selecteert u de plusknop (**+**) naast de naam van het schema in het canvas. An **[!UICONTROL Untitled Field]** tijdelijke aanduiding wordt weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![Tijdelijke aanduiding voor veld](../../images/ui/resources/schemas/root-custom-field.png)

Onder **[!UICONTROL Field name]** typt u de naam van het veld dat u wilt toevoegen. Het systeem zoekt automatisch naar standaardvelden die overeenkomen met de query en geeft deze onder weer **[!UICONTROL Recommended Standard Fields]**, met inbegrip van de veldgroepen waartoe zij behoren.

![Aanbevolen standaardvelden](../../images/ui/resources/schemas/standard-field-search.png)

Sommige standaardvelden hebben dezelfde naam, maar de structuur van deze velden kan afhankelijk zijn van de veldgroep waaruit ze afkomstig zijn. Als een standaardveld is genest in een bovenliggend object in de veldgroepsstructuur, wordt het bovenliggende veld ook opgenomen in het schema als het onderliggende veld wordt toegevoegd.

Selecteer het voorvertoningspictogram (![Pictogram Voorvertoning](../../images/ui/resources/schemas/preview-icon.png)) naast een standaardveld om de structuur van de veldgroep weer te geven en om beter te begrijpen hoe deze kan worden genest. Als u het standaardveld aan het schema wilt toevoegen, selecteert u het plusteken (![Plus-pictogram](../../images/ui/resources/schemas/add-icon.png)).

![Standaardveld toevoegen](../../images/ui/resources/schemas/add-standard-field.png)

Het canvas wordt bijgewerkt om het standaardveld weer te geven dat aan het schema is toegevoegd, inclusief bovenliggende velden die het is genest onder de structuur van de veldgroep. De naam van de veldgroep wordt ook onder **[!UICONTROL Field groups]** in het linkerspoor. Als u meer velden uit dezelfde veldgroep wilt toevoegen, selecteert u **[!UICONTROL Manage related fields]** in het rechterspoor.

![Standaardveld toegevoegd](../../images/ui/resources/schemas/standard-field-added.png)

### Aangepaste velden toevoegen {#add-custom-fields}

Net als bij de workflow voor standaardvelden kunt u ook uw eigen aangepaste velden rechtstreeks aan een schema toevoegen.

Als u velden wilt toevoegen aan het hoofdniveau van een schema, selecteert u de plus (**+**) naast de naam van het schema in het canvas. An **[!UICONTROL Untitled Field]** tijdelijke aanduiding wordt weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![Aangepast basisveld](../../images/ui/resources/schemas/root-custom-field.png)

Typ de naam van het veld dat u wilt toevoegen en het systeem zoekt automatisch naar de desbetreffende standaardvelden. Als u een nieuw aangepast veld wilt maken, selecteert u de bovenste optie die wordt toegevoegd met **([!UICONTROL New Field])**.

![Nieuw veld](../../images/ui/resources/schemas/custom-field-search.png)

Na het verstrekken van een vertoningsnaam en gegevenstype voor het gebied, is de volgende stap het gebied aan een ouderXDM middel toe te wijzen. Als het schema een aangepaste klasse gebruikt, kunt u [Voeg het veld toe aan de toegewezen klasse](#add-to-class) of [veldgroep](#add-to-field-group) in plaats daarvan. Als uw schema echter een standaardklasse gebruikt, kunt u het aangepaste veld alleen aan een veldgroep toewijzen.

#### Het veld toewijzen aan een aangepaste veldgroep {#add-to-field-group}

>[!NOTE]
>
>In deze sectie wordt alleen beschreven hoe u het veld toewijst aan een aangepaste veldgroep. Als u in plaats daarvan een standaardveldgroep met het nieuwe aangepaste veld wilt uitbreiden, raadpleegt u de sectie over [aangepaste velden toevoegen aan standaardveldgroepen](#custom-fields-for-standard-groups).

Selecteer onder **[!UICONTROL Assign to]** de optie **[!UICONTROL Field Group]**. Als uw schema een standaardklasse gebruikt, is dit de enige beschikbare optie en door gebrek geselecteerd.

Vervolgens moet u een veldgroep selecteren waaraan het nieuwe veld moet worden gekoppeld. Typ de naam van de veldgroep in de opgegeven tekstinvoer. Als u bestaande aangepaste veldgroepen hebt die overeenkomen met de invoer, worden deze weergegeven in de vervolgkeuzelijst. U kunt ook een unieke naam typen om een nieuwe veldgroep te maken.

![Veldgroep selecteren](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>Als u een bestaande aangepaste veldgroep selecteert, nemen alle andere schema&#39;s die die veldgroep gebruiken ook het nieuwe toegevoegde veld over nadat u de wijzigingen hebt opgeslagen. Selecteer daarom alleen een bestaande veldgroep als u dit type propagatie wilt gebruiken. Anders kunt u beter een nieuwe aangepaste veldgroep maken.

Selecteer de veldgroep in de lijst en selecteer **[!UICONTROL Apply]**.

![Veld toepassen](../../images/ui/resources/schemas/apply-field.png)

Het nieuwe veld wordt toegevoegd aan het canvas en krijgt een naamruimte onder uw [huurder-id](../../api/getting-started.md#know-your-tenant_id) om conflicten met standaard XDM gebieden te vermijden. De veldgroep waaraan u het nieuwe veld hebt gekoppeld, wordt ook weergegeven onder **[!UICONTROL Field groups]** in het linkerspoor.

![Tenant-id](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>De overige velden die door de geselecteerde aangepaste veldgroep worden opgegeven, worden standaard uit het schema verwijderd. Als u enkele van deze velden aan het schema wilt toevoegen, selecteert u een veld dat tot de groep behoort en selecteert u vervolgens **[!UICONTROL Manage related fields]** in het rechterspoor.

#### Het veld toewijzen aan een aangepaste klasse {#add-to-class}

Selecteer onder **[!UICONTROL Assign to]** de optie **[!UICONTROL Class]**. Het invoerveld hieronder wordt vervangen door de naam van de aangepaste klasse van het huidige schema om aan te geven dat het nieuwe veld wordt toegewezen aan deze klasse.

![De [!UICONTROL Class] optie die wordt geselecteerd voor de nieuwe gebiedstoewijzing.](../../images/ui/resources/schemas/assign-field-to-class.png)

Ga door met het configureren van het veld naar wens en selecteer **[!UICONTROL Apply]** wanneer gereed.

![[!UICONTROL Apply] geselecteerd voor het nieuwe veld.](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

Het nieuwe veld wordt toegevoegd aan het canvas en krijgt een naamruimte onder uw [huurder-id](../../api/getting-started.md#know-your-tenant_id) om conflicten met standaard XDM gebieden te vermijden. Als u de klassenaam in de linkerrails selecteert, wordt het nieuwe veld weergegeven als onderdeel van de klassenstructuur.

![Het nieuwe veld dat wordt toegepast op de structuur van de aangepaste klasse, weergegeven op het canvas.](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### Aangepaste velden toevoegen aan de structuur van standaardveldgroepen {#custom-fields-for-standard-groups}

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

## Een schema inschakelen voor realtime-klantprofiel {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="Een schema voor profiel inschakelen"
>abstract="Wanneer een schema voor Profiel wordt toegelaten, nemen om het even welke datasets die van dit schema worden gecreeerd aan het Profiel van de Klant in real time deel, dat gegevens uit ongelijksoortige bronnen samenvoegt om een volledige mening van elke klant te construeren. Als een schema eenmaal is gebruikt om gegevens in te voeren in Profiel, kan het niet worden uitgeschakeld. Raadpleeg de documentatie voor meer informatie."

[Klantprofiel in realtime](../../../profile/home.md) voegt gegevens uit verschillende bronnen samen om een volledige weergave van elke afzonderlijke klant samen te stellen. Als u wilt dat de gegevens die door een schema worden vastgelegd, aan dit proces deelnemen, moet u het schema inschakelen voor gebruik in [!DNL Profile].

>[!IMPORTANT]
>
>Om een schema voor toe te laten [!DNL Profile]moet er een primair identiteitsveld zijn gedefinieerd. Zie de handleiding op [identiteitsvelden definiëren](../fields/identity.md) voor meer informatie .

Als u het schema wilt inschakelen, selecteert u eerst de naam van het schema in de linkertrack en vervolgens de naam van het schema **[!UICONTROL Profile]** schakelen in de rechterspoorstaaf.

![](../../images/ui/resources/schemas/profile-toggle.png)

Er verschijnt een pop-upvenster met de waarschuwing dat een schema dat is ingeschakeld en opgeslagen, niet kan worden uitgeschakeld. Selecteren **[!UICONTROL Enable]** om door te gaan.

![](../../images/ui/resources/schemas/profile-confirm.png)

Het canvas verschijnt weer met de [!UICONTROL Profile] schakeloptie ingeschakeld.

>[!IMPORTANT]
>
>Aangezien het schema nog niet wordt bewaard, is dit het punt van geen terugkeer als u uw mening verandert over het laten van het schema aan het Profiel van de Klant in real time: zodra u sparen een toegelaten schema, kan het niet meer worden onbruikbaar gemaakt. Selecteer de **[!UICONTROL Profile]** schakelt u het schema opnieuw uit.

Selecteer **[!UICONTROL Save]** het schema opslaan.

![](../../images/ui/resources/schemas/profile-enabled.png)

Het schema is nu ingeschakeld voor gebruik in Real-Time Klantprofiel. Wanneer het Platform gegevens in datasets opneemt die op dit schema worden gebaseerd, zullen die gegevens in uw samengevoegde gegevens van het Profiel worden opgenomen.

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

Selecteer een klasse in de lijst om de beschrijving ervan rechts in het dialoogvenster weer te geven. U kunt ook **[!UICONTROL Preview class structure]** om de velden en metagegevens weer te geven die aan de klasse zijn gekoppeld. Selecteren **[!UICONTROL Assign class]** om door te gaan.

![](../../images/ui/resources/schemas/assign-class.png)

Er wordt een nieuw dialoogvenster geopend waarin u wordt gevraagd te bevestigen dat u een nieuwe klasse wilt toewijzen. Selecteren **[!UICONTROL Assign]** ter bevestiging.

![](../../images/ui/resources/schemas/assign-confirm.png)

Nadat de klassewijziging is bevestigd, wordt het canvas opnieuw ingesteld en gaat alle compositievoortgang verloren.

## Volgende stappen

In dit document worden de basisbeginselen besproken van het maken en bewerken van schema&#39;s in de gebruikersinterface van het platform. U wordt ten zeerste aangeraden de [zelfstudie Schema maken](../../tutorials/create-schema-ui.md) voor een uitvoerige werkschema voor het bouwen van een volledig schema in UI, met inbegrip van het creëren van de groepen van het douanegebied en gegevenstypes voor unieke gebruiksgevallen.

Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie de [[!UICONTROL Schemas] werkruimte - overzicht](../overview.md).

Leren hoe u schema&#39;s kunt beheren in het dialoogvenster [!DNL Schema Registry] API, zie [schema&#39;s eindpuntgids](../../api/schemas.md).
