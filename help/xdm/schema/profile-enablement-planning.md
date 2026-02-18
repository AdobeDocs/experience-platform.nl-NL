---
keywords: Experience Platform;profiel;real-time klantprofiel;schema;dataset;planning;enablement
solution: Experience Platform
title: Planning voor de Inschakeling van het Profiel van de Klant in real time
description: Herzie de belangrijkste overwegingen u moet evalueren alvorens schema's en datasets voor het Profiel van de Klant in real time toe te laten.
source-git-commit: da40dfde57b17b6a7387451eec48569174ad544b
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Planning voor de Inschakeling van het Profiel van de Klant in real time

Gebruik deze pagina om te bevestigen dat uw schema en dataset klaar zijn alvorens u hen voor het Profiel van de Klant in real time toelaat. Voltooi deze planningscontrole nadat u uw schemagebieden ontwerpt maar alvorens u het schema voor Profiel toelaat. Met Profielactivering worden permanente gedragswijzigingen toegepast op uw gegevensmodel. U kunt schema-activering niet omkeren, en het toelaten van een dataset beïnvloedt hoe zijn verslagen binnen het Profiel van de Klant in real time worden verwerkt. Herzie deze richtlijn om onbedoelde enablement, kwesties van de gegevenskwaliteit, of beperkingen op lange termijn in uw schemaontwerp te vermijden.

Als u Profiel inschakelt, bepaalt u hoe uw gegevens in Experience Platform worden opgeslagen, samengevoegd en geactiveerd. De planning zorgt ervoor dat uw schemastructuur, identiteitsconfiguratie, en datasetdoel correct zijn alvorens u de verandering aanbrengt. Nadat u deze planningcontrole hebt voltooid, kunt u doorgaan met het inschakelen van gegevens voor Profiel in de gebruikersinterface van **[!UICONTROL Schema Editor]** of **[!UICONTROL Dataset]** .

## Vereisten

Controleer voordat u deze planningshandleiding gebruikt of:

