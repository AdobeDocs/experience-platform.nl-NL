---
keywords: Experience Platform;thuis;populaire onderwerpen;ui;UI;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Gegevensmodel;Gegevensmodel;Onderzoek;klasse;veldgroep;gegevenstype;schema;
solution: Experience Platform
title: De Middelen van het Schema in UI onderzoeken
description: Leer hoe te om bestaande schema's, klassen, de groepen van het schemagebied, en gegevenstypes in het gebruikersinterface van de Experience Platform te onderzoeken.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 0%

---

# Schema-bronnen in de gebruikersinterface verkennen

In Adobe Experience Platform worden alle XDM-schemabronnen (Experience Data Model) opgeslagen in [!DNL Schema Library] , inclusief standaardbronnen die worden geleverd door Adobe en aangepaste bronnen die door uw organisatie zijn gedefinieerd. In de interface van het Experience Platform kunt u de structuur en de gebieden van om het even welk bestaand schema, klasse, gebiedsgroep, of gegevenstype in [!DNL Schema Library] bekijken. Dit is vooral nuttig wanneer het plannen van en het voorbereidingen treffen voor gegevensopname, aangezien UI informatie over de verwachte gegevenstypes en gebruiksgevallen van elk gebied verstrekt door deze middelen XDM verstrekt.

Deze zelfstudie behandelt de stappen voor het verkennen van bestaande schema&#39;s, klassen, gebiedsgroepen, en gegevenstypes in Experience Platform UI.

## Een schemabron opzoeken {#lookup}

Selecteer **[!UICONTROL Schemas]** in de gebruikersinterface van het platform in de linkernavigatie. De werkruimte van [!UICONTROL Schemas] biedt een tabblad **[!UICONTROL Browse]** waarin alle schema&#39;s in uw organisatie worden verkend, samen met extra specifieke tabbladen voor respectievelijk **[!UICONTROL Classes]** , **[!UICONTROL Field groups]** en **[!UICONTROL Data types]** .

![](../images/ui/explore/tabs.png)

Het filterpictogram (![ Beeld van het Pictogram van de Filter ](/help/images/icons/filter.png)) openbaart controles in het linkerspoor om onderaan vermelde resultaten te versmallen. De weergegeven besturingselementen verschillen afhankelijk van het type bron dat wordt vermeld.

Als u bijvoorbeeld de lijst wilt filteren om alleen standaardgegevenstypen weer te geven die door Adobe worden aangeboden, selecteert u respectievelijk **[!UICONTROL Datatype]** en **[!UICONTROL Adobe]** onder de secties **[!UICONTROL Type]** en **[!UICONTROL Owner]** .

De **[!UICONTROL Included in Profile]** knevel staat u toe om resultaten te filtreren om slechts middelen te tonen die in schema&#39;s worden gebruikt die voor gebruik in [ in real time het Profiel van de Klant ](../../profile/home.md) zijn toegelaten. Met de schakeloptie **[!UICONTROL Show adhoc schemas]** wordt de lijst met schema&#39;s gefilterd die zijn gemaakt met velden waarvan de naamruimte is ingesteld voor gebruik met slechts één gegevensset.

![ het [!UICONTROL Schemas] werkruimte [!UICONTROL Browse] lusje met het benadrukte filterenpaneel.](../images/ui/explore/filter.png)

Wanneer u bronnen op de tabbladen **[!UICONTROL Classes]** , **[!UICONTROL Field groups]** of **[!UICONTROL Data types]** weergeeft, kunt u **[!UICONTROL Adobe]** selecteren om alleen standaardbronnen weer te geven of **[!UICONTROL Customer]** om alleen bronnen weer te geven die door uw organisatie zijn gemaakt.

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

### Standaardklasse- en veldgroepindicator {#standard-class-and-field-group-indicator}

