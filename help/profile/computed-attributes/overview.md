---
title: Overzicht van berekende kenmerken
description: Berekende kenmerken zijn functies om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---

# Overzicht van berekende kenmerken

Personalization op basis van gebruikersgedrag is een belangrijke vereiste voor marketers om het effect van personalisatie te maximaliseren. U kunt bijvoorbeeld marketingberichten aanpassen met het meest recent bekeken product om de conversie te stimuleren, of de webpagina aanpassen op basis van de totale aankopen die gebruikers hebben gedaan om het retoucheren te stimuleren.

Met behulp van berekende kenmerken kunnen gedragsgegevens van profielen snel worden omgezet in geaggregeerde waarden op profielniveau zonder afhankelijk te zijn van technische bronnen voor:

- Het toelaten van gerichte één-aan-één of partijverpersoonlijking met activering van gedragsaggregaten aan de bestemmingen van Real-Time Customer Data Platform en gebruik in Adobe Journey Optimizer
- Vereenvoudigde publiekssegmentatie met opslag van gedragsaggregaten als profielkenmerken
- Standaardisering van geaggregeerde profielgedragsgegevens voor gebruik op verschillende platforms en toepassingen
- Beter gegevensbeheer met consolidatie van gegevens van gebeurtenissen met een oud profiel in betekenisvolle gedragsinzichten

Deze aggregaten worden berekend op basis van de gegevenssets voor gebeurtenissen met profiel die in Adobe Experience Platform worden ingevoerd. Elk gegevens verwerkt attribuut is een profielattribuut dat op uw schema van de profielunie wordt gecreeerd, en is gegroepeerd onder de &quot;SystemComputedAttribute&quot;gebiedsgroep in uw unieschema.

Voorbeelden van gebruiksgevallen zijn:

- E-mails met totale bonuspunten aanpassen om gebruikers te feliciteren met hun promotieniveau
- Communicatie aan gebruikers aanpassen op basis van aankooptellingen en frequentie
- E-mails met abonnementen aanpassen op basis van vervaldatums van abonnementen
- Opnieuw gericht gebruikers die een product hebben bekeken maar niet gekocht met het laatst bekeken product
- Gebeurtenisaggregaten activeren via berekende kenmerken op een downstreamsysteem met Real-Time CDP Destination
- Meerdere, op gebeurtenissen gebaseerde doelgroepen samenvouwen tot een meer versmalde groep met berekende kenmerken
- Niet-geverifieerde gebruikers offsite opnieuw toewijzen met behulp van recente partner-id&#39;s uit gebeurtenissen

Deze handleiding helpt u om de rol van berekende kenmerken in Experience Platform beter te begrijpen, en om de basisbeginselen van berekende kenmerken uit te leggen.

## Berekende kenmerken begrijpen

Met Adobe Experience Platform kunt u eenvoudig gegevens uit meerdere bronnen importeren en samenvoegen om [!DNL Real-Time Customer Profiles] te genereren. Elk profiel bevat belangrijke informatie met betrekking tot een persoon, zoals zijn contactgegevens, voorkeuren en aankoopgeschiedenis, die een 360 graden mening van de klant verstrekken.

Een deel van de informatie die in het profiel wordt verzameld, is gemakkelijk te begrijpen wanneer de gegevensvelden rechtstreeks worden gelezen (bijvoorbeeld &quot;voornaam&quot;), terwijl andere gegevens meerdere berekeningen vereisen of op andere velden en waarden vertrouwen om de informatie te genereren (bijvoorbeeld &quot;totaal voor levenslange aanschaf&quot;). Om deze gegevens in één oogopslag begrijpelijker te maken, kunt u in [!DNL Experience Platform] berekende kenmerken maken die deze verwijzingen en berekeningen automatisch uitvoeren en de waarde in het juiste veld retourneren.

De berekende attributen omvatten het creëren van een uitdrukking, of &quot;regel&quot;, die op inkomende gegevens werkt en de resulterende waarde in een profielattribuut opslaat. Expressies kunnen op meerdere verschillende manieren worden gedefinieerd, zodat u kunt opgeven op welke gebeurtenissen moet worden geaggregeerd, welke functies moeten worden geaggregeerd of hoe lang de zoekopdracht moet duren.

### Functies

Met berekende kenmerken kunt u gebeurtenisaggregaten zelf definiëren door vooraf gedefinieerde functies te gebruiken. De details over deze functies zijn hieronder te vinden:

