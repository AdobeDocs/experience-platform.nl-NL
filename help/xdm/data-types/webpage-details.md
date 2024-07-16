---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Webpagina-details;datatype;gegevenstype;gegevenstype;webpagina
solution: Experience Platform
title: Gegevenstype webpagina Details
description: Meer informatie over het gegevenstype Experience Data Model (XDM) van de webpagina.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# [!UICONTROL Web page details] gegevenstype

[!UICONTROL Web page details] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat details over een Web-pagina beschrijft die net is geladen en bekeken, zoals geregistreerd door een ExperienceEvent.

Het gegevenstype is bedoeld voor alle paginagegevens en voor het eerst laden van webtoepassingen van één pagina (SPA). Voor interactie die op een geladen pagina gebeuren die geen nieuwe paginading teweegbrengt, zie het ](./web-interaction.md) gegevenstype van de 0} Webinteractie {.[

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Measure]](./measure.md) | Het aantal weergaven op een webpagina. |
| `URL` | String | De normatieve of gebruikelijke URL van de webpagina. Dit kan al dan niet de daadwerkelijke URL zijn die wordt gebruikt om de pagina te bereiken. Gebruik `webLink` om de URL op te nemen die wordt gebruikt om de pagina te bereiken. Het formaat van URI zou [ RFC 3986 ](https://tools.ietf.org/html/rfc3986) norm moeten volgen. |
| `isErrorPage` | Boolean | Deze eigenschap gebruikt een markering om aan te geven of de pagina een foutpagina is of niet. Deze markering wordt gebruikt om webinteracties breed te categoriseren. De fout wordt gedefinieerd door de toepassing en kan overeenkomen met een pagina die wordt aangeboden met een HTTP-foutcode. |
| `isHomePage` | Boolean | Deze eigenschap gebruikt een markering om aan te geven of de pagina een homepage is of niet. Deze markering wordt gebruikt om webinteracties breed te categoriseren. De definitie van de homepage wordt bepaald door de toepassing. |
| `name` | String | De normatieve naam van de webpagina. Deze naam is niet noodzakelijkerwijs de paginatitel of is rechtstreeks gekoppeld aan pagina-inhoud, maar wordt gebruikt om de pagina&#39;s van een site te ordenen voor classificatiedoeleinden. |
| `server` | String | De normatieve of gebruikelijke server die de webpagina host. Dit kan al dan niet de gastheer of de server zijn die eigenlijk de paginainteractie aandiende. |
| `siteSection` | String | De normatieve naam van de sitesectie waarin deze webpagina zich bevindt. Dit kan worden gebruikt om de interactie te classificeren of te categoriseren. |
| `viewName` | String | De naam van de weergave, binnen een pagina. Deze eigenschap wordt meestal gebruikt bij toepassingen of pagina&#39;s van één pagina die tabs of besturingselementen hebben die het merendeel van de paginalay-out wijzigen. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
