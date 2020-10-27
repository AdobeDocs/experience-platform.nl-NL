---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: Bepaal een verband tussen twee schema's gebruikend de Redacteur van het Schema van het Schema
description: Dit document verstrekt een zelfstudie voor het bepalen van een verband tussen twee schema's gebruikend de Redacteur van het Schema in het gebruikersinterface van het Experience Platform.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 097fe219e0d64090de758f388ba98e6024db2201
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---


# Bepaal een verband tussen twee schema&#39;s gebruikend [!DNL Schema Editor]

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van Adobe Experience Platform. Het bepalen van deze verhoudingen binnen de structuur van uw [!DNL Experience Data Model] (XDM) schema&#39;s staat u toe om complexe inzichten in uw klantengegevens te bereiken.

Terwijl de schemaverhoudingen door het gebruik van het unieschema kunnen worden afgeleid en [!DNL Real-time Customer Profile], is dit slechts op schema&#39;s van toepassing die de zelfde klasse delen. Om een verband tussen twee schema&#39;s te vestigen die tot verschillende klassen behoren, moet een specifiek relatiegebied aan een bronschema worden toegevoegd, dat de identiteit van een bestemmingsschema van verwijzingen voorziet.

Dit document verstrekt een zelfstudie voor het bepalen van een verband tussen twee schema&#39;s gebruikend de Redacteur van het Schema in het [!DNL Experience Platform] gebruikersinterface. Voor stappen bij het bepalen van schemaverhoudingen gebruikend API, zie de zelfstudie over het [bepalen van een verhouding gebruikend de Registratie API](relationship-api.md)van het Schema.

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL XDM System] en de Schema-editor in de [!DNL Experience Platform] UI. Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [XDM-systeem in Experience Platform](../home.md): Een overzicht van XDM en zijn implementatie in [!DNL Experience Platform].
* [Basisbeginselen van de schemacompositie](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [Maak een schema met het [!DNL Schema Editor]](create-schema-ui.md)volgende: Een zelfstudie waarin de basisbeginselen van het werken met de [!DNL Schema Editor]code worden besproken.

## Een bron- en doelschema definiëren

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Voor demonstratiedoeleinden, leidt dit leerprogramma tot een verband tussen leden van het loyaliteitsprogramma van een organisatie (die in een &quot;[!DNL Loyalty Members]&quot;schema wordt bepaald) en hun favoriet hotel (die in een &quot;[!DNL Hotels]&quot;schema wordt bepaald).

>[!IMPORTANT]
>
>Om een relatie tot stand te brengen, moeten beide schema&#39;s primaire identiteiten hebben bepaald en voor [!DNL Real-time Customer Profile]. Zie de sectie over het [toelaten van een schema voor gebruik in Profiel](./create-schema-ui.md#profile) in de schemacreatie zelfstudie als u begeleiding op hoe te om uw schema&#39;s dienovereenkomstig te vormen vereist.

De verhoudingen van het schema worden vertegenwoordigd door een specifiek gebied binnen een **bronschema** dat naar een ander gebied binnen een **bestemmingsschema** verwijst. In de stappen die volgen, &quot;[!DNL Loyalty Members]&quot;zal het bronschema zijn, terwijl &quot;[!DNL Hotels]&quot;als bestemmingsschema zal handelen.

Voor verwijzingsdoeleinden, beschrijven de volgende secties de structuur van elk schema dat in dit leerprogramma wordt gebruikt alvorens een verhouding is bepaald.

### [!DNL Loyalty Members] schema

Het bronschema &quot;[!DNL Loyalty Members]&quot;is gebaseerd op de [!DNL XDM Individual Profile] klasse, en is het schema dat in het leerprogramma voor het [creëren van een schema in UI](create-schema-ui.md)werd samengesteld. Het omvat een `loyalty` voorwerp onder zijn `_tenantId` namespace, die verscheidene loyaliteitspecifieke gebieden omvat. Een van deze velden `loyaltyId`fungeert als primaire identiteit voor het schema onder de naamruimte [!UICONTROL E-mail] . Zoals u onder **[!UICONTROL Schemaeigenschappen]** ziet, is dit schema ingeschakeld voor gebruik in [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Het bestemmingsschema &quot;[!DNL Hotels]&quot;is gebaseerd op een douane &quot;[!DNL Hotels]&quot;klasse, en bevat gebieden die een hotel beschrijven. Het `hotelId` veld fungeert als primaire identiteit voor het schema onder een aangepaste `hotelId` naamruimte. Net als het [!DNL Loyalty Members] schema is dit schema ook ingeschakeld voor [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Een relatie-mix maken

>[!NOTE]
>
>Deze stap wordt slechts vereist als uw bronschema geen specifiek tekenreeks-type gebied heeft dat als verwijzing naar het bestemmingsschema moet worden gebruikt. Als dit veld al in uw bronschema is gedefinieerd, gaat u verder met de volgende stap voor het [definiëren van een relatieveld](#relationship-field).

Om een verband tussen twee schema&#39;s te bepalen, moet het bronschema een specifiek gebied hebben dat als verwijzing naar het bestemmingsschema moet worden gebruikt. U kunt dit veld toevoegen aan het bronschema door een nieuwe mix te maken.

Selecteer eerst **[!UICONTROL Toevoegen]** in de sectie **[!UICONTROL Mixins]** .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Het dialoogvenster [!UICONTROL Mixin] toevoegen wordt weergegeven. Van hier, uitgezochte **[!UICONTROL creeer nieuwe mengeling]**. Voer in de tekstvelden die worden weergegeven een weergavenaam en beschrijving in voor de nieuwe mix. Selecteer Mengsel **[!UICONTROL toevoegen]** wanneer u klaar bent.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Het canvas verschijnt weer met &quot;[!DNL Favorite Hotel]&quot; in de sectie **[!UICONTROL Mixins]** . Selecteer de naam van de mix en selecteer vervolgens het veld **** Toevoegen naast het `Loyalty Members` veld op hoofdniveau.

![](../images/tutorials/relationship/loyalty-add-field.png)

Er wordt een nieuw veld weergegeven op het canvas onder de `_tenantId` naamruimte. Geef onder **[!UICONTROL Eigenschappen]** Veld een veldnaam en weergavenaam voor het veld op en stel het type in op &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Als u klaar bent, selecteert u **[!UICONTROL Toepassen]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Het bijgewerkte `favoriteHotel` veld wordt weergegeven op het canvas. Selecteer **[!UICONTROL Opslaan]** om de wijzigingen in het schema te voltooien.

![](../images/tutorials/relationship/relationship-field-save.png)

## Een relatieveld definiëren voor het bronschema {#relationship-field}

Zodra uw bronschema een specifiek die verwijzingsgebied heeft wordt bepaald, kunt u het als relatiegebied aanwijzen.

Selecteer het `favoriteHotel` veld op het canvas en schuif omlaag onder **[!UICONTROL Veldeigenschappen]** totdat het selectievakje **[!UICONTROL Relatie]** wordt weergegeven. Schakel het selectievakje in om de vereiste parameters voor het configureren van een relatieveld weer te geven.

![](../images/tutorials/relationship/relationship-checkbox.png)

Selecteer dropdown voor het schema **[!UICONTROL van de]** Verwijzing en selecteer het bestemmingsschema voor de verhouding (&quot;[!DNL Hotels]&quot;in dit voorbeeld). Als het bestemmingsschema voor wordt toegelaten [!DNL Profile], wordt het gebied van de naamruimte **[!UICONTROL van de Identiteit van de]** Verwijzing automatisch geplaatst aan namespace van de primaire identiteit van het bestemmingsschema. Als voor het schema geen primaire identiteit is gedefinieerd, moet u de naamruimte die u wilt gebruiken handmatig selecteren in het vervolgkeuzemenu. Selecteer **[!UICONTROL Toepassen]** wanneer u klaar bent.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Het `favoriteHotel` veld wordt nu gemarkeerd als een relatie op het canvas en geeft de naam en naamruimte voor de referentie-id van het doelschema weer. Selecteer **[!UICONTROL Opslaan]** om uw wijzigingen op te slaan en de workflow te voltooien.

![](../images/tutorials/relationship/relationship-save.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een één-op-één verhouding tussen twee schema&#39;s gecreeerd gebruikend [!DNL Schema Editor]. Voor stappen op hoe te om verhoudingen te bepalen die API gebruiken, zie de zelfstudie over het [bepalen van een verhouding gebruikend de Registratie API](relationship-api.md)van het Schema.