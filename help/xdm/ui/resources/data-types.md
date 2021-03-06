---
keywords: Experience Platform;thuis;populaire onderwerpen;ui;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Gegevensmodel;Gegevensmodel;Gegevensmodel;Schemaregister;Schema;Schema;schema's;Schema's;Schema's;creëren;gegevenstype;gegevenstypen;
solution: Experience Platform
title: Gegevenstypen maken en bewerken met de gebruikersinterface
topic-legacy: tutorial
type: Tutorial
description: Leer hoe u gegevenstypen maakt en bewerkt in de gebruikersinterface van het Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 14128b247b003a54cb0d91167bb46fccf16ed799
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 0%

---

# Gegevenstypen maken en bewerken met de gebruikersinterface

In het Model van Gegevens van de Ervaring (XDM), zijn de gegevenstypes herbruikbare gebieden die veelvoudige subfields bevatten. Terwijl gelijkaardig aan de groepen van het schemagebied in zoverre zij voor het verenigbare gebruik van een multi-gebiedstructuur toestaan, zijn de gegevenstypes flexibeler omdat zij overal in de schemastructuur kunnen worden omvat terwijl de gebiedsgroepen slechts op het wortelniveau kunnen worden toegevoegd.

Adobe Experience Platform biedt vele standaardgegevenstypen die kunnen worden gebruikt voor een groot aantal gangbare praktijkbeheertoepassingen. U kunt echter ook uw eigen aangepaste gegevenstypen definiëren om aan uw unieke bedrijfsbehoeften te voldoen.

Deze zelfstudie behandelt de stappen voor het maken en bewerken van aangepaste gegevenstypen in de gebruikersinterface van het Platform.

## Vereisten

Deze handleiding vereist een goed begrip van XDM System. Verwijs naar [XDM overzicht](../../home.md) voor een inleiding aan de rol van XDM binnen het ecosysteem van het Experience Platform, en [grondbeginselen van schemacompositie](../../schema/composition.md) voor hoe de gegevenstypes tot XDM schema&#39;s bijdragen.

Hoewel niet vereist voor deze gids, wordt het geadviseerd dat u het leerprogramma ook [het samenstellen van een schema in UI](../../tutorials/create-schema-ui.md) volgt om zich met de diverse mogelijkheden van [!DNL Schema Editor] vertrouwd te maken.

## [!DNL Schema Editor] openen voor een gegevenstype

Selecteer **[!UICONTROL Schemas]** in de linkernavigatie in de interface van het Platform om de werkruimte [!UICONTROL Schemas] te openen en selecteer vervolgens het tabblad **[!UICONTROL Data types]**. Een lijst van beschikbare gegevenstypes wordt getoond, met inbegrip van die door Adobe en die door uw organisatie worden bepaald.

![](../../images/ui/resources/data-types/data-types-tab.png)

Hier hebt u twee opties:

