---
title: Een relatie definiëren tussen twee schema's in Real-time Customer Data Platform B2B Edition
description: Leer hoe u een vele-op-één relatie tussen twee schema's in Real-time Customer Data Platform B2B Edition definieert.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: 86a230d746d6642437c4e37958c07a1186ebadc3
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 0%

---

# Een veel-op-een relatie definiëren tussen twee schema&#39;s in Real-time Customer Data Platform B2B Edition {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="Referentieschema"
>abstract="Selecteer het schema u een verband met wilt vestigen. Afhankelijk van de klasse van het schema, kan het bestaande verhoudingen met andere entiteiten in de context B2B ook hebben. Zie de documentatie om te leren hoe de B2B schemaklassen op elkaar betrekking hebben."

Real-time Customer Data Platform B2B Edition biedt verschillende XDM-klassen (Experience Data Model) die fundamentele B2B-gegevensentiteiten vastleggen, waaronder [rekeningen](../classes/b2b/business-account.md), [kansen](../classes/b2b/business-opportunity.md), [campagnes](../classes/b2b/business-campaign.md)en meer. Door schema&#39;s te bouwen die op deze klassen worden gebaseerd en hen toe te laten voor gebruik binnen [Klantprofiel in realtime](../../profile/home.md), kunt u gegevens uit verschillende bronnen samenvoegen in een verenigde vertegenwoordiging genoemd een unieschema.

Unieschema&#39;s kunnen echter alleen velden bevatten die zijn vastgelegd door schema&#39;s die dezelfde klasse delen. Hier komen schemarelaties binnen. Door relaties in uw B2B-schema&#39;s uit te voeren, kunt u beschrijven hoe deze bedrijfsentiteiten met elkaar verband houden en kunt u kenmerken van meerdere klassen in downstreamgevallen van segmentatiegebruik opnemen.

Het volgende diagram verstrekt een voorbeeld van hoe de verschillende klassen B2B op elkaar in een basisimplementatie kunnen betrekking hebben:

![B2B-klassenrelaties](../images/tutorials/relationship-b2b/classes.png)

Deze zelfstudie behandelt de stappen om een vele-aan-één verhouding tussen twee schema&#39;s in Echte - tijd CDP B2B Uitgave te bepalen.

