---
title: Reacties sorteren in de Reactor-API
description: Leer hoe u resultaten kunt filteren wanneer u bronnen opsomt in de Reactor-API.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Reacties sorteren in de Reactor-API

Door de eindpunten van lijsten in de Reactor-API te plaatsen, kunt u teruggestuurde bronnen sorteren op basis van opgegeven kenmerken. U kunt de sorteervolgorde van de reactie configureren door een parameter `sort` in het aanvraagpad op te geven.

## Sorteren oplopend

De middelen kunnen door een attribuut in stijgende orde door te specificeren worden gesorteerd
kenmerk waarmee moet worden gesorteerd en vooraf moet worden bepaald met een `+`:

`GET /companies/:company_id/properties?sort=+name`

## Aflopend sorteren

De middelen kunnen door een attribuut in dalende orde worden gesorteerd door te specificeren
kenmerk waarmee moet worden gesorteerd en vooraf moet worden bepaald met een `-`:

`GET /companies/:company_id/properties?sort=-name`

## Meerdere sorteren

Als u op meerdere waarden wilt sorteren, geeft u de sorteerinstructies op als een komma als scheidingsteken
lijst:

`GET /companies/:company_id/properties?sort=+name,-org_id`
