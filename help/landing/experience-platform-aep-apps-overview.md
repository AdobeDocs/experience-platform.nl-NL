---
title: Hoe Adobe Experience Platform en toepassingen samenwerken
description: Adobe Experience Platform en elke toepassing werken alleen, en ze werken samen om uw klantdoelstellingen te ondersteunen.
solution: Experience Platform
feature: Getting Started
topic: Overview
role: Architect, Developer, Data Architect, Data Engineer, Business Practitioner
exl-id: c4f8e2a1-6b3d-4f92-9c7e-1a2b3c4d5e6f
source-git-commit: 60e7d803d72089348f11a34d6386aa9ccc51f487
workflow-type: tm+mt
source-wordcount: '3250'
ht-degree: 0%

---


# Hoe Adobe Experience Platform en toepassingen samenwerken

In dit onderwerp worden drie ideeën beschreven.

1. Wat [!DNL Adobe Experience Platform] op zichzelf doet.
2. Wat elke toepassing op zichzelf doet.
3. Hoe het platform en de toepassingen samenwerken zodat kan uw organisatie zijn doelstellingen ontmoeten en uw klanten goed dienen.

Deel dit onderwerp met marketers, producteigenaars, en mensen die de oplossing bouwen of in werking stellen. Nadat u het hebt gelezen, gebruikt u stapsgewijze hulplijnen in [!DNL Experience League] wanneer u producttaken of technische details nodig hebt.