- [Een nieuw gegevenstype maken](#create)
- [Een bestaand gegevenstype selecteren om te bewerken](#edit)

### Een nieuw gegevenstype maken {#create}

Selecteer **[!UICONTROL Create data type]** op het tabblad **[!UICONTROL Data types]**.

![](../../images/ui/resources/data-types/create.png)

De [!DNL Schema Editor] verschijnt, die de huidige structuur van het nieuwe gegevenstype in het canvas tonen. Aan de rechterkant van de editor kunt u een weergavenaam en een optionele beschrijving voor het gegevenstype opgeven. Zorg ervoor dat u een unieke en beknopte naam voor uw gegevenstype opgeeft, omdat dit zo is dat het wordt geïdentificeerd wanneer u het aan een schema toevoegt.

Deze zelfstudie maakt een gegevenstype dat een restauratie-eigenschap beschrijft, zodat het gegevenstype de weergavenaam &quot;Restaurant&quot; krijgt.

![](../../images/ui/resources/data-types/data-type-properties.png)

Van hier, kunt u vooruit naar [volgende sectie ](#add-fields) overslaan om gebieden aan het nieuwe gegevenstype toe te voegen.

### Een bestaand gegevenstype bewerken

>[!NOTE]
>
>Zodra een bestaand gegevenstype in een schema wordt gebruikt dat voor gebruik in het Profiel van de Klant in real time is toegelaten, slechts kunnen niet-destructieve veranderingen daarna in dat gegevenstype worden aangebracht. Zie [regels van schemaevolutie](../../schema/composition.md#evolution) voor meer informatie.

Alleen aangepaste gegevenstypen die door uw organisatie zijn gedefinieerd, kunnen worden bewerkt. Als u de weergegeven lijst wilt verkleinen, selecteert u het filterpictogram (![Filter Pictogram](../../images/ui/resources/data-types/filter.png)) om besturingselementen voor filtering weer te geven op basis van [!UICONTROL Owner]. Selecteer **[!UICONTROL Customer]** om alleen aangepaste gegevenstypen weer te geven die eigendom zijn van uw organisatie.

Selecteer in de lijst het gegevenstype dat u wilt bewerken om de rechtertrack te openen, met daarin de details van het gegevenstype. Selecteer de naam van het gegevenstype in de rechterrail om de structuur ervan te openen in [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Velden toevoegen aan het gegevenstype {#add-fields}

Als u velden wilt toevoegen aan het gegevenstype, selecteert u het pictogram **plus (+)** naast het veld op hoofdniveau op het canvas. Hieronder wordt een nieuw veld weergegeven en de rechtertrack wordt bijgewerkt met besturingselementen voor het nieuwe veld.

![](../../images/ui/resources/data-types/new-field.png)

Gebruik de besturingselementen in het rechterspoor om de details van het nieuwe veld te configureren. Zie de gids op [het bepalen van gebieden in UI](../fields/overview.md#define) voor specifieke stappen op om het gebied aan het gegevenstype te vormen en toe te voegen.

Het gegevenstype Restaurant vereist een tekenreeksveld voor de naam van het restaurant. Als zodanig wordt [!UICONTROL Field name] ingesteld als &quot;name&quot; en [!UICONTROL Type] als &quot;[!UICONTROL String]&quot;. Selecteer **[!UICONTROL Apply]** om de wijzigingen op het veld toe te passen.

![](../../images/ui/resources/data-types/name-field.png)

Voeg desgewenst meer velden aan het gegevenstype toe. Het gegevenstype Restaurant heeft nu extra velden voor merk, zitcapaciteit en vloerruimte.

![](../../images/ui/resources/data-types/more-fields.png)

Naast basisvelden kunt u ook andere gegevenstypen nesten binnen het aangepaste gegevenstype. Het gegevenstype Restaurant vereist bijvoorbeeld een veld dat het fysieke adres van de eigenschap vertegenwoordigt. In dit scenario, kunt u een nieuw &quot;adres&quot;gebied toevoegen dat het standaardgegevenstype &quot;[!UICONTROL Postal address]&quot;wordt toegewezen.

![](../../images/ui/resources/data-types/address-field.png)

Dit toont aan hoe de flexibele gegevenstypes in termen van het beschrijven van uw gegevens kunnen zijn: gegevenstypen kunnen velden gebruiken die ook gegevenstypen zijn, die zelf verdere gegevenstypen kunnen bevatten, enzovoort. Dit staat u toe om gemeenschappelijke gegevenspatronen door uw schema&#39;s te abstract en opnieuw te gebruiken XDM, die het gemakkelijker maken om complexe gegevensstructuren te vertegenwoordigen.

Als u klaar bent met het toevoegen van velden aan het gegevenstype, selecteert u **[!UICONTROL Save]** om uw wijzigingen op te slaan en het gegevenstype toe te voegen aan [!DNL Schema Library].

## Het gegevenstype toevoegen aan een klasse of veldgroep

Nadat u een gegevenstype hebt gemaakt, kunt u het in uw schema&#39;s gebruiken. Aangezien XDM-schema&#39;s bestaan uit een klasse en nul of meer veldgroepen, kunnen velden die door een gegevenstype worden verschaft, niet rechtstreeks aan een schema worden toegevoegd. In plaats daarvan moeten ze worden opgenomen in een klasse of een veldgroep.

Begin door de stappen te volgen betrokken met [toevoegend een gebied aan een klasse ](./classes.md#add-fields) of [toevoegend een gebied aan een gebiedsgroep](./field-groups.md#add-fields). Wanneer u **[!UICONTROL Type]** voor het nieuwe gebied kiest, selecteer de naam van uw gegevenstype van dropdown menu.

## Een object met meerdere velden omzetten in een gegevenstype {#convert}

Wanneer u een object-type gebied met veelvoudige subgebieden in [!DNL Schema Editor] creeert, kunt u dat gebied in een gegevenstype omzetten zodat kunt u die zelfde gebiedsstructuur in een verschillende klasse of een gebiedsgroep gebruiken.

Als u een objecttypeveld wilt omzetten in een gegevenstype, selecteert u het veld op het canvas. Voordat u het veld converteert, moet u ervoor zorgen dat **[!UICONTROL Display name]** een beschrijving bevat van de gegevens die het object bevat, aangezien dit de naam van het gegevenstype wordt. Wanneer u klaar bent om het veld om te zetten, selecteert u **[!UICONTROL Convert to new data type]** in de rechterrails.

![](../../images/ui/resources/data-types/convert-object.png)

Het canvas werkt het gegevenstype van het veld bij van &quot;[!UICONTROL Object]&quot; naar het nieuwe gegevenstype. De subvelden bevatten ook kleine vergrendelingspictogrammen naast de subvelden. Dit betekent dat het niet langer om afzonderlijke velden gaat, maar om een gebied dat deel uitmaakt van een gegevenstype met meerdere velden. Deze structuur kan nu opnieuw worden gebruikt in andere klassen en veldgroepen door dit gegevenstype te selecteren in het vervolgkeuzemenu **[!UICONTROL Type]** wanneer u een nieuw veld definieert.

![](../../images/ui/resources/data-types/converted.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u gegevenstypen kunt maken en bewerken met de gebruikersinterface van het Platform. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie [[!UICONTROL Schemas] werkruimteoverzicht](../overview.md).

Meer informatie over het beheren van gegevenstypen met de [!DNL Schema Registry]-API vindt u in de [gids voor gegevenstypen](../../api/data-types.md).
