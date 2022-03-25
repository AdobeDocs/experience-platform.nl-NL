---
keywords: Experience Platform;aan de slag;klantenhulp;populaire onderwerpen;input van klantenhulp;klantenoutput
solution: Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Invoer en uitvoer in AI van de Klant
topic-legacy: Getting started
description: Meer informatie over de vereiste gebeurtenissen, invoer en uitvoer die door de AI van de Klant worden gebruikt.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '3042'
ht-degree: 0%

---

# Invoer en uitvoer in AI van de Klant

In het volgende document worden de verschillende vereiste gebeurtenissen, invoer en uitvoerbestanden beschreven die in de AI van de Klant worden gebruikt.

## Aan de slag

De AI van de Klant werkt door één van de volgende datasets te analyseren om de scores van de kromme of van de omzettingsdichtheid te voorspellen:

- Adobe Analytics-gegevens gebruiken de [Bronconnector voor analyse](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager-gegevens gebruiken de [Audience Manager-bronaansluiting](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- Gegevensset Experience Event (EE)
- Gegevensset met consumentenervaringen (CEE)

U kunt veelvoudige datasets van verschillende bronnen toevoegen als elk van de datasets het zelfde identiteitstype (namespace) zoals ECID deelt. Voor meer informatie bij het toevoegen van veelvoudige datasets, bezoek [Handleiding voor AI-gebruikers van klant](./user-guide/configure.md#select-data)

>[!IMPORTANT]
>
>De bronschakelaars nemen tot vier weken aan backfill gegevens in beslag. Als u onlangs opstelling een schakelaar plaatst, zou u moeten verifiëren dat de dataset de minimumlengte van gegevens heeft die voor AI van de Klant wordt vereist. Controleer de [historische gegevens](#data-requirements) om te verifiëren u genoeg gegevens voor uw vooruitgangsdoel hebt.

Voor dit document is basiskennis van het CEE-schema vereist. Controleer de [Intelligente services voor het verzamelen van gegevens](../data-preparation.md) documentatie voordat u verdergaat.

In de volgende tabel wordt een aantal gangbare terminologie beschreven die in dit document wordt gebruikt:

| Term | Definitie |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | XDM is het basiskader dat Adobe Experience Cloud, aangedreven door Adobe Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op het juiste moment te leveren. De methodologie waarop het Experience Platform wordt gebouwd, het Systeem van XDM, stelt de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform in werking. |
| XDM-schema | Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens. Voordat gegevens in Platform kunnen worden opgenomen, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. Schema&#39;s bestaan uit een basis-XDM-klasse en nul of meer schemaveldgroepen. |
| XDM-klasse | Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. De klassen XDM beschrijven het kleinste aantal eigenschappen een schema moet bevatten om een bepaald gegevensgedrag te vertegenwoordigen. |
| [Veldengroepen](../../xdm/schema/composition.md) | Een component die een of meer velden in een schema definieert. Veldgroepen dwingen af hoe hun velden worden weergegeven in de hiërarchie van het schema en tonen daarom in elk schema dezelfde structuur aan waarin ze zijn opgenomen. Veldgroepen zijn alleen compatibel met specifieke klassen, zoals bepaald door hun `meta:intendedToExtend` kenmerk. |
| [Gegevenstype](../../xdm/schema/composition.md) | Een component die ook een of meer velden voor een schema kan bevatten. In tegenstelling tot veldgroepen worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn. De gegevenstypen die in dit document worden beschreven, worden ondersteund door zowel de CEE- als Adobe Analytics-schema&#39;s. |
| Churn | Een meting van het percentage accounts dat de abonnementen annuleert of niet vernieuwt. Een hoge wisselkoers kan een negatief effect hebben op de maandelijkse terugkerende inkomsten (MRR) en kan ook wijzen op ontevredenheid over een product of dienst. |
| [Klantprofiel in realtime](../../profile/home.md) | Klantprofiel in realtime biedt een gecentraliseerd consumentenprofiel voor gericht en gepersonaliseerd ervaringsbeheer. Elk profiel bevat gegevens die op alle systemen zijn geaggregeerd, en actioneerbare tijdstempelaccounts van gebeurtenissen waarbij de persoon is betrokken die hebben plaatsgevonden in een van de systemen die u met Experience Platform gebruikt. |

## Invoergegevens van AI van de klant

>[!TIP]
>
> De AI van de Klant bepaalt automatisch welke gebeurtenissen nuttig voor voorspellingen zijn en roept een waarschuwing op als de beschikbare gegevens niet voldoende zijn om kwaliteitsvoorspellingen te produceren.

AI van de Klant steunt de datasets van Adobe Analytics, Adobe Audience Manager, van de Gebeurtenis van de Ervaring (EE), en van de Ervaring van de Consumenten (CEE). Het CEE-schema vereist dat u tijdens het maken van het schema veldgroepen toevoegt. Als u de datasets van Adobe Analytics of van Adobe Audience Manager gebruikt, brengt de bronschakelaar direct de standaardgebeurtenissen (Handel, de details van de Web-pagina, Toepassing, en Onderzoek) in kaart die hieronder tijdens het verbindingsproces worden vermeld. You can add multiple datasets from different sources if each of the datasets shares the same identity type (namespace) such as an ECID.

Ga voor meer informatie over het koppelen van Adobe Analytics-gegevens of Audience Manager-gegevens naar de [Toewijzingen van analytische velden](../../sources/connectors/adobe-applications/analytics.md) of [Veldtoewijzingen Audience Manager](../../sources/connectors/adobe-applications/mapping/audience-manager.md) hulplijn.

### Standard events used by Customer AI {#standard-events}

De Gebeurtenissen van de Ervaring XDM worden gebruikt voor het bepalen van diverse klantengedrag. Depending on how your data is structured, the event types listed below may not encompass all of your customer&#39;s behaviors. It is up to you to determine what fields have the necessary data that is needed to clearly and unambiguously identify web user activity. Depending on your prediction goal, the required fields that are needed can change.

De AI van de klant is afhankelijk van verschillende gebeurtenistypen voor de eigenschappen van het bouwmodel. Deze gebeurtenistypen worden automatisch aan uw schema toegevoegd gebruikend veelvoudige XDM gebiedsgroepen.

>[!NOTE]
>
>Als u Adobe Analytics- of Adobe Audience Manager-gegevens gebruikt, wordt het schema automatisch gemaakt met de vereiste standaardgebeurtenissen die nodig zijn om uw gegevens vast te leggen. If you are creating your own custom CEE schema to capture data, you need to consider what field groups are needed to capture your data.

Het is niet nodig gegevens te hebben voor elk van de hieronder vermelde standaardgebeurtenissen, maar voor bepaalde scenario&#39;s zijn bepaalde gebeurtenissen vereist. Als u standaardgebeurtenisgegevens hebt, is het raadzaam deze op te nemen in uw schema. Als u bijvoorbeeld een AI-toepassing van de Klant wilt maken om aankoopgebeurtenissen te voorspellen, is het handig om gegevens van de `Commerce` en `Web page details` gegevenstypen.

Als u een veldgroep wilt weergeven in de gebruikersinterface van het Platform, selecteert u de optie **[!UICONTROL Schemas]** op de linkerspoorstaaf, gevolgd door het selecteren van **[!UICONTROL Field groups]** tab.

| Veldgroep | Het type Event | XDM field path |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | order | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | kassa | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | aankopen | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web Details] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Application Details] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Search Details] | zoeken | search.keywords |

Bovendien kan de AI van de Klant abonnementsgegevens gebruiken om betere modellen van de Koor te bouwen. Subscription data is needed for each profile using the [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md) data type format. De meeste velden zijn optioneel, maar voor een optimaal chroommodel is het zeer raadzaam gegevens te verstrekken voor zoveel mogelijk velden, zoals: `startDate`, `endDate`en alle andere relevante gegevens.

### Aangepaste gebeurtenissen en profielkenmerken toevoegen

Als u over informatie beschikt die u in aanvulling op de [standaardgebeurtenisvelden](#standard-events) wordt gebruikt door de AI van de Klant, wordt een aangepaste gebeurtenis en een optie van het douaneprofielattribuut verstrekt tijdens uw [instantieconfiguratie](./user-guide/configure.md#custom-events).

If the dataset you selected includes custom events or profile attributes such as a &quot;hotel reservation&quot; or &quot;employee of X company&quot; defined in your schema, you can add them to your instance. These additional custom events and profile attributes are used by Customer AI to improve the quality of your model and provide more accurate results.

### Historische gegevens {#data-requirements}

Klanten-AI hebben historische gegevens nodig voor modeltraining, maar de hoeveelheid vereiste gegevens is gebaseerd op twee sleutelelementen: resultaatvenster en in aanmerking komende populatie.

By default, Customer AI looks for a user to have had activity in the last 120 days if no eligible population definition is provided during the application configuration. Additionally, Customer AI requires a minimum of 500 qualifying and 500 non-qualifying events (1000 total) of historical data based on a predicted goal definition.

The following examples provided use a simple formula to help you determine the minimum amount of data required. Als u meer dan de minimumvereiste hebt, zal uw model waarschijnlijk nauwkeurigere resultaten verstrekken. Als u minder dan het vereiste minimumbedrag hebt, zal het model ontbreken aangezien er geen voldoende hoeveelheid gegevens voor modelopleiding is.

**Formule**:

Minimumlengte van de vereiste gegevens = subsidiabele populatie + resultaatvenster

>[!NOTE]
>
> 30 is het minimumaantal dagen dat vereist is voor de in aanmerking komende bevolking. If this is not provided the default is 120 days.

Voorbeelden:

- U wilt voorspellen of een klant waarschijnlijk een horloge in de komende 30 dagen zal kopen. U wilt ook gebruikers scoren die de afgelopen 60 dagen enige internetactiviteit hebben gehad. In dat geval is de minimumlengte van de vereiste gegevens 60 dagen + 30 dagen. De in aanmerking komende populatie is 60 dagen en het resultaatvenster is 30 dagen in totaal 90 dagen.

- U wilt voorspellen of de gebruiker waarschijnlijk de komende 7 dagen een horloge zal kopen. In dit geval is de minimumlengte van de vereiste gegevens 120 dagen + 7 dagen. De in aanmerking komende populatie staat standaard op 120 dagen en het resultaatvenster is 7 dagen in totaal 127 dagen.

- U wilt voorspellen of de klant waarschijnlijk de komende 7 dagen een horloge zal kopen. U wilt ook gebruikers scoren die de afgelopen 7 dagen enige internetactiviteit hebben gehad. In dat geval is de minimumlengte van de vereiste gegevens 30 dagen + 7 dagen. De in aanmerking komende populatie duurt minimaal 30 dagen en de resultaatperiode bedraagt 7 dagen in totaal 37 dagen.

Naast de minimaal vereiste gegevens, werkt de AI van de Klant ook het best met recente gegevens. In dit geval doet de AI van de Klant een prognose voor de toekomst op basis van recente gedragsgegevens van een gebruiker. Met andere woorden, recentere gegevens zullen waarschijnlijk een nauwkeurigere voorspelling opleveren.

### Voorbeeldscenario&#39;s

In deze sectie worden verschillende scenario&#39;s voor exemplaren van AI van de Klant beschreven evenals de vereiste en geadviseerde gebeurtenistypen. Zie de [tabel met standaardgebeurtenissen](#standard-events) voor meer informatie over de veldgroep en het veldpad.

>[!NOTE]
>
> De vereiste gebeurtenistypen worden gebruikt om Webgebruikersactiviteit duidelijk en ondubbelzinnig te identificeren. Het aantal vereiste gebeurtenistypen wordt gewijzigd op basis van het voorspellingsdoel en de structuur van uw schema. Als u niet zeker bent dat een bepaald gebeurtenistype nodig is, wordt geadviseerd om dat gebeurtenistype te omvatten terwijl het bouwen van uw CEE schema. Als u Adobe Analytics- of Adobe Audience Manager-gegevens gebruikt, moeten de vereiste standaardgebeurtenissen beschikbaar zijn, afhankelijk van de gegevens die u streamt.

### Scenario 1: Aankoop van conversie op een e-commercewebsite

**Voorspeldoel:** Verwacht dat de profielen die hiervoor in aanmerking komen, een bepaald kledingartikel op een website kunnen kopen.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- bestellen
- kassa
- aankopen
- webVisit
- zoeken

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw Customer AI-exemplaar. Als de gegevens beschikbaar zijn voor een bepaald gegevenstype, wordt aangeraden dat deze gegevens in het schema worden opgenomen.

### Scenario 2: Abonnementsconversie op een website van de mediastreamingservice

**Voorspeldoel:** Verwacht dat de conversiegevoeligheid van de abonnementen ertoe leidt dat de in aanmerking komende profielen zich vastleggen op een bepaald abonnementsniveau, zoals een standaard- of premieplan.

**Required standard event types:**

The event types listed below are required for an optimal Customer AI output with this particular prediction goal. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- order
- checkouts
- aankopen
- webVisit
- search

In this example, `order`, `checkouts`, and `purchases` are used to indicate that a subscription was purchased and its type.

Voor een accuraat model wordt bovendien aangeraden om een aantal van de beschikbare eigenschappen in het dialoogvenster [gegevenstype abonnement](../../xdm/data-types/subscription.md).

**Additional recommended standard event types:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw Customer AI-exemplaar. It is recommended that if the data is available for a particular data type, that this data is included in your schema.

### Scenario 3: Churn op een e-commercewebsite

**Prediction goal:** Predict the likelihood that a purchase event will not occur.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. It is possible to exclude a required event depending on your prediction goal, however, excluding multiple events can lead to poor results.

- order
- checkouts
- aankopen
- webVisit
- search

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw Customer AI-exemplaar. It is recommended that if the data is available for a particular data type, that this data is included in your schema.

### Scenario 4: Upsell conversion on an e-commerce retail website

**Voorspeldoel:** Verwacht de koopkracht van de populatie die een specifiek product heeft gekocht om een nieuw verwant product te kopen.

**Required standard event types:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- bestellen
- kassa
- aankopen
- webVisit
- zoeken

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw Customer AI-exemplaar. Als de gegevens beschikbaar zijn voor een bepaald gegevenstype, wordt aangeraden dat deze gegevens in het schema worden opgenomen.

### Scenario 5: Abonnement (churn) op een online nieuwszender opzeggen

**Voorspeldoel:** Verwacht wordt dat de in aanmerking komende bevolking geneigd is om volgende maand af te zien van een dienst.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- webVisit
- zoeken

Voor een accuraat model wordt bovendien aangeraden om een aantal van de beschikbare eigenschappen in het dialoogvenster [gegevenstype abonnement](../../xdm/data-types/subscription.md).

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw Customer AI-exemplaar. Als de gegevens beschikbaar zijn voor een bepaald gegevenstype, wordt aangeraden dat deze gegevens in het schema worden opgenomen.

### Scenario 6: Mobiele toepassing starten

**Voorspeldoel:** Verwacht de neiging van in aanmerking komende profielen om een betaalde mobiele toepassing in de volgende X dagen te lanceren. Dit is vergelijkbaar met het voorspellen van de KPI (Key Performance Indicator) van &quot;Maandelijkse Actieve Gebruikers&quot;.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. It is possible to exclude a required event depending on your prediction goal, however, excluding multiple events can lead to poor results.

- order
- kassa
- purchases
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

In this example, `order`, `checkouts`, and `purchases` are used when a mobile application needs to be  purchased.

**Additional recommended standard event types:**

Any of the remaining [event types](#standard-events) may be required based on the complexity of your goal and eligible population while configuring your Customer AI instance. It is recommended that if the data is available for a particular data type, that this data is included in your schema.

### Scenario 7: Traits realized (Adobe Audience Manager)

**Voorspeldoel:** Verwacht de neiging om sommige eigenschappen te verwezenlijken.

**Vereiste standaardgebeurtenistypen:**

Als u kenmerken van Adobe Audience Manager wilt gebruiken, moet u een bronverbinding maken met de [Audience Manager-bronaansluiting](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). The source connector automatically creates the schema with the proper field group(s). U hoeft niet handmatig extra gebeurtenistypen toe te voegen om het schema te laten werken met Customer AI.

Wanneer u een nieuwe klant-AI-instantie configureert, `audienceName` en `audienceID` U kunt een bepaalde eigenschap selecteren om te scoren terwijl u uw doel definieert.

## AI-uitvoergegevens van klant

De AI van de Klant produceert verscheidene attributen voor individuele profielen die als verkiesbaar worden beschouwd. Er zijn twee manieren om de score (output) te verbruiken op basis van wat u hebt voorzien. If you have a Real-time Customer Profile-enabled dataset, you can consume insights from Real-time Customer Profile in the [Segment Builder](../../segmentation/ui/segment-builder.md). Als u geen profiel-Toegelaten dataset hebt, kunt u [De AI-uitvoer van de klant downloaden](./user-guide/download-scores.md) dataset beschikbaar op het data Lake.

>[!NOTE]
>
> De waarden van de output worden verbruikt door het Profiel van de Klant in real time dat kan worden gebruikt om segmenten tot stand te brengen en te bepalen.

In de onderstaande tabel worden de verschillende kenmerken beschreven die in de uitvoer van AI van de Klant zijn aangetroffen:

| Kenmerk | Beschrijving |
| ----- | ----------- |
| Score | De relatieve waarschijnlijkheid voor een klant om het voorspelde doel binnen het bepaalde tijdkader te bereiken. Deze waarde moet niet worden beschouwd als een waarschijnlijkheidspercentage, maar veeleer als de waarschijnlijkheid dat een individu vergeleken wordt met de totale populatie. This score ranges from 0 to 100. |
| Probability | Deze eigenschap is de ware waarschijnlijkheid van een profiel voor het bereiken van het voorspelde doel binnen het bepaalde tijdkader. Bij het vergelijken van outputs over verschillende doelstellingen, wordt geadviseerd dat u waarschijnlijkheid over percentiel of score overweegt. Probability should always be used when determining the average probability across the eligible population, as the probability tends to be on the lower side for events that do not occur frequently. Waarden voor de waarschijnlijkheid liggen tussen 0 en 1. |
| Percentile | This value provides information regarding the performance of a profile relative to other similarly scored profiles. Een profiel met een percentielrang van 99 voor churn geeft bijvoorbeeld aan dat het risico op churning groter is dan 99% van alle andere profielen die zijn gescaureerd. De percentages variëren van 1 tot 100. |
| Type volheid | The selected propensity type. |
| Score-datum | The date on which scoring occurred. |
| Influentiële factoren | Voorspelde redenen waarom een profiel waarschijnlijk wordt omgezet of afgekapt. Factoren bestaan uit de volgende kenmerken:<ul><li>Code: Het profiel of gedragskenmerk dat de voorspelde score van een profiel positief beïnvloedt. </li><li>Waarde: De waarde van het profiel of gedragskenmerk.</li><li>Belangrijk: Hiermee wordt het gewicht van het profiel of gedragskenmerk op de voorspelde score aangegeven (laag, gemiddeld, hoog)</li></ul> |

## Volgende stappen {#next-steps}

Nadat u de gegevens hebt voorbereid en al uw gegevens en schema&#39;s hebt geïnstalleerd, begint u met het volgende: [Een AI-instantie van een klant configureren](./user-guide/configure.md) hulplijn. Deze gids begeleidt u door het creëren van een geval voor Klant AI.