Binnen de Redacteur van het Schema, worden de standaard (Adobe-geproduceerde) klassen en de gebiedsgroepen vermeld met het hangslotpictogram (![ A hangslotpictogram.](/help/images/icons/lock-closed.png). Het hangslot verschijnt in de linkerspoorstaaf naast de klasse of de naam van de gebiedsgroep, evenals naast om het even welk gebied in het schemadiagram dat een deel van een systeem-geproduceerde middel is.

![ de Redacteur van het Schema met het gemarkeerde hangslotpictogram ](../images/ui/explore/schema-editor-padlock-icon.png)

Zie [ douanegebieden aan standaardgebiedsgroepen ](./resources/schemas.md) documentatie voor begeleiding toevoegen. U kunt een standaardklasse niet bewerken.

### Door het systeem gegenereerde velden {#system-fields}

Sommige veldnamen worden voorafgegaan door een onderstrepingsteken, zoals `_repo` en `_id` . Deze vertegenwoordigen placeholders voor gebieden die het systeem automatisch zal produceren en toewijzen aangezien de gegevens worden opgenomen.

Daarom moeten de meeste van deze velden worden uitgesloten van de structuur van uw gegevens wanneer u deze opneemt in Platform. De belangrijkste uitzondering op deze regel is het [`_{TENANT_ID}` gebied ](../api/getting-started.md#know-your-tenant_id), dat alle gebieden XDM die onder uw organisatie worden gecreeerd namespaced onder moeten zijn.

### Datatypen {#data-types}

Voor elk veld dat op het canvas wordt weergegeven, wordt het corresponderende gegevenstype naast de naam weergegeven en wordt in één oogopslag het type gegevens aangegeven dat het veld verwacht voor opname.

![](../images/ui/explore/data-types.png)

Om het even welk gegevenstype dat met vierkante haakjes (`[]`) wordt toegevoegd vertegenwoordigt een serie van dat bepaalde gegevenstype. Bijvoorbeeld, wijst een gegevenstype van **[!UICONTROL String]\ []** erop dat het gebied een serie van koordwaarden verwacht. Een gegevenstype van **[!UICONTROL Payment Item]\ []** wijst op een serie van voorwerpen die met het [!UICONTROL Payment Item] gegevenstype in overeenstemming zijn.

Als een arrayveld is gebaseerd op een objecttype, kunt u het pictogram ervan op het canvas selecteren om de verwachte kenmerken voor elk arrayitem weer te geven.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

Wanneer u de naam van een veld op het canvas selecteert, wordt de rechterrails bijgewerkt en worden details over dat veld onder **[!UICONTROL Field properties]** weergegeven. Dit kan een beschrijving bevatten van het bedoelde gebruiksgeval van het veld, standaardwaarden, patronen, indelingen, of het veld al dan niet is vereist, enzovoort.

![](../images/ui/explore/field-properties.png)

Als het veld dat u inspecteert een opsommingsveld is, geeft de rechterspoorstaaf ook de acceptabele waarden weer die het veld verwacht te ontvangen.

![](../images/ui/explore/enum-field.png)

### Identiteitsvelden {#identity}

Wanneer het inspecteren van schema&#39;s die identiteitsgebieden bevatten, zijn deze gebieden vermeld in het linkerspoor onder de klasse of de gebiedsgroep die hen aan het schema verstrekt. Selecteer de naam van het identiteitsveld in de linkerrail om het veld op het canvas weer te geven, ongeacht hoe diep het veld is genest.

De gebieden van de identiteit worden benadrukt in het canvas met een vingerafdrukpictogram (![ Beeld van het Pictogram van de Vingerprint ](/help/images/icons/identity-service.png)). Als u de naam van het identiteitsgebied selecteert, kunt u extra informatie zoals [ identiteitsnamespace ](../../identity-service/features/namespaces.md) bekijken en of het gebied al dan niet de primaire identiteit voor het schema is.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Zie de gids op [ bepalende identiteitsgebieden ](./fields/identity.md) voor meer informatie over identiteitsgebieden en hun verhouding met de stroomafwaartse diensten van het Platform.

### Relatievelden {#relationship}

Als u een schema inspecteert dat een relatieveld bevat, zal het gebied in de linkerspoorstaaf onder **[!UICONTROL Relationships]** worden vermeld. Selecteer de naam van het relatieveld in de linkerrail om het veld op het canvas weer te geven, ongeacht hoe diep het veld is genest.

Relatievelden worden ook op unieke wijze gemarkeerd op het canvas en tonen de naam van het referentieschema waarnaar het veld koppelt. Als u de naam van het relatieveld selecteert, kunt u de identiteitsnaamruimte van de primaire identiteit van het verwijzingsschema in het juiste spoor bekijken.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Zie het leerprogramma op [ creërend een verband in UI ](../tutorials/relationship-ui.md) voor meer informatie over het gebruik van verhoudingen in schema&#39;s XDM.

## Volgende stappen

In dit document wordt beschreven hoe u bestaande XDM-bronnen kunt verkennen in de gebruikersinterface van het Experience Platform. Zie het [[!UICONTROL Schemas] overzicht van de werkruimte ](./overview.md) voor meer informatie over de verschillende functies van de [!UICONTROL Schemas] -werkruimte en [!DNL Schema Editor] .
