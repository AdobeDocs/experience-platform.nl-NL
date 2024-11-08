---
title: Significante wijzigingen en Audience Forecasting volgen met AI Assistant
description: Leer hoe u AI Assistant kunt gebruiken om belangrijke wijzigingen te controleren en het publiek in Adobe Experience Platform te voorspellen.
badge: Alpha
source-git-commit: 37d2886cc5d7b3a019d23f76973d79547865298b
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Belangrijke wijzigingen en verwachte publieksgroei bewaken met AI Assistant

>[!AVAILABILITY]
>
>Deze functie is in Alpha en is mogelijk niet beschikbaar voor uw organisatie. Neem contact op met het accountteam van uw Adobe als u wilt deelnemen aan het Alpha-programma en toegang wilt krijgen tot deze functie.

In het hedendaagse gegevensgestuurde marketinglandschap zijn tijdige en nauwkeurige inzichten van essentieel belang. Of u nu een zakelijke gebruiker bent of marketingactiviteiten uitvoert, u hebt de mogelijkheid nodig om consistent te communiceren met uw publiek en om snel en ondoordringbaar aanpassingen te maken op basis van duidelijke inzichten. Als u de uitlijning wilt behouden of uw bedrijfsdoelstellingen wilt bereiken, moet u over de informatie beschikken die u kunt gebruiken om efficiënte campagnes te voeren en bronnen te optimaliseren.

U kunt de Medewerker van AI voor Adobe Experience Platform gebruiken om significante veranderingen te controleren en groeiprognoses voor uw publiek en datasetgrootte te verstrekken. U kunt deze informatie dan gebruiken om de integriteit van uw publieksgegevens te verzekeren en toekomstgerichte prognoses aan te bieden om gegeven-geïnformeerde besluitvorming te steunen.

Lees dit document om te leren hoe u significante veranderingen kunt controleren en de publieksgroei en schommelingen kunt voorspellen gebruikend AI Medewerker.

## Belangrijke terminologie en definities {#key-terminology-and-definitions}

Zie de volgende tabel voor een lijst met belangrijke terminologie en de bijbehorende definities.

| Terminologie | Definitie |
| --- | --- |
| Belangrijke wijziging | Een significante verandering is een grote op percentage-gebaseerde verandering in publiek of datasetgrootte, die door specifieke drempels wordt bepaald (bijvoorbeeld, 10% voor grote publiek). Significante wijzigingen helpen anomalieën op te sporen die de gegevensstabiliteit beïnvloeden. |
| Anomalies | Anomalies zijn onverwachte variaties in gegevens, zoals een plotselinge 20% groei in a **High-Value het publiek van de Kopers**. Een anomalie kan worden veroorzaakt door een mogelijk probleem met gegevensinvoer of een wijziging in de definitie van het publiek. |
| Historische gegevens | Historische gegevens hebben betrekking op langetermijngegevens, meestal 1 tot 3 jaar. U kunt historische gegevens gebruiken om patronen bij te houden. **Nota**: Tijdens het stadium van de Alpha, verstrekt AI Medewerker historische gegevens van maximaal 13 maanden. |
| Nieuwe/recente gegevens | Nieuwe of recente gegevens hebben betrekking op gegevenspunten die gedurende een korte periode, doorgaans gedurende een week of tot 30 dagen, zijn waargenomen. U kunt nieuwe of recente gegevens gebruiken om directe tendensen te benadrukken en snelle aanpassingen te maken. |
| Voorspelling | Een prognose is een voorspelling van toekomstige doelgroepen of gegevenssetgrootten op basis van trends uit het verleden. U kunt prognosegegevens gebruiken om planning op lange termijn te steunen. |
| Grootte publiek | De grootte van het publiek verwijst naar het totale aantal profielen binnen een publiek. De grootte van het publiek wordt bijgewerkt met elke herhaling van gegevensopname. |
| Tijdskader voor vergelijking | In de AI-assistent worden vooraf gedefinieerde tijdframes voor de vergelijking gebruikt. Recente anomalieën zijn standaard ingesteld op een 7-daagse terugblik, terwijl anomalieën uit het verleden 30 dagen duren. Historische trends bestrijken maximaal 13 maanden. |

{style="table-layout:auto"}

## Voorbeelden van hoofdletters gebruiken {#use-case-examples}

