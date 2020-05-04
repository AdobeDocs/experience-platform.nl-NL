---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: De gids van de het oplossen van problemen van het Systeem van de Gegevens van de Ervaring Model (XDM)
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# De gids van de het oplossen van problemen van het Systeem van de Gegevens van de Ervaring Model (XDM)

Dit document biedt antwoorden op veelgestelde vragen over het Systeem van de Gegevens van de Ervaring (XDM), evenals een het oplossen van problemengids voor gemeenschappelijke fouten. Raadpleeg de handleiding voor het oplossen van problemen bij het [ervaringsplatform voor vragen en het oplossen van problemen met betrekking tot andere services in het Adobe Experience Platform](../landing/troubleshooting.md).

**Het Model van Gegevens van de ervaring (XDM)** is een open-bronspecificatie die gestandaardiseerde schema&#39;s voor het beheer van de klantenervaring bepaalt. De methodologie waarop het Platform van de Ervaring wordt gebouwd, **XDM Systeem**, stelt de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform in werking. Het **Schemaregister** biedt een gebruikersinterface en een RESTful-API voor toegang tot de **Schemabibliotheek** binnen het Experience Platform. Zie de [XDM documentatie](home.md) voor meer informatie.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over XDM System en het gebruik van de Schema Registry API.

### Hoe voeg ik velden toe aan een schema?

U kunt velden aan een schema toevoegen met behulp van een mix. Elke mix is compatibel met een of meer klassen, waardoor de mix kan worden gebruikt in elk schema dat een van die compatibele klassen implementeert. Hoewel het Platform van de Ervaring van Adobe verscheidene industriemengins van hun eigen vooraf bepaalde gebieden voorziet, kunt u uw eigen gebieden aan een schema toevoegen door nieuwe mengen tot stand te brengen gebruikend API of de gebruikersinterface.

Zie de handleiding voor het [maken van een mixindocument](api/create-mixin.md) in de handleiding voor ontwikkelaars van de API voor het registreren van schema voor meer informatie over het maken van nieuwe mixins in de API. Als u UI gebruikt, zie het [leerprogramma](./tutorials/create-schema-ui.md)van de Redacteur van het Schema.

### Wat zijn de beste toepassingen voor mixins versus gegevenstypes?

