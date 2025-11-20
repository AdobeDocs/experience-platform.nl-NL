---
keywords: Experience Platform;home;populaire onderwerpen;ui;UI;XDM;XDM systeem;ervaringsgegevensmodel;Beleidingsgegevensmodel;Gegevensmodel;Gegevensmodel;Gegevensmodel;Schema-editor;Schema;Schema;Schema;Schema's;Schema's;Maken;Relatie;Referentie;Referentie;
solution: Experience Platform
title: Een relatie tussen twee schema's definiëren met de Schema-editor
description: Dit document biedt een zelfstudie voor het definiëren van een relatie tussen twee schema's met behulp van de Schema-editor in de Experience Platform-gebruikersinterface.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5f9fdc9eff4d8bba049c03058d24e80e9b89e953
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---

# Een een-op-een relatie tussen twee schema&#39;s definiëren met de [!DNL Schema Editor] {#relationship-ui}

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

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van Adobe Experience Platform. Door deze relaties te definiëren binnen de structuur van uw [!DNL Experience Data Model] (XDM)-schema&#39;s kunt u complexe inzichten in uw klantgegevens opdoen.

Hoewel schemarelaties kunnen worden afgeleid door het gebruik van het samenvoegingsschema en [!DNL Real-Time Customer Profile] , geldt dit alleen voor schema&#39;s die dezelfde klasse delen. Om een verband tussen twee schema&#39;s te vestigen die tot verschillende klassen behoren, moet een specifiek relatiegebied aan een bronschema worden toegevoegd, dat de identiteit van het andere verwante schema verwijzingen.

>[!NOTE]
>
>Als zowel de bron als bestemmingsschema&#39;s tot de zelfde klasse behoren, zou een specifiek relatiegebied **niet** moeten worden gebruikt. In dit geval, gebruik het unieschema UI om de verhouding te zien. De instructies op hoe te om dit te doen kunnen in de [ sectie van meningsverhoudingen ](../../profile/ui/union-schema.md#view-relationships) van de gids UI van het unieschema worden gevonden.

Dit document bevat een zelfstudie voor het definiëren van een relatie tussen twee schema&#39;s met behulp van de Schema-editor in de gebruikersinterface van [!DNL Experience Platform] . Voor stappen bij het bepalen van schemaverhoudingen die API gebruiken, zie het leerprogramma op [ het bepalen van een verhouding gebruikend de Registratie API van het Schema ](relationship-api.md).

>[!NOTE]
>
>Voor stappen op hoe te om een vele-aan-één verhouding in Adobe Real-Time Customer Data Platform B2B edition tot stand te brengen, zie de gids op [ het creëren van B2B verhoudingen ](./relationship-b2b.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL XDM System] en de Schema-editor in de gebruikersinterface van [!DNL Experience Platform] . Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [ XDM Systeem in Experience Platform ](../home.md): Een overzicht van XDM en zijn implementatie in [!DNL Experience Platform].
* [ Grondbeginselen van schemacompositie ](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [ creeer een schema gebruikend  [!DNL Schema Editor]](create-schema-ui.md): Een leerprogramma dat de grondbeginselen van het werken met [!DNL Schema Editor] behandelt.

## Een bron- en referentieschema definiëren

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Voor demonstratiedoeleinden, leidt dit leerprogramma tot een verband tussen leden van het loyaliteitsprogramma van een organisatie (die in een &quot;[!DNL Loyalty Members]&quot;schema wordt bepaald) en hun favoriet hotel (die in een &quot;[!DNL Hotels]&quot;schema wordt bepaald).

>[!IMPORTANT]
>
>Om een relatie tot stand te brengen, moeten beide schema&#39;s primaire identiteiten hebben bepaald en voor [!DNL Real-Time Customer Profile] worden toegelaten. Zie de sectie op [ toelatend een schema voor gebruik in Profiel ](./create-schema-ui.md#profile) in het leerprogramma van de schemaverwezenlijking als u begeleiding op hoe te om uw schema&#39;s dienovereenkomstig te vormen vereist.

De verhoudingen van het schema worden vertegenwoordigd door een specifiek gebied binnen a **bronschema** dat aan een ander gebied binnen a **verwijzingsschema** richt. In de stappen die volgen, &quot;[!DNL Loyalty Members]&quot;zal het bronschema zijn, terwijl &quot;[!DNL Hotels]&quot;als verwijzingsschema zal dienst doen.

In de volgende secties wordt de structuur beschreven van elk schema dat in deze zelfstudie wordt gebruikt voordat een relatie is gedefinieerd.

### [!DNL Loyalty Members] schema

Het bronschema &quot;[!DNL Loyalty Members]&quot;is gebaseerd op de [!DNL XDM Individual Profile] klasse, die gebied bevat dat leden van een loyaliteitsprogramma beschrijft. Een van deze velden, `personalEmail.addess` , fungeert als primaire identiteit voor het schema onder de naamruimte [!UICONTROL Email] . Zoals u onder **[!UICONTROL Schema Properties]** ziet, is dit schema ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile] .

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Het verwijzingsschema &quot;[!DNL Hotels]&quot;is gebaseerd op een douane &quot;[!DNL Hotels]&quot;klasse, en bevat gebieden die een hotel beschrijven. Als u wilt deelnemen aan een relatie, moet voor het referentieschema ook een primaire identiteit zijn gedefinieerd en ingeschakeld voor [!UICONTROL Profile] . In dit geval, `_tenantId.hotelId` handelt als primaire identiteit voor het schema, gebruikend een douane &quot;[!DNL Hotel ID]&quot;identiteitsnaamruimte.

