---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Schema Register;Schema Register;Descriptor;Descriptor;Descriptors;Identiteit;Vriendelijke naam;Alternatieve naam;AlternateDisplayInfo;Referentie;relatie;Relatie
solution: Experience Platform
title: Descriptors API-eindpunt
description: Het /descriptors eindpunt in de Registratie API van het Schema staat u toe om XDM beschrijvers binnen uw ervaringstoepassing programmatically te beheren.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '2882'
ht-degree: 0%

---

# Het eindpunt van descriptors

De schema&#39;s bepalen de structuur van gegevensentiteiten maar specificeren niet hoe om het even welke datasets die van deze schema&#39;s worden gecreeerd op elkaar betrekking hebben. In Adobe Experience Platform kunt u beschrijvingen gebruiken om deze relaties te beschrijven en interpreterende metagegevens aan een schema toe te voegen.

Descriptors zijn metagegevensobjecten op huurniveau die op schema&#39;s in Adobe Experience Platform zijn toegepast. Ze definiëren structurele relaties, sleutels en gedragsvelden (zoals tijdstempels of versioning) die van invloed zijn op de manier waarop gegevens worden gevalideerd, samengevoegd of downstream worden geïnterpreteerd.

Een schema kan een of meer beschrijvingen bevatten. Elke descriptor definieert een `@type` en de `sourceSchema` waarop deze van toepassing is. De beschrijver is automatisch op alle datasets van dat schema van toepassing.

In Adobe Experience Platform is een descriptor metagegevens die gedragsregels of structurele betekenis toevoegen aan een schema.
Er zijn verschillende typen descriptors, waaronder:

