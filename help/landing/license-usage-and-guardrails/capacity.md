---
title: Gebruik en capaciteit van licenties
description: Meer informatie over het gebruik van licenties en capaciteitsbeperkingen in Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: b3b0792a1a1dd5270dec697539ed58d895814fc8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# Gebruik van licenties en capaciteiten

In Adobe Experience Platform, laat de capaciteit u weten of uw organisatie om het even welk van uw gidsen heeft overschreden en geeft u informatie over hoe te om deze kwesties op te lossen.

Voor meer informatie over geleiders in Experience Platform, te lezen gelieve het [ overzicht van de Bewindingen van Real-Time CDP ](../../rtcdp/guardrails/overview.md).

## Capaciteit, gedrag {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Streaming doorvoer"
>abstract="De het stromen productiewaarde meet de gecombineerde piekbinnenkomende gebeurtenissen per seconde voor het stromen van opname in de dienst van het Profiel, over uw productie en ontwikkelingszandbakken."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Aantal gestreamde doelgroepen"
>abstract="Het maximum aantal streaming publiek per sandbox. Dit getal is inclusief het aantal randsoorten dat u in de sandbox hebt."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Edge-publiek"
>abstract="Het maximumaantal randpubliek per sandbox."

Capaciteit ondersteunt momenteel de volgende services:

- Streaming segmentering
- Streaming opname

Binnen deze diensten, worden de volgende gidsen gevolgd:

- Maximumaantal streamingdeelnemers is 500
   - Van deze 500 streamingdeelnemers is het maximumaantal randsoorten 150
- De maximale gecombineerde doorvoer voor streamingsegmentatie is 1500 records per seconde (rps)

De publiekscapaciteit is op a **zandbak** niveau. Dit betekent dat u voor elke sandbox die u in uw organisatie hebt, 500 streaming publiek kunt hebben, waarvan 150 Edge-publiek.

De productiecapaciteit is op een **organisatie** niveau en kan aan uw individuele zandbakken worden verdeeld. Met de 1500 rps voor het streamen van de segmentatiedoorvoer kunt u bijvoorbeeld de productie-sandbox instellen op 1500 rps en de ontwikkelingssandbox op 150 rps.

Experience Platform berekent de doorvoer van de sandbox in telkens 15 minuten. Deze productie wordt gemeten in real time, met de gegevens die elke 60 seconden verfrissen.

Als uw gebruik 80% en 90% van uw gelicentieerde capaciteit bereikt, zal Experience Platform een alarm afgeven, op het bericht dat u het maximum van uw gespecificeerde capaciteit bereikt. U kunt de instellingen wijzigen om het capaciteitspercentage aan te passen aan de waarschuwing of de waarschuwing volledig verwijderen.

Als uw gebruik tot meer dan 100% van uw vergunning capaciteit gaat, zult u beschouwd in strijd met uw capaciteit worden. Op dit punt, zult u prestatieslatentie ervaren, en uw doelstellingen van het de dienstniveau (SLTs) zullen **niet** worden gewaarborgd.

## Veelgestelde vragen

In de volgende sectie worden veelgestelde vragen over de mogelijkheden van Capaciteit beschreven.

### Kan ik een maximum gecombineerde productielimiet hebben die tot minder dan mijn doelmaximum samenvat?

+++ Antwoord

Nee. De maximum gecombineerde productielimiet **moet** som tot de guardrail van uw organisatie.

+++

### Wat gebeurt er als ik mijn maximale capaciteit overschrijd?

+++ Antwoord

Dit hangt af van de vraag welke capaciteit wordt overschreden.

Als u het maximale aantal toegestane doelgroepen overschrijdt, heeft dit momenteel geen invloed op uw buitensporige doelgroepen. Het vermogen om een nieuw publiek te creëren kan in de toekomst echter beperkt zijn.

Als u uw het stromen productie overschrijdt, zult u prestatieslatentie in uw opname en segmentatie ervaren.

+++

### Waarom zou ik mijn maximale capaciteit moeten respecteren?

+++ Antwoord

Uw gegevens blijven consistent en de integriteit van uw gegevens blijft intact als u binnen uw maximale capaciteit werkt.

U verzekert verenigbare prestaties tijdens piekgebeurtenissen, vermijdend technische kwesties die systeemprestaties negatief zouden kunnen beïnvloeden en uw stroomafwaartse klantenervaring beïnvloeden, uiteindelijk verbeterend uw gegevenshygiëne en algemene systeemprestaties.

+++

### Wat zijn beste praktijken om het stromen segmenteringsproductie te beheren?

+++ Antwoord

Om uw het stromen segmenteringsproductie het best te beheren, zou u uw datasets moeten evalueren om ervoor te zorgen zij aan gegevens noodzakelijk voor verpersoonlijking voorrang geven.


Als verwerking in real time niet vereist is, moet u batch-opname gebruiken in plaats van streaming opname.

+++
