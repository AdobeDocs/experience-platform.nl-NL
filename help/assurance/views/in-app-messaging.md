---
title: Berichtenweergave in de app
description: Deze handleiding bevat informatie over de weergave In-App Messaging in Adobe Experience Platform Assurance.
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 1%

---

# Weergave Berichten in de app in Betrouwbaarheid

In de weergave Berichten in de app in Adobe Experience Platform Assurance kunt u uw app valideren, in-app berichten controleren die aan uw apparaat worden geleverd en berichten naar uw apparaat simuleren.

## Berichten op apparaat

Aan de bovenkant van de **[!UICONTROL Messages on Device]** tab is een **[!UICONTROL Message]** vervolgkeuzelijst. Dit omvat alle berichten die in de zitting van de Verzekering zijn ontvangen. Als een bericht niet in deze lijst voorkomt, betekent dit dat de app het nooit heeft ontvangen.

![Bericht](./images/in-app-messaging/message.png)

Als u een bericht selecteert, wordt veel informatie over dat bericht weergegeven, zoals in de onderstaande secties wordt beschreven.

### Berichtvoorbeeld

In het rechterdeelvenster bevindt zich een **[!UICONTROL Message Preview]** venster, waarin een voorbeeld van het bericht wordt weergegeven. Selecteren **[!UICONTROL Simulate on Device]** zal dat bericht naar om het even welke apparaten verzenden die momenteel met de zitting worden verbonden.

![Voorvertoning](./images/in-app-messaging/preview.png)

### Berichtgedrag

Onder de **[!UICONTROL Message Preview]** is de **[!UICONTROL Message Behavior]** tab. Dit heeft alle details rond hoe het bericht wordt getoond. Deze informatie omvat plaatsingsinformatie, animaties, veeggebaren, en verschijningsmontages.

![Gedraging](./images/in-app-messaging/gestures.png)

### Tabblad Info

In de linkersectie, zijn er vier lusjes die details over het bericht tonen. De **[!UICONTROL Info]** wordt informatie over de berichtcampagne weergegeven die vanuit Adobe Journey Optimizer (AJO) is geladen.

U kunt ook **[!UICONTROL View campaign]** om het bericht in AJO voor inspectie of het uitgeven te openen.

![Info](./images/in-app-messaging/info.png)

### Tabblad Regels

De **[!UICONTROL Rules]** toont wat er moet gebeuren voordat dit bericht wordt weergegeven. Dit geeft inzicht in precies wat een bericht zal teweegbrengen om worden getoond. Kijk naar dit voorbeeld:

![Regels](./images/in-app-messaging/rules.png)

In het voorbeeld worden drie verschillende voorwaarden voor de regel weergegeven. Als u een gebeurtenis selecteert (uit een lijst met gebeurtenissen, het tabblad Analyseren of in de tijdlijn), wordt die gebeurtenis aan de hand van deze regels geëvalueerd. Als de gebeurtenis overeenkomt met een voorwaarde, wordt een groen vinkje weergegeven:

![Regelafstemming](./images/in-app-messaging/rule-match.png)

Als de gebeurtenis niet overeenkomt, wordt een rood pictogram weergegeven:

![Regel komt niet overeen](./images/in-app-messaging/rule-mismatch.png)

Als alle drie voorwaarden overeenkomen met de huidige gebeurtenis, wordt het bericht weergegeven.

### Tab analyseren

De **[!UICONTROL Analyze]** bevat aanvullende inzichten in de regels. Hier, filtreren wij elke gebeurtenis in de zitting op hoe dicht onze berichtregel de gebeurtenis aanpast.

![Analyseren](./images/in-app-messaging/analyze.png)

In het voorbeeld in het dialoogvenster **[!UICONTROL Rules Tab]** er zijn drie voorwaarden in de regel . Op dit tabblad ziet u welk percentage van de regel elke gebeurtenis overeenkomt. De meeste gebeurtenissen komen overeen met 33% (een van de drie voorwaarden) en de rest komt overeen met 100%.

Dientengevolge, kunt u gebeurtenissen vinden die dicht aan aanpassing maar niet volledig de regel aanpassen.

![Drempel](./images/in-app-messaging/threshold.png)

De **[!UICONTROL Match Threshold]** kunt u filteren welke gebeurtenissen moeten worden weergegeven. Dit kan bijvoorbeeld worden ingesteld op 50% - 90% om een lijst met gebeurtenissen op te halen die precies overeenkomen met twee van de drie voorwaarden.

### Tabblad Interacties

De **[!UICONTROL Interactions]** wordt een lijst weergegeven met interactiegebeurtenissen die voor traceringsdoeleinden naar Edge zijn verzonden.

![Interacties](./images/in-app-messaging/interactions.png)

Er zijn gewoonlijk vier interactiegebeurtenissen wanneer een bericht wordt getoond:

```
trigger > display > interact > dismiss
```

Aan de interactie ‘interactie’ is een aanvullende waarde ‘actie’ gekoppeld. Mogelijke waarden zijn &quot;click&quot; of &quot;cancel&quot;.

De validatiekolom geeft aan of de interactiegebeurtenis correct door Edge is ontvangen en verwerkt.

## Validatie

De **[!UICONTROL Validation]** -tab voert validaties uit op basis van uw huidige sessie, waarbij wordt gecontroleerd of de app correct is geconfigureerd voor In-App-berichten:

![Validatie](./images/in-app-messaging/validation.png)

Als er fouten worden gevonden, worden er details weergegeven over de manier waarop deze fouten moeten worden gecorrigeerd.

## Gebeurtenislijst

![Validatie](./images/in-app-messaging/event-list.png)

De **[!UICONTROL Event List]** biedt een snel overzicht van alle gebeurtenissen in de Betrouwbaarheidssessie die betrekking hebben op In-App Messaging. Enkele gebeurtenissen die u hier ziet zijn:

* Verzoeken en antwoorden om berichten op te halen
* Gebeurtenissen van berichten weergeven
* Gebeurtenissen voor het bijhouden van interacties

In deze weergave kunt u veel standaardfuncties voor gebeurtenislijsten gebruiken, zoals zoekopdrachten toepassen, filters toepassen, kolommen toevoegen of verwijderen en gegevens exporteren.

Selecteer een gebeurtenis om de onbewerkte details van de gebeurtenis weer te geven in het rechterdeelvenster.

Vanuit het rechterdeelvenster Details kan de geselecteerde gebeurtenis worden gemarkeerd. Dit is handig om iets te markeren dat door een andere persoon moet worden gecontroleerd.
