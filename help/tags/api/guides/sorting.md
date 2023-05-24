---
title: Reacties sorteren in de Reactor-API
description: Leer hoe u resultaten kunt filteren wanneer u bronnen opsomt in de Reactor-API.
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Reacties sorteren in de Reactor-API

Door de eindpunten van lijsten in de Reactor-API te plaatsen, kunt u teruggestuurde bronnen sorteren op basis van opgegeven kenmerken. U kunt de sorteervolgorde van de reactie configureren door een `sort` in het aanvraagpad.

## Sorteren oplopend

De middelen kunnen door een attribuut in stijgende orde worden gesorteerd door het attribuut te specificeren waardoor te sorteren, en het met een prefixeren `+`:

`GET /companies/:company_id/properties?sort=+name`

## Aflopend sorteren

De middelen kunnen door een attribuut in dalende orde worden gesorteerd door het attribuut te specificeren waardoor te sorteren, en het vooraf te bevestigen met a `-`:

`GET /companies/:company_id/properties?sort=-name`

## Meerdere sorteren

Als u op meerdere waarden wilt sorteren, voert u de sorteerinstructies in als een lijst met door komma&#39;s gescheiden waarden:

`GET /companies/:company_id/properties?sort=+name,-org_id`
