---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;enum;primaire identiteit;primaire identiteit;XDM individueel profiel;ExperienceEvent;XDM ExperienceEvent;ExperienceEvent;ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;schema ontwerp;best practices
solution: Experience Platform
title: Aanbevolen procedures voor gegevensmodellering
description: Dit document verstrekt een inleiding aan de schema's van het Gegevensmodel van de Ervaring (XDM) en de bouwstenen, de beginselen, en beste praktijken voor het samenstellen van schema's die in Adobe Experience Platform moeten worden gebruikt.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: fed8502afad1dfcb0b4dc91141dd621eacda720c
workflow-type: tm+mt
source-wordcount: '3214'
ht-degree: 0%

---

# Aanbevolen procedures voor gegevensmodellering

[!DNL Experience Data Model] (XDM) is het kernkader dat klantenervaringsgegevens door gemeenschappelijke structuren en definities voor gebruik in de stroomafwaartse diensten van Adobe Experience Platform te verstrekken gestandaardiseerd. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen en gebruikt om waardevolle inzichten van klantenacties te bereiken, klantenpubliek te bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden uit te drukken.

Aangezien XDM uiterst veelzijdig en aanpasbaar door ontwerp is, is het belangrijk om beste praktijken voor gegevensmodellering te volgen wanneer het ontwerpen van uw schema&#39;s. Dit document behandelt de belangrijkste besluiten en overwegingen die u moet maken wanneer het in kaart brengen van uw gegevens van de klantenervaring aan XDM.

## Aan de slag

Alvorens deze gids te lezen, herzie het [ XDM overzicht van het Systeem ](../home.md) voor een inleiding op hoog niveau aan XDM en zijn rol binnen Experience Platform.

Aangezien deze gids zich uitsluitend op zeer belangrijke overwegingen betreffende schemaontwerp concentreert, wordt u sterk geadviseerd om de [ grondbeginselen van schemacompositie ](./composition.md) voor gedetailleerde verklaringen van de individuele schemaelementen te lezen die door deze gids worden vermeld.

## Overzicht van best practices {#summary}

De aanbevolen aanpak voor het ontwerpen van uw gegevensmodel voor gebruik in Experience Platform kan als volgt worden samengevat:

1. Begrijp de zaken van het bedrijfsgebruik voor uw gegevens.
1. Identificeer de primaire gegevensbronnen die in [!DNL Platform] moeten worden gebracht om die gebruiksgevallen te behandelen.
1. Identificeer om het even welke secundaire gegevensbronnen die ook van belang kunnen zijn. Als momenteel bijvoorbeeld slechts één bedrijfseenheid in uw organisatie geïnteresseerd is in het verzenden van gegevens naar [!DNL Platform] , heeft een vergelijkbare bedrijfseenheid mogelijk ook belangstelling voor het verzenden van vergelijkbare gegevens in de toekomst. Het overwegen van deze secundaire bronnen helpt het gegevensmodel over uw volledige organisatie te standaardiseren.
1. Creeer een diagram van de entiteitverhouding op hoog niveau (ERD) voor de gegevensbronnen die zijn geïdentificeerd.
1. Zet de ERD op hoog niveau om in een [!DNL Platform] -centric ERD (inclusief profielen, Experience Events en lookup-entiteiten).

De stappen met betrekking tot het identificeren van de toepasselijke gegevensbronnen die worden vereist om uw zaken van het bedrijfsgebruik uit te voeren variëren van organisatie tot organisatie. Hoewel de overige secties in dit document zich richten op de laatste stappen voor het organiseren en samenstellen van een ERD nadat de gegevensbronnen zijn geïdentificeerd, kunnen de toelichtingen bij de verschillende componenten van het diagram u informeren over welke van uw gegevensbronnen naar [!DNL Platform] moeten worden gemigreerd.

## Een ERD op hoog niveau maken {#create-an-erd}

Zodra u de gegevensbronnen hebt bepaald die u in [!DNL Platform] wilt brengen, creeer een ERD op hoog niveau helpen het proces begeleiden om uw gegevens aan schema&#39;s toe te wijzen XDM.

