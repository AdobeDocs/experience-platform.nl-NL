---
keywords: Experience Platform;aan de slag;klantenhulp;populaire onderwerpen;input van klantenhulp;klantenoutput
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Invoer en uitvoer in AI van de Klant
topic: Getting started
description: Meer informatie over de vereiste gebeurtenissen, invoer en uitvoer die door de AI van de Klant worden gebruikt.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '2867'
ht-degree: 0%

---

# Invoer en uitvoer in AI van de Klant

In het volgende document worden de verschillende vereiste gebeurtenissen, invoer en uitvoerbestanden beschreven die in de AI van de Klant worden gebruikt.

## Aan de slag

De AI van de Klant werkt door één van de volgende datasets te analyseren om de scores van de kromme of van de omzettingsdichtheid te voorspellen:

- Gegevensset met consumentenervaringen (CEE)
- Adobe Analytics-gegevens met de [Bronconnector voor analyse](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager-gegevens die gebruikmaken van de [Audience Manager-bronconnector](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>De bronschakelaars nemen tot vier weken aan backfill gegevens in beslag. Als u onlangs opstelling een schakelaar plaatst, zou u moeten verifiëren dat de dataset de minimumlengte van gegevens heeft die voor AI van de Klant wordt vereist. Controleer de sectie [historische gegevens](#data-requirements) om te controleren of u voldoende gegevens hebt voor uw voorspellingsdoel.

Voor dit document is basiskennis van het CEE-schema vereist. Lees de [Intelligent Services-gegevensvoorbereiding](../data-preparation.md)-documentatie voordat u verdergaat.

In de volgende tabel wordt een aantal gangbare terminologie beschreven die in dit document wordt gebruikt:

| Term | Definitie |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | XDM is het basiskader dat Adobe Experience Cloud, aangedreven door Adobe Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op het juiste moment te leveren. De methodologie waarop het Experience Platform wordt gebouwd, het Systeem van XDM, stelt de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform in werking. |
| XDM-schema | Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens. Voordat gegevens in Platform kunnen worden opgenomen, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. Schema&#39;s bestaan uit een basis-XDM-klasse en nul of meer mixins. |
| XDM-klasse | Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. De klassen XDM beschrijven het kleinste aantal eigenschappen een schema moet bevatten om een bepaald gegevensgedrag te vertegenwoordigen. |
| [Mixins](../../xdm/schema/composition.md) | Een component die een of meer velden in een schema definieert. Mixins dwingen af hoe hun gebieden in de hiërarchie van het schema verschijnen, en tonen daarom de zelfde structuur in elk schema dat zij inbegrepen zijn. Mixins zijn alleen compatibel met specifieke klassen, zoals die door hun `meta:intendedToExtend`-kenmerk worden geïdentificeerd. |
| [Gegevenstype](../../xdm/schema/composition.md) | Een component die ook een of meer velden voor een schema kan bevatten. In tegenstelling tot mengsels, worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn. De gegevenstypen die in dit document worden beschreven, worden ondersteund door zowel de CEE- als Adobe Analytics-schema&#39;s. |
| Churn | Een meting van het percentage accounts dat de abonnementen annuleert of niet vernieuwt. Een hoge wisselkoers kan een negatief effect hebben op de maandelijkse terugkerende inkomsten (MRR) en kan ook wijzen op ontevredenheid over een product of dienst. |
| [Klantprofiel in realtime](../../profile/home.md) | Klantprofiel in realtime biedt een gecentraliseerd consumentenprofiel voor gericht en gepersonaliseerd ervaringsbeheer. Elk profiel bevat gegevens die op alle systemen zijn geaggregeerd, en actioneerbare tijdstempelaccounts van gebeurtenissen waarbij de persoon is betrokken die hebben plaatsgevonden in een van de systemen die u met Experience Platform gebruikt. |

## Invoergegevens van AI van de klant

>[!TIP]
>
> De AI van de Klant bepaalt automatisch welke gebeurtenissen nuttig voor voorspellingen zijn en roept een waarschuwing op als de beschikbare gegevens niet voldoende zijn om kwaliteitsvoorspellingen te produceren.

AI van de Klant steunt CEE, Adobe Analytics, en de datasets van Adobe Audience Manager. Het CEE-schema vereist dat u tijdens het maken van het schema mixins toevoegt. Als u de datasets van Adobe Analytics of van Adobe Audience Manager gebruikt, brengt de bronschakelaar direct de standaardgebeurtenissen (Handel, de details van de Web-pagina, Toepassing, en Onderzoek) in kaart die hieronder tijdens het verbindingsproces worden vermeld.

Voor meer informatie over het in kaart brengen van de gegevens van Adobe Analytics of van de Audience Manager, bezoek [het gebiedsafbeeldingen van Analytics](../../sources/connectors/adobe-applications/analytics.md) of [Audience Manager van gebiedsafbeeldingen ](../../sources/connectors/adobe-applications/mapping/audience-manager.md) gids.

### Standaardgebeurtenissen gebruikt door AI {#standard-events}

De Gebeurtenissen van de Ervaring XDM worden gebruikt voor het bepalen van diverse klantengedrag. Afhankelijk van de structuur van uw gegevens, omvatten de hieronder vermelde gebeurtenistypen mogelijk niet alle gedragingen van uw klant. Het is aan u om te bepalen welke gebieden de noodzakelijke gegevens hebben die nodig zijn om Webgebruikersactiviteit duidelijk en ondubbelzinnig te identificeren. Afhankelijk van uw voorspellingsdoel, kunnen de vereiste gebieden veranderen die nodig zijn.

De AI van de klant is afhankelijk van verschillende gebeurtenistypen voor de eigenschappen van het bouwmodel. Deze gebeurtenistypen worden automatisch toegevoegd aan uw schema met behulp van meerdere XDM-mixen.

>[!NOTE]
>
>Als u Adobe Analytics- of Adobe Audience Manager-gegevens gebruikt, wordt het schema automatisch gemaakt met de vereiste standaardgebeurtenissen die nodig zijn om uw gegevens vast te leggen. Als u uw eigen douaneCEE schema creeert om gegevens te vangen, moet u overwegen welke mengen nodig zijn om uw gegevens te vangen.

Het is niet nodig gegevens te hebben voor elk van de hieronder vermelde standaardgebeurtenissen, maar voor bepaalde scenario&#39;s zijn bepaalde gebeurtenissen vereist. Als u standaardgebeurtenisgegevens hebt, is het raadzaam deze op te nemen in uw schema. Als u bijvoorbeeld een AI-toepassing van de Klant wilt maken om aankoopgebeurtenissen te voorspellen, is het handig om gegevens te hebben van de gegevenstypen `Commerce` en `Web page details`.

Als u een mix wilt weergeven in de interface van het Platform, selecteert u de tab **[!UICONTROL Schemas]** op de linkertrack, gevolgd door de tab **[!UICONTROL Mixins]**.


| Mixin | Het type Event | XDM-veldpad |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | bestellen | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
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

Bovendien kan de AI van de Klant abonnementsgegevens gebruiken om betere modellen van de Koor te bouwen. Abonnementsgegevens zijn nodig voor elk profiel met de indeling [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md) voor gegevenstypen. De meeste velden zijn echter optioneel voor een optimaal churn-model. Het wordt echter ten zeerste aanbevolen gegevens op te geven voor zoveel mogelijk velden, zoals `startDate`, `endDate` en alle andere relevante details.

### Historische gegevens {#data-requirements}

Klanten-AI hebben historische gegevens nodig voor modeltraining, maar de hoeveelheid vereiste gegevens is gebaseerd op twee sleutelelementen: resultaatvenster en in aanmerking komende populatie.

Standaard zoekt de AI van de Klant naar een gebruiker die activiteit heeft gehad in de laatste 120 dagen als er tijdens de toepassingsconfiguratie geen definitie van de in aanmerking komende populatie is opgegeven. Daarnaast vereist de AI van de Klant minimaal 500 gekwalificeerde en 500 niet-kwalificerende gebeurtenissen (in totaal 1000) van historische gegevens op basis van een voorspelde doeldefinitie.

In de volgende voorbeelden wordt een eenvoudige formule gebruikt om u te helpen de minimale vereiste hoeveelheid gegevens te bepalen. Als u meer dan de minimumvereiste hebt, zal uw model waarschijnlijk nauwkeurigere resultaten verstrekken. Als u minder dan het vereiste minimumbedrag hebt, zal het model ontbreken aangezien er geen voldoende hoeveelheid gegevens voor modelopleiding is.

**Formule**:

Minimumlengte van de vereiste gegevens = subsidiabele populatie + resultaatvenster

>[!NOTE]
>
> 30 is het minimumaantal dagen dat vereist is voor de in aanmerking komende bevolking. Als dit niet wordt verstrekt is het gebrek 120 dagen.

Voorbeelden :

- U wilt voorspellen of een klant waarschijnlijk een horloge in de komende 30 dagen zal kopen. U wilt ook gebruikers scoren die de afgelopen 60 dagen enige internetactiviteit hebben gehad. In dat geval is de minimumlengte van de vereiste gegevens 60 dagen + 30 dagen. De in aanmerking komende populatie is 60 dagen en het resultaatvenster is 30 dagen in totaal 90 dagen.

- U wilt voorspellen of de gebruiker waarschijnlijk de komende 7 dagen een horloge zal kopen. In dat geval is de minimumlengte van de vereiste gegevens 120 dagen + 7 dagen. De in aanmerking komende populatie staat standaard op 120 dagen en het resultaatvenster is 7 dagen in totaal 127 dagen.

- U wilt voorspellen of de klant waarschijnlijk de komende 7 dagen een horloge zal kopen. U wilt ook gebruikers scoren die de afgelopen 7 dagen enige internetactiviteit hebben gehad. In dat geval is de minimumlengte van de vereiste gegevens 30 dagen + 7 dagen. De in aanmerking komende populatie duurt minimaal 30 dagen en de resultaatperiode bedraagt 7 dagen in totaal 37 dagen.

Naast de minimaal vereiste gegevens, werkt de AI van de Klant ook het best met recente gegevens. In dit geval doet de AI van de Klant een prognose voor de toekomst op basis van recente gedragsgegevens van een gebruiker. Met andere woorden, recentere gegevens zullen waarschijnlijk een nauwkeurigere voorspelling opleveren.

### Voorbeeldscenario&#39;s

In deze sectie worden verschillende scenario&#39;s voor exemplaren van AI van de Klant beschreven evenals de vereiste en geadviseerde gebeurtenistypen. Raadpleeg de bovenstaande [standaardgebeurtenissentabel](#standard-events) voor meer informatie over de mixin en het veldpad.

>[!NOTE]
>
> De vereiste gebeurtenistypen worden gebruikt om Webgebruikersactiviteit duidelijk en ondubbelzinnig te identificeren. Het aantal vereiste gebeurtenistypen wordt gewijzigd op basis van het voorspellingsdoel en de structuur van uw schema. Als u niet zeker bent dat een bepaald gebeurtenistype nodig is, wordt geadviseerd om dat gebeurtenistype te omvatten terwijl het bouwen van uw CEE schema. Als u Adobe Analytics- of Adobe Audience Manager-gegevens gebruikt, moeten de vereiste standaardgebeurtenissen beschikbaar zijn, afhankelijk van de gegevens die u streamt.

### Scenario 1: Aankoop van conversie op een e-commercewebsite

**Voorspeldoelstelling:** voorspellen dat de in aanmerking komende profielen een bepaald kledingstuk op een website kunnen kopen.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- bestellen
- kassa
- aankopen
- webVisit
- zoeken

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw AI-instantie van de klant. Als de gegevens beschikbaar zijn voor een bepaald gegevenstype, wordt aangeraden dat deze gegevens in het schema worden opgenomen.

### Scenario 2: Abonnementsconversie op een website van de mediastreamingservice

**Voorspellingsdoel:** voorspellen dat de conversiegevoeligheid van de in aanmerking komende profielen voor een abonnement een bepaald abonnementsniveau, zoals een standaard- of premieplan, zal overschrijden.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- bestellen
- kassa
- aankopen
- webVisit
- zoeken

In dit voorbeeld worden `order`, `checkouts` en `purchases` gebruikt om aan te geven dat een abonnement is aangeschaft en het type ervan.

Bovendien, voor een nauwkeurig model wordt geadviseerd dat u gebruik van sommige beschikbare eigenschappen in [het type van abonnementsgegevens ](../../xdm/data-types/subscription.md) maakt.

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw AI-instantie van de klant. Als de gegevens beschikbaar zijn voor een bepaald gegevenstype, wordt aangeraden dat deze gegevens in het schema worden opgenomen.

### Scenario 3: Churn op een e-commercewebsite

**Voorspeldoel:** voorspellen hoe waarschijnlijk het is dat een aankoopgebeurtenis niet plaatsvindt.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- bestellen
- kassa
- aankopen
- webVisit
- zoeken

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw AI-instantie van de klant. Als de gegevens beschikbaar zijn voor een bepaald gegevenstype, wordt aangeraden dat deze gegevens in het schema worden opgenomen.

### Scenario 4: Conversie via e-commerce

**Voorspeldoelstelling:** voorspellen hoe populair de bevolking die een specifiek product heeft aangeschaft, een nieuw verwant product kan aanschaffen.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- bestellen
- kassa
- aankopen
- webVisit
- zoeken

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw AI-instantie van de klant. Als de gegevens beschikbaar zijn voor een bepaald gegevenstype, wordt aangeraden dat deze gegevens in het schema worden opgenomen.

### Scenario 5: Abonnement (churn) op een online nieuwszender opzeggen

**Voorspellingsdoel:** voorspellen dat de in aanmerking komende bevolking geneigd zal zijn om volgende maand af te zien van een dienst.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- webVisit
- zoeken

Bovendien, voor een nauwkeurig model wordt geadviseerd dat u gebruik van sommige beschikbare eigenschappen in [het type van abonnementsgegevens ](../../xdm/data-types/subscription.md) maakt.

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw AI-instantie van de klant. Als de gegevens beschikbaar zijn voor een bepaald gegevenstype, wordt aangeraden dat deze gegevens in het schema worden opgenomen.

### Scenario 6: Mobiele toepassing starten

**Voorspellingsdoel:** voorspellen of een betaalde mobiele toepassing de komende X dagen waarschijnlijk de in aanmerking komende profielen zal worden gestart. Dit is vergelijkbaar met het voorspellen van de KPI (Key Performance Indicator) van &quot;Maandelijkse Actieve Gebruikers&quot;.

**Vereiste standaardgebeurtenistypen:**

De onderstaande gebeurtenistypen zijn vereist voor een optimale AI-uitvoer van de Klant met dit specifieke voorspellingsdoel. Het is mogelijk om een vereiste gebeurtenis uit te sluiten, afhankelijk van uw voorspellingsdoel, maar het uitsluiten van meerdere gebeurtenissen kan leiden tot slechte resultaten.

- bestellen
- kassa
- aankopen
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

In dit voorbeeld worden `order`, `checkouts` en `purchases` gebruikt wanneer een mobiele toepassing moet worden aangeschaft.

**Aanvullende aanbevolen standaardgebeurtenistypen:**

Een van de resterende [gebeurtenistypen](#standard-events) kan vereist zijn op basis van de complexiteit van uw doel en in aanmerking komende populatie tijdens de configuratie van uw AI-instantie van de klant. Als de gegevens beschikbaar zijn voor een bepaald gegevenstype, wordt aangeraden dat deze gegevens in het schema worden opgenomen.

### Scenario 7: Afgerealiseerde transacties (Adobe Audience Manager)

**Voorspelingsdoel:** voorspellen dat bepaalde kenmerken waarschijnlijk zullen worden gerealiseerd.

**Vereiste standaardgebeurtenistypen:**

Om eigenschappen van Adobe Audience Manager te gebruiken, moet u een bronverbinding tot stand brengen gebruikend [Audience Manager bronschakelaar](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). De bronschakelaar leidt automatisch tot het schema met juiste mengeling(en). U hoeft niet handmatig extra gebeurtenistypen toe te voegen om het schema te laten werken met Customer AI.

Wanneer u een nieuwe klant-AI-instantie configureert, kunnen `audienceName` en `audienceID` worden gebruikt om een bepaald kenmerk te selecteren voor scoring bij het definiëren van uw doel.

## AI-uitvoergegevens van klant

De AI van de Klant produceert verscheidene attributen voor individuele profielen die als verkiesbaar worden beschouwd. Er zijn twee manieren om de score (output) te verbruiken op basis van wat u hebt voorzien. Als u een in real time Klantprofiel-Toegelaten dataset hebt, kunt u inzichten van het Profiel van de Klant in real time in [de Bouwer van het Segment](../../segmentation/ui/segment-builder.md) verbruiken. Als u geen profiel-toegelaten dataset hebt, kunt u [de output van de Klant AI ](./user-guide/download-scores.md) dataset beschikbaar op het gegevensmeer downloaden.

>[!NOTE]
>
> De waarden van de output worden verbruikt door het Profiel van de Klant in real time dat kan worden gebruikt om segmenten tot stand te brengen en te bepalen.

In de onderstaande tabel worden de verschillende kenmerken beschreven die in de uitvoer van AI van de Klant zijn aangetroffen:

| Attribute | Beschrijving |
| ----- | ----------- |
| Score | De relatieve waarschijnlijkheid voor een klant om het voorspelde doel binnen het bepaalde tijdkader te bereiken. Deze waarde moet niet worden beschouwd als een waarschijnlijkheidspercentage, maar veeleer als de waarschijnlijkheid dat een individu vergeleken wordt met de totale populatie. Deze score varieert van 0 tot 100. |
| Waarschijnlijkheid | Deze eigenschap is de ware waarschijnlijkheid van een profiel voor het bereiken van het voorspelde doel binnen het bepaalde tijdkader. Bij het vergelijken van outputs over verschillende doelstellingen, wordt geadviseerd dat u waarschijnlijkheid over percentiel of score overweegt. Bij het bepalen van de gemiddelde waarschijnlijkheid in de in aanmerking komende populatie moet altijd rekening worden gehouden met de waarschijnlijkheid, aangezien de waarschijnlijkheid aan de onderkant ligt voor gebeurtenissen die niet vaak voorkomen. Waarden voor de waarschijnlijkheid liggen tussen 0 en 1. |
| Percentage | Deze waarde biedt informatie over de prestaties van een profiel ten opzichte van andere profielen met een vergelijkbare score. Een profiel met een percentielrang van 99 voor churn geeft bijvoorbeeld aan dat het risico op churning groter is dan 99% van alle andere profielen die zijn gescaureerd. De percentages variëren van 1 tot 100. |
| Type volheid | Het geselecteerde type buigzaamheid. |
| Score-datum | De datum waarop de scoring heeft plaatsgevonden. |
| Influentiële factoren | Voorspelde redenen waarom een profiel waarschijnlijk wordt omgezet of afgekapt. Factoren bestaan uit de volgende kenmerken:<ul><li>Code: Het profiel of gedragskenmerk dat de voorspelde score van een profiel positief beïnvloedt. </li><li>Waarde: De waarde van het profiel of gedragskenmerk.</li><li>Belangrijk: Hiermee wordt het gewicht van het profiel of gedragskenmerk op de voorspelde score aangegeven (laag, gemiddeld, hoog)</li></ul> |

## Volgende stappen {#next-steps}

Zodra u uw gegevens hebt voorbereid en al uw geloofsbrieven en schema&#39;s op zijn plaats hebt, begin door [een Instantie van de Klant te volgen AI](./user-guide/configure.md) gids te vormen. Deze gids begeleidt u door het creëren van een geval voor Klant AI.
