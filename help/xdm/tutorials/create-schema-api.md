---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Gegevensmodel;Gegevensmodel;Schema register;Schema Register;Schema;Schema;schema's;Schema's;Maken
solution: Experience Platform
title: Een schema maken met de API voor het schemaregister
type: Tutorial
description: Deze zelfstudie gebruikt de API voor schemaregistratie om u door de stappen te laten lopen om een schema samen te stellen met een standaardklasse.
exl-id: fa487a5f-d914-48f6-8d1b-001a60303f3d
source-git-commit: 3dffa9687f3429b970e8fceebd6864a5b61ead21
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 0%

---

# Een schema maken met de API van [!DNL Schema Registry]

[!DNL Schema Registry] wordt gebruikt om [!DNL Schema Library] binnen Adobe Experience Platform te openen. [!DNL Schema Library] bevat middelen die aan u door Adobe, [!DNL Experience Platform] partners, en verkopers ter beschikking worden gesteld waarvan toepassingen u gebruikt. Het register biedt een gebruikersinterface en RESTful-API die toegang bieden tot alle beschikbare bibliotheekbronnen.

Deze zelfstudie gebruikt de [!DNL Schema Registry] API om u door de stappen te laten lopen om een schema samen te stellen met een standaardklasse. Als u het gebruikersinterface in [!DNL Experience Platform] liever zou gebruiken, verstrekt het [ Zelfstudie van de Redacteur van het Schema ](create-schema-ui.md) geleidelijke instructies voor het uitvoeren van gelijkaardige acties in de schemaredacteur.

>[!NOTE]
>
>Als u CSV gegevens in Platform opneemt, kunt u [ kaart dat gegevens aan een XDM schema dat door AI-Gegenereerde aanbevelingen ](../../ingestion/tutorials/map-csv/recommendations.md) wordt gecreeerd (momenteel in bèta) zonder het moeten manueel het schema creëren zelf.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
   * [ Grondbeginselen van schemacompositie ](../schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Alvorens dit leerprogramma te beginnen, te herzien gelieve de [ ontwikkelaarsgids ](../api/getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan [!DNL Schema Registry] API met succes te maken. Dit omvat uw `{TENANT_ID}` , het concept &quot;containers&quot; en de vereiste kopteksten voor het indienen van aanvragen (met speciale aandacht voor de header `Accept` en de mogelijke waarden ervan).

Deze zelfstudie doorloopt de stappen voor het samenstellen van een schema voor leden van Loyalty&#39;s dat gegevens beschrijft die betrekking hebben op de leden van een programma voor loyaliteit in de detailhandel. Alvorens te beginnen, kunt u aan voorproef het [ volledige schema van de Leden van de Loyalty ](#complete-schema) in het bijlage wensen.

## Een schema met een standaardklasse samenstellen

Een schema kan worden beschouwd als de blauwdruk voor de gegevens die u wilt invoeren in [!DNL Experience Platform] . Elk schema bestaat uit een klasse en nul of meer groepen schemavelden. Met andere woorden, u hoeft geen veldgroep toe te voegen om een schema te definiëren, maar in de meeste gevallen wordt ten minste één veldgroep gebruikt.

### Een klasse toewijzen

Het proces van de schemacompositie begint met de selectie van een klasse. De klasse definieert de belangrijkste gedragsaspecten van de gegevens (record- versus tijdreeks) en de minimale velden die vereist zijn om de gegevens te beschrijven die worden ingevoerd.

Het schema dat u in deze zelfstudie maakt, gebruikt de klasse [!DNL XDM Individual Profile] . [!DNL XDM Individual Profile] is een standaardklasse die door Adobe wordt verstrekt voor het bepalen van verslaggedrag. Meer informatie over gedrag kan in [ grondbeginselen van schemacompositie ](../schema/composition.md) worden gevonden.

Om een klasse toe te wijzen, wordt een API vraag gemaakt om (POST) een nieuw schema in de huurderscontainer tot stand te brengen. Deze vraag omvat de klasse het schema zal uitvoeren. Elk schema mag slechts één klasse implementeren.

**API formaat**

```http
POST /tenant/schemas
```

**Verzoek**

De aanvraag moet een `allOf` -kenmerk bevatten dat naar de `$id` van een klasse verwijst. Dit attribuut bepaalt de &quot;basisklasse&quot;die het schema zal uitvoeren. In dit voorbeeld is de basisklasse de [!DNL XDM Individual Profile] -klasse. De `$id` van de [!DNL XDM Individual Profile] -klasse wordt gebruikt als de waarde van het `$ref` -veld in de onderstaande `allOf` -array.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Members",
        "description": "Information for all members of the loyalty program",
        "allOf": [
            {
              "$ref": "https://ns.adobe.com/xdm/context/profile"
            }
        ]
      }'
```

**Reactie**

Een geslaagde aanvraag retourneert HTTP Response Status 201 (Gemaakt) met een hoofdtekst van de reactie die de details bevat van het nieuwe schema, inclusief `$id`, `meta:altIt` en `version` . Deze waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry] .

```JSON
{
  "$id": "https://ns.adobe.com/tenantId/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_tenantId.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310304048,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_tenantId"
}
```

### Een schema opzoeken

Als u het nieuwe schema wilt weergeven, voert u een opzoekaanvraag (GET) uit met de URI `meta:altId` of de URL-gecodeerde `$id` voor het schema.

**API formaat**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema dat u wilt opzoeken. |

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F533ca5da28087c44344810891b0f03d9\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

**Reactie**

De antwoordindeling is afhankelijk van de header `Accept` die met de aanvraag is verzonden. Experimenteer met verschillende kopteksten in `Accept` om te zien welke het beste aan uw behoeften voldoen.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310304048,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:allFieldAccess": true
}
```

### Een veldgroep toevoegen {#add-a-field-group}

Nu het schema Loyalty-leden is gemaakt en bevestigd, kunnen er veldgroepen aan worden toegevoegd.

Er zijn verschillende standaardveldgroepen beschikbaar voor gebruik, afhankelijk van de geselecteerde schemaklasse. Elke veldgroep bevat een `intendedToExtend` -veld dat de klasse(n) definieert waarmee die veldgroep compatibel is.

Veldgroepen definiëren concepten, zoals &quot;naam&quot; of &quot;adres&quot;, die opnieuw kunnen worden gebruikt in elk schema dat dezelfde informatie moet vastleggen.

**API formaat**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema waaraan u de veldgroep toevoegt. |

**Verzoek**

Dit verzoek werkt het schema van de Leden van de Loyalty bij om de gebieden binnen de [[!UICONTROL Demographic Details] gebiedsgroep ](../field-groups/profile/demographic-details.md) (`profile-person-details`) te omvatten.

Door de `profile-person-details` gebiedsgroep toe te voegen, vangt het schema van de Leden van de Loyalty nu demografische informatie voor de leden van het loyaliteitsprogramma zoals hun voornaam, familienaam, en verjaardag.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-person-details"}}
      ]'
