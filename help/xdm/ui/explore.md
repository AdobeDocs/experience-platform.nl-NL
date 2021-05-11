---
keywords: Experience Platform;thuis;populaire onderwerpen;ui;UI;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Gegevensmodel;Gegevensmodel;Onderzoek;klasse;veldgroep;gegevenstype;schema;
solution: Experience Platform
title: XDM-bronnen verkennen in de gebruikersinterface
description: Leer hoe te om bestaande schema's, klassen, de groepen van het schemagebied, en gegevenstypes in het gebruikersinterface van de Experience Platform te onderzoeken.
topic-legacy: tutorial
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
translation-type: tm+mt
source-git-commit: ddf66ab277e5882afe7ffbdd87ee5df958c3e7b0
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# XDM-bronnen verkennen in de gebruikersinterface

In Adobe Experience Platform worden alle XDM-bronnen (Experience Data Model) opgeslagen in de [!DNL Schema Library], inclusief standaardbronnen die worden geleverd door Adobe en aangepaste bronnen die zijn gedefinieerd door uw organisatie. In het Experience Platform UI, kunt u de structuur en de gebieden van om het even welk bestaand schema, klasse, de groep van het schemagebied, of gegevenstype in [!DNL Schema Library] bekijken. Dit is vooral nuttig wanneer het plannen van en het voorbereidingen treffen voor gegevensopname, aangezien UI informatie over de verwachte gegevenstypes en gebruiksgevallen van elk gebied verstrekt door deze middelen XDM verstrekt.

Deze zelfstudie behandelt de stappen voor het verkennen van bestaande schema&#39;s, klassen, gebiedsgroepen, en gegevenstypes in Experience Platform UI.

## Een XDM-resource {#lookup} opzoeken

Selecteer **[!UICONTROL Schemas]** in de linkernavigatie in de interface van het Platform. De [!UICONTROL Schemas] werkruimte verstrekt een **[!UICONTROL Browse]** lusje om alle bestaande middelen XDM in uw organisatie, samen met extra specifieke lusjes voor het onderzoeken **[!UICONTROL Classes]**, **[!UICONTROL Field groups]**, en **[!UICONTROL Data types]** specifiek te onderzoeken.

![](../images/ui/explore/tabs.png)

Op het [!UICONTROL Browse] lusje, kunt u het filterpictogram (![de Beeld van het Pictogram van het Filter ](../images/ui/explore/icon.png)) gebruiken om controles in het linkerspoor zichtbaar te maken om onderaan vermelde resultaten te beperken.

Als u bijvoorbeeld de lijst wilt filteren zodat alleen standaardgegevenstypen worden weergegeven die door Adobe worden geleverd, selecteert u **[!UICONTROL Datatype]** en **[!UICONTROL Adobe]** onder respectievelijk de secties **[!UICONTROL Type]** en **[!UICONTROL Owner]**.

Met de schakeloptie **[!UICONTROL Included in Profile]** kunt u resultaten filteren om alleen bronnen weer te geven die worden gebruikt in schema&#39;s die zijn ingeschakeld voor gebruik in [Real-time klantprofiel](../../profile/home.md).

![](../images/ui/explore/filter.png)

U kunt de zoekbalk ook gebruiken om de resultaten verder omlaag te brengen. Wanneer u naar een termijn zoekt, vertegenwoordigen de hoogste punten middelen de waarvan namen de onderzoeksvraag aanpassen. Onder deze punten, onder **[!UICONTROL Standard Fields]**, zullen om het even welke middelen die gebieden bevatten die de vraag aanpassen worden vermeld. Dit staat u toe om naar middelen te zoeken XDM die op het type van gegevens worden gebaseerd zij bevatten, zonder het moeten de naam van het middel vooraf kennen.

![](../images/ui/explore/search.png)

De middelen die in onderzoeksresultaten worden getoond worden bevolen eerst door titelgelijken, dan door beschrijvingsgelijken. Hoe meer woorden in een van deze categorieën overeenkomen, hoe hoger de bron in de lijst.

>[!NOTE]
>
>Voor standaard XDM-bronnen retourneert de zoekfunctie alleen afzonderlijke velden die een naamruimte `xdm` bevatten. Velden die zich onder een andere naamruimte bevinden (zoals uw huurder-id), worden alleen geretourneerd als ze zich in een aangepaste bron bevinden.

Wanneer u de bron hebt gevonden die u wilt verkennen, selecteert u de naam in de lijst om de structuur ervan op het canvas weer te geven.

## Een XDM-bron zoeken op het canvas {#explore}

Wanneer u een bron hebt geselecteerd, wordt de structuur ervan geopend in het canvas.

![](../images/ui/explore/canvas.png)

