---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Marketingacties
topic: developer guide
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---


# Marketingacties

Een marketingactie in het kader van het beheer van de gegevens van Adobe Experience Platforms is een actie die een [!DNL Experience Platform] gegevensconsument onderneemt en waarvoor moet worden gecontroleerd op schendingen van het beleid inzake gegevensgebruik.

Als u werkt met marketingacties in de API, moet u het `/marketingActions` eindpunt gebruiken.

## Alle marketingacties weergeven

Om een lijst van alle marketing acties te bekijken, kan een GET verzoek worden gemaakt aan `/marketingActions/core` of `/marketingActions/custom` dat alle beleid voor de gespecificeerde container terugkeert.

**API-indeling**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Verzoek**

Het volgende verzoek retourneert een lijst met alle aangepaste marketingacties die door de IMS-organisatie zijn gedefinieerd.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Het reactieobject geeft het totale aantal marketingacties in de container (`count`) op en de `children` array bevat de details voor elke marketingactie, inclusief de `name` en een `href` voor de marketingactie. Dit pad (`_links.self.href`) wordt gebruikt om de `marketingActionsRefs` array te voltooien bij het [maken van een gegevensgebruiksbeleid](policies.md#create-policy).

```JSON
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

## Een specifieke marketingactie opzoeken

U kunt ook een opzoekverzoek (GET) uitvoeren om de details van een specifieke marketingactie te bekijken. Dit gebeurt met behulp `name` van de marketingactie. Als de naam onbekend is, kan deze worden gevonden met de bovenstaande aanvraag voor de aanbieding (GET).

**API-indeling**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Het reactieobject bevat de details voor de marketingactie, inclusief het pad (`_links.self.href`) dat nodig is om naar de marketingactie te verwijzen bij het definiëren van een beleid voor gegevensgebruik (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## Een marketingactie maken of bijwerken

Met de [!DNL Policy Service] API kunt u uw eigen marketingacties definiëren en bestaande acties bijwerken. Het creëren en het bijwerken allebei worden gedaan gebruikend een verrichting van de ZET aan de naam van de marketing actie.

**API-indeling**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**Verzoek**

In het verzoek dat volgt, merk op dat `name` in de verzoeklading het zelfde als `{marketingActionName}` in de API vraag is. In tegenstelling tot het `id` van een beleid dat read-only en systeem-geproduceerd is, vereist het creëren van een marketing actie u om de _voorgenomen_ naam van de marketing actie te verstrekken aangezien u het creeert.

>[!NOTE] Het ontbreken om `{marketingActionName}` in de vraag te leveren zal in een 405 Fout (Methode niet Toegestaan) resulteren aangezien u niet wordt toegelaten om PPUT aan het `/marketingActions/custom` eindpunt direct uit te voeren. Ook, als `name` in de lading niet `{marketingActionName}` in de weg aanpast, zult u een 400 Fout (Onjuiste Verzoek) ontvangen.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**Antwoord**

Als dit gelukt is, ontvangt u een HTTP-status 201 (Gemaakt) en bevat de responsstructuur de details van de nieuwe marketingactie. Het antwoord `name` in de reactie moet overeenkomen met wat in de aanvraag is verzonden.

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## Een marketingactie verwijderen

Het is mogelijk marketingacties te verwijderen door een DELETE verzoek te sturen naar de gebruiker `{marketingActionName}` van de marketingactie die u wilt verwijderen.

>[!NOTE] U kunt geen marketingacties verwijderen waarnaar wordt verwezen door een bestaand beleid. Als u dit probeert, treedt een fout van 400 op (Onjuist verzoek) samen met een foutbericht dat de `id` (of meerdere id&#39;s) bevat van een beleid (of beleid) dat een verwijzing bevat naar de marketingactie die u wilt verwijderen.

**API-indeling**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**Verzoek**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Als de marketing actie met succes is geschrapt, zal de reactiekarakter met een Status 200 van HTTP (O.K.) leeg zijn.

U kunt de schrapping bevestigen door te proberen om (GET) de marketing actie te zoeken. U ontvangt een HTTP-status 404 (Niet gevonden) samen met het foutbericht &quot;Niet gevonden&quot; omdat de marketingactie is verwijderd.
