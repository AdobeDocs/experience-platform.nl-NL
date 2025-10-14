---
keywords: Experience Platform;home;populaire onderwerpen;ui;UI;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;exploreren;klasse;field groep;gegevenstype;schema;
solution: Experience Platform
title: De Middelen van het Schema in UI onderzoeken
description: Leer hoe u bestaande schema's, klassen, schemaveldgroepen en gegevenstypen in de Experience Platform-gebruikersinterface kunt verkennen.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---

# Schema-bronnen in de gebruikersinterface verkennen

In Adobe Experience Platform worden alle XDM-schemabronnen (Experience Data Model) opgeslagen in de [!DNL Schema Library] , inclusief standaardbronnen die worden geleverd door Adobe en aangepaste bronnen die zijn gedefinieerd door uw organisatie. In Experience Platform UI, kunt u de structuur en de gebieden van om het even welk bestaand schema, klasse, gebiedsgroep, of gegevenstype in [!DNL Schema Library] bekijken. Dit is vooral nuttig wanneer het plannen van en het voorbereidingen treffen voor gegevensopname, aangezien UI informatie over de verwachte gegevenstypes en gebruiksgevallen van elk gebied verstrekt door deze middelen XDM verstrekt.

Deze zelfstudie behandelt de stappen voor het verkennen van bestaande schema&#39;s, klassen, veldgroepen en gegevenstypen in de gebruikersinterface van Experience Platform.

## Een schemabron opzoeken {#lookup}

Selecteer **[!UICONTROL Schemas]** in de gebruikersinterface van Experience Platform in de linkernavigatie. De werkruimte van [!UICONTROL Schemas] biedt een tabblad **[!UICONTROL Browse]** waarin alle schema&#39;s in uw organisatie worden verkend, samen met extra specifieke tabbladen voor respectievelijk **[!UICONTROL Classes]** , **[!UICONTROL Field groups]** , **[!UICONTROL Data types]** en **[!UICONTROL Relationships]** .