| Functie | Beschrijving | Ondersteunde gegevenstypen | Voorbeeldgebruik |
| -------- | ----------- | -------------------- | ------------- |
| SUM | Een functie die **&#x200B;**&#x200B;omhoog de gespecificeerde waarde voor gekwalificeerde gebeurtenissen sommen. | Gehele getallen, getallen en nummers | Totaal van alle aankopen in de afgelopen 7 dagen |
| TELLEN | Een functie die **&#x200B;**&#x200B;telt het aantal gebeurtenissen die voor de bepaalde regel zijn voorgekomen. | N.v.t. | Aantal aankopen in de laatste drie maanden |
| MIN | Een functie die de **minimum** waarde voor de gekwalificeerde gebeurtenissen vindt. | Gehele getallen, getallen, nummers, tijdstempels | Eerste aankoopgegevens in de laatste 7 dagen <br/> Minimumorderbedrag in de laatste 4 weken |
| MAX | Een functie die de **maximum** waarde voor de gekwalificeerde gebeurtenissen vindt. | Gehele getallen, getallen, nummers, tijdstempels | Laatste aankoopgegevens in de laatste 7 dagen <br/> Maximumorderbedrag in de laatste 4 weken |
| MOST_RECENT | Een functie die de opgegeven kenmerkwaarde van de meest recente gekwalificeerde gebeurtenis vindt. Deze functie geeft **zowel** de waarde evenals timestamp van de attributen. | Alle primitieve waarden, arrays met primitieve waarden | Laatste product bekeken in de afgelopen 7 dagen |

### Termijnen voor opzoeken

De berekende attributen worden berekend in partijen, die u uw aggregaten en het gebruiken van de recentste gebeurtenissen vers laten houden. Om deze scenario&#39;s met minimale vertraging te steunen, verfrist frequentie afhankelijk van de periode van de gebeurtenisraadpleging varieert.

De terugkijkperiode verwijst naar de hoeveelheid tijd die wanneer het samenvoegen van de Gebeurtenissen van de Ervaring voor het gegevens verwerkte attribuut wordt herzien. Deze periode kan in uren, dagen, weken, of maanden worden bepaald.

De vernieuwingsfrequentie verwijst naar de frequentie waarmee de berekende kenmerken worden vernieuwd. Deze waarde is afhankelijk van de terugzoekperiode en wordt automatisch ingesteld.

| Opzoekperiode | Frequentie vernieuwen |
| --------------- | ----------------- |
| Tot 24 uur | Uur |
| Tot 7 dagen | Dagelijks |
| Tot 4 weken | Wekelijks |
| Tot 6 maanden | Maandelijks |

Als uw berekende kenmerk bijvoorbeeld een terugzoekperiode van de laatste 7 dagen heeft, wordt deze waarde berekend op basis van de waarden van de laatste 7 dagen en vervolgens dagelijks vernieuwd.

>[!NOTE]
>
>Zowel worden de weken als de maanden beschouwd als **kalenderweken** en **kalendermaanden** wanneer gebruikt in gebeurtenisraadplegingen. De kalenderweek begint op de **Zondag** en beëindigt op de **Zaterdag** van de week. De kalendermaand begint op **eerste** van de maand en beëindigt op de **laatste dag** van de maand.

De raadplegingsperiode voor gegevens verwerkte attributen is a **het rollen** raadplegingsperiode. Als bijvoorbeeld een eerste evaluatie plaatsvindt op 15 oktober om 12 uur &#39;s middags UTC, zou de terugzoekperiode van twee weken alle gebeurtenissen ophalen van 1 oktober tot 15 oktober, vernieuwen in één week op 22 oktober en vervolgens alle gebeurtenissen ophalen van 8 oktober tot 22 oktober.

**snel verfrist zich** {#fast-refresh}

Met Snel vernieuwen kunt u uw kenmerken up-to-date houden. Als u deze optie inschakelt, kunt u uw berekende kenmerken dagelijks vernieuwen, zelfs voor langere terugzoekperiodes, zodat u snel kunt reageren op gebruikersactiviteiten.

>[!NOTE]
>
>Als u snel vernieuwt inschakelt, varieert de terugzoekduur van de gebeurtenis, aangezien de terugzoekperiode wekelijks of maandelijks wordt teruggedraaid.
>
>Als u een gegevens verwerkt attribuut met een twee-week raadplegingsperiode met snel creeert toegelaten verfrist zich, betekent dit dat de aanvankelijke raadplegingsperiode twee weken zal zijn. Nochtans, met elke dag verfrist zich, zal de raadplegingsperiode gebeurtenissen van de extra dag omvatten. Deze toevoeging van dagen gaat door tot de volgende kalenderweek begint, waarin het terugkijkvenster zal rollen en aan twee weken terugkeren.
>
>Als er bijvoorbeeld een terugzoekperiode van twee weken was die op 15 maart (zondag) begon en de functie voor snel vernieuwen ingeschakeld is, en dagelijks vernieuwt, blijft de terugzoekperiode inclusief tot 22 maart, waar deze weer op twee weken wordt ingesteld. Kortom, wordt het gegevens verwerkte attribuut **verfrist** dagelijks, met de raadplegingsperiode die van **twee** weken aan **drie** weken tijdens de week stijgt, en dan terugkeert terug naar **twee** weken.

## Volgende stappen

Om meer over het creëren van en het beheren van gegevens verwerkte attributen te leren, te lezen gelieve de [ gegevens verwerkte handleiding van attributen API ](./api.md) of [ gegevens verwerkte attributen UI gids ](./ui.md).
