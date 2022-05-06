---
title: Adobe Target gebruiken met de SDK van het Web van het Platform
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven gebruikend Adobe Target
keywords: doel;adobe target;activity.id;experience.id;renderDecisions;DecisionScopes;prehide snippet;vec;Form-Based Experience Composer;xdm;publiek;decisions;scope;schema;system diagram;diagram
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: cdcbfdec6a232495aacaf9066d880bc9a10455d1
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 3%

---

# Gebruiken [!DNL Adobe Target] met de [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan persoonlijke ervaringen leveren en weergeven die worden beheerd in [!DNL Adobe Target] naar het webkanaal. U kunt een redacteur gebruiken WYSIWYG, genoemd [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) of een niet-visuele interface [Form-based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), om uw activiteiten en personaliservaringen te maken, te activeren en te leveren.

>[!IMPORTANT]
>
>De [Adobe Target-documentatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en) omvat onderwerpen die informatie specifiek voor het Web SDK van het Platform bevatten aangezien het op de eigenschappen en de functionaliteit van het Doel betrekking heeft.

De volgende functies zijn getest en worden momenteel ondersteund in [!DNL Target]:

* [A/B-tests](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T Rapportage van indrukking en conversie](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization-activiteiten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Gerichte ervaring](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [MVT (Multivariate Tests)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations-activiteiten](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Native doelindruk en conversiemelding](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-ondersteuning](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] systeemdiagram

Het volgende diagram helpt u het werkschema van begrijpen [!DNL Target] en [!DNL Platform Web SDK] randbeslissing.

![Diagram van de randbeslissing van Adobe Target met het Web SDK van het Platform](./assets/target-platform-web-sdk.png)

| Bellen | Details |
| --- | --- |
| 1 | Het apparaat laadt de [!DNL Platform Web SDK]. De [!DNL Platform Web SDK] verzendt een verzoek naar het randnetwerk met XDM- gegevens, identiteitskaart van het Milieu van Datastreams, overgegaan parameters, en identiteitskaart van de Klant (facultatief). De pagina (of containers) is vooraf verborgen. |
| 2 | Het Edge-netwerk verzendt de aanvraag naar de Edge-services om deze te verrijken met de informatie over de bezoeker-id, toestemming en andere bezoekerscontext, zoals geolocatie en apparaatvriendelijke namen. |
| 3 | Het randnetwerk verzendt het verrijkte verpersoonlijkingsverzoek naar het [!DNL Target] rand met de parameters Visitor ID en passed-in. |
| 4 | Profielscripts worden uitgevoerd en vervolgens toegevoegd aan [!DNL Target] profielopslag. De opslag van het profiel haalt segmenten van uit [!UICONTROL Audience Library] (bijvoorbeeld segmenten die worden gedeeld vanuit [!DNL Adobe Analytics], [!DNL Adobe Audience Manager]de [!DNL Adobe Experience Platform]). |
| 5 | Gebaseerd op parameters en profielgegevens van het URL-verzoek, [!DNL Target] Hiermee bepaalt u welke activiteiten en ervaringen worden weergegeven voor de bezoeker voor de huidige paginaweergave en voor toekomstige vooraf ingestelde weergaven. [!DNL Target] stuurt dit vervolgens terug naar het Edge-netwerk. |
| 6 | a. Het randnetwerk verzendt de verpersoonlijkingsreactie terug naar de pagina, naar keuze met inbegrip van profielwaarden voor extra verpersoonlijking. Gepersonaliseerde inhoud op de huidige pagina wordt zo snel mogelijk weergegeven zonder flikkering van de standaardinhoud.<br>b. De gepersonaliseerde inhoud voor meningen die als resultaat van gebruikersacties in Één enkele Toepassing van de Pagina (SPA) worden getoond wordt in het voorgeheugen ondergebracht zodat kan het onmiddellijk zonder een extra servervraag worden toegepast wanneer de meningen worden teweeggebracht. <br>c. Het Edge-netwerk verzendt de bezoeker-id en andere waarden in cookies, zoals toestemming, sessie-id, identiteit, cookie-controle, personalisatie enzovoort. |
| 7 | Het Edge-netwerk voorwaarts [!UICONTROL Analytics for Target] (A4T) Gegevens (metagegevens over activiteit, ervaring en conversie) naar de [!DNL Analytics] rand. |

## Inschakelen [!DNL Adobe Target]

Inschakelen [!DNL Target]Ga als volgt te werk:

1. Inschakelen [!DNL Target] in uw [datastream](../../fundamentals/datastreams.md) met de juiste clientcode.
1. Voeg de `renderDecisions` aan uw gebeurtenissen.

Vervolgens kunt u desgewenst ook de volgende opties toevoegen:

* **`decisionScopes`**: Haal specifieke activiteiten op (handig voor activiteiten die zijn gemaakt met de op formulieren gebaseerde composer) door deze optie aan uw gebeurtenissen toe te voegen.
* **[Fragment vooraf verbergen](../manage-flicker.md)**: Alleen bepaalde delen van de pagina verbergen.

## Adobe Target VEC gebruiken

Als u de VEC wilt gebruiken met een [!DNL Platform Web SDK] de implementatie, installatie en activeer [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) of [Chroom](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

Zie voor meer informatie [Helpextensie Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) in de *Adobe Target-gids*.

## Aangepaste inhoud renderen

Zie [Renderen van personalisatie-inhoud](../rendering-personalization-content.md) voor meer informatie .

## Soorten publiek in XDM

Wanneer u een publiek voor uw [!DNL Target] activiteiten die via de [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl) moeten worden gedefinieerd en gebruikt. Nadat u XDM schema&#39;s, klassen, en de groepen van het schemagebied bepaalt, kunt u tot een [!DNL Target] publieksregel gedefinieerd door XDM-gegevens voor doelversie. Within [!DNL Target], XDM-gegevens worden weergegeven in de [!UICONTROL Audience Builder] als een aangepaste parameter. XDM wordt geserialiseerd gebruikend puntaantekening (bijvoorbeeld) `web.webPageDetails.name`).

Als u [!DNL Target] activiteiten met vooraf gedefinieerd publiek die aangepaste parameters of een gebruikersprofiel gebruiken, worden niet correct via de SDK geleverd. In plaats van aangepaste parameters of het gebruikersprofiel te gebruiken, moet u in plaats daarvan XDM gebruiken. Er is echter een out-of-the-box-publiek voor doelgebieden die worden ondersteund via de [!DNL Platform Web SDK] die geen XDM vereisen. Deze velden zijn beschikbaar in het dialoogvenster [!DNL Target] UI die geen XDM vereist:

* Doelbibliotheek
* Geo
* Netwerk
* Besturingssysteem
* Sitepagina&#39;s
* Browser
* Verkeersbronnen
* Tijdschema

Zie voor meer informatie [Categorieën voor soorten publiek](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) in de *Adobe Target-gids*.

### Reactietokens

Reactietokens worden vooral gebruikt voor het verzenden van metagegevens naar derden, zoals Google, Facebook, enz. De tokens van de reactie zijn teruggekeerd in `meta` veld binnen `propositions` -> `items`. Hier volgt een voorbeeld:

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Als u de reactietokens wilt verzamelen, moet u zich abonneren op `alloy.sendEvent` beloven, doorlopen `propositions`
en verwijder de gegevens uit `items` -> `meta`. Elke `proposition` heeft een `renderAttempted` Booleaans veld dat aangeeft of de `proposition` is weergegeven of niet. Zie het onderstaande voorbeeld:

```js
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Wanneer automatische rendering is ingeschakeld, bevat de proposities-array:

#### Bij laden van pagina:

* Op formulier gebaseerde composer `propositions` with `renderAttempted` markering ingesteld op `false`
* Op Visual Experience Composer gebaseerde voorstellen met `renderAttempted` markering ingesteld op `true`
* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van één pagina-toepassing met `renderAttempted` markering ingesteld op `true`

#### Bij weergave - wijzigen (voor weergaven in cache):

* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van één pagina-toepassing met `renderAttempted` markering ingesteld op `true`

Wanneer automatische rendering is uitgeschakeld, bevat de proposities-array:

#### Bij laden van pagina:

* Op formulier gebaseerde composer `propositions` with `renderAttempted` markering ingesteld op `false`
* Op Visual Experience Composer gebaseerde voorstellen met `renderAttempted` markering ingesteld op `false`
* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van één pagina-toepassing met `renderAttempted` markering ingesteld op `false`

#### Bij weergave - wijzigen (voor weergaven in cache):

* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van één pagina-toepassing met `renderAttempted` markering ingesteld op `false`

### Eén profiel bijwerken

De [!DNL Platform Web SDK] Hiermee kunt u het profiel bijwerken naar de [!DNL Target] en de [!DNL Platform Web SDK] als een ervaringsgebeurtenis.

Als u een [!DNL Target] , zorgt u ervoor dat de profielgegevens worden doorgegeven met het volgende:

* Onder `“data {“`
* Onder `“__adobe.target”`
* Voorvoegsel `“profile.”` zoals hieronder

| Sleutel | Type | Beschrijving |
| --- | --- | --- |
| `renderDecisions` | Boolean | Instrueert de personaliseringscomponent of het DOM acties zou moeten interpreteren |
| `decisionScopes` | Array `<String>` | Een lijst van werkingsgebied om besluiten voor terug te winnen |
| `xdm` | Object | Gegevens geformatteerd in XDM die in het Web SDK van het Platform als ervaringsgebeurtenis landen |
| `data` | Object | Arbitraire sleutel/waardeparen verzonden naar [!DNL Target] oplossingen onder de doelklasse. |

Normaal [!DNL Platform Web SDK] code die deze opdracht gebruikt ziet er als volgt uit:

**`sendEvent`met profielgegevens**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Profielkenmerken verzenden naar Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Aanbevelingen aanvragen

De volgende tabellijsten [!DNL Recommendations] kenmerken en of elk kenmerk wordt ondersteund via de [!DNL Platform Web SDK]:

| Categorie | Kenmerk | Ondersteuningsstatus |
| --- | --- | --- |
| Recommendations - Kenmerken van standaardentiteiten | entity.id | Ondersteund |
|  | entity.name | Ondersteund |
|  | entity.categoryId | Ondersteund |
|  | entity.pageUrl | Ondersteund |
|  | entity.thumbnailUrl | Ondersteund |
|  | entity.message | Ondersteund |
|  | entity.value | Ondersteund |
|  | entity.inventory | Ondersteund |
|  | entity.brand | Ondersteund |
|  | entity.margin | Ondersteund |
|  | entity.event.detailsOnly | Ondersteund |
| Recommendations - Aangepaste entiteitskenmerken | entity.yourCustomAttributeName | Ondersteund |
| Recommendations - Gereserveerde parameters mbox/page | excludeIds | Ondersteund |
|  | cartIds | Ondersteund |
|  | productPurchasedId | Ondersteund |
| Pagina- of itemcategorie voor categorie-affiniteit | user.categoryId | Ondersteund |

**Recommendations-kenmerken verzenden naar Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Foutopsporing

mboxTrace en mboxDebug zijn afgekeurd. Gebruiken [[!DNL Platform Web SDK] foutopsporing](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologie

__Voorstellen:__ In [!DNL Target], correleren met de ervaring die is geselecteerd uit een activiteit.

__Schema:__ Het schema van een besluit is het soort aanbod in [!DNL Target].

__Toepassingsgebied:__ De reikwijdte van het besluit. In [!DNL Target], het bereik is de mBox. De algemene mBox is de `__view__` bereik.

__XDM:__ XDM wordt geserialiseerd in puntnotatie en dan gezet in [!DNL Target] als mBox-parameters.
