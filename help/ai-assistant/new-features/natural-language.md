---
title: Natuurlijke taalschatting met AI Assistant
description: Leer hoe u de mogelijkheden van AI Assistant voor het schatten van natuurlijke talen gebruikt.
badge: Alpha
source-git-commit: aef3be05ca23abe9ed8275aa562fdd3313a7e2d0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Aanduiding van natuurlijke talen met AI Assistant

>[!AVAILABILITY]
>
>Deze functie is in Alpha en is mogelijk niet beschikbaar voor uw organisatie. Neem contact op met het accountteam van uw Adobe als u wilt deelnemen aan het Alpha-programma en toegang wilt krijgen tot deze functie.

U kunt de mogelijkheden van de Schatting van de Natuurlijke Taal van AI Medewerker voor Adobe Experience Platform gebruiken om publieksgrootte te schatten en publiekseigenschappen te voorspellen die op eenvoudige, conversationele vragen worden gebaseerd. Met deze functie kunt u publieksinzichten toegankelijker en gebruiksvriendelijker maken. Dit kan bijzonder nuttig voor uw zaken en marketing verrichtingen zijn gebruiksgevallen, vooral als u uw publiek dagelijks beheert en op deze inzichten vertrouwt om efficiënte marketing strategieën te vormen.

Met de natuurlijke mogelijkheden van de taalverwerking van AI Assistant kunt u vragen stellen zoals: &quot;Hoeveel profielen heb ik in Californië tussen 25 en 35 jaar&quot; of &quot;Hoeveel klanten van hoge waarde hebben wij?&quot; of zelfs &quot;Welk percentage van mijn publiek zal waarschijnlijk binnen de volgende maand kopen?&quot; AI Assistant interpreteert deze vragen en retourneert schattingen of eigenschapscores die u kunt gebruiken om met gegevens geïnformeerde beslissingen te nemen.

Lees dit document om te leren hoe u de mogelijkheden van AI Assistant voor het schatten van natuurlijke talen kunt gebruiken.

## Belangrijke terminologie en definities {#key-terminology-and-definitions}

Zie de volgende tabel voor een lijst met belangrijke terminologie en de bijbehorende definities.

| Terminologie | Definitie |
| --- | --- |
| Schatting van de omvang van het publiek | Het proces om het aantal leden binnen een specifiek publiek te berekenen dat op een bepaalde criteria wordt gebaseerd. U kunt uw schattingen van de grootte baseren op profielgegevens, inclusief profielen die zich niet in een publiek bevinden. Bovendien, kunt u de schattingen van de publieksgrootte terugwinnen zonder het moeten eerst een publiek creëren. Gebruik dit inzicht om de schaal van uw bereik voor gerichte campagnes te begrijpen. |
| Propensiteitsschatting | Een voorspelling van de waarschijnlijkheid dat leden in een publiek binnen een bepaald tijdsbestek specifiek gedrag vertonen (zoals: een aankoop maken, chatten). Propensiteitsschatting is specifiek voor het publiek in Real-time Customer Data Platform, maar kan profielgegevens bevatten, inclusief profielen bij elk publiek. U kunt naar dit inzicht verwijzen wanneer u uw campagnes optimaliseert en strategieën voor het behoud van het publiek beheert. |
| Verwerking van natuurlijke talen | De capaciteit van AI Assistant om vragen te interpreteren en te antwoorden die in de dagelijkse taal worden gesteld, zodat u conversatie kunt gebruiken en relevante inzichten kunt ontvangen zonder technische vragen te gebruiken. |
| Vooraf gedefinieerde tijdframes | Standaardtijdbereiken (&quot;vorige maand&quot;, &quot;volgende 30 dagen&quot;) ondersteund door AI Assistant voor het schatten van de omvang en eigenschappen van het publiek. **Nota**: De tijdkaders van de douane kunnen niet volledig tijdens het stadium van de Alpha worden gesteund. |
| Opnamegegevens | De gegevensset die door AI Assistant wordt gebruikt om ramingen te verstrekken. Deze gegevens worden elke 24-48 uur door Real-time Customer Data Platform bijgewerkt en daarom weerspiegelen inzichten mogelijk geen realtime wijzigingen in het publiek. |

