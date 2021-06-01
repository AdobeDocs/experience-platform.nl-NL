---
keywords: Experience Platform;home;populaire onderwerpen;XDM;XDM systeem;XDM individueel profiel;XDM ExperienceEvent;XDM ExperienceEvent;ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;ExperienceDataModel;Experience gegevensmodel;Experience Data Model;Data Model;Data Model;Data Model;schema;Problemen;FAQ;Unieschema;UNION PROFILE;union profile;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;
solution: Experience Platform
title: XDM System Troubleshooting Guide
description: Hier vindt u antwoorden op veelgestelde vragen over het XDM (Experience Data Model), inclusief stappen voor het oplossen van veelvoorkomende API-fouten.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 415938f6f3aeec342774b73d1ae5f2dc0e27349c
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 0%

---

# Handleiding voor probleemoplossing voor XDM-systemen

Dit document biedt antwoorden op veelgestelde vragen over [!DNL Experience Data Model] (XDM) en XDM System in Adobe Experience Platform, inclusief een gids voor probleemoplossing voor algemene fouten. Raadpleeg de [handleiding voor het oplossen van Experience Platforms](../landing/troubleshooting.md) voor vragen en het oplossen van problemen met betrekking tot andere services van Platforms.

**[!DNL Experience Data Model](XDM)** is een open-bronspecificatie die gestandaardiseerde schema&#39;s voor het beheer van de klantenervaring bepaalt. De methode waarop [!DNL Experience Platform] wordt gebouwd, **XDM System**, exploiteert [!DNL Experience Data Model] schema&#39;s voor gebruik door [!DNL Platform] diensten. **[!DNL Schema Registry]** verstrekt een gebruikersinterface en een RESTful API om tot **[!DNL Schema Library]** binnen [!DNL Experience Platform] toegang te hebben. Zie [XDM documentatie](home.md) voor meer informatie.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over XDM System en het gebruik van de [!DNL Schema Registry] API.

### Hoe voeg ik velden toe aan een schema?

U kunt velden toevoegen aan een schema met behulp van een schemaveldgroep. Elke veldgroep is compatibel met een of meer klassen, zodat de veldgroep kan worden gebruikt in elk schema dat een van die compatibele klassen implementeert. Hoewel Adobe Experience Platform verschillende industrieveldgroepen hun eigen vooraf gedefinieerde velden biedt, kunt u uw eigen velden aan een schema toevoegen door aangepaste veldgroepen te maken met behulp van de API of de gebruikersinterface.

