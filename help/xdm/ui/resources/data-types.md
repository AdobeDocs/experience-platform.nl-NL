---
keywords: Experience Platform;thuis;populaire onderwerpen;ui;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Gegevensmodel;Gegevensmodel;Gegevensmodel;Schemaregister;Schema;Schema;schema's;Schema's;Schema's;creëren;gegevenstype;gegevenstypen;
solution: Experience Platform
title: Gegevenstypen maken en bewerken met de gebruikersinterface
type: Tutorial
description: Leer hoe u gegevenstypen maakt en bewerkt in de gebruikersinterface van het Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: c04e5a49f2a4e90345ca20ecd0547d02b5004fcf
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 0%

---

# Gegevenstypen maken en bewerken met de gebruikersinterface {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="Standaardfilter of aangepast gegevenstype"
>abstract="De lijst met beschikbare gegevenstypen wordt vooraf gefilterd op basis van de manier waarop ze zijn gemaakt. Selecteer het keuzerondje dat u wilt kiezen tussen de opties Standaard en Aangepast. De optie Standaard toont entiteiten die zijn gemaakt door Adobe en de optie Aangepast geeft entiteiten weer die binnen uw organisatie zijn gemaakt. Raadpleeg de documentatie voor meer informatie over het maken en bewerken van gegevenstypen."

In het Model van Gegevens van de Ervaring (XDM), zijn de gegevenstypes herbruikbare gebieden die veelvoudige subfields bevatten. Terwijl gelijkaardig aan de groepen van het schemagebied in zoverre zij voor het verenigbare gebruik van een multi-gebiedstructuur toestaan, zijn de gegevenstypes flexibeler omdat zij overal in de schemastructuur kunnen worden omvat terwijl de gebiedsgroepen slechts op het wortelniveau kunnen worden toegevoegd.

Adobe Experience Platform biedt vele standaardgegevenstypen die kunnen worden gebruikt voor een groot aantal gangbare praktijkbeheertoepassingen. U kunt echter ook uw eigen aangepaste gegevenstypen definiëren om aan uw unieke bedrijfsbehoeften te voldoen.

>[!NOTE]
>
>Als een veld is gedefinieerd als een specifiek gegevenstype, kunt u niet hetzelfde veld met een ander gegevenstype in een ander schema maken. Deze beperking geldt voor de huurder van uw organisatie.

Deze zelfstudie behandelt de stappen voor het maken en bewerken van aangepaste gegevenstypen in de gebruikersinterface van Platform.

## Vereisten {#prerequisites}

Deze handleiding vereist een goed begrip van XDM System. Zie de [XDM-overzicht](../../home.md) voor een inleiding op de rol van XDM binnen het ecosysteem van het Experience Platform, en [grondbeginselen van de schemacompositie](../../schema/composition.md) voor hoe de gegevenstypes tot schema XDM bijdragen.

Hoewel dit niet nodig is voor deze handleiding, wordt u aangeraden de zelfstudie ook op te volgen [samenstellen van een schema in UI](../../tutorials/create-schema-ui.md) om vertrouwd te maken met de verschillende mogelijkheden van de [!DNL Schema Editor].

## Open de [!DNL Schema Editor] voor een gegevenstype {#data-type}

Selecteer in de interface Platform de optie **[!UICONTROL Schemas]** in de linkernavigatie om de [!UICONTROL Schemas] werkruimte selecteert u vervolgens de **[!UICONTROL Data types]** tab. Er wordt een lijst met beschikbare gegevenstypen weergegeven. De lijst met gegevenstypen wordt automatisch gefilterd op basis van de manier waarop ze zijn gemaakt. Met de standaardinstelling worden de gegevenstypen weergegeven die door de Adobe worden gedefinieerd. U kunt de lijst ook filteren om de lijsten weer te geven die door uw organisatie zijn gemaakt.

![De [!UICONTROL Schemas] werkruimte met [!UICONTROL Schemas] in de linkernavigatie en [!UICONTROL Data types] gemarkeerd.](../../images/ui/resources/data-types/data-types-tab.png)

Hier hebt u de volgende opties:

