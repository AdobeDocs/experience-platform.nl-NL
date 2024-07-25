---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;veldgroep;veldgroepen;
solution: Experience Platform
title: Groep met schemavelden maken en bewerken in de gebruikersinterface
description: Leer hoe u groepen met schemavelden maakt en bewerkt in de gebruikersinterface van het Experience Platform.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---

# Groepen schemavelden maken en bewerken in de gebruikersinterface {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="Standaardfilter of aangepast veldgroepfilter"
>abstract="De lijst met beschikbare veldgroepen wordt vooraf gefilterd op basis van de manier waarop ze zijn gemaakt. Selecteer het keuzerondje dat u wilt kiezen tussen de opties Standaard en Aangepast. De optie Standaard toont entiteiten die zijn gemaakt door Adobe en de optie Aangepast geeft entiteiten weer die binnen uw organisatie zijn gemaakt. Raadpleeg de documentatie voor meer informatie over het maken en bewerken van veldgroepen."

In het Model van Gegevens van de Ervaring (XDM), zijn de groepen van het schemagebied herbruikbare componenten die één of meerdere gebieden bepalen die bepaalde functies zoals persoonlijke details, hotelvoorkeur, of adres uitvoeren. Veldgroepen moeten worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert.

Een veldgroep definieert met welke klasse(n) het compatibel is, op basis van het gedrag van de gegevens die de veldgroep vertegenwoordigt (record- of tijdreeks). Dit betekent dat niet alle veldgroepen beschikbaar zijn voor gebruik met alle klassen.

Adobe Experience Platform biedt een groot aantal standaardveldgroepen die een groot aantal gevallen van marketinggebruik bestrijken. U kunt echter ook uw eigen aangepaste veldgroepen maken en bewerken om aanvullende concepten voor uw bedrijf in uw XDM-schema&#39;s te definiëren. Deze handleiding biedt een overzicht van het maken, bewerken en beheren van aangepaste veldgroepen voor uw organisatie in de interface van het platform.

## Vereisten {#prerequisites}

Deze handleiding vereist een goed begrip van XDM System. Verwijs naar het [ XDM overzicht ](../../home.md) voor een inleiding aan de rol van XDM binnen het Experience Platform ecosysteem, en de [ grondbeginselen van schemacompositie ](../../schema/composition.md) voor hoe de gebiedsgroepen tot XDM schema&#39;s bijdragen.

Terwijl niet vereist voor deze gids, wordt het geadviseerd dat u ook het leerprogramma volgt op [ samenstellend een schema in UI ](../../tutorials/create-schema-ui.md) om zich met de diverse mogelijkheden van [!DNL Schema Editor] vertrouwd te maken.

## Een nieuwe veldgroep maken {#create}