{style="table-layout:auto"}

## Voorbeelden van hoofdletters gebruiken {#use-case-examples}

De mogelijkheden van AI Assistant voor het schatten van natuurlijke talen kunnen met name nuttig zijn voor de volgende gebruiksgevallen:

### Marketing

Als professionele marketingmanager kunnen uw verantwoordelijkheden het beheren en controleren van publieksgegevens omvatten om ervoor te zorgen dat deze in overeenstemming zijn met uw bedrijfsdoelstellingen. Met de functie voor het schatten van de natuurlijke taal van AI Assistant kunt u snel inzichten verzamelen in de omvang en de eigenschappen van het publiek zonder dat u eerst een publiek of uitgebreide kennis over gegevensanalyse hoeft te maken.

hen helpen een consistente, gegevensgestuurde aanpak in hun workflows te handhaven.

### Zakelijke gebruikers en verkopers

Als zakelijke gebruiker en marketeer kan snelle toegang tot publieksgegevens van cruciaal belang zijn voor het welslagen van uw campagneplanning, -gerichtheid en -evaluatie. Met de functie voor het schatten van de natuurlijke taal van AI Assistant kunt u de toegang tot publieksinformatie vereenvoudigen, eenvoudige vragen stellen en inzichten ontvangen die u kunt gebruiken om uw publiek te helpen bij het maken en optimaliseren van campagnes.

## Belangrijkste kenmerken

>[!IMPORTANT]
>
>De volgende functies zijn in Alpha en zijn gericht op grondmogelijkheden van de schatting van natuurlijke talen. Aangezien deze functie in Alpha is, moet u ervoor zorgen dat u de reacties tweemaal controleert die u van AI Medewerker voor nauwkeurigheid ontvangt.

### Schatting van de omvang van het publiek

U kunt zoekopdrachten in natuurlijke talen gebruiken om AI Assistant te vragen de grootte van specifieke doelgroepen te bepalen. Deze functie kan met name handig zijn om het bereik en de impact van doelgroepen te bepalen. Als marketingstrategist kunt u bijvoorbeeld vragen stellen zoals:

* &quot;Hoeveel profielen wonen er in New York?&quot;
* &quot;Hoeveel profielen heb ik met een e-mail en heb ik goedgekeurd?&quot;

Gebruik deze functie om het schatten van de omvang van het publiek te vereenvoudigen en directe antwoorden te krijgen zonder het moeten complexe gegevensfilters of segmentdefinities navigeren.

### Propensiteitsschatting van het publiek

>[!TIP]
>
>Uw rekening van het Experience Platform moet met [ AI van de Klant ](../../intelligent-services/customer-ai/overview.md) worden voorzien om de mogelijkheden van de de bezitsraming van AI Medewerker te gebruiken.

U kunt de schatting van de doeldichtheid gebruiken om de waarschijnlijkheid van specifieke gedragingen of acties binnen een publiek te bepalen. U kunt bijvoorbeeld vragen stellen zoals:

* &quot;Welk percentage van mijn huidige publiek zal waarschijnlijk in de volgende maand kopen?&quot;
* &quot;Hoeveel profielen heb ik met een hoge neiging om te converteren?&quot;

Door vragen in de natuurlijke taal te stellen, kunt u populatiescores ophalen die het percentage of de waarschijnlijkheid aangeven dat publieksleden bepaalde gedragingen vertonen. Zo kunt u proactieve aanpassingen aanbrengen in uw campagnes of retentiestrategieën.

## Voorbeelden van vragen voor publieksgrootte en propensiteitsschatting

Hieronder volgen voorbeeldvragen die u kunt stellen aan AI Assistant om inzicht te krijgen in publieksformaten en gedragseigenschappen:

### Schatting van grootte publiek