In het onderstaande voorbeeld ziet u een vereenvoudigde ERD voor een bedrijf dat gegevens wil importeren in [!DNL Platform] . Het diagram benadrukt de essentiële entiteiten die in klassen XDM, met inbegrip van klantenrekeningen, hotels, adressen, en verscheidene gemeenschappelijke e-commercegebeurtenissen zouden moeten worden gesorteerd.

![ een entiteitrelationeel diagram dat de essentiële entiteiten benadrukt die in klassen XDM voor gegevensopname zouden moeten worden gesorteerd.](../images/best-practices/erd.png)

## Entiteiten sorteren in profiel-, zoekopdracht- en gebeurteniscategorieën {#sort-entities}

Nadat u een ERD hebt gemaakt om de essentiële entiteiten te identificeren die u in [!DNL Platform] wilt plaatsen, moeten deze entiteiten worden gesorteerd in profiel-, zoekopdracht- en gebeurteniscategorieën:

| Categorie | Beschrijving |
| --- | --- |
| Profielentiteiten | Profielentiteiten vertegenwoordigen kenmerken die betrekking hebben op een individuele persoon, doorgaans een klant. De entiteiten die onder deze categorie vallen zouden door schema&#39;s moeten worden vertegenwoordigd die op de **[!DNL XDM Individual Profile]klasse** worden gebaseerd. |
| Entiteiten opzoeken | Opzoekentiteiten zijn concepten die betrekking kunnen hebben op een individuele persoon, maar die niet rechtstreeks kunnen worden gebruikt om de persoon te identificeren. De entiteiten die onder deze categorie vallen zouden door schema&#39;s moeten worden vertegenwoordigd die op **worden gebaseerd douaneklassen**, en zijn verbonden met profielen en gebeurtenissen door [ schemaverhoudingen ](../tutorials/relationship-ui.md). |
| Gebeurtenisentiteiten | Gebeurtenisentiteiten vertegenwoordigen concepten met betrekking tot acties die een klant kan uitvoeren, systeemgebeurtenissen of andere concepten waarbij u wijzigingen in de loop van de tijd wilt bijhouden. De entiteiten die onder deze categorie vallen zouden door schema&#39;s moeten worden vertegenwoordigd die op de **[!DNL XDM ExperienceEvent]klasse** worden gebaseerd. |

{style="table-layout:auto"}

### Overwegingen bij het sorteren van entiteiten {#considerations}

In de volgende secties vindt u meer informatie over het sorteren van uw entiteiten in de bovenstaande categorieën.

#### Meerdere en onveranderlijke gegevens {#mutable-and-immutable-data}

Een primaire manier om te sorteren tussen entiteitscategorieën is of de gegevens die worden vastgelegd, veranderbaar zijn of niet.

Kenmerken die bij profielen of opzoekentiteiten horen, zijn doorgaans veranderbaar. De voorkeuren van een klant kunnen bijvoorbeeld in de loop der tijd veranderen en de parameters van een abonnementsplan kunnen afhankelijk van de markttendensen worden bijgewerkt.

Gebeurtenisgegevens zijn daarentegen doorgaans onveranderlijk. Aangezien gebeurtenissen aan een specifieke tijdstempel zijn gekoppeld, verandert de &quot;systeemmomentopname&quot; die een gebeurtenis biedt, niet. Een gebeurtenis kan bijvoorbeeld de voorkeuren van een klant vastleggen wanneer een klant een winkelwagentje uitcheckt en wordt niet gewijzigd, zelfs niet als de voorkeuren van de klant later veranderen. Gebeurtenisgegevens kunnen niet worden gewijzigd nadat deze zijn opgenomen.

Om samen te vatten, bevatten de profielen en de raadplegingsentiteiten veranderlijke attributen en vertegenwoordigen de recentste informatie over de onderwerpen zij vangen, terwijl de gebeurtenissen onveranderlijke verslagen van het systeem op een specifiek tijdstip zijn.

#### Klantkenmerken {#customer-attributes}

Als een entiteit kenmerken bevat die betrekking hebben op een individuele klant, is het zeer waarschijnlijk een profielentiteit. Voorbeelden van klantkenmerken zijn:

* Persoonlijke gegevens zoals naam, geboortedatum, geslacht en account-id(s).
* Locatiegegevens zoals adressen en GPS-gegevens.
* Contactgegevens zoals telefoonnummers en e-mailadressen.

