---
title: Statusbeheer client
description: Meer informatie over het beheer van de clientstatus in Adobe Experience Platform Edge Network
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: client;state;management;edge;network;gateway;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---

# Statusbeheer client

De Edge Network zelf is staatloos (het houdt zijn eigen sessie niet aan). Nochtans zijn er bepaalde gebruik-gevallen die cliënt-zijstaatpersistentie vereisen, zoals:

* Consistente apparaatidentificatie
* Gebruikerstoestemming verzamelen en afdwingen
* Id van personalisatiesessie behouden

De Edge Network gebruikt een protocol voor staatbeheer, waarbij het opslagaspect wordt gedelegeerd aan de client/SDK, en neemt statusvermeldingen op in de reacties. Voor browsers worden de items opgeslagen als cookies.

De verantwoordelijkheid van de klant is deze op te slaan en op te nemen in alle volgende verzoeken. De cliënt moet ook zorgen voor juiste vervaldatum voor ingangen, zoals die door de gateway worden geïnstrueerd. Wanneer de items als cookies zijn opgeslagen, werkt de browser dit alles automatisch.

Hoewel de statusitems altijd een normale `String` -waarde hebben (zichtbaar voor de aanroeper/SDK), mag u de waarden op geen enkele manier gebruiken of wijzigen. De waardestructuur/indeling of zelfs de naam zelf kan op elk gewenst moment veranderen. Dit kan leiden tot onverwacht gedrag voor clients die de status intern gebruiken. De staat is bedoeld om altijd door de gateway zelf of andere randdiensten worden verbruikt.

## De status van de client als metagegevens behouden

De status die wordt geretourneerd door de [!DNL Edge Network] in de hoofdtekst van de reactie is een `Handle` -object met het type `state:store` .

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
| `key` | String | **Vereiste**. De naam van het item. |
| `value` | String | *Facultatief*. De invoerwaarde. |
| `maxAge` | Geheel | *Facultatieve* de tijd (in seconden) tot de ingang verloopt. Als items ontbreken, worden deze alleen voor de huidige sessie opgeslagen. |
| `attrs` | `Map<String, String>` | *Facultatief*. Een optionele lijst met entry-attributen. Voor alle veilige verbindingen met een veilige HTTP-verwijzingsheader wordt het kenmerk `SameSite` ingesteld op `None` . |


Om multitagging te ondersteunen (d.w.z. meerdere SDK-instanties in dezelfde eigenschap, die mogelijk naar verschillende organisaties verwijzen), worden alle statusvermeldingen automatisch vooraf vastgelegd met `kndctr_` en de URL-veilige organisatie-id.

Wanneer de client-SDK een `state:store` -greep in het antwoord ontvangt, moet deze het volgende doen:

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

Als u met browserclients werkt, kan de Edge Network automatisch doorgaan met de invoer als browsercookies. Dit staat transparante steun van de staatsopslag toe, aangezien browsers het protocol van het staatsbeheer door gebrek respecteren.

Bijna alle ingangen worden materialized als eerste partijkoekjes wanneer toegelaten en gesteund (zie de nota hieronder), maar de gateway kon sommige derdekoekjes ook opslaan wanneer de derde `adobedc.demdex.net` domein wordt gebruikt.

Aangezien de ingangen altijd aan een specifiek werkingsgebied (apparaat/toepassing) door hun definitie gebonden zijn, slechts zal de ondergroep die met de huidige verzoekcontext compatibel is door Edge Network worden geschreven. Ongeschreven items zijn
geretourneerd binnen een `state:store` -greep.

Normaliter worden items met toepassingsbereik altijd geschreven als cookies van de eerste partij, terwijl items met apparaatbereik worden geschreven als cookies van derden. Het besluit is volledig transparant aan de bezoeker, beslist de gateway welke ingangen, afhankelijk van de vraagcontext kunnen worden geschreven.

De aanroeper moet expliciet ondersteuning inschakelen voor het opslaan van de clientstatus als cookies, via de markering `meta.state.cookiesEnabled` :

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
| `cookiesEnabled` | Boolean | Als deze optie is ingesteld, wordt ondersteuning voor cookies ingeschakeld. De standaardwaarde is `false` . |
| `domain` | String | Vereist als `cookiesEnabled: true` . Het domein op hoofdniveau waarop de cookies moeten worden geschreven. De Edge Network gebruikt deze waarde om te bepalen of de status kan worden voortgezet als cookies. |

Zelfs als ondersteuning voor cookies wordt ingeschakeld via de markering `cookiesEnabled` , schrijft de Adobe Experience Platform Edge Network alleen de statusitems als de aanvraag voor het domein op het hoogste niveau overeenkomt met de `domain` die door de aanroeper is opgegeven. Wanneer er een probleem is, worden items geretourneerd in een `state:store` -greep.

U kunt de cookies van de eerste fabrikant niet schrijven (zelfs niet als ondersteuning is ingeschakeld) in de volgende gevallen:

* De aanvraag is afkomstig van het domein `adobedc.demdex.net` van derden.
* De aanvraag wordt uitgevoerd op een domein van de eerste partij `CNAME` , anders dan het domein dat door de aanroeper in `meta.state.domain` wordt opgegeven.

## Koekjesbeveiliging

Alle koekjes hebben de [&#x200B; Veilige vlag &#x200B;](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) toegelaten waar mogelijk.

Alle veilige koekjes hebben het [&#x200B; attribuut SameSite &#x200B;](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) geplaatst aan `None`, betekenend dat de koekjes in alle contexten, zowel 1st partij als dwars-oorsprong worden verzonden.

* Voor de eerste-partijkoekjes (`kndcrt_*`), wordt de `Secure` vlag slechts geplaatst wanneer de verzoekcontext veilig (HTTPS) is en wanneer verwijzer ([&#x200B; de Kopbal van HTTP van de Verwijzing &#x200B;](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) ook HTTPS is. Als de verwijzer niet veilig (HTTP) is, wordt de `Secure` vlag weggelaten om het Web SDK toe te staan om hen te lezen. Een beveiligde cookie kan niet worden gelezen vanuit een onveilige context.
* Voor het cookie van derden (demdex) wordt de markering `Secure` altijd ingesteld, aangezien alle aanvragen HTTPS zijn. De aanvraagcontext is dus veilig en deze cookie wordt nooit gelezen vanuit JavaScript.

De markering `Secure` is niet aanwezig in de metagegevensweergave van cookies. Alleen het kenmerk `SameSite` wordt opgenomen. In dit geval is het de verantwoordelijkheid van de client om de markering `Secure` correct in te stellen wanneer het kenmerk `SameSite` aanwezig is. Cookies met `SameSite=None` moeten ook het kenmerk `Secure` opgeven, omdat hiervoor een beveiligde context (HTTPS) is vereist.
