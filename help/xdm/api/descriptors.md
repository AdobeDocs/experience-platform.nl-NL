---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Schema Register;Schema Register;Descriptor;Descriptors;Descriptors;Identiteit;Vriendelijke naam;Alternatieve naam;AlternateInfo;Referentie;Referentie;Relatie;Relatie
solution: Experience Platform
title: Descriptors API-eindpunt
description: Het /descriptors eindpunt in de Registratie API van het Schema staat u toe om XDM beschrijvers binnen uw ervaringstoepassing programmatically te beheren.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 44355aa2ddf03b20aca64c6675414b73682bc2b5
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 0%

---

# Het eindpunt van descriptors

De schema&#39;s bepalen een statische mening van gegevensentiteiten, maar verstrekken geen specifieke details over hoe gegevens die op deze regelingen (datasets, bijvoorbeeld) worden gebaseerd op elkaar kunnen betrekking hebben. Met Adobe Experience Platform kunt u deze relaties en andere interpreterende metagegevens over een schema beschrijven aan de hand van beschrijvingen.

De beschrijvers van het schema zijn huurdersvlakke meta-gegevens, betekenend zij aan uw organisatie uniek zijn en alle beschrijvingsverrichtingen vinden in de huurderscontainer plaats.

Op elk schema kunnen een of meer schemabeschrijvingsentiteiten zijn toegepast. Elke schemadescriptorentiteit bevat een descriptor `@type` en de `sourceSchema` waarop deze van toepassing is. Zodra toegepast, zullen deze beschrijvers op alle datasets van toepassing zijn die gebruikend het schema worden gecreeerd.

Met het eindpunt `/descriptors` in de [!DNL Schema Registry] API kunt u beschrijvingen programmatisch beheren binnen uw ervaringstoepassing.

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Schema Registry]  API ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

## Een lijst met descriptoren ophalen {#list}

U kunt alle beschrijvingen weergeven die door uw organisatie zijn gedefinieerd door een aanvraag voor een GET in te dienen bij `/tenant/descriptors` .

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

Als u de details van een specifieke descriptor wilt bekijken, kunt u een afzonderlijke descriptor opzoeken (GET) met de bijbehorende `@id` .

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

U kunt een nieuwe beschrijver tot stand brengen door een verzoek van de POST aan het `/tenant/descriptors` eindpunt te doen.

>[!IMPORTANT]
>
>Met [!DNL Schema Registry] kunt u verschillende beschrijvende typen definiëren. Elk beschrijvingstype vereist dat zijn eigen specifieke gebieden in het aanvraaglichaam worden verzonden. Zie [ bijlage ](#defining-descriptors) voor een volledige lijst van beschrijvers en de gebieden noodzakelijk om hen te bepalen.

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

Met dit verzoek wordt in feite de descriptor herschreven, zodat de aanvraaginstantie alle velden moet bevatten die vereist zijn voor het definiëren van een descriptor van dat type. Met andere woorden, is de verzoeklading om (PUT) een beschrijver bij te werken het zelfde als de nuttige lading aan [ creeert (POST) een beschrijver ](#create) van het zelfde type.

>[!IMPORTANT]
>
>Net als bij het maken van beschrijvingen met behulp van POST-aanvragen, vereist elk descriptortype dat de eigen specifieke velden worden verzonden in de ladingen voor verzoeken om PUT. Zie [ bijlage ](#defining-descriptors) voor een volledige lijst van beschrijvers en de gebieden noodzakelijk om hen te bepalen.

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

Het uitvoeren van a [ raadpleging (GET) verzoek ](#lookup) om de beschrijver te bekijken toont aan dat de gebieden nu zijn bijgewerkt om op de veranderingen te wijzen die in het verzoek van de PUT worden verzonden.

## Een descriptor verwijderen {#delete}

Soms moet u een descriptor verwijderen die u in de [!DNL Schema Registry] hebt gedefinieerd. Dit wordt gedaan door een verzoek van de DELETE te doen van verwijzingen `@id` van de beschrijver die u wenst te verwijderen.

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

Om de beschrijver te bevestigen is geschrapt, kunt u a [ raadplegingsverzoek ](#lookup) tegen de beschrijver `@id` uitvoeren. De reactie retourneert HTTP-status 404 (Niet gevonden) omdat de descriptor is verwijderd uit de [!DNL Schema Registry] .

## Bijlage

In de volgende sectie vindt u aanvullende informatie over het werken met descriptoren in de API van [!DNL Schema Registry] .

### descriptoren definiëren {#defining-descriptors}

>[!NOTE]
>
>Het maximumaantal beschrijvingen dat op een schema kan worden toegepast is 4000.

In de volgende secties vindt u een overzicht van de beschikbare descriptortypen, inclusief de vereiste velden voor het definiëren van een descriptor voor elk type.

>[!IMPORTANT]
>
>U kunt het naamruimteobject voor huurders niet labelen, omdat het systeem dat label zou toepassen op elk aangepast veld in die sandbox. In plaats daarvan, moet u de bladknoop onder dat voorwerp specificeren die u moet etiketteren.

#### Identiteitsbeschrijving

Een identiteitsbeschrijver signaleert dat &quot;[!UICONTROL sourceProperty]&quot;van &quot;[!UICONTROL sourceSchema]&quot;een [!DNL Identity] gebied is zoals die door [ wordt beschreven de Dienst van de Identiteit van Adobe Experience Platform ](../../identity-service/home.md).

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
| `xdm:namespace` | De `id` - of `code` -waarde van de naamruimte identity. Een lijst van namespaces kan worden gevonden gebruikend [[!DNL Identity Service API] ](https://developer.adobe.com/experience-platform-apis/references/identity-service). |
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

#### Relatiebeschrijving

Relationship-descriptors beschrijven een relatie tussen twee verschillende schema&#39;s, die u hebt afgesloten op de eigenschappen die worden beschreven in `sourceProperty` en `destinationProperty` . Zie het leerprogramma op [ bepalend een verband tussen twee schema&#39;s ](../tutorials/relationship-api.md) voor meer informatie.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor een relatiebeschrijver, moet deze waarde aan `xdm:descriptorOneToOne` worden geplaatst. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Pad naar het veld in het bronschema waar de relatie wordt gedefinieerd. Moet beginnen met een &quot;/&quot; en niet eindigen met een &quot;/&quot;. Plaats geen &quot;eigenschappen&quot; in het pad (bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | De `$id` URI van het verwijzingsschema deze beschrijver bepaalt een verhouding met. |
| `xdm:destinationVersion` | De belangrijkste versie van het referentieschema. |
| `xdm:destinationProperty` | Optioneel pad naar een doelveld binnen het referentieschema. Als deze eigenschap wordt weggelaten, wordt het doelveld afgeleid van velden die een overeenkomende ID-descriptor bevatten (zie hieronder). |

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

U kunt [ een gebied binnen een douaneXDM middel ](../tutorials/field-deprecation-api.md#custom) verwerpen door a `meta:status` attributen toe te voegen die aan `deprecated` aan het betrokken gebied worden geplaatst. Als u velden die worden verschaft door standaard XDM-bronnen in uw schema&#39;s wilt vervangen, kunt u echter een vervangen velddescriptor toewijzen aan het desbetreffende schema om hetzelfde effect te bereiken. Gebruikend [ correcte `Accept` kopbal ](../tutorials/field-deprecation-api.md#verify-deprecation), kunt u dan bekijken welke standaardgebieden voor een schema verouderd zijn wanneer het omhoog kijken in API.

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
