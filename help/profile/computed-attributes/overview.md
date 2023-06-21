---
title: Overzicht van berekende kenmerken
description: Berekende kenmerken zijn functies om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt.
badge: "Bèta"
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Overzicht van berekende kenmerken

>[!IMPORTANT]
>
>De berekende kenmerken staan momenteel in **bèta** en is **niet** beschikbaar voor alle gebruikers.

Personalisatie op basis van gebruikersgedrag is een belangrijke vereiste voor marketers om het effect van personalisatie te maximaliseren. U kunt bijvoorbeeld marketingberichten aanpassen met het meest recent bekeken product om de conversie te stimuleren, of de webpagina aanpassen op basis van de totale aankopen die gebruikers hebben gedaan om het retoucheren te stimuleren.

Met behulp van berekende kenmerken kunnen gedragsgegevens van profielen snel worden omgezet in geaggregeerde waarden op profielniveau zonder afhankelijk te zijn van technische bronnen voor:

- Het toelaten van gerichte verpersoonlijking met activering van gedragsaggregaten aan de bestemmingen van Real-time Customer Data Platform, gebruik in Adobe Journey Optimizer, of in segmentatie
- Standaardisering van geaggregeerde profielgedragsgegevens voor gebruik op verschillende platforms en toepassingen
- Beter gegevensbeheer met consolidatie van gegevens van gebeurtenissen met een oud profiel in betekenisvolle gedragsinzichten

Deze aggregaten worden berekend op basis van de gegevenssets voor gebeurtenissen met profiel die in Adobe Experience Platform worden ingevoerd. Elk gegevens verwerkt attribuut is een profielattribuut dat op uw schema van de profielunie wordt gecreeerd, en is gegroepeerd onder &quot;Berekend Attribuut&quot;gebiedsgroep in uw unieschema.

Voorbeelden van gebruiksgevallen zijn het personaliseren van advertenties met de naam van het laatst weergegeven product voor mensen die de afgelopen 7 dagen geen aankopen hebben gedaan, het personaliseren van marketinge-mails met totale bonuspunten waarmee gebruikers worden gefeliciteerd met hun promotie naar een Premium-niveau, of het berekenen van de levensduurwaarde van elke klant om een betere doelgerichtheid te bereiken.

Deze handleiding helpt u om de rol van berekende kenmerken in het Platform beter te begrijpen, en om de grondbeginselen van berekende kenmerken uit te leggen.

## Berekende kenmerken begrijpen

Met Adobe Experience Platform kunt u eenvoudig gegevens uit meerdere bronnen importeren en samenvoegen om te genereren [!DNL Real-Time Customer Profiles]. Elk profiel bevat belangrijke informatie met betrekking tot een persoon, zoals zijn contactgegevens, voorkeuren en aankoopgeschiedenis, die een 360 graden mening van de klant verstrekken.

Een deel van de informatie die in het profiel wordt verzameld, is gemakkelijk te begrijpen wanneer de gegevensvelden rechtstreeks worden gelezen (bijvoorbeeld &quot;voornaam&quot;), terwijl andere gegevens meerdere berekeningen vereisen of op andere velden en waarden vertrouwen om de informatie te genereren (bijvoorbeeld &quot;totaal voor levenslange aanschaf&quot;). Om deze gegevens in één oogopslag begrijpelijker te maken, [!DNL Platform] Hiermee kunt u berekende kenmerken maken die deze verwijzingen en berekeningen automatisch uitvoeren en de waarde in het juiste veld retourneren.

De berekende attributen omvatten het creëren van een uitdrukking, of &quot;regel&quot;, die op inkomende gegevens werkt en de resulterende waarde in een profielattribuut opslaat. Expressies kunnen op meerdere verschillende manieren worden gedefinieerd, zodat u kunt opgeven op welke gebeurtenissen moet worden geaggregeerd, welke functies moeten worden geaggregeerd of hoe lang de zoekopdracht moet duren.

### Functies

Met berekende kenmerken kunt u gebeurtenisaggregaten zelf definiëren door vooraf gedefinieerde functies te gebruiken. De details over deze functies zijn hieronder te vinden:

