---
keywords: Experience Platform;thuis;populaire onderwerpen;ui;UI;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Gegevensmodel;Gegevensmodel;Onderzoek;klasse;veldgroep;gegevenstype;schema;
solution: Experience Platform
title: De Middelen van het Schema in UI onderzoeken
description: Leer hoe te om bestaande schema's, klassen, de groepen van het schemagebied, en gegevenstypes in het gebruikersinterface van de Experience Platform te onderzoeken.
topic-legacy: tutorial
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 744d87c82b7e7e06782c6c1b9db2ec46a5444d28
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Schema-bronnen in de gebruikersinterface verkennen

In Adobe Experience Platform worden alle XDM-schemabronnen (Experience Data Model) opgeslagen in het [!DNL Schema Library], inclusief standaardbronnen die worden geleverd door Adobe en aangepaste bronnen die zijn gedefinieerd door uw organisatie. In de interface van het Experience Platform kunt u de structuur en de gebieden van om het even welk bestaand schema, klasse, gebiedsgroep, of gegevenstype in bekijken [!DNL Schema Library]. Dit is vooral nuttig wanneer het plannen van en het voorbereidingen treffen voor gegevensopname, aangezien UI informatie over de verwachte gegevenstypes en gebruiksgevallen van elk gebied verstrekt door deze middelen XDM verstrekt.

Deze zelfstudie behandelt de stappen voor het verkennen van bestaande schema&#39;s, klassen, gebiedsgroepen, en gegevenstypes in Experience Platform UI.

## Een schemabron opzoeken {#lookup}

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Schemas]** in de linkernavigatie. De [!UICONTROL Schemas] werkruimte biedt een **[!UICONTROL Browse]** tabblad om alle schema&#39;s in uw organisatie te verkennen, samen met extra speciale tabbladen voor het verkennen van **[!UICONTROL Classes]**, **[!UICONTROL Field groups]**, en **[!UICONTROL Data types]** respectievelijk.

![](../images/ui/explore/tabs.png)

Het filterpictogram (![Pictogramafbeelding filteren](../images/ui/explore/icon.png)) onthult controles in de linkerspoorstaaf om de vermelde resultaten te beperken. De weergegeven besturingselementen verschillen afhankelijk van het type bron dat wordt vermeld.

Als u bijvoorbeeld de lijst wilt filteren zodat alleen standaardgegevenstypen worden weergegeven die door Adobe worden geleverd, selecteert u **[!UICONTROL Datatype]** en **[!UICONTROL Adobe]** onder de **[!UICONTROL Type]** en **[!UICONTROL Owner]** secties.

De **[!UICONTROL Included in Profile]** knevel staat u toe om resultaten te filtreren om slechts middelen te tonen die in schema&#39;s worden gebruikt die voor gebruik binnen zijn toegelaten [Klantprofiel in realtime](../../profile/home.md).

![](../images/ui/explore/filter.png)

Wanneer u bronnen op de **[!UICONTROL Classes]**, **[!UICONTROL Field groups]**, of **[!UICONTROL Data types]** tabs, kunt u selecteren **[!UICONTROL Adobe]** alleen standaardbronnen tonen of **[!UICONTROL Customer]** om alleen bronnen weer te geven die door uw organisatie zijn gemaakt.

![](../images/ui/explore/filter-data-type.png)

U kunt de zoekbalk ook gebruiken om de resultaten verder omlaag te brengen.

![](../images/ui/explore/search.png)

De middelen die in onderzoeksresultaten worden getoond worden bevolen eerst door titelgelijken, dan door beschrijvingsgelijken. Hoe meer woorden in een van deze categorieën overeenkomen, hoe hoger de bron in de lijst.

Wanneer u de bron hebt gevonden die u wilt verkennen, selecteert u de naam in de lijst om de structuur ervan op het canvas weer te geven.

## Een XDM-resource verkennen in het canvas {#explore}

Wanneer u een bron hebt geselecteerd, wordt de structuur ervan geopend in het canvas.

![](../images/ui/explore/canvas.png)

Alle objecten-type gebieden die sub-eigenschappen bevatten worden doen ineenstorten door gebrek wanneer zij eerst in het canvas verschijnen. Als u de subeigenschappen van een veld wilt weergeven, selecteert u het pictogram naast de naam.

![](../images/ui/explore/field-expand.png)

### Door het systeem gegenereerde velden {#system-fields}

