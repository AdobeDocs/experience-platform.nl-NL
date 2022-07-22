---
keywords: Experience Platform;populaire onderwerpen;XDM;XDM-systeem;XDM individueel profiel;XDM ExperienceEvent;XDM Experience Event;ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;ExperienceData model;Experience data model;Experience Data Model;Data Model;Data Model;Data Model;schema;Problemen;FAQ;FAQ;Unieschema;UNION PROFILE;union profile;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: XDM System Troubleshooting Guide
description: Hier vindt u antwoorden op veelgestelde vragen over het XDM (Experience Data Model), inclusief stappen voor het oplossen van veelvoorkomende API-fouten.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 5ffc93c8715d1184b2a239c1d631b117a531e5c1
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 0%

---

# Handleiding voor probleemoplossing voor XDM-systemen

Dit document geeft antwoorden op veelgestelde vragen over [!DNL Experience Data Model] (XDM) en XDM System in Adobe Experience Platform, met inbegrip van een het oplossen van problemengids voor gemeenschappelijke fouten. Voor vragen en problemen met betrekking tot andere services van Platforms raadpleegt u de [Handleiding voor het oplossen van problemen met Experience Platforms](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** is een open-source specificatie die gestandaardiseerde schema&#39;s voor het beheer van de klantervaring definieert. De methode [!DNL Experience Platform] is gebouwd, **XDM-systeem**, operaliseert [!DNL Experience Data Model] schema&#39;s voor gebruik door [!DNL Platform] diensten. De **[!DNL Schema Registry]** biedt een gebruikersinterface en een RESTful-API voor toegang tot de **[!DNL Schema Library]** binnen [!DNL Experience Platform]. Zie de [XDM-documentatie](home.md) voor meer informatie .

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over XDM System en het gebruik van de [!DNL Schema Registry] API.

### Hoe voeg ik velden toe aan een schema?

U kunt velden toevoegen aan een schema met behulp van een schemaveldgroep. Elke veldgroep is compatibel met een of meer klassen, zodat de veldgroep kan worden gebruikt in elk schema dat een van die compatibele klassen implementeert. Hoewel Adobe Experience Platform verschillende industrieveldgroepen hun eigen vooraf gedefinieerde velden biedt, kunt u uw eigen velden aan een schema toevoegen door aangepaste veldgroepen te maken met behulp van de API of de gebruikersinterface.

Voor meer informatie over het maken van veldgroepen in het dialoogvenster [!DNL Schema Registry] API, zie [eindhulplijn veldgroep](api/field-groups.md#create). Als u UI gebruikt, zie [Zelfstudie Schema Editor](./tutorials/create-schema-ui.md).

### Wat zijn de beste toepassingen voor veldgroepen versus gegevenstypen?

[Veldgroepen](./schema/composition.md#field-group) zijn componenten die een of meer velden in een schema definiëren. Veldgroepen dwingen af hoe hun velden worden weergegeven in de hiërarchie van het schema en tonen daarom in elk schema dezelfde structuur aan waarin ze zijn opgenomen. Veldgroepen zijn alleen compatibel met specifieke klassen, zoals bepaald door hun `meta:intendedToExtend` kenmerk.

[Gegevenstypen](./schema/composition.md#data-type) U kunt ook een of meer velden voor een schema opgeven. In tegenstelling tot veldgroepen worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn.

### Wat is unieke identiteitskaart voor een schema?

Alles [!DNL Schema Registry] resources (schema&#39;s, veldgroepen, gegevenstypen, klassen) hebben een URI die fungeert als een unieke id voor referentie- en opzoekdoeleinden. Wanneer u een schema in de API weergeeft, vindt u dit in het bovenste niveau `$id` en `meta:altId` kenmerken.

Zie voor meer informatie de [resource-id](api/getting-started.md#resource-identification) in de [!DNL Schema Registry] API-handleiding.

### Wanneer begint een schema het breken van veranderingen te verhinderen?

Het breken kan veranderingen in een schema worden aangebracht zolang het nooit in de verwezenlijking van een dataset of toegelaten voor gebruik in is gebruikt [[!DNL Real-time Customer Profile]](../profile/home.md). Zodra een schema in datasetverwezenlijking is gebruikt of voor gebruik met toegelaten [!DNL Real-time Customer Profile], de regels van [Schemaevolutie](schema/composition.md#evolution) strikt door het systeem worden gehandhaafd.

### Wat is de maximumgrootte van een lang gebiedstype?

Een lang veldtype is een geheel getal met een maximale grootte van 53(+1) bits, waardoor het een mogelijk bereik heeft tussen -9007199254740992 en 9007199254740992. Dit komt door een beperking van de manier waarop JavaScript-implementaties van JSON lange gehele getallen vertegenwoordigen.

Zie het document over [Beperkingen voor XDM-veldtypen](./schema/field-constraints.md).

### Hoe definieer ik identiteiten voor mijn schema?

In [!DNL Experience Platform], worden identiteiten gebruikt om een onderwerp (gewoonlijk een individuele persoon) te identificeren ongeacht de bronnen van gegevens die worden geïnterpreteerd. Ze worden in schema&#39;s gedefinieerd door de sleutelvelden als &quot;Identiteit&quot; te markeren. Veelgebruikte velden voor identiteiten zijn e-mailadres, telefoonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM-id en andere unieke id-velden.

Velden kunnen als id&#39;s worden gemarkeerd met de API of de gebruikersinterface.

#### Identiteiten definiëren in de API

In de API worden identiteiten vastgesteld door identiteitsbeschrijvers te maken. Identiteitsbeschrijvers geven aan dat een bepaalde eigenschap voor een schema een unieke id is.

De beschrijvers van de identiteit worden gecreeerd door een verzoek van de POST aan het /descriptors eindpunt. Als dit lukt, ontvangt u een HTTP Status 201 (Gemaakt) en een reactieobject met de details van de nieuwe descriptor.

Zie het document op [beschrijvingen](api/descriptors.md) in de [!DNL Schema Registry] ontwikkelaarshandleiding.

#### Identiteiten definiëren in de gebruikersinterface

Open het schema in de Schema-editor en selecteer het veld in het dialoogvenster **[!UICONTROL Structure]** in de editor die u als een identiteit wilt markeren. Onder **[!UICONTROL Field Properties]** aan de rechterkant selecteert u de **[!UICONTROL Identity]** selectievakje.

Zie de sectie over het [identiteitsvelden definiëren](./tutorials/create-schema-ui.md#identity-field) in de zelfstudie van de Schema-editor.

### Heeft mijn schema een primaire identiteit nodig?

Primaire identiteiten zijn optioneel, omdat schema&#39;s ofwel nul ofwel één ervan kunnen hebben. Een schema moet echter een primaire identiteit hebben voordat het schema kan worden ingeschakeld voor gebruik in [!DNL Real-time Customer Profile]. Zie de [identiteit](./tutorials/create-schema-ui.md#identity-field) voor meer informatie.

### Hoe laat ik een schema voor gebruik binnen toe [!DNL Real-time Customer Profile]?

Schema&#39;s zijn ingeschakeld voor gebruik in [[!DNL Real-time Customer Profile]](../profile/home.md) door de toevoeging van een tag &quot; union &quot; binnen de `meta:immutableTags` kenmerk van het schema. Een schema inschakelen voor gebruik met [!DNL Profile] kan worden uitgevoerd met de API of de gebruikersinterface.

#### Een bestaand schema inschakelen voor [!DNL Profile] API gebruiken

Voer een PATCH-verzoek in om het schema bij te werken en het `meta:immutableTags` attribuut as an array containing the value &quot;union&quot;. Als de update succesvol is, zal de reactie het bijgewerkte schema tonen dat nu de verenigingsmarkering bevat.

Voor meer informatie over het gebruiken van API om een schema voor gebruik toe te laten binnen [!DNL Real-time Customer Profile], zie de [vakbonden](./api/unions.md) document van de [!DNL Schema Registry] ontwikkelaarshandleiding.

#### Een bestaand schema inschakelen voor [!DNL Profile] gebruiken van UI

In [!DNL Experience Platform], selecteert u **[!UICONTROL Schemas]** in de linkernavigatie, en selecteer de naam van het schema u wenst om van de lijst van schema&#39;s toe te laten. Dan, aan de rechterkant van de redacteur onder **[!UICONTROL Schema Properties]**, selecteert u **[!UICONTROL Profile]** om het aan te schakelen.


Zie de sectie over [gebruik in het profiel van de Klant in real time](./tutorials/create-schema-ui.md#profile) in de [!UICONTROL Schema Editor] zelfstudie.

### Kan ik een samenvoegingsschema direct uitgeven?

Unieschema&#39;s zijn alleen-lezen en worden automatisch gegenereerd door het systeem. Ze kunnen niet rechtstreeks worden bewerkt. Unieschema&#39;s worden voor een specifieke klasse gemaakt wanneer een tag union wordt toegevoegd aan een schema dat die klasse implementeert.

Voor meer informatie over vakbonden in XDM, zie [vakbonden](./api/unions.md) in de [!DNL Schema Registry] API-handleiding.

### Hoe moet ik mijn gegevensbestand formatteren om gegevens in mijn schema in te voeren?

[!DNL Experience Platform] accepteert gegevensbestanden in beide [!DNL Parquet] of JSON-indeling. De inhoud van deze dossiers moet met het schema in overeenstemming zijn dat door de dataset van verwijzingen wordt voorzien. Zie voor meer informatie over de aanbevolen procedures voor het opnemen van gegevensbestanden de [overzicht van batch-opname](../ingestion/home.md).

## Fouten en problemen oplossen

Hieronder volgt een lijst met foutberichten die u kunt tegenkomen wanneer u werkt met de [!DNL Schema Registry] API.

### Bron niet gevonden

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

Deze fout wordt weergegeven wanneer het systeem een bepaalde bron niet kan vinden. De bron kan zijn verwijderd of het pad in de API-aanroep is ongeldig. Controleer of u een geldig pad voor uw API-aanroep hebt ingevoerd voordat u het opnieuw probeert. U kunt willen controleren dat u correcte identiteitskaart voor het middel bent ingegaan, en dat de weg behoorlijk namespaced met de aangewezen container (globaal of huurder) is.

>[!NOTE]
>
>Afhankelijk van het type resource dat wordt opgehaald, kan deze fout elk van de volgende methoden gebruiken `type` URI&#39;s:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Zie voor meer informatie over het samenstellen van opzoekpaden in de API de [container](./api/getting-started.md#container) en [resource-id](api/getting-started.md#resource-identification) in de [!DNL Schema Registry] ontwikkelaarshandleiding.

### Titel is niet uniek

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

Dit foutbericht wordt weergegeven wanneer u een bron probeert te maken met een titel die al door een andere bron wordt gebruikt. Titels moeten uniek zijn voor alle typen bronnen. Als u bijvoorbeeld een veldgroep probeert te maken met een titel die al wordt gebruikt door een schema, ontvangt u deze fout.

### Validatiefout naamruimte

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

Dit foutbericht wordt weergegeven wanneer u een bron probeert te maken met velden met een onjuiste naam of wanneer u onjuist benoemde velden toevoegt aan een bestaande bron.

De middelen die door uw organisatie IMS worden bepaald moeten hun gebieden onder uw huurdersidentiteitskaart namespace om conflicten met andere industrie en verkopersmiddelen te vermijden. Wanneer het bouwen van een schema gebruikend standaardgebiedsgroepen, om het even welke douanevelden die u binnen de structuur van die gebiedsgroepen toevoegt moeten ook namespaced onder uw huurdersidentiteitskaart zijn.

>[!NOTE]
>
>Afhankelijk van de specifieke aard van de naamruimtefout kan deze fout een van de volgende methoden gebruiken `type` URI&#39;s samen met verschillende berichtdetails:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Gedetailleerde voorbeelden van juiste gegevensstructuren voor XDM-bronnen vindt u in de handleiding Schema Registry API:

* [Een aangepaste klasse maken](./api/classes.md#create)
* [Een aangepaste veldgroep maken](./api/field-groups.md#create)
* [Een aangepast gegevenstype maken](./api/data-types.md#create)

### Koptekst accepteren is ongeldig

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

De verzoeken van de GET in [!DNL Schema Registry] API vereist een `Accept` zodat het systeem kan bepalen hoe de reactie wordt opgemaakt. Deze fout treedt op wanneer een vereiste `Accept` header is ongeldig of ontbreekt.

Afhankelijk van het eindpunt gebruikt u, `detailed-message` eigenschap geeft aan wat een geldige waarde is `Accept` header moet eruit zien als een succesvol antwoord . Zorg ervoor dat u de juiste gegevens hebt ingevoerd en `Accept` -header die compatibel is met de API-aanvraag die u wilt uitvoeren, voordat u het opnieuw probeert.

>[!NOTE]
>
>Afhankelijk van het eindpunt dat wordt gebruikt, kan deze fout om het even welk volgend gebruiken `type` URI&#39;s:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Voor lijsten met compatibele Accept-headers voor verschillende API-aanvragen raadpleegt u de bijbehorende secties in het dialoogvenster [Handleiding voor ontwikkelaars van het schema Register](./api/overview.md).

### [!DNL Real-time Customer Profile] fouten

De volgende foutberichten zijn gekoppeld aan bewerkingen die zijn betrokken bij het inschakelen van schema&#39;s voor [!DNL Real-time Customer Profile]. Zie de [vakbonden](./api/unions.md) in de [!DNL Schema Registry] API-handleiding voor meer informatie.

#### Er moet een identiteitsbeschrijving voor verwijzingen zijn

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

Dit foutbericht wordt weergegeven wanneer u een schema wilt inschakelen voor [!DNL Profile] en een van de eigenschappen ervan bevat een relatiedescriptor zonder een referentie-id-descriptor. Voeg een beschrijver van de verwijzingsIdentiteit aan het schemagebied in kwestie toe om deze fout op te lossen.

#### De naamruimten van het beschrijvingsveld voor de referentie-id en het doelschema moeten overeenkomen

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

Om schema&#39;s toe te laten die relatiebeschrijvers voor gebruik binnen bevatten [!DNL Profile], moeten de naamruimte van het bronveld en de primaire naamruimte van het doelveld gelijk zijn. Dit foutbericht wordt weergegeven wanneer u een schema wilt inschakelen dat een naamruimte zonder overeenkomst bevat voor de verwijzingsidentiteitsbeschrijving. Zorg ervoor dat de `xdm:namespace` de waarde van het de identiteitsgebied van het bestemmingsschema past dat van aan `xdm:identityNamespace` in de ID-beschrijving van de bronveld om dit probleem op te lossen.

Zie de sectie over een lijst met standaardnaamruimtecodes voor identiteiten [standaardnaamruimten](../identity-service/namespaces.md) in het naamruimteoverzicht van de identiteit.

#### Het schema moet een identityMap of primaire identiteit bevatten

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

Voordat u een schema inschakelt voor Profiel, moet u eerst [een primaire identiteitsdescriptor maken](./api/descriptors.md#create) voor het schema, of omvat een gebied van de identiteitskaart om bij de primaire identiteit in plaats daarvan te handelen.

#### Kan incompatibele gegevenstypen niet samenvoegen

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

Alle profiel-toegelaten schema&#39;s die tot de zelfde klasse behoren moeten samen kunnen samenvoegen om het verenigingsschema voor die klasse te construeren. Deze fout verschijnt wanneer u een gebied aan een schema probeert toe te voegen de waarvan weg door een ander profiel-toegelaten schema wordt gedeeld en het gegevenstype verschillend is dan origineel. Aangezien de schema&#39;s zowel profiel-toegelaten zijn als het zelfde gebiedspad bevatten, zou het Profiel proberen om deze twee gebieden in één samen te voegen wanneer het construeren van het verenigingsschema. Omdat verschillende gegevenstypen niet samen kunnen worden samengevoegd, wordt dit beschouwd als een samenvoegconflict en is dit niet toegestaan.

U lost het probleem op door een andere naam voor het veld te kiezen of het onder een uniek, naamloos object te nesten om samenvoegconflicten met andere, voor profiel geschikte schema&#39;s onder dezelfde klasse met vergelijkbare velden te voorkomen.