* &quot;Hoeveel profielen heb ik met een e-mail of mobiel telefoonnummer?&quot;
* &quot;Hoeveel profielen heb ik in New York?&quot;
* &quot;Wat zijn de top 5 staten waar mijn klanten wonen?&quot;

### Pensiteitsschatting publiek

* &quot;Welk percentage van mijn publiek zal waarschijnlijk binnen de volgende maand kopen?&quot;
* &quot;Hoeveel klanten worden verwacht in het volgende kwartaal om te zetten?&quot;

U kunt de flexibiliteit die zoekopdrachten in natuurlijke talen bieden, gebruiken om snel inzicht te krijgen in de dynamiek van het publiek zonder dat u technische expertise nodig hebt.

## Veelgestelde vragen

Lees deze sectie voor antwoorden op vaak gestelde vragen over de schatting van natuurlijke talen met AI Assistant.

### Hoe vaak verfrist de AI Medewerker publieksgegevens?

De gegevens van AI Assistant worden elke 24-48 uur vernieuwd. Daarom kunnen de schattingen kleine vertragingen weergeven. Dit betekent dat wanneer u vraagt naar &quot;huidige&quot; gegevens, de reactie de meest recente momentopname weerspiegelt, die tot 48 uur oud kan zijn.

### Mag ik vragen om publieksgrootten of eigenschappen met aangepaste datumbereiken?

Momenteel ondersteunt AI Assistant vooraf gedefinieerde datumbereiken, zoals &quot;vorige maand&quot; of &quot;volgende 30 dagen&quot;. Aangepaste datumbereiken die verder gaan dan deze vooraf gedefinieerde opties, worden niet volledig ondersteund in de Alpha. Als een aangepast tijdkader wordt aangevraagd, verschaft AI Assistant inzichten op basis van het meest overeenkomende beschikbare tijdkader.

### Hoe berekent AI Assistant eigenschapscores?

De scores van de volheid worden berekend gebruikend [ AI van de Klant ](../../intelligent-services/customer-ai/overview.md). AI Assistant maakt gebruik van modellen voor machinaal leren om de waarschijnlijkheid te voorspellen van specifiek gedrag van het publiek, zoals aankopen en verven, binnen de gevraagde tijd. Tijdens het Alpha-stadium gebruikt de berekening van de densiteitsscore in AI Assistant geen ervaringsgebeurtenissen of gedragsgegevens.

### Zal AI Assistant de publieksgrootten of -eigenschappen schatten op basis van real-time gegevens?

Nee, real-time gegevens zijn op dit moment niet beschikbaar. De schattingen zijn gebaseerd op recente gegevensmomentopnamen, die elke 24 tot 48 uur worden bijgewerkt. Real-time updates vallen buiten het bereik tijdens de Alpha.

### Hoe worden de eigenschappen berekend?

AI Assistant vertrouwt op AI-modellen van de Klant om mogelijke of eigenschapscores te beantwoorden.

## Functies buiten bereik

De volgende mogelijkheden worden momenteel niet ondersteund:

### Schattingen van de omvang van de doelgroep gebaseerd op gedragsgegevens

De Medewerker van AI kan momenteel geen vragen beantwoorden die op gedragsgegevens zoals **worden gebaseerd &quot;hoeveel gebruikers een product aan karretje in de afgelopen 30 dagen hebben toegevoegd&quot;**. U kunt echter in Real-Time CDP een kenmerk voor gegevensverwerking maken dat dergelijke waarden vooraf kan berekenen. Deze berekende kenmerken zijn vervolgens beschikbaar in AI Assistant. Voor meer informatie, lees de documentatie over [ gegevens verwerkte attributen ](../../profile/computed-attributes/overview.md).

### Updates van realtime gegevens

De schattingen van AI Assistant zijn gebaseerd op recente, maar niet real-time gegevensmomentopnamen. De gegevens verfrissen zich om de 24-48 uur, zodat weerspiegelen de inzichten deze vertraging. Deze beperking betekent dat gebruikers geen onmiddellijke updates kunnen ontvangen als een segment of dataset binnen een korte tijdspanne beduidend verandert.