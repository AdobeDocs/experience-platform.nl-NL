---
title: Toegangslabels toepassen om gebruikerstoegang tot brongegevens te beheren met behulp van de API
description: Leer hoe u de Flow Service API kunt gebruiken om toegangslabels toe te passen en gebruikerstoegang tot uw brongegevens te beheren.
hide: true
hidefromtoc: true
source-git-commit: 80fb60abdf33eb2a7ca691a9a48a811c632b34fc
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Toegangslabels toepassen om gebruikerstoegang tot brongegevens te beheren met behulp van de API

U kunt de functies gebruiken die door [ op attributen-gebaseerde toegangscontrole ](../../../access-control/abac/overview.md) in Real-Time CDP worden verstrekt om etiketten op uw brongegevens toe te passen. Met deze eigenschap, kunt u ervoor zorgen dat slechts een ondergroep van gebruikers in uw organisatie toegang tot specifieke brongegevens krijgt.

Wanneer u een toegangslabel aan een bepaalde gegevensstroom toevoegt, slechts kunnen de gebruikers die toegang tot een rol hebben die dat etiket wordt toegewezen dat dataflow bekijken en uitgeven. Als een gegevensstroom van bronnen niet met om het even welke etiketten wordt gemerkt, is het zichtbaar aan alle gebruikers die tot uw organisatie behoren. Als u bijvoorbeeld het label C12 toepast op een gegevensstroom, kunnen gebruikers die zijn toegewezen aan een rol die niet het label C12 heeft, de gegevensstroom niet weergeven en bewerken met het label C12.

Lees deze gids voor informatie over hoe te om toegangslabels op uw brongegevens toe te passen gebruikend [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Alvorens met de etiketten van de toegangscontrole te werken, zorg ervoor dat u zich eerst met de mogelijkheden van op attribuut-gebaseerde toegangsbeheer vertrouwt. Raadpleeg de volgende documentatie voor meer informatie:

* [Overzicht van toegangsbeheer op basis van kenmerken](../../../access-control/abac/overview.md)
* [Op attributen-gebaseerde toegangsbeheergids van begin tot eind](../../../access-control/abac/end-to-end-guide.md)
* [API-handleiding voor toegangsbeheer op basis van kenmerken](../../../access-control/abac/api/overview.md)
* [Verklarende woordenlijst met gegevensgebruikslabels](../../../data-governance/labels/reference.md)

## Toegangslabels toepassen op gegevensstromen van bronnen

>[!NOTE]
>
>* U kunt geen labels toepassen op een flowuitvoering. De flowuitvoering neemt echter alle labels over die u op de bovenliggende gegevensstroom toepast.
>
>* Als u geen meningstoegang tot een dataflow hebt, dan zult u ook niet kunnen bekijken het overeenkomstige stroomlooppas is.

Als u een label aan een gegevensstroom wilt toevoegen, vraagt u PATCH het `/flows` -eindpunt aan en geeft u de id van de gegevensstroom op die u wilt bijwerken.

**API formaat**

```http
PATCH /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{FLOW_ID}` | De id van de gegevensstroom die u wilt bijwerken. |

**Verzoek**

>[!TIP]
>
>Als u een PATCH-aanvraag wilt indienen, geeft u de versie/tag van de gegevensstroom op die u wilt bijwerken als een `if-match` headerparameter.

Met de volgende aanvraag wordt het label C12 aan de gegevensstroom met de id: `84224def-1e2a-4d95-9ea2-132d697ed2aa` toegevoegd.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Het gedeelte van de gegevensstroom dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de eigenschap wilt bijwerken. |



**Reactie**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API en tegelijk uw flow-id op te geven.

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Zodra u met succes toegangsetiketten aan uw gegevensstroom hebt gevormd, zal om het even welke gebruiker die geen toegang tot dat etiket heeft niet meer de dataflow kunnen terugwinnen. Als een gebruiker die niet is voorzien van het label C12, bijvoorbeeld een GET-aanvraag indient om de gegevensstroom met de id op te halen: `84224def-1e2a-4d95-9ea2-132d697ed2aa` , ontvangt hij of zij het volgende antwoord:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

Op dezelfde manier kunnen gebruikers zonder toegang tot het label C12 geen PATCH- of DELETE-aanvragen indienen tegen de bijgewerkte gegevensstroom en krijgen ze de volgende reactie:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## Volgende stappen

U weet nu hoe u toegangslabels op de gegevensstromen van uw bronnen kunt toepassen. U kunt er nu voor zorgen dat alleen een specifieke groep gebruikers in uw organisatie toegang heeft tot bepaalde gegevensstromen van bronnen. Lees de volgende documentatie voor meer informatie:

* [Toegangslabels toepassen op brongegevens in de gebruikersinterface](../ui/labels.md)
* [Overzicht van toegangsbeheer](../../../access-control/home.md)