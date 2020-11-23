---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;descriptor;Descriptor;descriptors;Descriptors;identity;Identity;friendly name;Friendly name;alternatedisplayinfo;reference;Reference;relationship;Relationship
solution: Experience Platform
title: Beschrijvers
description: Het /descriptors eindpunt in de Registratie API van het Schema staat u toe om XDM beschrijvers binnen uw ervaringstoepassing programmatically te beheren.
topic: developer guide
translation-type: tm+mt
source-git-commit: e92294b9dcea37ae2a4a398c9d3397dcf5aa9b9e
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---


# Het eindpunt van descriptors

De schema&#39;s bepalen een statische mening van gegevensentiteiten, maar verstrekken geen specifieke details over hoe gegevens die op deze regelingen (datasets, bijvoorbeeld) worden gebaseerd op elkaar kunnen betrekking hebben. Met Adobe Experience Platform kunt u deze relaties en andere interpreterende metagegevens over een schema beschrijven aan de hand van beschrijvingen.

De beschrijvers van het schema zijn huurdersvlakke meta-gegevens, die zij aan uw IMS Organisatie uniek zijn en alle beschrijvingsverrichtingen in de huurderscontainer plaatsvinden.

Op elk schema kunnen een of meer schemabeschrijvingsentiteiten zijn toegepast. Elke schemabeschrijvingsentiteit bevat een beschrijver `@type` en de `sourceSchema` waarop het van toepassing is. Zodra toegepast, zullen deze beschrijvers op alle datasets van toepassing zijn die gebruikend het schema worden gecreeerd.

Het `/descriptors` eindpunt in [!DNL Schema Registry] API staat u toe om beschrijvers binnen uw ervaringstoepassing programmatically te beheren.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Lees voordat u verdergaat de gids [Aan de](./getting-started.md) slag voor koppelingen naar gerelateerde documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar elke Experience Platform-API te kunnen uitvoeren.

## Een lijst met descriptoren ophalen {#list}

U kunt alle beschrijvingen weergeven die door uw organisatie zijn gedefinieerd door een aanvraag voor een GET in te dienen bij `/tenant/descriptors`.

**API-indeling**

```http
GET /tenant/descriptors
```

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

De antwoordindeling is afhankelijk van de `Accept` header die in de aanvraag wordt verzonden. Bericht dat het `/descriptors` eindpunt `Accept` kopballen gebruikt die verschillend zijn dan alle andere eindpunten in [!DNL Schema Registry] API.

>[!IMPORTANT]
>
>Descriptors vereisen unieke `Accept` kopballen die `xed` met `xdm`, vervangen en ook een `link` optie aanbieden die aan beschrijvers uniek is. De juiste `Accept` kopballen zijn inbegrepen in de voorbeelden roepen hieronder, maar neem extra voorzichtigheid in acht om ervoor te zorgen de correcte kopballen worden gebruikt wanneer het werken met beschrijvers.

| `Accept` header | Beschrijving |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Hiermee wordt een array met beschrijvings-id&#39;s geretourneerd |
| `application/vnd.adobe.xdm-link+json` | Hiermee wordt een array van beschrijvende API-paden geretourneerd |
| `application/vnd.adobe.xdm+json` | Hiermee wordt een array van uitgebreide beschrijvingsobjecten geretourneerd |
| `application/vnd.adobe.xdm-v2+json` | Deze `Accept` header moet worden gebruikt om pagineringsmogelijkheden te gebruiken. |

**Antwoord**

Het antwoord bevat een array voor elk beschrijvende type waarvoor beschrijvingen zijn gedefinieerd. Met andere woorden, als er geen beschrijvers van een bepaalde `@type` gedefinieerde definitie zijn, retourneert het register geen lege array voor dat descriptortype.

