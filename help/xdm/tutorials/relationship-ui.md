---
keywords: Experience Platform;thuis;populaire onderwerpen;ui;UI;XDM;XDM systeem;ervaringsgegevensmodel;Ervaar gegevensmodel;Gegevensmodel;Gegevensmodel;Gegevensmodel;Schema redacteur;Schema;Schema;schema's;Schema's;creëren;verhouding;Verhouding;verwijzing;Verwijzing;
solution: Experience Platform
title: Bepaal een verhouding tussen Twee Schema's gebruikend de Redacteur van het Schema
description: Dit document verstrekt een zelfstudie voor het bepalen van een verband tussen twee schema's gebruikend de Redacteur van het Schema in het gebruikersinterface van het Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 3b16c0766c7d54b18ceea4c9f40ccb370b9f9685
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# Bepaal een één-op-één verhouding tussen twee schema&#39;s gebruikend [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="Schema-relaties"
>abstract="Schema&#39;s die tot verschillende klassen behoren, kunnen via relatievelden contextueel worden gekoppeld, zodat u complexere segmentatieregels kunt maken. Zie de documentatie voor meer informatie over schemaverhoudingen."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="Referentieschema"
>abstract="Selecteer het schema waarmee u een relatie wilt maken. Dit schema kan een andere klasse zijn dan het huidige schema. Zie de documentatie voor meer informatie over schemaverhoudingen."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="Naamruimte van verwijzing"
>abstract="De naamruimte (type) voor het primaire identiteitsveld van het referentieschema. Het referentieschema moet een bestaand primair identiteitsveld hebben om aan een relatie te kunnen deelnemen. Zie de documentatie voor meer informatie over schemaverhoudingen."

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van Adobe Experience Platform. Deze relaties definiëren binnen de structuur van uw [!DNL Experience Data Model] (XDM) schema&#39;s staan u toe om complexe inzichten in uw klantengegevens te bereiken.

Hoewel schemarelaties kunnen worden afgeleid door het gebruik van het union-schema en [!DNL Real-Time Customer Profile]Dit geldt alleen voor schema&#39;s die dezelfde klasse delen. Om een verband tussen twee schema&#39;s te vestigen die tot verschillende klassen behoren, moet een specifiek relatiegebied aan een bronschema worden toegevoegd, dat de identiteit van het andere verwante schema verwijzingen.

Dit document bevat een zelfstudie voor het definiëren van een relatie tussen twee schema&#39;s met behulp van de Schema-editor in het dialoogvenster [!DNL Experience Platform] gebruikersinterface. Raadpleeg de zelfstudie voor meer informatie over het definiëren van schema-relaties met de API [een relatie definiëren met de API voor het schemaregister](relationship-api.md).

