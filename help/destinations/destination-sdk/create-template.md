---
description: Als deel van Doel SDK, verstrekt Adobe ontwikkelaarshulpmiddelen om u in het vormen van en het testen van uw bestemming te helpen. Op deze pagina wordt beschreven hoe u een sjabloon voor berichttransformatie kunt maken en testen.
title: Een sjabloon voor berichttransformatie maken en testen
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# Een sjabloon voor berichttransformatie maken en testen {#create-template}

## Overzicht {#overview}

Als deel van Doel SDK, verstrekt Adobe ontwikkelaarshulpmiddelen om u in het vormen van en het testen van uw bestemming te helpen. Op deze pagina wordt beschreven hoe u een sjabloon voor berichttransformatie kunt maken en testen. Voor informatie over hoe te om uw bestemming te testen, lees [Test uw bestemmingsconfiguratie](./test-destination.md).

Als u **een sjabloon voor berichttransformatie wilt maken en testen** tussen het doelschema in Adobe Experience Platform en de berichtindeling die door uw bestemming wordt ondersteund, gebruikt u het *Sjabloonontwerpgereedschap* hieronder beschreven.  Lees meer over de gegevenstransformatie tussen bron en doelschema in [berichtformaat document](./message-format.md#using-templating).

Hieronder wordt geïllustreerd hoe het creëren van en het testen van een malplaatje van de berichttransformatie in [bestemmingsconfiguratiewerkschema](./configure-destination-instructions.md) in Doel SDK past:

![Grafiek van waar creeer malplaatjestap in het werkschema van de bestemmingsconfiguratie past](./assets/create-template-step.png)

## Waarom u een malplaatje van de berichttransformatie moet creëren en testen {#why-create-message-transformation-template}

Één van de eerste stappen in het creëren van uw bestemming in Doel SDK moet over denken hoe het gegevensformaat voor segmentlidmaatschap, identiteiten, en profielattributen wordt getransformeerd wanneer uitgevoerd van Adobe Experience Platform naar uw bestemming. Vind informatie over de transformatie tussen Adobe XDM schema en uw bestemmingsschema in [berichtformaat document](./message-format.md#using-templating).

Voor de transformatie moet u een transformatiesjabloon opgeven, vergelijkbaar met dit voorbeeld: [Maak een sjabloon die segmenten, identiteiten en profielkenmerken](./message-format.md#segments-identities-attributes) verzendt.

Adobe verstrekt een malplaatjehulpmiddel dat u toestaat om het berichtmalplaatje tot stand te brengen en te testen dat gegevens van het formaat XDM van de Adobe in het formaat XDM in het formaat omzet dat door uw bestemming wordt gesteund. Het gereedschap heeft twee API-eindpunten die u kunt gebruiken:
* Gebruik *voorbeeldmalplaatje API* om een steekproefmalplaatje te krijgen.
* Gebruik *render malplaatje API* om het steekproefmalplaatje terug te geven zodat kunt u het resultaat met het verwachte gegevensformaat van uw bestemming vergelijken. Nadat u de geëxporteerde gegevens hebt vergeleken met de gegevensindeling die uw bestemming verwacht, kunt u de sjabloon bewerken. Op deze manier komen de geëxporteerde gegevens die u genereert overeen met de gegevensindeling die door de bestemming wordt verwacht.

## Hoe te om het steekproefmalplaatje API te gebruiken en malplaatje API terug te geven om een malplaatje voor uw bestemming tot stand te brengen {#iterative-process}

Het proces om het malplaatje te krijgen en te testen is iteratief. Herhaal de onderstaande stappen totdat de geëxporteerde profielen overeenkomen met de verwachte gegevensindeling van de bestemming.

1. Eerst, [krijg een steekproefmalplaatje](./create-template.md#sample-template-api).
2. Gebruik de voorbeeldsjabloon als beginpunt om zelf een concept te maken.
3. Roep het [render malplaatje API eindpunt](./create-template.md#render-template-api) met uw eigen malplaatje. Adobe genereert voorbeeldprofielen op basis van uw schema en retourneert het resultaat of eventuele aangetroffen fouten.
4. Vergelijk de geëxporteerde gegevens met de gegevensindeling die door de bestemming wordt verwacht. Bewerk indien nodig de sjabloon.
5. Herhaal dit proces totdat de geëxporteerde profielen overeenkomen met de verwachte gegevensindeling van de bestemming.

## Stappen die moeten worden voltooid voordat de sjabloon wordt gemaakt {#prerequisites}

Voordat u de sjabloon kunt maken, moet u de onderstaande stappen uitvoeren:

1. [Maak een doelserverconfiguratie](./destination-server-api.md). De sjabloon die u genereert, verschilt op basis van de waarde die u opgeeft voor de parameter `maxUsersPerRequest`.
   * Gebruik `maxUsersPerRequest=1` als u een API vraag aan uw bestemming één enkel profiel, samen met zijn segmentkwalificaties, identiteiten, en profielattributen wilt omvatten.
   * Gebruik `maxUsersPerRequest` met een waarde groter dan één als u een API vraag aan uw bestemming veelvoudige profielen, samen met hun segmentkwalificaties, identiteiten, en profielattributen wilt omvatten.
2. [Creeer een bestemmingsconfiguratie ](./destination-configuration-api.md#create) en voeg identiteitskaart van de configuratie van de bestemmingsserver in toe  `destinationDelivery.destinationServerId`.
3. [Krijg identiteitskaart van de bestemmingsconfiguratie ](./destination-configuration-api.md#retrieve-list) die u enkel creeerde, zodat kunt u het in het hulpmiddel van de malplaatjeverwezenlijking gebruiken.

## Een voorbeeldsjabloon ophalen met de voorbeeldsjabloon-API {#sample-template-api}

>[!NOTE]
>
>Voor volledige API verwijzingsdocumentatie, lees [de verrichtingen van de steekproefmalplaatje API](./sample-template-api.md).

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

## Escape-sjabloon voor tekens {#character-escape-template}

Voordat u de sjabloon kunt gebruiken om profielen te renderen die overeenkomen met de verwachte indeling van de bestemming, moet u de sjabloon niet opnieuw tekenen, zoals hieronder in de schermafbeelding wordt weergegeven.

![Video die laat zien hoe u aan tekens ontsnappende sjablonen kunt toevoegen met een online gereedschap voor het verwijderen van tekens](./assets/escape-characters.gif)

U kunt een online gereedschap voor het verwijderen van tekens gebruiken. De bovenstaande demo gebruikt de [JSON Escape-notter](https://jsonformatter.org/json-escape).

## Sjabloon-API renderen {#render-template-api}

Nadat u een sjabloon voor berichttransformatie hebt gemaakt met de [voorbeeldsjabloon-API](./create-template.md#sample-template-api), kunt u de sjabloon [renderen](./render-template-api.md) om geëxporteerde gegevens te genereren op basis van de sjabloon. Op deze manier kunt u controleren of de profielen die Adobe Experience Platform naar uw bestemming zou exporteren, overeenkomen met de verwachte indeling van uw bestemming.

Raadpleeg de API-naslaggids voor voorbeelden van aanroepen die u kunt uitvoeren:

* [Een sjabloon renderen zonder profielen die in de hoofdtekst zijn verzonden](./render-template-api.md#multiple-profiles-no-body)
* [Een sjabloon renderen met profielen die in de hoofdtekst zijn verzonden](./render-template-api.md#multiple-profiles-with-body)

Bewerk de sjabloon en stel aanroepen in naar het API-eindpunt van de rendersjabloon totdat de geëxporteerde profielen overeenkomen met de verwachte gegevensindeling van de bestemming.

## Voeg uw karakter-beschermde malplaatje aan de configuratie van de bestemmingsserver toe

Zodra u met uw malplaatje van de berichttransformatie wordt tevredengesteld, voeg het aan uw [configuratie van de bestemmingsserver](./server-and-template-configuration.md), in `httpTemplate.requestBody.value` toe.