Wanneer u de `link``Accept` koptekst gebruikt, wordt elke descriptor weergegeven als een arrayitem in de notatie `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

Als u de details van een specifieke descriptor wilt bekijken, kunt u een afzonderlijke descriptor opzoeken (GET) met behulp van de bijbehorende `@id`descriptor.

**API-indeling**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De naam `@id` van de descriptor die u wilt opzoeken. |

**Verzoek**

Het volgende verzoek wint een beschrijver door zijn `@id` waarde terug. Descriptors hebben geen versioned, daarom wordt geen `Accept` kopbal vereist in het raadplegingsverzoek.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de descriptor, inclusief de details `@type` en `sourceSchema`, plus aanvullende informatie die afhankelijk is van het type descriptor. De geretourneerde waarde `@id` moet overeenkomen met de beschrijving die in de aanvraag is `@id` opgegeven.

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
  "imsOrg": "{IMS_ORG}",
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
>Met [!DNL Schema Registry] deze optie kunt u verschillende beschrijvingstypen definiëren. Elk beschrijvingstype vereist dat zijn eigen specifieke gebieden in het aanvraaglichaam worden verzonden. Zie de [bijlage](#defining-descriptors) voor een volledige lijst van beschrijvers en de gebieden noodzakelijk om hen te bepalen.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

In het volgende verzoek wordt een identiteitsbeschrijving gedefinieerd in een veld &quot;E-mailadres&quot; in een voorbeeldschema. Zo kunt u het e-mailadres gebruiken als id om informatie over het individu aan elkaar te koppelen. [!DNL Experience Platform]

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de details van de nieuwe descriptor, inclusief de `@id`beschrijving. Het `@id` is een alleen-lezen veld dat door de API is toegewezen [!DNL Schema Registry] en wordt gebruikt voor het verwijzen naar de descriptor in de API.

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

U kunt een descriptor bijwerken door de descriptor op te nemen `@id` in het pad van een verzoek om PUT.

**API-indeling**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De naam `@id` van de descriptor die u wilt bijwerken. |

**Verzoek**

Dit verzoek herschrijft in wezen de descriptor, zodat de aanvraaginstantie alle velden moet bevatten die vereist zijn voor het definiëren van een descriptor van dat type. Met andere woorden, de aanvraaglading om (PUT) een beschrijver bij te werken is het zelfde als nuttige lading om (POST) een beschrijver [van het zelfde type te](#create) creëren.

>[!IMPORTANT]
>
>Net als bij het maken van beschrijvingen met behulp van POST-aanvragen, vereist elk descriptortype dat de eigen specifieke velden worden verzonden in de ladingen voor verzoeken om PUT. Zie de [bijlage](#defining-descriptors) voor een volledige lijst van beschrijvers en de gebieden noodzakelijk om hen te bepalen.

In het volgende voorbeeld wordt een identiteitsdescriptor bijgewerkt om naar een andere `xdm:sourceProperty` (`mobile phone`) te verwijzen en de waarde in `xdm:namespace` te `Phone`wijzigen.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de status `@id` van de bijgewerkte descriptor (die moet overeenkomen met de `@id` verzonden in de aanvraag).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Als u een [opzoekverzoek](#lookup) (GET) uitvoert om de beschrijving weer te geven, wordt weergegeven dat de velden nu zijn bijgewerkt met de wijzigingen die zijn verzonden in het verzoek om PUT.

## Een descriptor verwijderen {#delete}

Het kan voorkomen dat u een descriptor moet verwijderen die u in het document hebt gedefinieerd [!DNL Schema Registry]. Dit wordt gedaan door een verzoek van de DELETE te maken van verwijzingen `@id` van de beschrijver u wenst te verwijderen.

**API-indeling**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De naam `@id` van het beschrijvingsbestand dat u wilt verwijderen. |

**Verzoek**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

Om te bevestigen dat de beschrijver is geschrapt, kunt u een [raadplegingsverzoek](#lookup) tegen de beschrijver uitvoeren `@id`. De reactie retourneert HTTP-status 404 (Niet gevonden) omdat de descriptor is verwijderd uit de [!DNL Schema Registry].

## Aanhangsel

De volgende sectie bevat aanvullende informatie over het werken met descriptoren in de [!DNL Schema Registry] API.

### descriptoren definiëren {#defining-descriptors}

In de volgende secties vindt u een overzicht van de beschikbare descriptortypen, inclusief de vereiste velden voor het definiëren van een descriptor voor elk type.

#### Identiteitsbeschrijving

Een identiteitsbeschrijver signaleert dat &quot;[!UICONTROL sourceProperty]&quot;van &quot;[!UICONTROL sourceSchema]&quot;een [!DNL Identity] gebied is zoals die door de Dienst [van de Identiteit van](../../identity-service/home.md)Adobe Experience Platform wordt beschreven.

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
| `@type` | Het type descriptor dat wordt gedefinieerd. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Het pad naar de specifieke eigenschap die de identiteit zal zijn. Het pad moet beginnen met een &quot;/&quot; en niet eindigen met een pad. Plaats geen &quot;eigenschappen&quot; in het pad (gebruik bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;) |
| `xdm:namespace` | De `id` of `code` waarde van de naamruimte identity. U kunt een lijst met naamruimten vinden met de [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)instructies. |
| `xdm:property` | Of `xdm:id` of `xdm:code`, afhankelijk van de `xdm:namespace` gebruikte methode. |
| `xdm:isPrimary` | Een optionele booleaanse waarde. Indien waar (true), wordt het veld als de primaire identiteit aangegeven. Schema&#39;s mogen slechts één primaire identiteit bevatten. |

#### Beschrijvende naam

Met beschrijvingen van uw vriendschappelijke naam kan een gebruiker de `title`, `description`en `meta:enum` waarden van de kernvelden van het bibliotheekschema wijzigen. Dit is vooral handig wanneer u werkt met &quot;eVars&quot; en andere &quot;generieke&quot; velden die u wilt labelen voor informatie die specifiek is voor uw organisatie. De gebruikersinterface kan deze gebruiken om een vriendelijkere naam weer te geven of om alleen velden met een vriendelijke naam weer te geven.

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
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Het pad naar de specifieke eigenschap die de identiteit zal zijn. Het pad moet beginnen met een &quot;/&quot; en niet eindigen met een pad. Plaats geen &quot;eigenschappen&quot; in het pad (gebruik bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;) |
| `xdm:title` | De nieuwe titel die u voor dit veld wilt weergeven, geschreven in Alles Beginhoofdletter. |
| `xdm:description` | Een optionele beschrijving kan samen met de titel worden toegevoegd. |
| `meta:enum` | Als het veld dat door wordt aangegeven een tekenreeksveld `xdm:sourceProperty` is, wordt de lijst met voorgestelde waarden voor het veld in de `meta:enum` UI [!DNL Experience Platform] bepaald. Het is belangrijk om op te merken dat `meta:enum` geen opsomming verklaart of om het even welke gegevensbevestiging voor het XDM gebied verstrekt.<br><br>Deze mag alleen worden gebruikt voor de belangrijkste XDM-velden die door Adobe worden gedefinieerd. Als het bronbezit een douanegebied is dat door uw organisatie wordt bepaald, zou u het `meta:enum` bezit van het gebied door een verzoek van de PATCH aan het oudermiddel van het gebied direct moeten uitgeven. |

#### Relatiebeschrijving

Relationship-descriptors beschrijven een relatie tussen twee verschillende schema&#39;s, die u hebt afgesloten op de eigenschappen die in `sourceProperty` en `destinationProperty`worden beschreven. Zie de zelfstudie over het [definiëren van een relatie tussen twee schema&#39;s](../tutorials/relationship-api.md) voor meer informatie.

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
| `@type` | Het type descriptor dat wordt gedefinieerd. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Pad naar het veld in het bronschema waar de relatie wordt gedefinieerd. Moet beginnen met een &quot;/&quot; en niet eindigen met een &quot;/&quot;. Plaats geen &quot;eigenschappen&quot; in het pad (bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | De `$id` URI van het doelschema waarmee deze descriptor een relatie definieert. |
| `xdm:destinationVersion` | De belangrijkste versie van het bestemmingsschema. |
| `xdm:destinationProperty` | Optioneel pad naar een doelveld binnen het doelschema. Als deze eigenschap wordt weggelaten, wordt het doelveld afgeleid van velden die een overeenkomende ID-descriptor bevatten (zie hieronder). |


#### Referentie-identiteitsdescriptor

De identiteitsbeschrijvers van de verwijzing verstrekken een verwijzingscontext aan de primaire identiteit van een schemagebied, toelatend het om door gebieden in andere schema&#39;s worden van verwijzingen voorzien. Velden moeten al zijn gelabeld met een identiteitsdescriptor voordat er een verwijzingsdescriptor op kan worden toegepast.

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
| `@type` | Het type descriptor dat wordt gedefinieerd. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Pad naar het veld in het bronschema waar de descriptor wordt gedefinieerd. Moet beginnen met een &quot;/&quot; en niet eindigen met een &quot;/&quot;. Plaats geen &quot;eigenschappen&quot; in het pad (bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | De naamruimtecode van de identiteit voor de eigenschap source. |