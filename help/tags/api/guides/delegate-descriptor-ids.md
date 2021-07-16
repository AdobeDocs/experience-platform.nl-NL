---
title: Beschrijvende id's delegeren
description: Leer over afgevaardigde beschrijver IDs in Reactor API, en hoe zij middelen met uitbreidingen verbinden.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Id&#39;s van beschrijvingsbestanden delegeren

Wanneer u tags gebruikt in Adobe Experience Platform, worden alle functies die u op uw site kunt implementeren, geleverd door extensies. De mogelijkheden die door elke extensie worden geboden, worden gedefinieerd door de ontwikkelaar van de extensie. Wanneer een uitbreiding wordt opgesteld, wordt het gebundeld met zijn diverse mogelijkheden in de vorm van een [uitbreidingspakket](../endpoints/extension-packages.md). De functies die ontwikkelaars aan een extensiepakket toevoegen, worden beschouwd als &#39;gedelegeerde&#39; van dat pakket.

Elke afgevaardigde binnen een uitbreidingspakket wordt gegeven een unieke identiteitskaart van de afgevaardigde van de beschrijver. De afgevaardigde beschrijver identiteitskaart voor een bepaald middel vertelt het systeem welk soort middel het is en tot welk uitbreidingspakket het behoort.

## Syntaxis

Een afgevaardigde beschrijver ID bestaat uit drie koorden die door dubbel-dubbelepelkarakters (`::`) worden aangesloten, die de naam van het uitbreidingspakket, het afgevaardigde type, en de afgevaardigde naam vertegenwoordigen, respectievelijk. Deze tekenreeksen worden samengesteld om leesbaar te zijn voor de mens en worden automatisch gegenereerd en toegewezen door het systeem wanneer een extensiepakket wordt ingevoegd.

Als een extensiepakket met de naam `example-package` bijvoorbeeld een handeling met de naam `custom-code` heeft, heeft die handeling de volgende id van de gedelegeerde descriptor: `example-package::actions::custom-code`.

## Het gebruiken van afgevaardigde beschrijver IDs op toepasselijke middelen

De beschrijvings IDs van de delegatie is belangrijk om te begrijpen wanneer het over het bepalen van regelcomponenten (gebeurtenissen, voorwaarden, en acties) en gegevenselementen in API komt. In de onderstaande secties wordt beschreven hoe deze id&#39;s voor elke bron worden afgespeeld.

### Regelcomponenten

Een [regelcomponent](../endpoints/rule-components.md) moet worden gekoppeld aan een gebeurtenis, voorwaarde of handeling die tot een extensiepakket behoort. Dit vertegenwoordigt het &quot;type&quot;van de regelcomponent aangezien het tot de logica van de algemene regel (een gebeurtenis, een voorwaarde, of een actie) behoort. Daarom wanneer het creëren van een regelcomponent, moet een identiteitskaart van de afgevaardigde van de beschrijver worden verstrekt om erop te wijzen welke gebeurtenis, voorwaarde, of actie de regelcomponent zou moeten worden geassocieerd met.

Als u bijvoorbeeld een gebeurtenisregelcomponent wilt maken die is gebaseerd op een gebeurtenis `click` in een extensiepakket `example-package`, gebruikt de regelcomponent de volgende waarde `delegate_descriptor_id`: `example-package::events::click`.

Zie de sectie over [het creëren van een regelcomponent](../endpoints/rule-components.md#create) voor meer informatie.

### Gegevenselementen

Een [gegevenselement](../endpoints/data-elements.md) moet met een uitbreidingspakket worden geassocieerd wanneer het eerst wordt gecreeerd, aangezien elk uitbreidingspakket de compatibele types voor zijn elementen van gedelegeerde gegevens, evenals hun voorgenomen gedrag bepaalt.

Als u bijvoorbeeld een gegevenselement wilt maken dat het type `cookie` gebruikt zoals gedefinieerd door het extensiepakket `example-package`, gebruikt het gegevenselement de volgende `delegate_descriptor_id`-waarde: `example-package::dataElements::cookie`.

Zie de sectie over [het creëren van een gegevenselement](../endpoints/data-elements.md#create) voor meer informatie.

### Extensies

Een [extensie](../endpoints/extensions.md) wordt automatisch gekoppeld aan een extensiepakket wanneer dit voor het eerst wordt gemaakt en wordt weergegeven binnen het `relationships`-object van de extensie. Als uw extensie aangepaste instellingen nodig heeft, is ook een id voor de gedelegeerde descriptor vereist.

>[!NOTE]
>
>Extensies waarvoor geen aangepaste instellingen vereist zijn, hebben geen id voor de gedelegeerde descriptor nodig.

Als u bijvoorbeeld een id van een gedelegeerde descriptor wilt toevoegen aan een extensie die tot het extensiepakket `example-package` behoort, gebruikt de extensie de volgende waarde `delegate_descriptor_id`: `example-package::extensionConfiguration::config`.

Zie de handleiding bij [het maken van een extensie](../endpoints/extensions.md#create) voor meer informatie.