Het vermogen van AI Assistant om significante wijzigingen en een voorspeld publiek te volgen, kan bijzonder nuttig zijn voor de volgende gebruiksgevallen:

### Marketing

De handelings verrichtingen (marketing ops) beroeps zijn verantwoordelijk voor het verzekeren van de integriteit en de consistentie van publieksgegevens. Als lid van een marketingteam kunt u onder andere de kwaliteit van de gegevens controleren, reageren op onverwachte wijzigingen en een stabiele basis voor alle marketinginspanningen handhaven. U kunt de anomalieopsporing van AI Assistant gebruiken om significante publiek of datasetveranderingen te ontdekken en te richten, daardoor ontwrichtingen te verhinderen die campagneprestaties zouden kunnen beïnvloeden.

### Zakelijke gebruikers en verkopers

Als zakelijke gebruiker en marketeer kunt u op nauwkeurige publieksinzichten vertrouwen om gegevensgestuurde beslissingen te nemen en ervoor te zorgen dat uw campagnes het beoogde publiek effectief bereiken. Met de voorspellingsmogelijkheden van AI Assistant kunt u de groei of reductie van het publiek voorspellen en strategische aanpassingen in bronnen mogelijk maken en u kunt deze in de loop der tijd als doelgroep gebruiken.

## Belangrijkste kenmerken

>[!IMPORTANT]
>
>De volgende kenmerken bevinden zich in Alpha en zijn gericht op basiscapaciteiten bij het monitoren en voorspellen. Aangezien deze functie in Alpha is, moet u ervoor zorgen dat u de reacties tweemaal controleert die u van AI Medewerker voor nauwkeurigheid ontvangt.

### Belangrijke wijzigingen in het publiek en de gegevens controleren

U kunt AI Medewerker gebruiken om significante veranderingen in publiek en datasetgrootte te identificeren door afwijkingen van typische patronen te volgen. Elke significante verandering is gebaseerd op vooraf bepaalde drempels die aan de schaal van het publiek worden aangepast.

| Grootte publiek | Aantal profielen | Beschrijving |
| --- | --- | --- |
| Klein publiek | 1 tot 100.000 profielen | Hiermee wordt een wijziging van 30% of meer gemarkeerd, tenzij een specifiek percentage is opgegeven. |
| Medium-publiek | Profielen van 100.000 tot 500.000 | Hiermee wordt een wijziging van 25% of meer gemarkeerd, tenzij een specifiek percentage is opgegeven. |
| Groot publiek | 500.000 tot 1 miljoen profielen | Hiermee wordt een wijziging van 20% of meer gemarkeerd, tenzij een specifiek percentage is opgegeven. |
| Zeer groot publiek | Meer dan 1 miljoen profielen | Hiermee wordt een wijziging van 10% of meer gemarkeerd, tenzij een specifiek percentage is opgegeven. |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

#### Voorbeeldscenario

Significante wijzigingen wijzen op anomalieën die de stabiliteit van het publiek of de betrouwbaarheid van gegevens kunnen beïnvloeden. Bijvoorbeeld, als a **Hoog-Waarde van de Kopers** publiek een plotselinge 15% daling in grootte ervaart, dan zal AI Medewerker dit als significante verandering markeren. Vervolgens kunt u deze informatie gebruiken om mogelijke problemen te onderzoeken en op te lossen voordat deze van invloed zijn op uw campagnes.

>[!ENDSHADEBOX]

>[!TIP]
>
>In AI Assistant worden belangrijke wijzigingen in de publieksformaten niet automatisch gemeld. U moet een gesprek met AI Assistant beginnen en vragen welk publiek aanzienlijk of met een bepaalde marge is gewijzigd, binnen een bepaalde periode.

### Prognose van het publiek en de groei van gegevenssets

U kunt de Medewerker van AI gebruiken om historische gegevenstrends en project toekomstige publiek en datasetgrootte van verwijzingen te voorzien. U kunt deze inzichten dan gebruiken om uw middelplanning en strategieaanpassingen te steunen. Momenteel, kunt u AI Medewerker gebruiken om publiek en datasetgroei voor 30 dagen te voorspellen. Door verwachte publieksgroei of daling te begrijpen, kunt u het richten strategieën aanpassen en uw middelen dienovereenkomstig toewijzen.

### Inzicht in historische publieksformaten

