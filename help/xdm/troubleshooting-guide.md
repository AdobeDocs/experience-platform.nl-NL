---
keywords: Experience Platform;home;populaire onderwerpen;XDM;XDM-systeem;XDM individueel profiel;XDM ExperienceEvent;XDM ExperienceEvent;ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;ExperienceData model;Experience gegevensmodel;Experience Data Model;Data Model;Data Model;Data Model;Schema;Problemen;FAQ;Unieschema;UNION PROFILE;union profile
solution: Experience Platform
title: De gids van de het oplossen van problemen van het Systeem van de Gegevens van de Ervaring Model (XDM)
description: Dit document biedt antwoorden op veelgestelde vragen over het Systeem van de Gegevens van de Ervaring (XDM), evenals een het oplossen van problemengids voor gemeenschappelijke fouten.
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 0%

---


# [!DNL Experience Data Model] (XDM) Handleiding voor systeemprobleemoplossing

Dit document biedt antwoorden op veelgestelde vragen over [!DNL Experience Data Model] (XDM)-systeem en een gids voor probleemoplossing voor algemene fouten. Raadpleeg de [handleiding voor het oplossen van Experience Platforms](../landing/troubleshooting.md) voor vragen en het oplossen van problemen met betrekking tot andere services in Adobe Experience Platform.

**[!DNL Experience Data Model](XDM)** is een open-bronspecificatie die gestandaardiseerde schema&#39;s voor het beheer van de klantenervaring bepaalt. De methode waarop [!DNL Experience Platform] wordt gebouwd, **XDM System**, exploiteert [!DNL Experience Data Model] schema&#39;s voor gebruik door [!DNL Platform] diensten. **[!DNL Schema Registry]** verstrekt een gebruikersinterface en een RESTful API om tot **[!DNL Schema Library]** binnen [!DNL Experience Platform] toegang te hebben. Zie [XDM documentatie](home.md) voor meer informatie.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over XDM System en het gebruik van de [!DNL Schema Registry] API.

### Hoe voeg ik velden toe aan een schema?

U kunt velden aan een schema toevoegen met behulp van een mix. Elke mix is compatibel met een of meer klassen, waardoor de mix kan worden gebruikt in elk schema dat een van die compatibele klassen implementeert. Hoewel Adobe Experience Platform verschillende industriemengsels van hun eigen vooraf gedefinieerde velden voorziet, kunt u uw eigen velden aan een schema toevoegen door nieuwe combinaties te maken met behulp van de API of de gebruikersinterface.