>[!NOTE]
>
>Raadpleeg de handleiding voor meer informatie over het maken van een vele-op-één relatie in Adobe Real-time Customer Data Platform B2B Edition [B2B-relaties maken](./relationship-b2b.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL XDM System] en de Schema-editor in de [!DNL Experience Platform] UI. Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [XDM-systeem in Experience Platform](../home.md): Een overzicht van XDM en zijn implementatie in [!DNL Experience Platform].
* [Basisbeginselen van de schemacompositie](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [Een schema maken met de opdracht [!DNL Schema Editor]](create-schema-ui.md): Een zelfstudie waarin de basisbeginselen van het werken met de [!DNL Schema Editor].

## Een bron- en referentieschema definiëren

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Voor demonstratiedoeleinden creëert deze zelfstudie een relatie tussen leden van het loyaliteitsprogramma van een organisatie (gedefinieerd in een &quot;[!DNL Loyalty Members]&quot; schema) en hun favoriete hotel (gedefinieerd in &quot;[!DNL Hotels]&quot; schema).

>[!IMPORTANT]
>
>Om een relatie tot stand te brengen, moeten beide schema&#39;s primaire identiteiten hebben bepaald en geschikt zijn gemaakt voor [!DNL Real-Time Customer Profile]. Zie de sectie over [een schema inschakelen voor gebruik in profiel](./create-schema-ui.md#profile) in de zelfstudie van de schemaverwezenlijking als u begeleiding op hoe te om uw schema&#39;s dienovereenkomstig te vormen vereist.

Schemarelaties worden vertegenwoordigd door een specifiek veld binnen een **bronschema** dat naar een ander veld binnen een **referentieschema**. In de volgende stappen: &quot;[!DNL Loyalty Members]&quot; wordt het bronschema, terwijl &quot;[!DNL Hotels]&quot; fungeert als het referentieschema.

In de volgende secties wordt de structuur beschreven van elk schema dat in deze zelfstudie wordt gebruikt voordat een relatie is gedefinieerd.

### [!DNL Loyalty Members] schema

Het bronschema &quot;[!DNL Loyalty Members]&quot; is gebaseerd op de [!DNL XDM Individual Profile] klasse, die gebied bevat dat leden van een loyaliteitsprogramma beschrijft. Een van deze velden, `personalEmail.addess`, dient als primaire identiteit voor het schema onder het [!UICONTROL Email] naamruimte. Zoals onder **[!UICONTROL Schema Properties]**, is dit schema ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Het referentieschema &quot;[!DNL Hotels]&quot; is gebaseerd op een aangepaste &quot;[!DNL Hotels]&quot; en bevat velden die een hotel beschrijven. Om aan een verhouding deel te nemen, moet het verwijzingsschema ook een primaire bepaalde identiteit hebben en toegelaten voor [!UICONTROL Profile]. In dit geval: `_tenantId.hotelId`handelt als primaire identiteit voor het schema, gebruikend een douane &quot;[!DNL Hotel ID]naamruimte identiteit.

![Inschakelen voor profiel](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Als u wilt leren hoe u aangepaste naamruimten kunt maken, raadpleegt u de [Identiteitsdocumentatie](../../identity-service/namespaces.md#manage-namespaces).

## Een relatieveldgroep maken

>[!NOTE]
>
>Deze stap wordt slechts vereist als uw bronschema geen specifiek koord-type gebied heeft dat als wijzer aan de primaire identiteit van het verwijzingsschema moet worden gebruikt. Als dit veld al in uw bronschema is gedefinieerd, gaat u verder met de volgende stap van [relatieveld definiëren](#relationship-field).

Om een verhouding tussen twee schema&#39;s te bepalen, moet het bronschema een specifiek gebied hebben dat op de primaire identiteit van het verwijzingsschema zal wijzen. U kunt dit gebied aan het bronschema toevoegen door een nieuwe groep van het schemagebied te creëren of bestaande uit te breiden.

In het geval van de [!DNL Loyalty Members] schema, een nieuw `preferredHotel` het veld zal worden toegevoegd om het voorkeurhotel van het loyaliteitslid voor bedrijfsbezoeken aan te geven . Begin door het plusteken te selecteren (**+**) naast de naam van het bronschema.

![](../images/tutorials/relationship/loyalty-add-field.png)

Er wordt een nieuwe plaatsaanduiding voor velden weergegeven op het canvas. Onder **[!UICONTROL Field properties]** geeft u een veldnaam en weergavenaam voor het veld op en stelt u het type in op &quot;[!UICONTROL String]&quot;. Onder **[!UICONTROL Assign to]** selecteert u een bestaande veldgroep die u wilt uitbreiden of typt u een unieke naam om een nieuwe veldgroep te maken. In dit geval wordt &quot;[!DNL Preferred Hotel]&quot; wordt een veldgroep gemaakt.

![](../images/tutorials/relationship/relationship-field-details.png)

Als u klaar bent, selecteert u **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

De bijgewerkte `preferredHotel` wordt weergegeven op het canvas, dat zich onder een `_tenantId` object omdat het een aangepast veld is. Selecteren **[!UICONTROL Save]** om uw wijzigingen in het schema te voltooien.

![](../images/tutorials/relationship/relationship-field-save.png)

## Een relatieveld definiëren voor het bronschema {#relationship-field}

Zodra uw bronschema een specifiek die verwijzingsgebied heeft wordt bepaald, kunt u het als relatiegebied aanwijzen.

>[!NOTE]
>
>In de onderstaande stappen wordt beschreven hoe u een relatieveld definieert met behulp van de besturingselementen voor rechterspoor op het canvas. Als u toegang hebt tot de Real-Time CDP B2B Edition, kunt u ook een een-op-een relatie definiëren met behulp van de [zelfde dialoogvenster](./relationship-b2b.md#relationship-field) zoals wanneer het creëren van vele-aan-één verhoudingen.

Selecteer `preferredHotel` veld op het canvas, schuiven vervolgens omlaag onder **[!UICONTROL Field properties]** tot de **[!UICONTROL Relationship]** wordt weergegeven. Schakel het selectievakje in om de vereiste parameters voor het configureren van een relatieveld weer te geven.

![](../images/tutorials/relationship/relationship-checkbox.png)

Vervolgkeuzelijst selecteren voor **[!UICONTROL Reference schema]** en selecteer het referentieschema voor de relatie (&quot;[!DNL Hotels]&quot; in dit voorbeeld). Onder **[!UICONTROL Reference identity namespace]** selecteert u de naamruimte van het identiteitsveld van het referentieschema (in dit geval &quot;[!DNL Hotel ID]&quot;). Selecteren **[!UICONTROL Apply]** wanneer gereed.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

De `preferredHotel` wordt nu gemarkeerd als een relatie op het canvas en geeft de naam van het referentieschema weer. Selecteren **[!UICONTROL Save]** om uw wijzigingen op te slaan en de workflow te voltooien.

![](../images/tutorials/relationship/relationship-save.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u met succes een één-aan-één verhouding tussen twee schema&#39;s gecreeerd gebruikend [!DNL Schema Editor]. Raadpleeg de zelfstudie voor meer informatie over het definiëren van relaties met de API [een relatie definiëren met de API voor het schemaregister](relationship-api.md).
