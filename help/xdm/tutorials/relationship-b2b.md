---
title: Definieer een relatie tussen twee schema's in Real-time Customer Data Platform B2B Edition
description: Leer hoe te om een vele-aan-één verhouding tussen twee schema's in Platform B2B van de Gegevens van de Klant in real time te bepalen .
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# Definieer een relatie tussen twee schema&#39;s in Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>Als u geen real-time Platform B2B van de Gegevens van de Klant gebruikt, zie de gids op [het creëren van een niet-B2B verhouding](./relationship-ui.md) in plaats daarvan.

Real-time Customer Data Platform B2B Edition biedt verschillende XDM-klassen (Experience Data Model) die essentiële B2B-gegevensentiteiten vastleggen, zoals [accounts](../classes/b2b/business-account.md), [Opportunity](../classes/b2b/business-opportunity.md), [campagnes](../classes/b2b/business-campaign.md) en meer. Door schema&#39;s te bouwen die op deze klassen worden gebaseerd en hen toe te laten voor gebruik in [Real-time Profiel van de Klant](../../profile/home.md), kunt u gegevens van ongelijksoortige bronnen in een verenigde vertegenwoordiging samenvoegen genoemd een unieschema.

Unieschema&#39;s kunnen echter alleen velden bevatten die zijn vastgelegd door schema&#39;s die dezelfde klasse delen. Hier komen schemarelaties binnen. Door relaties in uw B2B-schema&#39;s uit te voeren, kunt u beschrijven hoe deze bedrijfsentiteiten met elkaar verband houden en kunt u kenmerken van meerdere klassen in downstreamgevallen van segmentatiegebruik opnemen.

Het volgende diagram verstrekt een voorbeeld van hoe de verschillende klassen B2B op elkaar in een basisimplementatie kunnen betrekking hebben:

![B2B-klassenrelaties](../images/tutorials/relationship-b2b/classes.png)

Deze zelfstudie behandelt de stappen om een vele-aan-één verhouding tussen twee schema&#39;s in Echte - tijd CDP B2B Uitgave te bepalen.

