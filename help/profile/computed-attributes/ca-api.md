---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Computed Attributes API Endpoint
topic: hulplijn
type: Documentatie
description: In Adobe Experience Platform zijn berekende kenmerken functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt. Deze handleiding laat zien hoe u berekende kenmerken kunt maken, weergeven, bijwerken en verwijderen met de realtime-API voor klantprofiel.
translation-type: tm+mt
source-git-commit: 6ae96ab25bd7992fe93d15bfc16b58a2fe7b4b7c
workflow-type: tm+mt
source-wordcount: '2279'
ht-degree: 0%

---


# (Alpha) Berekende attributen API eindpunt

>[!IMPORTANT]
>
>De berekende kenmerkfunctionaliteit die in dit document wordt beschreven, bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt. Deze handleiding bevat voorbeeld-API-aanroepen voor het uitvoeren van standaard-CRUD-bewerkingen met behulp van het `/computedAttributes`-eindpunt.

Als u meer wilt weten over berekende kenmerken, leest u eerst [berekende kenmerken overzicht](overview.md).

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van [Real-time het Profiel van de Klant API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Voordat u verdergaat, bekijkt u eerst de [Aan de slag-handleiding voor profiel-API](../api/getting-started.md) voor koppelingen naar aanbevolen documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen die in dit document worden weergegeven en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een Experience Platform-API met succes uit te voeren.

## Veld voor berekende kenmerken configureren

Om een gegevens verwerkt attribuut tot stand te brengen, moet u eerst het gebied in een schema identificeren dat de gegevens verwerkte attributenwaarde zal houden.

Raadpleeg de documentatie bij [het configureren van een berekend kenmerk](configure-api.md) voor een complete end-to-end handleiding voor het maken van een berekend kenmerkveld in een schema.

>[!WARNING]
>
>Als u wilt doorgaan met de API-handleiding, moet een veld voor berekende kenmerken zijn geconfigureerd.

## Een berekend kenmerk maken {#create-a-computed-attribute}

Als het berekende kenmerkveld is gedefinieerd in het schema voor het inschakelen van het profiel, kunt u nu een berekend kenmerk configureren. Als u dit nog niet hebt gedaan, volgt u de workflow die wordt beschreven in de [documentatie voor het configureren van een berekend kenmerk](configure-api.md).

Om een gegevens verwerkt attribuut tot stand te brengen, begin door een verzoek van de POST aan het `/config/computedAttributes` eindpunt met een verzoeklichaam te doen dat de details van de gegevens verwerkte attributen bevat die u wenst om tot stand te brengen.

**API-indeling**

```http
POST /config/computedAttributes
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `name` | De naam van het berekende kenmerkveld, als een tekenreeks. |
| `path` | Het pad naar het veld met het berekende kenmerk. Dit pad wordt gevonden in het `properties`-kenmerk van het schema en mag NIET de veldnaam in het pad opnemen. Laat bij het schrijven van het pad de verschillende niveaus van `properties`-kenmerken weg. |
| `{TENANT_ID}` | Als u niet vertrouwd met uw huurdersidentiteitskaart bent, gelieve te verwijzen naar de stappen voor het vinden van uw huurdersidentiteitskaart in [de ontwikkelaarsgids van de Registratie van het Schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Een beschrijving van het berekende kenmerk. Dit is vooral handig als er meerdere berekende kenmerken zijn gedefinieerd, omdat hierdoor anderen binnen uw IMS-organisatie kunnen bepalen welk kenmerk correct moet worden berekend. |
| `expression.value` | Een geldige [!DNL Profile Query Language] (PQL)-expressie. De berekende kenmerken ondersteunen momenteel de volgende functies: som, aantal, min, max en boolean. Raadpleeg de documentatie [voorbeeld van PQL-expressies](expressions.md) voor een lijst met voorbeeldexpressies. |
| `schema.name` | De klasse waarop het schema met het berekende kenmerkveld is gebaseerd. Voorbeeld: `_xdm.context.experienceevent` voor een schema dat op de klasse XDM ExperienceEvent wordt gebaseerd. |

**Antwoord**

Een met succes gecreeerd gegevens verwerkt attribuut keert de Status 200 van HTTP (O.K.) en een reactielichaam terug die de details van het onlangs gecreeerde gegevens verwerkte attribuut bevatten. Deze details omvatten een uniek, read-only, systeem-geproduceerd `id` die voor het van verwijzingen voorzien van het gegevens verwerkte attribuut tijdens andere API verrichtingen kunnen worden gebruikt.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Eigenschap | Beschrijving |
|---|---|
| `id` | Een unieke, alleen-lezen, door het systeem gegenereerde id die kan worden gebruikt voor het verwijzen naar het berekende kenmerk tijdens andere API-bewerkingen. |
| `imsOrgId` | De IMS-organisatie die betrekking heeft op het berekende kenmerk, moet overeenkomen met de waarde die in de aanvraag is verzonden. |
| `sandbox` | Het sandboxobject bevat details van de sandbox waarin het berekende kenmerk is geconfigureerd. Deze informatie wordt getekend vanuit de sandboxheader die in de aanvraag wordt verzonden. Zie het [sandboxoverzicht](../../sandboxes/home.md) voor meer informatie. |
| `positionPath` | Een array met de gedeconstrueerde `path` naar het veld dat in de aanvraag is verzonden. |
| `returnSchema.meta:xdmType` | Het type veld waarin het berekende kenmerk wordt opgeslagen. |
| `definedOn` | Een array die de samenvoegingsschema&#39;s weergeeft waarop het berekende kenmerk is gedefinieerd. Bevat één object per samenvoegingsschema. Dit houdt in dat er meerdere objecten in de array kunnen zijn als het berekende kenmerk aan meerdere schema&#39;s is toegevoegd op basis van verschillende klassen. |
| `active` | Een booleaanse waarde die weergeeft of het berekende kenmerk actief is of niet. De standaardwaarde is `true`. |
| `type` | Het type van gecreeerde bron, in dit geval &quot;ComputedAttribute&quot;is de standaardwaarde. |
| `createEpoch` en `updateEpoch` | De tijd waarop het berekende attribuut werd gecreeerd en het laatst bijgewerkt, respectievelijk. |

## Een berekend kenmerk maken dat verwijst naar bestaande berekende kenmerken

Het is ook mogelijk om een berekend attribuut tot stand te brengen dat verwijzingen bestaande gegevens verwerkte attributen. Om dit te doen, begin door een verzoek van de POST aan het `/config/computedAttributes` eindpunt te doen. De aanvraaginstantie zal verwijzingen naar de gegevens verwerkte attributen in het `expression.value` gebied zoals aangetoond in het volgende voorbeeld bevatten.

**API-indeling**

```http
POST /config/computedAttributes
```

**Verzoek**

In dit voorbeeld zijn al twee berekende kenmerken gemaakt en worden deze gebruikt om een derde te definiëren. De bestaande berekende kenmerken zijn:

* **`totalSpend`:** Vangt het totale dollarbedrag dat een klant heeft uitgegeven.
* **`countPurchases`:** Telt het aantal aankopen dat een klant heeft gedaan.

De onderstaande aanvraag verwijst naar de twee bestaande berekende kenmerken, waarbij een geldige PQL wordt gebruikt om te delen om het nieuwe `averageSpend` berekende kenmerk te berekenen.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "averageSpend",
        "path" : "_{TENANT_ID}.purchaseSummary",
        "description" : "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `name` | De naam van het berekende kenmerkveld, als een tekenreeks. |
| `path` | Het pad naar het veld met het berekende kenmerk. Dit pad wordt gevonden in het `properties`-kenmerk van het schema en mag NIET de veldnaam in het pad opnemen. Laat bij het schrijven van het pad de verschillende niveaus van `properties`-kenmerken weg. |
| `{TENANT_ID}` | Als u niet vertrouwd met uw huurdersidentiteitskaart bent, gelieve te verwijzen naar de stappen voor het vinden van uw huurdersidentiteitskaart in [de ontwikkelaarsgids van de Registratie van het Schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Een beschrijving van het berekende kenmerk. Dit is vooral handig als er meerdere berekende kenmerken zijn gedefinieerd, omdat hierdoor anderen binnen uw IMS-organisatie kunnen bepalen welk kenmerk correct moet worden berekend. |
| `expression.value` | Een geldige PQL-expressie. De berekende kenmerken ondersteunen momenteel de volgende functies: som, aantal, min, max en boolean. Raadpleeg de documentatie [voorbeeld van PQL-expressies](expressions.md) voor een lijst met voorbeeldexpressies.<br/><br/>In dit voorbeeld verwijst de expressie naar twee bestaande berekende kenmerken. Naar de kenmerken wordt verwezen met behulp van `path` en `name` van het berekende kenmerk zoals deze worden weergegeven in het schema waarin de berekende kenmerken zijn gedefinieerd. Het `path` van het eerste berekende kenmerk waarnaar wordt verwezen, is bijvoorbeeld `_{TENANT_ID}.purchaseSummary` en het `name` is `totalSpend`. |
| `schema.name` | De klasse waarop het schema met het berekende kenmerkveld is gebaseerd. Voorbeeld: `_xdm.context.experienceevent` voor een schema dat op de klasse XDM ExperienceEvent wordt gebaseerd. |

**Antwoord**

Een met succes gecreeerd gegevens verwerkt attribuut keert de Status 200 van HTTP (O.K.) en een reactielichaam terug die de details van het onlangs gecreeerde gegevens verwerkte attribuut bevatten. Deze details omvatten een uniek, read-only, systeem-geproduceerd `id` die voor het van verwijzingen voorzien van het gegevens verwerkte attribuut tijdens andere API verrichtingen kunnen worden gebruikt.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
      },
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| Eigenschap | Beschrijving |
|---|---|
| `id` | Een unieke, alleen-lezen, door het systeem gegenereerde id die kan worden gebruikt voor het verwijzen naar het berekende kenmerk tijdens andere API-bewerkingen. |
| `imsOrgId` | De IMS-organisatie die betrekking heeft op het berekende kenmerk, moet overeenkomen met de waarde die in de aanvraag is verzonden. |
| `sandbox` | Het sandboxobject bevat details van de sandbox waarin het berekende kenmerk is geconfigureerd. Deze informatie wordt getekend vanuit de sandboxheader die in de aanvraag wordt verzonden. Zie het [sandboxoverzicht](../../sandboxes/home.md) voor meer informatie. |
| `positionPath` | Een array met de gedeconstrueerde `path` naar het veld dat in de aanvraag is verzonden. |
| `returnSchema.meta:xdmType` | Het type veld waarin het berekende kenmerk wordt opgeslagen. |
| `definedOn` | Een array die de samenvoegingsschema&#39;s weergeeft waarop het berekende kenmerk is gedefinieerd. Bevat één object per samenvoegingsschema. Dit houdt in dat er meerdere objecten in de array kunnen zijn als het berekende kenmerk aan meerdere schema&#39;s is toegevoegd op basis van verschillende klassen. |
| `active` | Een booleaanse waarde die weergeeft of het berekende kenmerk actief is of niet. De standaardwaarde is `true`. |
| `type` | Het type van gecreeerde bron, in dit geval &quot;ComputedAttribute&quot;is de standaardwaarde. |
| `createEpoch` en `updateEpoch` | De tijd waarop het berekende attribuut werd gecreeerd en het laatst bijgewerkt, respectievelijk. |

## Toegang krijgen tot berekende kenmerken

Wanneer u werkt met berekende kenmerken met behulp van de API, hebt u twee opties voor toegang tot berekende kenmerken die door uw organisatie zijn gedefinieerd. Ten eerste moeten alle berekende kenmerken worden vermeld. Ten tweede moet een specifiek berekend kenmerk worden weergegeven op basis van het unieke `id`.

De stappen voor beide toegangspatronen worden beschreven in dit document. Selecteer een van de volgende opties om te beginnen:

* **[Alle bestaande berekende kenmerken](#list-all-computed-attributes) weergeven:** retourneren een lijst met alle bestaande berekende kenmerken die uw organisatie heeft gemaakt.
* **[Bekijk een specifiek gegevens verwerkt attribuut](#view-a-computed-attribute):** keer de details van één enkel gegevens verwerkt attribuut door zijn identiteitskaart tijdens het verzoek te specificeren.

### Alle berekende kenmerken {#list-all-computed-attributes} weergeven

Uw IMS Organisatie kan veelvoudige gegevens verwerkte attributen tot stand brengen, en het uitvoeren van een verzoek van de GET aan het `/config/computedAttributes` eindpunt staat u toe om van alle bestaande gegevens verwerkte attributen voor uw organisatie een lijst te maken.

**API-indeling**

```http
GET /config/computedAttributes
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvol antwoord omvat een `_page` attribuut dat het totale aantal gegevens verwerkte attributen (`totalCount`) en het aantal gegevens verwerkte attributen op de pagina (`pageSize`) verstrekt.

De reactie bevat ook een `children`-array die bestaat uit een of meer objecten, die elk de details van één berekend kenmerk bevatten. Als uw organisatie geen berekende kenmerken heeft, zijn `totalCount` en `pageSize` 0 (nul) en is `children` array leeg.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Eigenschap | Beschrijving |
|---|---|
| `_page.totalCount` | Het totale aantal berekende kenmerken dat door uw IMS-organisatie is gedefinieerd. |
| `_page.pageSize` | Het aantal berekende kenmerken dat op deze resultatenpagina wordt geretourneerd. Als `pageSize` gelijk is aan `totalCount`, betekent dit dat er slechts één pagina met resultaten is en alle berekende kenmerken zijn geretourneerd. Als deze niet gelijk zijn, zijn er extra pagina&#39;s met resultaten die kunnen worden geopend. Zie `_links.next` voor meer informatie. |
| `children` | Een array die bestaat uit een of meer objecten, die elk de details van één berekend kenmerk bevatten. Als er geen berekende kenmerken zijn gedefinieerd, is de `children`-array leeg. |
| `id` | Een unieke, alleen-lezen, door het systeem gegenereerde waarde die automatisch wordt toegewezen aan een berekend kenmerk wanneer dit wordt gemaakt. Voor meer informatie over de componenten van een gegevens verwerkt attribuut voorwerp, te zien gelieve de sectie over [het creëren van een gegevens verwerkt attribuut](#create-a-computed-attribute) vroeger in deze zelfstudie. |
| `_links.next` | Als één pagina met berekende kenmerken wordt geretourneerd, is `_links.next` een leeg object, zoals in de voorbeeldreactie hierboven wordt getoond. Als uw organisatie veel berekende kenmerken heeft, worden deze geretourneerd op meerdere pagina&#39;s die u kunt openen door een GET-aanvraag in te dienen bij de waarde `_links.next`. |

### Een berekend kenmerk {#view-a-computed-attribute} weergeven

U kunt een specifiek gegevens verwerkt attribuut bekijken door een verzoek van de GET aan het `/config/computedAttributes` eindpunt en met inbegrip van gegevens verwerkte kenmerkidentiteitskaart in de verzoekweg te richten.

**API-indeling**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{ATTRIBUTE_ID}` | De id van het berekende kenmerk dat u wilt weergeven. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Een berekend kenmerk bijwerken

Mocht u vinden dat u een bestaand gegevens verwerkt attribuut moet bijwerken, kan dit worden gedaan door een verzoek van PATCH aan het `/config/computedAttributes` eindpunt en met inbegrip van identiteitskaart van berekende toegeschreven die u in de verzoekweg wenst bij te werken.

**API-indeling**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{ATTRIBUTE_ID}` | De id van het berekende kenmerk dat u wilt bijwerken. |

**Verzoek**

In dit verzoek wordt [JSON-patchopmaak](http://jsonpatch.com/) gebruikt om de &quot;waarde&quot; van het veld &quot;expression&quot; bij te werken.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Eigenschap | Beschrijving |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Een geldige [!DNL Profile Query Language] (PQL)-expressie. De berekende kenmerken ondersteunen momenteel de volgende functies: som, aantal, min, max en boolean. Raadpleeg de documentatie [voorbeeld van PQL-expressies](expressions.md) voor een lijst met voorbeeldexpressies. |

**Antwoord**

Een geslaagde update retourneert HTTP Status 204 (Geen inhoud) en een lege antwoordinstantie. Als u wilt bevestigen dat de update succesvol was, kunt u een verzoek van de GET uitvoeren om het gegevens verwerkte attribuut door zijn identiteitskaart te bekijken.

## Een berekend kenmerk verwijderen

Het is ook mogelijk om een berekend attribuut te schrappen gebruikend API. Dit wordt gedaan door een verzoek van DELETE aan het `/config/computedAttributes` eindpunt en met inbegrip van identiteitskaart van de gegevens verwerkte attributen te doen die u wenst om in de verzoekweg te schrappen.

>[!NOTE]
>
>Wees voorzichtig bij het verwijderen van een kenmerk dat u hebt berekend, omdat het in meerdere schema&#39;s wordt gebruikt en de bewerking DELETE niet ongedaan kan worden gemaakt.

**API-indeling**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{ATTRIBUTE_ID}` | De id van het berekende kenmerk dat u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Antwoord**

Een succesvol verwijderingsverzoek retourneert HTTP Status 200 (OK) en een lege antwoordinstantie. Om de schrapping te bevestigen succesvol was, kunt u een verzoek van de GET om het gegevens verwerkte attribuut door zijn identiteitskaart uit te voeren. Als het kenmerk is verwijderd, ontvangt u een HTTP Status 404 (Not Found)-fout.

## Een segmentdefinitie maken die verwijst naar een berekend kenmerk

Met Adobe Experience Platform kunt u segmenten maken die een groep specifieke kenmerken of gedragingen definiëren op basis van een groep profielen. Een segmentdefinitie omvat een uitdrukking die een vraag inkapselt die in PQL wordt geschreven. Deze expressies kunnen ook verwijzen naar berekende kenmerken.

In het volgende voorbeeld wordt een segmentdefinitie gemaakt die verwijst naar een bestaand berekend kenmerk. Meer over segmentdefinities, en hoe te om met hen in de Dienst API van de Segmentatie te werken, gelieve te verwijzen naar [segment definities API eindpuntgids](../../segmentation/api/segment-definitions.md).

Om te beginnen, doe een verzoek van de POST aan het `/segment/definitions` eindpunt, verstrekkend de gegevens verwerkte attributen in het verzoeklichaam.

**API-indeling**

```http
POST /segment/definitions
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | Een unieke naam voor het segment, als een tekenreeks. |
| `description` | Een door de mens leesbare beschrijving van de definitie. |
| `schema.name` | Het schema dat is gekoppeld aan de entiteiten in het segment. Bestaat uit een veld `id` of `name`. |
| `expression` | Een object dat velden bevat met informatie over de segmentdefinitie. |
| `expression.type` | Geeft het expressietype aan. Momenteel wordt alleen &quot;PQL&quot; ondersteund. |
| `expression.format` | Geeft de structuur van de expressie in waarde aan. Momenteel wordt alleen `pql/text` ondersteund. |
| `expression.value` | Een geldige PQL-expressie, in dit voorbeeld bevat deze een verwijzing naar een bestaand berekend kenmerk. |

Voor meer informatie over de attributen van de schemadefinitie, gelieve te verwijzen naar de voorbeelden die in [segment definities API eindpuntgids worden verstrekt](../../segmentation/api/segment-definitions.md).

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde segmentdefinitie terug. Meer over de voorwerpen van de de reactie van de segmentdefinitie, verwijs naar [segment definities API eindpuntgids](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## Volgende stappen

Nu u de grondbeginselen van berekende attributen hebt geleerd, bent u klaar om te beginnen bepalend hen voor uw organisatie.