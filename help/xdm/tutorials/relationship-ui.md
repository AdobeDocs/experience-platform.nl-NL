---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Bepaal een verband tussen twee schema's gebruikend de Redacteur van het Schema van het Schema
topic: tutorials
translation-type: tm+mt
source-git-commit: 6d291ac9a8c194dd63e411e4d064492c38412749
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---


# Bepaal een verband tussen twee schema&#39;s gebruikend [!DNL Schema Editor]

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van Adobe Experience Platform. Het bepalen van deze verhoudingen binnen de structuur van uw [!DNL Experience Data Model] (XDM) schema&#39;s staat u toe om complexe inzichten in uw klantengegevens te bereiken.

Terwijl de schemaverhoudingen door het gebruik van het unieschema kunnen worden afgeleid en [!DNL Real-time Customer Profile], is dit slechts op schema&#39;s van toepassing die de zelfde klasse delen. Om een verband tussen twee schema&#39;s te vestigen die tot verschillende klassen behoren, moet een specifiek **relatiegebied** aan een bronschema worden toegevoegd, dat de identiteit van een bestemmingsschema verwijst.

Dit document verstrekt een zelfstudie voor het bepalen van een verband tussen twee schema&#39;s gebruikend de Redacteur van het Schema in het [!DNL Experience Platform] gebruikersinterface. Voor stappen bij het bepalen van schemaverhoudingen gebruikend API, zie de zelfstudie over het [bepalen van een verhouding gebruikend de Registratie API](relationship-api.md)van het Schema.

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL XDM System] en de Schema-editor in de [!DNL Experience Platform] UI. Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [XDM-systeem in Experience Platform](../home.md): Een overzicht van XDM en zijn implementatie in [!DNL Experience Platform].
* [Basisbeginselen van de schemacompositie](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [Een schema maken met de Schema-editor](create-schema-ui.md): Een zelfstudie waarin de basisbeginselen van het werken met de [!DNL Schema Editor]code worden besproken.

## Een bron- en doelschema definiëren

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Voor demonstratiedoeleinden creëert deze zelfstudie een relatie tussen leden van het loyaliteitsprogramma van een organisatie (gedefinieerd in een schema &quot;[!UICONTROL Loyalty Member]&quot;) en hun favoriete hotels (gedefinieerd in een &quot;[!DNL Hotels]&quot; schema).

>[!IMPORTANT]
>
>Om een relatie tot stand te brengen, moeten beide schema&#39;s primaire identiteiten hebben bepaald en voor [!DNL Real-time Customer Profile]. Zie de sectie over het [toelaten van een schema voor gebruik in Profiel](./create-schema-ui.md#profile) in de schemacreatie zelfstudie als u begeleiding op hoe te om uw schema&#39;s dienovereenkomstig te vormen vereist.

De verhoudingen van het schema worden vertegenwoordigd door een specifiek gebied binnen een **bronschema** dat naar een ander gebied binnen een **bestemmingsschema** verwijst. In de stappen die volgen, &quot;[!UICONTROL Loyalty Leden]&quot;zal het bronschema zijn, terwijl &quot;[!DNL Hotels]&quot;als bestemmingsschema zal handelen.

Voor verwijzingsdoeleinden, beschrijven de volgende secties de structuur van elk schema dat in dit leerprogramma wordt gebruikt alvorens een verhouding is bepaald.

### [!UICONTROL Schema voor leden] van Loyalty

Het bronschema &quot;Leden[!UICONTROL van de]Loyalty&quot;is gebaseerd op de klasse XDM, en is het schema dat in het leerprogramma voor het [!DNL Individual Profile] creëren van een schema in UI [](create-schema-ui.md)werd geconstrueerd. Het omvat een &quot;[!UICONTROL loyalty]&quot;voorwerp onder zijn \_huurderId&quot;namespace, die verscheidene loyaliteitspecifieke gebieden omvat. Één van deze gebieden, &quot;loyaltyId&quot;, dient als primaire identiteit voor het schema onder &quot;[!UICONTROL E-mail]&quot;namespace. Zoals u onder _[!UICONTROL Schemaeigenschappen]_ziet, is dit schema ingeschakeld voor gebruik in[!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### Hotelschema

Het doelschema &quot;[!UICONTROL Hotels]&quot; is gebaseerd op een aangepaste klasse &quot;[!UICONTROL Hotels]&quot; en bevat velden die een hotel beschrijven. Het veld[!UICONTROL E-mail]fungeert als primaire identiteit voor het schema onder de naamruimte[!UICONTROL E-mail]. Net als &quot;[!UICONTROL Loyalty-leden]&quot; is dit schema ook ingeschakeld voor [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Een relatie-mix maken

>[!NOTE]
>
>Deze stap wordt slechts vereist als uw bronschema geen specifiek koord-type gebied heeft dat als verwijzing naar een ander schema moet worden gebruikt. Als dit veld al in uw bronschema is gedefinieerd, gaat u verder met de volgende stap voor het [definiëren van een relatieveld](#relationship-field).

Om een verband tussen twee schema&#39;s te bepalen, moet het bronschema een specifiek gebied hebben dat als verwijzing naar het bestemmingsschema moet worden gebruikt. U kunt dit veld toevoegen aan het bronschema door een nieuwe mix te maken.

Klik eerst op **[!UICONTROL Toevoegen]** in de sectie _[!UICONTROL Mixins]_.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Het dialoogvenster _[!UICONTROL Mixin]_toevoegen wordt weergegeven. Klik hier op**[!UICONTROL  Nieuwe mixer ]**maken. Voer in de tekstvelden die worden weergegeven een weergavenaam en beschrijving in voor de nieuwe mix. Klik op**[!UICONTROL  Mixin ]**toevoegen wanneer u klaar bent.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Het canvas verschijnt weer met &quot;[!UICONTROL Loyalty Relationship]&quot; in de sectie _[!UICONTROL Mixins]_. Klik op de mixnaam en klik vervolgens op Veld****toevoegen naast het veld[!UICONTROL Loyalty-leden]op hoofdniveau.

![](../images/tutorials/relationship/loyalty-add-field.png)

Er wordt een nieuw veld weergegeven op het canvas onder de naamruimte &quot;\_huurderId&quot;. Geef onder _[!UICONTROL Veldeigenschappen]_een veldnaam en weergavenaam voor het veld op en stel het type in op &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Klik op **[!UICONTROL Toepassen]** als u klaar bent.

![](../images/tutorials/relationship/relationship-field-apply.png)

Het bijgewerkte veld[!UICONTROL FavorietHotel]wordt weergegeven op het canvas. Klik op **[!UICONTROL Opslaan]** om de wijzigingen in het schema te voltooien.

![](../images/tutorials/relationship/relationship-field-save.png)

## Een relatieveld definiëren voor het bronschema {#relationship-field}

Zodra uw bronschema een specifiek die verwijzingsgebied heeft wordt bepaald, kunt u het als relatiegebied aanwijzen.

Selecteer het referentieveld op het canvas en schuif omlaag onder _[!UICONTROL Veldeigenschappen]_totdat het selectievakje**[!UICONTROL  Relatie ]**wordt weergegeven. Schakel het selectievakje in om de vereiste parameters voor het configureren van een relatieveld weer te geven.

![](../images/tutorials/relationship/relationship-checkbox.png)

Selecteer dropdown voor het Schema **[!UICONTROL van de]** Verwijzing en selecteer het bestemmingsschema voor de verhouding (&quot;[!UICONTROL Hotels]&quot;in dit voorbeeld). Als het bestemmingsschema voor Profiel wordt toegelaten, wordt het gebied van Namespace van de Identiteit van de **[!UICONTROL Verwijzing]** automatisch geplaatst aan namespace van de primaire identiteit van het bestemmingsschema. Als voor het schema geen primaire identiteit is gedefinieerd, moet u de naamruimte die u wilt gebruiken handmatig selecteren in het vervolgkeuzemenu. Klik op **[!UICONTROL Toepassen]** als u klaar bent.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Het veld wordt weergegeven als een relatie op het canvas met de naam en naamruimte voor de referentie-id van het doelschema. Klik op **[!UICONTROL Opslaan]** om de wijzigingen op te slaan en de workflow te voltooien.

![](../images/tutorials/relationship/relationship-save.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een één-op-één verhouding tussen twee schema&#39;s gecreeerd gebruikend [!DNL Schema Editor]. Voor stappen op hoe te om verhoudingen te bepalen die API gebruiken, zie de zelfstudie over het [bepalen van een verhouding gebruikend de Registratie API](relationship-api.md)van het Schema.