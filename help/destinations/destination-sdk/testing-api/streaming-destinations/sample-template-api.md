---
description: Leer hoe u de API voor bestemmingstests gebruikt om een sjabloon voor de transformatie van testberichten voor uw bestemming te genereren.
title: Een transformatiesjabloon voor een voorbeeldbericht genereren
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Een transformatiesjabloon voor een voorbeeldbericht genereren {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**API eindpunt**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Deze pagina maakt een lijst en beschrijft alle API verrichtingen die u het gebruiken van het `/authoring/testing/template/sample` API eindpunt kunt uitvoeren, om het malplaatje van de a [ berichttransformatie ](../../functionality/destination-server/message-format.md#using-templating) voor uw bestemming te produceren. Voor een beschrijving van de functionaliteit die door dit eindpunt wordt gesteund, lees [ creeer malplaatje ](create-template.md).

## Aan de slag met API-voorbeeldbewerkingen voor sjablonen {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Voorbeeldsjabloon ophalen {#generate-sample-template}

U kunt een steekproefmalplaatje krijgen door een verzoek van GET aan het `authoring/testing/template/sample/` eindpunt te doen en bestemmingsidentiteitskaart van de bestemmingsconfiguratie te verstrekken die op wordt gebaseerd die u uw malplaatje creeert.

>[!TIP]
>
>* De doel-id die u hier moet gebruiken, is de `instanceId` die overeenkomt met een doelconfiguratie die is gemaakt met het `/destinations` -eindpunt. Verwijs naar [ terugwinnen een bestemmingsconfiguratie ](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) voor meer details.

**API formaat**

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
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met een voorbeeldsjabloon die u kunt bewerken om aan te passen aan de verwachte gegevensindeling.

Als bestemmingsidentiteitskaart u verstrekt aan een bestemmingsconfiguratie met [ beste inspanningssamenvoeging ](../../functionality/destination-configuration/aggregation-policy.md) en `maxUsersPerRequest=1` in het samenvoegingsbeleid beantwoordt, keert het verzoek een steekproefmalplaatje gelijkend op dit terug:

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
        {#- Alternative syntax for filtering audiences by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Als bestemmingsidentiteitskaart u verstrekt aan een malplaatje van de bestemmingsserver met [ configureerbare samenvoeging ](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) of [ beste inspanningssamenvoeging ](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) met `maxUsersPerRequest` groter dan één beantwoordt, keert het verzoek een steekproefmalplaatje gelijkend op dit terug:

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
                {#- Alternative syntax for filtering audiences by status: -#}
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

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een sjabloon voor berichttransformatie kunt genereren met behulp van het API-eindpunt van `/authoring/testing/template/sample` . Daarna, kunt u [ gebruiken teruggeeft malplaatje API eindpunt ](render-template-api.md) om uitgevoerde profielen te produceren die op het malplaatje worden gebaseerd en hen tegen het verwachte gegevensformaat van uw bestemming te vergelijken.
