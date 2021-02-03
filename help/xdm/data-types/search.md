---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;search;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype zoeken
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Search Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 2%

---


# [!UICONTROL Type ] zoekgegevens

 Zoekt een standaard gegevenstype van het Model van de Gegevens van de Ervaring (XDM) dat informatie over de activiteit van het Webonderzoek bevat.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `isPaid` | Boolean | Wordt gebruikt om aan te geven of de zoekopdracht is betaald of niet. |
| `keywords` | Tekenreeks | De trefwoorden voor de zoekopdracht. |
| `pageDepth` | Geheel | De paginadiepte in de zoekresultaten. |
| `position` | Geheel | De positie of rang van de aanbieding op de pagina met zoekresultaten. |
| `searchEngine` | Tekenreeks | Het zoekprogramma dat door de zoekopdracht wordt gebruikt. |
| `searchEngineID` | Tekenreeks | De toepassingsspecifieke id die wordt gebruikt om het zoekprogramma te identificeren. |
| `slot` | Tekenreeks | De benoemde sectie van de pagina waar het zoekresultaat werd weergegeven. De waarde van deze eigenschap moet gelijk zijn aan een van de bekende opsommingswaarden die u definieert, zoals `top`, `side` of `bottom`. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)