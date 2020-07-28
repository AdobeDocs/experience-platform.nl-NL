---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: De gids van de het oplossen van problemen van het Systeem van de Gegevens van de Ervaring Model (XDM)
topic: troubleshooting
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 0%

---


# [!DNL Experience Data Model] (XDM) Handleiding voor systeemprobleemoplossing

Dit document biedt antwoorden op veelgestelde vragen over [!DNL Experience Data Model] (XDM) System en een gids voor probleemoplossing voor algemene fouten. Voor vragen en het oplossen van problemen met betrekking tot andere diensten in Adobe Experience Platform, gelieve te verwijzen naar de het oplossen van problemengids [van het](../landing/troubleshooting.md)Experience Platform.

**[!DNL Experience Data Model](XDM)**is een open-bronspecificatie die gestandaardiseerde schema&#39;s voor het beheer van de klantenervaring bepaalt. De methodologie waarop[!DNL Experience Platform]wordt gebouwd,**Systeem **XDM, exploiteert[!DNL Experience Data Model]schema&#39;s voor gebruik door de[!DNL Platform]diensten. De **[!DNL Schema Registry]**toepassing biedt een gebruikersinterface en een RESTful-API voor toegang tot de **[!DNL Schema Library]**binnenste API[!DNL Experience Platform]. Zie de[XDM documentatie](home.md)voor meer informatie.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over XDM System en het gebruik van de [!DNL Schema Registry] API.

### Hoe voeg ik velden toe aan een schema?

U kunt velden aan een schema toevoegen met behulp van een mix. Elke mix is compatibel met een of meer klassen, waardoor de mix kan worden gebruikt in elk schema dat een van die compatibele klassen implementeert. Hoewel Adobe Experience Platform verschillende industriemengsels van hun eigen vooraf gedefinieerde velden voorziet, kunt u uw eigen velden aan een schema toevoegen door nieuwe combinaties te maken met behulp van de API of de gebruikersinterface.

Zie voor meer informatie over het maken van nieuwe combinaties in de API de handleiding voor [het maken van een mixindocument](api/create-mixin.md) in de [!DNL Schema Registry] API-ontwikkelaar. Als u UI gebruikt, zie het [leerprogramma](./tutorials/create-schema-ui.md)van de Redacteur van het Schema.

### Wat zijn de beste toepassingen voor mixins versus gegevenstypes?