```

**Reactie**

In het antwoord wordt de zojuist toegevoegde veldgroep weergegeven in de array `meta:extends` en wordt een `$ref` weergegeven voor de veldgroep in het kenmerk `allOf` .

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310912096,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "b480f28a35f356b237fc129e796074a3f33a7a67df273f6a8beaee1ec6465540",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### Meer veldgroepen toevoegen

Voor de schema&#39;s van Loyalty-leden zijn nog twee standaardveldgroepen vereist, die u kunt toevoegen door de stappen te herhalen met een andere veldgroep.

>[!TIP]
>
>Het is nuttig om alle beschikbare gebiedsgroepen te herzien om zich met de gebieden vertrouwd te maken inbegrepen in elk. U kunt (GET) alle gebiedsgroepen vermelden beschikbaar voor gebruik met een bepaalde klasse door een verzoek tegen elk van &quot;globale&quot;en &quot;huurder&quot;containers uit te voeren, die slechts die gebiedsgroepen terugkeren waar het &quot;meta:intendedToExtend&quot;gebied de klasse aanpast u gebruikt. In dit geval is het de [!DNL XDM Individual Profile] -klasse, dus wordt [!DNL XDM Individual Profile] `$id` gebruikt:
>
>```http
>GET /global/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>GET /tenant/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>```

**API formaat**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema dat u bijwerkt. |

**Verzoek**

Met dit verzoek wordt het schema Loyalty-leden bijgewerkt en worden de velden in de volgende standaardveldgroepen opgenomen:

* [[!UICONTROL Personal Contact Details]](../field-groups/profile/personal-contact-details.md) (`profile-personal-details`): Voegt contactinformatie zoals huisadres, e-mailadres, en huistelefoon toe.
* [[!UICONTROL Loyalty Details]](../field-groups/profile/loyalty-details.md) (`profile-loyalty-details`): Voegt contactinformatie zoals huisadres, e-mailadres, en huistelefoon toe.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"}}
      ]'  
```

**Reactie**

In het antwoord worden de zojuist toegevoegde veldgroepen weergegeven in de array `meta:extends` en wordt een `$ref` weergegeven voor de veldgroep in het kenmerk `allOf` .

Het schema Loyalty-leden moet nu vier `$ref` -waarden in de `allOf` array: `profile` , `profile-person-details` , `profile-personal-details` en `profile-loyalty-details` bevatten, zoals hieronder wordt weergegeven.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.2",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673311559934,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1de5ed1a07e3478719952f0a8c94d5e5390d5a9a998761adb4cf1989137fd6ea",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### Een nieuwe veldgroep definiëren

