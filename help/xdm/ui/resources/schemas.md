---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;schema;schema's;
solution: Experience Platform
title: Schema's maken en bewerken in de gebruikersinterface
description: Leer de basisbeginselen van het maken en bewerken van schema's in de Experience Platform-gebruikersinterface.
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 9691ce1ca560acce7a9512df7eb92e61962bc467
workflow-type: tm+mt
source-wordcount: '3899'
ht-degree: 0%

---

# Schema&#39;s maken en bewerken in de gebruikersinterface {#create-edit-schemas-in-ui}

Deze handleiding biedt een overzicht van het maken, bewerken en beheren van XDM-schema&#39;s (Experience Data Model) voor uw organisatie in de gebruikersinterface van Adobe Experience Platform.

>[!IMPORTANT]
>
>De schema&#39;s XDM zijn uiterst aanpasbaar, en daarom kunnen de stappen betrokken bij het creëren van een schema variëren afhankelijk van welk soort gegevens u het schema wilt vangen. Dientengevolge, behandelt dit document slechts de basisinteractie u met schema&#39;s in UI kunt maken, en sluit verwante stappen uit zoals het aanpassen van klassen, groepen van het schemagebied, gegevenstypes, en gebieden.
>
>Voor een volledige tour van het proces van de schemaverwezenlijking, volg samen met de [ zelfstudie van de schemaverwezenlijking ](../../tutorials/create-schema-ui.md) om een volledig voorbeeldschema tot stand te brengen en met de vele mogelijkheden van [!DNL Schema Editor] vertrouwd te maken.

## Vereisten {#prerequisites}

Deze handleiding vereist een goed begrip van XDM System. Verwijs naar het [ XDM overzicht ](../../home.md) voor een inleiding aan de rol van XDM binnen het ecosysteem van Experience Platform, en de [ grondbeginselen van schemacompositie ](../../schema/composition.md) voor een overzicht van hoe schema&#39;s worden geconstrueerd.

## Een nieuw schema maken {#create}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u handmatig een nieuw schema maakt in de gebruikersinterface. Als u CSV gegevens in Platform opneemt, kunt u het Leren van de Machine (ML) algoritmen gebruiken aan **een schema van steekproefCSV gegevens** produceren. Deze workflow komt overeen met uw gegevensindeling en maakt automatisch een nieuw schema op basis van de structuur en inhoud van uw CSV-bestand. Zie de [ ML-Begeleidde van de schemaverwezenlijking ](../ml-assisted-schema-creation.md) voor meer informatie over dit werkschema.

Selecteer in de werkruimte [!UICONTROL Schemas] de optie **[!UICONTROL Create schema]** in de rechterbovenhoek.

