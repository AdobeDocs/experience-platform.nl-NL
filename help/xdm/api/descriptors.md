---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beschrijvers
topic: developer guide
translation-type: tm+mt
source-git-commit: c8cc57a8629f04c7af68b6f5cfee365527caa3c1
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# Beschrijvers

De schema&#39;s bepalen een statische mening van gegevensentiteiten, maar verstrekken geen specifieke details over hoe gegevens die op deze regelingen (datasets, bijvoorbeeld) worden gebaseerd op elkaar kunnen betrekking hebben. Met het Adobe Experience Platform kunt u deze relaties en andere interpreterende metagegevens over een schema beschrijven aan de hand van beschrijvingen.

De beschrijvers van het schema zijn huurdersvlakke meta-gegevens, die zij aan uw IMS Organisatie uniek zijn en alle beschrijvingsverrichtingen in de huurderscontainer plaatsvinden.

Op elk schema kunnen een of meer schemabeschrijvingsentiteiten zijn toegepast. Elke schemabeschrijvingsentiteit bevat een beschrijver `@type` en de `sourceSchema` waarop het van toepassing is. Zodra toegepast, zullen deze beschrijvers op alle datasets van toepassing zijn die gebruikend het schema worden gecreeerd.

Dit document bevat voorbeelden van API-aanroepen voor beschrijvingen en een volledige lijst met beschikbare descriptoren en de velden die vereist zijn voor het definiëren van elk type.

>[!NOTE] De beschrijvers vereisen unieke Accept kopballen die `xed` `xdm`met vervangen, maar anders zeer gelijkend op Accept kopballen die elders in de Registratie van het Schema worden gebruikt kijken. De juiste Accept kopballen zijn inbegrepen in de steekproefvraag hieronder, maar neem extra voorzichtigheid in acht om ervoor te zorgen de correcte kopballen worden gebruikt.

## Lijstbeschrijvingen

Één enkel GET verzoek kan worden gebruikt om een lijst van alle beschrijvers terug te keren die door uw organisatie zijn bepaald.

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

De responsindeling is afhankelijk van de Accept-header die in de aanvraag wordt verzonden. Bericht dat het `/descriptors` eindpuntgebruik Accepteert kopballen die verschillend zijn dan alle andere eindpunten in de Registratie API van het Schema.

Descriptor accepteert koppen die worden vervangen `xed` door `xdm`, en biedt een `link` optie die uniek is voor beschrijvingen.

| Accepteren | Beschrijving |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Hiermee wordt een array met beschrijvings-id&#39;s geretourneerd |
| `application/vnd.adobe.xdm-link+json` | Hiermee wordt een array van beschrijvende API-paden geretourneerd |
| `application/vnd.adobe.xdm+json` | Hiermee wordt een array van uitgebreide beschrijvingsobjecten geretourneerd |

**Antwoord**

Het antwoord bevat een array voor elk beschrijvende type waarvoor beschrijvingen zijn gedefinieerd. Met andere woorden, als er geen beschrijvers van een bepaalde `@type` gedefinieerde definitie zijn, retourneert het register geen lege array voor dat descriptortype.

