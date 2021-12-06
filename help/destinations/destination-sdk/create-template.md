---
description: Als onderdeel van Destination SDK biedt Adobe hulpprogramma's voor ontwikkelaars die u helpen bij het configureren en testen van uw bestemming. Op deze pagina wordt beschreven hoe u een sjabloon voor berichttransformatie kunt maken en testen.
title: Een sjabloon voor berichttransformatie maken en testen
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: aa5898369d41ba48a1416a0b4ea82f6345333d18
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# Een sjabloon voor berichttransformatie maken en testen {#create-template}

## Overzicht {#overview}

Als onderdeel van Destination SDK biedt Adobe hulpprogramma&#39;s voor ontwikkelaars die u helpen bij het configureren en testen van uw bestemming. Op deze pagina wordt beschreven hoe u een sjabloon voor berichttransformatie kunt maken en testen. Voor informatie over hoe te om uw bestemming te testen, lees [De doelconfiguratie testen](./test-destination.md).

Naar **een sjabloon voor berichttransformatie maken en testen** tussen het doelschema in Adobe Experience Platform en de berichtindeling die door uw bestemming wordt ondersteund, gebruikt u de *Sjabloonontwerpgereedschap* hieronder beschreven.  Lees meer over de gegevenstransformatie tussen bron en doelschema in [berichtenformaat](./message-format.md#using-templating).

Hieronder wordt geïllustreerd hoe het creëren van en het testen van een malplaatje van de berichttransformatie in het [doelconfiguratieworkflow](./configure-destination-instructions.md) in Destination SDK:

![Grafiek van waar creeer malplaatjestap in het werkschema van de bestemmingsconfiguratie past](./assets/create-template-step.png)

## Waarom u een malplaatje van de berichttransformatie moet creëren en testen {#why-create-message-transformation-template}

Een van de eerste stappen bij het maken van uw bestemming in Destination SDK is na te denken over de manier waarop de gegevensindeling voor segmentlidmaatschap, identiteiten en profielkenmerken wordt getransformeerd wanneer deze van Adobe Experience Platform naar uw bestemming worden geëxporteerd. Vind informatie over de transformatie tussen Adobe XDM schema en uw bestemmingsschema in [berichtenformaat](./message-format.md#using-templating).

De transformatie is alleen succesvol als u een transformatiesjabloon opgeeft, vergelijkbaar met dit voorbeeld: [Een sjabloon maken die segmenten, identiteiten en profielkenmerken verstuurt](./message-format.md#segments-identities-attributes).

Adobe verstrekt een malplaatjehulpmiddel dat u toestaat om het berichtmalplaatje tot stand te brengen en te testen dat gegevens van het formaat XDM van de Adobe in het formaat XDM in het formaat omzet dat door uw bestemming wordt gesteund. Het gereedschap heeft twee API-eindpunten die u kunt gebruiken:
* Gebruik de *voorbeeldsjabloon-API* om een voorbeeldsjabloon te verkrijgen.
* Gebruik de *sjabloon-API renderen* om het steekproefmalplaatje terug te geven zodat kunt u het resultaat met het verwachte gegevensformaat van uw bestemming vergelijken. Nadat u de geëxporteerde gegevens hebt vergeleken met de gegevensindeling die uw bestemming verwacht, kunt u de sjabloon bewerken. Op deze manier komen de geëxporteerde gegevens die u genereert overeen met de gegevensindeling die door de bestemming wordt verwacht.

## Stappen die moeten worden voltooid voordat de sjabloon wordt gemaakt {#prerequisites}

Voordat u de sjabloon kunt maken, moet u de onderstaande stappen uitvoeren:

1. [Een doelserverconfiguratie maken](./destination-server-api.md). De sjabloon die u genereert, verschilt op basis van de waarde die u opgeeft voor de `maxUsersPerRequest` parameter.
   * Gebruiken `maxUsersPerRequest=1` als u wilt dat een API-aanroep naar uw bestemming één profiel bevat, samen met de segmentkwalificaties, -identiteiten en -profielkenmerken.
   * Gebruiken `maxUsersPerRequest` met een waarde groter dan één als u een API-aanroep naar uw bestemming meerdere profielen wilt opnemen, samen met hun segmentkwalificaties, identiteiten en profielkenmerken.
2. [Een doelconfiguratie maken](./destination-configuration-api.md#create) en voeg identiteitskaart van de configuratie van de bestemmingsserver in toe `destinationDelivery.destinationServerId`.
3. [Krijg identiteitskaart van de bestemmingsconfiguratie](./destination-configuration-api.md#retrieve-list) die u net hebt gemaakt, zodat u deze kunt gebruiken in het gereedschap voor het maken van sjablonen.

## Hoe te om het steekproefmalplaatje API te gebruiken en malplaatje API terug te geven om een malplaatje voor uw bestemming tot stand te brengen {#iterative-process}

>[!TIP]
>
>Voordat u de sjabloon voor berichttransformatie maakt en bewerkt, kunt u beginnen met het aanroepen van de [sjabloon-API-eindpunt renderen](./render-template-api.md#render-exported-data) met een eenvoudige sjabloon die uw onbewerkte profielen exporteert zonder transformaties toe te passen. De syntaxis voor de eenvoudige sjabloon is: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

Het proces om het malplaatje te krijgen en te testen is iteratief. Herhaal de onderstaande stappen totdat de geëxporteerde profielen overeenkomen met de verwachte gegevensindeling van de bestemming.

1. Eerste, [een voorbeeldsjabloon ophalen](./create-template.md#sample-template-api).
2. Gebruik de voorbeeldsjabloon als beginpunt om zelf een concept te maken.
3. Roep de [sjabloon-API-eindpunt renderen](./create-template.md#render-template-api) met uw eigen sjabloon. Adobe genereert voorbeeldprofielen op basis van uw schema en retourneert het resultaat of eventuele aangetroffen fouten.
4. Vergelijk de geëxporteerde gegevens met de gegevensindeling die door de bestemming wordt verwacht. Bewerk indien nodig de sjabloon.
5. Herhaal dit proces totdat de geëxporteerde profielen overeenkomen met de verwachte gegevensindeling van de bestemming.

## Een voorbeeldsjabloon ophalen met de voorbeeldsjabloon-API {#sample-template-api}

>[!NOTE]
>
>Voor volledige API-naslagdocumentatie leest u [API-bewerkingen voor voorbeeldsjablonen ophalen](./sample-template-api.md).

Voeg een bestemmingsidentiteitskaart aan de vraag, zoals hieronder getoond toe, en de reactie zal een malplaatjevoorbeeld terugkeren die aan bestemmingsidentiteitskaart beantwoordt.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

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

## Escape-sjabloon voor tekens {#character-escape-template}

Voordat u de sjabloon kunt gebruiken om profielen te renderen die overeenkomen met de verwachte indeling van de bestemming, moet u de sjabloon niet opnieuw tekenen, zoals hieronder in de schermafbeelding wordt weergegeven.

![Video die laat zien hoe u aan tekens ontsnappende sjablonen kunt toevoegen met een online gereedschap voor het verwijderen van tekens](./assets/escape-characters.gif)

U kunt een online gereedschap voor het verwijderen van tekens gebruiken. In de bovenstaande demo wordt het [JSON Escape-indeling](https://jsonformatter.org/json-escape).

## Sjabloon-API renderen {#render-template-api}

Nadat u een sjabloon voor berichttransformatie hebt gemaakt met de opdracht [voorbeeldsjabloon-API](./create-template.md#sample-template-api), kunt u [de sjabloon renderen](./render-template-api.md) om geëxporteerde gegevens te genereren op basis van deze gegevens. Op deze manier kunt u controleren of de profielen die Adobe Experience Platform naar uw bestemming zou exporteren, overeenkomen met de verwachte indeling van uw bestemming.

Raadpleeg de API-naslaggids voor voorbeelden van aanroepen die u kunt uitvoeren:

* [Een sjabloon renderen zonder profielen die in de hoofdtekst zijn verzonden](./render-template-api.md#multiple-profiles-no-body)
* [Een sjabloon renderen met profielen die in de hoofdtekst zijn verzonden](./render-template-api.md#multiple-profiles-with-body)

Bewerk de sjabloon en stel aanroepen in naar het API-eindpunt van de rendersjabloon totdat de geëxporteerde profielen overeenkomen met de verwachte gegevensindeling van de bestemming.

## Voeg uw karakter-beschermde malplaatje aan de configuratie van de bestemmingsserver toe

Als u tevreden bent met de sjabloon voor berichttransformatie, voegt u deze toe aan uw [doelserverconfiguratie](./server-and-template-configuration.md), in `httpTemplate.requestBody.value`.
