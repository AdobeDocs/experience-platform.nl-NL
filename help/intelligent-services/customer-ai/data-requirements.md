---
keywords: Experience Platform;aan de slag;klantenhulp;populaire onderwerpen;klanteninput;klanteninput;klantenoutput; gegevensvereisten
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Gegevensvereisten in AI van de Klant
topic-legacy: Getting started
description: Meer informatie over de vereiste gebeurtenissen, invoer en uitvoer die door de AI van de Klant worden gebruikt.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2538'
ht-degree: 0%

---


# Invoer en uitvoer in AI van de Klant

In het volgende document worden de verschillende vereiste gebeurtenissen, invoer en uitvoerbestanden beschreven die in de AI van de Klant worden gebruikt.

## Aan de slag {#getting-started}

Hier volgen de stappen voor het samenstellen van nevenmodellen en het identificeren van doelgroepen voor gepersonaliseerde marketing in Customer AI:

1. Gevallen van het gebruik van het overzicht: Hoe zouden de aandrijvingsmodellen helpen om doelpubliek voor gepersonaliseerde marketing te identificeren? Wat zijn mijn bedrijfsdoelstellingen en overeenkomstige tactieken om het doel te bereiken? Waar kan de propensiteitsmodellering in dit proces passen?

2. Prioriteit geven aan gebruiksgevallen: welke zijn de hoogste prioriteiten voor het bedrijf?

3. Bouw modellen in Klant AI: bekijk dit [ snelle leerprogramma ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html) en verwijs naar onze [ gids UI ](../customer-ai/user-guide/configure.md) voor een geleidelijke proces om een model te bouwen.

4. [ bouwt segmenten ](../customer-ai/user-guide/create-segment.md) gebruikend modelresultaten.

5. Voer gerichte bedrijfsacties uit die op deze segmenten worden gebaseerd. De resultaten controleren en de acties doorlopen om deze te verbeteren.

Hier zijn voorbeeldconfiguraties voor uw eerste model.  Het voorbeeldmodel, dat in dit document is ingebouwd, gebruikt een AI-model van de Klant om te voorspellen wie in de komende 30 dagen waarschijnlijk zal converteren voor een handelsbedrijf. De inputdataset is een dataset van Adobe Analytics.

| Stap | Definitie | Voorbeeld |
| ---- | ------ | ------- |
| Instellen | Geef basisinformatie over het model op. | **Naam**: Het model van de de koopsheid van het potlood <br> **ModelType**: Omzetting |
| Gegevens selecteren | Specificeer de datasets die worden gebruikt om het model te bouwen. | **Dataset**: dataset van Adobe Analytics <br> **Identiteit**: Verzeker de identiteitskolom voor elke dataset wordt geplaatst om een gemeenschappelijke identiteit te zijn. |
| Doel definiëren | Definieer het doel, de in aanmerking komende populatie, aangepaste gebeurtenissen en profielkenmerken. | **Voorspellingsdoel**: Uitgezochte `commerce.purchases.value` evenaart aan potlood <br> **venster van de Resultaat**: 30 dagen. |
| Opties instellen | Stel de planning voor het vernieuwen van het model in en schakel scores voor profiel in | **Programma**: Wekelijks <br> **laat voor profiel** toe: Dit moet voor de modeloutput worden toegelaten die in segmentatie moet worden gebruikt. |

## Overzicht van gegevens {#data-overview}

In de volgende secties wordt een overzicht gegeven van de verschillende vereiste gebeurtenissen, invoer en uitvoerbestanden die in de AI van de Klant worden gebruikt.

De AI van de klant werkt door de volgende datasets te analyseren om te voorspellen (wanneer een klant waarschijnlijk zal stoppen met het gebruik van het product) of de conversie (wanneer een klant waarschijnlijk een aankoop zal doen) eigenschapscores:

- De gegevens van Adobe Analytics die de [ bron van Analytics schakelaar ](../../sources/tutorials/ui/create/adobe-applications/analytics.md) gebruiken
- Adobe Audience Manager gegevens die de [ bronVerbinding van Audience Manager gebruiken ](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [ dataset van de Gebeurtenis van de Ervaring ](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [ de dataset van de Gebeurtenis van de Ervaring van de consument ](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

U kunt veelvoudige datasets van verschillende bronnen toevoegen als elk van de datasets het zelfde identiteitstype (namespace) zoals ECID deelt. Voor meer informatie bij het toevoegen van veelvoudige datasets, bezoek de [ AI gebruikersgids van de Klant ](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Source-connectors hebben tot vier weken nodig om back-ups te maken van gegevens. Als u onlangs opstelling een schakelaar plaatst, zou u moeten verifiëren dat de dataset de minimumlengte van gegevens heeft die voor AI van de Klant wordt vereist. Gelieve te herzien de [ historische gegevens ](#data-requirements) sectie om te verifiëren u genoeg gegevens voor uw vooruitgangsdoel hebt.

In de volgende tabel wordt een aantal gangbare terminologie beschreven die in dit document wordt gebruikt:

| Term | Definitie |
| --- | --- |
| [ Model van de Gegevens van de Ervaring (XDM) ](../../xdm/home.md) | XDM is het basiskader dat Adobe Experience Cloud, aangedreven door Adobe Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op het juiste moment te leveren. Experience Platform gebruikt XDM System om gegevens op een bepaalde manier te organiseren die het voor de diensten van Experience Platform gemakkelijker maken te gebruiken. |
| [ XDM Schema ](../../xdm/schema/composition.md) | Experience Platform gebruikt schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens. Voordat gegevens in Experience Platform kunnen worden ingevoerd, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. Schema&#39;s bestaan uit een basis-XDM-klasse en nul of meer schemaveldgroepen. |
| [ klasse XDM ](../../xdm/schema/field-constraints.md) | Alle XDM-schema&#39;s beschrijven gegevens die als `Experience Event` kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. De klassen XDM beschrijven het kleinste aantal eigenschappen een schema moet bevatten om een bepaald gegevensgedrag te vertegenwoordigen. |
| [Veldengroepen](../../xdm/schema/composition.md) | Een component die een of meer velden in een schema definieert. Veldgroepen dwingen af hoe hun velden worden weergegeven in de hiërarchie van het schema en tonen daarom in elk schema dezelfde structuur aan waarin ze zijn opgenomen. Veldgroepen zijn alleen compatibel met specifieke klassen, zoals bepaald door het kenmerk `meta:intendedToExtend` ervan. |
| [ Type van Gegevens ](../../xdm/schema/composition.md) | Een component die ook een of meer velden voor een schema kan bevatten. In tegenstelling tot veldgroepen worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn. De gegevenstypen die in dit document worden beschreven, worden ondersteund door zowel de CEE- als Adobe Analytics-schema&#39;s. |
| [ Real-time het Profiel van de Klant ](../../profile/home.md) | Klantprofiel in realtime biedt een gecentraliseerd consumentenprofiel voor gericht en gepersonaliseerd ervaringsbeheer. Elk profiel bevat gegevens die op alle systemen zijn geaggregeerd, en actioneerbare tijdstempelaccounts van gebeurtenissen waarbij de persoon is betrokken die hebben plaatsgevonden in een van de systemen die u met Experience Platform gebruikt. |

## Invoergegevens van AI van de klant {#customer-ai-input-data}

Voor inputdatasets, zoals Adobe Analytics en Adobe Audience Manager, wijzen de respectieve bronschakelaars direct de gebeurtenissen in deze standaardgebiedsgroepen (Commerce, Web, Toepassing, en Onderzoek) door gebrek tijdens het verbindingsproces in kaart. In de onderstaande tabel worden de gebeurtenisvelden weergegeven in de standaardveldgroepen voor Klanten-AI.

Voor meer informatie bij het in kaart brengen van de gegevens van Adobe Analytics of van Audience Manager, bezoek de het gebiedsafbeeldingen van Analytics of Audience Manager [ gebied in kaart brengen gids ](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

U kunt de Gebeurtenis van de Ervaring of de Gebeurtenis XDM schema&#39;s van de Ervaring voor inputdatasets gebruiken die niet via één van de bovengenoemde schakelaars worden bevolkt. Extra XDM gebiedsgroepen kunnen tijdens het proces van de schemaverwezenlijking worden toegevoegd. De veldgroepen kunnen door Adobe worden opgegeven, net als de standaardveldgroepen of een aangepaste veldgroep, die overeenkomt met de gegevensrepresentatie in de Experience Platform.

>[!IMPORTANT]
>
>U moet ervoor zorgen dat de gegevens in deze inputdatasets worden bevolkt. Als geen gebeurtenissen van standaardgebiedsgroepen in de inputdatasets worden gevonden, moet u douanegebeurtenissen tijdens het configuratiewerkschema toevoegen. Zie details over aangepaste gebeurtenissen.

### Door de AI van de Klant gebruikte standaardveldgroepen {#standard-events}

De Gebeurtenissen van de ervaring worden gebruikt om diverse klantengedrag te bepalen. Afhankelijk van de structuur van uw gegevens, omvatten de hieronder vermelde gebeurtenistypen mogelijk niet alle gedragingen van uw klant. Het is aan u om te bepalen welke gebieden de noodzakelijke gegevens hebben die nodig zijn om Web of andere kanaal-specifieke gebruikersactiviteit duidelijk en ondubbelzinnig te identificeren. Afhankelijk van uw voorspellingsdoel, kunnen de vereiste gebieden veranderen die nodig zijn.

>[!NOTE]
>
>Als u Adobe Analytics- of Adobe Audience Manager-gegevens gebruikt, wordt het schema automatisch gemaakt met de vereiste standaardgebeurtenissen die nodig zijn om uw gegevens vast te leggen. Als u uw eigen EE-schema maakt om gegevens vast te leggen, moet u overwegen welke veldgroepen nodig zijn om uw gegevens vast te leggen.

Klant-AI gebruikt standaard de gebeurtenissen in deze vier standaardveldgroepen: Commerce, Web, Application en Search. Het is niet nodig om voor elke gebeurtenis gegevens te hebben in de hieronder vermelde standaardveldgroepen, maar voor bepaalde scenario&#39;s zijn bepaalde gebeurtenissen vereist. Als u gebeurtenissen in de beschikbare standaardveldgroepen hebt, is het raadzaam deze op te nemen in uw schema. Als u bijvoorbeeld een AI-model van de klant wilt maken voor het voorspellen van aankoopgebeurtenissen, is het handig om gegevens te hebben van de veldgroepen Commerce en Webpagina details.

Als u een veldgroep wilt weergeven in de gebruikersinterface van Experience Platform, selecteert u de tab **[!UICONTROL Schemas]** in de linkertrack, gevolgd door de tab **[!UICONTROL Field groups]** .

| Veldgroep | Het type Event | XDM-veldpad |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | bestellen | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | uitchecken | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | aankopen | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Web Details] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL Application Details] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL Search Details] | zoeken | `search.keywords` |

Bovendien kan de AI van de Klant abonnementsgegevens gebruiken om betere modellen van de Koor te bouwen. Abonnementsgegevens zijn nodig voor elk profiel met de gegevensindeling [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md) . De meeste velden zijn echter optioneel voor een optimaal chroommodel. Het wordt echter ten zeerste aanbevolen gegevens op te geven voor zoveel mogelijk velden, zoals `startDate` , `endDate` en alle andere relevante details. Neem contact op met uw accountteam voor extra ondersteuning voor deze functie.

### Aangepaste gebeurtenissen en profielkenmerken toevoegen {#add-custom-events}

Als u informatie hebt u wenst om naast de standaard [ standaardgebeurtenisgebieden ](#standard-events) te omvatten die door Klant AI worden gebruikt, kunt u de [ configuratie van de douanegebeurtenis ](./user-guide/configure.md#custom-events) gebruiken om de gegevens te verhogen die door het model worden gebruikt.

#### Wanneer moet u aangepaste gebeurtenissen gebruiken?

De gebeurtenissen van de douane zijn noodzakelijk wanneer de datasets die in de stap van de datasetselectie worden gekozen *niets* van de standaardgebeurtenisgebieden bevatten die door Klant AI worden gebruikt. De AI van de Klant heeft informatie over minstens één gebeurtenis van het gebruikersgedrag buiten het resultaat nodig.

Aangepaste gebeurtenissen zijn handig voor:

- Het opnemen van domeinkennis of voorafgaande expertise in het model.

- De kwaliteit van het voorspellende model verbeteren.

- Meer inzichten en interpretaties verzamelen.

De beste kandidaten voor aangepaste gebeurtenissen zijn gegevens die domeinkennis bevatten die het resultaat kunnen voorspellen. Algemene voorbeelden van aangepaste gebeurtenissen zijn onder andere:

- Registreren voor account

- Abonneren op nieuwsbrief

- Maak een vraag aan de klantendienst

Hieronder volgt een selectie industriespecifieke voorbeelden van aangepaste gebeurtenissen:

| Industrie | Aangepaste gebeurtenissen |
| --- | --- |
| Detailhandel | In-store transactie <br> Teken omhoog voor de kaart van de club <br> de mobiele coupon van de Clip. |
| Entertainment | Schaf uw abonnement aan op <br> Stream video. |
| Ziekenhuis | Reservering voor restaurant maken <br> Aankooppunten. |
| Reizen | Informatie over bekende reizigers toevoegen Aankoopmijlen. |
| Communicatie | Plan upgraden/downgraden/annuleren. |

Aangepaste gebeurtenissen moeten door de gebruiker geïnitieerde acties vertegenwoordigen om te kunnen worden geselecteerd. Bijvoorbeeld, &quot;E-mail verzendt&quot;is een actie die door een teller en niet door de gebruiker in werking wordt gesteld, zodat zou het niet als douanegebeurtenis moeten worden gebruikt.

### Historische gegevens

Voor modeltraining zijn historische gegevens vereist. De vereiste duur voor het bestaan van gegevens binnen het systeem wordt bepaald door twee sleutelelementen: het resultaatvenster en de in aanmerking komende populatie.

Standaard zoekt de AI van de Klant naar een gebruiker die in de laatste 45 dagen activiteit heeft gehad als er geen definitie van de in aanmerking komende populatie is opgegeven tijdens de toepassingsconfiguratie. Daarnaast vereist de AI van de Klant minimaal 500 gekwalificeerde en 500 niet-kwalificerende gebeurtenissen (in totaal 1000) op basis van historische gegevens op basis van een voorspelde doeldefinitie.

In de volgende voorbeelden wordt het gebruik van een eenvoudige formule getoond waarmee u de minimale hoeveelheid vereiste gegevens kunt bepalen. Als u meer gegevens hebt dan minimaal vereist, levert uw model waarschijnlijk nauwkeurigere resultaten op. Als u minder dan het vereiste minimumbedrag hebt, zal het model ontbreken, aangezien er niet genoeg gegevens voor modelopleiding zijn.

De AI van de Klant gebruikt een overlevingsmodel om de waarschijnlijkheid te schatten van een gebeurtenis die op een bepaald ogenblik voorkomt en beïnvloedende factoren te identificeren, naast onder toezicht leren die positieve en negatieve populaties bepaalt, en op besluit-gebaseerde bomen zoals `lightgbm` om een kansscore te produceren.

**Formule**:

De minimaal vereiste gegevensduur in het systeem bepalen:

- De minimale gegevens die nodig zijn om functies te maken, zijn 30 dagen. Vergelijk het terugkijkvenster voor geschiktheid met 30 dagen:

   - Als het terugkijkvenster van de geschiktheid meer dan 30 dagen is, het gegevensvereiste = verkiesbaarheids terugkijkvenster + resultaatvenster.

   - Anders is de gegevensvereiste gelijk aan 30 dagen + resultaatvenster.

** Als er meer dan één voorwaarde is voor het bepalen van de in aanmerking komende populatie, is het terugkijkvenster van geschiktheid het langste.

>[!NOTE]
>
>30 is het minimumaantal dagen dat vereist is voor de in aanmerking komende bevolking. Als dit niet wordt verstrekt is het gebrek 45 dagen.

**Voorbeelden**:

- U wilt voorspellen of een klant waarschijnlijk in de komende 30 dagen een horloge zal kopen voor hen die één of andere Webactiviteit in de laatste 60 dagen hebben.

   - Geschiktheidsterugkijkvenster = 60 dagen

   - Outcome window = 30 dagen

   - Vereiste gegevens = 60 dagen + 30 dagen = 90 dagen

- U wilt voorspellen of de gebruiker waarschijnlijk een horloge in de volgende 7 dagen **zal kopen zonder** het verstrekken van een expliciete in aanmerking komende bevolking. In dit geval is de in aanmerking komende populatie standaard &quot;diegenen die de afgelopen 45 dagen actief zijn geweest&quot; en is het resultaatvenster 7 dagen.

   - Geschikt terugkijkvenster = 45 dagen

   - Outcome window = 7 dagen

   - Vereiste gegevens = 45 dagen + 7 dagen = 52 dagen

- U wilt voorspellen of de klant waarschijnlijk in de komende 7 dagen een horloge zal kopen voor hen die één of andere Webactiviteit in de laatste 7 dagen hebben.

   - Geschiktheidsterugkijkvenster = 7 dagen

   - Minimale gegevens die vereist zijn om functies te maken = 30 dagen

   - Outcome window = 7 dagen

   - Vereiste gegevens = 30 dagen + 7 dagen = 37 dagen

Hoewel de AI van de Klant een minimumperiode vereist om de gegevens binnen het systeem te bestaan, werkt het ook het best met recente gegevens. Door gebruik te maken van recentere gedragsgegevens zal de AI van de Klant waarschijnlijk een nauwkeurigere voorspelling geven van het toekomstige gedrag van een gebruiker.

## AI-uitvoergegevens van klant {#customer-ai-output-data}

De AI van de Klant produceert verscheidene attributen voor individuele profielen die als verkiesbaar worden beschouwd. Er zijn twee manieren om de score (output) te verbruiken op basis van wat u hebt voorzien. Als u een in real time Klantprofiel-Toegelaten dataset in real time hebt, kunt u inzichten van het Profiel van de Klant in real time in de [ Bouwer van het Segment ](../../segmentation/ui/segment-builder.md) verbruiken. Als u geen profiel-toegelaten dataset hebt, kunt u [ de output van de Klant AI ](./user-guide/download-scores.md) dataset downloaden beschikbaar op het gegevensmeer.

U kunt de outputdataset in de Experience Platform **** werkruimte van Datasets vinden {. Alle de outputdatasets beginnen van de Klant AI met de naam **Scores van de Klant - NAME_OF_APP**. Op dezelfde manier beginnen alle de outputschema&#39;s van AI van de Klant met het naam **Schema van de Klant AI - Name_of_app**.

![ Naam van de outputdatasets in Klant AI ](./images/user-guide/cai-schema-name-of-app.png)

In de onderstaande tabel worden de verschillende kenmerken beschreven die in de uitvoer van AI van de Klant zijn aangetroffen:

| Kenmerk | Beschrijving |
| ----- | ----------- |
| [!UICONTROL Score] | De relatieve waarschijnlijkheid voor een klant om het voorspelde doel binnen het bepaalde tijdkader te bereiken. Deze waarde moet niet worden beschouwd als een waarschijnlijkheidspercentage, maar veeleer als de waarschijnlijkheid dat een individu vergeleken wordt met de totale populatie. Deze score varieert van 0 tot 100. |
| Waardigheid | Deze eigenschap is de ware waarschijnlijkheid van een profiel voor het bereiken van het voorspelde doel binnen het bepaalde tijdkader. Bij het vergelijken van outputs over verschillende doelstellingen, wordt u geadviseerd om waarschijnlijkheid over percentiel of score te overwegen. Bij het bepalen van de gemiddelde waarschijnlijkheid in de in aanmerking komende populatie moet altijd rekening worden gehouden met de waarschijnlijkheid, aangezien de waarschijnlijkheid aan de onderkant ligt voor gebeurtenissen die niet vaak voorkomen. Waarden voor het waarschijnlijkheidsbereik tussen 0 en 1. |
| Percentage | Deze waarde biedt informatie over de prestaties van een profiel ten opzichte van andere profielen met een vergelijkbare score. Een profiel met een percentielrang van 99 voor churn geeft bijvoorbeeld aan dat het risico op churning groter is dan 99% van alle andere profielen die zijn gescaureerd. De percentielen variëren van 1 tot 100. |
| Het type Propensiteit | Het geselecteerde type buigzaamheid. |
| Score-datum | De datum waarop de scoring heeft plaatsgevonden. |
| Influentiële factoren | Dit zijn voorspelde redenen waarom een profiel waarschijnlijk zal omzetten of draaien. Deze factoren bestaan uit de volgende kenmerken:<ul><li>Code: het profiel of gedragskenmerk dat de voorspelde score van een profiel positief beïnvloedt. </li><li>Waarde: de waarde van het profiel of gedragskenmerk.</li><li>Belang: geeft het gewicht van het profiel of gedragskenmerk op de voorspelde score aan (laag, gemiddeld, hoog)</li></ul> |

## Volgende stappen {#next-steps}

Zodra u uw gegevens voorbereidt en ervoor zorgt dat al uw geloofsbrieven en schema&#39;s op zijn plaats zijn, verwijs naar [ vorm een gids van de Instantie van de Klant AI ](./user-guide/configure.md), die u door een geleidelijke leerprogramma loopt om een instantie van de Klant te creëren AI.