Wanneer u de koptekst `link` Accepteren gebruikt, wordt elke descriptor weergegeven als een arrayitem in de notatie `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

## Een descriptor opzoeken

Als u de details van een specifieke descriptor wilt bekijken, kunt u een afzonderlijke descriptor opzoeken (GET) met behulp van zijn `@id`.

**API-indeling**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De naam `@id` van het beschrijvingsbestand dat u wilt opzoeken. |

**Verzoek**

De beschrijvers zijn niet versioned, daarom wordt geen Accept kopbal vereist in het raadplegingsverzoek.

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

## descriptor maken

Met de schemaregistratie kunt u verschillende beschrijvende typen definiëren. Elk beschrijvingstype vereist dat zijn eigen specifieke gebieden in het POST- verzoek worden verzonden. Een volledige lijst van beschrijvingen en de velden die nodig zijn om deze te definiëren, is beschikbaar in de bijlage over het [definiëren van beschrijvingen](#defining-descriptors).

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

In het volgende verzoek wordt een identiteitsdescriptor gedefinieerd in een voorbeeldschema in het veld E-mailadres. Dit vertelt het Platform van de Ervaring om het e-mailadres als herkenningsteken te gebruiken helpen informatie over het individu samenvoegen.

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

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de details van de nieuwe descriptor, inclusief de `@id`beschrijving. Het `@id` is een alleen-lezen veld dat is toegewezen door de schemaregistratie en dat wordt gebruikt voor het verwijzen naar de descriptor in de API.

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

## Descriptor bijwerken

U kunt een descriptor bijwerken door een PUT-aanvraag in te dienen die verwijst naar de beschrijving `@id` die u wilt bijwerken in het aanvraagpad.

**API-indeling**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De naam `@id` van de descriptor die u wilt bijwerken. |

**Verzoek**

Dit verzoek _herschrijft_ in wezen de descriptor, zodat de aanvraaginstantie alle velden moet bevatten die vereist zijn voor het definiëren van een descriptor van dat type. Met andere woorden, de bij te werken aanvraaglading (PUT) is de beschrijver het zelfde als nuttige lading om (POST) een beschrijver van het zelfde type tot stand te brengen.

In dit voorbeeld wordt de identiteitsbeschrijving bijgewerkt om naar een andere `xdm:sourceProperty` (&quot;mobiele telefoon&quot;) te verwijzen en de naam `xdm:namespace` te wijzigen in &quot;Telefoon&quot;.

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

Nadere bijzonderheden over de eigenschappen `xdm:namespace` en `xdm:property`, waaronder de manier waarop ze kunnen worden benaderd, zijn beschikbaar in de bijlage over het [definiëren van beschrijvingen](#defining-descriptors).

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de status `@id` van de bijgewerkte descriptor (die moet overeenkomen met de `@id` verzonden in de aanvraag).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Als u een opzoekverzoek (GET) uitvoert om de descriptor weer te geven, wordt weergegeven dat de velden nu zijn bijgewerkt met de wijzigingen die zijn verzonden in de PUT-aanvraag.

## descriptor verwijderen

Soms moet u een descriptor verwijderen die u in de schemaregistratie hebt gedefinieerd. Dit wordt gedaan door een verzoek van de SCHRAPPING te maken die van de beschrijver verwijst u wenst om te verwijderen. `@id`

**API-indeling**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De naam `@id` van het beschrijvingsbestand dat u wilt verwijderen. |

**Verzoek**

Koppen accepteren is niet vereist wanneer beschrijvingen worden verwijderd.

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

Om te bevestigen dat de descriptor is verwijderd, kunt u een opzoekverzoek uitvoeren op de descriptor `@id`. De reactie keert status 404 van HTTP terug (niet Gevonden) omdat de beschrijver uit de Registratie van het Schema is verwijderd.

## Aanhangsel

De volgende sectie verstrekt extra informatie betreffende het werken met beschrijvers in de Registratie API van het Schema.

### descriptoren definiëren

In de volgende secties vindt u een overzicht van de beschikbare descriptortypen, inclusief de vereiste velden voor het definiëren van een descriptor voor elk type.

#### Identiteitsbeschrijving

Een identiteitsbeschrijving geeft aan dat de &quot;sourceProperty&quot; van de &quot;sourceSchema&quot; een identiteitsveld is zoals beschreven door de Identity Service [van het](../../identity-service/home.md)Adobe Experience Platform.

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
| `xdm:namespace` | De `id` of `code` waarde van de naamruimte identity. Een lijst met naamruimten kunt u vinden met de API [van de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)identiteitsservice. |
| `xdm:property` | Of `xdm:id` of `xdm:code`, afhankelijk van de `xdm:namespace` gebruikte methode. |
| `xdm:isPrimary` | Een optionele booleaanse waarde. Indien waar (true), wordt het veld als de primaire identiteit aangegeven. Schema&#39;s mogen slechts één primaire identiteit bevatten. |

#### Beschrijvende naam

Met beschrijvende namen met een vriendelijke naam kan een gebruiker de `title`, `description`en `meta:enum` waarden van de kernvelden van het bibliotheekschema wijzigen. Dit is vooral handig wanneer u werkt met &quot;eVars&quot; en andere &quot;generieke&quot; velden die u wilt labelen voor informatie die specifiek is voor uw organisatie. De gebruikersinterface kan deze gebruiken om een vriendelijkere naam weer te geven of om alleen velden met een vriendelijke naam weer te geven.

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
| `meta:enum` | Als het veld dat wordt aangegeven door een tekenreeksveld `xdm:sourceProperty` is, wordt de lijst met voorgestelde waarden voor het veld in de gebruikersinterface van het ervaringsplatform `meta:enum` bepaald. Het is belangrijk om op te merken dat `meta:enum` geen opsomming verklaart of om het even welke gegevensbevestiging voor het XDM gebied verstrekt.<br><br>Deze mag alleen worden gebruikt voor de belangrijkste XDM-velden die door Adobe zijn gedefinieerd. Als de broneigenschap een aangepast veld is dat door uw organisatie is gedefinieerd, moet u in plaats daarvan de `meta:enum` eigenschap van het veld rechtstreeks bewerken via een [PUT-aanvraag](./update-resource.md). |

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

De identiteitsbeschrijvers van de verwijzing verstrekken een verwijzingscontext aan een schemagebied, toestaand het om met het primaire identiteitsgebied van een bestemmingsschema worden verbonden. Velden moeten al zijn gelabeld met een identiteitsdescriptor voordat er een verwijzingsdescriptor op kan worden toegepast.

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