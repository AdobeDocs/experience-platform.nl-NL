---
title: Statusbeheer client
description: Leer hoe Adobe Experience Platform Edge Network de clientstatus beheert
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: client;state;management;edge;network;gateway;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 1%

---

# Statusbeheer client

Het netwerk van de Rand zelf is stateless (het handhaaft zijn eigen zitting niet). Nochtans zijn er bepaalde gebruik-gevallen die cliënt-zijstaatpersistentie vereisen, zoals:

* Consistent apparaat-identificatie (zie [bezoekersidentificatie](visitor-identification.md))
* Gebruikerstoestemming verzamelen en afdwingen
* Id van personalisatiesessie behouden

Het netwerk van de Rand gebruikt een protocol van het staatsbeheer, dat het opslagaspect aan zijn cliënt/SDK delegeert, en omvat staatsingangen in zijn reacties. Voor browsers worden de items opgeslagen als cookies.

De verantwoordelijkheid van de klant is deze op te slaan en op te nemen in alle volgende verzoeken. De cliënt moet ook zorgen voor juiste vervaldatum voor ingangen, zoals die door de gateway worden geïnstrueerd. Wanneer de items als cookies zijn opgeslagen, werkt de browser dit alles automatisch.

Hoewel de statusvermeldingen altijd een normale waarde hebben `String` -waarde (zichtbaar voor de aanroeper/SDK). U mag de waarden op geen enkele manier gebruiken of wijzigen. De waardestructuur/indeling of zelfs de naam zelf kan op elk gewenst moment veranderen. Dit kan leiden tot onverwacht gedrag voor clients die de status intern gebruiken. De staat is bedoeld om altijd door de gateway zelf of andere randdiensten worden verbruikt.

## De clientstatus behouden als metagegevens

De staat die door [!DNL Edge Network] in de responsinstantie `Handle` object met het type `state:store`.

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| Kenmerk | Type | Beschrijving |
| --- | --- | --- |
| `key` | Tekenreeks | **Vereist**. De naam van het item. |
| `value` | Tekenreeks | *Optioneel*. De invoerwaarde. |
| `maxAge` | Geheel | *Optioneel* De ingstijd-aan-levende (TTL), in seconden. Als items ontbreken, worden deze alleen voor de huidige sessie opgeslagen. |
| `attrs` | `Map<String, String>` | *Optioneel*. Een optionele lijst met entry-attributen. Voor alle veilige verbindingen met een veilige referentie-HTTP-header, `SameSite` kenmerk is ingesteld op `None`. |


Voor ondersteuning van multitagging (d.w.z. meerdere SDK-instanties in dezelfde eigenschap, die mogelijk naar verschillende organisaties verwijzen), worden alle statusvermeldingen automatisch vooraf ingesteld op `kndctr_` en de URL-veilige organisatie-id.

Wanneer de client-SDK een `state:store` in de reactie moet deze het volgende doen:

* De ingangen van de opslag cliënt-kant, die de vervaltijd eerbiedigen door de gateway wordt geleverd.
* Laad ze vanuit de clientopslag en neem alle niet-verlopen items op in de volgende aanvragen.

Hier is een voorbeeld van een verzoek dat in de client-side opgeslagen staat overgaat:

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## De status van de client in browsercookies behouden

Wanneer het werken met browser cliënten, kan het Netwerk van de Rand automatisch de ingangen als browser koekjes voortzetten. Dit staat transparante steun van de staatsopslag toe, aangezien browsers het protocol van het staatsbeheer door gebrek respecteren.

Bijna alle ingangen worden geconcretiseerd als eerste partijkoekjes wanneer toegelaten en gesteund (zie de nota hieronder), maar de gateway kon sommige derdekoekjes ook opslaan wanneer de derde partij `adobedc.demdex.net` -domein wordt gebruikt.

Aangezien de ingangen altijd aan een specifiek werkingsgebied (apparaat/toepassing) door hun definitie gebonden zijn, slechts zal de ondergroep die met de huidige verzoekcontext compatibel is door het Netwerk van de Rand worden geschreven. Ongeschreven items worden geretourneerd binnen een `state:store` handgreep.

Normaliter worden items met toepassingsbereik altijd geschreven als cookies van de eerste partij, terwijl items met apparaatbereik worden geschreven als cookies van derden. Het besluit is volledig transparant aan de bezoeker, beslist de gateway welke ingangen, afhankelijk van de vraagcontext kunnen worden geschreven.

De aanroeper moet uitdrukkelijk steun voor het opslaan van cliëntstaat als koekjes toelaten, via `meta.state.cookiesEnabled` markering:

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| Kenmerk | Type | Beschrijving |
| --- | --- | --- |
| `cookiesEnabled` | Boolean | Als deze optie is ingesteld, wordt ondersteuning voor cookies ingeschakeld. De standaardwaarde is `false`. |
| `domain` | Tekenreeks | Vereist wanneer `cookiesEnabled: true`. Het domein op hoofdniveau waarop de cookies moeten worden geschreven. Het Edge-netwerk gebruikt deze waarde om te bepalen of de status als cookies kan worden voortgezet. |

Zelfs als ondersteuning voor cookies is ingeschakeld via het dialoogvenster `cookiesEnabled` markering, zal het Netwerk van de Rand van Adobe Experience Platform slechts de staatsingangen schrijven als het verzoek top-level domein met `domain` opgegeven door de aanroeper. Wanneer er een probleem is, worden items geretourneerd in een `state:store` handgreep.

U kunt de cookies van de eerste fabrikant niet schrijven (zelfs niet als ondersteuning is ingeschakeld) in de volgende gevallen:

* Het verzoek is afkomstig van de derde `adobedc.demdex.net` domein.
* Het verzoek is afkomstig van een eerste `CNAME` domein, verschillend van gespecificeerd door de bezoeker binnen `meta.state.domain`.

## Koekjesbeveiliging

Alle cookies hebben de [Veilige markering](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) indien mogelijk ingeschakeld.

Alle veilige cookies hebben de [Het kenmerk SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) instellen op `None`, wat betekent dat cookies in alle contexten worden verzonden, zowel in de eerste als in de andere partij.

* Voor de cookies van de eerste partij (`kndcrt_*`), de `Secure` markering wordt alleen ingesteld wanneer de aanvraagcontext beveiligd is (HTTPS) en wanneer de referentie ([Verwijzer HTTP-header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) is ook HTTPS. Als de verwijzer niet veilig (HTTP) is, `Secure` De vlag wordt weggelaten om het Web SDK toe te staan om hen te lezen. Een beveiligde cookie kan niet worden gelezen vanuit een onveilige context.
* Voor het cookie van derden (demdex): `Secure` markering is altijd ingesteld, aangezien alle aanvragen HTTPS zijn, de aanvraagcontext veilig is en dit cookie nooit vanuit JavaScript wordt gelezen.

De `Secure` markering is niet aanwezig in de [metagegevensweergave van cookies](#state-as-metadata). Alleen de `SameSite` -kenmerk is opgenomen. In dit geval is het de verantwoordelijkheid van de klant om de `Secure` wanneer de `SameSite` is present. Cookies met `SameSite=None` moet ook de `Secure` -kenmerk, aangezien voor deze toepassingen een beveiligde context (HTTPS) is vereist.
