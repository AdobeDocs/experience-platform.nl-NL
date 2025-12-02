---
title: _monitors
description: Voeg gebeurtenislisteners toe om fouten in de implementatie van uw tag op te sporen.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# `_monitors`

Met het `_satellite._monitors` -object kunt u gebeurtenislisteners maken en aangepaste code uitvoeren wanneer de bibliotheek een getriggerde regel detecteert. Zijn primair gebruik moet bij het zuiveren van uw implementatie helpen om ervoor te zorgen dat de regels correct teweegbrengen.

>[!IMPORTANT]
>
>Dit object is alleen bedoeld voor foutopsporing. Koppel geen productielogica aan dit object. De beschikbaarheid van eigenschappen of namen in dit object kan op elk gewenst moment door Adobe worden gewijzigd.

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

U kunt luisteren naar de volgende gebeurtenistypen:

## `ruleTriggered`

Deze callback functie brandt wanneer een gebeurtenis een regel teweegbrengt alvorens de voorwaarden en de acties van de regel zijn verwerkt. Als deze functie wordt geactiveerd, wordt `ruleCompleted` of `ruleConditionFailed` kort na (wederzijds exclusief) geactiveerd.

## `ruleCompleted`

De callback-functie `ruleCompleted` wordt geactiveerd na `ruleTriggered` wanneer de voorwaardecriteria van de regel zijn geslaagd en alle handelingen van de regel zijn uitgevoerd.

## `ruleConditionFailed`

De callback-functie `ruleConditionFailed` wordt geactiveerd na `ruleTriggered` wanneer ten minste een van de voorwaarden van de regel is mislukt.

## `Rule` -object

Elke callback-functie stelt een `Rule` -object beschikbaar dat informatie over de regel zelf bevat.

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| Naam | Type | Beschrijving |
|---|---|---|
| **`id`** | `string` | De unieke id voor de regel. |
| **`name`** | `string` | De vriendelijke naam van de regel. |
| **`events`** | `Event[]` | Een serie van gebeurtenissen die u hebt gevormd om de regel teweeg te brengen. |
| **`conditions`** | `Condition[]` | Een serie van voorwaarden die u hebt gevormd om de regel teweeg te brengen. |
| **`actions`** | `Action[]` | Een serie van acties die u hebt gevormd om uit te voeren wanneer de regel wordt teweeggebracht. |

## Voorbeeld

Voeg het volgende codefragment toe aan de HTML in de tag `<head>` voordat u de tagbibliotheekloader aanroept:

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

Aangezien de tagbibliotheek op dit punt op de pagina nog niet is geladen, wordt het eerste `_satellite` -object gemaakt en wordt een array op `_satellite._monitors` geïnitialiseerd. Het script voegt vervolgens een monitorobject aan die array toe.

Houd rekening met de volgende tips wanneer u beeldschermen gebruikt:

* Deze foutopsporingsberichten gebruiken `console.log` in plaats van [`_satellite.logger`](logger.md) omdat de haken zijn gemaakt voordat de tagbibliotheek wordt geladen.
* Hoewel het codevoorbeeld alle drie callback functies omvat, zijn zij geen vereiste gebieden. U kunt alleen de gewenste haken opnemen bij het opsporen van fouten in de regels op uw site.
* Meerdere monitoren zijn toegestaan, zelfs voor dezelfde gebeurtenissen. Als u veelvoudige monitors voor één enkele gebeurtenis gebruikt, is de vraagorde niet gewaarborgd.
* Zorg ervoor dat u `_monitors` __ creeert ladend de markeringsbibliotheek. Als u deze haken maakt nadat de bibliotheek is geladen, worden alleen de regels afgevangen die vanaf dat punt voorwaarts worden geactiveerd.
