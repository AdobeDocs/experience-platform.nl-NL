---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Gegevensmodel;Gegevensmodel;Schema register;Schema Register;Compatibiliteit;Compatibiliteitsmodus;Compatibiliteitsmodus;veldtype;veldtypen;
solution: Experience Platform
title: Aanhangsel voor schema-registratie-API
description: Dit document bevat aanvullende informatie over het werken met de API voor het registreren van het schema.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# Handboek Schema Register API-handleiding

Dit document bevat aanvullende informatie over het werken met de [!DNL Schema Registry] API.

## Query-parameters gebruiken {#query}

De [!DNL Schema Registry] ondersteunt het gebruik van queryparameters voor pagina- en filterresultaten bij het weergeven van bronnen.

>[!NOTE]
>
>Wanneer het combineren van veelvoudige vraagparameters, moeten zij door ampersands ( worden gescheiden`&`).

### Paginering {#paging}

De gemeenschappelijkste vraagparameters voor het pagineren omvatten:

| Parameter | Beschrijving |
| --- | --- |
| `orderby` | Resultaten sorteren op een bepaalde eigenschap. Voorbeeld: `orderby=title` sorteert de resultaten op titel in oplopende volgorde (A-Z). Een `-` vóór de parameterwaarde (`orderby=-title`) worden objecten op titel gesorteerd in aflopende volgorde (Z-A). |
| `limit` | Indien gebruikt in combinatie met een `orderby` parameter, `limit` beperkt het maximumaantal items dat voor een bepaald verzoek moet worden geretourneerd. Deze parameter kan niet worden gebruikt zonder een `orderby` parameter aanwezig.<br><br>De `limit` parameter geeft een positief geheel getal aan (tussen `0` en `500`) als *hint* over het maximumaantal objecten dat moet worden geretourneerd. Bijvoorbeeld: `limit=5` retourneert slechts vijf bronnen in de lijst. Deze waarde wordt echter niet strikt nageleefd. De werkelijke responsgrootte kan kleiner of groter zijn, omdat de betrouwbare werking van de `start` parameter, als er een wordt opgegeven. |
| `start` | Indien gebruikt in combinatie met een `orderby` parameter, `start` Hiermee geeft u aan waar de sublijst met items moet beginnen. Deze parameter kan niet worden gebruikt zonder een `orderby` parameter aanwezig. Deze waarde kan worden verkregen via de `_page.next` kenmerk van een reactie in een lijst en gebruikt voor toegang tot de volgende pagina met resultaten. Als de `_page.next` De waarde is null en er is geen extra pagina beschikbaar.<br><br>Deze parameter wordt meestal weggelaten om de eerste pagina met resultaten te verkrijgen. Daarna, `start` moet worden ingesteld op de maximumwaarde van de primaire sorteereigenschap van de `orderby` veld ontvangen op de vorige pagina. De API-reactie retourneert vervolgens items die beginnen met items met een primaire sorteereigenschap van `orderby` strikt groter dan (voor oplopend) of strikt kleiner dan (voor aflopend) de gespecificeerde waarde.<br><br>Als de `orderby` parameter is ingesteld op `orderby=name,firstname`de `start` parameter zou een waarde voor de `name` eigenschap. In dit geval, als u de volgende 20 ingangen van een middel onmiddellijk na de naam &quot;Miller&quot;wilde tonen, zou u gebruiken: `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### Filteren {#filtering}

U kunt de resultaten filteren met de `property` parameter, die wordt gebruikt om een specifieke exploitant op een bepaalde bezit JSON binnen de teruggewonnen middelen toe te passen. Tot de ondersteunde operatoren behoren:

| Operator | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `==` | Filtert op of de eigenschap gelijk is aan de opgegeven waarde. | `property=title==test` |
| `!=` | Filtert op of de eigenschap niet gelijk is aan de opgegeven waarde. | `property=title!=test` |
| `<` | Filtert op of de eigenschap kleiner is dan de opgegeven waarde. | `property=version<5` |
| `>` | Filtert op of de eigenschap groter is dan de opgegeven waarde. | `property=version>5` |
| `<=` | Filtert op of de eigenschap kleiner dan of gelijk is aan de opgegeven waarde. | `property=version<=5` |
| `>=` | Filtert op of de eigenschap groter dan of gelijk is aan de opgegeven waarde. | `property=version>=5` |
| `~` | Filtert op of de eigenschap overeenkomt met een opgegeven reguliere expressie. | `property=title~test$` |
| (Geen) | Wanneer alleen de naam van de eigenschap wordt opgegeven, worden alleen items geretourneerd waar de eigenschap bestaat. | `property=title` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>U kunt de `property` parameter om schemagebiedgroepen door hun compatibele klasse te filtreren. Bijvoorbeeld: `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` Hiermee worden alleen veldgroepen geretourneerd die compatibel zijn met de [!DNL XDM Individual Profile] klasse.

## Compatibiliteitsmodus {#compatibility}

[!DNL Experience Data Model] (XDM) is een openbaar gedocumenteerde specificatie, die door Adobe wordt gedreven om de interoperabiliteit, de expressiviteit, en de macht van digitale ervaringen te verbeteren. Adobe handhaaft de broncode en de formele definities XDM in een [open-bronproject op GitHub](https://github.com/adobe/xdm/). Deze definities worden geschreven in de Standaardaantekening XDM, gebruikend JSON-LD (de Nota van Objecten JavaScript voor Gekoppelde Gegevens) en Schema JSON als grammatica voor het bepalen van XDM schema&#39;s.

Wanneer u formele XDM-definities bekijkt in de openbare opslagplaats, ziet u dat standaard XDM verschilt van wat u in Adobe Experience Platform ziet. Wat u ziet in [!DNL Experience Platform] wordt genoemd de Wijze van de Verenigbaarheid, en het verstrekt een eenvoudige afbeelding tussen standaard XDM en de manier het binnen wordt gebruikt [!DNL Platform].

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
{
  "xdm:birthDate": {
    "title": "Birth Date",
    "type": "string",
    "format": "date"
  },
  "xdm:birthDayAndMonth": {
    "title": "Birth Date",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]"
  },
  "xdm:birthYear": {
    "title": "Birth year",
    "type": "integer",
    "minimum": 1,
    "maximum": 32767
  }
}
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{
  "birthDate": {
    "title": "Birth Date",
    "type": "string",
    "format": "date",
    "meta:xdmField": "xdm:birthDate",
    "meta:xdmType": "date"
  },
  "birthDayAndMonth": {
    "title": "Birth Date",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]",
    "meta:xdmField": "xdm:birthDayAndMonth",
    "meta:xdmType": "string"
  },
  "birthYear": {
    "title": "Birth year",
    "type": "integer",
    "minimum": 1,
    "maximum": 32767,
    "meta:xdmField": "xdm:birthYear",
    "meta:xdmType": "short"
  }
}
      </pre>
  </td>
  </tr>
</table>

### Waarom is de Wijze van de Verenigbaarheid noodzakelijk?

Adobe Experience Platform is ontworpen om met meerdere oplossingen en services te werken, elk met hun eigen technische uitdagingen en beperkingen (bijvoorbeeld hoe bepaalde technologieën speciale tekens verwerken). Om deze beperkingen te verhelpen, werd de compatibiliteitsmodus ontwikkeld.

Meeste [!DNL Experience Platform] diensten, waaronder [!DNL Catalog], [!DNL Data Lake], en [!DNL Real-Time Customer Profile] gebruiken [!DNL Compatibility Mode] in plaats van standaard-XDM. De [!DNL Schema Registry] API gebruikt ook [!DNL Compatibility Mode]en de voorbeelden in dit document worden allemaal weergegeven met [!DNL Compatibility Mode].

Het is nuttig om te weten dat een afbeelding tussen standaard XDM en de manier plaatsvindt het binnen [!DNL Experience Platform], maar het mag uw gebruik van [!DNL Platform] diensten.

Het open bronproject is beschikbaar aan u, maar wanneer het over het in wisselwerking staan met middelen door [!DNL Schema Registry]De API-voorbeelden in dit document bieden de aanbevolen procedures die u moet kennen en volgen.
