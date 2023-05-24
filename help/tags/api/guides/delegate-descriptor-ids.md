---
title: Beschrijvende id's delegeren
description: Leer over afgevaardigde beschrijver IDs in Reactor API, en hoe zij middelen met uitbreidingen verbinden.
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Id&#39;s van beschrijvingsbestanden delegeren

Wanneer u tags gebruikt in Adobe Experience Platform, worden alle functies die u op uw site kunt implementeren, geleverd door extensies. De mogelijkheden die door elke extensie worden geboden, worden gedefinieerd door de ontwikkelaar van de extensie. Wanneer een uitbreiding wordt opgesteld, wordt het gebundeld met zijn diverse mogelijkheden in de vorm van een [extensiepakket](../endpoints/extension-packages.md). De functies die ontwikkelaars aan een extensiepakket toevoegen, worden beschouwd als &#39;gedelegeerde&#39; van dat pakket.

Elke afgevaardigde binnen een uitbreidingspakket wordt gegeven een unieke identiteitskaart van de afgevaardigde van de beschrijver. De afgevaardigde beschrijver identiteitskaart voor een bepaald middel vertelt het systeem welk soort middel het is en tot welk uitbreidingspakket het behoort.

## Syntaxis

Een id van een gedelegeerde descriptor bestaat uit drie tekenreeksen die zijn gekoppeld door dubbele punttekens (`::`), die de naam van het extensiepakket, het gedelegeerde type en de gedelegeerde naam vertegenwoordigen. Deze tekenreeksen worden samengesteld om leesbaar te zijn voor de mens en worden automatisch gegenereerd en toegewezen door het systeem wanneer een extensiepakket wordt ingevoegd.

Als een extensiepakket bijvoorbeeld de naam `example-package` heeft een benoemde handeling `custom-code`, die actie de volgende identiteitskaart van de afgevaardigde zou hebben: `example-package::actions::custom-code`.

## Het gebruiken van afgevaardigde beschrijver IDs op toepasselijke middelen

De beschrijvings IDs van de delegatie is belangrijk om te begrijpen wanneer het over het bepalen van regelcomponenten (gebeurtenissen, voorwaarden, en acties) en gegevenselementen in API komt. In de onderstaande secties wordt beschreven hoe deze id&#39;s voor elke bron worden afgespeeld.

### Regelcomponenten

A [regelcomponent](../endpoints/rule-components.md) moet worden gekoppeld aan een gebeurtenis, voorwaarde of handeling die tot een extensiepakket behoort. Dit vertegenwoordigt het &quot;type&quot;van de regelcomponent aangezien het tot de logica van de algemene regel (een gebeurtenis, een voorwaarde, of een actie) behoort. Daarom wanneer het creëren van een regelcomponent, moet een identiteitskaart van de afgevaardigde van de beschrijver worden verstrekt om erop te wijzen welke gebeurtenis, voorwaarde, of actie de regelcomponent zou moeten worden geassocieerd met.

Bijvoorbeeld om een component van de gebeurtenisregel tot stand te brengen die op een `click` gebeurtenis in een extensiepakket `example-package`gebruikt de component rule het volgende `delegate_descriptor_id` waarde: `example-package::events::click`.

Zie de sectie over [een component rule maken](../endpoints/rule-components.md#create) voor meer informatie .

### Gegevenselementen

A [gegevenselement](../endpoints/data-elements.md) moet worden gekoppeld aan een extensiepakket wanneer dit voor het eerst wordt gemaakt, aangezien elk extensiepakket de compatibele typen definieert voor de elementen van gedelegeerde gegevens en voor het beoogde gedrag ervan.

Als u bijvoorbeeld een gegevenselement wilt maken dat het `cookie` type zoals gedefinieerd door een extensiepakket `example-package`gebruikt het gegevenselement het volgende `delegate_descriptor_id` waarde: `example-package::dataElements::cookie`.

Zie de sectie over [een gegevenselement maken](../endpoints/data-elements.md#create) voor meer informatie .

### Extensies

An [extension](../endpoints/extensions.md) wordt automatisch gekoppeld aan een extensiepakket wanneer dit voor het eerst wordt gemaakt en wordt weergegeven in de extensie `relationships` object. Als uw extensie aangepaste instellingen nodig heeft, is ook een id voor de gedelegeerde descriptor vereist.

>[!NOTE]
>
>Extensies waarvoor geen aangepaste instellingen vereist zijn, hebben geen id voor de gedelegeerde descriptor nodig.

Bijvoorbeeld, om een identiteitskaart van de afgevaardigde van de beschrijver aan een uitbreiding toe te voegen die tot het uitbreidingspakket behoort `example-package`wordt de extensie gebruikt voor de volgende `delegate_descriptor_id` waarde: `example-package::extensionConfiguration::config`.

Zie de handleiding op [een extensie maken](../endpoints/extensions.md#create) voor meer informatie .