![ laat voor Profiel ](../images/tutorials/relationship/hotels.png) toe

>[!NOTE]
>
>Leren hoe te om douaneidentiteit te creëren namespaces, verwijs naar de [ documentatie van de Dienst van de Identiteit ](../../identity-service/features/namespaces.md#manage-namespaces).

## Een relatieveldgroep maken

>[!NOTE]
>
>Deze stap wordt slechts vereist als uw bronschema geen specifiek koord-type gebied heeft dat als wijzer aan de primaire identiteit van het verwijzingsschema moet worden gebruikt. Als dit gebied reeds in uw bronschema wordt bepaald, overslaan aan de volgende stap van [ die een relatiegebied ](#relationship-field) bepalen.

Om een verhouding tussen twee schema&#39;s te bepalen, moet het bronschema een specifiek gebied hebben dat op de primaire identiteit van het verwijzingsschema zal wijzen. U kunt dit gebied aan het bronschema toevoegen door een nieuwe groep van het schemagebied te creëren of bestaande uit te breiden.

In het geval van het [!DNL Loyalty Members] schema, zal een nieuw `preferredHotel` gebied worden toegevoegd om het aangewezen hotel van het loyaliteitslid voor bedrijfbezoeken aan te geven. Begin door het plusteken (**+**) naast de naam van het bronschema te selecteren.

![](../images/tutorials/relationship/loyalty-add-field.png)

Er wordt een nieuwe plaatsaanduiding voor velden weergegeven op het canvas. Geef onder **[!UICONTROL Field properties]** een veldnaam en weergavenaam voor het veld op en stel het type in op &quot;[!UICONTROL String]&quot;. Selecteer onder **[!UICONTROL Assign to]** een bestaande veldgroep die u wilt uitbreiden of typ een unieke naam om een nieuwe veldgroep te maken. In dit geval wordt een nieuwe veldgroep &quot;[!DNL Preferred Hotel]&quot; gemaakt.

![](../images/tutorials/relationship/relationship-field-details.png)

Selecteer **[!UICONTROL Apply]** als u klaar bent.

![](../images/tutorials/relationship/relationship-field-apply.png)

Het bijgewerkte veld `preferredHotel` wordt weergegeven op het canvas, dat zich onder een object `_tenantId` bevindt, aangezien het een aangepast veld is. Selecteer **[!UICONTROL Save]** om de wijzigingen in het schema te voltooien.

![](../images/tutorials/relationship/relationship-field-save.png)

## Een relatieveld definiëren voor het bronschema {#relationship-field}

Zodra uw bronschema een specifiek die verwijzingsgebied heeft wordt bepaald, kunt u het als relatiegebied aanwijzen.

>[!NOTE]
>
>Relaties kunnen alleen worden ondersteund in tekenreeks- of tekenreeksarrayvelden.

Selecteer het veld `preferredHotel` op het canvas en selecteer vervolgens **[!UICONTROL Add relationship]** in het zijpaneel van **[!UICONTROL Field properties]** .

![ de Redacteur van het Schema met Add verhouding die in de eigenschappen sidebar van het Gebied wordt benadrukt.](../images/tutorials/relationship/add-relationship.png)

Het dialoogvenster [!UICONTROL Add relationship] wordt weergegeven. In dit dialoogvenster kunt u vereiste parameters instellen voor het configureren van een relatieveld. Voor Real-Time CDP B2C gebruikers, kunt u **slechts** plaatsen een één-aan-één verhouding tussen de bron en verwijzingsschema.

>[!NOTE]
>
>Als u toegang tot Real-Time CDP B2B edition hebt, kunt u de de juiste-spoorcontroles van het canvas gebruiken om een relatieveld te bepalen, evenals een vele-aan-één verhouding te bouwen gebruikend de [ zelfde dialoog ](./relationship-b2b.md#relationship-field).

![ de Add relatiedialoog.](../images/tutorials/relationship/add-relationship-dialog.png)

Gebruik dropdown voor **[!UICONTROL Reference schema]** en selecteer het verwijzingsschema voor de verhouding (&quot;[!DNL Hotels]&quot;in dit voorbeeld).

>[!NOTE]
>
>Alleen schema&#39;s met een primaire identiteit worden opgenomen in het vervolgkeuzemenu van het referentieschema. Deze bescherming verhindert u per ongeluk een verhouding met een schema tot stand te brengen dat nog niet behoorlijk wordt gevormd.

De identiteitsnaamruimte van het verwijzingsschema (in dit geval &quot;[!DNL Hotel ID]&quot;) wordt automatisch onder **[!UICONTROL Reference identity namespace]** gevuld. Selecteer **[!UICONTROL Apply]** wanneer u klaar bent.

![ voegt relatiedialoog met de gevormde relatieparameters toe en is benadrukt van toepassing.](../images/tutorials/relationship/apply-relationship.png)

Het veld `preferredHotel` wordt nu gemarkeerd als een relatie op het canvas en geeft de naam van het referentieschema weer. Selecteer **[!UICONTROL Save]** om uw wijzigingen op te slaan en de workflow te voltooien.

![ de Redacteur van het Schema met de relatieverwijzingen en sparen benadrukte.](../images/tutorials/relationship/relationship-save.png)

### Een bestaand relatieveld bewerken {#edit-relationship}

Als u het referentieschema wilt wijzigen, selecteert u een veld met een bestaande relatie en selecteert u vervolgens **[!UICONTROL Edit relationship]** in de zijbalk van **[!UICONTROL Field properties]** .

![ de Redacteur van het Schema met Edit benadrukte verhouding.](../images/tutorials/relationship/edit-relationship.png)

Het dialoogvenster [!UICONTROL Edit relationship] wordt weergegeven. Van hier, kunt u het proces volgen dat in [ wordt geschetst bepalend een relatieveld ](#relationship-field) of de verhouding schrappen. Selecteer **[!UICONTROL Delete relationship]** om de relatie met het referentieschema te verwijderen.

![ de Edit relatiedialoog.](../images/tutorials/relationship/edit-relationship-dialog.png)

## Filter en zoek naar relaties {#filter-and-search}

U kunt filteren en naar specifieke relaties in uw schema&#39;s zoeken op het tabblad [!UICONTROL Relationships] van de [!UICONTROL Schemas] -werkruimte. Met deze weergave kunt u snel uw relaties zoeken en beheren. Lees het document op [ het onderzoeken van schemamiddelen ](../ui/explore.md#lookup) voor gedetailleerde instructies op de het filtreren opties.

![ het lusje van Verhoudingen in de werkruimte van Schema&#39;s.](../images/tutorials/relationship-b2b/relationship-tab.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een één-op-één verhouding tussen twee schema&#39;s tot stand gebracht gebruikend [!DNL Schema Editor]. Voor stappen op hoe te om verhoudingen te bepalen die API gebruiken, zie het leerprogramma op [ bepalend een verband gebruikend de Registratie API van het Schema ](relationship-api.md).
