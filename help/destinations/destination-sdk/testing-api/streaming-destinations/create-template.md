---
description: Leer hoe u de API voor bestemmingstests gebruikt om de transformatiesjabloon voor het streaming doelbericht te testen voordat u de bestemming publiceert.
title: Een sjabloon voor berichttransformatie maken en testen
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# Een sjabloon voor berichttransformatie maken en testen {#create-template}

## Overzicht {#overview}

Als deel van Destination SDK, verstrekt de Adobe ontwikkelaarshulpmiddelen om u in het vormen van en het testen van uw bestemming te helpen. Op deze pagina wordt beschreven hoe u een sjabloon voor berichttransformatie kunt maken en testen. Voor informatie over hoe te om uw bestemming te testen, lees [ test uw bestemmingsconfiguratie ](streaming-destination-testing-overview.md).

Om **tot stand te brengen en een malplaatje van de berichttransformatie** tussen het doelschema in Adobe Experience Platform en het berichtformaat te testen dat door uw bestemming wordt gesteund, gebruik het *Malplaatje auteursgereedschap* verder hieronder beschreven.  Lees meer over de gegevenstransformatie tussen bron en doelschema in het [ document van het berichtformaat ](../../functionality/destination-server/message-format.md#using-templating).

Illustreerde hieronder is hoe het creëren van en het testen van een malplaatje van de berichttransformatie in het [ werkschema van de bestemmingsconfiguratie ](../../guides/configure-destination-instructions.md) in Destination SDK past:

![ Grafisch van waar creeer malplaatjestap in het werkschema van de bestemmingsconfiguratie ](../../assets/testing-api/create-template-step.png) past

## Waarom u een malplaatje van de berichttransformatie moet creëren en testen {#why-create-message-transformation-template}

Een van de eerste stappen bij het maken van uw bestemming in Destination SDK is na te denken over de manier waarop de gegevensindeling voor publiekslidmaatschap, identiteiten en profielkenmerken wordt getransformeerd wanneer deze worden geëxporteerd van Adobe Experience Platform naar uw bestemming. Vind informatie over de transformatie tussen Adobe XDM schema en uw bestemmingsschema in het [ document van het berichtformaat ](../../functionality/destination-server/message-format.md#using-templating).

Voor de transformatie om te slagen, moet u een transformatiemalplaatje verstrekken, gelijkend op dit voorbeeld: [ creeer een malplaatje dat segmenten, identiteiten, en profielattributen ](../../functionality/destination-server/message-format.md#segments-identities-attributes) verzendt.

Adobe verstrekt een malplaatjehulpmiddel dat u toestaat om het berichtmalplaatje tot stand te brengen en te testen dat gegevens van het formaat XDM van de Adobe in het formaat omzet dat door uw bestemming wordt gesteund. Het gereedschap heeft twee API-eindpunten die u kunt gebruiken:

* Gebruik *steekproefmalplaatje API* om een steekproefmalplaatje te krijgen.
* Gebruik *teruggeeft malplaatje API* om het steekproefmalplaatje terug te geven zodat kunt u het resultaat tegen het verwachte gegevensformaat van uw bestemming vergelijken. Nadat u de geëxporteerde gegevens hebt vergeleken met de gegevensindeling die uw bestemming verwacht, kunt u de sjabloon bewerken. Op deze manier komen de geëxporteerde gegevens die u genereert overeen met de gegevensindeling die door de bestemming wordt verwacht.

## Stappen die moeten worden voltooid voordat de sjabloon wordt gemaakt {#prerequisites}

Voordat u de sjabloon kunt maken, moet u de onderstaande stappen uitvoeren:

1. [ creeer een configuratie van de bestemmingsserver ](../../authoring-api/destination-server/create-destination-server.md). De sjabloon die u genereert, verschilt op basis van de waarde die u opgeeft voor de parameter `maxUsersPerRequest` .
   * Gebruik `maxUsersPerRequest=1` als u wilt dat een API-aanroep naar uw doel één profiel bevat, samen met de publiekskwalificaties, -identiteiten en -profielkenmerken ervan.
   * Gebruik `maxUsersPerRequest` met een waarde groter dan één als u een API-aanroep naar uw doel meerdere profielen wilt opnemen, samen met de kwalificaties van de doelgroep, identiteiten en profielkenmerken.
2. [ creeer een bestemmingsconfiguratie ](../../authoring-api/destination-configuration/create-destination-configuration.md) en voeg identiteitskaart van de configuratie van de bestemmingsserver in `destinationDelivery.destinationServerId` toe.
3. [ krijgt identiteitskaart van de bestemmingsconfiguratie ](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) die u enkel creeerde, zodat kunt u het in het hulpmiddel van de malplaatjeverwezenlijking gebruiken.
4. Begrijp [ welke functies en filters u ](../../functionality/destination-server/supported-functions.md) in het malplaatje van de berichttransformatie kunt gebruiken.

## De voorbeeldsjabloon-API gebruiken en sjabloon-API renderen om een sjabloon voor uw doel te maken {#iterative-process}

>[!TIP]
>
>Alvorens het creëren van en het uitgeven van uw malplaatje van de berichttransformatie, kunt u beginnen door [ terug malplaatje API eindpunt ](../../testing-api/streaming-destinations/render-template-api.md#render-exported-data) met een eenvoudig malplaatje te roepen dat uw ruwe profielen uitvoert zonder enige transformaties toe te passen. De syntaxis voor de eenvoudige sjabloon is: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

Het proces om het malplaatje te krijgen en te testen is iteratief. Herhaal de onderstaande stappen totdat de geëxporteerde profielen overeenkomen met de verwachte gegevensindeling van de bestemming.

1. Eerst, [ krijgt een steekproefmalplaatje ](../../testing-api/streaming-destinations/create-template.md#sample-template-api).
2. Gebruik de voorbeeldsjabloon als beginpunt om zelf een concept te maken.
3. Roep [ terug malplaatje API eindpunt ](../../testing-api/streaming-destinations/create-template.md#render-template-api) met uw eigen malplaatje. Adobe genereert voorbeeldprofielen op basis van uw schema en retourneert het resultaat of eventuele aangetroffen fouten.
4. Vergelijk de geëxporteerde gegevens met de gegevensindeling die door de bestemming wordt verwacht. Bewerk indien nodig de sjabloon.
5. Herhaal dit proces totdat de geëxporteerde profielen overeenkomen met de verwachte gegevensindeling van de bestemming.

## Een voorbeeldsjabloon ophalen met de voorbeeldsjabloon-API {#sample-template-api}

>[!NOTE]
>
>Voor volledige API verwijzingsdocumentatie, lees [ de verrichtingen van steekproefmalplaatje API ](../../testing-api/streaming-destinations/sample-template-api.md).

Voeg een bestemmingsidentiteitskaart aan de vraag, zoals hieronder getoond toe, en de reactie zal een malplaatjevoorbeeld terugkeren die aan bestemmingsidentiteitskaart beantwoordt.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

Als bestemmingsidentiteitskaart u verstrekt aan een bestemmingsconfiguratie met [ beste inspanningssamenvoeging ](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) en `maxUsersPerRequest=1` in het samenvoegingsbeleid beantwoordt, keert het verzoek een steekproefmalplaatje gelijkend op dit terug:

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

## Escape-sjabloon voor tekens {#character-escape-template}

Voordat u de sjabloon kunt gebruiken om profielen te renderen die overeenkomen met de verwachte indeling van de bestemming, moet u de sjabloon niet opnieuw tekenen, zoals hieronder in de schermafbeelding wordt weergegeven.

![ Video die toont hoe te karakter-vlucht een malplaatje gebruikend een online karakter het ontsnapen hulpmiddel ](../../assets/testing-api/escape-characters.gif)

U kunt een online gereedschap voor het verwijderen van tekens gebruiken. Bovenstaande demo gebruikt [ JSON Escape formatter ](https://jsonformatter.org/json-escape).

## Sjabloon-API renderen {#render-template-api}

Na het creëren van een malplaatje van de berichttransformatie gebruikend [ steekproefmalplaatje API ](create-template.md#sample-template-api), kunt u [ het malplaatje ](render-template-api.md) teruggeven om uitgevoerde gegevens te produceren die op het worden gebaseerd. Op deze manier kunt u controleren of de profielen die Adobe Experience Platform naar uw bestemming zou exporteren, overeenkomen met de verwachte indeling van uw bestemming.

Raadpleeg de API-naslaggids voor voorbeelden van aanroepen die u kunt uitvoeren:

* [Een sjabloon renderen zonder profielen die in de hoofdtekst zijn verzonden](render-template-api.md#multiple-profiles-no-body)
* [Een sjabloon renderen met profielen die in de hoofdtekst zijn verzonden](render-template-api.md#multiple-profiles-with-body)

Bewerk de sjabloon en stel aanroepen in naar het API-eindpunt van de rendersjabloon totdat de geëxporteerde profielen overeenkomen met de verwachte gegevensindeling van de bestemming.

## Voeg uw karakter-beschermde malplaatje aan de configuratie van de bestemmingsserver toe

Zodra u met uw malplaatje van de berichttransformatie wordt tevredengesteld, voeg het aan uw [ configuratie van de bestemmingsserver ](../../authoring-api/destination-server/create-destination-server.md), in `httpTemplate.requestBody.value` toe.