- [Een nieuw gegevenstype maken](#create)
- [Gegevenstypen filteren](#filter)
- [Een bestaand gegevenstype selecteren om te bewerken](#edit)

### Een nieuw gegevenstype maken {#create}

Selecteer op het tabblad **[!UICONTROL Data types]** de optie **[!UICONTROL Create data type]**.

![De [!UICONTROL Schemas] werkruimte [!UICONTROL Data types] tab met [!UICONTROL Create data type] gemarkeerd.](../../images/ui/resources/data-types/create.png)

De [!DNL Schema Editor] wordt weergegeven en geeft u de huidige structuur van het nieuwe gegevenstype op het canvas weer. Aan de rechterkant van de editor kunt u een weergavenaam en een optionele beschrijving voor het gegevenstype opgeven. Zorg ervoor dat u een unieke en beknopte naam voor uw gegevenstype opgeeft, omdat dit zo is dat het wordt geïdentificeerd wanneer u het aan een schema toevoegt.

Deze zelfstudie maakt een gegevenstype dat een restauratie-eigenschap beschrijft, zodat het gegevenstype de weergavenaam &quot;Restaurant&quot; krijgt.

![](../../images/ui/resources/data-types/data-type-properties.png)

Vanaf hier kunt u naar de [volgende sectie](#add-fields) om velden toe te voegen aan het nieuwe gegevenstype.

### Gegevenstypen filteren {#filter}

De lijst met beschikbare gegevenstypen wordt vooraf gefilterd op basis van de manier waarop ze zijn gemaakt. Selecteer het keuzerondje dat u wilt kiezen tussen de [!UICONTROL Standard] en [!UICONTROL Custom] opties. De [!UICONTROL Standard] toont entiteiten die zijn gemaakt door Adobe en de optie [!UICONTROL Custom] geeft entiteiten weer die binnen uw organisatie zijn gemaakt.

![De [!UICONTROL Data types] tabblad van het [!UICONTROL Schemas] werkruimte met [!UICONTROL Standard] en [!UICONTROL Custom] gemarkeerd.](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### Een bestaand gegevenstype bewerken {#edit}

>[!NOTE]
>
>Zodra een bestaand gegevenstype in een schema wordt gebruikt dat voor gebruik in het Profiel van de Klant in real time is toegelaten, slechts kunnen niet-destructieve veranderingen daarna in dat gegevenstype worden aangebracht. Zie de [regels voor schemaontwikkeling](../../schema/composition.md#evolution) voor meer informatie .

Alleen aangepaste gegevenstypen die door uw organisatie zijn gedefinieerd, kunnen worden bewerkt. Selecteren **[!UICONTROL Custom]** om alleen aangepaste gegevenstypen weer te geven die eigendom zijn van uw organisatie.

Selecteer in de lijst het gegevenstype dat u wilt bewerken om de rechtertrack te openen, met daarin de details van het gegevenstype. Vanuit het deelvenster Details kunt u ook een voorbeeldbestand downloaden, de JSON-structuur kopiëren of het gegevenstype aan een pakket toevoegen.

Selecteer de naam van het gegevenstype in het rechterspoor om de structuur ervan te openen in het dialoogvenster [!DNL Schema Editor].

![De [!UICONTROL Data types] tabblad van het [!UICONTROL Schemas] werkruimte, met een gegevenstype, [!UICONTROL Custom] en het gegevenstype [!UICONTROL Name] gemarkeerd.](../../images/ui/resources/data-types/edit.png)

## Velden toevoegen aan het gegevenstype {#add-fields}

Als u wilt beginnen met het toevoegen van velden aan het gegevenstype, selecteert u de optie **plus (+)** pictogram naast het veld op hoofdniveau op het canvas. Hieronder wordt een nieuw veld weergegeven en de rechtertrack wordt bijgewerkt met besturingselementen voor het nieuwe veld.

![](../../images/ui/resources/data-types/new-field.png)

Gebruik de besturingselementen in het rechterspoor om de details van het nieuwe veld te configureren. Zie de handleiding op [velden definiëren in de gebruikersinterface](../fields/overview.md#define) voor specifieke stappen op om het gebied aan het gegevenstype te vormen en toe te voegen.

Het gegevenstype Restaurant vereist een tekenreeksveld voor de naam van het restaurant. Als zodanig [!UICONTROL Field name] is ingesteld als &quot;name&quot; en [!UICONTROL Type] is ingesteld als &quot;[!UICONTROL String]&quot;. Selecteren **[!UICONTROL Apply]** om de wijzigingen toe te passen op het veld.

![](../../images/ui/resources/data-types/name-field.png)

Voeg desgewenst meer velden aan het gegevenstype toe. Het gegevenstype Restaurant heeft nu extra velden voor merk, zitcapaciteit en vloerruimte.

![](../../images/ui/resources/data-types/more-fields.png)

Naast basisvelden kunt u ook andere gegevenstypen nesten binnen het aangepaste gegevenstype. Het gegevenstype Restaurant vereist bijvoorbeeld een veld dat het fysieke adres van de eigenschap vertegenwoordigt. In dit scenario kunt u een nieuw &quot;adres&quot;gebied toevoegen dat het standaardgegevenstype &quot;[!UICONTROL Postal address]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Dit toont aan hoe de flexibele gegevenstypes in termen van het beschrijven van uw gegevens kunnen zijn: de gegevenstypes kunnen gebieden gebruiken die ook gegevenstypes zijn, die zelf verdere gegevenstypes kunnen bevatten, etc. Dit staat u toe om gemeenschappelijke gegevenspatronen door uw schema&#39;s te abstract en opnieuw te gebruiken XDM, die het gemakkelijker maken om complexe gegevensstructuren te vertegenwoordigen.

Nadat u alle velden aan het gegevenstype hebt toegevoegd, selecteert u **[!UICONTROL Save]** om uw wijzigingen op te slaan en het gegevenstype aan de [!DNL Schema Library].

## Het gegevenstype toevoegen aan een schema {#add-data-type}

Nadat u een gegevenstype hebt gemaakt, kunt u het in uw schema&#39;s gebruiken. Aangezien XDM-schema&#39;s bestaan uit een klasse en nul of meer veldgroepen, kunnen velden die door een gegevenstype worden verschaft, niet rechtstreeks aan een schema worden toegevoegd. In plaats daarvan moeten ze worden opgenomen in een klasse of een veldgroep.

Begin door de stappen te volgen betrokken bij [een veld toevoegen aan een klasse](./classes.md#add-fields) of [een veld toevoegen aan een veldgroep](./field-groups.md#add-fields). U kunt ook beginnen [een veld rechtstreeks aan een schema toevoegen](./schemas.md#add-individual-fields) en kiest u de bovenliggende klasse of veldgroep. Wanneer u **[!UICONTROL Type]** voor het nieuwe veld selecteert u de naam van het gegevenstype in het vervolgkeuzemenu.

## Een object met meerdere velden omzetten in een gegevenstype {#convert}

Wanneer u een objecttypeveld maakt met meerdere subvelden in het dialoogvenster [!DNL Schema Editor]kunt u dat veld omzetten in een gegevenstype, zodat u dezelfde veldstructuur kunt gebruiken in een andere klasse of veldgroep.

Als u een objecttypeveld wilt omzetten in een gegevenstype, selecteert u het veld op het canvas. Voordat u het veld converteert, moet u ervoor zorgen dat **[!UICONTROL Display name]** bevat een beschrijving van de gegevens die het object bevat, aangezien dit de naam van het gegevenstype wordt. Als u klaar bent om het veld om te zetten, selecteert u **[!UICONTROL Convert to new data type]** in het rechterspoor.

![](../../images/ui/resources/data-types/convert-object.png)

Het canvas werkt het gegevenstype van het veld bij van &quot;[!UICONTROL Object]&quot; aan het nieuwe gegevenstype. Deze structuur kan nu opnieuw worden gebruikt in andere klassen en veldgroepen door dit gegevenstype te selecteren in het menu **[!UICONTROL Type]** vervolgkeuzelijst bij het definiëren van een nieuw veld.

![](../../images/ui/resources/data-types/converted.png)

## Volgende stappen {#next-steps}

In deze handleiding wordt beschreven hoe u gegevenstypen kunt maken en bewerken met behulp van de interface van het platform. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie de [[!UICONTROL Schemas] werkruimte - overzicht](../overview.md).

Leren hoe u gegevenstypen beheert met de opdracht [!DNL Schema Registry] API, zie [eindhulplijn gegevenstypen](../../api/data-types.md).
