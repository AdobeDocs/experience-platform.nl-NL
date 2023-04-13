---
keywords: Experience Platform;aan de slag gaan;klantenhulp;populaire onderwerpen;input van klantensteun;klantenoutput; gegevensvereisten
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Gegevensvereisten in AI van de Klant
topic-legacy: Getting started
description: Meer informatie over de vereiste gebeurtenissen, invoer en uitvoer die door de AI van de Klant worden gebruikt.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2471'
ht-degree: 0%

---


# Invoer en uitvoer in AI van de Klant

In het volgende document worden de verschillende vereiste gebeurtenissen, invoer en uitvoerbestanden beschreven die in de AI van de Klant worden gebruikt.

## Aan de slag {#getting-started}

Hier volgen de stappen voor het samenstellen van nevenmodellen en het identificeren van doelgroepen voor gepersonaliseerde marketing in Customer AI:

1. Gevallen van gebruik in contouren: Hoe zouden de aandrijvingsmodellen helpen om doelpubliek voor gepersonaliseerde marketing te identificeren? Wat zijn mijn bedrijfsdoelstellingen en overeenkomstige tactieken om het doel te bereiken? Waar kan de propensiteitsmodellering in dit proces passen?

2. Prioriteit van de gebruiksgevallen: Welke zijn de hoogste prioriteiten voor het bedrijfsleven?

3. Modellen samenstellen in de AI van de Klant: Dit bekijken [snelle zelfstudie](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html) en verwijzen naar onze [UI-hulplijn](../customer-ai/user-guide/configure.md) voor een stapsgewijs proces om een model te bouwen.

4. [Segmenten maken](../customer-ai/user-guide/create-segment.md) modelresultaten gebruiken.

5. Voer gerichte bedrijfsacties uit die op deze segmenten worden gebaseerd. De resultaten controleren en de acties doorlopen om deze te verbeteren.

Hier zijn voorbeeldconfiguraties voor uw eerste model.  Het voorbeeldmodel, dat in dit document is ingebouwd, gebruikt een AI-model van de Klant om te voorspellen wie in de komende 30 dagen waarschijnlijk zal converteren voor een handelsbedrijf. De inputdataset is een dataset van Adobe Analytics.

| Stap | Definitie | Voorbeeld |
| ---- | ------ | ------- |
| Instellen | Geef basisinformatie over het model op. | **Naam**: Propensatiemodel potloodaankoop <br> **Modeltype**: Conversie |
| Gegevens selecteren | Specificeer de datasets die worden gebruikt om het model te bouwen. | **Gegevensset**: Adobe Analytics-gegevensset <br> **Identiteit**: Zorg ervoor dat de identiteitskolom voor elke gegevensset is ingesteld op een gemeenschappelijke identiteit. |
| Doel definiëren | Definieer het doel, de in aanmerking komende populatie, aangepaste gebeurtenissen en profielkenmerken. | **Voorspeldoel**: Selecteren `commerce.purchases.value` is gelijk aan potlood <br> **Venster Uitvoer**: 30 dagen. |
| Opties instellen | Stel de planning voor het vernieuwen van het model in en schakel scores voor profiel in | **Schema**: Wekelijks <br> **Inschakelen voor profiel**: Dit moet worden toegelaten voor de modeloutput die in segmentatie moet worden gebruikt. |

## Overzicht van gegevens {#data-overview}

In de volgende secties wordt een overzicht gegeven van de verschillende vereiste gebeurtenissen, invoer en uitvoerbestanden die in de AI van de Klant worden gebruikt.

De AI van de klant werkt door de volgende datasets te analyseren om te voorspellen (wanneer een klant waarschijnlijk zal stoppen met het gebruik van het product) of de conversie (wanneer een klant waarschijnlijk een aankoop zal doen) eigenschapscores:

- Adobe Analytics-gegevens gebruiken de [Bronconnector voor analyse](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager-gegevens gebruiken de [Audience Manager-bronaansluiting](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Gegevensset Experience Event](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [Gegevensverzameling over ervaringen met consumenten](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

U kunt veelvoudige datasets van verschillende bronnen toevoegen als elk van de datasets het zelfde identiteitstype (namespace) zoals ECID deelt. Voor meer informatie bij het toevoegen van veelvoudige datasets, bezoek [Handleiding voor AI-gebruikers van klant](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>De bronschakelaars nemen tot vier weken aan backfill gegevens in beslag. Als u onlangs opstelling een schakelaar plaatst, zou u moeten verifiëren dat de dataset de minimumlengte van gegevens heeft die voor AI van de Klant wordt vereist. Controleer de [historische gegevens](#data-requirements) om te verifiëren u genoeg gegevens voor uw vooruitgangsdoel hebt.

In de volgende tabel wordt een aantal gangbare terminologie beschreven die in dit document wordt gebruikt:

| Term | Definitie |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | XDM is het basiskader dat Adobe Experience Cloud, aangedreven door Adobe Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op het juiste moment te leveren. Het Platform gebruikt het Systeem XDM om gegevens op een bepaalde manier te organiseren die het voor de diensten van het Platform gemakkelijker maakt te gebruiken. |
| [XDM-schema](../../xdm/schema/composition.md) | Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens. Voordat gegevens in Platform kunnen worden opgenomen, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. Schema&#39;s bestaan uit een basis-XDM-klasse en nul of meer schemaveldgroepen. |
| [XDM-klasse](../../xdm/schema/field-constraints.md) | Alle XDM-schema&#39;s beschrijven gegevens die als `Experience Event`. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. De klassen XDM beschrijven het kleinste aantal eigenschappen een schema moet bevatten om een bepaald gegevensgedrag te vertegenwoordigen. |
| [Veldengroepen](../../xdm/schema/composition.md) | Een component die een of meer velden in een schema definieert. Veldgroepen dwingen af hoe hun velden worden weergegeven in de hiërarchie van het schema en tonen daarom in elk schema dezelfde structuur aan waarin ze zijn opgenomen. Veldgroepen zijn alleen compatibel met specifieke klassen, zoals bepaald door hun `meta:intendedToExtend` kenmerk. |
| [Gegevenstype](../../xdm/schema/composition.md) | Een component die ook een of meer velden voor een schema kan bevatten. In tegenstelling tot veldgroepen worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn. De gegevenstypen die in dit document worden beschreven, worden ondersteund door zowel de CEE- als Adobe Analytics-schema&#39;s. |
| [Klantprofiel in real time](../../profile/home.md) | Klantprofiel in realtime biedt een gecentraliseerd consumentenprofiel voor gericht en gepersonaliseerd ervaringsbeheer. Elk profiel bevat gegevens die op alle systemen zijn geaggregeerd, en actioneerbare tijdstempelaccounts van gebeurtenissen waarbij de persoon is betrokken die hebben plaatsgevonden in een van de systemen die u met Experience Platform gebruikt. |

## Invoergegevens van AI van de klant {#customer-ai-input-data}

Voor inputdatasets, zoals Adobe Analytics en Adobe Audience Manager, wijzen de respectieve bronschakelaars direct de gebeurtenissen in deze standaardgebiedsgroepen (Handel, Web, Toepassing, en Onderzoek) door gebrek tijdens het verbindingsproces in kaart. In de onderstaande tabel worden de gebeurtenisvelden weergegeven in de standaardveldgroepen voor Klanten-AI.

Voor meer informatie over het in kaart brengen van de gegevens van Adobe Analytics of van de Audience Manager gegevens, bezoek de het gebiedsafbeeldingen van de Analyse of Audience Manager [hulplijn voor veldtoewijzingen](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

U kunt de Gebeurtenis van de Ervaring of de Gebeurtenis XDM schema&#39;s van de Ervaring voor inputdatasets gebruiken die niet via één van de bovengenoemde schakelaars worden bevolkt. Extra XDM gebiedsgroepen kunnen tijdens het proces van de schemaverwezenlijking worden toegevoegd. De veldgroepen kunnen worden opgegeven door Adobe, zoals de standaardveldgroepen of een aangepaste veldgroep, die overeenkomt met de gegevensrepresentatie in het Platform.

>[!IMPORTANT]
>
>U moet ervoor zorgen dat de gegevens in deze inputdatasets worden bevolkt. Als geen gebeurtenissen van standaardgebiedsgroepen in de inputdatasets worden gevonden, moet u douanegebeurtenissen tijdens het configuratiewerkschema toevoegen. Zie details over aangepaste gebeurtenissen.

### Door de AI van de Klant gebruikte standaardveldgroepen {#standard-events}

De Gebeurtenissen van de ervaring worden gebruikt om diverse klantengedrag te bepalen. Afhankelijk van hoe uw gegevens gestructureerd zijn, omvatten de hieronder vermelde gebeurtenistypen mogelijk niet alle gedragingen van uw klant. Het is aan u om te bepalen welke gebieden de noodzakelijke gegevens hebben die nodig zijn om Web of andere kanaal-specifieke gebruikersactiviteit duidelijk en ondubbelzinnig te identificeren. Afhankelijk van uw voorspellingsdoel, kunnen de vereiste gebieden veranderen die nodig zijn.

>[!NOTE]
>
>Als u Adobe Analytics- of Adobe Audience Manager-gegevens gebruikt, wordt het schema automatisch gemaakt met de vereiste standaardgebeurtenissen die nodig zijn om uw gegevens vast te leggen. Als u uw eigen EE-schema maakt om gegevens vast te leggen, moet u overwegen welke veldgroepen nodig zijn om uw gegevens vast te leggen.

Klant-AI gebruikt standaard de gebeurtenissen in deze vier standaardveldgroepen: Handel, Web, Toepassing, en Onderzoek. Het is niet nodig voor elke gebeurtenis gegevens te hebben in de hieronder vermelde standaardveldgroepen, maar voor bepaalde scenario&#39;s zijn bepaalde gebeurtenissen vereist. Als u gebeurtenissen in de beschikbare standaardveldgroepen hebt, is het raadzaam deze op te nemen in uw schema. Bijvoorbeeld, als u een model van AI van de Klant voor het voorspellen van aankoopgebeurtenissen wilde tot stand brengen, is het nuttig om gegevens van de de detailsgebiedgroepen van de Handel en van de Web-pagina te hebben.

Als u een veldgroep wilt weergeven in de gebruikersinterface van het Platform, selecteert u de optie **[!UICONTROL Schemas]** op de linkerspoorstaaf, gevolgd door het selecteren van **[!UICONTROL Field groups]** tab.

| Veldgroep | Het type Event | XDM-veldpad |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | bestellen | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | kassa | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
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

Bovendien kan de AI van de Klant abonnementsgegevens gebruiken om betere modellen van de Koor te bouwen. Abonnementsgegevens zijn nodig voor elk profiel dat de [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md) indeling van gegevenstype. De meeste velden zijn optioneel, maar voor een optimaal chroommodel is het zeer raadzaam gegevens te verstrekken voor zoveel mogelijk velden, zoals: `startDate`, `endDate`en alle andere relevante gegevens. Neem contact op met uw accountteam voor extra ondersteuning voor deze functie.

### Aangepaste gebeurtenissen en profielkenmerken toevoegen {#add-custom-events}

Als u over informatie beschikt die u naast de standaardinstelling wilt opnemen [standaardgebeurtenisvelden](#standard-events) gebruikt door AI van de Klant, kunt u gebruiken [aangepaste gebeurtenisconfiguratie](./user-guide/configure.md#custom-events) om de gegevens te verhogen die door het model worden gebruikt.

#### Wanneer moet u aangepaste gebeurtenissen gebruiken?

De gebeurtenissen van de douane zijn noodzakelijk wanneer de datasets die in de stap van de datasetselectie worden gekozen bevatten *none* van de standaardvelden voor gebeurtenissen die door de AI van de Klant worden gebruikt. De AI van de Klant heeft informatie over minstens één gebeurtenis van het gebruikersgedrag buiten het resultaat nodig.

Aangepaste gebeurtenissen zijn handig voor:

- Het opnemen van domeinkennis of voorafgaande expertise in het model.

- Verbetering van de kwaliteit van het voorspellende model.

- Meer inzichten en interpretaties verzamelen.

De beste kandidaten voor aangepaste gebeurtenissen zijn gegevens die domeinkennis bevatten die het resultaat kunnen voorspellen. Algemene voorbeelden van aangepaste gebeurtenissen zijn onder andere:

- Registreren voor account

- Abonneren op nieuwsbrief

- Maak een vraag aan de klantendienst

Hieronder volgt een selectie industriespecifieke voorbeelden van aangepaste gebeurtenissen:

| Industrie | Aangepaste gebeurtenissen |
| --- | --- |
| Detailhandel | Transactie in de winkel<br>Aanmelden voor clubkaart<br>Mobiele coupon knippen. |
| Entertainment | Lidmaatschap voor koopseizoen <br> Video streamen. |
| Ziekenhuis | Reservering restaurant maken <br> Koop loyaliteitspunten. |
| Reizen | Informatie over bekende reizigers toevoegen Aankoopmijlen. |
| Communicatie | Plan upgraden/downgraden/annuleren. |

Aangepaste gebeurtenissen moeten door de gebruiker geïnitieerde acties vertegenwoordigen om te kunnen worden geselecteerd. Bijvoorbeeld, &quot;E-mail verzendt&quot;is een actie die door een teller en niet door de gebruiker in werking wordt gesteld, zodat zou het niet als douanegebeurtenis moeten worden gebruikt.

### Historische gegevens

Voor modeltraining zijn historische gegevens vereist. De vereiste duur voor gegevens binnen het systeem wordt bepaald door twee sleutelelementen: het resultatenvenster en de in aanmerking komende populatie.

Standaard zoekt de AI van de Klant naar een gebruiker die in de laatste 45 dagen activiteit heeft gehad als er geen definitie van de in aanmerking komende populatie is opgegeven tijdens de toepassingsconfiguratie. Daarnaast vereist de AI van de Klant minimaal 500 gekwalificeerde en 500 niet-kwalificerende gebeurtenissen (in totaal 1000) op basis van historische gegevens op basis van een voorspelde doeldefinitie.

In de volgende voorbeelden wordt het gebruik van een eenvoudige formule getoond waarmee u de minimale hoeveelheid vereiste gegevens kunt bepalen. Als u meer gegevens hebt dan minimaal vereist, levert uw model waarschijnlijk nauwkeurigere resultaten op. Als u minder dan het vereiste minimumbedrag hebt, zal het model ontbreken, aangezien er niet genoeg gegevens voor modelopleiding zijn.

**Formule**:

De minimaal vereiste gegevensduur in het systeem bepalen:

- De minimale gegevens die nodig zijn om functies te maken, zijn 30 dagen. Vergelijk het terugkijkvenster voor geschiktheid met 30 dagen:

   - Als het terugkijkvenster van de geschiktheid meer dan 30 dagen is, het gegevensvereiste = verkiesbaarheids terugkijkvenster + resultaatvenster.

   - Anders is de gegevensvereiste 30 dagen + resultaatvenster.

** Als er meer dan één voorwaarde is voor het bepalen van de in aanmerking komende populatie, is het terugkijkvenster van geschiktheid het langste.

>[!NOTE]
>
>30 is het minimumaantal dagen dat vereist is voor de in aanmerking komende bevolking. Als dit niet wordt verstrekt is het gebrek 45 dagen.

**Voorbeelden**:

- U wilt voorspellen of een klant waarschijnlijk in de komende 30 dagen een horloge zal kopen voor hen die één of andere Webactiviteit in de laatste 60 dagen hebben.

   - Geschiktheidsterugkijkvenster = 60 dagen

   - Outcome window = 30 dagen

   - Vereiste gegevens = 60 dagen + 30 dagen = 90 dagen

- U wilt voorspellen of de gebruiker waarschijnlijk de komende 7 dagen een horloge zal kopen **zonder** een expliciete in aanmerking komende bevolking. In dit geval is de in aanmerking komende populatie standaard &quot;diegenen die de afgelopen 45 dagen actief zijn geweest&quot; en is het resultaatvenster 7 dagen.

   - Geschiktheidsterugkijkvenster = 45 dagen

   - Outcome window = 7 dagen

   - Vereiste gegevens = 45 dagen + 7 dagen = 52 dagen

- U wilt voorspellen of de klant waarschijnlijk in de komende 7 dagen een horloge zal kopen voor hen die één of andere Webactiviteit in de laatste 7 dagen hebben.

   - Geschiktheidsterugkijkvenster = 7 dagen

   - Minimale gegevens die vereist zijn om functies te maken = 30 dagen

   - Outcome window = 7 dagen

   - Vereiste gegevens = 30 dagen + 7 dagen = 37 dagen

Hoewel de AI van de Klant een minimumperiode vereist om de gegevens binnen het systeem te bestaan, werkt het ook het best met recente gegevens. Door gebruik te maken van recentere gedragsgegevens zal de AI van de Klant waarschijnlijk een nauwkeurigere voorspelling geven van het toekomstige gedrag van een gebruiker.

## AI-uitvoergegevens van klant {#customer-ai-output-data}

De AI van de Klant produceert verscheidene attributen voor individuele profielen die als verkiesbaar worden beschouwd. Er zijn twee manieren om de score (output) te verbruiken op basis van wat u hebt voorzien. Als u een Real-time dataset van het Profiel van de Klant hebt toegelaten, kunt u inzichten van het Profiel van de Klant in real time in [Segment Builder](../../segmentation/ui/segment-builder.md). Als u geen profiel-Toegelaten dataset hebt, kunt u [De AI-uitvoer van de klant downloaden](./user-guide/download-scores.md) dataset beschikbaar op het data Lake.

U kunt de outputdataset in het Platform vinden **Gegevenssets** werkruimte. Alle AI-uitvoergegevenssets van de klant beginnen met de naam **AI-scores van klant - NAME_OF_APP**. Evenzo beginnen alle AI-uitvoerschema&#39;s van de Klant met de naam **AI-schema van klant - Naam_van_app**.

![Naam van de gegevensreeksen van de uitvoer in AI van de Klant](./images/user-guide/cai-schema-name-of-app.png)

In de onderstaande tabel worden de verschillende kenmerken beschreven die in de uitvoer van AI van de Klant zijn aangetroffen:

| Kenmerk | Beschrijving |
| ----- | ----------- |
| [!UICONTROL Score] | De relatieve waarschijnlijkheid voor een klant om het voorspelde doel binnen het bepaalde tijdkader te bereiken. Deze waarde moet niet worden beschouwd als een waarschijnlijkheidspercentage, maar veeleer als de waarschijnlijkheid dat een individu vergeleken wordt met de totale populatie. Deze score varieert van 0 tot 100. |
| Waarschijnlijkheid | Deze eigenschap is de ware waarschijnlijkheid van een profiel voor het bereiken van het voorspelde doel binnen het bepaalde tijdkader. Bij het vergelijken van outputs over verschillende doelstellingen, wordt u geadviseerd om waarschijnlijkheid over percentiel of score te overwegen. Bij het bepalen van de gemiddelde waarschijnlijkheid in de in aanmerking komende populatie moet altijd rekening worden gehouden met de waarschijnlijkheid, aangezien de waarschijnlijkheid aan de onderkant ligt voor gebeurtenissen die niet vaak voorkomen. Waarden voor het waarschijnlijkheidsbereik tussen 0 en 1. |
| Percentage | Deze waarde biedt informatie over de prestaties van een profiel ten opzichte van andere profielen met een vergelijkbare score. Een profiel met een percentielrang van 99 voor churn geeft bijvoorbeeld aan dat het risico op churning groter is dan 99% van alle andere profielen die zijn gescaureerd. De percentielen variëren van 1 tot 100. |
| Type volheid | Het geselecteerde type buigzaamheid. |
| Score-datum | De datum waarop de scoring heeft plaatsgevonden. |
| Influentiële factoren | Dit zijn voorspelde redenen waarom een profiel waarschijnlijk wordt omgezet of afgekapt. Deze factoren bestaan uit de volgende kenmerken:<ul><li>Code: Het profiel of gedragskenmerk dat de voorspelde score van een profiel positief beïnvloedt. </li><li>Waarde: De waarde van het profiel of gedragskenmerk.</li><li>Belangrijk: Hiermee wordt het gewicht van het profiel of gedragskenmerk op de voorspelde score aangegeven (laag, gemiddeld, hoog)</li></ul> |

## Volgende stappen {#next-steps}

Wanneer u uw gegevens hebt voorbereid en ervoor zorgt dat al uw referenties en schema&#39;s aanwezig zijn, raadpleegt u de [Een AI-instantie van een klant configureren](./user-guide/configure.md) gids, die u door een geleidelijke leerprogramma begeleidt om een instantie van de Klant te creëren AI.