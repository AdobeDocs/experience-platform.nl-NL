---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;search;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype zoeken
description: Leer over het het gegevenstype van de Gegevens van de Ervaring van het Onderzoek Model (XDM).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# [!UICONTROL Search] gegevenstype

[!UICONTROL Search] is een standaard XDM-gegevenstype (Experience Data Model) dat informatie bevat over zoekactiviteiten op het web.

![ onderzoeksbeeld ](../images/data-types/search.PNG) {width= 500}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `isPaid` | Boolean | Wordt gebruikt om aan te geven of de zoekopdracht is betaald of niet. |
| `keywords` | String | De trefwoorden voor de zoekopdracht. |
| `pageDepth` | Geheel | De paginadiepte in de zoekresultaten. |
| `position` | Geheel | De positie of rang van de aanbieding op de pagina met zoekresultaten. |
| `searchEngine` | String | Het zoekprogramma dat door de zoekopdracht wordt gebruikt. |
| `searchEngineID` | String | De toepassingsspecifieke id die wordt gebruikt om het zoekprogramma te identificeren. |
| `slot` | String | De benoemde sectie van de pagina waar het zoekresultaat werd weergegeven. De waarde van deze eigenschap moet gelijk zijn aan een van de bekende opsommingswaarden die u definieert, zoals `top` , `side` of `bottom` . |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