>[!NOTE]
>
>Als u Real-time Customer Data Platform B2B Edition niet gebruikt of een een-op-een relatie wilt maken, raadpleegt u de handleiding [een één-op-één relatie maken](./relationship-ui.md) in plaats daarvan.
>
>Dit leerprogramma concentreert zich op hoe te om relaties tussen B2B- schema&#39;s in het Platform UI manueel te vestigen. Als u gegevens van een B2B bronverbinding brengt, kunt u een auto-generatienut gebruiken om de vereiste schema&#39;s, identiteiten, en verhoudingen in plaats daarvan tot stand te brengen. Raadpleeg de documentatie bij bronnen over B2B-naamruimten en -schema&#39;s voor meer informatie over [het gebruik van het hulpprogramma voor automatisch genereren](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL XDM System] en de Schema-editor in de [!DNL Experience Platform] UI. Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [XDM-systeem in Experience Platform](../home.md): Een overzicht van XDM en zijn implementatie in [!DNL Experience Platform].
* [Basisbeginselen van de schemacompositie](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [Een schema maken met de opdracht [!DNL Schema Editor]](create-schema-ui.md): Een zelfstudie waarin de grondbeginselen van het maken en bewerken van schema&#39;s in de gebruikersinterface worden besproken.

## Een bron- en doelschema definiëren

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Voor demonstratiedoeleinden leidt deze zelfstudie tot een verband tussen bedrijfskansen (die in &quot;[!DNL Opportunities]&quot; schema) en hun bijbehorende bedrijfsrekening (bepaald in &quot;[!DNL Accounts]&quot; schema).

Schemarelaties worden vertegenwoordigd door een specifiek veld binnen een **bronschema** dat verwijst naar het primaire identiteitsveld van een **doelschema**. In de volgende stappen: &quot;[!DNL Opportunities]&quot; dient als het bronschema, terwijl &quot;[!DNL Accounts]&quot; fungeert als het doelschema.

### Inzicht in identiteiten in B2B-relaties

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Naamruimte van verwijzing"
>abstract="De naamruimte (type) voor het primaire identiteitsveld van het referentieschema. Het referentieschema moet een bestaand primair identiteitsveld hebben om aan een relatie te kunnen deelnemen. Raadpleeg de documentatie voor meer informatie over identiteiten in B2B-relaties."

Om een verhouding te vestigen, moet het bestemmingsschema een bepaalde primaire identiteit hebben. Houd er bij het instellen van een primaire identiteit voor een B2B-entiteit rekening mee dat op tekenreeks gebaseerde entiteit-id&#39;s elkaar kunnen overlappen als u deze verzamelt op verschillende systemen of locaties, wat tot gegevensconflicten in Platform kan leiden.

Om hiermee rekening te houden, bevatten alle standaard B2B-klassen &quot;sleutelvelden&quot; die voldoen aan de [[!UICONTROL B2B Source] gegevenstype](../data-types/b2b-source.md). Dit gegevenstype verschaft velden voor een tekenreeks-id voor de B2B-entiteit, samen met andere contextuele informatie over de bron van de id. Een van deze velden, `sourceKey`voegt de waarden van de andere velden in het gegevenstype samen tot een geheel unieke identificatie voor de entiteit. Dit veld moet altijd worden gebruikt als de primaire identiteit voor B2B-entiteitsschema&#39;s.

![sourceKey, veld](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Wanneer [een XDM-veld instellen als identiteit](../ui/fields/identity.md)moet u een naamruimte voor identiteit opgeven om de identiteit onder te definiëren. Dit kan een standaardnaamruimte zijn die door Adobe wordt geboden of een aangepaste naamruimte die door uw organisatie wordt gedefinieerd. In de praktijk is de naamruimte gewoon een contextafhankelijke tekenreeks en kan deze worden ingesteld op elke gewenste waarde, mits deze voor uw organisatie van belang is voor het categoriseren van het identiteitstype. Zie het overzicht op [naamruimten](../../identity-service/namespaces.md) voor meer informatie .

Voor verwijzingsdoeleinden, beschrijven de volgende secties de structuur van elk schema dat in dit leerprogramma wordt gebruikt alvorens een verhouding is bepaald. Let op waar de primaire identiteiten zijn gedefinieerd in de schemastructuur en de aangepaste naamruimten die ze gebruiken.

### [!DNL Opportunities] schema

Het bronschema &quot;[!DNL Opportunities]&quot; is gebaseerd op de [!UICONTROL XDM Business Opportunity] klasse. Een van de velden die door de klasse worden verschaft. `opportunityKey`, dient als id voor het schema. In het bijzonder de `sourceKey` onder de `opportunityKey` object wordt ingesteld als de primaire identiteit van het schema onder een aangepaste naamruimte [!DNL B2B Opportunity].

Zoals onder **[!UICONTROL Schema Properties]**, is dit schema ingeschakeld voor gebruik in [!DNL Real-time Customer Profile].

![Opportuniteitsschema](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

Het doelschema &quot;[!DNL Accounts]&quot; is gebaseerd op de [!UICONTROL XDM Account] klasse. Het hoofdniveau `accountKey` bevat het veld `sourceKey` die als primaire identiteit onder een aangepaste naamruimte fungeert die [!DNL B2B Account]. Dit schema is ook ingeschakeld voor gebruik in Profiel.

![Accounts-schema](../images/tutorials/relationship-b2b/accounts.png)

## Een relatieveld definiëren voor het bronschema {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Relatienaam uit huidig schema"
>abstract="A label that describes the relationship from the current schema to the reference schema (example, &#39;Related Account&#39;). Dit label wordt gebruikt in Profiel en Segmentatie om context te geven aan gegevens van verwante B2B-entiteiten. Zie de documentatie om meer over het bouwen van B2B schemaverhoudingen te leren."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Relatienaam van referentieschema"
>abstract="A label that describes the relationship from the reference schema to the current schema (example, &#39;Related Opportunity&#39;). Dit label wordt gebruikt in Profiel en Segmentatie om context te geven aan gegevens van verwante B2B-entiteiten. Zie de documentatie om meer over het bouwen van B2B schemaverhoudingen te leren."

Om een verband tussen twee schema&#39;s te bepalen, moet het bronschema een specifiek gebied hebben dat verwijzingen de primaire identiteit van het bestemmingsschema. De standaard B2B-klassen omvatten specifieke bronsleutelvelden voor algemeen verwante bedrijfsentiteiten. De [!UICONTROL XDM Business Opportunity] klasse bevat bronsleutelvelden voor een verwante account (`accountKey`) en een daarmee samenhangende campagne (`campaignKey`). U kunt echter ook andere [!UICONTROL B2B Source] velden naar het schema door aangepaste veldgroepen te gebruiken als u meer dan de standaardcomponenten nodig hebt.

>[!NOTE]
>
>Momenteel, slechts kunnen vele-aan-één en één-aan-één verhoudingen van een bronschema aan een bestemmingsschema worden bepaald. Voor één-aan-vele verhoudingen, moet u het relatiegebied in het schema bepalen dat &quot;velen&quot;vertegenwoordigt.

Als u een relatieveld wilt instellen, selecteert u het pijlpictogram (![Pictogram Pijl](../images/tutorials/relationship-b2b/arrow.png)) naast het desbetreffende veld op het canvas. In het geval van de [!DNL Opportunities] schema, dit is het `accountKey.sourceKey` omdat het doel is om een veel-op-één relatie met een account tot stand te brengen.

![Relatie-knop](../images/tutorials/relationship-b2b/relationship-button.png)

Er wordt een dialoogvenster weergegeven waarin u de details van de relatie kunt opgeven. Het relatietype wordt automatisch ingesteld op **[!UICONTROL Many-to-one]**.

![Relatiedialoog](../images/tutorials/relationship-b2b/relationship-dialog.png)

Onder **[!UICONTROL Reference Schema]**, gebruikt u de zoekbalk om de naam van het doelschema te zoeken. Wanneer u de naam van het doelschema markeert, wordt **[!UICONTROL Reference Identity Namespace]** wordt automatisch bijgewerkt naar de naamruimte van de primaire identiteit van het schema.

![Referentieschema](../images/tutorials/relationship-b2b/reference-schema.png)

Onder **[!UICONTROL Relationship Name From Current Schema]** en **[!UICONTROL Relationship Name From Reference Schema]** Geef vriendschappelijke namen voor de relatie op in de context van respectievelijk de bron- en bestemmingsschema&#39;s. Als u klaar bent, selecteert u **[!UICONTROL Save]** om de wijzigingen toe te passen en het schema op te slaan.

![Relatie naam](../images/tutorials/relationship-b2b/relationship-name.png)

Het canvas verschijnt weer, terwijl het relatieveld nu is gemarkeerd met de vriendelijke naam die u eerder hebt opgegeven. De relatienaam wordt ook vermeld onder de linkerspoorstaaf voor gemakkelijke verwijzing.

![Toegepaste relatie](../images/tutorials/relationship-b2b/relationship-applied.png)

Als u de structuur van het bestemmingsschema bekijkt, verschijnt de relatiemarkeerteken naast het primaire identiteitsveld van het schema en in de linkerspoorstaaf.

![Relatiemarkering bestemmingsschema](../images/tutorials/relationship-b2b/destination-relationship.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u met succes een vele-aan-één verhouding tussen twee schema&#39;s gecreeerd gebruikend [!DNL Schema Editor]. Zodra het gegeven is opgenomen gebruikend datasets die op deze schema&#39;s worden gebaseerd en dat het gegeven in de de gegevensopslag van het Profiel is geactiveerd, kunt u attributen van beide schema&#39;s voor multi-klassensegmenteringsgebruiksgevallen gebruiken. Raadpleeg de documentatie bij Real-time CDP B2B Edition voor meer informatie.
