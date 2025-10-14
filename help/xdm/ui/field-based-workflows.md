---
title: Op velden gebaseerde workflows in de Schema-editor
description: Leer hoe u velden van bestaande veldgroepen afzonderlijk kunt toevoegen aan uw XDM-schema's (Experience Data Model).
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# Op velden gebaseerde workflows in de Schema-editor

Adobe Experience Platform verstrekt een robuuste reeks gestandaardiseerde [&#x200B; gebiedsgroepen &#x200B;](../schema/composition.md#field-group) voor gebruik in de schema&#39;s van de Gegevens van de Ervaring van het Model (XDM). De structuur en de semantiek achter deze veldgroepen zijn zorgvuldig afgestemd op een grote verscheidenheid aan gebruikscategorieën voor segmentatie en andere downstreamtoepassingen in Experience Platform. U kunt ook uw eigen aangepaste veldgroepen definiëren voor unieke bedrijfsbehoeften.

Wanneer u een veldgroep aan een schema toevoegt, erft dat schema alle gebieden in die groep. U kunt nu echter afzonderlijke velden toevoegen aan uw schema zonder dat u andere velden uit de bijbehorende veldgroep hoeft op te nemen die u niet altijd hoeft te gebruiken.

In deze handleiding worden de verschillende methoden besproken voor het toevoegen van afzonderlijke velden aan een schema in de gebruikersinterface van Experience Platform.

## Vereisten

Dit leerprogramma veronderstelt dat u met de [&#x200B; samenstelling van schema&#39;s XDM &#x200B;](../schema/composition.md) vertrouwd bent en hoe te om de Redacteur van het Schema in Experience Platform UI te gebruiken. Om langs te volgen, zou u het proces van [&#x200B; moeten beginnen creërend een nieuw schema &#x200B;](./resources/schemas.md) en het aan een standaardklasse toe te wijzen alvorens met deze gids verder te gaan.

## Velden verwijderen die zijn toegevoegd uit standaardveldgroepen {#remove-field-group}

Nadat u een standaardveldgroep aan een schema hebt toegevoegd, kunt u alle standaardvelden verwijderen die u niet nodig hebt.

>[!NOTE]
>
>Het verwijderen van velden uit een standaardveldgroep heeft alleen invloed op het schema waaraan wordt gewerkt en heeft geen invloed op de veldgroep zelf. Als u standaardvelden in één schema verwijdert, zijn deze velden nog steeds beschikbaar in alle andere schema&#39;s waarin dezelfde veldgroep wordt gebruikt.

In het volgende voorbeeld is de standaardveldgroep **[!UICONTROL Demographic Details]** toegevoegd aan een schema. Als u één veld, zoals `maritalStatus` , wilt verwijderen, selecteert u het veld op het canvas en selecteert u vervolgens **[!UICONTROL Remove]** in de rechtertrack.

![&#x200B; de Redacteur van het Schema met de gebiedsgroep, het gebied van de Status van het Gezinshuis, en verwijdert benadrukte.](../images/ui/field-based-workflows/remove-single-field.png)

Als er meerdere velden zijn die u wilt verwijderen, kunt u de veldgroep als geheel beheren. Selecteer een veld dat tot de groep behoort op het canvas en selecteer vervolgens **[!UICONTROL Manage related fields]** in de rechtertrack.

![&#x200B; de Redacteur van het Schema met een gebied en beheer verwante benadrukte gebieden.](../images/ui/field-based-workflows/manage-related-fields.png)

Er verschijnt een dialoogvenster met de structuur van de veldgroep in kwestie. Hier kunt u de beschikbare selectievakjes gebruiken om de velden die u nodig hebt in of uit te schakelen. Selecteer **[!UICONTROL Confirm]** als u tevreden bent.

![&#x200B; beheert verwante gebieden dialoog met het diagram van de gebiedsgroep en bevestigt benadrukte.](../images/ui/field-based-workflows/select-fields.png)

Het canvas verschijnt weer met alleen de geselecteerde velden in de schemastructuur.

![&#x200B; de Redacteur van het Schema met de onlangs uitgegeven benadrukte gebiedsgroep.](../images/ui/field-based-workflows/fields-added.png)

## Standaardvelden rechtstreeks aan een schema toevoegen

U kunt velden van standaardveldgroepen rechtstreeks aan een schema toevoegen zonder dat u eerst de corresponderende veldgroep hoeft te kennen. Om een standaardgebied aan een schema toe te voegen, selecteer plus (**+**) pictogram naast de naam van het schema in het canvas. Er wordt een tijdelijke aanduiding **[!UICONTROL Untitled Field]** weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![&#x200B; de Redacteur van het Schema met benadrukte placeholder van het wortelgebied.](../images/ui/field-based-workflows/root-custom-field.png)

Typ onder **[!UICONTROL Field name]** de naam van het veld dat u wilt toevoegen. Het systeem zoekt automatisch naar standaardvelden die overeenkomen met de query en geeft deze onder **[!UICONTROL Recommended Standard Fields]** weer, inclusief de veldgroepen waartoe ze behoren.

![&#x200B; de benadrukte naam van het Gebied en een lijst van geadviseerde standaardgebieden binnen de gebiedseigenschappen van de Redacteur van het Schema worden getoond.](../images/ui/field-based-workflows/standard-field-search.png)

Sommige standaardvelden hebben dezelfde naam, maar de structuur van deze velden kan afhankelijk zijn van de veldgroep waaruit ze afkomstig zijn. Als een standaardveld is genest in een bovenliggend object in de veldgroepsstructuur, wordt het bovenliggende veld ook opgenomen in het schema als het onderliggende veld wordt toegevoegd.

Selecteer het voorproefpictogram (![&#x200B; pictogram van de Voorproef &#x200B;](/help/images/icons/preview.png)) naast een standaardgebied om de structuur van zijn gebiedsgroep te bekijken en beter te begrijpen hoe het zou kunnen worden genest. Om het standaardgebied aan het schema toe te voegen, selecteer het plusteken (![&#x200B; plus pictogram &#x200B;](/help/images/icons/add-circle.png)).

![&#x200B; voegt pictogram toe dat op een punt van de voorgestelde standaardgebieden wordt benadrukt.](../images/ui/field-based-workflows/add-standard-field.png)

Het canvas wordt bijgewerkt om het standaardveld weer te geven dat aan het schema is toegevoegd, inclusief bovenliggende velden die het is genest onder de structuur van de veldgroep. De naam van de veldgroep wordt ook vermeld onder **[!UICONTROL Field groups]** in de linkertrack. Als u meer velden van dezelfde veldgroep wilt toevoegen, selecteert u **[!UICONTROL Manage related fields]** in de rechtertrack.

![&#x200B; de Redacteur van het Schema met de groep van het Gebied, standaardgebied, en leidt verwante benadrukte gebieden.](../images/ui/field-based-workflows/standard-field-added.png)

## Aangepaste velden rechtstreeks aan een schema toevoegen

Net als bij de workflow voor standaardvelden kunt u ook uw eigen aangepaste velden rechtstreeks aan een schema toevoegen.

Om gebieden aan het wortelniveau van een schema toe te voegen, selecteer plus (**+**) pictogram naast de naam van het schema in het canvas. Er wordt een tijdelijke aanduiding **[!UICONTROL Untitled Field]** weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![&#x200B; de Redacteur van het Schema met toevoegen pictogram en een naamloos benadrukt gebied van het wortelniveau.](../images/ui/field-based-workflows/root-custom-field.png)

Typ de naam van het veld dat u wilt toevoegen en het systeem zoekt automatisch naar de desbetreffende standaardvelden. Om een nieuw douanegebied in plaats daarvan tot stand te brengen, selecteer de hoogste optie die met **wordt toegevoegd ([!UICONTROL New Field])**.

![&#x200B; de naam van het Gebied en de Nieuwe die suggestie van het Gebied binnen de gebiedseigenschappen van de Redacteur van het Schema wordt benadrukt.](../images/ui/field-based-workflows/custom-field-search.png)

Hier geeft u een weergavenaam en gegevenstype op voor het veld. Onder **[!UICONTROL Assign field group]** moet u een veldgroep selecteren waaraan het nieuwe veld moet worden gekoppeld. Begin in de naam van de gebiedsgroep te typen, en als u eerder [&#x200B; de groepen van het douanegebied &#x200B;](./resources/field-groups.md#create) hebt gecreeerd zullen zij in de dropdown lijst verschijnen. U kunt ook een unieke naam in het veld typen om een nieuwe veldgroep te maken.

![&#x200B; de naam van de Vertoning, het Type, en wijst aan gebied toe bezitsmontages die in de Redacteur van het Schema worden benadrukt.](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Als u een bestaande aangepaste veldgroep selecteert, nemen alle andere schema&#39;s die die veldgroep gebruiken ook het nieuwe toegevoegde veld over nadat u de wijzigingen hebt opgeslagen. Selecteer daarom alleen een bestaande veldgroep als u dit type propagatie wilt gebruiken. Anders kunt u beter een nieuwe aangepaste veldgroep maken.

Selecteer **[!UICONTROL Apply]** als u klaar bent.

![&#x200B; is van toepassing wordt benadrukt op de gebiedseigenschappen van de Redacteur van het Schema.](../images/ui/field-based-workflows/apply-field.png)

Het nieuwe gebied wordt toegevoegd aan het canvas, en is namespaced onder uw [&#x200B; huurder identiteitskaart &#x200B;](../api/getting-started.md#know-your-tenant_id) om conflicten met standaardXDM gebieden te vermijden. De veldgroep waarmee u het nieuwe veld hebt geassocieerd, wordt ook weergegeven onder **[!UICONTROL Field groups]** in de linkertrack.

![&#x200B; de Redacteur van het Schema met het nieuwe gebied dat aan het canvas wordt toegevoegd, en namespaced onder uw huurdersidentiteitskaart De groep en het gebied van het Gebied worden benadrukt.](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>De overige velden die door de geselecteerde aangepaste veldgroep worden opgegeven, worden standaard uit het schema verwijderd. Als u enkele van deze velden aan het schema wilt toevoegen, selecteert u een veld dat tot de groep behoort en selecteert u vervolgens **[!UICONTROL Manage related fields]** in de rechtertrack.

### Aangepaste velden toevoegen aan de structuur van standaardveldgroepen

Als het schema u werkt een voorwerp-type gebied heeft dat door een standaardgebiedsgroep wordt verstrekt, kunt u uw eigen douanevelden aan dat standaardobject toevoegen. Selecteer het plusteken (**+**) naast de wortel van het voorwerp.

>[!IMPORTANT]
>
>Om het even welke gebieden die aan een gebiedsgroep in één schema worden toegevoegd zullen ook in alle andere schema&#39;s verschijnen die die zelfde gebiedsgroep gebruiken.

![&#x200B; de Redacteur van het Schema met het plusteken naast een benadrukt standaardobject.](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Zie [&#x200B; creeer en geef schema&#39;s in de gids UI &#x200B;](./resources/schemas.md#custom-fields-for-standard-groups) voor meer informatie bij het toevoegen van douanegebieden uit.

## Volgende stappen

Deze gids behandelde de nieuwe op gebied-gebaseerde werkschema&#39;s voor de Redacteur van het Schema in Experience Platform UI. Voor meer informatie over het beheren van schema&#39;s in UI, zie het [&#x200B; overzicht UI &#x200B;](./overview.md).
