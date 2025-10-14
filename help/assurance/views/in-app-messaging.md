---
title: Berichtenweergave in de app
description: Deze handleiding bevat informatie over de weergave In-App Messaging in Adobe Experience Platform Assurance.
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Weergave Berichten in de app in Betrouwbaarheid

In de weergave Berichten in de app in Adobe Experience Platform Assurance kunt u uw app valideren, in-app berichten controleren die aan uw apparaat worden geleverd en berichten naar uw apparaat simuleren.

## Berichten op apparaat

Boven aan het tabblad **[!UICONTROL Messages on Device]** bevindt zich een **[!UICONTROL Message]** -vervolgkeuzelijst. Dit omvat alle berichten die in de zitting van de Verzekering zijn ontvangen. Als een bericht niet in deze lijst voorkomt, betekent dit dat de app het nooit heeft ontvangen.

![&#x200B; Bericht &#x200B;](./images/in-app-messaging/message.png)

Als u een bericht selecteert, wordt veel informatie over dat bericht weergegeven, zoals in de onderstaande secties wordt beschreven.

### Berichtvoorbeeld

In het rechterdeelvenster bevindt zich een **[!UICONTROL Message Preview]** -deelvenster, waarin een voorbeeld van het bericht wordt weergegeven. Als u **[!UICONTROL Simulate on Device]** selecteert, wordt dat bericht verzonden naar alle apparaten die op dat moment met de sessie zijn verbonden.

![&#x200B; Voorproef &#x200B;](./images/in-app-messaging/preview.png)

### Berichtgedrag

Onder het deelvenster **[!UICONTROL Message Preview]** bevindt zich de tab **[!UICONTROL Message Behavior]** . Dit heeft alle details rond hoe het bericht wordt getoond. Deze informatie omvat plaatsingsinformatie, animaties, veeggebaren, en verschijningsmontages.

![&#x200B; Gedrag &#x200B;](./images/in-app-messaging/gestures.png)

### Tabblad Info

In de linkersectie, zijn er vier lusjes die details over het bericht tonen. Op het tabblad **[!UICONTROL Info]** wordt informatie weergegeven die vanuit Adobe Journey Optimizer (AJO) is geladen over de berichtcampagne.

U kunt ook **[!UICONTROL View campaign]** selecteren om het bericht te openen in AJO voor inspectie of bewerking.

![&#x200B; Info &#x200B;](./images/in-app-messaging/info.png)

### Tabblad Regels

Het tabblad **[!UICONTROL Rules]** geeft aan wat er moet gebeuren voordat dit bericht wordt weergegeven. Dit geeft inzicht in precies wat een bericht zal teweegbrengen om worden getoond. Kijk naar dit voorbeeld:

![&#x200B; Regels &#x200B;](./images/in-app-messaging/rules.png)

In het voorbeeld worden drie verschillende voorwaarden voor de regel weergegeven. Als u een gebeurtenis selecteert (uit een lijst met gebeurtenissen, het tabblad Analyseren of in de tijdlijn), wordt die gebeurtenis aan de hand van deze regels geëvalueerd. Als de gebeurtenis overeenkomt met een voorwaarde, wordt een groen vinkje weergegeven:

![&#x200B; Overeenkomst van de Regel &#x200B;](./images/in-app-messaging/rule-match.png)

Als de gebeurtenis niet overeenkomt, wordt een rood pictogram weergegeven:

![&#x200B; Verkeerde de Regel &#x200B;](./images/in-app-messaging/rule-mismatch.png)

Als alle drie voorwaarden overeenkomen met de huidige gebeurtenis, wordt het bericht weergegeven.

### Tab analyseren

Het tabblad **[!UICONTROL Analyze]** biedt aanvullende inzichten in de regels. Hier, filtreren wij elke gebeurtenis in de zitting op hoe dicht onze berichtregel de gebeurtenis aanpast.

![&#x200B; analyseert &#x200B;](./images/in-app-messaging/analyze.png)

In het voorbeeld in de sectie **[!UICONTROL Rules Tab]** zijn er drie voorwaarden in de regel. Op dit tabblad ziet u welk percentage van de regel elke gebeurtenis overeenkomt. De meeste gebeurtenissen komen overeen met 33% (een van de drie voorwaarden) en de rest komt overeen met 100%.

Dientengevolge, kunt u gebeurtenissen vinden die dicht aan aanpassing maar niet volledig de regel aanpassen.

![&#x200B; Drempel &#x200B;](./images/in-app-messaging/threshold.png)

Met de schuifregelaar **[!UICONTROL Match Threshold]** kunt u filteren welke gebeurtenissen moeten worden weergegeven. Dit kan bijvoorbeeld worden ingesteld op 50% - 90% om een lijst met gebeurtenissen op te halen die precies overeenkomen met twee van de drie voorwaarden.

### Tabblad Interacties

Het tabblad **[!UICONTROL Interactions]** bevat een lijst met interactiegebeurtenissen die voor traceringsdoeleinden naar de Edge zijn verzonden.

![&#x200B; Interacties &#x200B;](./images/in-app-messaging/interactions.png)

Er zijn gewoonlijk vier interactiegebeurtenissen wanneer een bericht wordt getoond:

```
trigger > display > interact > dismiss
```

Aan de interactie ‘interactie’ is een aanvullende waarde ‘actie’ gekoppeld. Mogelijke waarden zijn &quot;click&quot; of &quot;cancel&quot;.

De validatiekolom geeft aan of de interactiegebeurtenis correct is ontvangen en verwerkt door de Edge.

## Validatie

Op het tabblad **[!UICONTROL Validation]** worden validaties uitgevoerd op basis van uw huidige sessie. Hierbij wordt gecontroleerd of de app correct is geconfigureerd voor berichtgeving in de app:

![&#x200B; Bevestiging &#x200B;](./images/in-app-messaging/validation.png)

Als er fouten worden gevonden, worden er details weergegeven over de manier waarop deze fouten moeten worden gecorrigeerd.

## Gebeurtenislijst

![&#x200B; Bevestiging &#x200B;](./images/in-app-messaging/event-list.png)

Het tabblad **[!UICONTROL Event List]** biedt een snelle weergave van alle gebeurtenissen in de Betrouwbaarheidssessie die betrekking hebben op In-App Messaging. Enkele gebeurtenissen die u hier ziet zijn:

* Verzoeken en antwoorden om berichten op te halen
* Gebeurtenissen van berichten weergeven
* Gebeurtenissen voor het bijhouden van interacties

In deze weergave kunt u veel standaardfuncties voor gebeurtenislijsten gebruiken, zoals zoekopdrachten toepassen, filters toepassen, kolommen toevoegen of verwijderen en gegevens exporteren.

Selecteer een gebeurtenis om de onbewerkte details van de gebeurtenis weer te geven in het rechterdeelvenster.

Vanuit het rechterdeelvenster Details kan de geselecteerde gebeurtenis worden gemarkeerd. Dit is handig om iets te markeren dat door een andere persoon moet worden gecontroleerd.
