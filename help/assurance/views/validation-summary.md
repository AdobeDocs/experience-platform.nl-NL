---
title: Weergave van validatieeditor
description: Deze handleiding bevat informatie over de weergave Validatie-editor in Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Weergave Validatie-editor

Met de validatie-editor kunt u snel en eenvoudig JavaScript-functies beheren om gebeurtenissen in een Adobe Experience Platform Assurance-sessie te valideren. Elke functie ontvangt de gebeurtenissen in een Assurance-sessie. U kunt functies schrijven om uw cliëntconfiguratie, gebeurtenisvoorwaarden, tests en gebruiksgevallen te bevestigen.

## Aan de slag met de validatie-editor

Na [ vestiging Assurance ](../tutorials/implement-assurance.md), op de **[!UICONTROL Home]** mening, selecteer **[!UICONTROL Validation Editor]**.

![ bevestiging-redacteur-scherm-opname ](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Een validatiefunctie schrijven

Met deze functie kunt u validatiefuncties voor uw Adobe Experience Platform Assurance-sessies maken, bewerken of verwijderen.

1. Selecteer **[!UICONTROL Create a New Validation]**.
2. Ga a **naam** in om de bevestiging te identificeren, dan a **categorie** en a **beschrijving** verstrekken.
3. Bewerk de code in de editor om de gebeurtenissen voor uw Assurance-sessie te valideren.

Nadat de functietests zijn voltooid, selecteert u **[!UICONTROL Publish]** om de validatie op te slaan.

### Gebeurtenisdefinitie

| Sleutel | Type | Beschrijving |
| :--- | :--- | :--- |
| `uuid` | String | Universally unique identifier for the event. |
| `timestamp` | Getal | Tijdstempel van de client wanneer de gebeurtenis naar Assurance is verzonden. |
| `eventNumber` | Getal | Wordt gebruikt om te bestellen wanneer de gebeurtenis is verzonden. Deze sleutel is handig wanneer gebeurtenissen dezelfde tijdstempel hebben. |
| `vendor` | String | De tekenreeks voor de identificatie van de leverancier in de omgekeerde domeinnaamnotatie (bijvoorbeeld com.adobe.assurance). |
| `type` | String | Wordt gebruikt om het type gebeurtenis aan te geven. |
| `payload` | Object | Definieert de gegevens voor de gebeurtenis en bevat unieke en algemene eigenschappen. Enkele veelvoorkomende eigenschappen zijn `ACPExtensionEventSource` en `ACPExtensionEventType` . |
| `annotations` | Array | Een array van annotatieobjecten. |

### Definitie van aantekening

| Sleutel | Type | Beschrijving |
| :--- | :--- | :--- |
| `uuid` | String | Universally unique identifier for the annotation. |
| `type` | String | Wordt gebruikt om het type annotatie aan te duiden. Dit is doorgaans de naam van de plug-in (bijvoorbeeld Analytics). |
| `payload` | Object | Definieert de gegevens die de gebeurtenis moeten aanvullen. In Adobe Analytics zijn de gegevens van de nabewerkte hit hierin opgenomen. |

### Validatieresultaten

Van de validatiefunctie wordt verwacht dat deze een object retourneert dat het volgende bevat:

| Sleutel | Type | Beschrijving |
| :--- | :--- | :--- |
| `message` | String | Het validatiebericht dat in de samenvattingsresultaten moet worden weergegeven. |
| `events` | Array | Een array met gebeurtenishulplijnen die moeten worden gerapporteerd als gematchte of niet-overeenkomende gebeurtenissen. |
| `links` | Array | Een array van `ValidationResultLink` -objecten naar verwijzingsdocumentatie en andere bronnen `{( type: 'doc'` &amp;vert;`'product', url: String )}` |
| `result` | String | Dit is het validatieresultaat en wordt verwacht dat het een van de opgesomde tekenreeksen is: &quot;gematcht&quot;, &quot;niet gematcht&quot;, &quot;onbekend&quot; |

## De validatieresultaten weergeven

De resultaten van de functie worden weergegeven in de resultatensectie onder de code-editor. Als het validatieresultaat `unknown` of `not matched` is en de `events` array een of meer `uuids` heeft, worden de gebeurtenissen in de tijdlijn gemarkeerd met de volgende kleuren:

* Groen - gematcht
* Oranje - onbekend
* Rood - niet overeenkomend

![ timing-Bevestiging-hoogtepunten-scherm-heet ](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Problemen oplossen

U kunt `console.log()` in uw functie toevoegen om punten aan de ontwikkelaarsconsole te drukken. U kunt ook de eigenschap message van het resultaatobject gebruiken om fouten op te sporen in berichten in het resultatenpaneel.

Als er een fout optreedt in de JavaScript-code-editor, wordt naast de reden een foutstatus weergegeven.

Om meer over bevestigingen te leren, gelieve te bezoeken de [ Bevestigingen van Adobe Experience Platform Assurance ](https://github.com/adobe/griffon-validation-plugins) GitHub. Hier zijn voorbeelden van validaties die eigendom zijn van Adobe. Zie [ wiki ](https://github.com/adobe/griffon-validation-plugins/wiki) voor meer gedetailleerde beschrijvingen van bevestigingen.
