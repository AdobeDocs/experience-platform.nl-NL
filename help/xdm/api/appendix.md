---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Schema Register;Schema Register;Compatibiliteit;Compatibiliteitsmodus;Compatibiliteitsmodus;Veld type;veldtypen;
solution: Experience Platform
title: Aanhangsel voor schema-registratie-API
description: Dit document bevat aanvullende informatie over het werken met de API voor het registreren van het schema.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---

# Handboek Schema Register API-handleiding

Dit document bevat aanvullende informatie over het werken met de [!DNL Schema Registry] API.

## Query-parameters gebruiken {#query}

[!DNL Schema Registry] steunt het gebruik van vraagparameters aan pagina en filterresultaten wanneer het vermelden van middelen.

>[!NOTE]
>
>Wanneer het combineren van veelvoudige vraagparameters, moeten zij door ampersands (`&`) worden gescheiden.

### Paginering {#paging}

De gemeenschappelijkste vraagparameters voor het pagineren omvatten:

| Parameter | Beschrijving |
| --- | --- |
| `orderby` | Resultaten sorteren op een bepaalde eigenschap. Voorbeeld: `orderby=title` sorteert de resultaten op titel in oplopende volgorde (A-Z). Wanneer u een `-` vóór de parameterwaarde ( `orderby=-title` ) toevoegt, worden items op titel gesorteerd in aflopende volgorde (Z-A). |
| `limit` | Wanneer `orderby` samen met een parameter wordt gebruikt, beperkt `limit` het maximumaantal items dat voor een bepaalde aanvraag moet worden geretourneerd. Deze parameter kan niet worden gebruikt zonder dat er een parameter `orderby` aanwezig is.<br><br> de `limit` parameter specificeert een positief geheel (tussen `0` en `500`) als a *wenk* over het maximumaantal punten dat zou moeten zijn teruggekeerd. `limit=5` retourneert bijvoorbeeld slechts vijf bronnen in de lijst. Deze waarde wordt echter niet strikt nageleefd. De werkelijke responsgrootte kan kleiner of groter zijn, zoals wordt beperkt door de noodzaak om de betrouwbare werking van de parameter `start` te bieden, als er een wordt opgegeven. |
| `start` | Wanneer gebruikt in combinatie met een parameter `orderby` , geeft `start` aan waar de lijst met items in de subset moet beginnen. Deze parameter kan niet worden gebruikt zonder dat er een parameter `orderby` aanwezig is. Deze waarde kan worden verkregen uit het `_page.next` -kenmerk van een lijstreactie en worden gebruikt om de volgende pagina met resultaten te openen. Als de waarde `_page.next` null is, is er geen extra pagina beschikbaar.<br><br> typisch, wordt deze parameter weggelaten om de eerste pagina van resultaten te verkrijgen. Vervolgens moet `start` worden ingesteld op de maximumwaarde van de primaire sorteereigenschap van het `orderby` -veld dat in de vorige pagina is ontvangen. De API-reactie retourneert vervolgens items die beginnen met items met een primaire sorteereigenschap van `orderby` strikt groter dan (voor oplopend) of strikt kleiner dan (voor aflopend) de opgegeven waarde.<br><br> Bijvoorbeeld, als de `orderby` parameter aan `orderby=name,firstname` wordt geplaatst, zou de `start` parameter een waarde voor het `name` bezit bevatten. In dit geval, als u de volgende 20 ingangen van een middel onmiddellijk na de naam &quot;Miller&quot;wilde tonen, zou u gebruiken: `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### Filteren {#filtering}

U kunt resultaten filteren met de parameter `property` , die wordt gebruikt om een specifieke operator toe te passen op een bepaalde JSON-eigenschap binnen de opgehaalde bronnen. Tot de ondersteunde operatoren behoren:

| Operator | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `==` | Filtert op of de eigenschap gelijk is aan de opgegeven waarde. | `property=title==test` |
| `!=` | Filtert op of de eigenschap niet gelijk is aan de opgegeven waarde. | `property=title!=test` |
| `<` | Filtert op of de eigenschap kleiner is dan de opgegeven waarde. | `property=version<5` |
| `>` | Filtert op of de eigenschap groter is dan de opgegeven waarde. | `property=version>5` |
| `<=` | Filtert op of de eigenschap kleiner dan of gelijk is aan de opgegeven waarde. | `property=version<=5` |
| `>=` | Filtert op of de eigenschap groter dan of gelijk is aan de opgegeven waarde. | `property=version>=5` |
| (Geen) | Wanneer alleen de naam van de eigenschap wordt opgegeven, worden alleen items geretourneerd waar de eigenschap bestaat. | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>U kunt de parameter `property` gebruiken om schemagebiedgroepen door hun compatibele klasse te filtreren. `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` retourneert bijvoorbeeld alleen veldgroepen die compatibel zijn met de klasse [!DNL XDM Individual Profile] .

## Compatibiliteitsmodus {#compatibility}

[!DNL Experience Data Model] (XDM) is een openbaar gedocumenteerde specificatie, die door Adobe wordt gedreven om de interoperabiliteit, de expressiviteit, en de macht van digitale ervaringen te verbeteren. Adobe handhaaft de broncode en de formele definities XDM in een [ open bronproject op GitHub ](https://github.com/adobe/xdm/). Deze definities worden geschreven in de Standaardaantekening XDM, gebruikend JSON-LD (de Nota van de Objecten van JavaScript voor Gekoppelde Gegevens) en Schema JSON als grammatica voor het bepalen van schema&#39;s XDM.

Wanneer u formele XDM-definities bekijkt in de openbare opslagplaats, ziet u dat standaard XDM verschilt van wat u in Adobe Experience Platform ziet. Wat u ziet in [!DNL Experience Platform] , wordt Compatibiliteitsmodus genoemd en biedt een eenvoudige toewijzing tussen standaard-XDM en de manier waarop deze wordt gebruikt binnen [!DNL Experience Platform] .

### Hoe de Wijze van de Verenigbaarheid werkt

De Wijze van de verenigbaarheid staat het model XDM JSON-LD toe om met bestaande gegevensinfrastructuur te werken door waarden binnen standaardXDM te veranderen terwijl het houden van de semantiek het zelfde. Er wordt een geneste JSON-structuur gebruikt, waarbij schema&#39;s in een boomachtige indeling worden weergegeven.

Het belangrijkste verschil tussen de standaard-XDM en de compatibiliteitsmodus is de verwijdering van het voorvoegsel &quot;xdm:&quot; voor veldnamen.

Hieronder volgt een vergelijking naast elkaar van verjaardagsgerelateerde velden (met verwijderde &quot;beschrijving&quot;-kenmerken) in zowel standaard XDM- als compatibiliteitsmodus. De velden Compatibiliteitsmodus bevatten een verwijzing naar het XDM-veld en het gegevenstype ervan in de kenmerken &quot;meta:xdmField&quot; en &quot;meta:xdmType&quot;.

<table style="table-layout:auto">
  <th>Standaard XDM</th>
  <th>Compatibiliteitsmodus</th>
  <tr>
  <td>
  <pre class=" language-json">
&lbrace;
  "xdm:bornDate": &lbrace;
    "titel": "geboortedatum",
    "type": "string",
    "format": "date"
  &rbrace;,
  "xdm:bornDayAndMonth": &lbrace;
    "titel": "geboortedatum",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]"
  &rbrace;,
  "xdm:bornYear": &lbrace;
    "titel": "geboortejaar";
    "type": "integer",
    "minimum": 1,
    "maximum": 32767
  &rbrace;
&rbrace;
  </pre>
  </td>
  <td>
  <pre class=" language-json">
&lbrace;
  "bornDate": &lbrace;
    "titel": "geboortedatum",
    "type": "string",
    "format": "date",
    "meta:xdmField": "xdm:bornDate",
    "meta:xdmType": "date"
  &rbrace;,
  "bornDayAndMonth": &lbrace;
    "titel": "geboortedatum",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]",
    "meta:xdmField": "xdm:bornDayAndMonth",
    "meta:xdmType": "string"
  &rbrace;,
  "bornYear": &lbrace;
    "titel": "geboortejaar";
    "type": "integer",
    "minimum": 1,
    "maximum": 32767,
    "meta:xdmField": "xdm:bornYear",
    "meta:xdmType": "short"
  &rbrace;
&rbrace;
      </pre>
  </td>
  </tr>
</table>

### Waarom is de Wijze van de Verenigbaarheid noodzakelijk?

Adobe Experience Platform is ontworpen om met meerdere oplossingen en services te werken, elk met hun eigen technische uitdagingen en beperkingen (bijvoorbeeld hoe bepaalde technologieën speciale tekens verwerken). Om deze beperkingen te verhelpen, werd de compatibiliteitsmodus ontwikkeld.

De meeste [!DNL Experience Platform] -services, inclusief [!DNL Catalog] , [!DNL Data Lake] en [!DNL Real-Time Customer Profile] use [!DNL Compatibility Mode] , vervangen door standaard-XDM. De [!DNL Schema Registry] API gebruikt ook [!DNL Compatibility Mode] en de voorbeelden in dit document worden allemaal weergegeven met [!DNL Compatibility Mode] .

Het is de moeite waard om te weten dat een afbeelding plaatsvindt tussen standaard XDM en de manier waarop het in [!DNL Experience Platform] wordt uitgevoerd, maar het zou niet uw gebruik van [!DNL Experience Platform] diensten moeten beïnvloeden.

Het opensource-project is beschikbaar voor u, maar als u communiceert met bronnen via de [!DNL Schema Registry] , bieden de API-voorbeelden in dit document de beste praktijken die u moet kennen en volgen.
