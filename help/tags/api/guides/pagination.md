---
title: Paginering van reacties in de Reactor-API
description: Leer hoe u resultaten kunt pagineren bij het weergeven van bronnen in de Reactor-API.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Paginering van reacties in de Reactor-API

Reacties die door de Reactor-API worden geretourneerd, worden gepagineerd. De standaardpaginagrootte is 25 elementen. Details over de paginering worden gerapporteerd in de sectie `meta.pagination `van het API-reactieobject:

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

Het is mogelijk om een specifieke pagina te krijgen en de grootte van een pagina te wijzigen door een `page` vraagparameter in de verzoekweg op te nemen.

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