![ de werkruimte van Schema&#39;s met [!UICONTROL Create Schema] benadrukte.](../../images/ui/resources/schemas/create-schema.png)

Het dialoogvenster [!UICONTROL Create a schema] wordt weergegeven. In dit dialoogvenster kunt u kiezen of u handmatig een schema wilt maken door velden en veldgroepen toe te voegen, of u kunt een CSV-bestand uploaden en XML-algoritmen gebruiken om een schema te genereren. Selecteer een workflow voor het maken van een schema in het dialoogvenster.

![ creeer een schemadialoog met de werkschemaopties en selecteer benadrukt.](../../images/ui/resources/schemas/create-a-schema-dialog.png)

### [!BADGE  Beta ] {type=Informative} Handboek of ML-bijgestaan schemaverwezenlijking {#manual-or-assisted}

Leren hoe u een algoritme van XML kunt gebruiken om een schemastructuur te adviseren die op een csv- dossier wordt gebaseerd, zie de [ machine het leren-bijgewoonde gids van de schemaverwezenlijking ](../ml-assisted-schema-creation.md). Deze UI-handleiding is gericht op de workflow voor handmatig maken.

### Handmatig schema maken {#manual-creation}

De [!UICONTROL Create schema] -workflow wordt weergegeven. U kunt een basisklasse voor het schema kiezen door **[!UICONTROL Individual Profile]** , **[!UICONTROL Experience Event]** of **[!UICONTROL Other]** te selecteren, gevolgd door **[!UICONTROL Next]** om uw keuze te bevestigen. Zie de documentatie [[!UICONTROL XDM individual profile]](../../classes/individual-profile.md) en [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md) voor meer informatie over deze klassen.

![ het [!UICONTROL Create schema] werkschema met de drie klassenopties en [!UICONTROL Next] benadrukte.](../../images/ui/resources/schemas/schema-class-options.png)

Wanneer u **[!UICONTROL Other]** kiest, wordt een lijst met beschikbare klassen weergegeven. Hier kunt u door bestaande klassen bladeren en deze filteren.

![ het [!UICONTROL Create schema] werkschema met [!UICONTROL Other] die in de [!UICONTROL Schema details] sectie wordt benadrukt.](../../images/ui/resources/schemas/other-schema-details.png)

Selecteer een keuzerondje om de klassen te filteren op basis van het feit of ze aangepaste of standaardklassen zijn. U kunt de beschikbare resultaten ook filteren op basis van hun industrie of naar een specifieke klasse zoeken met het zoekveld.

![ het [!UICONTROL Create schema] werkschema met de onderzoeksbar, [!UICONTROL Custom], en [!UICONTROL Industries] benadrukte.](../../images/ui/resources/schemas/filter-and-search.png)

Om u te helpen beslissen over de aangewezen klasse, zijn er info en voorproefpictogrammen voor elke klasse. Het infopictogram (![ Info pictogram.](/help/images/icons/info.png) ) opent een dialoogvenster met een beschrijving van de klasse en de industrie waaraan deze is gekoppeld.

![ het infopictogram en tooltip van de geselecteerde benadrukte klasse.](../../images/ui/resources/schemas/class-info.png)

Het voorproefpictogram (![ een voorproefpictogram.](/help/images/icons/preview.png)) opent een voorproefdialoog voor de klasse die een schemadiagram en zijn eigenschappen bevat.

![ een voorproef van de geselecteerde klasse met het schemadiagram en klasseneigenschappen.](../../images/ui/resources/schemas/class-preview.png)

Selecteer een willekeurige rij om een klasse te kiezen en selecteer vervolgens **[!UICONTROL Next]** om uw keuze te bevestigen.

![ het [!UICONTROL Create schema] werkschema met een klasse die van de lijst van beschikbare klassen wordt geselecteerd en [!UICONTROL Next] benadrukt.](../../images/ui/resources/schemas/select-class.png)

Nadat u een klasse hebt geselecteerd, wordt de sectie [!UICONTROL Name and review] weergegeven. In deze sectie geeft u een naam en beschrijving op om uw schema te identificeren. &#x200B;De basisstructuur van het schema (verstrekt door de klasse) wordt getoond in het canvas voor u om uw geselecteerde klasse en schemastructuur te herzien en te verifiëren.

Voer in het tekstveld een mensvriendelijke [!UICONTROL Schema display name] in. Voer vervolgens een geschikte beschrijving in om uw schema te identificeren. Wanneer u de schemastructuur hebt herzien en met uw montages gelukkig bent, uitgezocht **[!UICONTROL Finish]** om uw schema tot stand te brengen.

![ de [!UICONTROL Name and review] sectie van het [!UICONTROL Create schema] werkschema met [!UICONTROL Schema display name], [!UICONTROL Description], en [!UICONTROL Finish] benadrukte.](../../images/ui/resources/schemas/name-and-review.png)

De Schema-editor wordt weergegeven, waarbij de structuur van het schema op het canvas wordt weergegeven. Indien gewenst, kunt u [ nu beginnen toevoegend gebieden aan de klasse ](../../ui/resources/classes.md#add-fields).

![ de Redacteur van het Schema met de structuur van het schema die in het canvas wordt getoond.](../../images/ui/resources/schemas/edit.png)

## Een bestaand schema bewerken {#edit}

>[!NOTE]
>
Als een schema eenmaal is opgeslagen en gebruikt in gegevensinvoer, kunnen er alleen additieve wijzigingen in worden aangebracht. Zie de [ regels van schemaevolutie ](../../schema/composition.md#evolution) voor meer informatie.

Als u een bestaand schema wilt bewerken, selecteert u de tab **[!UICONTROL Browse]** en selecteert u vervolgens de naam van het schema dat u wilt bewerken. U kunt de zoekbalk ook gebruiken om de lijst met beschikbare opties te verfijnen.

![ de werkruimte van het Schema met een benadrukt schema.](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
Met de zoek- en filtermogelijkheden van de werkruimte kunt u het schema gemakkelijker vinden. Zie de gids bij [ het onderzoeken van middelen XDM ](../explore.md) voor meer informatie.

Nadat u een schema hebt geselecteerd, wordt de [!DNL Schema Editor] weergegeven met de structuur van het schema die op het canvas wordt weergegeven. U kunt [ gebiedsgroepen ](#add-field-groups) aan het schema nu toevoegen (of [ individuele gebieden ](#add-individual-fields) van die groepen toevoegen), [ uitgeeft de namen van de gebiedsvertoning ](#display-names), of [ uitgeeft bestaande groepen van het douaneveld ](./field-groups.md#edit) als het schema om het even welk aanwendt.

## Meer acties {#more}

Binnen de Redacteur van het Schema kunt u snelle acties ook voeren om de structuur JSON van het schema te kopiëren of het schema te schrappen als het niet voor het Profiel van de Klant in real time of bijbehorende datasets is toegelaten. Selecteer [!UICONTROL More] boven aan de weergave om een vervolgkeuzelijst met snelle acties weer te geven.

Met de functie voor JSON-structuur kopiëren kunt u zien hoe een voorbeeldlading eruit zou zien terwijl u nog steeds het schema en uw gegevenspipetten maakt. Dit is vooral handig voor situaties waarin het schema complexe structuren voor objecttoewijzingen bevat, zoals een identiteitskaart.

![ de Redacteur van het Schema met de Meer benadrukte knoop en de drop-down getoonde opties.](../../images/tutorials/create-schema/more-actions.png)

## Schakelen tussen weergavenamen {#display-name-toggle}

Voor uw gemak, verstrekt de Redacteur van het Schema een knevel om tussen de originele gebiedsnamen en de meer leesbare vertoningsnamen te veranderen. Dankzij deze flexibiliteit is het mogelijk uw schema&#39;s beter te detecteren en te bewerken. De knevel wordt gevonden bij het hoogste recht van de mening van de Redacteur van het Schema.

>[!NOTE]
>
De overgang van veldnamen naar weergavenamen is puur cosmetisch en verandert geen downstreambronnen.

![ de Redacteur van het Schema met [!UICONTROL Show display names for fields] benadrukte.](../../images/ui/resources/schemas/display-name-toggle.png)

De vertoningsnamen voor standaardgebiedsgroepen worden geproduceerd maar kunnen worden aangepast, zoals die in de [ vertoningsnamen ](#display-names) sectie wordt beschreven. De namen van de vertoning worden weerspiegeld over veelvoudige meningen UI, met inbegrip van afbeelding en datasetvoorproeven. De standaardinstelling is uitgeschakeld en geeft de oorspronkelijke waarden van veldnamen weer.

## Veldgroepen toevoegen aan een schema {#add-field-groups}

>[!NOTE]
>
In deze sectie wordt beschreven hoe u bestaande veldgroepen aan een schema kunt toevoegen. Als u een nieuwe groep van het douanegebied wilt tot stand brengen, zie de gids bij [ creërend en het uitgeven gebiedsgroepen ](./field-groups.md#create) in plaats daarvan.

Nadat u een schema hebt geopend in de [!DNL Schema Editor] , kunt u velden aan het schema toevoegen via veldgroepen. Selecteer om te beginnen **[!UICONTROL Add]** naast **[!UICONTROL Field groups]** in de linkertrack.

![ de Redacteur van het Schema met [!UICONTROL Add] van de [!UICONTROL Field groups] benadrukte sectie.](../../images/ui/resources/schemas/add-field-group-button.png)

Er wordt een dialoogvenster weergegeven met een lijst met veldgroepen die u voor het schema kunt selecteren. Aangezien de gebiedsgroepen slechts met één klasse compatibel zijn, slechts die gebiedsgroepen die met de geselecteerde klasse van het schema worden geassocieerd zullen worden vermeld. Standaard worden vermelde veldgroepen gesorteerd op basis van hun populariteit in uw organisatie.

![ de [!UICONTROL Add field groups] dialoog die met de [!UICONTROL Popularity] benadrukte kolom wordt benadrukt.](../../images/ui/resources/schemas/field-group-popularity.png)

Als u de algemene activiteit of het bedrijfsgebied van de gebieden kent u wilt toevoegen, selecteer één of meerdere industrie-verticale categorieën in de linkerspoorstaaf om de getoonde lijst van gebiedsgroepen te filtreren.

![ de [!UICONTROL Add field groups] dialoog die met de [!UICONTROL Industry] wordt benadrukt filters en de [!UICONTROL Industry] benadrukte kolom.](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
Voor meer informatie over beste praktijken voor industrie-specifieke gegevens modelleren in XDM, zie de documentatie over [ de modellen van de industriegegevens ](../../schema/industries/overview.md).

U kunt de zoekbalk ook gebruiken om de gewenste veldgroep te zoeken. Veldgroepen waarvan de naam overeenkomt met de query, worden boven in de lijst weergegeven. Onder **[!UICONTROL Standard Fields]** worden veldgroepen weergegeven die velden bevatten die de gewenste gegevenskenmerken beschrijven.

![ de [!UICONTROL Add field groups] dialoog met de [!UICONTROL Standard fields] benadrukte onderzoeksfunctie.](../../images/ui/resources/schemas/field-group-search.png)

Schakel het selectievakje in naast de naam van de veldgroep die u aan het schema wilt toevoegen. U kunt meerdere veldgroepen in de lijst selecteren, waarbij elke geselecteerde veldgroep in de rechtertrack verschijnt.

![ het [!UICONTROL Add field groups] dialoog met de benadrukte eigenschap van de checkbox selectie.](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
Voor om het even welke vermelde gebiedsgroep, kunt u op het informatiepictogram (![ info pictogram ](/help/images/icons/info.png)) bewegen of concentreren om een korte beschrijving van het soort gegevens te bekijken de gebiedsgroep vangt. U kunt het voorproefpictogram (![ voorproefpictogram ](/help/images/icons/preview.png)) ook selecteren om de structuur van de gebieden te bekijken die de gebiedsgroep verstrekt alvorens u besluit om het aan het schema toe te voegen.

Nadat u de veldgroepen hebt gekozen, selecteert u **[!UICONTROL Add field groups]** om deze aan het schema toe te voegen.

![ de [!UICONTROL Add field groups] dialoog met geselecteerde en [!UICONTROL Add field groups] benadrukte gebiedsgroepen.](../../images/ui/resources/schemas/add-field-group-finish.png)

De [!DNL Schema Editor] wordt weer weergegeven met de velden die door de veldgroep worden opgegeven, in het canvas.

![ [!DNL Schema Editor] met een getoonde voorbeeldschema.](../../images/ui/resources/schemas/field-groups-added.png)

>[!NOTE]
>
Binnen de Redacteur van het Schema, worden de standaard (Adobe-geproduceerde) klassen en de gebiedsgroepen vermeld met het hangslotpictogram ![ A hangslotpictogram.](/help/images/icons/lock-closed.png). Het hangslot verschijnt in de linkerspoorstaaf naast de klasse of de naam van de gebiedsgroep, evenals naast om het even welk gebied in het schemadiagram dat een deel van een systeem-geproduceerde middel is.
>
![ de Redacteur van het Schema met het gemarkeerde hangslotpictogram ](../../images/ui/explore/schema-editor-padlock-icon.png)

Na het toevoegen van een gebiedsgroep aan een schema, kunt u optioneel [ bestaande gebieden ](#remove-fields) verwijderen of [ nieuwe douanevelden ](#add-fields) toevoegen aan die groepen, afhankelijk van uw behoeften.

### Velden verwijderen die zijn toegevoegd uit veldgroepen {#remove-fields}

Nadat u een veldgroep aan een schema hebt toegevoegd, kunt u alle velden verwijderen die u niet nodig hebt.

>[!NOTE]
>
Het verwijderen van velden uit een veldgroep heeft alleen invloed op het schema waaraan wordt gewerkt en heeft geen invloed op de veldgroep zelf. Als u velden in één schema verwijdert, zijn deze velden nog steeds beschikbaar in alle andere schema&#39;s waarin dezelfde veldgroep wordt gebruikt.

In het volgende voorbeeld is de standaardveldgroep **[!UICONTROL Demographic Details]** toegevoegd aan een schema. Als u één veld, zoals `taxId` , wilt verwijderen, selecteert u het veld op het canvas en selecteert u vervolgens **[!UICONTROL Remove]** in de rechtertrack.

![ De [!DNL Schema Editor] with [!UICONTROL Remove] gemarkeerd. Deze actie verwijdert één enkel gebied.](../../images/ui/resources/schemas/remove-single-field.png)

Als er meerdere velden zijn die u wilt verwijderen, kunt u de veldgroep als geheel beheren. Selecteer een veld dat tot de groep behoort op het canvas en selecteer vervolgens **[!UICONTROL Manage related fields]** in de rechtertrack.

![ [!DNL Schema Editor] met [!UICONTROL Manage related fields] benadrukte.](../../images/ui/resources/schemas/manage-related-fields.png)

Er verschijnt een dialoogvenster met de structuur van de veldgroep in kwestie. Hier kunt u de beschikbare selectievakjes gebruiken om de velden die u nodig hebt in of uit te schakelen. Selecteer **[!UICONTROL Confirm]** als u tevreden bent.

![ de [!UICONTROL Manage related fields] dialoog met geselecteerde gebieden en [!UICONTROL Confirm] benadrukte.](../../images/ui/resources/schemas/select-fields.png)

Het canvas verschijnt weer met alleen de geselecteerde velden in de schemastructuur.

![ toegevoegde Gebieden ](../../images/ui/resources/schemas/fields-added.png)

### Aangepaste velden toevoegen aan veldgroepen {#add-fields}

Nadat u een veldgroep aan een schema hebt toegevoegd, kunt u aanvullende velden voor die groep definiëren. Om het even welke gebieden die aan een gebiedsgroep in één schema worden toegevoegd zullen ook in alle andere schema&#39;s verschijnen die die zelfde gebiedsgroep gebruiken.

Als een aangepast veld wordt toegevoegd aan een standaardveldgroep, wordt die veldgroep geconverteerd naar een aangepaste veldgroep en is de oorspronkelijke standaardveldgroep niet meer beschikbaar.

Als u een douanegebied aan een standaardgebiedsgroep wilt toevoegen, verwijs naar de [ sectie hieronder ](#custom-fields-for-standard-groups) voor specifieke instructies. Als u gebieden aan een groep van het douanegebied toevoegt, verwijs naar sectie over [ het uitgeven van de groepen van het douanegebied ](./field-groups.md) op de gids van de gebiedsgroepen UI.

Als u geen bestaande gebiedsgroepen wilt veranderen, kunt u [ tot een nieuwe groep van het douanegebied ](./field-groups.md#create) leiden om extra gebieden in plaats daarvan te bepalen.

## Afzonderlijke velden toevoegen aan een schema {#add-individual-fields}

Met de Schema-editor kunt u afzonderlijke velden rechtstreeks aan een schema toevoegen als u niet een hele veldgroep voor een bepaald gebruiksgeval wilt toevoegen. U kunt [ individuele gebieden van standaardgebiedsgroepen ](#add-standard-fields) toevoegen of [ uw eigen douanevelden ](#add-custom-fields) in plaats daarvan toevoegen.

>[!IMPORTANT]
>
Hoewel de Redacteur van het Schema functioneel u toestaat om individuele gebieden aan een schema direct toe te voegen, verandert dit niet het feit dat alle gebieden in een XDM schema door zijn klasse of een gebiedsgroep moeten worden verstrekt die met die klasse compatibel is. Zoals in de volgende secties wordt uitgelegd, worden alle afzonderlijke velden nog steeds gekoppeld aan een klasse of veldgroep als een belangrijke stap wanneer ze aan een schema worden toegevoegd.

### Standaardvelden toevoegen {#add-standard-fields}

U kunt velden van standaardveldgroepen rechtstreeks aan een schema toevoegen zonder dat u eerst de corresponderende veldgroep hoeft te kennen. Om een standaardgebied aan een schema toe te voegen, selecteer plus (**+**) pictogram naast de naam van het schema in het canvas. Er wordt een tijdelijke aanduiding **[!UICONTROL Untitled Field]** weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![ placeholder van het Gebied ](../../images/ui/resources/schemas/root-custom-field.png)

Typ onder **[!UICONTROL Field name]** de naam van het veld dat u wilt toevoegen. Het systeem zoekt automatisch naar standaardvelden die overeenkomen met de query en geeft deze onder **[!UICONTROL Recommended Standard Fields]** weer, inclusief de veldgroepen waartoe ze behoren.

![ geadviseerde Standaard Gebieden ](../../images/ui/resources/schemas/standard-field-search.png)

Sommige standaardvelden hebben dezelfde naam, maar de structuur van deze velden kan afhankelijk zijn van de veldgroep waaruit ze afkomstig zijn. Als een standaardveld is genest in een bovenliggend object in de veldgroepsstructuur, wordt het bovenliggende veld ook opgenomen in het schema als het onderliggende veld wordt toegevoegd.

Selecteer het voorproefpictogram (![ pictogram van de Voorproef ](/help/images/icons/preview.png)) naast een standaardgebied om de structuur van zijn gebiedsgroep te bekijken en beter te begrijpen hoe het zou kunnen worden genest. Om het standaardgebied aan het schema toe te voegen, selecteer het plusteken (![ plus pictogram ](/help/images/icons/add-circle.png)).

![ voeg standaardgebied ](../../images/ui/resources/schemas/add-standard-field.png) toe

Het canvas wordt bijgewerkt om het standaardveld weer te geven dat aan het schema is toegevoegd, inclusief bovenliggende velden die het is genest onder de structuur van de veldgroep. De naam van de veldgroep wordt ook vermeld onder **[!UICONTROL Field groups]** in de linkertrack. Als u meer velden van dezelfde veldgroep wilt toevoegen, selecteert u **[!UICONTROL Manage related fields]** in de rechtertrack.

![ Standaard toegevoegd gebied ](../../images/ui/resources/schemas/standard-field-added.png)

### Aangepaste velden toevoegen {#add-custom-fields}

Net als bij de workflow voor standaardvelden kunt u ook uw eigen aangepaste velden rechtstreeks aan een schema toevoegen.

Om gebieden aan het wortelniveau van een schema toe te voegen, selecteer plus (**+**) pictogram naast de naam van het schema in het canvas. Er wordt een tijdelijke aanduiding **[!UICONTROL Untitled Field]** weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![ Wortel douanegebied ](../../images/ui/resources/schemas/root-custom-field.png)

Typ de naam van het veld dat u wilt toevoegen en het systeem zoekt automatisch naar de desbetreffende standaardvelden. Om een nieuw douanegebied in plaats daarvan tot stand te brengen, selecteer de hoogste optie die met **wordt toegevoegd ([!UICONTROL New Field])**.

![ Nieuw gebied ](../../images/ui/resources/schemas/custom-field-search.png)

Nadat u een weergavenaam en gegevenstype hebt opgegeven for In het veld is de volgende stap het toewijzen van het veld aan een bovenliggende XDM-resource. Als uw schema een douaneklasse gebruikt, kunt u verkiezen om [ het gebied aan de toegewezen klasse ](#add-to-class) of a [ gebiedsgroep ](#add-to-field-group) in plaats daarvan toe te voegen. Als uw schema echter een standaardklasse gebruikt, kunt u het aangepaste veld alleen aan een veldgroep toewijzen.

#### Het veld toewijzen aan een aangepaste veldgroep {#add-to-field-group}

>[!NOTE]
>
In deze sectie wordt alleen beschreven hoe u het veld toewijst aan een aangepaste veldgroep. Als u een standaardgebiedsgroep met het nieuwe douanegebied in plaats daarvan wilt uitbreiden, zie de sectie op [ toevoegend douanegebieden aan standaardgebiedsgroepen ](#custom-fields-for-standard-groups).

Selecteer onder **[!UICONTROL Assign to]** de optie **[!UICONTROL Field Group]**. Als uw schema een standaardklasse gebruikt, is dit de enige beschikbare optie en door gebrek geselecteerd.

Vervolgens moet u een veldgroep selecteren waaraan het nieuwe veld moet worden gekoppeld. Typ de naam van de veldgroep in de opgegeven tekstinvoer. Als u bestaande aangepaste veldgroepen hebt die overeenkomen met de invoer, worden deze weergegeven in de vervolgkeuzelijst. U kunt ook typen a unieke naam om een nieuwe veldgroep te maken.

![ Uitgezochte gebiedsgroep ](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
Als u een bestaande aangepaste veldgroep selecteert, nemen alle andere schema&#39;s die die veldgroep gebruiken ook het nieuwe toegevoegde veld over nadat u de wijzigingen hebt opgeslagen. Selecteer daarom alleen een bestaande veldgroep als u dit type wilt gebruiken of voortplanting. Anders kunt u beter een nieuwe aangepaste veldgroep maken.

Selecteer **[!UICONTROL Apply]** nadat u de veldgroep in de lijst hebt geselecteerd.

![ pas gebied ](../../images/ui/resources/schemas/apply-field.png) toe

Het nieuwe gebied wordt toegevoegd aan het canvas, en is namespaced onder uw [ huurder identiteitskaart ](../../api/getting-started.md#know-your-tenant_id) om conflicten met standaardXDM gebieden te vermijden. De veldgroep waarmee u het nieuwe veld hebt geassocieerd, wordt ook weergegeven onder **[!UICONTROL Field groups]** in de linkertrack.

![ identiteitskaart van de HTENT ](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
De overige velden die door de geselecteerde aangepaste veldgroep worden opgegeven, worden standaard uit het schema verwijderd. Als u enkele van deze velden aan het schema wilt toevoegen, selecteert u een veld dat tot de groep behoort en selecteert u vervolgens **[!UICONTROL Manage related fields]** in de rechtertrack.

#### Het veld toewijzen aan een aangepaste klasse {#add-to-class}

Selecteer onder **[!UICONTROL Assign to]** de optie **[!UICONTROL Class]**. Het invoerveld hieronder wordt vervangen door de naam van de aangepaste klasse van het huidige schema om aan te geven dat het nieuwe veld wordt toegewezen aan deze klasse.

![ de [!UICONTROL Class] optie die voor de nieuwe gebiedstoewijzing wordt geselecteerd.](../../images/ui/resources/schemas/assign-field-to-class.png)

Ga door met het configureren van het veld naar wens en selecteer **[!UICONTROL Apply]** als u klaar bent.

![[!UICONTROL Apply] geselecteerd voor het nieuwe veld.](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

Het nieuwe gebied wordt toegevoegd aan het canvas, en is namespaced onder uw [ huurder identiteitskaart ](../../api/getting-started.md#know-your-tenant_id) om conflicten met standaardXDM gebieden te vermijden. Als u de klassenaam in de linkerrails selecteert, wordt het nieuwe veld weergegeven als onderdeel van de klassenstructuur.

![ het nieuwe gebied dat op de structuur van de douaneklasse wordt toegepast, op het canvas wordt vertegenwoordigd.](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### Aangepaste velden toevoegen aan de structuur van standaardveldgroepen {#custom-fields-for-standard-groups}

Als het schema waaraan u werkt een objecttype heeft field Door een standaardveldgroep kunt u uw eigen aangepaste velden toevoegen aan dat standaardobject.

>[!WARNING]
>
Om het even welke gebieden die aan een gebiedsgroep in één schema worden toegevoegd zullen ook in alle andere schema&#39;s verschijnen die die zelfde gebiedsgroep gebruiken. Als een aangepast veld wordt toegevoegd aan een standaardveldgroep, wordt die veldgroep geconverteerd naar een aangepaste veldgroep en is de oorspronkelijke standaardveldgroep niet meer beschikbaar.
>
Als u aan de bètaversie van deze functie hebt deelgenomen, ontvangt u een dialoogvenster met informatie over de standaardveldgroepen die u eerder hebt aangepast. Nadat u **[!UICONTROL Acknowledge]** hebt geselecteerd, worden de weergegeven bronnen geconverteerd naar aangepaste veldgroepen.
>
![ de dialoog van de Bevestiging om standaardgebiedsgroepen om te zetten ](../../images/ui/resources/schemas/beta-extension-confirmation.png)

Om te beginnen, selecteer plus (**+**) pictogram naast de wortel van het voorwerp dat door de standaardgebiedsgroep wordt verstrekt.

![ voeg gebied aan standaardvoorwerp ](../../images/ui/resources/schemas/add-field-to-standard-object.png) toe

Er verschijnt een waarschuwingsbericht waarin u wordt gevraagd te bevestigen of u de standaardveldgroep wilt converteren. Selecteer **[!UICONTROL Continue creating field group]** om door te gaan.

![ bevestigt de omzetting van de gebiedsgroep ](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

Het canvas verschijnt opnieuw met een naamloze plaatsaanduiding voor het nieuwe veld. Merk op dat de naam van de standaardgebiedsgroep met &quot; ([!UICONTROL Extended])&quot;is toegevoegd om erop te wijzen dat het van de originele versie is gewijzigd. Gebruik vanaf hier de besturingselementen in de rechterspoorstaaf om de eigenschappen van het veld te definiëren.

![ Gebied dat aan standaardvoorwerp ](../../images/ui/resources/schemas/standard-field-group-converted.png) wordt toegevoegd

Nadat u de wijzigingen hebt toegepast, wordt het nieuwe veld onder de naamruimte van de huurder-id weergegeven in het standaardobject. Deze geneste naamruimte voorkomt conflicten met veldnamen binnen de veldgroep zelf om te voorkomen dat wijzigingen worden verbroken in andere schema&#39;s die dezelfde veldgroep gebruiken.

![ Gebied dat aan standaardvoorwerp ](../../images/ui/resources/schemas/added-to-standard-object.png) wordt toegevoegd

## Een schema inschakelen voor realtime-klantprofiel {#profile}

[!CONTEXTUALHELP]
id="platform_schemas_enableforprofile"
title="Een schema voor profiel inschakelen"
abstract="Wanneer een schema voor Profiel wordt toegelaten, nemen om het even welke datasets die van dit schema worden gecreeerd aan het Profiel van de Klant in real time deel, dat gegevens uit ongelijksoortige bronnen samenvoegt om een volledige mening van elke klant te construeren. Als een schema eenmaal is gebruikt om gegevens in te voeren in Profiel, kan het niet worden uitgeschakeld. Raadpleeg de documentatie voor meer informatie."

[ Real-Time het Profiel van de Klant ](../../../profile/home.md) voegt gegevens van ongelijksoortige bronnen samen om een volledige mening van elke individuele klant te construeren. Als u wilt dat de gegevens die door een schema worden vastgelegd, aan dit proces deelnemen, moet u het schema inschakelen voor gebruik in [!DNL Profile] .

>[!IMPORTANT]
>
Als u een schema voor [!DNL Profile] wilt inschakelen, moet er een primair identiteitsveld zijn gedefinieerd. Zie de gids op [ bepalende identiteitsgebieden ](../fields/identity.md) voor meer informatie.

Als u het schema wilt inschakelen, selecteert u eerst de naam van het schema in de linkertrack en vervolgens de **[!UICONTROL Profile]** -toets in de rechterrail.

![](../../images/ui/resources/schemas/profile-toggle.png)

Er verschijnt een pop-upvenster met de waarschuwing dat een schema dat is ingeschakeld en opgeslagen, niet kan worden uitgeschakeld. Selecteer **[!UICONTROL Enable]** om door te gaan.

![](../../images/ui/resources/schemas/profile-confirm.png)

Het canvas verschijnt weer met de schakeloptie [!UICONTROL Profile] ingeschakeld.

>[!IMPORTANT]
>
Aangezien het schema nog niet wordt bewaard, is dit het punt van geen terugkeer als u uw mening verandert over het laten van het schema aan het Profiel van de Klant in real time: zodra u sparen een toegelaten schema, kan het niet meer worden onbruikbaar gemaakt. Selecteer nogmaals de schakeloptie **[!UICONTROL Profile]** om het schema uit te schakelen.

Als u het proces wilt voltooien, selecteert u **[!UICONTROL Save]** om het schema op te slaan.

![](../../images/ui/resources/schemas/profile-enabled.png)

Het schema is nu ingeschakeld voor gebruik in Real-Time Klantprofiel. Wanneer het Platform gegevens in datasets opneemt die op dit schema worden gebaseerd, zullen die gegevens in uw samengevoegde gegevens van het Profiel worden opgenomen.

## Weergavenamen voor schemavelden bewerken {#display-names}

Nadat u een klasse hebt toegewezen en veldgroepen aan een schema hebt toegevoegd, kunt u de weergavenamen van de velden van een schema bewerken, ongeacht of die velden zijn voorzien door standaard- of aangepaste XDM-bronnen.

>[!NOTE]
>
Onthoud dat de weergavenamen van velden die tot standaardklassen of -veldgroepen behoren, alleen kunnen worden bewerkt in de context van een specifiek schema. Met andere woorden, het veranderen van de vertoningsnaam van een standaardgebied in één schema beïnvloedt andere schema&#39;s niet die de zelfde bijbehorende klasse of de gebiedsgroep gebruiken.
>
Zodra u veranderingen de vertoningsnamen voor de gebieden van een schema aanbrengt, worden die veranderingen onmiddellijk weerspiegeld in om het even welke bestaande datasets die op dat schema worden gebaseerd.

Wijzig de veldnamen in de weergavenamen door in te schakelen **[!UICONTROL Show display names for fields]** . Als u de weergavenaam van een schemaveld wilt bewerken, selecteert u het veld op het canvas. Geef in de rechtertrack de nieuwe naam onder **[!UICONTROL Display name]** .

![](../../images/ui/resources/schemas/display-name.png)

Selecteer **[!UICONTROL Apply]** in de rechtertrack en het canvas wordt bijgewerkt om de nieuwe weergavenaam van het veld weer te geven. Selecteer **[!UICONTROL Save]** om de wijzigingen toe te passen op het schema.

![](../../images/ui/resources/schemas/display-name-changed.png)

## De klasse van een schema wijzigen {#change-class}

U kunt de klasse van een schema op om het even welk punt tijdens het aanvankelijke samenstellingsproces veranderen alvorens het schema is bewaard.

>[!WARNING]
>
Het opnieuw toewijzen van de klasse voor een schema zou met uiterste voorzichtigheid moeten worden gedaan. Veldgroepen zijn alleen compatibel met bepaalde klassen. Als u de klasse wijzigt, worden het canvas en alle velden die u hebt toegevoegd opnieuw ingesteld.

Als u een klasse opnieuw wilt toewijzen, selecteert u **[!UICONTROL Assign]** links op het canvas.

![](../../images/ui/resources/schemas/assign-class-button.png)

Een dialoog verschijnt die een lijst van alle beschikbare klassen, met inbegrip van om het even welke die door uw organisatie (de eigenaar wordt &quot;[!UICONTROL Customer]&quot;) wordt bepaald en standaardklassen toont door Adobe worden bepaald.

Selecteer een klasse in de lijst om de beschrijving ervan rechts in het dialoogvenster weer te geven. U kunt ook **[!UICONTROL Preview class structure]** selecteren om de velden en metagegevens weer te geven die aan de klasse zijn gekoppeld. Selecteer **[!UICONTROL Assign class]** om door te gaan.

![](../../images/ui/resources/schemas/assign-class.png)

Er wordt een nieuw dialoogvenster geopend waarin u wordt gevraagd te bevestigen dat u een nieuwe klasse wilt toewijzen. Selecteer **[!UICONTROL Assign]** om te bevestigen.

![](../../images/ui/resources/schemas/assign-confirm.png)

Nadat de klassewijziging is bevestigd, wordt het canvas opnieuw ingesteld en gaat alle compositievoortgang verloren.

## Volgende stappen {#next-steps}

In dit document worden de basisbeginselen besproken van het maken en bewerken van schema&#39;s in de gebruikersinterface van het platform. Het wordt sterk geadviseerd dat u het [ leerprogramma van de schemaverwezenlijking ](../../tutorials/create-schema-ui.md) voor een uitvoerig werkschema voor de bouw van een volledig schema in UI herziet, met inbegrip van het creëren van de groepen van het douanegebied en gegevenstypes for unieke gebruiksgevallen.

Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie het [[!UICONTROL Schemas] overzicht van de werkruimte ](../overview.md).

Leren hoe te om schema&#39;s in [!DNL Schema Registry] API te beheren, zie de [ gids van het schemaeindpunt ](../../api/schemas.md).
