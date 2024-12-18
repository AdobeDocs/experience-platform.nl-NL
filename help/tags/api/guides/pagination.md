---
title: Paginering van reacties in de Reactor-API
description: Leer hoe u resultaten kunt pagineren bij het weergeven van bronnen in de Reactor-API.
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Paginering van reacties in de Reactor-API

Reacties die door de Reactor-API worden geretourneerd, worden gepagineerd. De standaardpaginagrootte is 25 elementen. De details over de paginering worden gemeld in de `meta.pagination ` sectie van het API antwoordvoorwerp:

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

Het is mogelijk om een specifieke pagina op te halen en de grootte van een pagina te wijzigen door een `page` query-parameter op te nemen in het aanvraagpad.

## Een specifieke pagina ophalen

Een specifieke pagina ophalen:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## Het paginaformaat wijzigen

Het paginaformaat wijzigen:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

De verschillende opties kunnen samen worden gecombineerd:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