Hoewel de standaardveldgroep [!UICONTROL Loyalty Details] nuttige aan loyaliteit gerelateerde velden aan het schema biedt, zijn er aanvullende loyaliteitsvelden die niet in standaardveldgroepen zijn opgenomen.

Als u deze velden wilt toevoegen, kunt u uw eigen aangepaste veldgroepen definiëren in de container van `tenant` . Deze veldgroepen zijn uniek voor uw organisatie en zijn niet zichtbaar of bewerkbaar voor iedereen buiten uw organisatie.

Als u een nieuwe veldgroep wilt maken (POSTEN), moet uw aanvraag een `meta:intendedToExtend` -veld bevatten dat de `$id` bevat voor de basisklasse(n) waarmee de veldgroep compatibel is, samen met de eigenschappen die de veldgroep zal bevatten.

Aangepaste eigenschappen moeten onder `TENANT_ID` worden genest om conflicten met andere veldgroepen of velden te voorkomen.

**API formaat**

```http
POST /tenant/fieldgroups
```

**Verzoek**

Met deze aanvraag wordt een nieuwe veldgroep gemaakt die een `loyaltyTier` -object bevat dat vier velden bevat die specifiek zijn voor het specifieke loyaliteitsprogramma van een bedrijf: `id` , `effectiveDate` , `currentThreshold` en `nextThreshold` .

```SHELL
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Tier",
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Captures info about the current loyalty tier of a customer.",
        "definitions": {
          "loyaltyTier": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "loyaltyTier": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "title": "Loyalty Tier Identifier",
                        "type": "string",
                        "description": "Loyalty Tier Identifier."
                      },
                      "effectiveDate": {
                        "title": "Effective Date",
                        "type": "string",
                        "format": "date-time",
                        "description": "Date the member joined their current loyalty tier."
                      },
                      "currentThreshold": {
                        "title": "Current Point Threshold",
                        "type": "integer",
                        "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                      },
                      "nextThreshold": {
                        "title": "Next Point Threshold",
                        "type": "integer",
                        "description": "The number of loyalty points the member must accrue to graduate to the next tier."
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/loyaltyTier"
          }
        ]
      }'
```

**Reactie**

