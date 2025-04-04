---
title: Een expertisecentrum inschakelen met behulp van sandbox-tools
description: Schakel een expertisecentrum in met behulp van sandboxgereedschappen door een 'gouden sandbox'-pakket te maken waarmee u de aanbevolen procedures voor meerdere sandboxen kunt standaardiseren.
exl-id: 6f242ad5-bb02-4a6d-b255-d196dd5fe4b8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 2%

---

# Een expertisecentrum inschakelen met behulp van sandbox-tools

Schakel een expertisecentrum in met behulp van sandboxgereedschappen door een &#39;gouden sandbox&#39;-pakket te maken waarmee u de aanbevolen procedures voor meerdere sandboxen kunt standaardiseren.

![ Overzicht van het uitvoeren van pakketten over verschillende organisaties ](../images/use-cases/packages-across-orgs.png){zoomable="yes"}

## Waarom dit gebruiksgeval overwegen {#why-this-use-case}

Veel grote bedrijven of bedrijven gebruiken meerdere sandboxen voor verschillende organisaties, teams, regio&#39;s of ontwikkelomgevingen. Met de macht van [ zandbak tooling ](../ui/sandbox-tooling.md), kunt u een gouden zandbakpakket tot stand brengen om consistentie, naleving, en groepering van de normen van uw organisatie over veelvoudige zandbakken te verzekeren.

Dit gouden zandbakpakket leidt tot een centrum van excellentie om zeer belangrijke configuraties efficiënt te delen. Met behulp van sandboxgereedschappen kunt u het pakket gemakkelijk importeren over meerdere sandboxen. U kunt uw pakket ook delen met andere organisaties voor algemene consistentie.

Voer de stappen uit die in dit gebruiksgeval worden beschreven om zelf een gouden sandboxpakket te maken.

## Voorbeeld van industrie {#industry-example}

Neem bijvoorbeeld een bank die actief is in verschillende regio&#39;s, zoals Noord-Amerika, Europa en Afrika. Elke markt of regio heeft een eigen Adobe Experience Platform-instantie. Deze bank wil een gecentraliseerd gegevensmodel onderhouden dat wordt beheerd door een wereldwijd team van architecten waar één enkele versie van het gegevensmodel op alle markten kan worden uitgeduwd.

Deze bank kiest ervoor om sandboxgereedschappen te handhaven om een gouden sandboxpakket te maken en te onderhouden. Dit draagt bij aan de efficiëntie van de ontwikkeling, maakt consistente gegevensmodellen mogelijk en zorgt voor consistentie in alle regio&#39;s.

## Vereisten en planning {#prerequisites-and-planning}

Wanneer u van plan bent om uw eigen centrum van excellentie binnen uw organisatie te creëren, overweeg de volgende eerste vereisten in uw planningsproces:

- Identificeer de beste praktijken en configuraties om in uw pakket te omvatten.
- Maak een sandbox met alle relevante en gevalideerde configuraties die als de gouden sandbox moeten worden ingesteld.
- Verkrijg indien nodig de inbreng van belanghebbenden en ga akkoord met uw basislijnstandaarden.

### UI-functionaliteit, Experience Platform-componenten en Experience Cloud-producten die u wilt gebruiken {#ui-functionality-and-elements}

Als u dit geval wilt gebruiken, moet u meerdere gebieden van Adobe Experience Platform gebruiken. Verzeker u de noodzakelijke [ op attributen-gebaseerde toegangsbeheertoestemmingen ](../../access-control/abac/overview.md) voor al deze gebieden hebt, of uw systeembeheerder vragen om u de noodzakelijke toestemmingen te verlenen.