>[!NOTE]
>
>Dit onderwerp is een overzicht. Voor hoe te stappen, gebruikersinterfaceacties, en API details, zie de verbindingen in [ Aanvullende middelen ](#additional-resources).

## Wat zijn de toepassingen en wat is het belangrijkste doel van elk {#applications-at-a-glance}

In deze documentatie is een toepassing een Adobe-product met licentie dat op [!DNL Adobe Experience Platform] wordt uitgevoerd. Toepassingen gebruiken hetzelfde klantprofiel, dezelfde gegevensstructuur, dezelfde identiteitskoppelingen en dezelfde gegevensregels als het platform. Elke toepassing voegt zijn eigen schermen en workflows toe voor een type werk (bijvoorbeeld het verzenden van publiek naar kanalen, het uitvoeren van reizen of het melden van resultaten).

In de onderstaande tabel wordt elke toepassing weergegeven. Het geeft een korte beschrijving en een hoofddoel. Niet elke productafdruk wordt vermeld. Wat je kunt kopen, is afhankelijk van je licentie.

| Toepassing | Wat het is | Hoofddoel |
|---------------|------------|----------------|
| [[!DNL Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/home) | Toepassing van klantgegevens en publiek | Breng uw eigen klantgegevens bij elkaar. Bouw publiek dat vaak bijwerkt. Send publiek en kenmerken naar advertenties, e-mail, mobiele apps en andere gereedschappen. De gegevensregels worden toegepast. Dezelfde productfamilie ondersteunt consumentenbedrijven, zakelijke klanten en gemengde modellen. Raadpleeg de Help bij het product voor versies. |
| [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/en/docs/journey-optimizer) | Aanvraag voor reizen en berichten | Plan en voer persoonlijke reizen uit (bijvoorbeeld welkomstpaden, behoud of follow-up na service). Verzend berichten via kanalen met behulp van livegebeurtenissen en profielgegevens. |
| [[!DNL Customer Journey Analytics]](https://experienceleague.adobe.com/en/docs/customer-journey-analytics) | Toepassing van de analyse over kanalen | Meet en bestudeer hoe klanten door reizen en hoe marketing presteert. Hiermee gebruikt u gegevens die zijn voorbereid in [!DNL Adobe Experience Platform] . |
| [[!DNL Adobe Mix Modeler]](https://experienceleague.adobe.com/en/docs/mix-modeler) | Aanvraag voor marketingmeting en -planning | Breng de metingen samen (inclusief modellering van marketingmix). Plan uitgavenscenario&#39;s voor marketing. Gebruikt gegevens die via [!DNL Adobe Experience Platform] zijn verbonden, zodat teams kunnen zien wat de resultaten en planningsbudgetten beïnvloedt. |

>[!NOTE]
>
>Andere Adobe Experience Cloud-producten kunnen verbinding maken met [!DNL Adobe Experience Platform] . Dit onderwerp concentreert zich op toepassingen die het platform als hun belangrijkste bron van klantengegevens gebruiken. Productnamen, edities en wat wordt verkocht, kunnen verschillen per licentie en land of regio.

## Wat u na het lezen wilt begrijpen {#learning-outcomes}

Nadat u dit onderwerp leest, zou u het volgende moeten kunnen doen.

1. Beschrijf het platform zelf — leg uit wat [!DNL Adobe Experience Platform] doet als gedeelde basis voor gegevens en gegevensregels. U kunt dit uitleggen zonder een specifieke toepassing een naam te geven.
2. Beschrijf elke belangrijkste toepassing op zich — Zeg welk bedrijfsdoel elke toepassing steunt en welk type van werk het is.
3. Beschrijf hoe het platform en de toepassingen samen passen — verklaar hoe de klantenprofielen, identiteiten, gegevensvormen (schema&#39;s), en gegevensregels zich van het platform in toepassingen bewegen. Verklaar waarom de teams geen afzonderlijke, conflicterende gegevenspijpleidingen voor elk hulpmiddel moeten bouwen.
4. Verbind een doel met het juiste deel van de oplossing — Voor een steekproefdoel (bijvoorbeeld &quot;looppas op instapweigering over e-mail en mobiel&quot;), noem welke delen van het platform en welke toepassingen gewoonlijk dat doel steunen.

In dit onderwerp, betekent &quot;uw doelstellingen&quot;wat uw organisatie (bijvoorbeeld de groei, de efficiency, of het klantenvertrouwen) wil. &quot;Uw klanten&quot; betekent mensen die met uw merk communiceren. Het platform en de toepassingen bestaan om uw teams te helpen die klanten dienen.

## Wie moet dit onderwerp lezen? {#who-should-read}

| Uw rol | Hoe helpt dit onderwerp |
|-----------|------------------------|
| Zakelijke en marketingleiders | Verbind klant en merkdoelstellingen met platformeigenschappen en toepassingen. Gebruik dezelfde woorden als uw technische teams. |
| Personen die marketingactiviteiten, analyses of ervaring met klanten uitvoeren | Zie waar de gegevens bij elkaar komen, waar de keuzen worden gemaakt, en welke toepassing past welke stap. |
| Architecten, ingenieurs en ontwikkelaars | Gebruik hetzelfde eenvoudige model en dezelfde termen als de rest van [!DNL Experience League] wanneer u ontwerpt of bouwt. |

## Hoe [!DNL Adobe Experience Platform] zelfstandig werkt {#platform-alone}

[!DNL Adobe Experience Platform] is de basislaag voor gegevens van de klantenervaring. Het is geen enkel marketingscherm. Het is gebaseerd op services die op de achtergrond worden uitgevoerd. Voordat u een toepassing opent, kan het platform het volgende doen.

| Wat het platform doet | Waarom dit u helpt |
|--------------------------|---------------------|
| Hiermee worden gegevens van websites, apps en bedrijfssystemen (in bestanden of als een live stream) ingevoerd | U blijft niet vastzitten met één kanaal of één database. In de loop der tijd kunt u een vollediger weergave maken. |
| Structueert gegevens met schema&#39;s die op het Model van de Gegevens van de Ervaring (XDM) worden gebaseerd zodat delen de gebeurtenissen en de gebieden één betekenis | Teams die gegevens analyseren, een publiek sturen en controleren of ze aan de normen voldoen, gebruiken allemaal dezelfde definities. Dat vermindert fouten en herhaalt werk. |
| Koppelingsidentiteiten zodat binnen uw regels dezelfde persoon of account kan worden herkend op verschillende apparaten en systemen | De teams kunnen van één mening van de klant werken waar het beleid toestaat. |
| Houdt [!DNL Real-Time Customer Profile] bij als live weergave voor beslissingen en het verzenden van gegevens | Keuzen kunnen huidige gegevens gebruiken, niet alleen een oud bestand van gisteren. |
| Bouwt soorten publiek (segmentatie) van profielgegevens, gedrag, en toestemming | U bepaalt wie op één plaats wordt opgenomen. In andere stappen wordt die logica opnieuw gebruikt. |
| Verstuurt gegevens naar bestemmingen (exporteren en verbonden systemen) en past gegevensregels toe via labels, beleidsregels en [!DNL Privacy Service] | Teams kunnen sneller bewegen terwijl ze de toestemming en de wet volgen. |

Kortom, het platform verenigt klantgegevens, past regels toe en bereidt gegevens voor gebruik voor. Het vervangt niet de volledige schermen die de toepassingen voor reisontwerp, media werkschema&#39;s, of dwars-kanaalrapporten verstrekken. Toepassingen bieden deze ervaringen.

### Platformservices in één oogopslag {#core-platform-services}

| Gebied | Wat het op de basislaag doet |
|------|--------------------------------|
| Gegevensverzameling ([!DNL Tags] , [!DNL Experience Platform Web SDK] , [!DNL Experience Platform Mobile SDK] , gegevensstreams) | Gegevens op een standaardmanier verzamelen uit digitale ervaringen. |
| Bronnen en gegevens invoeren | Verbind gegevens van bedrijfssystemen en wolkenbronnen met het platform. |
| XDM en schema&#39;s | De structuur en betekenis van ervaringsgegevens instellen. |
| [!DNL Identity Service] | Verbind herkenningstekens in één mening binnen beleid. |
| [!DNL Real-Time Customer Profile] | Houd het actieve profiel dat wordt gebruikt voor beslissingen en het verzenden van gegevens. |
| Segmentatie | Bepaal publiek van profielgegevens en gebeurtenissen. |
| Bestemmingen | Verzend publiek en attributen naar andere systemen die marketing of de dienst in werking stellen. |
| Gegevensbeheer, [!DNL Privacy Service] toestemming | Bepaal hoe gegevens kunnen worden gebruikt. |
| [!DNL Data Science Workspace] | Stel modellen voor machinetolken samen, trainen en uitvoeren op basis van platformgegevens. Dit is een platformfunctie, geen toepassing. |
| [!DNL Query Service] | Voer SQL uit op Experience Platform-gegevens voor analyse en rapportage. Dit is een platformservice, geen toepassing. |

Deze gebieden ondersteunen een eenvoudige stroom: verzamelen → verenigen → besluiten → activeren → meten. De gegevensregels zijn bij elke stap van toepassing.

## Hoe toepassingen zelfstandig werken {#applications-alone}

Een korte lijst van elke toepassing en zijn belangrijkste doel is in [ wat de toepassingen zijn, en het belangrijkste doel van elk ](#applications-at-a-glance). In de onderstaande tabel vindt u meer informatie. Hierin wordt aangegeven wat elke toepassing afzonderlijk doet en welk doel de toepassing ondersteunt.

Toepassingen zijn gebruikerservaring en workflows op het platform. Elk onderdeel helpt uw teams een hoofdtype werk te doen. Allemaal tekenen ze uit hetzelfde profiel en dezelfde gegevensregels. Teams hoeven niet de volledige gegevensstapel voor elk gereedschap te kopiëren.

| Toepassing | Wat zij zelfstandig doet (hoofdbaan) | Welk doel het helpt u bereiken |
|-------------|-------------------------------------|------------------------------|
| [[!DNL Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/home) | Beheer publiek en activering: maak segmenten, werk vaak lidmaatschap bij, verzend publiek en attributen naar bestemmingen. Biedt ondersteuning voor consumenten, bedrijven en gevallen van gemengd gebruik, afhankelijk van uw licentie. | Bereik de juiste mensen en sluit de verkeerde op betaalde, bezeten, en partnerkanalen uit gebruikend uw eigen verenigde klantengegevens. |
| [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/en/docs/journey-optimizer) | De reizen van het ontwerp en verzenden berichten: reactie op gebeurtenissen, takwegen, en verzend over kanalen van één reiswerkruimte. | Voer gepersonaliseerde reeksen uit (bijvoorbeeld op instapniveau, behoud of service follow-up) die reageren op wat de klant zojuist heeft gedaan. |
| [[!DNL Customer Journey Analytics]](https://experienceleague.adobe.com/en/docs/customer-journey-analytics) | Reizen en campagneresultaten rapporteren en analyseren met behulp van één gegevensbasis. | Bekijk wat er gebeurd is en waarom er langs verschillende kanalen heen is, zodat u uw uitgaven en ervaring kunt verbeteren. |
| [[!DNL Adobe Mix Modeler]](https://experienceleague.adobe.com/en/docs/mix-modeler) | Combineer platform-verbonden gegevens met modellen om kanalen te meten en planningsscenario&#39;s in werking te stellen. | Plan en pas marketing uitgaven met een gestage mening van hoe kanalen en andere factoren resultaten beïnvloeden aan. |

Kortom, toepassingen zijn de manier waarop teams hun dagelijkse werk doen (activering, reizen, analyse, marketing meting). Het platform is wat de klantengegevens en de regels houdt die elk van die teams vertrouwen. Het platform biedt ook vragen en geavanceerde modellering door de diensten hierboven aan.

>[!IMPORTANT]
>
>Welke toepassingen u kunt gebruiken, is afhankelijk van uw Adobe-licentie. De eigenschappen, de grenzen, en de beschikbaarheid kunnen veranderen. Controleer uw contract en de meest recente [!DNL Experience League] documentatie.

## De manier waarop het platform en de toepassingen samenwerken {#platform-and-apps-together}

Als we zeggen dat platform en toepassingen samenwerken, bedoelen we drie dingen.

1. Eén klantprofiel, vele producten — [!DNL Real-Time Customer Profile], [!DNL Identity Service] en gegevensregels worden gedeeld. [!DNL Real-Time CDP] , [!DNL Adobe Journey Optimizer] , [!DNL Customer Journey Analytics] en [!DNL Adobe Mix Modeler] lezen vanuit dezelfde basis (en verwante gegevens). U kunt slechts één klantlijst voor analyses en een andere lijst voor marketing bijhouden wanneer uw proces dit vereist.
2. Eén betekenis van wat er gebeurde — Gegevens worden gevormd met XDM-schema&#39;s. Dezelfde gebeurtenis kan de rapportage, reizen en publieksregels doorgeven. Teams besteden minder tijd aan discussiëren over definities.
3. Één plaats voor gegevensregels — De Etiketten en het beleid zijn op de gegevens van toepassing die de toepassingen gebruiken. Gegevensregels worden niet alleen later toegevoegd in elk gereedschap.


### End-to-end flows (hoe werk wordt uitgevoerd op platform en apps) {#end-to-end-flows}

| Stadium | Wat het platform doet | Gewoonlijk toevoegen aan toepassingen |
|-------|----------------------------|-------------------------------------|
| Know | Gegevens invoeren, structureren, koppelen, identiteit koppelen, profiel bijwerken | Toepassingen lezen Profiel en gebeurtenissen. Ze vervangen niet de stap om gegevens in te voeren. |
| Beslissen | Bouw segmenten en controleer wie het gebruiken verenigde gegevens kwalificeert | [!DNL Real-Time CDP] voor het opbouwen van publiek. [!DNL Adobe Journey Optimizer] voor reispaden en de volgende beste actie in context. |
| Activeren | Doelen en gecontroleerde uitvoer van soorten publiek en kenmerken | [!DNL Real-Time CDP] ondersteunt veel activeringspatronen. De reizen verzenden berichten door de kanalen u opstelling. |
| Meetlat | Gebeurtenissen en identiteiten die één model in de gegevenslaag volgen | [!DNL Customer Journey Analytics] voor reis- en campagnerapportage. [!DNL Adobe Mix Modeler] voor uniforme marketing meting en planning die platform-verbonden gegevens gebruikt. |

## Voorbeeld: één workflow die gebruikmaakt van het platform en alle vier toepassingen {#example-full-stack-workflow}

Het onderstaande artikel is een gemeenschappelijk patroon. Uw teams kunnen de volgorde wijzigen of een stap overslaan. Het doel is te laten zien hoe [!DNL Adobe Experience Platform] en [!DNL Real-Time CDP] , [!DNL Adobe Journey Optimizer] , [!DNL Customer Journey Analytics] en [!DNL Adobe Mix Modeler] allemaal in hetzelfde programma kunnen worden weergegeven.

### Het scenario {#example-scenario}

Een handelsmerk voert een seizoensgebonden acquisitie- en instapprogramma uit. Leiderschap wil uitgaven plannen, nieuwe kopers bereiken met betaalde media, nieuwe klanten verwelkomen met berichten en rapporteren over resultaten. Het merk gebruikt verenigde klantgegevens op [!DNL Adobe Experience Platform].

### Wat gebeurt er in de workflow? {#example-steps}

1. [!DNL Adobe Experience Platform] (het platform)\
   Teams brengen web- en toepassingsgebeurtenissen, bestellingen, toestemming en kosten- of prestatiegegevens van advertenties in, voor zover beschikbaar. Gegevens gebruiken gedeelde XDM-schema&#39;s. [!DNL Identity Service] koppelt bekende klanten. [!DNL Real-Time Customer Profile] wordt bijgewerkt terwijl mensen winkelen en zich aanmelden. Gegevensregels en toestemming worden op het platform opgeslagen.\
   *Zonder deze stap, hebben de toepassingen hieronder niets betrouwbaar te lezen.*

2. [!DNL Adobe Mix Modeler]\
   Marketing en financiën evalueren hoe kanalen bijdragen aan verkoop en hoe het budget over de media voor het seizoen kan worden verdeeld. Zij gebruiken modellen en planningsmeningen die op geharmoniseerde marketing en resultaatgegevens voortbouwen verbonden aan het platform.\
   *Deze stap beantwoordt &quot;hoe wij&quot;op een planningsniveau moeten investeren. Het verzendt geen e-mail of bouwt geen publiek van dag tot dag op zich.*

3. [!DNL Real-Time CDP]\
   Overnameteams bouwen een publiek (bijvoorbeeld kopers of mensen die objecten in een winkelwagentje hebben achtergelaten). Ze activeren die doelgroepen naar reclame en andere bestemmingen. Zij kunnen ook onderdrukkingspubliek bouwen zodat worden de huidige klanten niet gericht als vooruitzichten.\
   *deze stap antwoordt &quot;wie wij in betaalde en bezeten kanalen zouden moeten bereiken of uitsluiten.&quot;*

4. [!DNL Adobe Journey Optimizer]\
   Levenscyclusteams voeren een welkomstreis uit na een aankoop of aanmelding. Tijdens de reis wordt geluisterd naar profiel- of gebeurtenisvoorwaarden, filialen (bijvoorbeeld eerste aankoop versus herhalen) en worden e-mail- of mobiele berichten verzonden.\
   *deze stap beantwoordt &quot;welk bericht of weg deze persoon volgende krijgt.&quot;*

5. [!DNL Customer Journey Analytics]\
   Analyseteams bouwen rapporten en dashboards op het volledige pad, van touch to purchase and onboarding. Zij meten trechters, kanalen, en segmenten gebruikend de zelfde gebeurtenis en profiel-gesteunde definities de zaken elders gebruiken.\
   *deze stap beantwoordt &quot;wat in de reis gebeurde en welke delen werkten.&quot;*

Teams voeren vaak stap 2 tot en met 5 parallel uit over een kwart. Mix Modeler-updates kunnen langzamer plaatsvinden dan live publiek of reizen. Dat is normaal.

### De manier waarop toepassingen samenwerken {#example-together}

- Eén profiel en één gebeurtenismodel. Dezelfde persoon en dezelfde gebeurtenissen lopen van het platform over in [!DNL Real-Time CDP] , [!DNL Adobe Journey Optimizer] en [!DNL Customer Journey Analytics] . Mix Modeler gebruikt verbonden en geharmoniseerde gegevens van het platform. Het kan samenvattingen (bijvoorbeeld wekelijkse uitgaven) evenals gebeurtenis-vlakke gegevens, afhankelijk van opstelling gebruiken.
- Andere banen, dezelfde waarheid. [!DNL Real-Time CDP] duwt wie te bereiken. [!DNL Adobe Journey Optimizer] voert uit wat er na een actie gebeurt. In [!DNL Customer Journey Analytics] wordt weergegeven wat er in de verschillende stappen is gebeurd. [!DNL Adobe Mix Modeler] biedt ondersteuning voor het verschuiven van het budget op een hoger niveau.
- De gegevensregels reizen met de gegevens. De etiketten en de toestemming op het platform beïnvloeden welke profielen in segmenten, reizen, en rapportering kunnen worden gebruikt.

### Waarschuwing bij configuratie {#example-gotchas}

>[!IMPORTANT]
>
>Deze kwesties veroorzaken verwarring bij echte projecten. Behandel ze als controlepunten voor uw architecten en beheerders.

| Gebied | Wat u moet controleren |
|------|----------------|
| Identiteit | Als web, app en CRM verschillende id&#39;s of naamruimte-instellingen verzenden, kan het profiel één persoon in twee splitsen. Segmenten, reizen en rapporten komen niet overeen. Lijn identiteitsregels en primaire id&#39;s uit voordat u de activering schaalt. |
| Regels voor instemming en gegevens | Als de gegevenssets die worden gebruikt in [!DNL Real-Time CDP] of [!DNL Adobe Journey Optimizer] niet correct zijn gelabeld of goedgekeurd, kunt u de personen die u niet moet activeren of een melding weergeven. Controleer labels, beleidsregels en toestemmingsvelden op dezelfde gegevenssets die u voor publiek en reizen gebruikt. |
| [!DNL Real-Time CDP] en [!DNL Adobe Journey Optimizer] tegelijkertijd | Dezelfde persoon kan in een actief publiek en op een reis zitten. U kunt dubbel-bericht of conflict met aanbiedingen als u geen suppressielijsten, de filters van de reisingang, of duidelijke regels voor wie een reis ingaat. Coördineer eerst de teams en test eerst in een zandbak. |
| [!DNL Customer Journey Analytics] definities | Rapporten gebruiken [!UICONTROL Data views] en metrische regels. Als deze definities niet overeenkomen met de gebeurtenissen of kenmerken die uw marketers in [!DNL Real-Time CDP] of [!DNL Adobe Journey Optimizer] gebruiken, zijn dashboards het niet eens met campagnerapporten. Dimensies en metrische definities uitlijnen met belanghebbenden. |
| [!DNL Adobe Mix Modeler] timing en gegevensvorm | Mix-modellering maakt vaak gebruik van geharmoniseerde of opgerold ingere ingangen en geplande vernieuwingen. Verwacht niet hetzelfde real-time antwoord als [!DNL Real-Time Customer Profile] . De gegevens over de uitgaven en de resultaten moeten in harmonisering in kaart worden gebracht en worden schoongemaakt. Onjuiste toewijzingen maken kanaalkrediet en begrotingsadvies scheef. |
| Mix Modeler vergeleken met Journey Analytics | Mix Modeler richt zich op de bijdrage en planning op kanaalniveau. [!DNL Customer Journey Analytics] richt zich op reiswegen en segmenten. Ze beantwoorden verwante maar verschillende vragen. Dwing één KPI niet om andere zonder een gedocumenteerde brug aan te passen. |
| Sandboxes | Configuratie in een sandbox wordt niet automatisch naar de productie verplaatst. Plan een bevorderingsproces voor schema&#39;s, segmenten, reizen, en verbindingen. |
| Tijdzones | Voor reizen, rapportagevensters en advertentieplatforms kunnen verschillende tijdzones worden gebruikt. Verkeerd uitgelijnde vensters veroorzaken &quot;verkeerde&quot;aantallen en gebroken reisingang. |

### Afvoerkanalen en beperkingen {#example-guardrails}

Adobe publiceert handleidingen voor [!DNL Adobe Experience Platform] en voor elke toepassing. De begeleiding beschrijft grenzen, verwachte prestaties, en veilige waaiers voor configuratie. Ze helpen u fouten, vertragingen of instabiel gedrag te voorkomen. Guardrails zijn geen serviceniveau-overeenkomsten (SLA&#39;s). Ze garanderen geen snelheid of uptime in juridische zin.

In uw contract, productbeschrijving en verkooporder kunnen contractuele limieten of rechten worden vastgelegd. Deze regels kunnen afwijken van de algemene documentatie. In geval van twijfel kunt u de overeenkomst en het Adobe-accountteam samen met [!DNL Experience League] gebruiken.

| Onderwerp | Wat moet u plannen? |
|-------|------------------|
| Zachte limieten en harde limieten | Sommige limieten zijn richtlijnen. Als je ver voorbij ze gaat, kunnen de prestaties dalen of de latentie toenemen. Andere limieten worden vastgesteld door het systeem of door uw contract. U kunt deze waarden niet overschrijden zonder dat u de instellingen of aankopen wijzigt. |
| Waar grenswaarden gelden | Er gelden veel limieten op organisatieniveau, niet per sandbox. Sandboxomgevingen hebben vaak kleinere uiteinden dan productie. Testresultaten in een sandbox geven mogelijk geen prestaties op volledige schaal weer. |
| Opname en profiel | Het volume van de hoge gebeurtenis, het identiteitsvolume, of het profieltellingen beïnvloeden kosten, snelheid, en stabiliteit. Volg de instructies voor het opnemen van gegevens en Profiel wanneer u pijpleidingen ontwerpt. Bij zeer grote doelgroepen of zeer frequente updates kunnen activeringspaden onder druk komen te staan. |
| Segmentering en activering | [!DNL Real-Time CDP] heeft hulplijnen voor segmenten, activering en doelen. De bestemmingen van de partner hebben ook hun eigen kappen, dossiergrootte, of vereiste gebieden. Een segment dat in UI werkt kan bij een bestemming nog ontbreken of beknotten als u beide kanten negeert. |
| [!DNL Adobe Journey Optimizer] | De reizen, de kanalen, en de berichttarieven hebben productgrenzen. Complexe reizen of grote volumes moeten worden gecontroleerd aan de hand van [!DNL Adobe Journey Optimizer] instructies, zodat de berichten betrouwbaar blijven. |
| [!DNL Customer Journey Analytics] | Rapportage heeft limieten op verbindingen, [!UICONTROL Data views], rijen en kardinaliteit. De zware afmetingen of de zeer grote gebeurtenisvolumes vereisen ontwerprevisie zodat blijven de rapporten bruikbaar. |
| [!DNL Adobe Mix Modeler] | Modellering en planning hangen af van voldoende geschiedenis en schone geharmoniseerde gegevens. Er zijn productgrenzen op datasets, modellen, en vernieuw gedrag. Met dunne of lawaaierige gegevens ontstaan zwakke of instabiele modellen. |
| API&#39;s en automatisering | Programmatische vraag gebruikt tariefgrenzen en quota. Batchtaken die deze limieten negeren, kunnen mislukken of vertragen. |
| Regio&#39;s en beschikbaarheid | Sommige eigenschappen, bestemmingen, of toepassingen zijn niet beschikbaar in elk gebied. Bevestig het gebied voor gegevensresidentie en productbeschikbaarheid alvorens u het volledige werkschema ontwerpt. |

>[!NOTE]
>
>Numerieke limieten en standaardwaarden veranderen in de loop van de tijd. Kopieer de limieten uit dit overzicht niet naar een ontwerpdocument. Gebruik de huidige pagina&#39;s met instructies in [!DNL Experience League] , de gebruiksweergave van uw licentie waar uw organisatie deze pagina&#39;s heeft en uw contract.

### Meer informatie {#where-to-read-guardrails}

* [ Experience Platform en toepassingsgidsen ](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-diagrams/architecture-overview/guardrails) - Overzicht van hoe de gidsen over het platform en de toepassingen werken.
* [ Guardrails voor gegevensopname ](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails) — De productie van de Opname en verwante grenzen.
* [ de guardrails van Real-Time CDP ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview) — Segmenten, activering, en gebruik van Real-Time CDP.
* [ gebruik van de Vergunning ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/data-management-best-practices) — Het beheer van gegevens en de praktijken van het vergunningsgebruik op Experience Platform (waar van toepassing op uw org).

Als uw workflow veel leunt op [!DNL Customer Journey Analytics] , [!DNL Adobe Journey Optimizer] , [!DNL Adobe Mix Modeler] of [!DNL Query Service] , leest u ook de hulplijnonderwerpen voor die producten in de Help bij het product.

## Uw doelen toewijzen aan het platform en aan toepassingen {#goals-map}

In deze tabel kunt u zien wat u wilt, wat het platform biedt en welke toepassingen u helpen.

| Uw doel | Wat moet u van het platform gebruiken? | Wat moet u doen met toepassingen |
|-----------|-------------------------------------|--------------------------------------|
| Eén persoon of account bekijken via kanalen | [!DNL Identity Service], [!DNL Real-Time Customer Profile], XDM | Alle vermelde toepassingen profiteren hiervan. [!DNL Real-Time CDP] en [!DNL Adobe Journey Optimizer] gebruiken profiel voor het verzenden van soorten publiek en reizen. |
| Campagnes en lijsten met up-to-date lidmaatschap uitvoeren | Profiel, segmentatie, doelen, gegevensregels | [!DNL Real-Time CDP] voor de manier waarop publiek wordt verzonden. Doelen dragen beleidscontext. |
| Voer multi-step ervaringen uit die op gedrag reageren | Profiel, livegebeurtenissen, gegevensregels | [!DNL Adobe Journey Optimizer] voor reislogica en berichten. |
| Verslag over reizen en kanalen met overeenkomstige nummers | Gedeelde XDM-gebeurtenissen en -identiteiten | [!DNL Customer Journey Analytics] voor analyse op dezelfde gegevens. |
| Kijk hoe kanalen bijdragen en marketingbudgetten plannen | Verenigde datasets, gegevensregels, gegevens klaar voor modellen | [!DNL Adobe Mix Modeler] voor mix-modellering en uitgavenplanning. |
| Houd marketing en de dienst gericht op klantenfeiten | Profiel, gegevensregels, optionele verbindingen met andere systemen | De manier waarop u verbinding maakt met andere systemen kan variëren. Het platform blijft de basis voor klantgegevens. |

## Rollen en handboeien {#roles-and-handoffs}

| Stadium | Wie is vaak betrokken | Wat ze voornamelijk gebruiken |
|-------|------------------------|----------------------|
| Definitie van betekenis en regels voor gegevens | Beheer van gegevens, juridisch, marketingleiderschap | Schema&#39;s, labels, beleid op het platform |
| Opbouw van verzamelings- en gegevenspijpleidingen | Gegevensingenieurs, marketingtechnologie | [!DNL Tags], SDK&#39;s, bronnen, gegevensprep op het platform |
| Stimulerend publiek en reizen maken | Marketing, CRM, teams voor reizen | Toepassingen ([!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer]) boven op hetzelfde profiel |
| Dag tot dag activeren en uitvoeren | Marketing, media, levenscyclusteams | Doelen, reisrapportage, waarschuwingen |
| Controle en verbetering | Analyse, compatibiliteit, bewerkingen | Auditlogboeken, controleren, dashboards |

## Terminologie {#terminology}

* [!DNL Adobe Experience Platform] — Gedeelde services en functies: gegevens invoegen, gegevensmodellen, [!DNL Identity Service] , [!DNL Real-Time Customer Profile] , segmentatie, doelen, gegevensbeheer, privacy en functies zoals [!DNL Data Science Workspace] en [!DNL Query Service] .
* Toepassingen — Gelicentieerde producten op het platform (bijvoorbeeld [!DNL Real-Time CDP] , [!DNL Adobe Journey Optimizer] , [!DNL Customer Journey Analytics] , [!DNL Adobe Mix Modeler] ) die workflows verpakken voor specifieke taken. Ze zijn niet hetzelfde als platformservices zoals [!DNL Query Service] en [!DNL Data Science Workspace] .

Dit past de manier aan het [ de documentatieoverzicht van Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/documentation/overview) groepeert inhoud.

## Aanvullende bronnen {#additional-resources}

* [ overzicht van Adobe Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/home) — Belangrijkste ingangspunten voor hulp.
* [ de documentatieoverzicht van Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/documentation/overview) — Hoe de hulponderwerpen worden georganiseerd.
* [ Digitale ervaringsblauwdrukken ](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/overview/experience-cloud) — De ontwerpen van het voorbeeld door geval en industrie te gebruiken.

Zie voor praktijkgericht leren zelfstudies en cursussen in [!DNL Experience League] over [!DNL Experience Platform Web SDK] , XDM en schema&#39;s, identiteit, segmentatie en doelen.

>[!NOTE]
>
>Wanneer u dit onderwerp toevoegt aan een Adobe-documentatieopslagplaats, controleert u `exl-id`, `feature` en `topic` op uw repo-regels. Vervang de tijdelijke aanduiding `exl-id` in de YAML-koptekst als in uw werkstroom een nieuwe id wordt toegewezen.
