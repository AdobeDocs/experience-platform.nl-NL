---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: Aanhangsel voor ontwikkelaar van het schemaregister
description: Dit document bevat aanvullende informatie over het werken met de API voor het registreren van het schema.
topic: developer guide
translation-type: tm+mt
source-git-commit: 42d3bed14c5f926892467baeeea09ee7a140ebdc
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Aanhangsel

Dit document bevat aanvullende informatie over het werken met de [!DNL Schema Registry] API.

## Compatibiliteitsmodus

[!DNL Experience Data Model] (XDM) is een openbaar gedocumenteerde specificatie, die door Adobe wordt gedreven om de interoperabiliteit, de expressiviteit, en de macht van digitale ervaringen te verbeteren. Adobe handhaaft de broncode en de formele definities XDM in een [open bronproject op GitHub](https://github.com/adobe/xdm/). Deze definities worden geschreven in de Standaardaantekening XDM, gebruikend JSON-LD (de Nota van Objecten JavaScript voor Gekoppelde Gegevens) en Schema JSON als grammatica voor het bepalen van XDM schema&#39;s.

Wanneer u formele XDM-definities bekijkt in de openbare opslagplaats, ziet u dat standaard XDM verschilt van wat u in Adobe Experience Platform ziet. Wat u ziet in [!DNL Experience Platform] wordt genoemd de Wijze van de Verenigbaarheid, en het verstrekt een eenvoudige afbeelding tussen standaardXDM en de manier het binnen wordt gebruikt [!DNL Platform].

### Hoe de Wijze van de Verenigbaarheid werkt

De Wijze van de verenigbaarheid staat het model XDM JSON-LD toe om met bestaande gegevensinfrastructuur te werken door waarden binnen standaardXDM te veranderen terwijl het houden van de semantiek het zelfde. Er wordt een geneste JSON-structuur gebruikt, waarbij schema&#39;s in een boomachtige indeling worden weergegeven.

Het belangrijkste verschil tussen de standaard-XDM en de compatibiliteitsmodus is de verwijdering van het voorvoegsel &quot;xdm:&quot; voor veldnamen.

Hieronder volgt een vergelijking naast elkaar van verjaardagsgerelateerde velden (met verwijderde &quot;beschrijving&quot;-kenmerken) in zowel standaard XDM- als compatibiliteitsmodus. De velden Compatibiliteitsmodus bevatten een verwijzing naar het XDM-veld en het gegevenstype ervan in de kenmerken &quot;meta:xdmField&quot; en &quot;meta:xdmType&quot;.

<table>
  <th>Standaard XDM</th>
  <th>Compatibiliteitsmodus</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {1} "xdm:bornDate": {1} "title": "Geboortedatum", "type": "string", "format": "date", }, "xdm:bornDayAndMonth": {1} "title": "Geboortedatum", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear": {1} "title": "Geboortejaar", "type": "integer", "minimum": 1, "maximum": 32767 }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        {"bornDate": {1} "title": "Geboortedatum", "type": "string", "format": "date", "meta:xdmField": "xdm:bornDate", "meta:xdmType": "date" }, "bornDayAndMonth": {1} "title": "Geboortedatum", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth", "meta:xdmType": "string" }, "bornYear": {1} "title": "Geboortejaar", "type": "integer", "minimum": 1, "maximum": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### Waarom is de Wijze van de Verenigbaarheid noodzakelijk?

Adobe Experience Platform is ontworpen om met meerdere oplossingen en services te werken, elk met hun eigen technische uitdagingen en beperkingen (bijvoorbeeld hoe bepaalde technologieën speciale tekens verwerken). Om deze beperkingen te verhelpen, werd de compatibiliteitsmodus ontwikkeld.

De meeste [!DNL Experience Platform] services, inclusief [!DNL Catalog], [!DNL Data Lake]en [!DNL Real-time Customer Profile] [!DNL Compatibility Mode] gebruik in plaats van standaard-XDM. De [!DNL Schema Registry] API gebruikt ook [!DNL Compatibility Mode]en de voorbeelden in dit document worden allemaal weergegeven met behulp van [!DNL Compatibility Mode].

Het is de moeite waard om te weten dat een afbeelding tussen standaard XDM en de manier plaatsvindt het binnen wordt operationeel [!DNL Experience Platform], maar het zou uw gebruik van de [!DNL Platform] diensten niet moeten beïnvloeden.

Het opensource-project is beschikbaar voor u, maar als u communiceert met bronnen via de [!DNL Schema Registry]API, bieden de API-voorbeelden in dit document de beste praktijken die u moet kennen en volgen.