[Mixins](./schema/composition.md#mixin) zijn componenten die een of meer velden in een schema definiëren. Mixins dwingen af hoe hun gebieden in de hiërarchie van het schema verschijnen, en tonen daarom de zelfde structuur in elk schema dat zij inbegrepen zijn. Mixins zijn alleen compatibel met specifieke klassen, zoals die door hun `meta:intendedToExtend` kenmerk worden geïdentificeerd.

[Gegevenstypen](./schema/composition.md#data-type) kunnen ook een of meer velden voor een schema bevatten. In tegenstelling tot mengsels, worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn.

### Wat is unieke identiteitskaart voor een schema?

Alle [!DNL Schema Registry] middelen (schema&#39;s, mixins, gegevenstypes, klassen) hebben URI die als unieke identiteitskaart voor verwijzing en raadplegingsdoeleinden dienst doet. Wanneer u een schema in de API weergeeft, vindt u dit in de kenmerken op hoofdniveau `$id` en `meta:altId` kenmerken.

Zie de sectie [Schema-identificatie](api/getting-started.md#schema-identification) in de [!DNL Schema Registry] API-ontwikkelaarsgids voor meer informatie.

### Wanneer begint een schema het breken van veranderingen te verhinderen?

De brekende veranderingen kunnen in een schema worden aangebracht zolang het nooit in de verwezenlijking van een dataset of toegelaten voor gebruik binnen is gebruikt [!DNL Real-time Customer Profile](../profile/home.md). Zodra een schema in datasetverwezenlijking of toegelaten voor gebruik met is gebruikt, worden de regels van de Evolutie [!DNL Real-time Customer Profile]van het [](schema/composition.md#evolution) Schema strikt gehandhaafd door het systeem.

### Wat is de maximumgrootte van een lang gebiedstype?

Een lang veldtype is een geheel getal met een maximale grootte van 53(+1) bits, waardoor het een mogelijk bereik heeft tussen -9007199254740992 en 9007199254740992. Dit komt door een beperking van de manier waarop JavaScript-implementaties van JSON lange gehele getallen vertegenwoordigen.

Zie de sectie [XDM-veldtypen](api/appendix.md#field-types) definiëren in de handleiding voor ontwikkelaars van de [!DNL Schema Registry] API voor meer informatie over veldtypen.

### Hoe definieer ik identiteiten voor mijn schema?

In [!DNL Experience Platform]dat geval worden identiteiten gebruikt om een onderwerp (doorgaans een individuele persoon) te identificeren, ongeacht de bronnen van gegevens die worden geïnterpreteerd. Ze worden in schema&#39;s gedefinieerd door de sleutelvelden als &quot;Identiteit&quot; te markeren. Veelgebruikte velden voor identiteiten zijn e-mailadres, telefoonnummer, CRM-id [!DNL Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/nl-NL/id-service/using/home.html)en andere unieke id-velden.

Velden kunnen als id&#39;s worden gemarkeerd met de API of de gebruikersinterface.

#### Identiteiten definiëren in de API

In de API worden identiteiten vastgesteld door identiteitsbeschrijvers te maken. Identiteitsbeschrijvers geven aan dat een bepaalde eigenschap voor een schema een unieke id is.

De beschrijvers van de identiteit worden gecreeerd door een verzoek van de POST aan het /descriptors eindpunt. Als dit lukt, ontvangt u een HTTP Status 201 (Gemaakt) en een reactieobject met de details van de nieuwe descriptor.

Zie het document over de sectie [descriptors](api/descriptors.md) in de handleiding voor [!DNL Schema Registry] ontwikkelaars voor meer informatie over het maken van identiteitsbeschrijvers in de API.

#### Identiteiten definiëren in de gebruikersinterface

Open het schema in de Schema-editor en klik in de sectie **[!UICONTROL Structuur]** van de editor op het veld dat u als identiteit wilt markeren. Klik rechts onder **[!UICONTROL Veldeigenschappen]** op het selectievakje **[!UICONTROL Identiteit]** .

Zie de sectie over het [definiëren van identiteitsvelden](./tutorials/create-schema-ui.md#identity-field) in de zelfstudie van de Schema-editor voor meer informatie over het beheren van identiteiten in de gebruikersinterface.

### Heeft mijn schema een primaire identiteit nodig?

Primaire id&#39;s zijn optioneel omdat schema&#39;s er 0 of 1 kunnen hebben. Nochtans, moet een schema een primaire identiteit hebben opdat het schema voor gebruik binnen wordt toegelaten [!DNL Real-time Customer Profile]. Zie de [identiteitssectie](./tutorials/create-schema-ui.md#identity-field) van het leerprogramma van de Redacteur van het Schema voor meer informatie.

### Hoe laat ik een schema voor gebruik binnen toe [!DNL Real-time Customer Profile]?

De schema&#39;s worden toegelaten voor gebruik binnen [!DNL Real-time Customer Profile](../profile/home.md) door de toevoeging van een &quot;unie&quot;markering, die in de `meta:immutableTags` attributen van het schema wordt gevestigd. Het toelaten van een schema voor gebruik met [!DNL Profile] kan worden gedaan gebruikend API of de gebruikersinterface.

#### Een bestaand schema inschakelen voor het [!DNL Profile] gebruik van de API

Voer een PATCH-verzoek in om het schema bij te werken en het `meta:immutableTags` kenmerk toe te voegen als een array met de waarde &quot;union&quot;. Als de update succesvol is, zal de reactie het bijgewerkte schema tonen dat nu de verenigingsmarkering bevat.

Zie het document [!DNL Real-time Customer Profile]union [](./api/unions.md) [!DNL Schema Registry] in de handleiding voor ontwikkelaars voor meer informatie over het gebruik van de API om een schema voor gebruik in te schakelen.

#### Het toelaten van een bestaand schema voor het [!DNL Profile] gebruiken van UI

Klik in [!DNL Experience Platform]de linkernavigatie op **[!UICONTROL Schema&#39;s]** en selecteer de naam van het schema dat u wilt inschakelen in de lijst met schema&#39;s. Klik vervolgens rechts van de editor onder **[!UICONTROL Schemaeigenschappen]** op **[!UICONTROL Profiel]** om deze in of uit te schakelen.


Voor meer informatie, zie de sectie over [gebruik in het Profiel](./tutorials/create-schema-ui.md#profile) van de Klant in real time in de [!UICONTROL Redacteur] van het Schema.

### Kan ik een samenvoegingsschema direct uitgeven?

Unieschema&#39;s zijn alleen-lezen en worden automatisch gegenereerd door het systeem. Ze kunnen niet rechtstreeks worden bewerkt. Unieschema&#39;s worden voor een specifieke klasse gemaakt wanneer een tag union wordt toegevoegd aan een schema dat die klasse implementeert.

Zie de sectie [union](./api/unions.md) [!DNL Schema Registry] in de API developer guide voor meer informatie over samenvoegingen in XDM.

### Hoe moet ik mijn gegevensbestand formatteren om gegevens in mijn schema in te voeren?

[!DNL Experience Platform] Accepteert gegevensbestanden in één van beide [!DNL Parquet] of formaat JSON. De inhoud van deze dossiers moet met het schema in overeenstemming zijn dat door de dataset van verwijzingen wordt voorzien. Voor details over beste praktijken voor gegevensuitwisseling, zie het [batch ingesinsectieoverzicht](../ingestion/home.md).

## Fouten en problemen oplossen

Hieronder volgt een lijst met foutberichten die kunnen optreden wanneer u met de [!DNL Schema Registry] API werkt.

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

Zie de secties over [container](./api/getting-started.md#container) - en [schemaidentificatie](api/getting-started.md#schema-identification) in de handleiding voor [!DNL Schema Registry] ontwikkelaars voor meer informatie over het samenstellen van opzoekpaden in de API.

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

Dit foutbericht wordt weergegeven wanneer u een nieuwe mix probeert te maken met velden met een onjuiste naam. Mixins die door uw IMS-organisatie zijn gedefinieerd, moeten hun velden naamruimte geven met een naamruimte `TENANT_ID` om conflicten met andere bronnen in de branche en de leverancier te voorkomen. Gedetailleerde voorbeelden van juiste gegevensstructuren voor mixins vindt u in het document over het [maken van een mixinsectie](api/create-mixin.md) in de [!DNL Schema Registry] API-ontwikkelaarsgids.


### [!DNL Real-time Customer Profile] fouten

De volgende foutberichten zijn gekoppeld aan bewerkingen die zijn betrokken bij het inschakelen van schema&#39;s voor [!DNL Real-time Customer Profile]. Zie de sectie [union](./api/unions.md) in de [!DNL Schema Registry] API-ontwikkelaarsgids voor meer informatie.

#### Om profieldatasets toe te laten zou het schema geldig moeten zijn

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Dit foutenbericht toont wanneer u probeert om een profieldataset voor een schema toe te laten dat niet voor is toegelaten [!DNL Real-time Customer Profile]. Zorg ervoor dat het schema een verenigingsmarkering bevat alvorens de dataset toe te laten.

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

Dit foutbericht wordt weergegeven wanneer u probeert een schema in te schakelen voor [!DNL Profile] en een van de eigenschappen ervan een relatiebeschrijving bevat zonder een referentie-id-descriptor. Voeg een beschrijver van de verwijzingsIdentiteit aan het schemagebied in kwestie toe om deze fout op te lossen.

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

Om schema&#39;s toe te laten die relatiebeschrijvers voor gebruik binnen bevatten [!DNL Profile], moet namespace van het brongebied en primaire namespace van het doelgebied het zelfde zijn. Dit foutbericht wordt weergegeven wanneer u een schema wilt inschakelen dat een naamruimte zonder overeenkomst bevat voor de verwijzingsidentiteitsbeschrijving. Zorg ervoor dat de `xdm:namespace` waarde van het de identiteitsgebied van het bestemmingsschema dat van het `xdm:identityNamespace` bezit in de beschrijver van de verwijzingsidentiteit van het brongebied aanpast om deze kwestie op te lossen.

Zie de sectie over [standaardnaamruimten](../identity-service/namespaces.md) in het overzicht van naamruimte voor identiteiten voor een lijst met ondersteunde naamruimtecodes.

### Koptekstfouten accepteren

De meeste GET-aanvragen in de [!DNL Schema Registry] API vereisen een header Accepteren, zodat het systeem kan bepalen hoe de reactie moet worden opgemaakt. Hieronder volgt een lijst met veelvoorkomende fouten die aan de koptekst Accepteren zijn gekoppeld. Voor lijsten van compatibele Accept kopballen voor verschillende API verzoeken, gelieve te verwijzen naar hun overeenkomstige secties in de de ontwikkelaarsgids [van de Registratie van het](api/getting-started.md)Schema.

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

Zie de koptekstsectie [Accepteren](api/getting-started.md#accept) in de handleiding voor [!DNL Schema Registry] ontwikkelaars voor een lijst met ondersteunde koppen.

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

Als u probeert een versie op te nemen in de koptekst Accepteren bij het weergeven van bronnen (GET), wordt deze fout weergegeven. Versies zijn alleen vereist wanneer u een opzoekaanvraag probeert uit te voeren voor één resource. Verwijder de versie uit de koptekst Accepteren om de fout op te lossen.