Als u een nieuwe veldgroep wilt maken, moet u eerst een schema selecteren waaraan de veldgroep wordt toegevoegd. U kunt verkiezen om [ een nieuw schema ](./schemas.md#create) tot stand te brengen of [ een bestaand schema selecteren om uit te geven ](./schemas.md#edit).

Als u het schema hebt geopend in de [!DNL Schema Editor] , selecteert u **[!UICONTROL Add]** naast de [!UICONTROL Field groups] -sectie in de linkertrack.

![](../../images/ui/resources/field-groups/add-field-group.png)

Selecteer **[!UICONTROL Create new field group]** in het dialoogvenster dat wordt weergegeven. Hier kunt u een **[!UICONTROL Display name]** en **[!UICONTROL Description]** opgeven voor de veldgroep. Selecteer **[!UICONTROL Add field groups]** als u klaar bent.

![](../../images/ui/resources/field-groups/create-field-group.png)

De lus [!DNL Schema Editor] verschijnt weer, terwijl de nieuwe veldgroep in de linkertrack wordt weergegeven. Aangezien dit een gloednieuwe veldgroep is, biedt deze momenteel geen velden aan het schema en blijft het canvas daarom ongewijzigd. U kunt [ nu beginnen toevoegend gebieden aan de gebiedsgroep ](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Veldgroepen filteren {#filter}

De lijst met beschikbare veldgroepen wordt vooraf gefilterd op basis van de manier waarop ze zijn gemaakt. Met de standaardinstelling worden de veldgroepen weergegeven die door Adobe worden gedefinieerd. Nochtans, kunt u de lijst ook filtreren om die te tonen die door uw organisatie worden gecreeerd. Selecteer het keuzerondje dat u wilt kiezen tussen de opties [!UICONTROL Standard] en [!UICONTROL Custom] . De optie [!UICONTROL Standard] toont entiteiten die zijn gemaakt door Adobe en de optie [!UICONTROL Custom] geeft entiteiten weer die binnen uw organisatie zijn gemaakt.

![ het [!UICONTROL Field groups] lusje van de [!UICONTROL Schemas] werkruimte met [!UICONTROL Standard] en [!UICONTROL Custom] benadrukte.](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)

## Een bestaande veldgroep bewerken {#edit}

>[!NOTE]
>
>Alleen aangepaste veldgroepen die door uw organisatie zijn gedefinieerd, kunnen volledig worden bewerkt en aangepast. Voor de belangrijkste veldgroepen die door Adobe worden gedefinieerd, kunnen alleen de weergavenamen voor de bijbehorende velden worden bewerkt binnen de context van de afzonderlijke schema&#39;s. Zij worden vermeld in de Redacteur van het Schema door een hangslotpictogram (![ A hangslotpictogram.](/help/images/icons/lock-closed.png)). Zie de sectie op [ het uitgeven vertoningsnamen voor schemagebieden ](./schemas.md#display-names) voor details.
>
>Nadat een aangepaste veldgroep is opgeslagen en in een schema voor gegevensinvoer is gebruikt, kunnen daarna alleen additieve wijzigingen in de veldgroep worden aangebracht. Zie de [ regels van schemaevolutie ](../../schema/composition.md#evolution) voor meer informatie.

Als u een bestaande veldgroep wilt bewerken, moet u eerst een schema openen waarin de veldgroep in de [!DNL Schema Editor] wordt gebruikt. U kunt [ een bestaand schema selecteren om uit te geven ](./schemas.md#edit), of u kunt [ een nieuw schema ](./schemas.md#create) tot stand brengen en de gebiedsgroep in kwestie toevoegen.

Zodra u het schema open in de redacteur hebt, kunt u [ beginnen toevoegend gebieden aan de gebiedsgroep ](#add-fields).

## Velden toevoegen aan een veldgroep {#add-fields}

>[!NOTE]
>
>Deze sectie richt zich op het toevoegen van velden aan aangepaste veldgroepen. Voor informatie over hoe te om douanegebieden aan standaardgebiedsgroepen toe te voegen, verwijs naar de [ schema&#39;s UI gids ](./schemas.md#custom-fields-for-standard-groups).

Om gebieden aan een groep van het douanegebied toe te voegen, begin door **plus (+) te selecteren** pictogram naast de naam van het schema in het canvas.

![](../../images/ui/resources/field-groups/add-field.png)

Er verschijnt een tijdelijke aanduiding **[!UICONTROL Untitled Field]** in het canvas en de rechterrails worden bijgewerkt om besturingselementen weer te geven waarmee de eigenschappen van het veld worden geconfigureerd. Zie de gids op [ definiërend gebieden in UI ](../fields/overview.md#define) voor specifieke stappen op hoe te om verschillende gebiedstypes te vormen.

Selecteer onder **[!UICONTROL Assign to]** de optie **[!UICONTROL Field Group]** en gebruik vervolgens het vervolgkeuzemenu om de gewenste veldgroep in de lijst te selecteren. U kunt beginnen in naam van de gebiedsgroep in te typen om benedenresultaten te beperken.

![](../../images/ui/resources/field-groups/select-field-group.png)

Selecteer onder **[!UICONTROL Assign to]** de optie **[!UICONTROL Field Group]** en gebruik vervolgens het vervolgkeuzemenu om de gewenste veldgroep in de lijst te selecteren. U kunt beginnen in naam van de gebiedsgroep in te typen om benedenresultaten te beperken.

![](../../images/ui/resources/field-groups/select-field-group.png)

Nadat het veld aan het schema is toegevoegd, wordt het toegewezen aan de geselecteerde veldgroep. Voeg zo veel velden toe aan de veldgroep. Als u klaar bent, selecteert u **[!UICONTROL Save]** om zowel het schema als de veldgroep op te slaan.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Als dezelfde veldgroep al in andere schema&#39;s wordt gebruikt, worden de toegevoegde velden automatisch in die schema&#39;s weergegeven.

## Volgende stappen {#next-steps}

In deze handleiding wordt beschreven hoe u veldgroepen kunt maken en bewerken met behulp van de interface van het platform. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie het [[!UICONTROL Schemas] overzicht van de werkruimte ](../overview.md).

Leren hoe te om gebiedsgroepen te beheren gebruikend [!DNL Schema Registry] API, zie de [ gids van het gebiedsgroepseindpunt van groepen ](../../api/field-groups.md).