* Een schema ontwerpen met de API voor het registreren van het schema **[!UICONTROL Schema Editor]** of het schema. Zie de [&#x200B; zelfstudie van de schemaverwezenlijking &#x200B;](../tutorials/create-schema-ui.md) beginnen.
* Er is ten minste één identiteitsveld geconfigureerd in uw schema. Herzie de [&#x200B; gids van de de configuratieconfiguratie van het identiteitsgebied &#x200B;](../ui/fields/identity.md) voor instructies.
* Het fundamentele begrip van [&#x200B; in real time het Profiel van de Klant &#x200B;](../../profile/home.md) en hoe het schema&#39;s gebruikt om verenigde klantenmeningen te bouwen.
* De aangewezen toestemmingen om schema&#39;s en datasets voor Profiel toe te laten. Neem contact op met de systeembeheerder als u geen toegang hebt tot de opties voor het inschakelen van profielen.

Als u deze eerste vereisten niet hebt voltooid, begin met het [&#x200B; leerprogramma van de schemaverwezenlijking &#x200B;](../tutorials/create-schema-ui.md) alvorens met deze planningsgids te werk te gaan.

## Waarom planning belangrijk is {#why-planning-matters}

Als u Profiel inschakelt, wordt de manier waarop Experience Platform met uw gegevens omgaat, permanent gewijzigd. De volgende permanente wijzigingen zijn van toepassing op schema&#39;s en datasets.

**Schema&#39;s**: Wanneer u een schema voor Profiel toelaat, kunt u niet het onbruikbaar maken of schrappen. U kunt velden ook niet uit het schema verwijderen of de naam ervan wijzigen nadat er gegevens zijn ingevoerd. Dit permanente betekent dat uw schemaontwerp volledig en stabiel moet zijn alvorens u Profiel toelaat, aangezien u niet de beslissing kunt omkeren of de structuur later vereenvoudigen.

**Datasets**: Wanneer u een dataset voor Profiel toelaat, gebruikt het Profiel van de Klant in real time zijn verslagen om profielen te bouwen en bij te werken. Herzie het gedrag van de datasetenactivering in de [&#x200B; gids van de datasetgebruiker &#x200B;](../../catalog/datasets/enable-for-profile.md). In tegenstelling tot schema&#39;s, kunt u de dataset later onbruikbaar maken of schrappen, maar het doen dit verwijdert bijbehorende profielverslagen en kan segmentatie of activeringswerkschema&#39;s beïnvloeden. Overweeg de stroomafwaartse invloed alvorens u veranderingen in een toegelaten dataset aanbrengt.

Omdat deze veranderingen stroomafwaartse processen beïnvloeden, verifieer dat een schema en zijn datasets voor Profiel aangewezen zijn alvorens u hen toelaat.

### De workflow voor inschakelen

U moet zowel het schema ALS de datasets toelaten die dat schema voor Profiel gebruiken. Bronnen in de volgende volgorde inschakelen:

1. **laat het schema voor Profiel** toe: laat eerst Profiel op het schema in **[!UICONTROL Schema Editor]** toe. Dit staat om het even welke dataset toe die dit schema gebruikt om voor Profiel worden toegelaten.
2. **laat individuele datasets voor Profiel** toe: Nadat het schema wordt toegelaten, laat Profiel op elke dataset toe die tot verenigde klantenprofielen zou moeten bijdragen.

U kunt geen dataset voor Profiel toelaten als zijn schema niet reeds wordt toegelaten. Het schema fungeert als een voorwaarde voor het inschakelen van gegevenssets. Dit proces in twee stappen zorgt ervoor dat uw gegevensmodel wordt gevalideerd voordat het Real-Time Klantprofiel met de verwerking van records begint.

## Wanneer moet u een schema of gegevensset voor profiel inschakelen {#when-to-enable}

Controleer de onderstaande criteria om te controleren of de functie Profiel geschikt is voor uw gegevens.

Profiel inschakelen in de volgende situaties:

* De gegevens dragen bij aan een verenigd klantprofiel.
* De gegevens zijn vereist voor segmentatie- of activeringsworkflows.
* Het schema omvat identiteitsgebieden die een persoon of een klant-vlakke sleutel vertegenwoordigen.
* De dataset bevat de Gebeurtenissen van de Ervaring of profielattributen die over kanalen moeten worden vastgemaakt. Herzie de [&#x200B; klasse XDM ExperienceEvent &#x200B;](../classes/experienceevent.md) om gebeurtenisvereisten te bevestigen.

## Wanneer niet om een schema of dataset voor Profiel toe te laten {#when-not-to-enable}

Schakel Profiel niet in de volgende gevallen in:

* Het schema vertegenwoordigt raadpleging of verwijzing-slechts gegevens.
* De gegevensset bevat test-, tijdelijke of niet-productiegegevens.
* De gegevens identificeren geen persoon of worden alleen gebruikt voor rapportage.
* Het schema is experimenteel of structureel onvolledig.

Als u Profiel in deze scenario&#39;s inschakelt, kunnen er onnodige profielen worden gemaakt, kan het licentiegebruik toenemen of kunnen schemabeperkingen op lange termijn worden geïntroduceerd.

## Belangrijkste overwegingen voordat u Profiel inschakelt {#key-considerations}

Herzie de overwegingen in deze sectie om ervoor te zorgen dat uw schema en dataset het gebruiksgevallen van het Profiel en gegevensbeheer op lange termijn steunen. Alvorens Profiel toe te laten, verifieer uw schemastructuur, identiteitsconfiguratie, en datasetdoel.

### Gereedheid van schema

Controleer de schemastructuur om te bevestigen dat het de vereisten van het Profiel steunt. Het schema moet de velden bevatten die vereist zijn voor segmentatie en activering, maar mag geen velden bevatten die experimenteel zijn of die niet op lange termijn nodig zijn. Herinner dat om het even welke extra gebieden u na enablement toevoegt additief moet zijn (zie [&#x200B; beperkingen van de schemasonutabiliteit &#x200B;](#why-planning-matters) voor details). Deze beperking betekent dat u de veldselectie zorgvuldig moet valideren voordat u Profiel inschakelt. Voor details op toegestane updates, zie de [&#x200B; regels van de schemaevolutie &#x200B;](./composition.md#evolution).

### Identiteitsconfiguratie

De configuratie van de identiteit bepaalt hoe het Profiel verslagen over datasets stitches. Begin door te bevestigen dat een geldige primaire identiteit wordt geselecteerd-dit gebied moet stabiel, uniek, en constant bevolkt over alle verslagen zijn. Controleer of naamruimten correct zijn toegewezen om stitching-fouten te voorkomen. Als u secundaire identiteiten gebruikt, bevestig dat zij uw gebruiksgevallen steunen zonder profielbotsingen te veroorzaken, die kunnen voorkomen wanneer de verschillende individuen de zelfde identiteitswaarde delen. In real time het Profiel van de Klant lost botsingen op door samenvoegbeleid toe te passen dat bepaalt welke gegevens belangrijkheid nemen wanneer het conflicteren verslagen samen worden vastgemaakt.

### Doel van gegevensset

Schakel een dataset alleen in voor Profiel wanneer deze rechtstreeks bijdraagt aan profielkenmerken of Experience Events die worden gebruikt in workflows die worden gedownload. Vermijd het inschakelen van gegevenssets die opzoekings- of referentiegegevens bevatten die niet worden gebruikt in segmentatie, test- of voorbeeldgegevens, of door het besturingssysteem gegenereerde records die niet zijn bedoeld voor activering. Deze gegevenstypen dragen niet bij aan uniforme klantprofielen en veroorzaken onnodige opslagoverhead. Als een dataset geen identiteitsgebieden of gegevens van het klantengedrag bevat die segmentatie en activering steunen, laat het niet voor Profiel toe.

**Voorbeeld**:

U schakelt een gegevensset &quot;Aankoopgebeurtenissen klant&quot; in die transactiegegevens met de id&#39;s van de klant bevat. In real time het Profiel van de Klant gebruikt deze gebeurtenissen om klantenchronologie te bouwen en segmentatie toe te laten die op aankoopgedrag wordt gebaseerd.

U laat GEEN dataset van de Catalogus van het &quot;Product toe&quot;die slechts de verwijzingsgegevens van SKU zonder klantenherkenningstekens bevat. Als u dit type gegevensset inschakelt, ontstaat onnodige opslagoverhead zonder dat u een bijdrage hoeft te leveren aan uniforme klantprofielen.

## Pre-enablement checklist {#pre-enablement-checklist}

Gebruik deze controlelijst om gereedheid te bevestigen voordat u een schema of dataset voor Profiel inschakelt. Voltooi elk item voordat u Profiel inschakelt.

### Controles op schemaniveau

Begin door te bevestigen dat uw schemaontwerp volledig en stabiel is. Controleer uw schema om te bevestigen dat alle vereiste gebieden voor uw gebruiksgeval aanwezig zijn en dat geen experimentele of tijdelijke gebieden inbegrepen zijn. Raadpleeg de [&#x200B; beste praktijken van het schemaontwerp &#x200B;](./best-practices.md) om uw schema te verzekeren volgt geadviseerde patronen. Verkrijg goedkeuring van uw team op de definitieve gebiedslijst (zie [&#x200B; beperkingen van de schemasonutabiliteit &#x200B;](#why-planning-matters)).

Controleer vervolgens of uw primaire identiteitsconfiguratie juist is. Open uw schema in **[!UICONTROL Schema Editor]** en bepaal de plaats van het gebied duidelijk met het identiteitspictogram. Controleer of dit veld consistent wordt ingevuld in de brongegevens en of de naamruimte van de identiteit geschikt is voor uw gebruik. De primaire identiteit moet stabiel en uniek zijn en moet in alle records op betrouwbare wijze worden weergegeven om ervoor te zorgen dat het profiel correct wordt gekoppeld.

Tot slot bevestig dat u niet de schemastructuur moet anders noemen of reorganiseren. De de structuurveranderingen van het schema zijn beperkt tot additieve slechts updates (zie [&#x200B; beperkingen van de schemasonutabiliteit &#x200B;](#why-planning-matters)). Om het even welke dubbelzinnigheid op lange termijn in het noemen of organisatie kan niet later worden verbeterd, zo los deze kwesties alvorens toe te laten op.

### Controles op gegevensniveau

Voor elke dataset wilt u toelaten, begin door te bevestigen dat het profiel-relevante gegevens bevat. Controleer steekproefverslagen om te verifiëren zij klant of gebeurtenisgegevens eerder dan zuiver operationele of verwijzingsinformatie bevatten. Zorg ervoor dat de verslagen identiteitswaarden omvatten die met klantenprofielen verbinden. Datasets zonder identiteitsvelden of gedragsgegevens van de klant moeten niet worden ingeschakeld voor Profiel.

Bepaal of de dataset aan identiteit het stitching of segmentatie zou moeten bijdragen door te begrijpen hoe zijn identiteitswaarden op andere datasets in uw profiel-toegelaten milieu betrekking hebben. Overweeg of de verslagen in deze dataset met bestaande profielen zouden moeten verbinden of nieuwe profielfragmenten tot stand brengen. Herzie de [&#x200B; documentatie van het samenvoegingsbeleid &#x200B;](../../profile/merge-policies/overview.md) om te begrijpen hoe het Profiel van de Klant in real time verslagen over datasets stitseert en hoe deze dataset in uw algemene identiteitsstrategie past.

Alvorens de dataset toe te laten, schat het aantal unieke identiteitswaarden het bevat en verifieer dat deze identiteitswaarden daadwerkelijke klanten eerder dan testrekeningen of systeemherkenningstekens vertegenwoordigen. Bevestig dat het toelaten van deze dataset zich op uw vergunningsrechten richt, aangezien elke unieke identiteit tot uw adresseerbare publiekstelling bijdraagt. Het toelaten van het profiel verhoogt opslag en verwerkingskosten, zodat verzekert de dataset waarde verstrekt die deze investering rechtvaardigt.

Als u deze checklist invult, voorkomt u problemen die na activering niet kunnen worden hersteld.

## Het toelaten van Profiel voor uw schema en dataset {#enable-profile}

Voer de volgende stappen uit nadat u de checklist voor pre-activering hebt voltooid om Profiel in te schakelen. Zoals verklaard in [&#x200B; Begrijpend het enablement werkschema &#x200B;](#why-planning-matters), moet u het schema toelaten alvorens u om het even welke datasets toelaat die dat schema gebruiken.

### Uw schema inschakelen voor profiel

Profiel eerst op uw schema inschakelen:

1. Navigeer naar **[!UICONTROL Schemas]** in de gebruikersinterface van Experience Platform.
2. Selecteer het schema in de lijst om het te openen in de **[!UICONTROL Schema Editor]** .
3. Selecteer de **[!UICONTROL Profile]** -schakeloptie in de rechtertrack. In het deelvenster Schema-eigenschappen wordt een bevestigingsvenster weergegeven.
4. Selecteer **[!UICONTROL Enable]** om te bevestigen. Het schema is nu ingeschakeld voor Profiel.

Voor gedetailleerde instructies, zie de [&#x200B; gids van het schema enablement &#x200B;](../ui/resources/schemas.md#profile) in de documentatie van de Redacteur van het Schema.

### Gegevenssets voor profiel inschakelen

Nadat uw schema voor Profiel wordt toegelaten, laat elke dataset toe die tot verenigde profielen zou moeten bijdragen:

1. Navigeer naar **[!UICONTROL Datasets]** in de gebruikersinterface van Experience Platform.
2. Selecteer een dataset van de lijst om de pagina van de datasetdetails te openen.
3. Selecteer de **[!UICONTROL Profile]** -schakeloptie in de rechtertrack. Het deelvenster Eigenschappen van de gegevensset wordt bijgewerkt om te tonen dat Profiel is ingeschakeld.

Herhaal dit proces voor elke dataset die tot het Profiel van de Klant in real time zou moeten bijdragen. Voor gedetailleerde instructies en opties van de API van enablement, verwijs naar de datasetgebruikersgids waarnaar in de sectie van Eerste vereisten wordt verwezen.

### Waarom ordenen belangrijk is

Zoals verklaard in [&#x200B; Begrijpend het enablement werkschema &#x200B;](#why-planning-matters), moet u het schema toelaten alvorens datasets toe te laten. Dit zorgt ervoor dat het Profiel van de Klant in real time de schemastructuur profielverrichtingen steunt alvorens dataset toe te staan toelaat toelaat, en dat alle datasets die het schema gebruiken de correcte gebiedsdefinities voor segmentatie en identiteit het stitching erven.

Nadat u zowel het schema als de datasets toelaat, begint het Profiel van de Klant in real time verwerkingsverslagen en bouwend verenigde klantenprofielen. Records die zijn ingevoerd voordat ze zijn ingeschakeld, worden niet opgenomen in profielen, tenzij u de gegevens opnieuw inneemt.

## Volgende stappen {#next-steps}

U hebt de permanente gevolgen van de activering van het Profiel herzien, bevestigd dat uw schema en datasets klaar zijn, en bevestigd dat uw identiteitsconfiguratie uw gebruiksgevallen steunt. Om uw begrip van schemastructuur en gebiedsverhoudingen te verdiepen, herzie de [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../schema/composition.md), die de regels van de schemaevolutie verklaart en hoe de gebieden binnen het gegevensmodel interactie aangaan. Als u kwesties tijdens of na enablement ontmoet, raadpleeg de [&#x200B; XDM het oplossen van problemengids &#x200B;](../troubleshooting-guide.md) voor gemeenschappelijke problemen en oplossingen. Meer over leren hoe identiteit namespaces profiel het stitching en resolutie beïnvloedt, herzie het [&#x200B; overzicht van Identiteitsnaamruimten &#x200B;](../../identity-service/features/namespaces.md).