Alle objecten-type gebieden die sub-eigenschappen bevatten worden doen ineenstorten door gebrek wanneer zij eerst in het canvas verschijnen. Als u de subeigenschappen van een veld wilt weergeven, selecteert u het pictogram naast de naam.

![](../images/ui/explore/field-expand.png)

### Door het systeem gegenereerde velden {#system-fields}

Sommige veldnamen worden voorafgegaan door een onderstrepingsteken, zoals `_repo` en `_id`. Deze vertegenwoordigen placeholders voor gebieden die het systeem automatisch zal produceren en toewijzen aangezien de gegevens worden opgenomen.

Daarom moeten de meeste van deze velden van de gegevensstructuur worden uitgesloten wanneer u gegevens in het Platform opneemt. De belangrijkste uitzondering op deze regel is het [`_{TENANT_ID}` gebied](../api/getting-started.md#know-your-tenant_id), dat alle gebieden XDM die onder uw organisatie worden gecreeerd namespaced onder moeten zijn.

### Datatypen {#data-types}

Voor elk veld dat op het canvas wordt weergegeven, wordt het corresponderende gegevenstype naast de naam weergegeven en wordt in één oogopslag het type gegevens aangegeven dat het veld verwacht voor opname.

![](../images/ui/explore/data-types.png)

Om het even welk gegevenstype dat met vierkante haakjes (`[]`) wordt toegevoegd vertegenwoordigt een serie van dat bepaalde gegevenstype. Een gegevenstype van **[!UICONTROL String]\[]** geeft bijvoorbeeld aan dat het veld een array van tekenreekswaarden verwacht. Een gegevenstype van **[!UICONTROL Payment Item]\[]** geeft een array van objecten aan die voldoen aan het gegevenstype [!UICONTROL Payment Item].

Als een arrayveld is gebaseerd op een objecttype, kunt u het pictogram ervan op het canvas selecteren om de verwachte kenmerken voor elk arrayitem weer te geven.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Field properties] {#field-properties}

Wanneer u de naam van een veld op het canvas selecteert, wordt de rechterrails bijgewerkt om details over dat veld onder **[!UICONTROL Field properties]** weer te geven. Dit kan een beschrijving bevatten van het bedoelde gebruiksgeval van het veld, standaardwaarden, patronen, indelingen, of het veld al dan niet is vereist, enzovoort.

![](../images/ui/explore/field-properties.png)

Als het veld dat u inspecteert een opsommingsveld is, geeft de rechterspoorstaaf ook de acceptabele waarden weer die het veld verwacht te ontvangen.

![](../images/ui/explore/enum-field.png)

### Identiteitsvelden {#identity}

Wanneer het inspecteren van schema&#39;s die identiteitsgebieden bevatten, zijn deze gebieden vermeld in het linkerspoor onder de klasse of de gebiedsgroep die hen aan het schema verstrekt. Selecteer de naam van het identiteitsveld in de linkerrail om het veld op het canvas weer te geven, ongeacht hoe diep het veld is genest.

Identiteitsvelden worden op het canvas gemarkeerd met een vingerafdrukpictogram (![Vingerafdrukpictogram Afbeelding](../images/ui/explore/identity-symbol.png)). Als u de naam van het identiteitsgebied selecteert, kunt u extra informatie zoals [identity namespace](../../identity-service/namespaces.md) bekijken en of het gebied de primaire identiteit voor het schema is of niet.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Zie de handleiding bij [het definiëren van identiteitsvelden](./fields/identity.md) voor meer informatie over identiteitsvelden en hun relatie met services voor downstreamPlatforms.

### Relatievelden {#relationship}

Als u een schema inspecteert dat een relatieveld bevat, zal het gebied in de linkerspoorstaaf onder **[!UICONTROL Relationships]** worden vermeld. Selecteer de naam van het relatieveld in de linkerrail om het veld op het canvas weer te geven, ongeacht hoe diep het veld is genest.

De gebieden van de verhouding worden ook uniek benadrukt in het canvas, die de naam van het bestemmingsschema tonen dat de gebiedsverwijzingen. Als u de naam van het relatieveld selecteert, kunt u de identiteitsnaamruimte van de primaire identiteit van het bestemmingsschema in het juiste spoor bekijken.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Zie het leerprogramma op [het creëren van een verhouding in UI](../tutorials/relationship-ui.md) voor meer informatie over het gebruik van verhoudingen in schema&#39;s XDM.

## Volgende stappen

In dit document wordt beschreven hoe u bestaande XDM-bronnen kunt verkennen in de gebruikersinterface van het Experience Platform. Voor meer informatie over de verschillende eigenschappen van de [!UICONTROL Schemas] werkruimte en [!DNL Schema Editor], zie [[!UICONTROL Schemas] werkruimteoverzicht](./overview.md).