[Mixins](./schema/composition.md#mixin) zijn componenten die een of meer velden in een schema definiëren. Mixins dwingen af hoe hun gebieden in de hiërarchie van het schema verschijnen, en tonen daarom de zelfde structuur in elk schema dat zij inbegrepen zijn. Mixins zijn alleen compatibel met specifieke klassen, zoals die door hun `meta:intendedToExtend` kenmerk worden geïdentificeerd.

[Gegevenstypen](./schema/composition.md#data-type) kunnen ook een of meer velden voor een schema bevatten. In tegenstelling tot mengsels, worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn.

### Wat is unieke identiteitskaart voor een schema?

Alle middelen van de Registratie van het Schema (schema&#39;s, mixins, gegevenstypes, klassen) hebben URI die als unieke identiteitskaart voor verwijzing en raadplegingsdoeleinden dienst doet. Wanneer u een schema in de API weergeeft, vindt u dit in de kenmerken op hoofdniveau `$id` en `meta:altId` kenmerken.

Voor meer informatie, zie de sectie van de [schemaidentificatie](api/getting-started.md#schema-identification) in de de ontwikkelaarsgids van de Registratie van het Schema API.

### Wanneer begint een schema het breken van veranderingen te verhinderen?

De het breken veranderingen kunnen in een schema worden aangebracht zolang het nooit in de verwezenlijking van een dataset of toegelaten voor gebruik in het Profiel [van de Klant](../profile/home.md)In real time is gebruikt. Zodra een schema in datasetverwezenlijking of toegelaten voor gebruik met het Profiel van de Klant in real time is gebruikt, worden de regels van de Evolutie [van het](schema/composition.md#evolution) Schema strikt gehandhaafd door het systeem.

### Wat is de maximumgrootte van een lang gebiedstype?

Een lang veldtype is een geheel getal met een maximale grootte van 53(+1) bits, waardoor het een mogelijk bereik heeft tussen -9007199254740992 en 9007199254740992. Dit komt door een beperking van de manier waarop JavaScript-implementaties van JSON lange gehele getallen vertegenwoordigen.

Voor meer informatie over gebiedstypes, zie de [Defining XDM gebiedstypes](api/appendix.md#field-types) sectie in de de ontwikkelaarsgids van de Registratie van het Schema API.

### Hoe definieer ik identiteiten voor mijn schema?

In het ervaringsplatform worden identiteiten gebruikt om een onderwerp (doorgaans een individuele persoon) te identificeren, ongeacht de bronnen van gegevens die worden geïnterpreteerd. Ze worden in schema&#39;s gedefinieerd door de sleutelvelden als &quot;Identiteit&quot; te markeren. Veelgebruikte velden voor identiteiten zijn e-mailadres, telefoonnummer, [Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/en/id-service/using/home.html), CRM-id en andere unieke id-velden.

Velden kunnen als id&#39;s worden gemarkeerd met de API of de gebruikersinterface.

#### Identiteiten definiëren in de API

In de API worden identiteiten vastgesteld door identiteitsbeschrijvers te maken. Identiteitsbeschrijvers geven aan dat een bepaalde eigenschap voor een schema een unieke id is.

De beschrijvers van de identiteit worden gecreeerd door een POST- verzoek aan het /descriptors eindpunt. Als dit lukt, ontvangt u een HTTP Status 201 (Gemaakt) en een reactieobject met de details van de nieuwe descriptor.

Zie het document over de sectie [descriptors](api/descriptors.md) in de handleiding voor ontwikkelaars van het schema voor meer informatie over het maken van identiteitsbeschrijvers in de API.

#### Identiteiten definiëren in de gebruikersinterface

Open het schema in de Schema-editor en klik in de sectie **Structuur** van de editor op het veld dat u als identiteit wilt markeren. Klik rechts onder **Veldeigenschappen** op het selectievakje **Identiteit** .

Zie de sectie over het [definiëren van identiteitsvelden](./tutorials/create-schema-ui.md#identity-field) in de zelfstudie van de Schema-editor voor meer informatie over het beheren van identiteiten in de gebruikersinterface.

### Heeft mijn schema een primaire identiteit nodig?

Primaire id&#39;s zijn optioneel omdat schema&#39;s er 0 of 1 kunnen hebben. Nochtans, moet een schema een primaire identiteit hebben opdat het schema voor gebruik in het Profiel van de Klant in real time wordt toegelaten. Zie de [identiteitssectie](./tutorials/create-schema-ui.md#identity-field) van het leerprogramma van de Redacteur van het Schema voor meer informatie.

### Hoe laat ik een schema voor gebruik in het Profiel van de Klant in real time toe?

De schema&#39;s worden toegelaten voor gebruik in het Profiel [van de Klant in](../profile/home.md) real time door de toevoeging van een &quot;unie&quot;markering, die in de `meta:immutableTags` attributen van het schema wordt gevestigd. U kunt een schema inschakelen voor gebruik met profiel via de API of de gebruikersinterface.

#### Een bestaand schema voor profiel inschakelen met de API

Voer een PATCH-verzoek in om het schema bij te werken en het `meta:immutableTags` kenmerk toe te voegen als een array met de waarde &quot;union&quot;. Als de update succesvol is, zal de reactie het bijgewerkte schema tonen dat nu de verenigingsmarkering bevat.

Voor meer informatie bij het gebruiken van API om een schema voor gebruik in het Profiel van de Klant in real time toe te laten, zie het [uniendocument](./api/unions.md) van de de ontwikkelaarsgids van het Registratie van het Schema.

#### Het toelaten van een bestaand schema voor Profiel gebruikend UI

Klik in Experience Platform op **Schema** &#39;s in de linkernavigatie en selecteer de naam van het schema dat u wilt inschakelen in de lijst met schema&#39;s. Klik vervolgens rechts van de editor onder **Schemaeigenschappen** op **Profiel** om deze in of uit te schakelen.


Voor meer informatie, zie de sectie over [gebruik in het Profiel](./tutorials/create-schema-ui.md#profile) van de Klant in real time in de Redacteur van het Schema zelfstudie.

### Kan ik een samenvoegingsschema direct uitgeven?

Unieschema&#39;s zijn alleen-lezen en worden automatisch gegenereerd door het systeem. Ze kunnen niet rechtstreeks worden bewerkt. Unieschema&#39;s worden voor een specifieke klasse gemaakt wanneer een tag union wordt toegevoegd aan een schema dat die klasse implementeert.

Voor meer informatie over unies in XDM, zie de [vakbondssectie](./api/unions.md) in de de ontwikkelaarsgids van de Registratie van het Schema API.

### Hoe moet ik mijn gegevensbestand formatteren om gegevens in mijn schema in te voeren?

Het Platform van de ervaring keurt gegevensdossiers in of Parquet of formaat JSON goed. De inhoud van deze dossiers moet met het schema in overeenstemming zijn dat door de dataset van verwijzingen wordt voorzien. Voor details over beste praktijken voor gegevensuitwisseling, zie het [batch ingesinsectieoverzicht](../ingestion/home.md).

## Fouten en problemen oplossen

Hieronder volgt een lijst met foutberichten die u kunt tegenkomen wanneer u werkt met de API voor schemaregistratie.

### Object niet gevonden

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

Deze fout wordt weergegeven wanneer het systeem een bepaalde bron niet kan vinden. De bron kan zijn verwijderd of het pad in de API-aanroep is ongeldig. Controleer of u een geldig pad voor uw API-aanroep hebt ingevoerd voordat u het opnieuw probeert. U kunt willen controleren dat u correcte identiteitskaart voor het middel bent ingegaan, en dat de weg behoorlijk namespaced met de aangewezen container (globaal of huurder) is.

Voor meer informatie bij het construeren van raadplegingswegen in API, zie de [container](./api/getting-started.md#container) en de secties van de [schemaidentificatie](api/getting-started.md#schema-identification) in de de ontwikkelaarsgids van de Registratie van het Schema.

### Titel moet uniek zijn

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

Dit foutbericht wordt weergegeven wanneer u een bron probeert te maken met een titel die al door een andere bron wordt gebruikt. Titels moeten uniek zijn voor alle typen bronnen. Als u bijvoorbeeld een mix probeert te maken met een titel die al wordt gebruikt door een schema, ontvangt u deze fout.

### Aangepaste velden moeten een veld op hoofdniveau gebruiken

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

Dit foutbericht wordt weergegeven wanneer u een nieuwe mix probeert te maken met velden met een onjuiste naam. Mixins die door uw IMS-organisatie zijn gedefinieerd, moeten hun velden naamruimte geven met een naamruimte `TENANT_ID` om conflicten met andere bronnen in de branche en de leverancier te voorkomen. Gedetailleerde voorbeelden van juiste gegevensstructuren voor mixins zijn te vinden in het document over het [creëren van een mixinsectie](api/create-mixin.md) in de ontwikkelaarsgids voor de Registratie van het Schema API.


### Fouten in het realtime profiel van de klant

De volgende foutberichten zijn gekoppeld aan bewerkingen die betrokken zijn bij het inschakelen van schema&#39;s voor realtime-klantprofiel. Zie de [vaksectie](./api/unions.md) in de ontwikkelaarsgids voor het Registratie van het Schema API voor meer informatie.

#### Om profieldatasets toe te laten zou het schema geldig moeten zijn

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Dit foutenbericht toont wanneer u probeert om een profieldataset voor een schema toe te laten dat niet voor het Profiel van de Klant in real time is toegelaten. Zorg ervoor dat het schema een verenigingsmarkering bevat alvorens de dataset toe te laten.

#### Er moet een identiteitsbeschrijving voor verwijzingen zijn

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

Dit foutbericht wordt weergegeven wanneer u een schema voor Profiel probeert in te schakelen en een van de eigenschappen een relatiebeschrijving bevat zonder een verwijzings-id-descriptor. Voeg een beschrijver van de verwijzingsIdentiteit aan het schemagebied in kwestie toe om deze fout op te lossen.

#### De naamruimten van het beschrijvingsveld voor de referentie-id en het doelschema moeten overeenkomen

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

Om schema&#39;s toe te laten die relatiebeschrijvers voor gebruik in Profiel bevatten, moet namespace van het brongebied en primaire namespace van het doelgebied het zelfde zijn. Dit foutbericht wordt weergegeven wanneer u een schema wilt inschakelen dat een naamruimte zonder overeenkomst bevat voor de verwijzingsidentiteitsbeschrijving. Zorg ervoor dat de `xdm:namespace` waarde van het de identiteitsgebied van het bestemmingsschema dat van het `xdm:identityNamespace` bezit in de beschrijver van de verwijzingsidentiteit van het brongebied aanpast om deze kwestie op te lossen.

Zie de sectie over [standaardnaamruimten](../identity-service/namespaces.md) in het overzicht van naamruimte voor identiteiten voor een lijst met ondersteunde naamruimtecodes.

### Koptekstfouten accepteren

De meeste GET verzoeken in de Registratie API van het Schema vereisen Accept kopbal voor het systeem om te bepalen hoe te om de reactie te formatteren. Hieronder volgt een lijst met veelvoorkomende fouten die aan de koptekst Accepteren zijn gekoppeld. Voor lijsten van compatibele Accept kopballen voor verschillende API verzoeken, gelieve te verwijzen naar hun overeenkomstige secties in de de ontwikkelaarsgids [van de Registratie van het](api/getting-started.md)Schema.

#### Accepteren van headerparameter is vereist

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Dit foutbericht wordt weergegeven wanneer een Accept-koptekst ontbreekt in een API-aanvraag. Zorg ervoor dat de koptekst Accepteren is opgenomen voordat u het opnieuw probeert.

#### Onbekende media accepteren opgegeven

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Dit foutbericht wordt weergegeven wanneer de header Accepteren ongeldig is. Controleer of u een Accept-header hebt ingevoerd die compatibel is met de API-aanvraag die u wilt uitvoeren voordat u het opnieuw probeert.

#### Onbekende indeling voor accepteren beschikbaar

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Dit foutbericht wordt weergegeven wanneer de koptekst Accepteren onjuist is opgegeven bij het opzoeken van een descriptor. Controleer of u een van de [ondersteunde koppen voor](./api/descriptors.md) Accepteren correct hebt ingevoerd voordat u het opnieuw probeert.

#### Versie moet worden opgegeven in de header Accepteren

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Dit foutbericht wordt weergegeven wanneer er geen versienummer is opgenomen in de koptekst Accepteren. Voor bepaalde elementen, zoals schema&#39;s, moet een versie worden opgegeven wanneer u afzonderlijke instanties opzoekt. Een Accept-koptekst met een versienummer ziet er ongeveer als volgt uit:

```plaintext
application/vnd.adobe.xed+json; version=1
```

Voor een lijst van gesteunde Accept kopballen, zie de [Accepteer kopbalsectie](api/getting-started.md#accept) in de de ontwikkelaarsgids van de Registratie van het Schema.

#### Versie mag niet worden opgegeven in de header Accepteren

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Als u probeert een versie op te nemen in de koptekst Accepteren bij het aanbieden van bronnen (GET), wordt deze fout weergegeven. Versies zijn alleen vereist wanneer u een opzoekaanvraag probeert uit te voeren voor één resource. Verwijder de versie uit de koptekst Accepteren om de fout op te lossen.