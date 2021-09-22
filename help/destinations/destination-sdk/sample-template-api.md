---
description: Deze pagina maakt een lijst en beschrijft van alle API verrichtingen die u kunt uitvoeren gebruikend `/authoring/testing/template/sample` API eindpunt, om een malplaatje van de testberichttransformatie voor uw bestemming te krijgen.
title: API-bewerkingen voor voorbeeldsjablonen ophalen
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Voorbeeld van sjabloon-API-bewerkingen {#get=sample-template-api-operations} ophalen

>[!IMPORTANT]
>
>**API-eindpunt**:  `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Deze pagina maakt een lijst en beschrijft van alle API verrichtingen die u kunt uitvoeren gebruikend het `/authoring/testing/template/sample` API eindpunt, om een [malplaatje van de berichttransformatie ](./message-format.md#using-templating) voor uw bestemming te produceren. Voor een beschrijving van de functionaliteit die door dit eindpunt wordt gesteund, lees [creeer malplaatje](./create-template.md).

## Aan de slag met API-voorbeeldbewerkingen voor sjablonen {#get-started}

Alvorens verder te gaan, te herzien [begonnen gids](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmingsauteur en vereiste kopballen te verkrijgen.

## Voorbeeldsjabloon ophalen {#generate-sample-template}

U kunt een steekproefmalplaatje krijgen door een verzoek van de GET tot het `authoring/testing/template/sample/` eindpunt te richten en bestemmingsidentiteitskaart van de bestemmingsconfiguratie te verstrekken die op wordt gebaseerd die u uw malplaatje creeert.

>[!TIP]
>
>* De bestemmingsidentiteitskaart die u hier zou moeten gebruiken is `instanceId` die aan een bestemmingsconfiguratie beantwoordt, die gebruikend het `/destinations` eindpunt wordt gecreeerd. Raadpleeg de [API referentie voor doelconfiguratie](./destination-configuration-api.md#retrieve-list).


**API-indeling**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_ID}` | Identiteitskaart van de bestemmingsconfiguratie waarvoor u een malplaatje van de berichttransformatie produceert. |

**Verzoek**

Het volgende verzoek produceert een nieuw steekproefmalplaatje, dat door de parameters wordt gevormd die in de lading worden verstrekt.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met een voorbeeldsjabloon die u kunt bewerken om aan te passen aan de verwachte gegevensindeling.

Als bestemmingsidentiteitskaart u verstrekt aan een bestemmingsconfiguratie met [beste inspanningssamenvoeging](./destination-configuration.md#best-effort-aggregation) en `maxUsersPerRequest=1` in het samenvoegingsbeleid beantwoordt, keert het verzoek een steekproefmalplaatje gelijkend op dit terug:

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Als de bestemmingsidentiteitskaart u verstrekt aan een malplaatje van de bestemmingsserver met [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) of [beste inspanningssamenvoeging](./destination-configuration.md#best-effort-aggregation) met `maxUsersPerRequest` groter dan één beantwoordt, keert het verzoek een steekproefmalplaatje gelijkend op dit terug:

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering segments by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## API-foutafhandeling {#api-error-handling}

De eindpunten van SDK API van de bestemming volgen de algemene API van het Experience Platform foutenmeldingsbeginselen. Raadpleeg [API-statuscodes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) en [headerfouten aanvragen](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) in de handleiding voor het oplossen van Platforms.

## Volgende stappen {#next-steps}

Na het lezen van dit document, weet u nu hoe te om een malplaatje van de berichttransformatie te produceren gebruikend het `/authoring/testing/template/sample` API eindpunt. Vervolgens kunt u het [Render-sjabloon-API-eindpunt](./render-template-api.md) gebruiken om geëxporteerde profielen te genereren op basis van de sjabloon en deze te vergelijken met de verwachte gegevensindeling van uw bestemming.