Voor details bij het creëren van gebiedsgroepen in [!DNL Schema Registry] API, zie [de gids van het gebiedseindpunt ](api/field-groups.md#create). Als u UI gebruikt, zie [het leerprogramma van de Redacteur van het Schema](./tutorials/create-schema-ui.md).

### Wat zijn de beste toepassingen voor veldgroepen versus gegevenstypen?

[Veldgroepen ](./schema/composition.md#field-group) zijn componenten die een of meer velden in een schema definiëren. Veldgroepen dwingen af hoe hun velden worden weergegeven in de hiërarchie van het schema en tonen daarom in elk schema dezelfde structuur aan waarin ze zijn opgenomen. Veldgroepen zijn alleen compatibel met specifieke klassen, zoals bepaald door het kenmerk `meta:intendedToExtend`.

[Gegevenstypen ](./schema/composition.md#data-type) kunnen ook een of meer velden voor een schema bevatten. In tegenstelling tot veldgroepen worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn.

### Wat is unieke identiteitskaart voor een schema?

Alle [!DNL Schema Registry] middelen (schema&#39;s, gebiedsgroepen, gegevenstypes, klassen) hebben URI die als unieke identiteitskaart voor verwijzing en raadplegingsdoeleinden dienst doet. Wanneer het bekijken van een schema in API, kan het in top-level `$id` en `meta:altId` attributen worden gevonden.

Zie de sectie [resource identification](api/getting-started.md#resource-identification) in de API-handleiding [!DNL Schema Registry] voor meer informatie.

### Wanneer begint een schema het breken van veranderingen te verhinderen?

Er kunnen verbrekende wijzigingen in een schema worden aangebracht zolang het schema nog nooit is gebruikt bij het maken van een gegevensset of is ingeschakeld voor gebruik in [[!DNL Real-time Customer Profile]](../profile/home.md). Zodra een schema in datasetverwezenlijking of toegelaten voor gebruik met [!DNL Real-time Customer Profile] is gebruikt, worden de regels van [Evolutie van het Schema](schema/composition.md#evolution) strikt gehandhaafd door het systeem.

### Wat is de maximumgrootte van een lang gebiedstype?

Een lang veldtype is een geheel getal met een maximale grootte van 53(+1) bits, waardoor het een mogelijk bereik heeft tussen -9007199254740992 en 9007199254740992. Dit komt door een beperking van de manier waarop JavaScript-implementaties van JSON lange gehele getallen vertegenwoordigen.

Voor meer informatie over gebiedstypes, zie het document op [XDM gebiedstype beperkingen](./schema/field-constraints.md).

### Hoe definieer ik identiteiten voor mijn schema?

In [!DNL Experience Platform], worden de identiteiten gebruikt om een onderwerp (typisch een individuele persoon) ongeacht de bronnen van gegevens te identificeren die worden geïnterpreteerd. Ze worden in schema&#39;s gedefinieerd door de sleutelvelden als &quot;Identiteit&quot; te markeren. Veelgebruikte gebieden voor identiteit omvatten e-mailadres, telefoonaantal, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), identiteitskaart van CRM, en andere unieke gebieden van identiteitskaart

Velden kunnen als id&#39;s worden gemarkeerd met de API of de gebruikersinterface.

#### Identiteiten definiëren in de API

In de API worden identiteiten vastgesteld door identiteitsbeschrijvers te maken. Identiteitsbeschrijvers geven aan dat een bepaalde eigenschap voor een schema een unieke id is.

De beschrijvers van de identiteit worden gecreeerd door een verzoek van de POST aan het /descriptors eindpunt. Als dit lukt, ontvangt u een HTTP Status 201 (Gemaakt) en een reactieobject met de details van de nieuwe descriptor.

Zie het document over de sectie [descriptors](api/descriptors.md) in de [!DNL Schema Registry]-handleiding voor ontwikkelaars voor meer informatie over het maken van identiteitsbeschrijvers in de API.

#### Identiteiten definiëren in de gebruikersinterface

Open het schema in de Schema-editor en selecteer het veld in de sectie **[!UICONTROL Structure]** van de editor dat u als identiteit wilt markeren. Selecteer onder **[!UICONTROL Field Properties]** aan de rechterkant het selectievakje **[!UICONTROL Identity]**.

Voor meer details over het beheren van identiteiten in UI, zie de sectie over [het bepalen van identiteitsgebieden](./tutorials/create-schema-ui.md#identity-field) in het leerprogramma van de Redacteur van het Schema.

### Heeft mijn schema een primaire identiteit nodig?

Primaire identiteiten zijn optioneel, omdat schema&#39;s ofwel nul ofwel één ervan kunnen hebben. Nochtans, moet een schema een primaire identiteit hebben opdat het schema voor gebruik in [!DNL Real-time Customer Profile] wordt toegelaten. Zie de sectie [identity](./tutorials/create-schema-ui.md#identity-field) van de zelfstudie van de Redacteur van het Schema voor meer informatie.

### Hoe laat ik een schema voor gebruik in [!DNL Real-time Customer Profile] toe?

De schema&#39;s worden toegelaten voor gebruik in [[!DNL Real-time Customer Profile]](../profile/home.md) door de toevoeging van een &quot;unie&quot;markering binnen het `meta:immutableTags` attribuut van het schema. Het toelaten van een schema voor gebruik met [!DNL Profile] kan worden gedaan gebruikend API of de gebruikersinterface.

#### Bezig met inschakelen van een bestaand schema voor [!DNL Profile] met behulp van de API

Voer een PATCH-verzoek in om het schema bij te werken en het kenmerk `meta:immutableTags` toe te voegen als een array met de waarde &quot;union&quot;. Als de update succesvol is, zal de reactie het bijgewerkte schema tonen dat nu de verenigingsmarkering bevat.

Voor meer informatie over het gebruiken van API om een schema voor gebruik in [!DNL Real-time Customer Profile] toe te laten, zie [union](./api/unions.md) document van [!DNL Schema Registry] ontwikkelaarsgids.

#### Het toelaten van een bestaand schema voor [!DNL Profile] gebruikend UI

Selecteer [!DNL Experience Platform] in de linkernavigatie en selecteer de naam van het schema dat u wilt inschakelen in de lijst met schema&#39;s. **[!UICONTROL Schemas]** Selecteer vervolgens **[!UICONTROL Profile]** aan de rechterkant van de editor onder **[!UICONTROL Schema Properties]** om deze in of uit te schakelen.


Zie de sectie over [gebruik in Real-time Klantprofiel](./tutorials/create-schema-ui.md#profile) in de zelfstudie [!UICONTROL Schema Editor] voor meer informatie.

### Kan ik een samenvoegingsschema direct uitgeven?

Unieschema&#39;s zijn alleen-lezen en worden automatisch gegenereerd door het systeem. Ze kunnen niet rechtstreeks worden bewerkt. Unieschema&#39;s worden voor een specifieke klasse gemaakt wanneer een tag union wordt toegevoegd aan een schema dat die klasse implementeert.

Voor meer informatie over unies in XDM, zie [union](./api/unions.md) sectie in de [!DNL Schema Registry] API gids.

### Hoe moet ik mijn gegevensbestand formatteren om gegevens in mijn schema in te voeren?

[!DNL Experience Platform] Accepteert gegevensbestanden in één van beide  [!DNL Parquet] of formaat JSON. De inhoud van deze dossiers moet met het schema in overeenstemming zijn dat door de dataset van verwijzingen wordt voorzien. Zie [batchverwerking overzicht](../ingestion/home.md) voor meer informatie over de beste werkwijzen voor het opnemen van gegevensbestanden.

## Fouten en problemen oplossen

Hieronder volgt een lijst met foutberichten die kunnen optreden wanneer u werkt met de API [!DNL Schema Registry].

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
>Afhankelijk van het middeltype dat wordt teruggewonnen, kan deze fout om het even welke volgende `type` URIs gebruiken:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Voor meer informatie bij het construeren van raadplegingswegen in API, zie [container](./api/getting-started.md#container) en [middelidentificatie](api/getting-started.md#resource-identification) secties in [!DNL Schema Registry] ontwikkelaarsgids.

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

De middelen die door uw organisatie IMS worden bepaald moeten hun gebieden onder uw huurdersidentiteitskaart namespace om conflicten met andere industrie en verkopersmiddelen te vermijden. Wanneer het bouwen van een schema gebruikend standaardgebiedsgroepen, om het even welke douanegebieden die u binnen de structuur van die gebiedsgroepen toevoegt moeten ook namespaced onder uw huurdersidentiteitskaart zijn.

>[!NOTE]
>
>Afhankelijk van de specifieke aard van de naamruimtefout kan deze fout elk van de volgende `type` URI&#39;s gebruiken samen met verschillende berichtdetails:
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

Voor aanvragen van GET in de [!DNL Schema Registry] API is een `Accept`-header vereist, zodat het systeem kan bepalen hoe de reactie moet worden opgemaakt. Deze fout treedt op wanneer een vereiste `Accept`-koptekst ongeldig is of ontbreekt.

Afhankelijk van het eindpunt u gebruikt, wijst het `detailed-message` bezit erop wat een geldige `Accept` kopbal als voor een succesvolle reactie zou moeten kijken. Controleer of u de juiste `Accept`-header hebt ingevoerd die compatibel is met het API-verzoek dat u wilt uitvoeren, voordat u het opnieuw probeert.

>[!NOTE]
>
>Afhankelijk van het eindpunt dat wordt gebruikt, kan deze fout om het even welke volgende `type` URIs gebruiken:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Voor lijsten van compatibele Accept kopballen voor verschillende API verzoeken, gelieve te verwijzen naar hun overeenkomstige secties in [de ontwikkelaarsgids van de Registratie van het Schema](./api/overview.md).

### [!DNL Real-time Customer Profile] fouten

De volgende foutberichten zijn gekoppeld aan bewerkingen die zijn betrokken bij het inschakelen van schema&#39;s voor [!DNL Real-time Customer Profile]. Zie de [union](./api/unions.md) sectie in de [!DNL Schema Registry] API gids voor meer informatie.

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

Dit foutenbericht toont wanneer u probeert om een schema voor [!DNL Profile] toe te laten en één van zijn eigenschappen bevat een relatiebeschrijver zonder een beschrijver van de verwijzingsidentiteit. Voeg een beschrijver van de verwijzingsIdentiteit aan het schemagebied in kwestie toe om deze fout op te lossen.

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

Om schema&#39;s toe te laten die relatiebeschrijvers voor gebruik in [!DNL Profile] bevatten, moet namespace van het brongebied en primaire namespace van het doelgebied het zelfde zijn. Dit foutbericht wordt weergegeven wanneer u een schema wilt inschakelen dat een naamruimte zonder overeenkomst bevat voor de verwijzingsidentiteitsbeschrijving. Zorg ervoor dat de `xdm:namespace`-waarde van het identiteitsveld van het doelschema overeenkomt met die van de eigenschap `xdm:identityNamespace` in de verwijzingsidentiteitsbeschrijving van het bronveld om dit probleem op te lossen.

Zie de sectie over [standaardnaamruimten](../identity-service/namespaces.md) in het overzicht van naamruimte voor identiteiten voor een lijst met standaardnaamruimtecodes.

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

Alvorens een schema voor Profiel toe te laten, moet u eerst [een primaire identiteitsbeschrijver](./api/descriptors.md#create) voor het schema creëren, of een gebied van de identiteitskaart omvatten om bij de primaire identiteit in plaats daarvan te handelen.