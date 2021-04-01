---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevens prep;api gids;schema's;
solution: Experience Platform
title: Schemas API Endpoint
topic: schema's
description: 'U kunt het `/functies'' eindpunt in Adobe Experience Platform API gebruiken om uw kaartuitdrukkingen en lijst beschikbare kaartsetfuncties te bevestigen. '
translation-type: tm+mt
source-git-commit: 60c80a73deb8c77f19d5963cc3319d46143fb4c3
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Functie-eindpunten

Met toewijzingsfuncties kunt u gegevens transformeren tussen bron- en doelschema&#39;s. U kunt het `/languages/el` eindpunt gebruiken om uw uitdrukkingen te bevestigen evenals een lijst van alle beschikbare afbeelding-vastgestelde functies te krijgen.

## Expressies valideren

U kunt bevestigen als uw huidige uitdrukking geldig is door een verzoek van de POST aan het `/languages/el/validate` eindpunt te doen.

**API-indeling**

```
POST /languages/el/validate
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met de validatiestatus van de expressie.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## Lijsttoewijzingsfuncties

U kunt een lijst van alle afbeelding-vastgestelde functies terugwinnen beschikbaar aan u door een verzoek van de GET aan het `/languages/el/functions` eindpunt te doen.

**API-indeling**

```
GET /languages/el/functions
```

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst van alle beschikbare toewijzingsfuncties.

>[!NOTE]
>
>Deze reactie is afgebroken voor de ruimte.

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## Operatoren voor lijsttoewijzing

U kunt een lijst van alle afbeelding-vastgestelde exploitanten terugwinnen beschikbaar aan u door een verzoek van de GET aan het `/languages/el/operators` eindpunt te doen.

**API-indeling**

```
GET /languages/el/operators
```

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst van alle beschikbare toewijzingsoperatoren.

>[!NOTE]
>
>Deze reactie is afgebroken voor de ruimte.

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
