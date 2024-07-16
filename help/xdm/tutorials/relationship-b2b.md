---
title: Een relatie definiëren tussen twee schema's in Real-time Customer Data Platform B2B Edition
description: Leer hoe u een vele-op-één relatie tussen twee schema's in Adobe Real-time Customer Data Platform B2B Edition definieert.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 0%

---

# Een veel-op-een relatie definiëren tussen twee schema&#39;s in Real-time Customer Data Platform B2B Edition {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="Referentieschema"
>abstract="Selecteer het schema u een verband met wilt vestigen. Afhankelijk van de klasse van het schema, kan het bestaande verhoudingen met andere entiteiten in de context B2B ook hebben. Zie de documentatie om te leren hoe de B2B schemaklassen op elkaar betrekking hebben."

De Uitgave van Adobe Real-time Customer Data Platform B2B verstrekt verscheidene klassen van de Gegevens van de Ervaring Model (XDM) die fundamentele B2B gegevensentiteiten, met inbegrip van [ rekeningen ](../classes/b2b/business-account.md) vangen, [ kansen ](../classes/b2b/business-opportunity.md), [ campagnes ](../classes/b2b/business-campaign.md), en meer. Door schema&#39;s te bouwen die op deze klassen worden gebaseerd en hen toe te laten voor gebruik in [ Real-Time Profiel van de Klant ](../../profile/home.md), kunt u gegevens van ongelijksoortige bronnen in een verenigde vertegenwoordiging samenvoegen genoemd een unieschema.

Unieschema&#39;s kunnen echter alleen velden bevatten die zijn vastgelegd door schema&#39;s die dezelfde klasse delen. Dit is waar schemaverhoudingen binnen komen. Door relaties in uw B2B-schema&#39;s uit te voeren, kunt u beschrijven hoe deze bedrijfsentiteiten met elkaar verband houden en kunt u kenmerken van meerdere klassen in downstreamgevallen van segmentatiegebruik opnemen.

Het volgende diagram verstrekt een voorbeeld van hoe de verschillende klassen B2B op elkaar in een basisimplementatie kunnen betrekking hebben:

![ B2B klassenverhoudingen ](../images/tutorials/relationship-b2b/classes.png)

Deze zelfstudie behandelt de stappen voor het definiëren van een vele-op-één relatie tussen twee schema&#39;s in Real-Time CDP B2B Edition.

