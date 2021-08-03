---
title: Adobe Target gebruiken met de SDK van het Web van het Platform
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven gebruikend Adobe Target
keywords: doel;adobe target;activity.id;experience.id;renderDecisions;DecisionScopes;prehide snippet;vec;Form-Based Experience Composer;xdm;publiek;decisions;scope;schema;system diagram;diagram
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 930756b4e10c42edf2d58be16c51d71df207d1af
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 3%

---

# [!DNL Adobe Target] gebruiken met [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan persoonlijke ervaringen leveren en weergeven die in  [!DNL Adobe Target] het webkanaal worden beheerd. U kunt een redacteur WYSIWYG, genoemd [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), of een niet-visuele interface, [Op vorm-gebaseerde Composer van de Ervaring](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), gebruiken om, uw activiteiten en verpersoonlijkingservaringen tot stand te brengen te activeren en te leveren.

>[!IMPORTANT]
>
>De [Adobe Target documentatie](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en) omvat onderwerpen die informatie specifiek voor het Web SDK van het Platform aangezien het op de eigenschappen en de functionaliteit van het Doel betrekking heeft.

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

Het volgende diagram helpt u het werkschema van [!DNL Target] en [!DNL Platform Web SDK] randbesluit begrijpen.

![Diagram van de randbeslissing van Adobe Target met het Web SDK van het Platform](./assets/target-platform-web-sdk.png)

| Bellen | Details |
| --- | --- |
| 1 | Het apparaat laadt [!DNL Platform Web SDK]. [!DNL Platform Web SDK] verzendt een verzoek naar het randnetwerk met XDM gegevens, identiteitskaart van het Milieu van Gegevensstromen, overgegaan parameters, en identiteitskaart van de Klant (facultatief). De pagina (of containers) is vooraf verborgen. |
| 2 | Het Edge-netwerk verzendt de aanvraag naar de Edge-services om deze te verrijken met de informatie over de bezoeker-id, toestemming en andere bezoekerscontext, zoals geolocatie en apparaatvriendelijke namen. |
| 3 | Het Edge-netwerk verzendt het verrijkte aanpassingsverzoek naar de [!DNL Target]-rand met de Bezoeker-id en doorgegeven-in-parameters. |
| 4 | Profielscripts worden uitgevoerd en vervolgens opgenomen in de profielopslag van [!DNL Target]. De opslag van het profiel haalt segmenten van [!UICONTROL Audience Library] (bijvoorbeeld, segmenten die van [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform] worden gedeeld). |
| 5 | Op basis van URL-aanvraagparameters en -profielgegevens bepaalt [!DNL Target] welke activiteiten en ervaringen moeten worden weergegeven voor de bezoeker voor de huidige paginaweergave en voor toekomstige vooraf ingestelde weergaven. [!DNL Target] stuurt dit vervolgens terug naar het Edge-netwerk. |
| 6 | a. Het randnetwerk verzendt de verpersoonlijkingsreactie terug naar de pagina, naar keuze met inbegrip van profielwaarden voor extra verpersoonlijking. Gepersonaliseerde inhoud op de huidige pagina wordt zo snel mogelijk weergegeven zonder flikkering van de standaardinhoud.<br>b. De gepersonaliseerde inhoud voor meningen die als resultaat van gebruikersacties in Één enkele Toepassing van de Pagina (SPA) worden getoond wordt in het voorgeheugen ondergebracht zodat kan het onmiddellijk zonder een extra servervraag worden toegepast wanneer de meningen worden teweeggebracht. <br>c. Het Edge-netwerk verzendt de bezoeker-id en andere waarden in cookies, zoals toestemming, sessie-id, identiteit, cookie-controle, personalisatie enzovoort. |
| 7 | Het Edge-netwerk stuurt [!UICONTROL Analytics for Target] (A4T) details (activiteit, ervaring en conversiemetagegevens) door naar de [!DNL Analytics] rand. |

## [!DNL Adobe Target] inschakelen

Ga als volgt te werk om [!DNL Target] in te schakelen:

1. Schakel [!DNL Target] in uw [datastream](../../fundamentals/datastreams.md) in met de juiste clientcode.
1. Voeg de optie `renderDecisions` toe aan uw gebeurtenissen.

Vervolgens kunt u desgewenst ook de volgende opties toevoegen:

* **`decisionScopes`**: Haal specifieke activiteiten op (handig voor activiteiten die zijn gemaakt met de op formulieren gebaseerde composer) door deze optie aan uw gebeurtenissen toe te voegen.
* **[Fragment](../manage-flicker.md)** vooraf verbergen: Alleen bepaalde delen van de pagina verbergen.

## Adobe Target VEC gebruiken