#### Gegevens bijhouden over een bepaalde tijd {#track-data}

Als u wilt analyseren hoe bepaalde kenmerken binnen een entiteit in de loop der tijd veranderen, is het waarschijnlijk een gebeurtenisentiteit. Als u bijvoorbeeld productitems aan een winkelwagentje toevoegt, kunt u dit traceren als add-to-cart-gebeurtenissen in [!DNL Platform] :

| Klant-id | Type | Product-id | Aantal | Tijdstempel |
| --- | --- | --- | --- | --- |
| 1234567 | Toevoegen | 275098 | 2 | 1 okt. 10:32 |
| 1234567 | Verwijderen | 275098 | 1 | 1 okt. 10:33 |
| 1234567 | Toevoegen | 486502 | 1 | 1 okt. 10:41 |
| 1234567 | Toevoegen | 910482 | 5 | 3 okt. 14:15 |

{style="table-layout:auto"}

#### Gebruiksgevallen voor segmentatie {#segmentation-use-cases}

Wanneer het categoriseren van uw entiteiten, is het belangrijk om over het publiek te denken u kunt willen bouwen om uw bijzondere zaken van het bedrijfsgebruik te richten.

Een bedrijf wil bijvoorbeeld alle &quot;Gold&quot; of &quot;Platinum&quot; leden van zijn loyaliteitsprogramma kennen die het afgelopen jaar meer dan vijf aankopen hebben gedaan. Op basis van deze segmentatielogica kunnen de volgende conclusies worden getrokken met betrekking tot de wijze waarop relevante entiteiten moeten worden vertegenwoordigd:

* &quot;Goud&quot; en &quot;Platinum&quot; staan voor de status van loyaliteit die van toepassing is op een individuele klant. Aangezien de segmentatielogica slechts met de huidige loyaliteitsstatus van klanten betrekking heeft, kunnen deze gegevens als deel van een profielschema worden gemodelleerd. Als u veranderingen in loyaliteitsstatus in tijd wilt volgen, kon u een extra gebeurtenisschema voor de veranderingen van de loyaliteitsstatus ook tot stand brengen.
* Aankopen zijn gebeurtenissen die zich op een bepaald moment voordoen en de segmentatielogica heeft betrekking op aankoopgebeurtenissen binnen een opgegeven tijdvenster. Deze gegevens moeten daarom als een gebeurtenisschema worden gemodelleerd.

#### Gebruiksgevallen activeren {#activation-use-cases}

Naast overwegingen met betrekking tot gevallen van segmentatiegebruik, zou u ook de activeringsgebruiksgevallen voor die doelgroepen moeten herzien om extra relevante attributen te identificeren.

Een bedrijf heeft bijvoorbeeld een publiek gemaakt op basis van de regel die `country = US` bevat. Wanneer het bedrijf dat publiek vervolgens activeert naar bepaalde downstreamdoelen, wil het alle geëxporteerde profielen filteren op basis van de thuisstaat. Daarom moet een `state` -kenmerk ook worden vastgelegd in de toepasselijke profielentiteit.

#### Geaggregeerde waarden {#aggregated-values}

Op basis van het gebruiksgeval en de granulariteit van uw gegevens moet u bepalen of bepaalde waarden vooraf moeten worden geaggregeerd voordat ze in een profiel of gebeurtenisentiteit worden opgenomen.

Een bedrijf wil bijvoorbeeld een publiek maken op basis van het aantal winkels. U kunt ervoor kiezen deze gegevens op te nemen met de laagste granulariteit door elke aanschafgebeurtenis met een tijdstempel op te nemen als een eigen entiteit. Hierdoor kan het aantal opgenomen gebeurtenissen echter soms exponentieel toenemen. Om het aantal ingebedde gebeurtenissen te verminderen, kunt u verkiezen om tot een gezamenlijke waarde `numberOfPurchases` over een week lange of maandlange periode te leiden. Andere statistische functies zoals MIN en MAX kunnen ook op deze situaties van toepassing zijn.

