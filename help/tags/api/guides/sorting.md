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

Door de eindpunten van lijsten in de Reactor-API te plaatsen, kunt u teruggestuurde bronnen sorteren op basis van opgegeven kenmerken. U kunt de sorteervolgorde van de reactie configureren door een parameter `sort` op te geven in het aanvraagpad.

## Sorteren oplopend

De middelen kunnen door een attribuut in stijgende orde door te specificeren worden gesorteerd
kenmerk waarop moet worden gesorteerd, en het kenmerk vooraf bepalen met een `+` :

`GET /companies/:company_id/properties?sort=+name`

## Aflopend sorteren

De middelen kunnen door een attribuut in dalende orde worden gesorteerd door te specificeren
kenmerk waarop moet worden gesorteerd, en het kenmerk vooraf bepalen met een `-` :

`GET /companies/:company_id/properties?sort=-name`

## Meerdere sorteeritems

Als u op meerdere waarden wilt sorteren, geeft u de sorteerinstructies op als een komma als scheidingsteken
lijst:

`GET /companies/:company_id/properties?sort=+name,-org_id`