Een geslaagde aanvraag retourneert HTTP Response Status 201 (Gemaakt) met een antwoordinstantie die de details bevat van de nieuwe veldgroep, inclusief de `$id` , `meta:altIt` en `version` . Deze waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry] .

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "type": "object",
              "properties": {
                "id": {
                  "title": "Loyalty Tier Identifier",
                  "type": "string",
                  "description": "Loyalty Tier Identifier.",
                  "meta:xdmType": "string"
                },
                "effectiveDate": {
                  "title": "Effective Date",
                  "type": "string",
                  "format": "date-time",
                  "description": "Date the member joined their current loyalty tier.",
                  "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                  "title": "Current Point Threshold",
                  "type": "integer",
                  "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                  "meta:xdmType": "int"
                },
                "nextThreshold": {
                  "title": "Next Point Threshold",
                  "type": "integer",
                  "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                  "meta:xdmType": "int"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673313004645,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### De aangepaste veldgroep toevoegen aan het schema

U kunt de zelfde stappen voor [ nu volgen toevoegend een standaardgebiedsgroep ](#add-a-field-group) om deze pas gecreëerde gebiedsgroep aan uw schema toe te voegen.

**API formaat**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema. |

**Verzoek**

Dit verzoek werkt (PATCH) het schema van Loyalty Leden bij om de gebieden binnen de nieuwe &quot;Loyalty Rij&quot;gebiedsgroep te omvatten.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"}}
      ]'
```

**Reactie**

U ziet dat de veldgroep is toegevoegd omdat de reactie nu de nieuwe veldgroep in de array `meta:extends` weergeeft en een `$ref` aan de veldgroep in het kenmerk `allOf` bevat.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Het huidige schema weergeven

U kunt nu een verzoek van de GET uitvoeren om het huidige schema te bekijken en te zien hoe de toegevoegde gebiedsgroepen aan de algemene structuur van het schema hebben bijgedragen.

**API formaat**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema. |

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**Reactie**

Door de header `application/vnd.adobe.xed-full+json; version=1` `Accept` te gebruiken, ziet u het volledige schema met alle eigenschappen. Deze eigenschappen zijn de gebieden die door de klasse en de gebiedsgroepen worden bijgedragen die zijn gebruikt om het schema samen te stellen. In het onderstaande voorbeeldantwoord worden alleen de onlangs toegevoegde velden weergegeven voor de ruimte. U kunt het volledige schema, met inbegrip van alle eigenschappen en hun attributen, in [ bijlage ](#appendix) aan het eind van dit document bekijken.

Onder `"properties"` ziet u de naamruimte `_{TENANT_ID}` die is gemaakt toen u de aangepaste veldgroep toevoegde. Binnen die naamruimte bevinden zich het `loyaltyTier` -object en de velden die zijn gedefinieerd toen de veldgroep werd gemaakt.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "type": "object",
              "properties": {
                "id": {
                  "title": "Loyalty Tier Identifier",
                  "type": "string",
                  "description": "Loyalty Tier Identifier.",
                  "meta:xdmType": "string"
                },
                "effectiveDate": {
                  "title": "Effective Date",
                  "type": "string",
                  "format": "date-time",
                  "description": "Date the member joined their current loyalty tier.",
                  "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                  "title": "Current Point Threshold",
                  "type": "integer",
                  "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                  "meta:xdmType": "int"
                },
                "nextThreshold": {
                  "title": "Next Point Threshold",
                  "type": "integer",
                  "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                  "meta:xdmType": "int"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673313004645,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### Een gegevenstype maken

De het gebiedsgroep van de Rij van de Loyalty die u creeerde bevat specifieke eigenschappen die in andere schema&#39;s nuttig zouden kunnen zijn. De gegevens kunnen bijvoorbeeld worden ingevoerd als onderdeel van een ervaringsgebeurtenis of worden gebruikt door een schema dat een andere klasse implementeert. In dit geval is het verstandig de objecthiërarchie op te slaan als een gegevenstype om het hergebruik van de definitie elders te vergemakkelijken.

Met gegevenstypen kunt u één keer een objecthiërarchie definiëren en ernaar verwijzen in een veld, net als bij elk ander scalair type.

Met andere woorden, staan de gegevenstypes voor het verenigbare gebruik van multi-gebiedsstructuren, met meer flexibiliteit dan gebiedsgroepen toe omdat zij overal in een schema kunnen worden omvat door hen als &quot;type&quot;van een gebied toe te voegen.

**API formaat**

```http
POST /tenant/datatypes
```

**Verzoek**

Als u een gegevenstype definieert, hebt u geen velden `meta:extends` of `meta:intendedToExtend` nodig en hoeven de velden niet onder de gebruikers-id te zijn genest om conflicten te voorkomen.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Tier",
        "type": "object",
        "description": "Loyalty Tier data type",
        "definitions": {
          "loyaltyTier": {
            "type": "object",
            "properties": {
              "id": {
                "title": "Loyalty Tier Identifier",
                "type": "string",
                "description": "Loyalty Tier Identifier."
              },
              "effectiveDate": {
                "title": "Effective Date",
                "type": "string",
                "format": "date-time",
                "description": "Date the member joined their current loyalty tier."
              },
              "currentThreshold": {
                "title": "Current Point Threshold",
                "type": "integer",
                "description": "The minimum number of loyalty points the member must maintain to remain in the       current tier."
              },
              "nextThreshold": {
                "title": "Next Point Threshold",
                "type": "integer",
                "description": "The number of loyalty points the member must accrue to graduate to the next tier."
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/loyaltyTier"
          }
        ]
      }'
```

**Reactie**

Een geslaagde aanvraag retourneert HTTP Response Status 201 (Gemaakt) met een antwoordinstantie die de details bevat van het nieuwe gegevenstype, inclusief `$id`, `meta:altIt` en `version` . Deze waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry] .

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
  "meta:altId": "_{TENANT_ID}.datatypes.c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Loyalty Tier data type",
  "definitions": {
    "loyaltyTier": {
      "type": "object",
      "properties": {
        "id": {
          "title": "Loyalty Tier Identifier",
          "type": "string",
          "description": "Loyalty Tier Identifier.",
          "meta:xdmType": "string"
        },
        "effectiveDate": {
          "title": "Effective Date",
          "type": "string",
          "format": "date-time",
          "description": "Date the member joined their current loyalty tier.",
          "meta:xdmType": "date-time"
        },
        "currentThreshold": {
          "title": "Current Point Threshold",
          "type": "integer",
          "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
          "meta:xdmType": "int"
        },
        "nextThreshold": {
          "title": "Next Point Threshold",
          "type": "integer",
          "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
          "meta:xdmType": "int"
        }
      },
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673378256699,
    "repo:lastModifiedDate": 1673378256699,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "8afba84c0c9a68126a7a1389f8523a1112bdf4405badc6dcddbbb4a0e18f5cdb",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

U kunt een opzoekverzoek (GET) uitvoeren met de URL-gecodeerde `$id` URI om het nieuwe gegevenstype rechtstreeks weer te geven. Zorg ervoor dat u de header `version` opneemt in de `Accept` -header voor een opzoekaanvraag.

### Gegevenstype gebruiken in schema

Nu het gegevenstype Loyalty Tier is gemaakt, kunt u het veld `loyaltyTier` in de veldgroep die u hebt gemaakt bijwerken (PATCH) en verwijzen naar het gegevenstype in plaats van de velden die er eerder waren.

**API formaat**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{FIELD_GROUP_ID}` | De `meta:altId` of URL gecodeerd `$id` van de veldgroep die moet worden bijgewerkt. |

**Verzoek**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "replace",
          "path": "/definitions/loyaltyTier/properties/_{TENANT_ID}/properties",
          "value": {
            "loyaltyTier": {
              "title": "Loyalty Tier",
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
              "description": "Loyalty tier info"
            }
          }
        }
      ]'
```

**Reactie**

Het antwoord bevat nu een verwijzing (`$ref`) naar het gegevenstype in het `loyaltyTier` -object in plaats van de velden die eerder waren gedefinieerd.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.1",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "title": "Loyalty Tier",
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
              "description": "Loyalty tier info",
              "type": "object",
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673378970276,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "4df8fa56d00991590364606bb2e219e1ea8f5717a51c0e6ae57ca956830b6a27",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

Als u een GET-verzoek uitvoert om het schema nu op te zoeken, geeft de eigenschap `loyaltyTier` de verwijzing naar het gegevenstype onder `meta:referencedFrom` weer:

```JSON
"_{TENANT_ID}": {
  "type": "object",
  "meta:xdmType": "object",
  "properties": {
    "loyaltyTier": {
      "title": "Loyalty Tier",
      "description": "Loyalty tier info",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "id": {
          "title": "Loyalty Tier Identifier",
          "type": "string",
          "description": "Loyalty Tier Identifier.",
          "meta:xdmType": "string"
        },
        "effectiveDate": {
          "title": "Effective Date",
          "type": "string",
          "format": "date-time",
          "description": "Date the member joined their current loyalty tier.",
          "meta:xdmType": "date-time"
        },
        "currentThreshold": {
          "title": "Current Point Threshold",
          "type": "integer",
          "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
          "meta:xdmType": "int"
        },
        "nextThreshold": {
          "title": "Next Point Threshold",
          "type": "integer",
          "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
          "meta:xdmType": "int"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
    }
  }
}
```

### Een identiteitsdescriptor definiëren

Schema&#39;s worden gebruikt voor het opnemen van gegevens in [!DNL Experience Platform] . Dit gegeven wordt uiteindelijk gebruikt over de veelvoudige diensten om één enkele, verenigde mening van een individu tot stand te brengen. Om dit proces te helpen, kunnen de zeer belangrijke gebieden als &quot;Identiteit&quot;worden gemerkt en, bij gegevensinvoer, worden de gegevens in die gebieden opgenomen in de Grafiek van de Identiteit voor dat individu. De grafiekgegevens kunnen vervolgens worden benaderd door [[!DNL Real-Time Customer Profile]](../../profile/home.md) en andere [!DNL Experience Platform] -services voor een aan elkaar gekoppelde weergave van elke afzonderlijke klant.

Velden die algemeen als &quot;Identiteit&quot;worden gemerkt omvatten: e-mailadres, telefoonaantal, [[!DNL Experience Cloud ID (ECID)] ](https://experienceleague.adobe.com/docs/id-service/using/home.html), identiteitskaart van CRM, of andere unieke gebieden van identiteitskaart Houd rekening met alle unieke id&#39;s die specifiek zijn voor uw organisatie, omdat dit ook goede identiteitsvelden kunnen zijn.

Identiteitsdescriptors geven aan dat de `sourceProperty` van de `sourceSchema` een unieke id is die als een identiteit moet worden beschouwd.

Voor meer informatie bij het werken met beschrijvers, zie de [ de ontwikkelaarsgids van de Registratie van het Schema ](../api/getting-started.md).

**API formaat**

```http
POST /tenant/descriptors
```

**Verzoek**

In het volgende verzoek wordt een identiteitsbeschrijving gedefinieerd in het veld `personalEmail.address` voor het schema Loyalty-leden. Dit vertelt [!DNL Experience Platform] om het e-mailadres van het loyaliteitslid als herkenningsteken te gebruiken helpen informatie over het individu verenigen. Deze vraag plaatst ook dit gebied als primaire identiteit voor het schema door `xdm:isPrimary` aan `true` te plaatsen, dat een vereiste voor [ toelatend het schema voor gebruik in het Profiel van de Klant in real time ](#profile) is.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

>[!NOTE]
>
>U kunt beschikbare &quot;xdm:namespace&quot;waarden een lijst maken, of nieuwe degenen creëren, gebruikend [[!DNL Identity Service API] ](https://www.adobe.io/experience-platform-apis/references/identity-service). De waarde voor &quot;xdm:property&quot; kan &quot;xdm:code&quot; of &quot;xdm:id&quot; zijn, afhankelijk van de gebruikte &quot;xdm:namespace&quot;.

**Reactie**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) met een antwoordinstantie die de details bevat van de zojuist gemaakte descriptor, inclusief de `@id` . `@id` is een alleen-lezen veld dat door [!DNL Schema Registry] is toegewezen en wordt gebruikt voor het verwijzen naar de descriptor in de API.

```JSON
{
  "@id": "719a4391897c097786efbaa6d4262bb928a1cd88540344c6",
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "imsOrg": "{ORG_ID}",
  "version": "1",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": true,
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production"
}
```

## Schema inschakelen voor gebruik in [!DNL Real-Time Customer Profile] {#profile}

Wanneer op het schema een primaire identiteitsbeschrijving is toegepast, kunt u het schema Loyalty-leden voor gebruik door [!DNL Real-Time Customer Profile] inschakelen door een `union` -tag toe te voegen aan het `meta:immutableTags` -kenmerk.

>[!NOTE]
>
>Voor meer informatie bij het werken met vakbondsmeningen, zie de sectie over [ vakbonden ](../api/unions.md) in de [!DNL Schema Registry] ontwikkelaarsgids.

### Een tag `union` toevoegen

Als u een schema wilt opnemen in de verenigingsweergave, moet de tag `union` worden toegevoegd aan het kenmerk `meta:immutableTags` van het schema. Dit gebeurt aan de hand van een PATCH-aanvraag om het schema bij te werken en een `meta:immutableTags` -array met de waarde `union` toe te voegen.

**API formaat**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema dat u inschakelt voor Profiel. |

**Verzoek**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Reactie**

De reactie toont aan dat de bewerking is uitgevoerd en het schema bevat nu een kenmerk op hoofdniveau, `meta:immutableTags` , dat een array is met de waarde &#39;union&#39;.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.4",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673380280074,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:immutableTags": [
    "union"
  ],
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### Schema&#39;s weergeven in een union

Het schema is nu toegevoegd aan de samenvoeging van [!DNL XDM Individual Profile] . Om een lijst van alle schema&#39;s te zien die een deel van de zelfde unie zijn, kunt u een verzoek uitvoeren van de GET gebruikend vraagparameters om de reactie te filtreren.

Met de query-parameter `property` kunt u opgeven dat alleen schema&#39;s worden geretourneerd die een `meta:immutableTags` -veld bevatten met een `meta:class` -waarde die gelijk is aan `$id` van de [!DNL XDM Individual Profile] -klasse.

**API Formaat**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

**Verzoek**

In het onderstaande voorbeeld worden alle schema&#39;s geretourneerd die deel uitmaken van de [!DNL XDM Individual Profile] union.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Het antwoord is een gefilterde lijst van schema&#39;s die alleen schema&#39;s bevatten die aan beide eisen voldoen. Herinner dat wanneer het gebruiken van veelvoudige vraagparameters, EN verhouding wordt verondersteld. De indeling van het antwoord op de lijst is afhankelijk van de `Accept` -header die in de aanvraag wordt verzonden.

```JSON
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d29a200b5deb6cfb55d3b865ef627f33",
      "meta:altId": "_{TENANT_ID}.schemas.d29a200b5deb6cfb55d3b865ef627f33",
      "version": "1.2",
      "title": "Profile Schema"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/5d70026f5522fc60b3c81f6523b83c86",
      "meta:altId": "_{TENANT_ID}.schemas.5d70026f5522fc60b3c81f6523b83c86",
      "version": "1.3",
      "title": "CRM Onboarding"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
      "meta:altId": "_{TENANT_ID}.schemas.653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
      "version": "1.1",
      "title": "Profile consents"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
      "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
      "version": "1.4",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
    "orderby": "updated",
    "next": null,
    "count": 4
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
    }
  }
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een schema samengesteld met gebruik van zowel standaardveldgroepen als een veldgroep die u hebt gedefinieerd. U kunt dit schema nu gebruiken om een dataset tot stand te brengen en recordgegevens in Adobe Experience Platform in te voeren.

Het volledige schema van de Leden van de Loyalty, zoals die door dit leerprogramma wordt gecreeerd, is beschikbaar in het bijlage dat volgt. Als u het schema bekijkt, kunt u zien hoe de veldgroepen bijdragen aan de algemene structuur en welke velden beschikbaar zijn voor gegevensinvoer.

Zodra u meer dan één schema hebt gecreeerd, kunt u verhoudingen tussen hen door het gebruik van relatiebeschrijvers bepalen. Zie het leerprogramma voor [ bepalend een verband tussen twee schema&#39;s ](relationship-api.md) voor meer informatie. Voor gedetailleerde voorbeelden van hoe te om alle verrichtingen (GET, POST, PUT, PATCH, en DELETE) in de registratie uit te voeren, gelieve te verwijzen naar de [ de ontwikkelaarsgids van de Registratie van het Schema ](../api/getting-started.md) terwijl het werken met API.

## Bijlage {#appendix}

De volgende informatie vormt een aanvulling op de API-zelfstudie.

## Volledig schema voor leden van Loyalty {#complete-schema}

Door dit leerprogramma, wordt een schema samengesteld om de leden van een programma van de kleinhandelsloyaliteit te beschrijven.

Het schema implementeert de klasse [!DNL XDM Individual Profile] en combineert meerdere veldgroepen. Deze legt informatie over de loyaliteitsleden vast met behulp van de standaardveldgroepen [!DNL Demographic Details] , [!UICONTROL Personal Contact Details] en [!UICONTROL Loyalty Details] , alsmede via een aangepaste geldigheidslandgroep die tijdens de zelfstudie is gedefinieerd.

In het volgende voorbeeld ziet u het voltooide schema Loyalty-leden in JSON-indeling:

+++Volledig schema weergeven

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.4",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyTier": {
          "title": "Loyalty Tier",
          "description": "Loyalty tier info",
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "id": {
              "title": "Loyalty Tier Identifier",
              "type": "string",
              "description": "Loyalty Tier Identifier.",
              "meta:xdmType": "string"
            },
            "effectiveDate": {
              "title": "Effective Date",
              "type": "string",
              "format": "date-time",
              "description": "Date the member joined their current loyalty tier.",
              "meta:xdmType": "date-time"
            },
            "currentThreshold": {
              "title": "Current Point Threshold",
              "type": "integer",
              "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
              "meta:xdmType": "int"
            },
            "nextThreshold": {
              "title": "Next Point Threshold",
              "type": "integer",
              "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
              "meta:xdmType": "int"
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
        }
      },
      "meta:xdmType": "object"
    },
    "_id": {
      "title": "Identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "A unique identifier for the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "@id"
    },
    "_repo": {
      "properties": {
        "createDate": {
          "type": "string",
          "format": "date-time",
          "meta:immutable": true,
          "meta:usereditable": false,
          "examples": [
            "2004-10-23T12:00:00-06:00"
          ],
          "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
          "meta:xdmType": "date-time",
          "meta:xdmField": "repo:createDate"
        },
        "modifyDate": {
          "type": "string",
          "format": "date-time",
          "meta:usereditable": false,
          "examples": [
            "2004-10-23T12:00:00-06:00"
          ],
          "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
          "meta:xdmType": "date-time",
          "meta:xdmField": "repo:modifyDate"
        }
      },
      "type": "object",
      "meta:xdmType": "object",
      "meta:xedConverted": true
    },
    "billingAddress": {
      "title": "Billing Address",
      "description": "Billing postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:billingAddress"
    },
    "createdByBatchID": {
      "title": "Created by batch identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "The dataset files in Catalog which has been originating the creation of the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:createdByBatchID"
    },
    "faxPhone": {
      "title": "Fax Phone",
      "description": "Fax phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the phone number.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:faxPhone"
    },
    "homeAddress": {
      "title": "Home Address",
      "description": "A home postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:homeAddress"
    },
    "homePhone": {
      "title": "Home Phone",
      "description": "Home phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the phone number.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:homePhone"
    },
    "loyalty": {
      "type": "object",
      "description": "Captures details related to the customer's loyalty rewards.",
      "properties": {
        "joinDate": {
          "title": "Program Join Date",
          "type": "string",
          "format": "date-time",
          "description": "Date which the visitor registered for the loyalty program.",
          "meta:xdmType": "date-time",
          "meta:xdmField": "xdm:joinDate"
        },
        "loyaltyID": {
          "title": "Program ID",
          "type": "array",
          "items": {
            "type": "string",
            "meta:xdmType": "string"
          },
          "description": "The loyalty program ID(s) associated with a specific user, if they are enrolled in the client's loyalty program.",
          "meta:xdmType": "array",
          "meta:xdmField": "xdm:loyaltyID"
        },
        "points": {
          "title": "Program Points Balance",
          "type": "number",
          "description": "Current balance of the loyalty points/awards in a visitor's loyalty account.",
          "meta:xdmType": "number",
          "meta:xdmField": "xdm:points"
        },
        "pointsExpiration": {
          "title": "Points Expiration",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "pointsExpirationDate": {
                "type": "string",
                "format": "date-time",
                "description": "Date on which the given portion of the loyalty points expire.",
                "meta:xdmType": "date-time",
                "meta:xdmField": "xdm:pointsExpirationDate"
              },
              "pointsExpiring": {
                "title": "Points Expiring",
                "type": "number",
                "description": "Point balance expiring as of the associated expiration date.",
                "meta:xdmType": "number",
                "meta:xdmField": "xdm:pointsExpiring"
              }
            },
            "meta:xdmType": "object"
          },
          "meta:xdmType": "array",
          "meta:xdmField": "xdm:pointsExpiration"
        },
        "pointsRedeemed": {
          "title": "Points Redeemed",
          "type": "number",
          "description": "Amount of points applied toward a purchase or otherwise redeemed.",
          "meta:xdmType": "number",
          "meta:xdmField": "xdm:pointsRedeemed"
        },
        "program": {
          "title": "Program Name",
          "type": "string",
          "description": "This should define the loyalty progam in which a visitor is enrolled.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:program"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "Captures the visitor's loyalty progam status, such as active, disabled, or suspended.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "tier": {
          "title": "Tier",
          "type": "string",
          "description": "Captures the loyalty progam tier in which a visitor is enrolled.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:tier"
        },
        "upgradeDate": {
          "title": "Program Name",
          "type": "string",
          "description": "Date which the customer was upgraded to the next tier level.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:upgradeDate"
        }
      },
      "meta:xdmType": "object",
      "meta:xdmField": "xdm:loyalty"
    },
    "mailingAddress": {
      "title": "Mailing Address",
      "description": "Mailing postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:mailingAddress"
    },
    "mobilePhone": {
      "title": "Mobile Phone",
      "description": "Mobile phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the phone number.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:mobilePhone"
    },
    "modifiedByBatchID": {
      "title": "Modified by batch identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:modifiedByBatchID"
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "birthDate": {
          "title": "Birth date(YYYY-MM-DD)",
          "type": "string",
          "format": "date",
          "description": "The full date a person was born.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:birthDate"
        },
        "birthDayAndMonth": {
          "title": "Birth date (MM-DD)",
          "type": "string",
          "pattern": "[0-1][0-9]-[0-9][0-9]",
          "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:birthDayAndMonth"
        },
        "birthYear": {
          "title": "Birth year",
          "type": "integer",
          "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date.",
          "minimum": 1,
          "maximum": 32767,
          "meta:xdmType": "short",
          "meta:xdmField": "xdm:birthYear"
        },
        "gender": {
          "title": "Gender",
          "type": "string",
          "enum": [
            "male",
            "female",
            "not_specified",
            "non_specific"
          ],
          "meta:enum": {
            "male": "Male",
            "female": "Female",
            "not_specified": "Not Specified",
            "non_specific": "Non-specific"
          },
          "description": "Gender identity of the person.\n",
          "default": "not_specified",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:gender"
        },
        "maritalStatus": {
          "title": "Marital Status",
          "type": "string",
          "enum": [
            "married",
            "single",
            "divorced",
            "widowed",
            "not_specified"
          ],
          "meta:enum": {
            "married": "Married",
            "single": "Single",
            "divorced": "Divorced",
            "widowed": "Widowed",
            "not_specified": "Not Specified"
          },
          "description": "Describes a person's relationship with a significant other.",
          "default": "not_specified",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:maritalStatus"
        },
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "courtesyTitle": {
              "title": "Courtesy title",
              "type": "string",
              "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:courtesyTitle"
            },
            "firstName": {
              "title": "First name",
              "type": "string",
              "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:firstName"
            },
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:fullName"
            },
            "lastName": {
              "title": "Last name",
              "type": "string",
              "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:lastName"
            },
            "middleName": {
              "title": "Middle name",
              "type": "string",
              "description": "Middle, alternative, or additional names supplied between the first name and last name.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:middleName"
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:suffix"
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        },
        "nationality": {
          "title": "Nationality",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:nationality"
        },
        "taxId": {
          "title": "Tax ID",
          "type": "string",
          "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
          "meta:status": "deprecated",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:taxId"
        },
        "type": {
          "title": "Type",
          "type": "string",
          "description": "The type of individual in different business contexts like B2C.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:type"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
      "meta:xdmField": "xdm:person"
    },
    "personID": {
      "title": "Person ID",
      "description": "Unique identifier of Person/Profile fragment.",
      "type": "string",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:personID"
    },
    "personalEmail": {
      "title": "Personal Email",
      "description": "A personal email address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "address": {
          "title": "Address",
          "type": "string",
          "format": "email",
          "description": "The technical address, for example, 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:address",
          "minLength": 1
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Additional display information that maybe available, for example, Microsoft Outlook rich address controls display 'John Smith smithjr@company.uk', 'John Smith' part is data that would be placed in the label.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary email indicator. A profile can have only one `primary` email address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the email address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "type": {
          "title": "Type",
          "type": "string",
          "description": "The way the account relates to the person for example 'work' or 'personal'.",
          "meta:enum": {
            "unknown": "Unknown",
            "personal": "Personal",
            "work": "Work",
            "education": "Education"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:type"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
      "meta:xdmField": "xdm:personalEmail",
      "required": [
        "address"
      ]
    },
    "repositoryCreatedBy": {
      "title": "Created by user identifier",
      "type": "string",
      "description": "User ID of who created the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:repositoryCreatedBy"
    },
    "repositoryLastModifiedBy": {
      "title": "Modified by user identifier",
      "type": "string",
      "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:repositoryLastModifiedBy"
    },
    "shippingAddress": {
      "title": "Shipping Address",
      "description": "Shipping postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:shippingAddress"
    }
  },
  "required": [
    "personalEmail"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673380280074,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:immutableTags": [
    "union"
  ],
  "meta:allFieldAccess": true
}
```

+++