>[!CAUTION]
>
>Experience Platform voert momenteel geen automatische waardecodering uit, hoewel dit voor toekomstige versies gepland is. Als u ervoor kiest geaggregeerde waarden te gebruiken, moet u de berekeningen extern uitvoeren voordat u de gegevens naar [!DNL Platform] verzendt.

#### Kardinaal {#cardinality}

De in uw ERD vastgestelde randvoorwaarden kunnen ook aanwijzingen geven over de manier waarop u uw entiteiten kunt indelen. Als er een een-op-veel relatie is tussen twee entiteiten, zal de entiteit die de &quot;velen&quot;vertegenwoordigt waarschijnlijk een gebeurtenisentiteit zijn. Er zijn echter ook gevallen waarin &quot;veel&quot; een set opzoekentiteiten is die als een array binnen een profielentiteit worden opgegeven.

>[!NOTE]
>
>Aangezien er geen universele aanpak bestaat om alle gevallen van gebruik te kunnen gebruiken, is het belangrijk om bij de indeling van entiteiten op basis van kardinaliteit rekening te houden met de voor- en nadelen van elke situatie. Zie de [ volgende sectie ](#pros-and-cons) voor meer informatie.

In de volgende tabel worden enkele gemeenschappelijke entiteitsrelaties en de categorieën beschreven die daaruit kunnen worden afgeleid:

| Relatie | Kardinaal | Categorieën entiteiten |
| --- | --- | --- |
| Klanten en winkelwagentjes | Eén naar vele | Eén klant kan veel winkelwagentjes hebben, dit zijn gebeurtenissen die in de loop der tijd kunnen worden bijgehouden. Klanten zouden daarom een profielentiteit zijn, terwijl winkelwagentjes een gebeurtenisentiteit zouden zijn. |
| Klanten en klantenaccounts | Eén op één | Één enkele klant kan slechts één loyaliteitsrekening hebben, en een loyaliteitsrekening kan slechts tot één klant behoren. Aangezien de relatie één-op-één is, vertegenwoordigen zowel Klanten als Loyalty&#39;s profielentiteiten. |
| Klanten en abonnementen | Eén naar vele | Eén klant kan vele abonnementen hebben. Aangezien het bedrijf slechts met de huidige abonnementen van een klant betrokken is, zijn de Klanten een profielentiteit, terwijl de Abonnementen een raadplegingsentiteit is. |

{style="table-layout:auto"}

### Pros en cons van verschillende entiteitsklassen {#pros-and-cons}

Hoewel het vorige gedeelte enkele algemene richtlijnen bevatte om te bepalen hoe u uw entiteiten kunt indelen, is het belangrijk te begrijpen dat er vaak voor- en nadelen zijn bij het kiezen van een categorie entiteiten in plaats van een andere categorie. In het volgende casestudy ziet u hoe u in deze situaties rekening kunt houden met uw opties.

Een bedrijf volgt actieve abonnementen voor hun klanten, waar één klant vele abonnementen kan hebben. Het bedrijf wil ook abonnementen voor segmentgebruiksgevallen, zoals het vinden van alle gebruikers met actieve abonnementen omvatten.

In dit scenario, heeft het bedrijf twee potentiële opties om de abonnementen van een klant in hun gegevensmodel te vertegenwoordigen:

1. [Profielkenmerken gebruiken](#profile-approach)
1. [Gebeurtenisentiteiten gebruiken](#event-approach)

#### Aanpak 1: Profielkenmerken gebruiken {#profile-approach}

De eerste benadering zou zijn om een array van abonnementen als attributen binnen de profielentiteit voor Klanten te omvatten. Objecten in deze array bevatten velden voor `category` , `status` , `planName` , `startDate` en `endDate` .

![ het schema van Klanten in de Redacteur van het Schema met de benadrukte klasse en structuur ](../images/best-practices/profile-schema.png)

**Pros**

* Segmentering is haalbaar voor het beoogde gebruik.
* In het schema blijven alleen de meest recente abonnementsrecords voor een klant behouden.

**Kons**

* De volledige array moet worden aangepast telkens wanneer er wijzigingen optreden in een veld in de array.
* Als verschillende gegevensbronnen of bedrijfseenheden gegevens in de array invoeren, wordt het lastig om de meest recente bijgewerkte array te synchroniseren over alle kanalen.

#### Aanpak 2: Gebeurtenisentiteiten gebruiken {#event-approach}

De tweede benadering zou gebeurtenisschema&#39;s moeten gebruiken om abonnementen te vertegenwoordigen. Dit betekent dat u dezelfde abonnementsvelden als de eerste aanpak moet invoeren, plus een abonnement-id, een klant-id en een tijdstempel van wanneer de abonnementsgebeurtenis heeft plaatsgevonden.

![ een diagram van het schema van de Gebeurtenissen van het Abonnement met de benadrukte klassen van de Gebeurtenis van de Ervaring XDM en abonnementenstructuur.](../images/best-practices/event-schema.png)

**Pros**

* De segmentatieregels kunnen flexibeler zijn (zoals het vinden van alle klanten die hun abonnementen in de laatste 30 dagen veranderden).
* Wanneer de abonnementsstatus van een klant verandert, hoeft u niet langer een lange, mogelijk complexe array bij te werken binnen de profielkenmerken van de klant. Dit is vooral nuttig als de gelijktijdige veranderingen in de abonnementenlijst van de klant van veelvoudige bronnen voorkomen.

**Kons**

* De segmentatie wordt complexer voor het originele voorgenomen gebruiksgeval (identificerend de status van de recentste abonnementen van klanten). Het publiek heeft nu extra logica nodig om de laatste abonnementsgebeurtenis voor een klant te markeren om zijn status te controleren.
* Gebeurtenissen hebben een hoger risico om automatisch te vervallen en te worden gewist uit de profielopslag. Zie de gids op [ Verlopen van de Gebeurtenis van de Ervaring ](../../profile/event-expirations.md) voor meer informatie.

## Schema&#39;s maken op basis van uw gecategoriseerde entiteiten {#schemas-for-categorized-entities}

Nadat u de entiteiten hebt gesorteerd in profiel-, opzoekfunctie- en gebeurteniscategorieën, kunt u beginnen met het omzetten van uw gegevensmodel in XDM-schema&#39;s. Voor demonstratiedoeleinden is het eerder getoonde model van voorbeeldgegevens in aangewezen categorieën in het volgende diagram gesorteerd:

![ A diagram van de schema&#39;s bevat in het profiel, de raadpleging, en gebeurtenisentiteiten ](../images/best-practices/erd-sorted.png)

De categorie waarop een entiteit is gesorteerd, moet de XDM-klasse bepalen waarop u het schema baseert. Herhaal dit:

* Profielentiteiten moeten de klasse [!DNL XDM Individual Profile] gebruiken.
* Gebeurtenisentiteiten moeten de klasse [!DNL XDM ExperienceEvent] gebruiken.
* Bij opzoeken moeten entiteiten aangepaste XDM-klassen gebruiken die door uw organisatie zijn gedefinieerd. Profiel- en gebeurtenisentiteiten kunnen dan via schemarelaties verwijzen naar deze opzoekentiteiten.

>[!NOTE]
>
>Hoewel gebeurtenisentiteiten bijna altijd worden vertegenwoordigd door afzonderlijke schema&#39;s, kunnen entiteiten in de profiel- of opzoekcategorieën worden gecombineerd in één XDM-schema, afhankelijk van hun kardinaliteit.
>
>Aangezien de entiteit Klanten bijvoorbeeld een één-op-één relatie heeft met de entiteit LoyaltyAccounts, kan het schema voor de entiteit Klanten ook een `LoyaltyAccount` -object bevatten dat de juiste loyaliteitsvelden voor elke klant bevat. Als de relatie echter één op vele is, kan de entiteit die de &quot;vele&quot;vertegenwoordigt door een afzonderlijk schema of een serie van profielattributen, afhankelijk van zijn ingewikkeldheid worden vertegenwoordigd.

De onderstaande secties bieden algemene richtlijnen voor het samenstellen van schema&#39;s op basis van uw ERD.

### Een iteratieve modelleringsaanpak hanteren {#iterative-modeling}

De [ regels van schemaevolutie ](./composition.md#evolution) dicteren dat slechts niet-destructieve veranderingen aan schema&#39;s kunnen worden aangebracht zodra zij zijn uitgevoerd. Met andere woorden, wanneer u een veld aan een schema toevoegt en er gegevens tegen dat veld zijn ingevoerd, kan het veld niet meer worden verwijderd. Daarom is het van essentieel belang om bij de eerste opzet van uw schema&#39;s een herhalende modelleringsaanpak te volgen, te beginnen met een vereenvoudigde implementatie die in de loop der tijd steeds complexer wordt.

Als u niet zeker bent of een bepaald gebied noodzakelijk is om in een schema te omvatten, is de beste praktijken het uit te sluiten. Als later wordt bepaald dat het veld nodig is, kan dit altijd worden toegevoegd in de volgende versie van het schema.

### Identiteitsvelden {#identity-fields}

In Experience Platform, worden de gebieden XDM duidelijk als identiteiten gebruikt om informatie over individuele klanten te verbinden die uit veelvoudige gegevensbronnen komen. Hoewel een schema meerdere velden kan hebben die zijn gemarkeerd als identiteiten, moet één primaire identiteit worden gedefinieerd om het schema in te schakelen voor gebruik in [!DNL Real-Time Customer Profile] . Zie de sectie op [ identiteitsgebieden ](./composition.md#identity) in de grondbeginselen van schemacompositie voor meer gedetailleerde informatie over het gebruiksgeval van deze gebieden.

Wanneer het ontwerpen van uw schema&#39;s, zijn om het even welke primaire sleutels in uw relationele gegevensbestandlijsten waarschijnlijk kandidaten voor primaire identiteiten. Andere voorbeelden van toepasselijke identiteitsgebieden zijn klant e-mailadressen, telefoonaantallen, rekening IDs, en [ ECID ](../../identity-service/features/ecid.md).

### Toepassingsschema-veldgroepen Adoben {#adobe-application-schema-field-groups}

Experience Platform verstrekt verscheidene uit-van-de-doos groepen van het XDM- schemagebied voor het vangen van gegevens met betrekking tot de volgende toepassingen van de Adobe:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

U kunt bijvoorbeeld de [[!UICONTROL Adobe Analytics ExperienceEvent Template] veldgroep ](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) gebruiken om [!DNL Analytics] -specifieke velden toe te wijzen aan uw XDM-schema&#39;s. Afhankelijk van de toepassingen van de Adobe u met werkt, zou u deze Adobe-Geleide gebiedsgroepen in uw schema&#39;s moeten gebruiken.

![ het schemadiagram van A van [!UICONTROL Adobe Analytics ExperienceEvent Template].](../images/best-practices/analytics-field-group.png)

Toepassingsveldgroepen Adoben wijzen automatisch een primaire standaardidentiteit toe via het gebruik van het veld `identityMap` . Dit is een door het systeem gegenereerd, alleen-lezen-object dat standaardidentiteitswaarden voor een individuele klant toewijst.

Voor Adobe Analytics is ECID de primaire standaardidentiteit. Als een klant geen ECID-waarde opgeeft, wordt de primaire identiteit standaard ingesteld op AID.

>[!IMPORTANT]
>
>Wanneer u veldgroepen van Adoben-toepassingen gebruikt, mogen geen andere velden worden gemarkeerd als de primaire identiteit. Als er extra eigenschappen zijn die als identiteiten moeten worden gemerkt, moeten deze gebieden in plaats daarvan als secundaire identiteiten worden toegewezen.

## Velden voor gegevensvalidatie {#data-validation-fields}

Wanneer u gegevens in het gegevenspeer opneemt, wordt de gegevensbevestiging slechts afgedwongen voor beperkte gebieden. Als u een bepaald veld tijdens een batch-opname wilt valideren, moet u het veld markeren als beperkt in het XDM-schema. Om te voorkomen dat slechte gegevens in Platform worden opgenomen, wordt u aangeraden de criteria voor validatie op veldniveau te definiëren wanneer u uw schema&#39;s maakt.

>[!IMPORTANT]
>
>Validatie geldt niet voor geneste kolommen. Als de veldindeling zich in een arraykolom bevindt, worden de gegevens niet gevalideerd.

Als u beperkingen voor een bepaald veld wilt instellen, selecteert u het veld in de Schema-editor om de zijbalk **[!UICONTROL Field properties]** te openen. Zie de documentatie op [ type-specifieke gebiedseigenschappen ](../ui/fields/overview.md#type-specific-properties) voor nauwkeurige beschrijvingen van de beschikbare gebieden.

![ de Redacteur van het Schema met de beperkingsgebieden die in [!UICONTROL Field properties] worden benadrukt sidebar.](../images/best-practices/data-validation-fields.png)

### Tips om de gegevensintegriteit te behouden {#data-integrity-tips}

Hieronder volgt een verzameling suggesties voor het behoud van gegevensintegriteit wanneer u een schema maakt.

* **overweeg primaire identiteiten**: Voor de producten van de Adobe zoals Web SDK, mobiele SDK, Adobe Analytics, en Adobe Journey Optimizer, dient het `identityMap` gebied vaak als primaire identiteit. Wijs geen extra velden aan als primaire identiteiten voor dat schema.
* **verzeker `_id` niet als identiteit** wordt gebruikt: Het `_id` gebied in de schema&#39;s van de Gebeurtenis van de Ervaring kan niet als identiteit worden gebruikt aangezien het voor verslaguniciteit wordt bedoeld.
* **vastgestelde lengtebeperkingen**: Het is beste praktijken om minimum en maximumlengten op gebieden te plaatsen duidelijk als identiteiten. Er wordt een waarschuwing weergegeven als u een aangepaste naamruimte wilt toewijzen aan een identiteitsveld zonder te voldoen aan de minimale en maximale lengte. Deze beperkingen helpen consistentie en gegevenskwaliteit te behouden.
* **pas patronen voor verenigbare waarden** toe: Als uw identiteitswaarden een specifiek patroon volgen, zou u **[!UICONTROL Pattern]** het plaatsen moeten gebruiken om deze beperking af te dwingen. Deze instelling kan regels bevatten zoals alleen cijfers, hoofdletters of kleine letters of specifieke tekencombinaties. Gebruik reguliere expressies die overeenkomen met patronen in de tekenreeksen.
* **Grenswaarden eVars in de schema&#39;s van Analytics**: Typisch, zou een schema Analytics slechts één eVar moeten hebben die als identiteit wordt aangewezen. Als u meer dan één eVar als identiteit wilt gebruiken, moet u controleren of de gegevensstructuur kan worden geoptimaliseerd.
* **verzekert uniciteit van een geselecteerd gebied**: Uw gekozen gebied zou uniek moeten zijn in vergelijking met de primaire identiteit in het schema. Als dit niet het geval is, merk het dan niet als een identiteit. Als bijvoorbeeld meerdere klanten hetzelfde e-mailadres kunnen opgeven, is die naamruimte geen geschikte identiteit. Dit beginsel is ook van toepassing op andere naamruimten zoals telefoonnummers. Als u een niet-uniek veld als een identiteit markeert, kan dit leiden tot het samenvouwen van het profiel.
* **verifieer minimumkoordlengten**: Alle koordgebieden zouden minstens één karakter in lengte moeten zijn, aangezien de koordwaarden nooit leeg zouden moeten zijn. Null-waarden voor niet-vereiste velden zijn echter acceptabel.

## Volgende stappen

In dit document worden de algemene richtlijnen en aanbevolen procedures voor het ontwerpen van uw gegevensmodel voor Experience Platform besproken. Samenvatten:

* Gebruik een top-down benadering door uw gegevenslijsten in profiel, raadpleging, en gebeurteniscategorieën te sorteren alvorens uw schema&#39;s te construeren.
* Er zijn vaak meerdere benaderingen en opties als het gaat om het ontwerpen van schema&#39;s voor verschillende doeleinden.
* Uw gegevensmodel zou uw zaken van het bedrijfsgebruik zoals segmentatie of de analyse van de klantenreis moeten steunen.
* Maak uw schema&#39;s zo eenvoudig mogelijk, en voeg slechts nieuwe gebieden toe wanneer absoluut noodzakelijk.

Zodra u klaar bent, zie het leerprogramma op [ creërend een schema in UI ](../tutorials/create-schema-ui.md) voor geleidelijke instructies op hoe te om een schema tot stand te brengen, wijs de aangewezen klasse voor de entiteit toe, en voeg gebieden toe om uw gegevens aan in kaart te brengen.