Naast het ontdekken van significante veranderingen, kunt u AI Medewerker gebruiken om historische inzichten terug te winnen en huidige publiek of datasetgrootte met vroegere gegevens te vergelijken. Deze functie ondersteunt het volgen van langetermijntrends en het beoordelen van de impact van eerdere marketingactiviteiten.

U kunt AI Medewerker vragen stellen zoals: &quot;Wat was de grootte van mijn &quot;Klanten van de Loyalty&quot;publiek vorige maand? historische gegevens te zien over de groei of de achteruitgang van dit specifieke publiek.

## Voorbeeldvragen voor het controleren van belangrijke wijzigingen

U kunt de vragen van uw AI-assistent op verschillende manieren formuleren.

* Als uw vraag een percentage bevat, zoals **&quot;Welk publiek is gewijzigd over 30% of meer?&quot;** gebruikt AI Assistant het percentage als referentiepunt.
* Als in uw vraag geen percentage is opgegeven, worden belangrijke wijzigingen op basis van de standaardinstellingen geïnterpreteerd door de AI Assistant.

Raadpleeg de volgende tabellen voor bijvoorbeeld query&#39;s die laten zien hoe AI Assistant belangrijke wijzigingen interpreteert op basis van de omvang van het publiek:

| Poortinformatie of publiekswijziging | Voorbeeld |
| --- | --- |
| <ul><li>Wat is de huidige grootte van {AUDIENCE_NAME}?</li><li>Toon het publiek dat een wijziging van {PERCENT} over {DATE_DURATION} heeft getoond.</li></ul> | <ul><li>Wat is de huidige grootte van het publiek van High-Value-winkels?</li><li>Toon het publiek dat de afgelopen week een verandering van 20% heeft vertoond.</li></ul> |

{style="table-layout:auto"}

| Publiek-specifieke vragen | Voorbeeld |
| --- | --- |
| <ul><li>Welk publiek is meer gewijzigd dan {PERCENT} in {DATE_OR_DURATION} ?</li><li>Toon me publiek met een significante verandering over {DATE_OR_DURATION}.</li><li>Toon me de verdeling van publiek met de grootste veranderingen over {DATE_OR_DURATION}.</li><li>Toon me publiek dat meer dan {PERCENT} op {DATE_OR_DURATION} is gedaald.</li></ul> | <ul><li>Welk publiek veranderde de afgelopen week meer dan 20%?</li><li>Toon me publiek met een significante verandering in de afgelopen zes maanden.</li><li>Toon me de verdeling van het publiek met de grootste veranderingen van 1 oktober tot 31 oktober.</li><li> Toon mij publiek dat sinds 31 augustus met meer dan 20 procent is gedaald. |

{style="table-layout:auto"}

## Aanvullende informatie

### De drempel voor &quot;belangrijke wijziging&quot; begrijpen

U kunt een specifiek percentage opgeven wanneer u de AI-assistent vraagt om informatie over belangrijke wijzigingen. Als u geen specifiek percentage verstrekt, dan zal AI Medewerker naar een vooraf bepaalde reeks drempels verwijzen om te bepalen wat als significante verandering kwalificeert. De standaarddrempels zijn gebaseerd op de grootte van een bepaald publiek. Raadpleeg de volgende tabel voor informatie over wat een belangrijke wijziging is, op basis van de omvang van het publiek:

| Grootte publiek | Wat is belangrijk? |
| --- | --- |
| 1 miljoen of meer | 10% of meer |
| 500 k tot 1 miljoen | 20% of meer |
| 100 tot 500 k | 25% of meer |
| Minder dan 100 kB | 30% of meer |

### Algemene tijdlijnen en specifieke datums

De Medewerker van AI steunt zowel specifieke als generische op tijd-gebaseerde vergelijkingen voor publieksgrootte, die hen interpreteren op de context wordt gebaseerd die in de vraag wordt verstrekt.

>[!BEGINTABS]

>[!TAB  Algemene chronologie ]

Algemene tijdlijnen verwijzen naar query&#39;s die taal gebruiken zoals &quot;deze week&quot; of &quot;vorige week&quot;. Als u AI Medewerker een vraag zoals stelt, &quot;Welke publiek veranderde met meer dan 20% in de laatste week?&quot;, dan zal AI Medewerker de **gemiddelde publieksgrootte** over de gespecificeerde periode berekenen en vergelijken.