- [Sandbox-tools](../ui/sandbox-tooling.md)
- [Sandboxbeheer](../ui/user-guide.md)
- [Gegevenssets](../../catalog/datasets/overview.md)
- [Schema&#39;s](../../xdm//home.md)
- [Doelgroepen](../../segmentation/home.md)
- [ reizen van Adobe Journey Optimizer ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

1. Maak de basislijnconfiguratie die uw beste werkwijzen in een gouden zandbak vertegenwoordigt. Dit kunnen voorwerpen zoals datasets, schema&#39;s, publiek, of reizen omvatten.
2. Exporteer de configuratie met behulp van sandboxgereedschappen naar een pakket.
3. Importeer dit pakket in alle relevante sandboxen.
4. Als u meerdere organisaties hebt, deelt u dit pakket in alle organisaties.
5. De invoer en de uitvoer controleren en veranderingen door controlelogboeken volgen.
6. Werk regelmatig uw gouden sandbox bij terwijl de standaarden evolueren om ervoor te zorgen dat alle sandboxen op één lijn blijven met de aanbevolen procedures.

## Hoe het gebruiksgeval te bereiken: Step-by-step instructies {#step-by-step-instructions}

Lees de onderstaande secties door, die koppelingen naar verdere documentatie bevatten, om alle stappen in het bovenstaande overzicht op hoog niveau te voltooien.

### Uw gouden sandbox maken

De eerste stap bij het inschakelen van uw expertisecentrum is het maken van uw gouden sandbox. Deze zandbak zou de basislijnconfiguraties moeten bevatten die uw beste praktijken vertegenwoordigen. Om deze gouden zandbak tot stand te brengen, volg de gids op [ creërend een nieuwe zandbak ](../ui/user-guide.md#create-a-new-sandbox) in Experience Platform.

Zodra uw zandbak is gecreeerd, begin creërend uw configuraties van basislijnobjecten, zoals [ schema&#39;s ](../../xdm/ui/resources/schemas.md#create-a-new-schema), [ datasets ](../../catalog/datasets/user-guide.md#create-a-dataset), of [ publiek ](../../segmentation/ui/segment-builder.md). Controleer uw configuraties voordat u verdergaat.

### Uw sandbox exporteren naar een pakket

Nu de sandbox de objectconfiguraties van de basislijn bevat, is deze klaar om te worden geëxporteerd naar een pakket met behulp van sandboxgereedschappen. Volg de gids op [ die een volledige zandbak ](../ui/sandbox-tooling.md#export-an-entire-sandbox) uitvoert om uw gouden zandbakpakket tot stand te brengen.

### Het pakket importeren in relevante sandboxen

Nu het pakket is gemaakt, kunt u dit pakket importeren in uw relevante sandboxen. U kunt het beste een pakket met een volledige sandbox importeren in een lege sandbox. Gebruikend zandbak tooling, kunt u gemakkelijk [ een volledig zandbakpakket ](../../sandboxes/ui/sandbox-tooling.md#import-the-entire-sandbox-package) in een zandbak direct binnen Experience Platform invoeren.

### Pakket delen over organisaties

Met gereedschappen voor sandboxen kunt u pakketten delen die u in verschillende organisaties hebt gemaakt. Volg het [ pakket delend gids ](../../sandboxes/ui/sharing-packages-across-orgs.md) om uw gouden zandbakpakket te delen.

### Invoer en uitvoer controleren aan de hand van auditlogs

Wanneer u het pakket importeert of exporteert, kunt u de status van de taken controleren met het dashboard van **[!UICONTROL Jobs]** in Experience Platform. Om meer over controletaken te leren, lees de gids over [ controlerende de invoerdetails ](../../sandboxes/ui/sandbox-tooling.md#monitor-import-details).

### De gouden sandbox regelmatig bijwerken

Nu uw gouden sandboxpakket klaar is, hebt u een gestandaardiseerd expertisecentrum opgericht dat u kunt blijven importeren in sandboxen of delen tussen organisaties. Aangezien uw beste praktijken veranderen en zich ontwikkelen, is het belangrijk om de basislijnobjecten configuraties in uw gouden zandbak regelmatig bij te werken. Terwijl u updates uitvoert aan de sandbox, kunt u nieuwe herhalingen van uw gouden sandboxpakket maken volgens hetzelfde proces.

>[!NOTE]
>
> De bovenstaande stappen volgen het proces in de gebruikersinterface van Experience Platform. Het is mogelijk om dezelfde stappen te volgen gebruikend API door diverse eindpunten. Verwijs naar de `sandboxes` [ eindpuntgids ](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/api/sandboxes#create) en de `packages` [ eindpuntgids ](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages) voor informatie bij het maken van elk verzoek door API.

## Andere gebruiksgevallen die worden bereikt via ondersteuning van partnergegevens {#other-use-cases}

Verken meer gebruiksgevallen die zijn ingeschakeld via gereedschappen voor sandboxen:

- [Back-up maken van objectconfiguraties met behulp van sandbox](./backup-object-configuration.md)
