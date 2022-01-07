---
description: Deze pagina maakt een lijst en beschrijft van alle API verrichtingen die u kunt uitvoeren gebruikend `/authoring/testing/template/sample` API eindpunt, om een malplaatje van de testberichttransformatie voor uw bestemming te krijgen.
title: API-bewerkingen voor voorbeeldsjablonen ophalen
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 6dd8a94e46b9bee6d1407e7ec945a722d8d7ecdb
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# API-bewerkingen voor voorbeeldsjablonen ophalen {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**API-eindpunt**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met de `/authoring/testing/template/sample` API-eindpunt, om een [berichttransformatiesjabloon](./message-format.md#using-templating) voor uw bestemming. Voor een beschrijving van de functionaliteit die door dit eindpunt wordt gesteund, lees [sjabloon maken](./create-template.md).

## Aan de slag met API-voorbeeldbewerkingen voor sjablonen {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Voorbeeldsjabloon ophalen {#generate-sample-template}

U kunt een voorbeeldsjabloon ophalen door een GET-aanvraag in te dienen bij de `authoring/testing/template/sample/` eindpunt en het verstrekken van bestemmingsidentiteitskaart van de bestemmingsconfiguratie die op wordt gebaseerd waarop u uw malplaatje creeert.

>[!TIP]
>
>* De doel-id die u hier moet gebruiken, is de `instanceId` die met een bestemmingsconfiguratie beantwoordt, die wordt gecreeerd gebruikend `/destinations` eindpunt. Zie de [API-naslaggids voor doelconfiguratie](./destination-configuration-api.md#retrieve-list).


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

Als de bestemmingsidentiteitskaart u verstrekt beantwoordt aan een bestemmingsconfiguratie met [beste inspanningsaggregatie](./destination-configuration.md#best-effort-aggregation) en `maxUsersPerRequest=1` in het samenvoegingsbeleid, keert het verzoek een steekproefmalplaatje gelijkend op dit terug:

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

Als de bestemmingsidentiteitskaart u verstrekt beantwoordt aan een malplaatje van de bestemmingsserver met [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) of [beste inspanningsaggregatie](./destination-configuration.md#best-effort-aggregation) with `maxUsersPerRequest` Bij meer dan één sjabloon retourneert de aanvraag een voorbeeldsjabloon die vergelijkbaar is met deze sjabloon:

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

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, kunt u nu een sjabloon voor berichttransformatie genereren met de opdracht `/authoring/testing/template/sample` API-eindpunt. Vervolgens kunt u de [API-eindpunt van sjabloon renderen](./render-template-api.md) om geëxporteerde profielen te genereren op basis van de sjabloon en deze te vergelijken met de verwachte gegevensindeling van uw bestemming.