>[!NOTE]
>
>Dit leerprogramma concentreert zich op hoe te om relaties tussen B2B- schema&#39;s in het Platform UI manueel te vestigen. Als u gegevens van een B2B bronverbinding brengt, kunt u een auto-generatienut gebruiken om de vereiste schema&#39;s, identiteiten, en verhoudingen in plaats daarvan tot stand te brengen. Zie de brondocumentatie op B2B namespaces en schema&#39;s voor meer informatie over [het gebruiken van het auto-generatienut](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL XDM System] en de Redacteur van het Schema in [!DNL Experience Platform] UI. Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [XDM-systeem in Experience Platform](../home.md): Een overzicht van XDM en zijn implementatie in  [!DNL Experience Platform].
* [Basisbeginselen van de schemacompositie](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [Maak een schema met het [!DNL Schema Editor]](create-schema-ui.md) volgende: Een zelfstudie waarin de grondbeginselen van het maken en bewerken van schema&#39;s in de gebruikersinterface worden besproken.

## Een bron- en doelschema definiëren

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Voor demonstratiedoeleinden, leidt dit leerprogramma tot een verband tussen bedrijfskansen (die in een &quot;[!DNL Opportunities]&quot;schema worden bepaald) en hun bijbehorende bedrijfsrekening (die in een &quot;[!DNL Accounts]&quot;schema wordt bepaald).

De verhoudingen van het schema worden vertegenwoordigd door een specifiek gebied binnen een **bronschema** dat verwijzingen het primaire identiteitsgebied van een **bestemmingsschema**. In de stappen die volgen, &quot;[!DNL Opportunities]&quot;dient als bronschema, terwijl &quot;[!DNL Accounts]&quot;als bestemmingsschema dienst doet.

### Inzicht in identiteiten in B2B-relaties

Om een relatie tot stand te brengen, moeten beide schema&#39;s primaire identiteiten hebben bepaald en voor [!DNL Real-time Customer Profile] worden toegelaten. Houd er bij het instellen van een primaire identiteit voor een B2B-entiteit rekening mee dat op tekenreeks gebaseerde entiteit-id&#39;s elkaar kunnen overlappen als u deze verzamelt op verschillende systemen of locaties, wat tot gegevensconflicten in Platform kan leiden.

Om dit te verklaren, bevatten alle standaardB2B klassen &quot;zeer belangrijke&quot;gebieden die aan het [[!UICONTROL B2B Source] gegevenstype ](../data-types/b2b-source.md) in overeenstemming zijn. Dit gegevenstype verschaft velden voor een tekenreeks-id voor de B2B-entiteit, samen met andere contextuele informatie over de bron van de id. Een van deze velden, `sourceKey`, voegt de waarden van de andere velden in het gegevenstype samen om een geheel unieke id voor de entiteit te produceren. Dit veld moet altijd worden gebruikt als de primaire identiteit voor B2B-entiteitsschema&#39;s.

![sourceKey, veld](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Wanneer [het plaatsen van een XDM gebied als identiteit](../ui/fields/identity.md), moet u een identiteitsnamespace verstrekken om de identiteit onder te bepalen. Dit kan een standaardnaamruimte zijn die door Adobe wordt geboden of een aangepaste naamruimte die door uw organisatie wordt gedefinieerd. In de praktijk is de naamruimte gewoon een contextafhankelijke tekenreeks en kan deze worden ingesteld op elke gewenste waarde, mits deze voor uw organisatie van belang is voor het categoriseren van het identiteitstype. Zie het overzicht op [identity namespaces](../../identity-service/namespaces.md) voor meer informatie.

Voor verwijzingsdoeleinden, beschrijven de volgende secties de structuur van elk schema dat in dit leerprogramma wordt gebruikt alvorens een verhouding is bepaald. Let op waar de primaire identiteiten zijn gedefinieerd in de schemastructuur en de aangepaste naamruimten die ze gebruiken.

### [!DNL Opportunities] schema

Het bronschema &quot;[!DNL Opportunities]&quot;is gebaseerd op de [!UICONTROL XDM Business Opportunity] klasse. Een van de velden die door de klasse worden opgegeven, `opportunityKey`, fungeert als id voor het schema. Het veld `sourceKey` onder het object `opportunityKey` wordt specifiek ingesteld als de primaire identiteit van het schema onder een aangepaste naamruimte met de naam [!DNL B2B Opportunity].
Zoals u onder **[!UICONTROL Schema Properties]** ziet, is dit schema ingeschakeld voor gebruik in [!DNL Real-time Customer Profile].

![Opportuniteitsschema](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

Het bestemmingsschema &quot;[!DNL Accounts]&quot;is gebaseerd op de [!UICONTROL XDM Account] klasse. Het veld op hoofdniveau `accountKey` bevat `sourceKey` dat als primaire identiteit fungeert onder een aangepaste naamruimte met de naam [!DNL B2B Account]. Dit schema is ook ingeschakeld voor gebruik in Profiel.

![Accounts-schema](../images/tutorials/relationship-b2b/accounts.png)

## Een relatieveld definiëren voor het bronschema {#relationship-field}

Om een verband tussen twee schema&#39;s te bepalen, moet het bronschema een specifiek gebied hebben dat verwijzingen de primaire identiteit van het bestemmingsschema. De standaard B2B-klassen omvatten specifieke bronsleutelvelden voor algemeen verwante bedrijfsentiteiten. De klasse [!UICONTROL XDM Business Opportunity] bevat bijvoorbeeld bronsleutelvelden voor een verwante account (`accountKey`) en een verwante campagne (`campaignKey`). U kunt echter ook andere [!UICONTROL B2B Source]-velden aan het schema toevoegen met behulp van aangepaste veldgroepen als u meer dan de standaardcomponenten nodig hebt.

>[!NOTE]
>
>Momenteel, slechts kunnen vele-aan-één verhoudingen van een bronschema aan een bestemmingsschema worden bepaald. Voor één-aan-vele verhoudingen, moet u het relatiegebied in het schema bepalen dat &quot;velen&quot;vertegenwoordigt.

Als u een relatieveld wilt instellen, selecteert u het pijlpictogram (![Pijlpictogram](../images/tutorials/relationship-b2b/arrow.png)) naast het desbetreffende veld binnen het canvas. In het geval van het [!DNL Opportunities] schema, is dit het `accountKey.sourceKey` gebied aangezien het doel een vele-aan-één verhouding met een rekening is te vestigen.

![Relatie-knop](../images/tutorials/relationship-b2b/relationship-button.png)

Er wordt een dialoogvenster weergegeven waarin u de details van de relatie kunt opgeven. Het relatietype wordt automatisch ingesteld op **[!UICONTROL Many-to-one]**.

![Relatiedialoog](../images/tutorials/relationship-b2b/relationship-dialog.png)

Onder **[!UICONTROL Reference Schema]**, gebruik de onderzoeksbar om de naam van het bestemmingsschema te vinden. Wanneer u de naam van het bestemmingsschema benadrukt, werkt het **[!UICONTROL Reference Identity Namespace]** gebied automatisch aan namespace van de primaire identiteit van het schema bij.

![Referentieschema](../images/tutorials/relationship-b2b/reference-schema.png)

Geef onder **[!UICONTROL Relationship Name From Current Schema]** en **[!UICONTROL Relationship Name From Reference Schema]** vriendschappelijke namen op voor de relatie in de context van respectievelijk de bron- en bestemmingsschema&#39;s. Als u klaar bent, selecteert u **[!UICONTROL Save]** om de wijzigingen toe te passen en het schema op te slaan.

![Relatie naam](../images/tutorials/relationship-b2b/relationship-name.png)

Het canvas verschijnt weer, terwijl het relatieveld nu is gemarkeerd met de vriendelijke naam die u eerder hebt opgegeven. De relatienaam wordt ook vermeld onder de linkerspoorstaaf voor gemakkelijke verwijzing.

![Toegepaste relatie](../images/tutorials/relationship-b2b/relationship-applied.png)

Als u de structuur van het bestemmingsschema bekijkt, verschijnt de relatiemarkeerteken naast het primaire identiteitsveld van het schema en in de linkerspoorstaaf.

![Relatiemarkering bestemmingsschema](../images/tutorials/relationship-b2b/destination-relationship.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een veel-aan-één verhouding tussen twee schema&#39;s tot stand gebracht gebruikend [!DNL Schema Editor]. Zodra het gegeven is opgenomen gebruikend datasets die op deze schema&#39;s worden gebaseerd en dat het gegeven in de de gegevensopslag van het Profiel is geactiveerd, kunt u attributen van beide schema&#39;s voor multi-klassensegmenteringsgebruiksgevallen gebruiken. Raadpleeg de documentatie bij Real-time CDP B2B Edition voor meer informatie.
