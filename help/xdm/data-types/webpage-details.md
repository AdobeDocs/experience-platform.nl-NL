---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Webpagina-details;datatype;gegevenstype;gegevenstype;webpagina
solution: Experience Platform
title: Gegevenstype webpagina Details
topic-legacy: overview
description: Dit document biedt een overzicht van het gegevenstype Experience Data Model (XDM) van de webpagina voor details.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 2%

---

# [!UICONTROL Web page details] gegevenstype

[!UICONTROL Web page details] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat details over een Web-pagina beschrijft die net is geladen en bekeken, zoals geregistreerd door een ExperienceEvent.

Het gegevenstype is bedoeld voor alle paginagegevens en voor het eerst laden van webtoepassingen die uit één pagina bestaan (SPA). Zie het gegevenstype [webinteractie](./web-interactions.md) voor interacties die plaatsvinden op een geladen pagina die geen nieuwe paginading activeren.

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Measure]](./measure.md) | Het aantal weergaven op een webpagina. |
| `URL` | Tekenreeks | De normatieve of gebruikelijke URL van de webpagina. Dit kan al dan niet de daadwerkelijke URL zijn die wordt gebruikt om de pagina te bereiken. Gebruik `webLink` om de URL op te nemen die wordt gebruikt om de pagina te bereiken. De indeling URI moet de [RFC 3986](https://tools.ietf.org/html/rfc3986)-standaard volgen. |
| `isErrorPage` | Boolean | Deze eigenschap gebruikt een markering om aan te geven of de pagina een foutpagina is of niet. Deze markering wordt gebruikt om webinteracties breed te categoriseren. De fout wordt gedefinieerd door de toepassing en kan overeenkomen met een pagina die wordt aangeboden met een HTTP-foutcode. |
| `isHomePage` | Boolean | Deze eigenschap gebruikt een markering om aan te geven of de pagina een homepage is of niet. Deze markering wordt gebruikt om webinteracties breed te categoriseren. De definitie van de homepage wordt bepaald door de toepassing. |
| `name` | Tekenreeks | De normatieve naam van de webpagina. Deze naam is niet noodzakelijkerwijs de paginatitel of is rechtstreeks gekoppeld aan pagina-inhoud, maar wordt gebruikt om de pagina&#39;s van een site te ordenen voor classificatiedoeleinden. |
| `server` | Tekenreeks | De normatieve of gebruikelijke server die de webpagina host. Dit kan al dan niet de gastheer of de server zijn die eigenlijk de paginainteractie aandiende. |
| `siteSection` | Tekenreeks | De normatieve naam van de sitesectie waarin deze webpagina zich bevindt. Dit kan worden gebruikt om de interactie te classificeren of te categoriseren. |
| `viewName` | Tekenreeks | De naam van de weergave, binnen een pagina. Deze eigenschap wordt meestal gebruikt bij toepassingen of pagina&#39;s van één pagina die tabs of besturingselementen hebben die het merendeel van de paginalay-out wijzigen. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)