>[!NOTE]
>
>Als u geen Real-time Customer Data Platform B2B Uitgave gebruikt of een één-aan-één verhouding wilt tot stand brengen, zie de gids op [ creërend een één-aan-één verhouding ](./relationship-ui.md) in plaats daarvan.
>
>Dit leerprogramma concentreert zich op hoe te om relaties tussen B2B- schema&#39;s in het Platform UI manueel te vestigen. Als u gegevens van een B2B bronverbinding brengt, kunt u een auto-generatienut gebruiken om de vereiste schema&#39;s, identiteiten, en verhoudingen in plaats daarvan tot stand te brengen. Zie de brondocumentatie op B2B namespaces en schema&#39;s voor meer informatie over [ gebruikend het auto-generatienut ](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL XDM System] en de Schema-editor in de gebruikersinterface van [!DNL Experience Platform] . Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [ XDM Systeem in Experience Platform ](../home.md): Een overzicht van XDM en zijn implementatie in [!DNL Experience Platform].
* [ Grondbeginselen van schemacompositie ](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [ creeer een schema gebruikend  [!DNL Schema Editor]](create-schema-ui.md): Een leerprogramma dat de grondbeginselen van behandelt om schema&#39;s in UI te bouwen en uit te geven.

## Een bron- en referentieschema definiëren

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Voor demonstratiedoeleinden, leidt dit leerprogramma tot een verband tussen bedrijfskansen (die in een &quot;[!DNL Opportunities]&quot;schema worden bepaald) en hun bijbehorende bedrijfsrekening (die in een &quot;[!DNL Accounts]&quot;schema wordt bepaald).

De verhoudingen van het schema worden vertegenwoordigd door een specifiek gebied binnen a **bronschema** dat verwijzingen het primaire identiteitsgebied van a **verwijzingsschema**. In de stappen die volgen, &quot;[!DNL Opportunities]&quot;dient als bronschema, terwijl &quot;[!DNL Accounts]&quot;als verwijzingsschema dienst doet.

### Inzicht in identiteiten in B2B-relaties

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Naamruimte van verwijzing"
>abstract="De naamruimte (type) voor het primaire identiteitsveld van het referentieschema. Het referentieschema moet een bestaand primair identiteitsveld hebben om aan een relatie te kunnen deelnemen. Raadpleeg de documentatie voor meer informatie over identiteiten in B2B-relaties."

Om een relatie tot stand te brengen, moet het referentieschema een gedefinieerde primaire identiteit hebben. Houd er bij het instellen van een primaire identiteit voor een B2B-entiteit rekening mee dat op tekenreeks gebaseerde entiteit-id&#39;s elkaar kunnen overlappen als u deze verzamelt op verschillende systemen of locaties, wat tot gegevensconflicten in Platform kan leiden.

Om dit te verklaren, bevatten alle standaardB2B klassen &quot;zeer belangrijke&quot;gebieden die met het [[!UICONTROL B2B Source] gegevenstype ](../data-types/b2b-source.md) in overeenstemming zijn. Dit gegevenstype verschaft velden voor een tekenreeks-id voor de B2B-entiteit, samen met andere contextuele informatie over de bron van de id. Een van deze velden, `sourceKey` , voegt de waarden van de andere velden in het gegevenstype samen om een geheel unieke id voor de entiteit te maken. Dit veld moet altijd worden gebruikt als de primaire identiteit voor B2B-entiteitsschema&#39;s.

![ sourceKey gebied ](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Wanneer [ plaatsend een XDM gebied als identiteit ](../ui/fields/identity.md), moet u een identiteit verstrekken namespace om de identiteit te bepalen onder. Dit kan een standaardnaamruimte zijn die door de Adobe wordt geboden of een aangepaste naamruimte die door uw organisatie wordt gedefinieerd. In de praktijk is de naamruimte gewoon een contextafhankelijke tekenreeks en kan deze worden ingesteld op elke gewenste waarde, mits deze voor uw organisatie van belang is voor het categoriseren van het identiteitstype. Zie het overzicht op [ identiteit namespaces ](../../identity-service/features/namespaces.md) voor meer informatie.

Voor verwijzingsdoeleinden, beschrijven de volgende secties de structuur van elk schema dat in dit leerprogramma wordt gebruikt alvorens een verhouding is bepaald. Let op waar de primaire identiteiten zijn gedefinieerd in de schemastructuur en de aangepaste naamruimten die ze gebruiken.

### [!DNL Opportunities] schema

Het bronschema &quot;[!DNL Opportunities]&quot; is gebaseerd op de [!UICONTROL XDM Business Opportunity] -klasse. Een van de velden die door de klasse, `opportunityKey`, wordt opgegeven, fungeert als id voor het schema. Het veld `sourceKey` onder het object `opportunityKey` wordt specifiek ingesteld als de primaire identiteit van het schema onder een aangepaste naamruimte met de naam [!DNL B2B Opportunity] .

Zoals u onder **[!UICONTROL Schema Properties]** ziet, is dit schema ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile] .

![ Schema van Kansen ](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

Het referentieschema &quot;[!DNL Accounts]&quot; is gebaseerd op de klasse [!UICONTROL XDM Account] . Het veld op hoofdniveau `accountKey` bevat de `sourceKey` die als primaire identiteit fungeert onder een aangepaste naamruimte met de naam [!DNL B2B Account] . Dit schema is ook ingeschakeld voor gebruik in Profiel.

![ het Schema van Rekeningen ](../images/tutorials/relationship-b2b/accounts.png)

## Een relatieveld definiëren voor het bronschema {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Relatienaam uit huidig schema"
>abstract="A label that describes the relationship from the current schema to the reference schema (example, &#39;Related Account&#39;). Dit label wordt gebruikt in Profiel en Segmentatie om context te geven aan gegevens van verwante B2B-entiteiten. Zie de documentatie om meer over het bouwen van B2B schemaverhoudingen te leren."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Relatienaam van referentieschema"
>abstract="A label that describes the relationship from the reference schema to the current schema (example, &#39;Related Opportunity&#39;). Dit label wordt gebruikt in Profiel en Segmentatie om context te geven aan gegevens van verwante B2B-entiteiten. Zie de documentatie om meer over het bouwen van B2B schemaverhoudingen te leren."

Om een verhouding tussen twee schema&#39;s te bepalen, moet het bronschema een specifiek gebied hebben dat op de primaire identiteit van het verwijzingsschema wijst. De standaard B2B-klassen omvatten specifieke bronsleutelvelden voor algemeen verwante bedrijfsentiteiten. Bijvoorbeeld, bevat de [!UICONTROL XDM Business Opportunity] klasse bronzeer belangrijke gebieden voor een verwante rekening (`accountKey`) en een verwante campagne (`campaignKey`). U kunt echter ook andere [!UICONTROL B2B Source] -velden aan het schema toevoegen door aangepaste veldgroepen te gebruiken als u meer dan de standaardcomponenten nodig hebt.

>[!NOTE]
>
>Momenteel, slechts kunnen vele-aan-één en één-aan-één verhoudingen van een bronschema aan een verwijzingsschema worden bepaald. Voor één-aan-vele verhoudingen, moet u het relatiegebied in het schema bepalen dat &quot;velen&quot;vertegenwoordigt.

Om een relatiegebied te plaatsen, selecteer het pijlpictogram (![ Pictogram van de Pijl ](../images/tutorials/relationship-b2b/arrow.png)) naast het gebied in kwestie binnen het canvas. In het geval van het [!DNL Opportunities] schema, is dit het `accountKey.sourceKey` gebied aangezien het doel een vele-aan-één verhouding met een rekening is te vestigen.

![ Knoop van de Verhouding ](../images/tutorials/relationship-b2b/relationship-button.png)

Er wordt een dialoogvenster weergegeven waarin u de details van de relatie kunt opgeven. Het relatietype wordt automatisch ingesteld op **[!UICONTROL Many-to-one]** .

![ de Dialoog van de Verhouding ](../images/tutorials/relationship-b2b/relationship-dialog.png)

Gebruik onder **[!UICONTROL Reference Schema]** de zoekbalk om de naam van het referentieschema te zoeken. Wanneer u de naam van het referentieschema markeert, wordt het veld **[!UICONTROL Reference Identity Namespace]** automatisch bijgewerkt naar de naamruimte van de primaire identiteit van het schema.

![ Schema van de Verwijzing ](../images/tutorials/relationship-b2b/reference-schema.png)

Geef onder **[!UICONTROL Relationship Name From Current Schema]** en **[!UICONTROL Relationship Name From Reference Schema]** vriendschappelijke namen op voor de relatie in de context van respectievelijk de bron- en referentieschema&#39;s. Als u klaar bent, selecteert u **[!UICONTROL Save]** om de wijzigingen toe te passen en het schema op te slaan.

![ Naam van de Verhouding ](../images/tutorials/relationship-b2b/relationship-name.png)

Het canvas verschijnt weer, terwijl het relatieveld nu is gemarkeerd met de vriendelijke naam die u eerder hebt opgegeven. De relatienaam wordt ook vermeld onder de linkerspoorstaaf voor gemakkelijke verwijzing.

![ Toegepaste Verhouding ](../images/tutorials/relationship-b2b/relationship-applied.png)

Als u de structuur van het verwijzingsschema bekijkt, verschijnt de relatiemarkeerteken naast het primaire identiteitsveld van het schema en in de linkerspoorstaaf.

![ de Teller van de Relatie van het Schema van de Bestemming ](../images/tutorials/relationship-b2b/destination-relationship.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een veel-op-één verhouding tussen twee schema&#39;s tot stand gebracht gebruikend [!DNL Schema Editor]. Zodra het gegeven gebruikend datasets is opgenomen die op deze schema&#39;s worden gebaseerd en dat het gegeven in de de gegevensopslag van het Profiel is geactiveerd, kunt u attributen van beide schema&#39;s voor [ multi-class gebruikscase van de segmentatie gebruiken ](../../rtcdp/segmentation/b2b.md).
