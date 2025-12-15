---
keywords: Experience Platform;populaire onderwerpen;XDM;XDM-systeem;XDM individueel profiel;XDM ExperienceEvent;XDM Experience Event;ExperienceEvent;Experience Event;XDM ExperienceEvent;XDM ExperienceEvent;Experience data model;Experience data model;Experience Data Model;Data Model;Data Model;schema;probleemoplossing;FAQ;faq;Union schema;UNION PROFILE;union profile;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: XDM System Troubleshooting Guide
description: Hier vindt u antwoorden op veelgestelde vragen over het XDM (Experience Data Model), inclusief stappen voor het oplossen van veelvoorkomende API-fouten.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 8ba80a1cc4529f9d4693e3f7cbd7584193915410
workflow-type: tm+mt
source-wordcount: '2368'
ht-degree: 0%

---

# Handleiding voor probleemoplossing voor XDM-systemen

Dit document bevat antwoorden op veelgestelde vragen over [!DNL Experience Data Model] (XDM) en XDM System in Adobe Experience Platform, waaronder een gids voor probleemoplossing voor algemene fouten. Voor vragen en het oplossen van problemen met betrekking tot andere diensten van Experience Platform, gelieve te verwijzen naar de [&#x200B; het oplossen van problemengids van Experience Platform &#x200B;](../landing/troubleshooting.md).

**[!DNL Experience Data Model] (XDM)** is een open-bronspecificatie die gestandaardiseerde schema&#39;s voor het beheer van de klantenervaring bepaalt. De methodologie waarop [!DNL Experience Platform] wordt gebouwd, **XDM Systeem**, exploiteert [!DNL Experience Data Model] schema&#39;s voor gebruik door [!DNL Experience Platform] diensten. De **[!DNL Schema Registry]** biedt een gebruikersinterface en een RESTful-API voor toegang tot de **[!DNL Schema Library]** within [!DNL Experience Platform] -API. Zie de [&#x200B; documentatie XDM &#x200B;](home.md) voor meer informatie.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over XDM System en het gebruik van de [!DNL Schema Registry] API.

## Basisbeginselen van schema

In deze sectie vindt u antwoorden op fundamentele vragen over schemastructuur, veldgebruik en identificatie in het XDM-systeem.

### Hoe voeg ik velden toe aan een schema?

U kunt velden aan een schema toevoegen met een schemaveldgroep. Elke veldgroep is compatibel met een of meer klassen, zodat de veldgroep kan worden gebruikt in elk schema dat een van die compatibele klassen implementeert. Hoewel Adobe Experience Platform verschillende industrieveldgroepen hun eigen vooraf gedefinieerde velden biedt, kunt u uw eigen velden aan een schema toevoegen door aangepaste veldgroepen te maken met behulp van de API of de gebruikersinterface.

Voor details bij het creëren van gebiedsgroepen in [!DNL Schema Registry] API, zie de [&#x200B; gids van het het eindpunt van de gebiedsgroep &#x200B;](api/field-groups.md#create). Als u UI gebruikt, zie het [&#x200B; leerprogramma van de Redacteur van het Schema &#x200B;](./tutorials/create-schema-ui.md).

### Wat zijn de beste toepassingen voor veldgroepen versus gegevenstypen?

[&#x200B; de groepen van het Gebied &#x200B;](./schema/composition.md#field-group) zijn componenten die één of meerdere gebieden in een schema bepalen. Veldgroepen dwingen af hoe hun velden worden weergegeven in de hiërarchie van het schema en tonen daarom in elk schema dezelfde structuur aan waarin ze zijn opgenomen. Veldgroepen zijn alleen compatibel met specifieke klassen, zoals bepaald door het kenmerk `meta:intendedToExtend` ervan.

[&#x200B; de types van Gegevens &#x200B;](./schema/composition.md#data-type) kunnen één of meerdere gebieden voor een schema ook verstrekken. In tegenstelling tot veldgroepen worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn.

### Wat is unieke identiteitskaart voor een schema?

Alle [!DNL Schema Registry] -bronnen (schema&#39;s, veldgroepen, gegevenstypen, klassen) hebben een URI die fungeert als unieke id voor referentie- en opzoekdoeleinden. Wanneer u een schema in de API weergeeft, vindt u dit in de kenmerken `$id` en `meta:altId` op hoofdniveau.

Voor meer informatie, zie de [&#x200B; middelidentificatie &#x200B;](api/getting-started.md#resource-identification) sectie in de [!DNL Schema Registry] API gids.

### Wat is de maximumgrootte van een lang gebiedstype?

Een lang veldtype is een geheel getal met een maximale grootte van 53(+1) bits, waardoor het een mogelijk bereik heeft tussen -9007199254740992 en 900719925474092. Dit is te wijten aan een beperking van de manier waarop JavaScript-implementaties van JSON lange gehele getallen vertegenwoordigen.

Voor meer informatie over gebiedstypes, zie het document op [&#x200B; XDM gebied typegrenzen &#x200B;](./schema/field-constraints.md).

### Wat is meta :AltId?

`meta:altId` is een unieke id voor een schema. `meta:altId` verstrekt gemakkelijk om identiteitskaart voor gebruik in API vraag van verwijzingen te voorzien. Met deze id vermijdt u dat deze telkens moet worden gecodeerd/gedecodeerd als deze wordt gebruikt, net als bij de JSON URI-indeling.
<!-- (Needs clarification - How do I retrieve it INCOMPLETE) ... -->

<!-- ### How can I generate a sample payload for a schema? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

### Wat zijn de gebruiksbeperkingen voor een gegevenstype van een kaart?

XDM plaatst de volgende beperkingen op het gebruik van dit gegevenstype:

- Kaarttypen MOETEN van het type `object` zijn.
- Voor typen toewijzingen MOET GEEN eigenschap zijn gedefinieerd (met andere woorden, ze definiëren &quot;lege&quot; objecten).
- Kaarttypen MOETEN een `additionalProperties.type` -veld bevatten dat de waarden beschrijft die binnen de kaart kunnen worden geplaatst, `string` of `integer` .
- Segmentatie tussen meerdere entiteiten kan alleen worden gedefinieerd op basis van de kaarttoetsen en niet op basis van de waarden.
- Kaarten worden niet ondersteund voor accountpubliek.
- Kaarten die zijn gedefinieerd in aangepaste XDM-objecten, zijn beperkt tot één niveau. Geneste kaarten kunnen niet worden gemaakt. Deze beperking geldt niet voor kaarten die zijn gedefinieerd in standaard XDM-objecten.
- Arrays met kaarten worden niet ondersteund.

Zie de [&#x200B; gebruiksbeperkingen voor kaartvoorwerpen &#x200B;](./ui/fields/map.md#restrictions) voor meer details.

>[!NOTE]
>
>Kaarten op meerdere niveaus of kaarten worden niet ondersteund.

<!-- You cannot create a complex map object. However, you can define map fields in the Schema Editor. See the guide on [defining map fields in the UI](./ui/fields/map.md) for more information. -->

<!-- ### How do I create a complex map object using APIs? -->

<!-- You cannot create a complex map object. -->

<!-- ### How can I manage schema inheritance in Adobe Experience Platform? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

## Schema Identity Management

Deze sectie bevat antwoorden op veelgestelde vragen over het definiëren en beheren van identiteiten binnen uw schema&#39;s.

### Hoe definieer ik identiteiten voor mijn schema?

In [!DNL Experience Platform] worden identiteiten gebruikt om een onderwerp (doorgaans een individuele persoon) te identificeren, ongeacht de bronnen van gegevens die worden geïnterpreteerd. Ze worden in schema&#39;s gedefinieerd door de sleutelvelden als &quot;Identiteit&quot; te markeren. Veelgebruikte gebieden voor identiteit omvatten e-mailadres, telefoonaantal, [[!DNL Experience Cloud ID (ECID)] &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL), identiteitskaart van CRM, en andere unieke gebieden van identiteitskaart

Velden kunnen als id&#39;s worden gemarkeerd met de API of de gebruikersinterface.

### Identiteiten definiëren in de API

In de API worden identiteiten vastgesteld door identiteitsbeschrijvers te maken. Identiteitsbeschrijvers geven aan dat een bepaalde eigenschap voor een schema een unieke id is.

De beschrijvers van de identiteit worden gecreeerd door een POST- verzoek aan het /descriptors eindpunt. Als dit lukt, ontvangt u een HTTP Status 201 (Gemaakt) en een reactieobject met de details van de nieuwe descriptor.

Voor meer details bij het creëren van identiteitsbeschrijvers in API, zie het document op [&#x200B; beschrijvers &#x200B;](api/descriptors.md) sectie in de [!DNL Schema Registry] ontwikkelaarsgids.

### Identiteiten definiëren in de gebruikersinterface

Open het schema in de Schema-editor en selecteer het veld in de sectie **[!UICONTROL Structure]** van de editor dat u als identiteit wilt markeren. Selecteer onder **[!UICONTROL Field Properties]** aan de rechterkant het selectievakje **[!UICONTROL Identity]** .

Voor meer details bij het beheren van identiteiten in UI, zie de sectie over [&#x200B; het bepalen van identiteitsgebieden &#x200B;](./tutorials/create-schema-ui.md#identity-field) sectie in het leerprogramma van de Redacteur van het Schema.

### Heeft mijn schema een primaire identiteit nodig?

Primaire identiteiten zijn optioneel, omdat schema&#39;s ofwel nul ofwel één ervan kunnen hebben. Een schema moet echter een primaire identiteit hebben voordat het schema kan worden ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile] . Zie de [&#x200B; identiteit &#x200B;](./tutorials/create-schema-ui.md#identity-field) sectie van het leerprogramma van de Redacteur van het Schema voor meer informatie.

## Schema profiel inschakelen

Deze sectie verstrekt begeleiding bij het toelaten van schema&#39;s voor gebruik met het Profiel van de Klant in real time.

### Hoe kan ik een schema inschakelen voor gebruik in [!DNL Real-Time Customer Profile]?

Schema&#39;s kunnen in [[!DNL Real-Time Customer Profile]](../profile/home.md) worden gebruikt door een tag &quot;union&quot; toe te voegen binnen het kenmerk `meta:immutableTags` van het schema. U kunt een schema inschakelen voor gebruik met [!DNL Profile] via de API of de gebruikersinterface.

### Een bestaand schema voor [!DNL Profile] inschakelen met de API

Voer een PATCH-verzoek in om het schema bij te werken en het kenmerk `meta:immutableTags` toe te voegen als een array met de waarde &quot;union&quot;. Als de update succesvol is, zal de reactie het bijgewerkte schema tonen dat nu de verenigingsmarkering bevat.

Voor meer informatie bij het gebruiken van API om een schema voor gebruik in [!DNL Real-Time Customer Profile] toe te laten, zie het [&#x200B; vakbonden &#x200B;](./api/unions.md) document van de [!DNL Schema Registry] ontwikkelaarsgids.

### Bezig met inschakelen van een bestaand schema voor [!DNL Profile] via de gebruikersinterface

Selecteer [!DNL Experience Platform] in **[!UICONTROL Schemas]** in de linkernavigatie en selecteer in de lijst met schema&#39;s de naam van het schema dat u wilt inschakelen. Selecteer vervolgens aan de rechterkant van de editor onder **[!UICONTROL Schema Properties]** de optie **[!UICONTROL Profile]** om deze in of uit te schakelen.

Voor meer informatie, zie de sectie over [&#x200B; gebruik in het Profiel van de Klant in real time &#x200B;](./tutorials/create-schema-ui.md#profile) in het [!UICONTROL Schema Editor] leerprogramma.

### Wanneer Adobe Analytics-gegevens als bron worden geïmporteerd, wordt het automatisch gemaakte schema ingeschakeld voor Profiel?

Het schema wordt niet automatisch toegelaten voor het Profiel van de Klant in real time. U moet uitdrukkelijk de dataset voor Profiel toelaten dat wordt gebaseerd op welk schema voor Profiel wordt toegelaten. Zie de documentatie om de [&#x200B; stappen en vereisten te leren nodig om een dataset voor gebruik in het Profiel van de Klant in real time &#x200B;](../catalog/datasets/user-guide.md#enable-profile) toe te laten.

### Kan ik profiel-toegelaten schema&#39;s schrappen? {#delete-profile-enabled}

U kunt geen schema schrappen nadat het voor het Profiel van de Klant in real time is toegelaten. Als een schema eenmaal is ingeschakeld voor Profiel, kan het niet worden uitgeschakeld of verwijderd en kunnen velden niet uit het schema worden verwijderd. Daarom is het essentieel om de schemaconfiguratie zorgvuldig te plannen en te verifiëren alvorens het voor Profiel toe te laten. U kunt een profiel-Toegelaten dataset echter schrappen. Hier vindt u informatie: <https://experienceleague.adobe.com/nl/docs/experience-platform/catalog/datasets/user-guide#delete-a-profile-enabled-dataset>

Als u niet meer voor een profiel-toegelaten schema wenst te worden gebruikt, adviseert het om het schema anders te noemen om **te omvatten** of **niet Inactief** gebruiken.

## Wijziging en beperkingen van het schema

Deze sectie verstrekt verduidelijkingen over de regels van de schemawijziging en de preventie van het breken van veranderingen.

### Wanneer begint een schema het breken van veranderingen te verhinderen?

Er kunnen verbluffende wijzigingen in een schema worden aangebracht zolang het schema nog nooit is gebruikt bij het maken van een gegevensset of is ingeschakeld voor gebruik in [[!DNL Real-Time Customer Profile]](../profile/home.md) . Zodra een schema in datasetverwezenlijking of toegelaten voor gebruik met [!DNL Real-Time Customer Profile] is gebruikt, worden de regels van [&#x200B; Evolutie van het Schema &#x200B;](schema/composition.md#evolution) strikt afgedwongen door het systeem.

### Kan ik een samenvoegingsschema direct uitgeven?

Unieschema&#39;s zijn alleen-lezen en worden automatisch gegenereerd door het systeem. Ze kunnen niet rechtstreeks worden bewerkt. Unieschema&#39;s worden voor een specifieke klasse gemaakt wanneer een tag union wordt toegevoegd aan een schema dat die klasse implementeert.

Voor meer informatie over unies in XDM, zie de [&#x200B; vakbonden &#x200B;](./api/unions.md) sectie in de [!DNL Schema Registry] API gids.

### Hoe moet ik mijn gegevensbestand formatteren om gegevens in mijn schema in te voeren?

[!DNL Experience Platform] accepteert gegevensbestanden in [!DNL Parquet] - of JSON-indeling. De inhoud van deze dossiers moet met het schema in overeenstemming zijn dat door de dataset van verwijzingen wordt voorzien. Voor details over beste praktijken voor datafile ingestie, zie het [&#x200B; overzicht van partijingestitie &#x200B;](../ingestion/home.md).

### Hoe kan ik een schema in een read-only schema omzetten?

U kunt een schema momenteel niet omzetten in alleen-lezen.

## Fouten en problemen oplossen

Hieronder volgt een lijst met foutberichten die kunnen optreden wanneer u werkt met de API van [!DNL Schema Registry] .

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

Deze fout wordt weergegeven wanneer het systeem een bepaalde bron niet kan vinden. De bron kan zijn verwijderd of het pad in de API-aanroep is ongeldig. Controleer of u een geldig pad voor uw API-aanroep hebt ingevoerd voordat u het opnieuw probeert. U kunt willen controleren dat u correcte identiteitskaart voor het middel bent ingegaan, en dat de weg behoorlijk genoemd met de aangewezen container (globaal of huurder) is.

>[!NOTE]
>
>Afhankelijk van het brontype dat wordt opgehaald, kan deze fout elk van de volgende `type` URI&#39;s gebruiken:
>
>- `http://ns.adobe.com/aep/errors/XDM-1010-404`
>- `http://ns.adobe.com/aep/errors/XDM-1011-404`
>- `http://ns.adobe.com/aep/errors/XDM-1012-404`
>- `http://ns.adobe.com/aep/errors/XDM-1013-404`
>- `http://ns.adobe.com/aep/errors/XDM-1014-404`
>- `http://ns.adobe.com/aep/errors/XDM-1015-404`
>- `http://ns.adobe.com/aep/errors/XDM-1016-404`
>- `http://ns.adobe.com/aep/errors/XDM-1017-404`

Voor meer informatie bij het construeren van raadplegingswegen in API, zie de [&#x200B; container &#x200B;](./api/getting-started.md#container) en [&#x200B; middelidentificatie &#x200B;](api/getting-started.md#resource-identification) secties in de [!DNL Schema Registry] ontwikkelaarsgids.

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

De middelen die door uw organisatie worden bepaald moeten hun gebieden onder uw huurdersidentiteitskaart namespace om conflicten met andere industrie en verkopersmiddelen te vermijden. Wanneer het bouwen van een schema gebruikend standaardgebiedsgroepen, om het even welke douanevelden die u binnen de structuur van die gebiedsgroepen toevoegt moeten ook namespaced onder uw huurdersidentiteitskaart zijn.

>[!NOTE]
>
>Afhankelijk van de specifieke aard van de naamruimtefout kan deze fout een van de volgende `type` URI&#39;s gebruiken samen met verschillende berichtdetails:
>
>- `http://ns.adobe.com/aep/errors/XDM-1020-400`
>- `http://ns.adobe.com/aep/errors/XDM-1021-400`
>- `http://ns.adobe.com/aep/errors/XDM-1022-400`
>- `http://ns.adobe.com/aep/errors/XDM-1023-400`
>- `http://ns.adobe.com/aep/errors/XDM-1024-400`

Gedetailleerde voorbeelden van juiste gegevensstructuren voor XDM-bronnen vindt u in de handleiding Schema Registry API:

- [Een aangepaste klasse maken](./api/classes.md#create)
- [Een aangepaste veldgroep maken](./api/field-groups.md#create)
- [Een aangepast gegevenstype maken](./api/data-types.md#create)

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

GET-aanvragen in de [!DNL Schema Registry] API vereisen een `Accept` -header, zodat het systeem kan bepalen hoe de reactie moet worden opgemaakt. Deze fout treedt op wanneer een vereiste `Accept` -koptekst ongeldig is of ontbreekt.

Afhankelijk van het eindpunt dat u gebruikt, geeft de eigenschap `detailed-message` aan hoe een geldige `Accept` -header eruit moet zien voor een geslaagde reactie. Controleer of u een `Accept` -header correct hebt ingevoerd die compatibel is met de API-aanvraag die u wilt uitvoeren voordat u het opnieuw probeert.

>[!NOTE]
>
>Afhankelijk van het eindpunt dat wordt gebruikt, kan deze fout om het even welke volgende `type` URIs gebruiken:
>
>- `http://ns.adobe.com/aep/errors/XDM-1006-400`
>- `http://ns.adobe.com/aep/errors/XDM-1007-400`
>- `http://ns.adobe.com/aep/errors/XDM-1008-400`
>- `http://ns.adobe.com/aep/errors/XDM-1009-400`

Voor lijsten van compatibele Accepteer kopballen voor verschillende API verzoeken, gelieve naar hun overeenkomstige secties in de [&#x200B; de ontwikkelaarsgids van de Registratie van het Schema &#x200B;](./api/overview.md) te verwijzen.

### [!DNL Real-Time Customer Profile] fouten

De volgende foutberichten zijn gekoppeld aan bewerkingen die van invloed zijn op het inschakelen van schema&#39;s voor [!DNL Real-Time Customer Profile] . Zie de [&#x200B; vakbonden &#x200B;](./api/unions.md) sectie in de [!DNL Schema Registry] API gids voor meer informatie.

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

Dit foutbericht wordt weergegeven wanneer u een schema voor [!DNL Profile] probeert in te schakelen en een van de eigenschappen een relatiebeschrijving zonder een verwijzings-id-descriptor bevat. Voeg een beschrijver van de verwijzingsIdentiteit aan het schemagebied in kwestie toe om deze fout op te lossen.

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

>[!NOTE]
>
>Voor deze fout verwijst het &quot;bestemmingsschema&quot;naar het verwijzingsschema in de verhouding.

Om schema&#39;s in te schakelen die relatiebeschrijvers voor gebruik in [!DNL Profile] bevatten, moeten de naamruimte van het bronveld en de primaire naamruimte van het verwijzingsveld gelijk zijn. Dit foutbericht wordt weergegeven wanneer u een schema wilt inschakelen dat een naamruimte zonder overeenkomst bevat voor de verwijzingsidentiteitsbeschrijving.

Zorg ervoor dat de `xdm:namespace` -waarde van het identiteitsveld van het referentieschema overeenkomt met die van de `xdm:identityNamespace` -eigenschap in het identiteitsbeschrijvingsbestand van het bronveld om dit probleem op te lossen.

Voor een lijst van standaardidentiteitsnamespacecodes, zie de sectie op [&#x200B; standaard namespaces &#x200B;](../identity-service/features/namespaces.md) in het overzicht van identiteitsnaamruimte.

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

Alvorens een schema voor Profiel toe te laten, moet u eerst [&#x200B; een primaire identiteitsbeschrijver &#x200B;](./api/descriptors.md#create) voor het schema creëren, of een gebied van de identiteitskaart omvatten om bij de primaire identiteit in plaats daarvan te handelen.

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