Voor details bij het creëren van nieuwe mengen in [!DNL Schema Registry] API, zie [mixin eindpuntgids](api/mixins.md#create). Als u UI gebruikt, zie [het leerprogramma van de Redacteur van het Schema](./tutorials/create-schema-ui.md).

### Wat zijn de beste toepassingen voor mixins versus gegevenstypes?

[](./schema/composition.md#mixin) Mixins zijn componenten die een of meer velden in een schema definiëren. Mixins dwingen af hoe hun gebieden in de hiërarchie van het schema verschijnen, en tonen daarom de zelfde structuur in elk schema dat zij inbegrepen zijn. Mixins zijn alleen compatibel met specifieke klassen, zoals die door hun `meta:intendedToExtend`-kenmerk worden geïdentificeerd.

[Gegevenstypen ](./schema/composition.md#data-type) kunnen ook een of meer velden voor een schema bevatten. In tegenstelling tot mengsels, worden gegevenstypen echter niet beperkt tot een bepaalde klasse. Dit maakt gegevenstypes een flexibelere optie om gemeenschappelijke gegevensstructuren te beschrijven die over veelvoudige schema&#39;s met potentieel verschillende klassen herbruikbaar zijn.

### Wat is unieke identiteitskaart voor een schema?

Alle [!DNL Schema Registry] middelen (schema&#39;s, mengen, gegevenstypes, klassen) hebben URI die als unieke identiteitskaart voor verwijzing en raadplegingsdoeleinden dienst doet. Wanneer het bekijken van een schema in API, kan het in top-level `$id` en `meta:altId` attributen worden gevonden.

Zie de sectie [resource identification](api/getting-started.md#resource-identification) in de [!DNL Schema Registry] API developer guide voor meer informatie.

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

Open het schema in de Schema-editor en selecteer het veld in de sectie **[!UICONTROL Structuur]** van de editor dat u als identiteit wilt markeren. Selecteer onder **[!UICONTROL Veldeigenschappen]** aan de rechterkant het selectievakje **[!UICONTROL Identiteit]**.

Voor meer details over het beheren van identiteiten in UI, zie de sectie over [het bepalen van identiteitsgebieden](./tutorials/create-schema-ui.md#identity-field) in het leerprogramma van de Redacteur van het Schema.

### Heeft mijn schema een primaire identiteit nodig?

Primaire id&#39;s zijn optioneel omdat schema&#39;s er 0 of 1 kunnen hebben. Nochtans, moet een schema een primaire identiteit hebben opdat het schema voor gebruik in [!DNL Real-time Customer Profile] wordt toegelaten. Zie de sectie [identity](./tutorials/create-schema-ui.md#identity-field) van de zelfstudie van de Redacteur van het Schema voor meer informatie.

### Hoe laat ik een schema voor gebruik in [!DNL Real-time Customer Profile] toe?

De schema&#39;s worden toegelaten voor gebruik in [[!DNL Real-time Customer Profile]](../profile/home.md) door de toevoeging van een &quot;unie&quot;markering, die in `meta:immutableTags` attributen van het schema wordt gevestigd. Het toelaten van een schema voor gebruik met [!DNL Profile] kan worden gedaan gebruikend API of de gebruikersinterface.

#### Bezig met inschakelen van een bestaand schema voor [!DNL Profile] met behulp van de API

Voer een PATCH-verzoek in om het schema bij te werken en het kenmerk `meta:immutableTags` toe te voegen als een array met de waarde &quot;union&quot;. Als de update succesvol is, zal de reactie het bijgewerkte schema tonen dat nu de verenigingsmarkering bevat.

Voor meer informatie over het gebruiken van API om een schema voor gebruik in [!DNL Real-time Customer Profile] toe te laten, zie [union](./api/unions.md) document van [!DNL Schema Registry] ontwikkelaarsgids.

#### Het toelaten van een bestaand schema voor [!DNL Profile] gebruikend UI

Selecteer [!DNL Experience Platform] in de linkernavigatie **[!UICONTROL Schema&#39;s]** en selecteer de naam van het schema dat u wilt inschakelen in de lijst met schema&#39;s. Selecteer vervolgens **[!UICONTROL Profiel]** aan de rechterkant van de editor onder **[!UICONTROL Schemaeigenschappen]** om deze in of uit te schakelen.


Zie de sectie over [gebruik in Real-time Klantprofiel](./tutorials/create-schema-ui.md#profile) in de zelfstudie [!UICONTROL Schema-editor] voor meer informatie.

### Kan ik een samenvoegingsschema direct uitgeven?

Unieschema&#39;s zijn alleen-lezen en worden automatisch gegenereerd door het systeem. Ze kunnen niet rechtstreeks worden bewerkt. Unieschema&#39;s worden voor een specifieke klasse gemaakt wanneer een tag union wordt toegevoegd aan een schema dat die klasse implementeert.

Voor meer informatie over unies in XDM, zie [union](./api/unions.md) sectie in [!DNL Schema Registry] API ontwikkelaarsgids.

### Hoe moet ik mijn gegevensbestand formatteren om gegevens in mijn schema in te voeren?

[!DNL Experience Platform] Accepteert gegevensbestanden in één van beide  [!DNL Parquet] of formaat JSON. De inhoud van deze dossiers moet met het schema in overeenstemming zijn dat door de dataset van verwijzingen wordt voorzien. Zie [batchverwerking overzicht](../ingestion/home.md) voor meer informatie over de beste werkwijzen voor het opnemen van gegevensbestanden.

## Fouten en problemen oplossen

Hieronder volgt een lijst met foutberichten die kunnen optreden wanneer u werkt met de API [!DNL Schema Registry].

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

Zie de secties [container](./api/getting-started.md#container) en [resource identification](api/getting-started.md#resource-identification) in de [!DNL Schema Registry]-ontwikkelaarshandleiding voor meer informatie over het samenstellen van opzoekpaden in de API.

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

Dit foutbericht wordt weergegeven wanneer u een nieuwe mix probeert te maken met velden met een onjuiste naam. Mixins die door uw IMS-organisatie zijn gedefinieerd, moeten hun velden naamruimte geven met een `TENANT_ID` om conflicten met andere bronnen in de branche en de leverancier te voorkomen. Gedetailleerde voorbeelden van juiste gegevensstructuren voor mengsels zijn te vinden in [mixins eindpuntgids](./api/mixins.md#create).


### [!DNL Real-time Customer Profile] fouten

De volgende foutberichten zijn gekoppeld aan bewerkingen die zijn betrokken bij het inschakelen van schema&#39;s voor [!DNL Real-time Customer Profile]. Zie de [union](./api/unions.md) sectie in de [!DNL Schema Registry] API ontwikkelaarsgids voor meer informatie.

#### Om profieldatasets toe te laten zou het schema geldig moeten zijn

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Dit foutenbericht toont wanneer u probeert om een profieldataset voor een schema toe te laten dat niet voor [!DNL Real-time Customer Profile] is toegelaten. Zorg ervoor dat het schema een verenigingsmarkering bevat alvorens de dataset toe te laten.

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

Dit foutenbericht toont wanneer u probeert om een schema voor [!DNL Profile] toe te laten en één van zijn eigenschappen bevat een relatiebeschrijver zonder een beschrijver van de verwijzingsidentiteit. Voeg een beschrijver van de verwijzingsIdentiteit aan het schemagebied in kwestie toe om deze fout op te lossen.

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

Om schema&#39;s toe te laten die relatiebeschrijvers voor gebruik in [!DNL Profile] bevatten, moet namespace van het brongebied en primaire namespace van het doelgebied het zelfde zijn. Dit foutbericht wordt weergegeven wanneer u een schema wilt inschakelen dat een naamruimte zonder overeenkomst bevat voor de verwijzingsidentiteitsbeschrijving. Zorg ervoor dat de `xdm:namespace`-waarde van het identiteitsveld van het doelschema overeenkomt met die van de eigenschap `xdm:identityNamespace` in de verwijzingsidentiteitsbeschrijving van het bronveld om dit probleem op te lossen.

Zie de sectie over [standaardnaamruimten](../identity-service/namespaces.md) in het overzicht van naamruimte voor identiteiten voor een lijst met ondersteunde naamruimtecodes.

### Koptekstfouten accepteren

De meeste verzoeken van GET in [!DNL Schema Registry] API vereisen een Accept kopbal zodat het systeem bepaalt hoe te om de reactie te formatteren. Hieronder volgt een lijst met veelvoorkomende fouten die aan de koptekst Accepteren zijn gekoppeld. Voor lijsten van compatibele Accept kopballen voor verschillende API verzoeken, gelieve te verwijzen naar hun overeenkomstige secties in [de ontwikkelaarsgids van de Registratie van het Schema](api/getting-started.md).

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

Dit foutbericht wordt weergegeven wanneer de koptekst Accepteren onjuist is opgegeven bij het opzoeken van een descriptor. Zorg ervoor dat u correct een van de [ondersteunde koppen voor Accepteren voor beschrijvingen hebt ingevoerd ](./api/descriptors.md) voordat u het opnieuw probeert.

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

Voor een lijst van gesteunde Accept kopballen, zie [Accept kopbal](api/getting-started.md#accept) sectie in de [!DNL Schema Registry] ontwikkelaarsgids.

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