| -functie | Beschrijving | Ondersteunde gegevenstypen | Voorbeeld van gebruik |
| -------- | ----------- | -------------------- | ------------- |
| SUM | Een functie die **sommen** Hiermee wordt de opgegeven waarde voor gekwalificeerde gebeurtenissen opgehaald. | Gehele getallen, getallen en nummers | Totaal van alle aankopen in de afgelopen 7 dagen |
| TELLEN | Een functie die **aantal** het aantal gebeurtenissen dat voor de bepaalde regel is opgetreden. | N.v.t. | Aantal aankopen in de laatste drie maanden |
| MIN | Een functie die de **minimum** waarde voor de gekwalificeerde gebeurtenissen. | Gehele getallen, getallen, nummers, tijdstempels | Gegevens van eerste aankoop in de laatste 7 dagen<br/>Minimumorderbedrag in de afgelopen 4 weken |
| MAX | Een functie die de **maximum** waarde voor de gekwalificeerde gebeurtenissen. | Gehele getallen, getallen, nummers, tijdstempels | Gegevens over laatste aankoop in de afgelopen 7 dagen<br/>Maximumbedrag van de bestelling in de afgelopen 4 weken |
| MOST_RECENT | Een functie de vondst de gespecificeerde attributenwaarde van de recentste gekwalificeerde gebeurtenis. | Alle primitieve waarden, arrays met primitieve waarden | Laatste product bekeken in de afgelopen 7 dagen |

### Termijnen

De berekende attributen worden berekend in partijen, die u uw aggregaten en het gebruiken van de recentste gebeurtenissen vers laten houden. Om deze bijna scenario&#39;s in real time te steunen, verfrist frequentie afhankelijk van de periode van de gebeurtenisterugzoeker varieert.

De terugkijkperiode verwijst naar de hoeveelheid tijd die wanneer het samenvoegen van de Gebeurtenissen van de Ervaring voor het gegevens verwerkte attribuut wordt herzien. Deze periode kan in uren, dagen, weken, of maanden worden bepaald.

De vernieuwingsfrequentie verwijst naar de frequentie waarmee de berekende kenmerken worden vernieuwd. Deze waarde is afhankelijk van de terugzoekperiode en wordt automatisch ingesteld.

| Opzoekperiode | Frequentie vernieuwen |
| --------------- | ----------------- |
| Tot 24 uur | Uurlijks |
| Tot 7 dagen | Dagelijks |
| Tot 4 weken | Wekelijks |
| Tot 6 maanden | Maandelijks |

Als uw berekende kenmerk bijvoorbeeld een terugzoekperiode van de laatste 7 dagen heeft, wordt deze waarde berekend op basis van de waarden van de laatste 7 dagen en vervolgens dagelijks vernieuwd.

>[!NOTE]
>
>Zowel weken als maanden worden beschouwd als **kalenderweken** en **kalendermaanden** bij gebruik in gebeurtenislookbacks.

**Snel vernieuwen**

>[!IMPORTANT]
>
>Maximaal **vijf** Voor kenmerken per sandbox kan snelle vernieuwing zijn ingeschakeld.

Met Snel vernieuwen kunt u uw kenmerken up-to-date houden. Als u deze optie inschakelt, kunt u uw berekende kenmerken dagelijks vernieuwen, zelfs voor langere terugzoekperiodes. Dit staat u toe om in bijna real time aan gebruikersactiviteiten te reageren. Deze waarde is alleen van toepassing op berekende kenmerken met een terugzoekperiode die langer is dan een week.

>[!NOTE]
>
>Als u snel vernieuwt inschakelt, varieert de terugzoekduur van de gebeurtenis, aangezien de terugzoekperiode wekelijks of maandelijks wordt vernieuwd.
>
>Bijvoorbeeld, als u een gegevens verwerkt attribuut met een twee week terugzoekperiode met snel creeert toegelaten verfrist, betekent dit dat de aanvankelijke raadplegingsperiode twee weken zal zijn. Nochtans, met elke dag verfrist zich, zal de raadplegingsperiode gebeurtenissen van de extra dag omvatten. Deze toevoeging van dagen gaat door tot de volgende kalenderweek begint, waarin het terugkijkvenster zal rollen en aan twee weken terugkeren.

## Volgende stappen

Voor meer informatie over het maken en beheren van berekende kenmerken leest u de [API-handleiding voor berekende kenmerken](./api.md) of de [UI-gids voor berekende kenmerken](./ui.md).
