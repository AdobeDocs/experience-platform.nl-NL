---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Inleiding tot berekende kenmerken
topic: hulplijn
type: Documentatie
description: Berekende kenmerken zijn functies om gegevens op gebeurtenisniveau samen te voegen tot profielniveaukenmerken. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt.
translation-type: tm+mt
source-git-commit: 08eff53f107549fab0f167a6c206b632f3c8c183
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---


# (Alpha) Overzicht van berekende kenmerken

>[!IMPORTANT]
>
>De functie voor berekende kenmerken bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt.

Elk berekend kenmerk bevat een expressie, ofwel &quot;rule&quot;, die binnenkomende gegevens evalueert en de resulterende waarde in een profielkenmerk opslaat. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. Deze berekende kenmerkwaarden kunnen dan in een profiel worden bekeken, worden gebruikt om een segment tot stand te brengen, of door een aantal verschillende toegangspatronen worden betreden.

Deze handleiding helpt u de rol van berekende kenmerken in Adobe Experience Platform beter te begrijpen.

## Berekende kenmerken begrijpen

Met Adobe Experience Platform kunt u eenvoudig gegevens uit meerdere bronnen importeren en samenvoegen om [!DNL Real-time Customer Profiles] te genereren. Elk profiel bevat belangrijke informatie met betrekking tot een persoon, zoals zijn contactgegevens, voorkeuren en aankoopgeschiedenis, die een 360 graden mening van de klant verstrekken.

Een deel van de informatie die in het profiel wordt verzameld, is gemakkelijk te begrijpen wanneer de gegevensvelden rechtstreeks worden gelezen (bijvoorbeeld &quot;voornaam&quot;), terwijl andere gegevens meerdere berekeningen vereisen of op andere velden en waarden vertrouwen om de informatie te genereren (bijvoorbeeld &quot;totaal voor levenslange aanschaf&quot;). Om deze gegevens in één oogopslag begrijpelijker te maken, kunt u met [!DNL Platform] berekende kenmerken maken die deze verwijzingen en berekeningen automatisch uitvoeren en de waarde in het juiste veld retourneren.

De berekende attributen omvatten het creëren van een uitdrukking, of &quot;regel&quot;, die op inkomende gegevens werkt en de resulterende waarde in een profielattribuut opslaat. Expressies kunnen op meerdere verschillende manieren worden gedefinieerd, zodat u kunt opgeven dat een regel alleen binnenkomende gebeurtenissen, binnenkomende gebeurtenis- en profielgegevens of binnenkomende gebeurtenissen, profielgegevens en historische gebeurtenissen evalueert.

### Gebruiksscenario’s

Bij gebruik van berekende kenmerken kan het gaan om eenvoudige berekeningen tot zeer complexe verwijzingen. Hier volgen een paar voorbeelden van gebruiksscenario&#39;s voor berekende kenmerken:

1. **[!UICONTROL Percentages]:** Een eenvoudig berekend kenmerk kan het opnemen van twee numerieke velden in een record omvatten en het splitsen van deze velden om een percentage te maken. U kunt bijvoorbeeld het totale aantal e-mails dat naar een individu is verzonden, opsplitsen in het aantal e-mails dat de persoon opent. Als u het resulterende berekende kenmerkveld bekijkt, wordt snel het percentage weergegeven van het totale aantal e-mails dat door het individu wordt geopend.
1. **[!UICONTROL Toepassingsgebruik]: in** een ander voorbeeld kunt u het aantal keren samenvoegen dat een gebruiker de toepassing opent. Door het totale aantal geopende toepassingen te volgen, op basis van afzonderlijke open gebeurtenissen, kunt u speciale aanbiedingen of berichten aan gebruikers aanbieden op hun 100e open, waardoor u een diepere betrokkenheid bij uw merk aanmoedigt.
1. **[!UICONTROL Levenstijdwaarden]:Het** verzamelen van lopende totalen, zoals een levenslange aankoopwaarde voor een klant, kan zeer moeilijk zijn. Dit vereist het bijwerken van het historische totaal telkens wanneer een nieuwe aankoopgebeurtenis plaatsvindt. Een gegevens verwerkt attribuut staat u toe om dit veel gemakkelijker te doen door de levenwaarde op één enkel gebied te handhaven dat automatisch na elke succesvolle koopgebeurtenis met betrekking tot de klant wordt bijgewerkt.

## Bekende beperkingen

### Vertraagde beschikbaarheid van nieuwe berekende kenmerken

De beschikbaarheid van nieuwe gegevens verwerkte attributen kan tot 2 uur worden vertraagd nadat het overeenkomstige schemaattribuut aan het unieschema wordt toegevoegd.

Deze vertraging is toe te schrijven aan de huidige caching configuratie. Na alfa kon de cache-vernieuwingsfrequentie worden verhoogd.

### Afhankelijkheidstracering in segmenten

De attributen van het schema die reeds in een uitdrukking van de segmentdefinitie zijn gebruikt, maar later omgezet in een gegevens verwerkt attribuut zullen niet als gebiedsdeel van dat segment worden gevolgd.

Wegens het feit dat geen gebiedsdeel is ontdekt, zal het Experience Platform niet automatisch de bijbehorende gegevens verwerkte attributen evalueren telkens als de segmentdefinitie wordt geëvalueerd.

Alternatief, kon de verwezenlijking van gegevens verwerkte attributen door een specifieke mengeling worden beheerd die nieuwe gegevens verwerkte attributen toevoegt die niet met bestaande attributen strijdig zijn. Een ander alternatief is eenvoudig het segment met correcte gebiedsspatiëring voor de nieuwe gegevens verwerkte attributen te ontspannen.