Als u de VEC met een [!DNL Platform Web SDK]-implementatie wilt gebruiken, installeert en activeert u de [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) of [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

Voor meer informatie, zie [de helperuitbreiding van de Composer van de Visuele Ervaring](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) in *Adobe Target gids*.

## Aangepaste inhoud renderen

Zie [Rendering personalization content](../rendering-personalization-content.md) voor meer informatie.

## Soorten publiek in XDM

Bij het bepalen van publiek voor uw [!DNL Target] activiteiten die via [!DNL Platform Web SDK] worden geleverd, [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl) moet worden bepaald en worden gebruikt. Nadat u XDM schema&#39;s, klassen, en de groepen van het schemagebied bepaalt, kunt u [!DNL Target] publieksregel tot stand brengen die door XDM gegevens voor het richten wordt bepaald. Binnen [!DNL Target], worden XDM gegevens getoond in [!UICONTROL Audience Builder] als douaneparameter. XDM wordt geserialiseerd gebruikend puntaantekening (bijvoorbeeld, `web.webPageDetails.name`).

Als u [!DNL Target] activiteiten met vooraf bepaald publiek hebt die douaneparameters of een gebruikersprofiel gebruiken, worden zij niet correct geleverd via SDK. In plaats van aangepaste parameters of het gebruikersprofiel te gebruiken, moet u in plaats daarvan XDM gebruiken. Er is echter een out-of-the-box publiek dat zich richt op velden die worden ondersteund via de [!DNL Platform Web SDK] en die geen XDM vereisen. Deze velden zijn beschikbaar in de interface [!DNL Target] die geen XDM vereist:

* Doelbibliotheek
* Geo
* Netwerk
* Besturingssysteem
* Sitepagina&#39;s
* Browser
* Verkeersbronnen
* Tijdschema

Zie [Categorieën voor soorten publiek](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) in de *Adobe Target-gids* voor meer informatie.

### Reactietokens

Responstkens worden vooral gebruikt om metagegevens naar derden te verzenden, zoals Google, Facebook, enz. Respontokens worden geretourneerd
in het veld `meta` in `propositions` -> `items`. Hier volgt een voorbeeld:

```
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

Als u de reactietokens wilt verzamelen, moet u zich abonneren op `alloy.sendEvent` promise, doorlopen `propositions`
en haalt u de details uit `items` -> `meta`. Elke `proposition` heeft een `renderAttempted` booleveld
die aangeeft of de `proposition` is gerenderd. Zie het onderstaande voorbeeld:

```
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

* Op formulier gebaseerde composer `propositions` met `renderAttempted` vlag ingesteld op `false`
* Op Visual Experience Composer gebaseerde voorstellingen met `renderAttempted` vlag ingesteld op `true`
* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van de toepassing Eén pagina met een `renderAttempted`-vlag ingesteld op `true`

#### Bij weergave - wijzigen (voor weergaven in cache):

* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van de toepassing Eén pagina met een `renderAttempted`-vlag ingesteld op `true`

Wanneer automatische rendering is uitgeschakeld, bevat de proposities-array:

#### Bij laden van pagina:

* Op formulier gebaseerde composer `propositions` met `renderAttempted` vlag ingesteld op `false`
* Op Visual Experience Composer gebaseerde voorstellingen met `renderAttempted` vlag ingesteld op `false`
* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van de toepassing Eén pagina met een `renderAttempted`-vlag ingesteld op `false`

#### Bij weergave - wijzigen (voor weergaven in cache):

* Op Visual Experience Composer gebaseerde voorstellingen voor een weergave van de toepassing Eén pagina met een `renderAttempted`-vlag ingesteld op `false`

### Eén profiel bijwerken

Met [!DNL Platform Web SDK] kunt u het profiel bijwerken naar het [!DNL Target]-profiel en naar [!DNL Platform Web SDK] als een ervaringsgebeurtenis.

Als u een [!DNL Target]-profiel wilt bijwerken, moet u ervoor zorgen dat de profielgegevens worden doorgegeven met het volgende:

* Onder `“data {“`
* Onder `“__adobe.target”`
* Voorvoegsel `“profile.”` bijv. als hieronder

| Sleutel | Type | Beschrijving |
| --- | --- | --- |
| `renderDecisions` | Boolean | Instrueert de personaliseringscomponent of het DOM acties zou moeten interpreteren |
| `decisionScopes` | Array `<String>` | Een lijst van werkingsgebied om besluiten voor terug te winnen |
| `xdm` | Object | Gegevens geformatteerd in XDM die in het Web SDK van het Platform als ervaringsgebeurtenis landen |
| `data` | Object | Willekeurige sleutel/waardeparen verzonden naar [!DNL Target] oplossingen onder de doelklasse. |

De typische [!DNL Platform Web SDK] code die dit bevel gebruikt kijkt als het volgende:

**`sendEvent`met profielgegevens**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Profielkenmerken verzenden naar Adobe Target:**

```
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

In de volgende tabel worden de [!DNL Recommendations]-kenmerken weergegeven en wordt aangegeven of elk kenmerk wordt ondersteund via de [!DNL Platform Web SDK]:

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

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```

## Foutopsporing

mboxTrace en mboxDebug zijn afgekeurd. Gebruik [[!DNL Platform Web SDK] foutopsporing](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologie

__Proposities:__ In  [!DNL Target]correleert de voorstelling met de ervaring die u hebt geselecteerd op basis van een activiteit.

__Schema:__ Het schema van een besluit is het soort aanbod in  [!DNL Target].

__Toepassingsgebied:__ het toepassingsgebied van de beschikking. In [!DNL Target], is het werkingsgebied mBox. Het globale mBox is het `__view__` werkingsgebied.

__XDM:__ XDM wordt geserialiseerd in puntnotatie en dan gezet in  [!DNL Target] als parameters mBox.