Gebruik deze benadering voor een bredere mening van publieksveranderingen in tijd, die u toestaat om trends binnen wekelijkse of maandelijkse intervallen beter te begrijpen.

>[!TAB  Specifieke data ]

Als uw vraagverwijzingen een specifieke datum, dan zal AI Medewerker de **nauwkeurige publieksgrootte** op elk van uw verstrekte data vergelijken.

Gebruik deze nauwkeurige vergelijking om veranderingen tussen specifieke punten in tijd te analyseren en duidelijkheid te bereiken over hoe de publieksgrootte op bepaalde dagen kan evolueren.

>[!ENDTABS]

U kunt van deze flexibiliteit profiteren om publieksdynamiek over zowel brede als nauwkeurige tijdkaders beter te begrijpen. Of u algemene trends volgt of exacte verschuivingen tussen bepaalde datums onderzoekt, u kunt het adaptieve mechanisme van AI Assistant gebruiken om de meest relatieve vergelijking voor uw query op te halen.

## Veelgestelde vragen {#faq}

Lees deze sectie voor antwoorden op vaak gestelde vragen over het controleren van significante veranderingen en publiek het voorspellen met AI Assistant.

### Hoeveel historische gegevens kan ik bekijken om publieksgrootte te zien stijgt of vermindert?

AI Assistant bevat twaalf maanden historische gegevens over de omvang van het publiek. U kunt vragen stellen over publieksveranderingen binnen dit tijdkader om de groei of dalingspatronen in het afgelopen jaar te begrijpen.

### Hoe ver terug in de geschiedenis kan ik publieksveranderingen zien?

De Medewerker van AI volgt publieksveranderingen van de dag het in uw organisatie wordt toegelaten en gaat zo ver terug aangezien de laatste publieksdefinitie verandert. Zodra toegelaten, controleert AI Medewerker onophoudelijk en registreert definitieveranderingen tot 12 maanden, die toekomstige gegevens het volgen en vergelijking toestaan.

### Hoeveel historische gegevens zijn er nodig voor een prognose?

Er zijn ten minste 30 dagen gegevens nodig om betrouwbare prognoses van de laatste wijziging in de publieksdefinitie te kunnen maken. In bepaalde gevallen, zoals het voorspellen voor [!DNL Black Friday], kan AI Assistant tot 12 maanden historische gegevens nodig hebben.

### Hoe interpreteert de AI Assistant &quot;recent&quot;?

De AI Assistant interpreteert &quot;onlangs&quot; als de laatste zeven dagen. Voor vragen die naar recente veranderingen verwijzen, overweegt AI Assistant gegevens van deze tijdsperiode om trends of verschuivingen te identificeren.

### Hoe vergelijkt de AI Assistant de omvang van het publiek?

Wanneer specifieke datums worden vermeld, vergelijkt AI Assistant de publieksgrootten op die specifieke dagen. Voor meer algemene vragen, zoals die welke naar &quot;laatste drie maanden&quot; of &quot;vorige week&quot; verwijzen, vergelijkt AI Assistant de gemiddelde omvang van die periode met het gemiddelde van de meest recente dag.

### Hoe actueel zijn de publieksgegevens van de AI Assistant?

Het kan 24 tot 48 uur duren voordat AI Assistant gegevens uit Real-time Customer Data Platform vernieuwt. Voor vragen die naar &quot;gisteren&quot; verwijzen, interpreteert AI Assistant dit dus als één dag voordat de meest recente gegevens beschikbaar zijn.

## Functies buiten bereik

De volgende mogelijkheden worden momenteel niet ondersteund:

### Geavanceerde analyse van de hoofdoorzaak

Hoewel AI Assistant belangrijke wijzigingen kan identificeren, kan deze momenteel geen gedetailleerde analyse van de hoofdoorzaak voor deze verschuivingen geven. De toekomstige herhalingen van AI Medewerker zijn bedoeld om te specificeren welke datasets of attributen tot significante veranderingen in uw publiek bijdragen.

### Uitgebreide historische datasetgrootte

Volledige historische tracering van gegevensgrootten wordt momenteel niet ondersteund. Momenteel, verstrekt AI Medewerker publiek en datasetgeschiedenis voor maximaal 13 maanden.