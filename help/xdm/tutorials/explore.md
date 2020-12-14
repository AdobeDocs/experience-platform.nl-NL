---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: XDM-bronnen verkennen in de gebruikersinterface
description: Deze zelfstudie behandelt de stappen voor het verkennen van bestaande schema's, klassen, mixins, en gegevenstypes in Experience Platform UI.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 49d37cdf14bd03b62fe64116842bacd0f806e5ce
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# XDM-bronnen verkennen in de gebruikersinterface

In Adobe Experience Platform, worden alle middelen van het Gegevensmodel van de Ervaring (XDM) opgeslagen in [!DNL Schema Library], met inbegrip van standaardmiddelen die door Adobe en douanemiddelen worden verstrekt die door uw organisatie worden bepaald. In de interface van het Experience Platform kunt u de structuur en de gebieden van om het even welk bestaand schema, klasse, mengsel, of gegevenstype in bekijken [!DNL Schema Library]. Dit is vooral nuttig wanneer het plannen van en het voorbereidingen treffen voor gegevensopname, aangezien UI informatie over de verwachte gegevenstypes en gebruiksgevallen van elk gebied verstrekt door deze middelen XDM verstrekt.

Deze zelfstudie behandelt de stappen voor het verkennen van bestaande schema&#39;s, klassen, mixins, en gegevenstypes in Experience Platform UI.

## Een XDM-bron opzoeken {#lookup}

Selecteer **[!UICONTROL Schema&#39;s]** in de linkernavigatie in de interface van het Platform. De [!UICONTROL werkruimte van Schema] verstrekt een **[!UICONTROL Browse]** lusje om alle bestaande middelen XDM in uw organisatie, samen met extra specifieke lusjes voor het onderzoeken van **[!UICONTROL Klassen]**, **[!UICONTROL Mixins]**, en de types **[!UICONTROL van]** Gegevens specifiek te onderzoeken.

![](../images/tutorials/explore/tabs.png)

Op het tabblad [!UICONTROL Bladeren] kunt u het filterpictogram (![Pictogramafbeelding](../images/tutorials/explore/icon.png)filteren) gebruiken om besturingselementen in de linkerrails weer te geven en de weergegeven resultaten te beperken tot beneden.

Als u bijvoorbeeld de lijst wilt filteren zodat alleen standaardgegevenstypen worden weergegeven die door Adobe worden geleverd, selecteert u **[!UICONTROL Datatype]** en **[!UICONTROL Adobe]** in respectievelijk de secties **[!UICONTROL Type]** en **[!UICONTROL Eigenaar]** .

Met de **[!UICONTROL insteekmodule Profiel]** kunt u resultaten filteren om alleen bronnen weer te geven die worden gebruikt in schema&#39;s die zijn ingeschakeld voor gebruik in [Real-time klantprofiel](../../profile/home.md).

![](../images/tutorials/explore/filter.png)

U kunt de zoekbalk ook gebruiken om resultaten te beperken tot bronnen waarvan de namen overeenkomen met de zoekquery.

![](../images/tutorials/explore/search.png)

Wanneer u de bron hebt gevonden die u wilt verkennen, selecteert u de naam in de lijst om de structuur ervan op het canvas weer te geven.

## Een XDM-resource verkennen in het canvas {#explore}

Wanneer u een bron hebt geselecteerd, wordt de structuur ervan geopend in het canvas.

![](../images/tutorials/explore/canvas.png)

Alle objecten-type gebieden die sub-eigenschappen bevatten worden doen ineenstorten door gebrek wanneer zij eerst in het canvas verschijnen. Als u de subeigenschappen van een veld wilt weergeven, selecteert u het pictogram naast de naam.

![](../images/tutorials/explore/field-expand.png)

### Door het systeem gegenereerde velden {#system-fields}

Sommige schemavelden worden voorafgegaan door een onderstrepingsteken, zoals `_repo` en `_id`. Deze vertegenwoordigen placeholders voor gebieden die het systeem automatisch zal produceren en toewijzen aangezien de gegevens worden opgenomen.

Als dusdanig, zouden de meeste van deze gebieden van de structuur van uw gegevens moeten worden uitgesloten wanneer het opnemen in Platform, met als belangrijkste uitzondering het `_{TENANT_ID}` gebied is, dat alle gebieden XDM die onder uw organisatie worden gecreeerd namespaced onder moeten zijn.

### Datatypen {#data-types}

Voor elk veld dat op het canvas wordt weergegeven, wordt het corresponderende gegevenstype naast de naam weergegeven en wordt in één oogopslag het type gegevens aangegeven dat het veld verwacht voor opname.

Elk gegevenstype dat met vierkante haken (`[]`) wordt toegevoegd, vertegenwoordigt een array van dat specifieke gegevenstype. Een gegevenstype van bijvoorbeeld **[!UICONTROL String]\[]** geeft aan dat het veld een array van tekenreekswaarden verwacht. Een gegevenstype van een **[!UICONTROL betalingsitem]\[]** geeft een array van objecten aan die voldoen aan het gegevenstype [!UICONTROL Betalingsitem] .

Als een arrayveld is gebaseerd op een objecttype, kunt u het pictogram ervan op het canvas selecteren om de verwachte kenmerken voor elk arrayitem weer te geven.

![](../images/tutorials/explore/array-type.png)

### [!UICONTROL Veldeigenschappen] {#field-properties}

Wanneer u de naam van een veld op het canvas selecteert, wordt de rechtertrack bijgewerkt met informatie over dat veld onder **[!UICONTROL Veldeigenschappen]**. Dit kan een beschrijving bevatten van het bedoelde gebruiksgeval van het veld, standaardwaarden, patronen, indelingen, of het veld al dan niet is vereist, enzovoort.

![](../images/tutorials/explore/field-properties.png)

Als het veld dat u inspecteert een opsommingsveld is, geeft de rechterspoorstaaf ook de acceptabele waarden weer die het veld verwacht te ontvangen.

![](../images/tutorials/explore/enum-field.png)

### Identiteitsvelden {#identity}

Wanneer u schema&#39;s inspecteert die identiteitsvelden bevatten, worden deze velden op het canvas gemarkeerd met een vingerafdrukpictogram (![vingerafdrukpictogram](../images/tutorials/explore/identity-symbol.png)). Als u de naam van het identiteitsveld selecteert, kunt u aanvullende informatie weergeven, zoals de naamruimte [van de](../../identity-service/namespaces.md) identiteit en of het veld de primaire identiteit voor het schema is of niet.

![](../images/tutorials/explore/identity-field.png)

### Relatievelden {#relationship}

De gebieden van de verhouding worden ook uniek benadrukt in het canvas, die de naam van het bestemmingsschema tonen dat de gebiedsverwijzingen. Als u de naam van het relatieveld selecteert, kunt u de identiteitsnaamruimte van de primaire identiteit van het bestemmingsschema bekijken.

![](../images/tutorials/explore/relationship-field.png)

>[!NOTE]
>
>Zie het leerprogramma bij het [creëren van een verhouding in UI](./create-schema-ui.md) voor meer informatie over het gebruik van verhoudingen in schema&#39;s XDM.

## Volgende stappen

In dit document wordt beschreven hoe u bestaande XDM-bronnen kunt verkennen in de gebruikersinterface van het Experience Platform. Voor meer informatie over de verschillende eigenschappen van de werkruimte van [!UICONTROL Schema] en [!DNL Schema Editor], zie de [schemaverwezenlijking zelfstudie](./create-schema-ui.md).