![&#x200B; de werkruimte van Schema&#39;s met verscheidene benadrukte lusjes.](../images/ui/explore/tabs.png)

Het filterpictogram (![&#x200B; Beeld van het Pictogram van de Filter &#x200B;](/help/images/icons/filter.png)) openbaart controles in het linkerspoor om onderaan vermelde resultaten te versmallen. Bronfilters zijn beschikbaar voor schema&#39;s en relaties op de tabbladen **[!UICONTROL Browse]** en **[!UICONTROL Relationships]** .

Op het tabblad [!UICONTROL Browse] van de [!UICONTROL Schemas] -werkruimte kunt u de schemavoorraad filteren. Gebruik **[!UICONTROL Included in Profile]** knevel om schema&#39;s slechts te tonen die voor gebruik in [&#x200B; Real-Time Profiel van de Klant &#x200B;](../../profile/home.md) zijn toegelaten. Met de schakeloptie **[!UICONTROL Show adhoc schemas]** kunt u de lijst met schema&#39;s filteren die zijn gemaakt met velden die zijn benoemd voor gebruik met slechts één gegevensset.

![&#x200B; het [!UICONTROL Schemas] werkruimte [!UICONTROL Browse] lusje met het benadrukte filterenpaneel.](../images/ui/explore/filters.png)

Op het tabblad [!UICONTROL Relationship] van de [!UICONTROL Schemas] -werkruimte kunt u de lijst met relaties filteren op basis van vier criteria. De filters omvatten [!UICONTROL Source schema] , [!UICONTROL Destination schema] , [!UICONTROL Source class] en [!UICONTROL Destination class] . De onderstaande tabel bevat een beschrijving van de filters.

| Filter | Beschrijving |
|-----------------------------------|------------|
| [!UICONTROL Source schema] | Selecteer een schema in het vervolgkeuzemenu [!UICONTROL Source schema] om alle relaties te zien waar het geselecteerde schema het beginpunt of de &quot;bron&quot; is. |
| [!UICONTROL Destination schema] | Selecteer een schema in het vervolgkeuzemenu [!UICONTROL Destination schema] om alle relaties weer te geven waarin het geselecteerde schema het doel of de bestemming is. |
| [!UICONTROL Source class] | Als u relaties wilt filteren op basis van de klasse van het initiërende schema, selecteert u een klasse in het vervolgkeuzemenu [!UICONTROL Source class] . |
| [!UICONTROL Destination class] | Als u relaties wilt weergeven die eindigen met schema&#39;s van een specifieke klasse, selecteert u een klasse in het vervolgkeuzemenu [!UICONTROL Destination class] . |

{style="table-layout:auto"}

![&#x200B; het lusje van Verhoudingen met de benadrukte filterssectie.](../images/ui/explore/relationships-filter.png)

U kunt de zoekbalk ook gebruiken om de resultaten verder omlaag te brengen.

![&#x200B; het Browse lusje van de werkruimte van Schema&#39;s met het benadrukte onderzoeksgebied.](../images/ui/explore/search.png)

De middelen die in onderzoeksresultaten worden getoond worden bevolen eerst door titelgelijken, dan door beschrijvingsgelijken. Hoe meer woorden in een van deze categorieën overeenkomen, hoe hoger de bron in de lijst.

Wanneer u de bron hebt gevonden die u wilt verkennen, selecteert u de naam in de lijst om de structuur ervan op het canvas weer te geven.

## Een XDM-resource verkennen in het canvas {#explore}

Wanneer u een bron hebt geselecteerd, wordt de structuur ervan geopend in het canvas.

![&#x200B; het Datatype werkruimtencanvas dat Commerce datatype toont.](../images/ui/explore/canvas.png)

Alle objecten-type gebieden die sub-eigenschappen bevatten worden doen ineenstorten door gebrek wanneer zij eerst in het canvas verschijnen. Als u de subeigenschappen van een veld wilt weergeven, selecteert u het pictogram naast de naam.

![&#x200B; het Datatype werkruimtekanvas met uitgebreide benadrukte gebieden en sub-eigenschappen.](../images/ui/explore/field-expand.png)

### Standaardklasse- en veldgroepindicator {#standard-class-and-field-group-indicator}

Binnen de Redacteur van het Schema, worden de standaard (Adobe-geproduceerde) klassen en de gebiedsgroepen vermeld met het hangslotpictogram (![&#x200B; A hangslotpictogram.](/help/images/icons/lock-closed.png). Het hangslot verschijnt in de linkerspoorstaaf naast de klasse of de naam van de gebiedsgroep, evenals naast om het even welk gebied in het schemadiagram dat een deel van een systeem-geproduceerde middel is.

![&#x200B; de Redacteur van het Schema met het gemarkeerde hangslotpictogram &#x200B;](../images/ui/explore/schema-editor-padlock-icon.png)

Zie [&#x200B; douanegebieden aan standaardgebiedsgroepen &#x200B;](./resources/schemas.md) documentatie voor begeleiding toevoegen. U kunt een standaardklasse niet bewerken.

### Door het systeem gegenereerde velden {#system-fields}

Sommige veldnamen worden voorafgegaan door een onderstrepingsteken, zoals `_repo` en `_id` . Deze vertegenwoordigen placeholders voor gebieden die het systeem automatisch zal produceren en toewijzen aangezien de gegevens worden opgenomen.

Daarom moeten de meeste van deze velden van de gegevensstructuur worden uitgesloten wanneer u ze in Experience Platform plaatst. De belangrijkste uitzondering op deze regel is het [`_{TENANT_ID}` gebied &#x200B;](../api/getting-started.md#know-your-tenant_id), dat alle gebieden XDM die onder uw organisatie worden gecreeerd namespaced onder moeten zijn.

### Datatypen {#data-types}

Voor elk veld dat op het canvas wordt weergegeven, wordt het corresponderende gegevenstype naast de naam weergegeven en wordt in één oogopslag het type gegevens aangegeven dat het veld verwacht voor opname.

![&#x200B; Datatype van het Adres van de Post dat op het canvas met zijn bijbehorende benadrukte gegevenstypes wordt getoond.](../images/ui/explore/data-types.png)

Om het even welk gegevenstype dat met vierkante haakjes (`[]`) wordt toegevoegd vertegenwoordigt een serie van dat bepaalde gegevenstype. Bijvoorbeeld, wijst een gegevenstype van **[!UICONTROL String]\ []** erop dat het gebied een serie van koordwaarden verwacht. Een gegevenstype van **[!UICONTROL Payment Item]\ []** wijst op een serie van voorwerpen die met het [!UICONTROL Payment Item] gegevenstype in overeenstemming zijn.

Als een arrayveld is gebaseerd op een objecttype, kunt u het pictogram ervan op het canvas selecteren om de verwachte kenmerken voor elk arrayitem weer te geven.

![&#x200B; een voorwerp op het canvas met een benadrukt seriegebied en de verwachte attributen voor elk getoonde seriepunt.](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

Wanneer u de naam van een veld op het canvas selecteert, wordt de rechterrails bijgewerkt en worden details over dat veld onder **[!UICONTROL Field properties]** weergegeven. Dit kan een beschrijving bevatten van het bedoelde gebruiksgeval van het veld, standaardwaarden, patronen, indelingen, of het veld al dan niet is vereist, enzovoort.

![&#x200B; gebied van A dat van het gegevenstype van Commerce met de benadrukte gebiedseigenschappen wordt geselecteerd.](../images/ui/explore/field-properties.png)

Als het veld dat u inspecteert een opsommingsveld is, geeft de rechterspoorstaaf ook de acceptabele waarden weer die het veld verwacht te ontvangen.

![&#x200B; de Redacteur van het Schema met een gebied selecteerde en enum waarden en vertoningsnamen die op de spoorstaaf van gebiedseigenschappen worden benadrukt.](../images/ui/explore/enum-field.png)

### Identiteitsvelden {#identity}

Wanneer het inspecteren van schema&#39;s die identiteitsgebieden bevatten, zijn deze gebieden vermeld in het linkerspoor onder de klasse of de gebiedsgroep die hen aan het schema verstrekt. Selecteer de naam van het identiteitsveld in de linkerrail om het veld op het canvas weer te geven, ongeacht hoe diep het veld is genest.

De gebieden van de identiteit worden benadrukt in het canvas met een vingerafdrukpictogram (![&#x200B; Beeld van het Pictogram van de Vingerprint &#x200B;](/help/images/icons/identity-service.png)). Als u de naam van het identiteitsgebied selecteert, kunt u extra informatie zoals [&#x200B; identiteitsnamespace &#x200B;](../../identity-service/features/namespaces.md) bekijken en of het gebied al dan niet de primaire identiteit voor het schema is.

![&#x200B; de Redacteur van het Schema met de identiteit van het schema die in het linkerspoor wordt benadrukt, het gebied in het schemadiagram wordt benadrukt, en de identiteit namespace die op de gebiedseigenschappen wordt benadrukt.](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Zie de gids op [&#x200B; bepalend identiteitsgebieden &#x200B;](./fields/identity.md) voor meer informatie over identiteitsgebieden en hun verhouding met de stroomafwaartse diensten van Experience Platform.

### Relatievelden {#relationship}

Als u een schema inspecteert dat een relatieveld bevat, zal het gebied in de linkerspoorstaaf onder **[!UICONTROL Relationships]** worden vermeld. Selecteer de naam van het relatieveld in de linkerrail om het veld op het canvas weer te geven, ongeacht hoe diep het veld is genest. Relatievelden worden ook op unieke wijze gemarkeerd op het canvas en tonen de naam van het referentieschema waarnaar het veld koppelt. Voor organisaties met B2B-mogelijkheden kunnen aangepaste relatienamen worden geschreven en in deze gevallen worden weergegeven op het canvas.

![&#x200B; de Redacteur van het Schema met het relatiegebied en geeft benadrukte verhouding uit.](../images/ui/explore/relationship-field.png)

Als u de naamruimte voor identiteit van de primaire identiteit van het referentieschema wilt weergeven, selecteert u het relatieveld en vervolgens **[!UICONTROL Edit relationship]** in de zijbalk van [!UICONTROL Field properties] . De parameters voor de relatie worden weergegeven in het dialoogvenster [!UICONTROL Edit relationship] dat wordt weergegeven.

![&#x200B; de Edit relatiedialoog met de getoonde relatieparameters.](../images/ui/explore/edit-relationship-dialog.png)

Zie het leerprogramma op [&#x200B; creërend een verband in UI &#x200B;](../tutorials/relationship-ui.md) voor meer informatie over het gebruik van verhoudingen in schema&#39;s XDM.

## Volgende stappen

In dit document wordt beschreven hoe u bestaande XDM-bronnen in de gebruikersinterface van Experience Platform kunt verkennen. Zie het [[!UICONTROL Schemas] overzicht van de werkruimte &#x200B;](./overview.md) voor meer informatie over de verschillende functies van de [!UICONTROL Schemas] -werkruimte en [!DNL Schema Editor] .
