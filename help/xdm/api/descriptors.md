---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Schema Register;Schema Register;Descriptor;Descriptors;Descriptors;Identiteit;Vriendelijke naam;Alternatieve naam;AlternateInfo;Referentie;Referentie;Relatie;Relatie
solution: Experience Platform
title: Descriptors API-eindpunt
description: Het /descriptors eindpunt in de Registratie API van het Schema staat u toe om XDM beschrijvers binnen uw ervaringstoepassing programmatically te beheren.
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: b92246e729ca26387a3d375e5627165a29956e52
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Het eindpunt van descriptors

De schema&#39;s bepalen een statische mening van gegevensentiteiten, maar verstrekken geen specifieke details over hoe gegevens die op deze regelingen (datasets, bijvoorbeeld) worden gebaseerd op elkaar kunnen betrekking hebben. Met Adobe Experience Platform kunt u deze relaties en andere interpreterende metagegevens over een schema beschrijven aan de hand van beschrijvingen.

De beschrijvers van het schema zijn huurdersvlakke meta-gegevens, die zij aan uw IMS Organisatie uniek zijn en alle beschrijvingsverrichtingen in de huurderscontainer plaatsvinden.

Op elk schema kunnen een of meer schemabeschrijvingsentiteiten zijn toegepast. Elke schemadescriptorentiteit bevat een descriptor `@type` en de `sourceSchema` waarop zij van toepassing is. Zodra toegepast, zullen deze beschrijvers op alle datasets van toepassing zijn die gebruikend het schema worden gecreeerd.