- [&#x200B; de beschrijver van de Identiteit &#x200B;](#identity-descriptor) - merkt een gebied als identiteit
- [&#x200B; Primaire zeer belangrijke beschrijver &#x200B;](#primary-key-descriptor) - dwingt uniciteit af
- [&#x200B; de beschrijver van de Verhouding &#x200B;](#relationship-descriptor) - bepaalt een buitenlands-zeer belangrijk toetreden
- [&#x200B; Alternatieve de beschrijver van vertoningsinfo &#x200B;](#friendly-name) - laat u een gebied in UI anders noemen
- [&#x200B; Versie &#x200B;](#version-descriptor) en [&#x200B; timestamp &#x200B;](#timestamp-descriptor) beschrijvers - spoorgebeurtenis die en veranderingsopsporing opdracht geven

Met het eindpunt `/descriptors` in de [!DNL Schema Registry] API kunt u beschrijvingen programmatisch beheren binnen uw ervaringstoepassing.

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Schema Registry]  API &#x200B;](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke Experience Platform API met succes te maken.

Naast standaardbeschrijvers, steunt [!DNL Schema Registry] beschrijvingstypes voor relationele schema&#39;s, zoals **primaire sleutel**, **versie** en **timestamp**. Deze dwingen eenheid af, controleren versioning, en bepalen tijd-reeksen gebieden op het schemaniveau. Als u niet vertrouwd met relationele schema&#39;s bent, herzie het [&#x200B; overzicht van Data Mirror &#x200B;](../data-mirror/overview.md) en [&#x200B; relationele schema&#39;s technische verwijzing &#x200B;](../schema/relational.md) alvorens verder te gaan.

>[!IMPORTANT]
>
>Zie [&#x200B; Bijlage &#x200B;](#defining-descriptors) voor details op alle beschrijvingstypes.

## Een lijst met descriptoren ophalen {#list}

U kunt alle beschrijvingen weergeven die door uw organisatie zijn gedefinieerd door een GET-aanvraag in te dienen bij `/tenant/descriptors` .

**API formaat**

```http
GET /tenant/descriptors
```

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Het eindpunt `/descriptors` gebruikt `Accept` headers die verschillen van alle andere eindpunten in de API [!DNL Schema Registry] .

>[!IMPORTANT]
>
>Descriptors vereisen unieke `Accept` headers die `xed` vervangen door `xdm` en bieden ook een `link` -optie die uniek is voor beschrijvingen. De juiste `Accept` headers zijn opgenomen in de onderstaande voorbeelden, maar Wees voorzichtig om te zorgen dat de juiste kopteksten worden gebruikt wanneer u met beschrijvingen werkt.

| `Accept` header | Beschrijving |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Hiermee wordt een array met beschrijvings-id&#39;s geretourneerd |
| `application/vnd.adobe.xdm-link+json` | Hiermee wordt een array van beschrijvende API-paden geretourneerd |
| `application/vnd.adobe.xdm+json` | Hiermee wordt een array van uitgebreide beschrijvingsobjecten geretourneerd |
| `application/vnd.adobe.xdm-v2+json` | Deze `Accept` header moet worden gebruikt om pagineringsmogelijkheden te gebruiken. |

{style="table-layout:auto"}

**Reactie**

Het antwoord bevat een array voor elk beschrijvende type waarvoor beschrijvingen zijn gedefinieerd. Met andere woorden, als er geen beschrijvers van een bepaalde `@type` gedefinieerd zijn, retourneert het register geen lege array voor dat beschrijvende type.

Wanneer u de header `link` `Accept` gebruikt, wordt elke descriptor weergegeven als een arrayitem in de notatie `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## Een descriptor opzoeken {#lookup}

Als u de details van een specifieke descriptor wilt bekijken, verzendt u een GET-aanvraag met behulp van de `@id` .

**API formaat**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De `@id` van de descriptor die u wilt opzoeken. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een descriptor opgehaald op basis van de waarde `@id` . Er is geen versiebeheer toegepast op descriptors. Daarom is geen `Accept` header vereist in het opzoekverzoek.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert de details van de descriptor, inclusief de `@type` en `sourceSchema` , plus aanvullende informatie die afhankelijk is van het type descriptor. De geretourneerde `@id` moet overeenkomen met de beschrijving `@id` in de aanvraag.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Een descriptor maken {#create}

U kunt een nieuwe descriptor maken door een POST-aanvraag in te dienen bij het eindpunt van `/tenant/descriptors` .

>[!IMPORTANT]
>
>Met [!DNL Schema Registry] kunt u verschillende beschrijvende typen definiëren. Elk beschrijvingstype vereist dat zijn eigen specifieke gebieden in het aanvraaglichaam worden verzonden. Zie [&#x200B; bijlage &#x200B;](#defining-descriptors) voor een volledige lijst van beschrijvers en de gebieden noodzakelijk om hen te bepalen.

**API formaat**

```http
POST /tenant/descriptors
```

**Verzoek**

In het volgende verzoek wordt een identiteitsbeschrijving gedefinieerd in een veld &quot;E-mailadres&quot; in een voorbeeldschema. Dit vertelt [!DNL Experience Platform] om het e-mailadres als herkenningsteken te gebruiken helpen informatie over het individu samenvoegen.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de details van de nieuwe descriptor, inclusief de `@id` ervan. `@id` is een alleen-lezen veld dat door [!DNL Schema Registry] is toegewezen en dat wordt gebruikt voor het verwijzen naar de descriptor in de API.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Een descriptor bijwerken {#put}

U kunt een descriptor bijwerken door de `@id` ervan op te nemen in het pad van een PUT-aanvraag.

**API formaat**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De `@id` van de descriptor die u wilt bijwerken. |

{style="table-layout:auto"}

**Verzoek**

Met dit verzoek wordt in feite de descriptor herschreven, zodat de aanvraaginstantie alle velden moet bevatten die vereist zijn voor het definiëren van een descriptor van dat type. Met andere woorden, is de verzoeklading om (PUT) een beschrijver bij te werken het zelfde als de nuttige lading aan [&#x200B; creeert (POST) een beschrijver &#x200B;](#create) van het zelfde type.

>[!IMPORTANT]
>
>Net als bij het maken van beschrijvingen met POST-aanvragen, vereist elk descriptortype dat de eigen specifieke velden worden verzonden in PUT-aanvraagladingen. Zie [&#x200B; bijlage &#x200B;](#defining-descriptors) voor een volledige lijst van beschrijvers en de gebieden noodzakelijk om hen te bepalen.

In het volgende voorbeeld wordt een identiteitsdescriptor bijgewerkt om naar een andere `xdm:sourceProperty` (`mobile phone` ) te verwijzen en wordt de waarde `xdm:namespace` in `Phone` gewijzigd.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de `@id` van de bijgewerkte descriptor (die moet overeenkomen met de `@id` die in de aanvraag is verzonden).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Het uitvoeren van het verzoek van de a [&#x200B; raadpleging (GET) &#x200B;](#lookup) om de beschrijver te bekijken toont aan dat de gebieden nu zijn bijgewerkt om op de veranderingen te wijzen die in het verzoek van PUT worden verzonden.

## Een descriptor verwijderen {#delete}

Soms moet u een descriptor verwijderen die u in de [!DNL Schema Registry] hebt gedefinieerd. Hiervoor doet u een DELETE-aanvraag die verwijst naar `@id` van de descriptor die u wilt verwijderen.

**API formaat**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De `@id` van de descriptor die u wilt verwijderen. |

{style="table-layout:auto"}

**Verzoek**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

Om de beschrijver te bevestigen is geschrapt, kunt u a [&#x200B; raadplegingsverzoek &#x200B;](#lookup) tegen de beschrijver `@id` uitvoeren. De reactie retourneert HTTP-status 404 (Niet gevonden) omdat de descriptor is verwijderd uit de [!DNL Schema Registry] .

## Bijlage {#appendix}

In de volgende sectie vindt u aanvullende informatie over het werken met descriptoren in de API van [!DNL Schema Registry] .

### descriptoren definiëren {#defining-descriptors}

>[!NOTE]
>
>Het maximumaantal descriptors dat op de sandbox van een organisatie kan worden toegepast, is 4000.

In de volgende secties vindt u een overzicht van de beschikbare descriptortypen, inclusief de vereiste velden voor het definiëren van een descriptor voor elk type.

>[!IMPORTANT]
>
>U kunt het naamruimteobject voor huurders niet labelen, omdat het systeem dat label zou toepassen op elk aangepast veld in die sandbox. In plaats daarvan, moet u de bladknoop onder dat voorwerp specificeren die u moet etiketteren.

#### Identiteitsbeschrijving {#identity-descriptor}

Een identiteitsbeschrijver signaleert dat &quot;[!UICONTROL sourceProperty]&quot;van &quot;[!UICONTROL sourceSchema]&quot;een [!DNL Identity] gebied is zoals die door [&#x200B; wordt beschreven de Dienst van de Identiteit van Experience Platform &#x200B;](../../identity-service/home.md).

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor een identiteitsdescriptor moet deze waarde worden ingesteld op `xdm:descriptorIdentity` . |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Het pad naar de specifieke eigenschap die de identiteit zal zijn. Het pad moet beginnen met een &quot;/&quot; en niet eindigen met een pad. Plaats geen &quot;eigenschappen&quot; in het pad (gebruik bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;) |
| `xdm:namespace` | De `id` - of `code` -waarde van de naamruimte identity. Een lijst van namespaces kan worden gevonden gebruikend [[!DNL Identity Service API] &#x200B;](https://developer.adobe.com/experience-platform-apis/references/identity-service). |
| `xdm:property` | Ofwel `xdm:id` of `xdm:code` , afhankelijk van de gebruikte `xdm:namespace` . |
| `xdm:isPrimary` | Een optionele booleaanse waarde. Indien waar (true), wordt het veld als de primaire identiteit aangegeven. Schema&#39;s mogen slechts één primaire identiteit bevatten. |

{style="table-layout:auto"}

#### Beschrijvende naam {#friendly-name}

Met beschrijvingen van vriendschappelijke namen kan een gebruiker de waarden `title` , `description` en `meta:enum` van de kernvelden van het bibliotheekschema wijzigen. Dit is vooral handig wanneer u werkt met &quot;eVars&quot; en andere &quot;generieke&quot; velden die u wilt labelen voor informatie die specifiek is voor uw organisatie. De gebruikersinterface kan deze gebruiken om een vriendelijkere naam weer te geven of om alleen velden weer te geven die een vriendelijke naam hebben.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor een beschrijvende naam moet deze waarde worden ingesteld op `xdm:alternateDisplayInfo` . |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Het pad naar de specifieke eigenschap waarvan u de details wilt wijzigen. Het pad moet beginnen met een schuine streep (`/`) en niet eindigen met een schuine streep. Neem `properties` niet op in het pad (gebruik bijvoorbeeld `/personalEmail/address` in plaats van `/properties/personalEmail/properties/address` ). |
| `xdm:title` | De nieuwe titel die u voor dit gebied wilt tonen, die in het Geval van de Titel wordt geschreven. |
| `xdm:description` | Een optionele beschrijving kan samen met de titel worden toegevoegd. |
| `meta:enum` | Als het veld dat wordt aangegeven door `xdm:sourceProperty` een tekenreeksveld is, kan `meta:enum` worden gebruikt om voorgestelde waarden toe te voegen voor het veld in de segmenteringsinterface. Het is belangrijk om op te merken dat `meta:enum` geen opsomming verklaart of om het even welke gegevensbevestiging voor het gebied XDM verstrekt.<br><br> dit zou slechts voor kernXDM gebieden moeten worden gebruikt die door Adobe worden bepaald. Als de broneigenschap een aangepast veld is dat door uw organisatie is gedefinieerd, moet u in plaats daarvan de eigenschap `meta:enum` van het veld rechtstreeks via een PATCH-aanvraag naar de bovenliggende bron van het veld bewerken. |
| `meta:excludeMetaEnum` | Als het veld dat wordt aangegeven door `xdm:sourceProperty` een tekenreeksveld is met bestaande voorgestelde waarden onder een `meta:enum` -veld, kunt u dit object opnemen in een beschrijvingsbestand voor een vriendelijke naam om sommige of al deze waarden uit te sluiten van segmentatie. De sleutel en waarde voor elke vermelding moeten overeenkomen met die in het oorspronkelijke `meta:enum` veld om de vermelding uit te sluiten. |

{style="table-layout:auto"}

#### Relatiebeschrijving {#relationship-descriptor}

Relationship-descriptors beschrijven een relatie tussen twee verschillende schema&#39;s, die u hebt afgesloten op de eigenschappen die worden beschreven in `xdm:sourceProperty` en `xdm:destinationProperty` . Zie het leerprogramma op [&#x200B; bepalend een verband tussen twee schema&#39;s &#x200B;](../tutorials/relationship-api.md) voor meer informatie.

Gebruik deze eigenschappen om te verklaren hoe een brongebied (buitenlandse sleutel) op een bestemmingsgebied ([&#x200B; primaire sleutel &#x200B;](#primary-key-descriptor) of kandidaat sleutel) betrekking heeft.

>[!TIP]
>
>A **buitenlandse sleutel** is een gebied in het bronschema (dat door `xdm:sourceProperty` wordt bepaald) dat verwijzingen een zeer belangrijk gebied in een ander schema. A **kandidaat sleutel** is om het even welk gebied (of reeks gebieden) in het bestemmingsschema dat uniek een verslag identificeert en in plaats van de primaire sleutel kan worden gebruikt.

De API ondersteunt twee patronen:

- `xdm:descriptorOneToOne`: standaard 1 :1 verhouding.
- `xdm:descriptorRelationship`: algemeen patroon voor nieuwe werk en relationele schema&#39;s (steunt kardinaliteit, het noemen, en niet-primaire zeer belangrijke doelstellingen).

##### Eén-op-één relatie (standaardschema&#39;s)

Gebruik dit wanneer het handhaven van bestaande standaard-schema-integraties die reeds op `xdm:descriptorOneToOne` steunen.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

In de volgende tabel worden de velden beschreven die nodig zijn om een één-op-één relatiebeschrijving te definiëren.

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor een relatiebeschrijver, moet deze waarde aan `xdm:descriptorOneToOne` worden geplaatst, tenzij u toegang tot Real-Time CDP B2B edition hebt. Met B2B edition kunt u `xdm:descriptorOneToOne` of [`xdm:descriptorRelationship`](#b2b-relationship-descriptor) gebruiken. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Pad naar het veld in het bronschema waar de relatie wordt gedefinieerd. Moet beginnen met een &quot;/&quot; en niet eindigen met &quot;/&quot;. Plaats geen &quot;eigenschappen&quot; in het pad (bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | De `$id` URI van het verwijzingsschema deze beschrijver bepaalt een verhouding met. |
| `xdm:destinationVersion` | De belangrijkste versie van het referentieschema. |
| `xdm:destinationProperty` | (Optioneel) Pad naar een doelveld binnen het referentieschema. Als deze eigenschap wordt weggelaten, wordt het doelveld afgeleid van velden die een overeenkomende ID-descriptor bevatten (zie hieronder). |

##### Algemene relatie (relationele schema&#39;s en aanbevolen voor nieuwe projecten)

Gebruik deze descriptor voor alle nieuwe implementaties en voor relationele schema&#39;s. Het staat u toe om de kardinaliteit van de verhouding (zoals één-aan-één of vele-aan-één) te bepalen, relatienamen te specificeren, en verbinding aan een bestemmingsgebied te verbinden dat niet de primaire sleutel (niet-primaire sleutel) is.

In de volgende voorbeelden ziet u hoe u een algemene relatiebeschrijving definieert.

**Minimaal voorbeeld:**

Dit minimale voorbeeld omvat slechts de vereiste gebieden om een vele-aan-één verhouding tussen twee schema&#39;s te bepalen.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceProperty": "/customer_ref",
  "xdm:sourceVersion": 1,
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:cardinality": "M:1"
}
```

**Voorbeeld met alle facultatieve gebieden:**

Dit voorbeeld bevat alle optionele velden, zoals relatienamen, weergavettels en een expliciet doelveld voor een niet-primaire sleutel.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/customer_ref",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationProperty": "/customer_id",
  "xdm:sourceToDestinationName": "CampaignToCustomer",
  "xdm:destinationToSourceName": "CustomerToCampaign",
  "xdm:sourceToDestinationTitle": "Customer campaigns",
  "xdm:destinationToSourceTitle": "Campaign customers",
  "xdm:cardinality": "M:1"
}
```

##### Een relatiebeschrijving kiezen

Gebruik de volgende richtlijnen om te beslissen welke relatiebeschrijving u wilt toepassen:

| Situatie | Te gebruiken beschrijver |
| --------------------------------------------------------------------- | ----------------------------------------- |
| Nieuwe werk- of relationele schema&#39;s | `xdm:descriptorRelationship` |
| Bestaande 1 :1 afbeelding in standaardschema&#39;s | Ga verder met `xdm:descriptorOneToOne` tenzij u functies nodig hebt die alleen door `xdm:descriptorRelationship` worden ondersteund. |
| Veelvoudige of optionele kardinaliteit vereist (`1:1`, `1:0`, `M:1`, `M:0`) | `xdm:descriptorRelationship` |
| Namen of titels voor gebruikersinterface/downstreamleesbaarheid vereisen | `xdm:descriptorRelationship` |
| Hebt u een doeldoel nodig dat geen identiteit is | `xdm:descriptorRelationship` |

>[!NOTE]
>
>Voor bestaande `xdm:descriptorOneToOne` -descriptors in standaardschema&#39;s blijven deze gebruiken, tenzij u functies nodig hebt zoals niet-primaire doeldoelen voor identiteitsdoeleinden, aangepaste naamgeving of uitgebreide standaardopties.

##### Capaciteitsvergelijking

In de volgende tabel worden de mogelijkheden van de twee descriptortypen vergeleken:

| Capaciteit | `xdm:descriptorOneToOne` | `xdm:descriptorRelationship` |
| ------------------ | ------------------------ | ------------------------------------------------------------------------ |
| Kardinaal | 1:1 | 1 :1, 1 :0, M :1, M :0 (informatief) |
| Doelstelling | Identiteit/expliciet veld | De primaire sleutel door gebrek, of niet-primaire sleutel via `xdm:destinationProperty` |
| Namen van velden | Niet ondersteund | `xdm:sourceToDestinationName` , `xdm:destinationToSourceName` en titels |
| Relationeel passend | Beperkt | Primair patroon voor relationele schema&#39;s |

##### Beperkingen en validatie

Volg deze vereisten en aanbevelingen wanneer het bepalen van een algemene relatiebeschrijver:

- Voor relationele schema&#39;s, plaats het brongebied (buitenlandse sleutel) op het wortelniveau. Dit is een huidige technische beperking voor inname, niet alleen een aanbeveling van best practices.
- Zorg ervoor dat de gegevenstypen van bron- en doelvelden compatibel zijn (numeriek, datum, Boolean, tekenreeks).
- Vergeet niet dat de kardinaliteit informatie is; opslag dwingt deze niet af. Geef een standaardindeling op in de notatie `<source>:<destination>` . Accepteerde waarden zijn: `1:1`, `1:0`, `M:1` of `M:0` .

#### Descriptor primaire sleutel {#primary-key-descriptor}

De primaire zeer belangrijke beschrijver (`xdm:descriptorPrimaryKey`) dwingt uniciteit en niet-krachtbeperkingen op één of meerdere gebieden in een schema af.

```json
{
  "@type": "xdm:descriptorPrimaryKey",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": ["/orderId", "/orderLineId"]
}
```

| Eigenschap | Beschrijving |
| -------------------- | ----------------------------------------------------------------------------- |
| `@type` | Moet `xdm:descriptorPrimaryKey` zijn. |
| `xdm:sourceSchema` | `$id` URI van het schema. |
| `xdm:sourceProperty` | JSON-aanwijzer(s) naar het veld of de velden met de primaire sleutel. Gebruik een array voor samengestelde sleutels. Voor tijdreeksschema&#39;s moet de samengestelde sleutel het tijdstempelveld bevatten om ervoor te zorgen dat de records uniek zijn. |

#### Versiebeschrijving {#version-descriptor}

>[!NOTE]
>
>In de Redacteur van het Schema UI, verschijnt de versiedescriptor als &quot;[!UICONTROL Version identifier]&quot;.

De versiedescriptor (`xdm:descriptorVersion`) wijst een gebied aan om conflicten van uit-van-orde veranderingsgebeurtenissen te ontdekken en te verhinderen.

```json
{
  "@type": "xdm:descriptorVersion",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/versionNumber"
}
```

| Eigenschap | Beschrijving |
| -------------------- | ------------------------------------------------------------- |
| `@type` | Moet `xdm:descriptorVersion` zijn. |
| `xdm:sourceSchema` | `$id` URI van het schema. |
| `xdm:sourceProperty` | JSON-aanwijzer naar het versieveld. Moet worden gemarkeerd met `required` . |

#### Tijdstempelbeschrijving {#timestamp-descriptor}

>[!NOTE]
>
>In de Redacteur van het Schema UI, verschijnt de timestamp beschrijver als &quot;[!UICONTROL Timestamp identifier]&quot;.

In de tijdstempeldescriptor (`xdm:descriptorTimestamp`) wordt een datum-tijdveld aangewezen als tijdstempel voor schema&#39;s met `"meta:behaviorType": "time-series"` .

```json
{
  "@type": "xdm:descriptorTimestamp",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/eventTime"
}
```

| Eigenschap | Beschrijving |
| -------------------- | ------------------------------------------------------------------------------------------ |
| `@type` | Moet `xdm:descriptorTimestamp` zijn. |
| `xdm:sourceSchema` | `$id` URI van het schema. |
| `xdm:sourceProperty` | JSON-aanwijzer naar het tijdstempelveld. Moet zijn gemarkeerd met `required` en van het type `date-time` zijn. |

##### B2B-relatiebeschrijving {#B2B-relationship-descriptor}

De Real-Time CDP B2B edition introduceert een alternatieve manier om relaties tussen schema&#39;s te definiëren, die vele-op-één relaties mogelijk maakt. Deze nieuwe relatie moet het `@type: xdm:descriptorRelationship` type hebben en de lading moet meer gebieden dan de `@type: xdm:descriptorOneToOne` verhouding omvatten. Zie het leerprogramma op [&#x200B; bepalend een schemaverhouding voor B2B edition &#x200B;](../tutorials/relationship-b2b.md) voor meer informatie.

```json
{
   "@type": "xdm:descriptorRelationship",
   "xdm:sourceSchema" : "https://ns.adobe.com/{TENANT_ID}/schemas/9f2b2f225ac642570a110d8fd70800ac0c0573d52974fa9a",
   "xdm:sourceVersion" : 1,
   "xdm:sourceProperty" : "/person-ref",
   "xdm:destinationSchema" : "https://ns.adobe.com/{TENANT_ID/schemas/628427680e6b09f1f5a8f63ba302ee5ce12afba8de31acd7",
   "xdm:destinationVersion" : 1,
   "xdm:destinationProperty": "/personId",
   "xdm:destinationNamespace" : "People", 
   "xdm:destinationToSourceTitle" : "Opportunity Roles",
   "xdm:sourceToDestinationTitle" : "People",
   "xdm:cardinality": "M:1"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor gebruik met de volgende velden moet de waarde worden ingesteld op `xdm:descriptorRelationship` . Voor informatie over extra types, zie de [&#x200B; sectie van de relatiebeschrijvers &#x200B;](#relationship-descriptor). |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Pad naar het veld in het bronschema waar de relatie wordt gedefinieerd. Moet beginnen met een &quot;/&quot; en niet eindigen met &quot;/&quot;. Plaats geen &quot;eigenschappen&quot; in het pad (bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | De `$id` URI van het verwijzingsschema deze beschrijver bepaalt een verhouding met. |
| `xdm:destinationVersion` | De belangrijkste versie van het referentieschema. |
| `xdm:destinationProperty` | (Optioneel) Pad naar een doelveld binnen het referentieschema. Dit moet aan primaire identiteitskaart van het schema, of aan een ander gebied met een compatibel gegevenstype aan `xdm:sourceProperty` oplossen. Indien weggelaten, werkt de relatie mogelijk niet zoals verwacht. |
| `xdm:destinationNamespace` | De naamruimte van de primaire id vanuit het referentieschema. |
| `xdm:destinationToSourceTitle` | De vertoningsnaam van de verhouding van het verwijzingsschema aan het bronschema. |
| `xdm:sourceToDestinationTitle` | De vertoningsnaam van de verhouding van het bronschema aan het verwijzingsschema. |
| `xdm:cardinality` | De samengevoegde relatie tussen de schema&#39;s. Deze waarde moet worden ingesteld op `M:1` . Hierbij wordt verwezen naar een vele-op-één relatie. |

{style="table-layout:auto"}

#### Referentie-identiteitsdescriptor

De identiteitsbeschrijvers van de verwijzing verstrekken een verwijzingscontext aan de primaire identiteit van een schemagebied, toelatend het om door gebieden in andere schema&#39;s worden van verwijzingen voorzien. In het referentieschema moet al een primair identiteitsveld zijn gedefinieerd voordat naar het kan worden verwezen door andere schema&#39;s via dit beschrijvingsbestand.

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor een identiteitsbeschrijving van een referentie moet deze waarde worden ingesteld op `xdm:descriptorReferenceIdentity` . |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Pad naar het veld in het bronschema dat wordt gebruikt om naar het referentieschema te verwijzen. Moet beginnen met een &quot;/&quot; en niet eindigen met een &quot;/&quot;. Plaats geen &quot;eigenschappen&quot; in het pad (bijvoorbeeld `/personalEmail/address` in plaats van `/properties/personalEmail/properties/address` ). |
| `xdm:identityNamespace` | De naamruimtecode van de identiteit voor de eigenschap source. |

{style="table-layout:auto"}

#### Vervangen velddescriptor

U kunt [&#x200B; een gebied binnen een douaneXDM middel &#x200B;](../tutorials/field-deprecation-api.md#custom) verwerpen door a `meta:status` attributen toe te voegen die aan `deprecated` aan het betrokken gebied worden geplaatst. Als u velden die worden verschaft door standaard XDM-bronnen in uw schema&#39;s wilt vervangen, kunt u echter een vervangen velddescriptor toewijzen aan het desbetreffende schema om hetzelfde effect te bereiken. Gebruikend [&#x200B; correcte `Accept` kopbal &#x200B;](../tutorials/field-deprecation-api.md#verify-deprecation), kunt u dan bekijken welke standaardgebieden voor een schema verouderd zijn wanneer het omhoog kijken in API.

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor. Voor een beschrijving van de gebiedsafbeelding moet deze waarde worden ingesteld op `xdm:descriptorDeprecated` . |
| `xdm:sourceSchema` | De URI `$id` van het schema waarop u de descriptor toepast. |
| `xdm:sourceVersion` | De versie van het schema waarop u de descriptor toepast. Moet worden ingesteld op `1` . |
| `xdm:sourceProperty` | Het pad naar de eigenschap in het schema waarop u de descriptor toepast. Als u de descriptor op meerdere eigenschappen wilt toepassen, kunt u een lijst met paden opgeven in de vorm van een array (bijvoorbeeld `["/firstName", "/lastName"]` ). |

{style="table-layout:auto"}