Sommige veldnamen worden voorafgegaan door een onderstrepingsteken, zoals `_repo` en `_id`. Deze vertegenwoordigen placeholders voor gebieden die het systeem automatisch zal produceren en toewijzen aangezien de gegevens worden opgenomen.

Daarom moeten de meeste van deze velden van de gegevensstructuur worden uitgesloten wanneer u gegevens in het Platform opneemt. De belangrijkste uitzondering op deze regel is de [`_{TENANT_ID}` field](../api/getting-started.md#know-your-tenant_id), waarin alle XDM-velden die onder uw organisatie worden gemaakt naamruimte moeten krijgen.

### Datatypen {#data-types}

Voor elk veld dat op het canvas wordt weergegeven, wordt het corresponderende gegevenstype naast de naam weergegeven en wordt in één oogopslag het type gegevens aangegeven dat het veld verwacht voor opname.

![](../images/ui/explore/data-types.png)

Elk gegevenstype dat wordt toegevoegd met vierkante haakjes (`[]`) vertegenwoordigt een array van dat specifieke gegevenstype. Bijvoorbeeld een gegevenstype van **[!UICONTROL String]\[]** Hiermee wordt aangegeven dat het veld een array van tekenreekswaarden verwacht. Een gegevenstype van **[!UICONTROL Payment Item]\[]** Hiermee wordt een array van objecten aangegeven die voldoen aan de [!UICONTROL Payment Item] gegevenstype.

Als een arrayveld is gebaseerd op een objecttype, kunt u het pictogram ervan op het canvas selecteren om de verwachte kenmerken voor elk arrayitem weer te geven.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

Wanneer u de naam van een veld op het canvas selecteert, wordt het rechterspoor bijgewerkt en worden de details van dat veld onder **[!UICONTROL Field properties]**. Dit kan een beschrijving bevatten van het bedoelde gebruiksgeval van het veld, standaardwaarden, patronen, indelingen, of het veld al dan niet is vereist, enzovoort.

![](../images/ui/explore/field-properties.png)

Als het veld dat u inspecteert een opsommingsveld is, geeft de rechterspoorstaaf ook de acceptabele waarden weer die het veld verwacht te ontvangen.

![](../images/ui/explore/enum-field.png)

### Identiteitsvelden {#identity}

Wanneer het inspecteren van schema&#39;s die identiteitsgebieden bevatten, zijn deze gebieden vermeld in het linkerspoor onder de klasse of de gebiedsgroep die hen aan het schema verstrekt. Selecteer de naam van het identiteitsveld in de linkerrail om het veld op het canvas weer te geven, ongeacht hoe diep het veld is genest.

Identiteitsvelden worden op het canvas gemarkeerd met een vingerafdrukpictogram (![Pictogramafbeelding voor vingerafdruk](../images/ui/explore/identity-symbol.png)). Als u de naam van het identiteitsveld selecteert, kunt u aanvullende informatie weergeven, zoals de [naamruimte identity](../../identity-service/namespaces.md) en of het veld de primaire identiteit voor het schema is.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Zie de handleiding op [identiteitsvelden definiëren](./fields/identity.md) voor meer informatie over identiteitsgebieden en hun relatie met downstreamdiensten van Platforms.

### Relatievelden {#relationship}

Als u een schema inspecteert dat een relatieveld bevat, zal het gebied in de linkerspoorstaaf onder worden vermeld **[!UICONTROL Relationships]**. Selecteer de naam van het relatieveld in de linkerrail om het veld op het canvas weer te geven, ongeacht hoe diep het veld is genest.

De gebieden van de verhouding worden ook uniek benadrukt in het canvas, die de naam van het bestemmingsschema tonen dat de gebiedsverwijzingen. Als u de naam van het relatieveld selecteert, kunt u de identiteitsnaamruimte van de primaire identiteit van het bestemmingsschema in het juiste spoor bekijken.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Zie de zelfstudie aan [het creëren van een verhouding in UI](../tutorials/relationship-ui.md) voor meer informatie over het gebruik van verhoudingen in schema&#39;s XDM.

## Volgende stappen

In dit document wordt beschreven hoe u bestaande XDM-bronnen kunt verkennen in de gebruikersinterface van het Experience Platform. Voor meer informatie over de verschillende eigenschappen van [!UICONTROL Schemas] werkruimte en [!DNL Schema Editor], zie de [[!UICONTROL Schemas] werkruimte - overzicht](./overview.md).