De `/descriptors` in de [!DNL Schema Registry] Met API kunt u beschrijvingen programmatisch beheren binnen uw ervaringstoepassing.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Een lijst met descriptoren ophalen {#list}

U kunt alle beschrijvingen weergeven die door uw organisatie zijn gedefinieerd door een GET-aanvraag in te dienen bij `/tenant/descriptors`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

De responsindeling is afhankelijk van `Accept` in de aanvraag verzonden. Let erop dat de `/descriptors` eindpuntgebruik `Accept` kopteksten die verschillen van alle andere eindpunten in de [!DNL Schema Registry] API.

>[!IMPORTANT]
>
>Descriptors vereisen unieke `Accept` kopteksten die vervangen `xed` with `xdm`en biedt tevens een `link` -optie die uniek is voor beschrijvingen. De juiste `Accept` De kopballen zijn inbegrepen in de voorbeelden hieronder vraag, maar neem extra voorzichtigheid in acht om ervoor te zorgen de correcte kopballen worden gebruikt wanneer het werken met beschrijvers.

| `Accept` header | Beschrijving |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Hiermee wordt een array met beschrijvings-id&#39;s geretourneerd |
| `application/vnd.adobe.xdm-link+json` | Hiermee wordt een array van beschrijvende API-paden geretourneerd |
| `application/vnd.adobe.xdm+json` | Hiermee wordt een array van uitgebreide beschrijvingsobjecten geretourneerd |
| `application/vnd.adobe.xdm-v2+json` | Dit `Accept` header moet worden gebruikt om pagineringsmogelijkheden te gebruiken. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Het antwoord bevat een array voor elk beschrijvende type waarvoor beschrijvingen zijn gedefinieerd. Met andere woorden, als er geen beschrijvingen zijn van een bepaalde `@type` gedefinieerd, retourneert het register geen lege array voor dat descriptortype.

Wanneer u de `link` `Accept` koptekst, wordt elke descriptor weergegeven als een arrayitem in de notatie `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

Als u de details van een specifieke descriptor wilt weergeven, kunt u een afzonderlijke descriptor opzoeken (GET) met behulp van de bijbehorende `@id`.

**API-indeling**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De `@id` van de descriptor die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt een descriptor opgehaald op basis van `@id` waarde. Er is geen versienummer voor de descriptors en daarom is er geen `Accept` header is vereist in het opzoekverzoek.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert de details van de descriptor, inclusief zijn `@type` en `sourceSchema`en aanvullende informatie die afhankelijk is van het type descriptor. De geretourneerde `@id` moet overeenkomen met de descriptor `@id` die in het verzoek worden verstrekt.

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

U kunt een nieuwe descriptor maken door een POST aan te vragen bij de `/tenant/descriptors` eindpunt.

>[!IMPORTANT]
>
>De [!DNL Schema Registry] Hiermee kunt u verschillende beschrijvende typen definiëren. Elk beschrijvingstype vereist dat zijn eigen specifieke gebieden in het aanvraaglichaam worden verzonden. Zie de [aanhangsel](#defining-descriptors) voor een volledige lijst van beschrijvingen en de velden die nodig zijn om deze te definiëren.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

In het volgende verzoek wordt een identiteitsbeschrijving gedefinieerd in een veld &quot;E-mailadres&quot; in een voorbeeldschema. Dit vertelt [!DNL Experience Platform] om het e-mailadres te gebruiken als id om informatie over het individu te koppelen.

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

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en de details van de nieuwe descriptor, inclusief de bijbehorende `@id`. De `@id` is een alleen-lezen veld dat is toegewezen door de [!DNL Schema Registry] en wordt gebruikt voor het verwijzen naar de descriptor in de API.

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

U kunt een descriptor bijwerken door de bijbehorende `@id` in de weg van een verzoek van de PUT.

**API-indeling**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De `@id` van de descriptor die u wilt bijwerken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Dit verzoek herschrijft in wezen de descriptor, zodat de aanvraaginstantie alle velden moet bevatten die vereist zijn voor het definiëren van een descriptor van dat type. Met andere woorden, de aanvraaglading om (PUT) een beschrijver bij te werken is het zelfde als nuttige lading aan [een descriptor maken (POST)](#create) van hetzelfde type.

>[!IMPORTANT]
>
>Net als bij het maken van beschrijvingen met behulp van POST-aanvragen, vereist elk descriptortype dat de eigen specifieke velden worden verzonden in de ladingen voor verzoeken om PUT. Zie de [aanhangsel](#defining-descriptors) voor een volledige lijst van beschrijvingen en de velden die nodig zijn om deze te definiëren.

In het volgende voorbeeld wordt een identiteitsdescriptor bijgewerkt om naar een ander voorbeeld te verwijzen `xdm:sourceProperty` (`mobile phone`) en wijzigt u de `xdm:namespace` tot `Phone`.

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

**Antwoord**

Een geslaagde reactie retourneert de HTTP-status 201 (Gemaakt) en de `@id` van de bijgewerkte descriptor (die moet overeenkomen met de `@id` verzonden in het verzoek).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Een [opzoekverzoek (GET)](#lookup) om de beschrijver te bekijken zal tonen dat de gebieden nu zijn bijgewerkt om op de veranderingen te wijzen die in het verzoek van de PUT worden verzonden.

## Een descriptor verwijderen {#delete}

Soms moet u een descriptor die u hebt gedefinieerd, verwijderen uit het dialoogvenster [!DNL Schema Registry]. Dit wordt gedaan door een verzoek van DELETE te doen van verwijzingen voorzien `@id` van de beschrijving die u wilt verwijderen.

**API-indeling**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DESCRIPTOR_ID}` | De `@id` van de descriptor die u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

Om te bevestigen dat de descriptor is verwijderd, kunt u een [opzoekverzoek](#lookup) tegen de descriptor `@id`. De reactie retourneert HTTP-status 404 (Niet gevonden) omdat de descriptor is verwijderd uit het dialoogvenster [!DNL Schema Registry].

## Aanhangsel

In de volgende sectie vindt u aanvullende informatie over het werken met descriptoren in de [!DNL Schema Registry] API.

### descriptoren definiëren {#defining-descriptors}

In de volgende secties vindt u een overzicht van de beschikbare descriptortypen, inclusief de vereiste velden voor het definiëren van een descriptor voor elk type.

#### Identiteitsbeschrijving

Een identiteitsbeschrijver signaleert dat &quot;[!UICONTROL sourceProperty]&quot; van de &quot;[!UICONTROL sourceSchema]&quot; is een [!DNL Identity] veld zoals beschreven door [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor een identiteitsbeschrijving moet deze waarde worden ingesteld op `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Het pad naar de specifieke eigenschap die de identiteit zal zijn. Het pad moet beginnen met een &quot;/&quot; en niet eindigen met een pad. Plaats geen &quot;eigenschappen&quot; in het pad (gebruik bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;) |
| `xdm:namespace` | De `id` of `code` waarde van de naamruimte identity. Een lijst met naamruimten vindt u in het dialoogvenster [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | Willekeurig `xdm:id` of `xdm:code`, afhankelijk van de `xdm:namespace` gebruikt. |
| `xdm:isPrimary` | Een optionele booleaanse waarde. Indien waar (true), wordt het veld als de primaire identiteit aangegeven. Schema&#39;s mogen slechts één primaire identiteit bevatten. |

{style=&quot;table-layout:auto&quot;}

#### Beschrijvende naam {#friendly-name}

Met beschrijvingen van familienaam kan een gebruiker de `title`, `description`, en `meta:enum` waarden van de kernvelden van het bibliotheekschema. Dit is vooral handig wanneer u werkt met &quot;eVars&quot; en andere &quot;generieke&quot; velden die u wilt labelen voor informatie die specifiek is voor uw organisatie. De gebruikersinterface kan deze gebruiken om een vriendelijkere naam weer te geven of om alleen velden met een vriendelijke naam weer te geven.

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
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor een beschrijvende naam moet deze waarde worden ingesteld op `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Het pad naar de specifieke eigenschap die de identiteit zal zijn. Het pad moet beginnen met een &quot;/&quot; en niet eindigen met een pad. Plaats geen &quot;eigenschappen&quot; in het pad (gebruik bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;) |
| `xdm:title` | De nieuwe titel die u voor dit veld wilt weergeven, geschreven in Alles Beginhoofdletter. |
| `xdm:description` | Een optionele beschrijving kan samen met de titel worden toegevoegd. |
| `meta:enum` | Indien het veld wordt aangegeven door `xdm:sourceProperty` is een tekenreeksveld, `meta:enum` bepaalt de lijst met voorgestelde waarden voor het veld in het dialoogvenster [!DNL Experience Platform] UI. Het is belangrijk op te merken dat `meta:enum` declareert geen opsomming of biedt geen gegevensvalidatie voor het XDM-veld.<br><br>Deze mag alleen worden gebruikt voor de belangrijkste XDM-velden die door Adobe worden gedefinieerd. Als de broneigenschap een aangepast veld is dat door uw organisatie is gedefinieerd, moet u in plaats daarvan de veldcode `meta:enum` rechtstreeks via een PATCH-verzoek aan de bovenliggende bron van het veld. |

{style=&quot;table-layout:auto&quot;}

#### Relatiebeschrijving

Relatiebeschrijvingen beschrijven een relatie tussen twee verschillende schema&#39;s, die worden vastgehouden op de eigenschappen die worden beschreven in `sourceProperty` en `destinationProperty`. Zie de zelfstudie aan [het bepalen van een verband tussen twee schema&#39;s](../tutorials/relationship-api.md) voor meer informatie .

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
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor een relatiebeschrijving moet deze waarde worden ingesteld op `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Pad naar het veld in het bronschema waar de relatie wordt gedefinieerd. Moet beginnen met een &quot;/&quot; en niet eindigen met een &quot;/&quot;. Plaats geen &quot;eigenschappen&quot; in het pad (bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | De `$id` URI of the destination schema this descriptor is define a relationship with. |
| `xdm:destinationVersion` | De belangrijkste versie van het bestemmingsschema. |
| `xdm:destinationProperty` | Optioneel pad naar een doelveld binnen het doelschema. Als deze eigenschap wordt weggelaten, wordt het doelveld afgeleid van velden die een overeenkomende ID-descriptor bevatten (zie hieronder). |

{style=&quot;table-layout:auto&quot;}

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
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor een identiteitsbeschrijving van een referentie moet deze waarde worden ingesteld op `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | De `$id` URI van het schema waarin de descriptor wordt gedefinieerd. |
| `xdm:sourceVersion` | De belangrijkste versie van het bronschema. |
| `xdm:sourceProperty` | Pad naar het veld in het bronschema waar de descriptor wordt gedefinieerd. Moet beginnen met een &quot;/&quot; en niet eindigen met een &quot;/&quot;. Plaats geen &quot;eigenschappen&quot; in het pad (bijvoorbeeld &quot;/PersonalEmail/address&quot; in plaats van &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | De naamruimtecode van de identiteit voor de eigenschap source. |

{style=&quot;table-layout:auto&quot;}

#### Vervangen velddescriptor

U kunt [een veld binnen een aangepaste XDM-bron vervangen](../tutorials/field-deprecation.md#custom) door een `meta:status` kenmerk ingesteld op `deprecated` op het betrokken gebied. Als u velden die worden verschaft door standaard XDM-bronnen in uw schema&#39;s wilt vervangen, kunt u echter een vervangen velddescriptor toewijzen aan het desbetreffende schema om hetzelfde effect te bereiken. Met de [correct `Accept` header](../tutorials/field-deprecation.md#verify-deprecation)kunt u vervolgens bekijken welke standaardvelden zijn vervangen voor een schema wanneer u het opzoekt in de API.

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
| `@type` | Het type descriptor. Voor een beschrijving van de veldafdrukking moet deze waarde worden ingesteld op `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | De URI `$id` van het schema waarop u de descriptor toepast. |
| `xdm:sourceVersion` | De versie van het schema waarop u de descriptor toepast. Moet worden ingesteld op `1`. |
| `xdm:sourceProperty` | Het pad naar de eigenschap in het schema waarop u de descriptor toepast. Als u de descriptor op meerdere eigenschappen wilt toepassen, kunt u een lijst met paden opgeven in de vorm van een array (bijvoorbeeld `["/firstName", "/lastName"]`). |

{style=&quot;table-layout:auto&quot;}
