---
title: Op velden gebaseerde workflows in de Schema-editor (bèta)
description: Leer hoe u velden van bestaande veldgroepen afzonderlijk kunt toevoegen aan uw XDM-schema's (Experience Data Model).
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: b7c6f37d3e6d824465713647b624473cff188378
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# Op velden gebaseerde workflows in de Schema-editor (bèta)

>[!IMPORTANT]
>
>De workflows die in dit document worden beschreven, zijn momenteel in bèta. De functionaliteit en documentatie kunnen worden gewijzigd.

Adobe Experience Platform biedt een robuuste set gestandaardiseerde [veldgroepen](../schema/composition.md#field-group) voor gebruik in XDM-schema&#39;s (Experience Data Model). De structuur en de semantiek achter deze veldgroepen zijn zorgvuldig afgestemd op een grote verscheidenheid aan segmentatiegebruikstoepassingen en andere downstreamtoepassingen in Platform. U kunt ook uw eigen aangepaste veldgroepen definiëren voor unieke bedrijfsbehoeften.

Wanneer u een veldgroep aan een schema toevoegt, erft dat schema alle gebieden in die groep. U kunt nu echter afzonderlijke velden toevoegen aan uw schema zonder dat u andere velden uit de bijbehorende veldgroep hoeft op te nemen die u niet altijd hoeft te gebruiken.

Deze handleiding behandelt de verschillende methoden voor het toevoegen van afzonderlijke velden aan een schema in de gebruikersinterface van het Platform.

## Vereisten

Deze zelfstudie veronderstelt dat u met [samenstelling van XDM schema&#39;s](../schema/composition.md) vertrouwd bent en hoe te om de Redacteur van het Schema in Platform UI te gebruiken. Als u de stappen wilt volgen, moet u het proces starten van [het maken van een nieuw schema](./resources/schemas.md) en het toewijzen aan een standaardklasse voordat u doorgaat met deze handleiding.

## Velden verwijderen die zijn toegevoegd uit standaardveldgroepen

Nadat u een standaardveldgroep aan een schema hebt toegevoegd, kunt u alle standaardvelden verwijderen die u niet nodig hebt.

>[!NOTE]
>
>Het verwijderen van velden uit een standaardveldgroep heeft alleen invloed op het schema waaraan wordt gewerkt en heeft geen invloed op de veldgroep zelf. Als u standaardvelden in één schema verwijdert, zijn deze velden nog steeds beschikbaar in alle andere schema&#39;s waarin dezelfde veldgroep wordt gebruikt.

In het volgende voorbeeld is de standaardveldgroep **[!UICONTROL Demographic Details]** toegevoegd aan een schema. Als u één veld wilt verwijderen, zoals `taxId`, selecteert u het veld op het canvas en selecteert u **[!UICONTROL Remove]** in de rechtertrack.

![Eén veld verwijderen](../images/ui/field-based-workflows/remove-single-field.png)

Als er meerdere velden zijn die u wilt verwijderen, kunt u de veldgroep als geheel beheren. Selecteer een veld dat tot de groep behoort op het canvas en selecteer vervolgens **[!UICONTROL Manage related fields]** in de rechtertrack.

![Gerelateerde velden beheren](../images/ui/field-based-workflows/manage-related-fields.png)

Er verschijnt een dialoogvenster met de structuur van de veldgroep in kwestie. Hier kunt u de beschikbare selectievakjes gebruiken om de velden die u nodig hebt in of uit te schakelen. Als u tevreden bent, selecteert u **[!UICONTROL Add fields]**.

![Velden selecteren uit veldgroep](../images/ui/field-based-workflows/select-fields.png)

Het canvas verschijnt weer met alleen de geselecteerde velden in de schemastructuur.

![Toegevoegde velden](../images/ui/field-based-workflows/fields-added.png)

## Standaardvelden rechtstreeks aan een schema toevoegen

U kunt velden van standaardveldgroepen rechtstreeks aan een schema toevoegen zonder dat u eerst de corresponderende veldgroep hoeft te kennen. Als u een standaardveld aan een schema wilt toevoegen, selecteert u de plusknop (**+**) naast de naam van het schema in het canvas. Er wordt een tijdelijke aanduiding **[!UICONTROL Untitled Field]** weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![Tijdelijke aanduiding voor veld](../images/ui/field-based-workflows/root-custom-field.png)

Typ onder **[!UICONTROL Field name]** de naam van het veld dat u wilt toevoegen. Het systeem zoekt automatisch naar standaardvelden die overeenkomen met de query en geeft deze weer onder **[!UICONTROL Recommended Standard Fields]**, inclusief de veldgroepen waartoe ze behoren.

![Aanbevolen standaardvelden](../images/ui/field-based-workflows/standard-field-search.png)

Sommige standaardvelden hebben dezelfde naam, maar de structuur van deze velden kan afhankelijk zijn van de veldgroep waaruit ze afkomstig zijn. Als een standaardveld is genest in een bovenliggend object in de veldgroepsstructuur, wordt het bovenliggende veld ook opgenomen in het schema als het onderliggende veld wordt toegevoegd.

Selecteer het voorvertoningspictogram (![Voorvertoningspictogram](../images/ui/field-based-workflows/preview-icon.png)) naast een standaardveld om de structuur van de veldgroep weer te geven en beter te begrijpen hoe deze kan worden genest. Om het standaardgebied aan het schema toe te voegen, selecteer het plusteken (![plus pictogram](../images/ui/field-based-workflows/add-icon.png)).

![Standaardveld toevoegen](../images/ui/field-based-workflows/add-standard-field.png)

Het canvas wordt bijgewerkt om het standaardveld weer te geven dat aan het schema is toegevoegd, inclusief bovenliggende velden die het is genest onder de veldgroepsstructuur. De naam van de veldgroep wordt ook vermeld onder **[!UICONTROL Field groups]** in de linkertrack. Als u meer velden van dezelfde veldgroep wilt toevoegen, selecteert u **[!UICONTROL Manage related fields]** in de rechtertrack.

![Standaardveld toegevoegd](../images/ui/field-based-workflows/standard-field-added.png)

## Aangepaste velden rechtstreeks aan een schema toevoegen

Als u eerder [aangepaste veldgroepen](./resources/field-groups.md#create) hebt gemaakt, kunt u direct aangepaste velden aan het schema toevoegen zonder deze eerst afzonderlijk aan een aangepaste veldgroep toe te voegen.

>[!WARNING]
>
>Wanneer u een aangepast veld aan een schema toevoegt, moet u nog steeds een bestaande aangepaste veldgroep selecteren waaraan u het wilt koppelen. Dit betekent dat u minstens één aangepaste veldgroep moet hebben gedefinieerd in de sandbox waarin u werkt, om aangepaste velden rechtstreeks aan een schema toe te voegen. Bovendien zullen andere schema&#39;s die die groep van het douaneveld gebruiken ook het onlangs toegevoegde gebied erven nadat u uw veranderingen bewaart.

Als u velden wilt toevoegen aan het hoofdniveau van een schema, selecteert u de plusknop (**+**) naast de naam van het schema in het canvas. Er wordt een tijdelijke aanduiding **[!UICONTROL Untitled Field]** weergegeven in de schemastructuur en de juiste spoorwegupdates om besturingselementen voor de configuratie van het veld zichtbaar te maken.

![Aangepast basisveld](../images/ui/field-based-workflows/root-custom-field.png)

Typ de naam van het aangepaste veld dat u wilt toevoegen en het systeem zoekt automatisch naar overeenkomende standaardvelden. Als u een nieuw aangepast veld wilt maken, selecteert u de bovenste optie die wordt toegevoegd met **([!UICONTROL New Field])**.

![Nieuw veld](../images/ui/field-based-workflows/custom-field-search.png)

Hier geeft u een weergavenaam en gegevenstype op voor het veld. Selecteer onder **[!UICONTROL Assign field group]** de aangepaste veldgroep waaraan u het nieuwe veld wilt koppelen.

![Veldgroep selecteren](../images/ui/field-based-workflows/select-field-group.png)

Selecteer **[!UICONTROL Apply]** als u klaar bent.

![Veld toepassen](../images/ui/field-based-workflows/apply-field.png)

Het nieuwe veld wordt toegevoegd aan het canvas en krijgt een naam onder de [huurder-id](../api/getting-started.md#know-your-tenant_id) om conflicten met standaard-XDM-velden te voorkomen. De veldgroep waaraan u het nieuwe veld hebt gekoppeld, wordt ook weergegeven onder **[!UICONTROL Field groups]** in de linkertrack.

![Tenant-id](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>De overige velden die door de geselecteerde aangepaste veldgroep worden opgegeven, worden standaard uit het schema verwijderd. Als u sommige van deze gebieden aan het schema wilt toevoegen, selecteer een gebied dat tot de groep behoort en dan **[!UICONTROL Manage related fields]** in het juiste spoor selecteren.

### Aangepaste velden toevoegen aan de structuur van standaardveldgroepen

Als het schema u werkt een voorwerp-type gebied heeft dat door een standaardgebiedsgroep wordt verstrekt, kunt u uw eigen douanevelden aan dat standaardobject toevoegen. Selecteer de plusknop (**+**) naast de hoofdmap van het object en geef de details van het aangepaste veld op in de rechtertrack.

![Veld toevoegen aan standaardobject](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Nadat u de wijzigingen hebt toegepast, wordt het nieuwe veld onder de naamruimte van de huurder-id weergegeven in het standaardobject. Deze geneste naamruimte voorkomt conflicten met veldnamen binnen de veldgroep zelf om te voorkomen dat wijzigingen worden verbroken in andere schema&#39;s die dezelfde veldgroep gebruiken.

## Volgende stappen

Deze gids behandelde de nieuwe op gebied-gebaseerde werkschema&#39;s voor de Redacteur van het Schema in de UI van het Platform. Voor meer informatie over het beheren van schema&#39;s in UI, zie [UI overzicht](./overview.md).
