---
title: Identiteitsgegevens in Web SDK
description: Leer hoe u Adobe Experience Cloud-id's (ECID's) kunt ophalen en beheren met de Adobe Experience Platform Web SDK.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 3724c43090e37d21384e9dfe45e60ee2eec68a81
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 0%

---


# Identiteitsgegevens in Web SDK

Het Web SDK van Adobe Experience Platform gebruikt [ Adobe Experience Cloud IDs (ECIDs) ](../../identity-service/features/ecid.md) om bezoekersgedrag te volgen. Met [!DNL ECIDs] kunt u ervoor zorgen dat elk apparaat een unieke id heeft die tijdens meerdere sessies kan blijven bestaan, zodat alle resultaten die tijdens en tussen websessies optreden, worden gekoppeld aan een specifiek apparaat.

Dit document biedt een overzicht van het beheren van [!DNL ECIDs] en [!DNL CORE IDs] met de Web SDK.

## ECID&#39;s bijhouden met Web SDK {#tracking-ecids-web-sdk}

Het Web SDK wijst en volgt [!DNL ECIDs] toe door koekjes te gebruiken, met veelvoudige beschikbare methodes om te vormen hoe deze koekjes worden geproduceerd.

Wanneer een nieuwe gebruiker op uw website aankomt, probeert de [ Dienst van de Identiteit van Adobe Experience Cloud ](../../identity-service/home.md) om een koekje van de apparatenidentificatie voor die gebruiker te plaatsen.

* Voor nieuwe bezoekers wordt een [!DNL ECID] gegenereerd en geretourneerd in de eerste reactie van de Edge Network van het Experience Platform.
* Voor het retourneren van bezoekers wordt [!DNL ECID] opgehaald uit het `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -cookie en door de Edge Network toegevoegd aan de payload van de aanvraag.

Nadat de cookie met [!DNL ECID] is ingesteld, bevat elke volgende aanvraag die door de Web SDK wordt gegenereerd, een gecodeerde [!DNL ECID] in het `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -cookie.

Wanneer u cookies gebruikt voor apparaatidentificatie, hebt u twee manieren om te werken met de Edge Network:

1. Creeer een NAAM op uw eigen domein dat aan `adobedc.net` richt. Deze methode wordt bedoeld als [ de inzameling van eerste partijgegevens ](#first-party).
1. Gegevens rechtstreeks verzenden naar het domein Edge Network `adobedc.net` . Deze methode wordt bedoeld als [ de inzameling van derdegegevens ](#third-party).

Zoals in de onderstaande secties wordt uitgelegd, heeft de methode voor gegevensverzameling die u kiest, een directe invloed op de levensduur van cookies in verschillende browsers.

## CORE-id&#39;s bijhouden met Web SDK {#tracking-coreid-web-sdk}

Als u Google Chrome gebruikt en cookies van derden hebt ingeschakeld en er geen `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -cookie is ingesteld, wordt het eerste verzoek om Edge Network uitgevoerd via een `demdex.net` -domein, dat een demdex-cookie instelt. Deze cookie bevat een [!DNL CORE ID] . Dit is een unieke gebruiker-id die afwijkt van de [!DNL ECID] .

Afhankelijk van uw implementatie, zou u [ tot  [!DNL CORE ID]](#retrieve-coreid) kunnen willen toegang hebben.

### Gegevensverzameling van eerste partijen {#first-party}

Voor het eerst verzamelen van gegevens moet u cookies instellen via een `CNAME` -lus in uw eigen domein dat naar `adobedc.net` wijst.

Hoewel browsers cookies die door `CNAME` eindpunten zijn ingesteld lang op dezelfde manier hebben verwerkt als de cookies die door de eindpunten van de site worden ingesteld, hebben recente wijzigingen die door browsers zijn geïmplementeerd, een verschil gemaakt in de manier waarop `CNAME` -cookies worden verwerkt. Hoewel er momenteel geen browsers zijn die `CNAME` cookies van de eerste partij standaard blokkeren, beperken sommige browsers de levensduur van cookies die met een `CNAME` zijn ingesteld tot slechts zeven dagen.

### Gegevensverzameling van derden {#third-party}

Bij gegevensverzameling van derden worden gegevens rechtstreeks naar het domein van de Edge Network verzonden `adobedc.net` .

De afgelopen jaren zijn webbrowsers steeds restrictiever geworden bij het verwerken van door derden ingestelde cookies. Sommige browsers blokkeren cookies van derden standaard. Als u cookies van derden gebruikt om sitebezoekers te identificeren, is de levensduur van deze cookies vrijwel altijd korter dan wat anders beschikbaar zou zijn in plaats daarvan met cookies van de eerste fabrikant. Soms verloopt een cookie van een andere fabrikant binnen maar liefst zeven dagen.

Ook, wanneer het gebruiken van derdegegevensinzameling, beperken sommige en blokkeerders verkeer tot eindpunten van de gegevensinzameling van de Adobe.

### Effecten van de levensduur van cookies op Adobe Experience Cloud-toepassingen {#lifespans}

Ongeacht of u eerste-partij of derdegegevensinzameling kiest, kan de tijdsduur een koekje een directe invloed op bezoekersaantallen in [ Adobe Analytics ](https://experienceleague.adobe.com/en/docs/analytics) en [ Customer Journey Analytics ](https://experienceleague.adobe.com/en/docs/customer-journey-analytics) aanhouden. Ook, kunnen de eindgebruikers inconsistente verpersoonlijkingservaringen ervaren wanneer [ Adobe Target ](https://experienceleague.adobe.com/en/docs/target) of [ Offer decisioning ](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision) op de plaats wordt gebruikt.

Neem bijvoorbeeld een situatie waarin u een personaliseringservaring hebt gemaakt waarmee elk item op de homepage wordt bevorderd als een gebruiker dit de afgelopen zeven dagen drie keer heeft bekeken.

Als een eindgebruiker drie keer per week bezoekt en vervolgens zeven dagen niet terugkeert naar de site, kan die gebruiker worden beschouwd als een nieuwe gebruiker wanneer hij of zij terugkeert naar de site omdat de cookies zijn verwijderd door een browserbeleid (afhankelijk van de browser die hij of zij gebruikte toen hij of zij de site bezocht). Als dit gebeurt, behandelt uw Analyse-hulpprogramma de bezoeker als een nieuwe gebruiker, ook al hebben ze de site iets meer dan zeven dagen geleden bezocht. Bovendien begint elke poging om de gebruikerservaring aan te passen opnieuw.

### FPID&#39;s (First-party device ID&#39;s) {#fpid}

Als u rekening wilt houden met de effecten van de levensduur van cookies zoals hierboven beschreven, kunt u uw eigen apparaat-id&#39;s instellen en beheren. Zie de gids op [ eerste-partijapparaat IDs ](./first-party-device-ids.md) voor meer informatie.

## De ECID en het gebied voor de huidige gebruiker ophalen {#retrieve-ecid}

Afhankelijk van uw gebruiksgeval zijn er twee manieren waarop u toegang kunt krijgen tot [!DNL ECID] :

* [ wint  [!DNL ECID]  door Gegevens voor de Inzameling van Gegevens ](#retrieve-ecid-data-prep) terug: Dit is de geadviseerde methode die u zou moeten gebruiken.
* [ wint  [!DNL ECID]  door het `getIdentity()` bevel ](#retrieve-ecid-getidentity) terug: Gebruik slechts deze methode wanneer u de [!DNL ECID] informatie op de cliënt-kant vereist.

### De [!DNL ECID] ophalen via Data Prep voor gegevensverzameling {#retrieve-ecid-data-prep}

Het gebruik [ Prep van Gegevens voor de Inzameling van Gegevens ](../../datastreams/data-prep.md) om [!DNL ECID] aan een [!DNL XDM] gebied in kaart te brengen. Dit is de aanbevolen manier om toegang te krijgen tot [!DNL ECID] .

U doet dit door het bronveld in te stellen op het volgende pad:

```js
xdm.identityMap.ECID[0].id
```

Stel het doelveld vervolgens in op een XDM-pad waar het veld van het type `string` is.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### De [!DNL ECID] ophalen via de opdracht `getIdentity()` {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>U moet de ECID alleen via de opdracht `getIdentity()` ophalen als u de instructie [!DNL ECID] aan de clientzijde nodig hebt. Als u slechts ECID aan een XDM gebied wilt in kaart brengen, gebruik [ Prep van Gegevens voor de Inzameling van Gegevens ](#retrieve-ecid-data-prep) in plaats daarvan.

Gebruik de opdracht `getIdentity` om de unieke ECID voor de huidige bezoeker op te halen. Voor nieuwe bezoekers die nog geen [!DNL ECID] hebben, genereert deze opdracht een nieuwe [!DNL ECID] . `getIdentity` retourneert ook de regio-id voor de bezoeker.

>[!NOTE]
>
>Deze methode wordt meestal gebruikt met aangepaste oplossingen waarvoor de [!DNL Experience Cloud] -id moet worden gelezen of waarvoor een locatiehint voor Adobe Audience Manager nodig is. Het wordt niet gebruikt door een standaardimplementatie.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## De CORE-id voor de huidige gebruiker ophalen {#retrieve-coreid}

Als u de CORE-id voor een gebruiker wilt ophalen, gebruikt u de opdracht [`getIdentity()`](../commands/getidentity.md) , zoals hieronder wordt weergegeven.

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```


## `identityMap` gebruiken {#using-identitymap}

Gebruikend een XDM [`identityMap` gebied ](../../xdm/schema/composition.md#identityMap), kunt u een apparaat/een gebruiker identificeren gebruikend veelvoudige identiteiten, hun authentificatiestatus plaatsen, en beslissen welke herkenningsteken als primaire wordt beschouwd. Als er geen id is ingesteld als `primary` , wordt standaard de waarde `ECID` gebruikt.

`identityMap` -velden worden bijgewerkt met de opdracht `sentEvent` .

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>Adobe raadt aan naamruimten die een persoon, zoals `CRMID` , als primaire identiteit vertegenwoordigen, te verzenden.


Elk bezit binnen `identityMap` vertegenwoordigt identiteiten die tot een bepaalde [ identiteit namespace ](../../identity-service/features/namespaces.md) behoren. De bezitsnaam zou het symbool van identiteitskaart namespace moeten zijn, die u in het gebruikersinterface van Adobe Experience Platform onder &quot;[!UICONTROL Identities]&quot;kunt vinden. De eigenschapswaarde moet een array zijn met identiteiten die betrekking hebben op die naamruimte identity.

>[!IMPORTANT]
>
>De naamruimte-id die in de `identityMap` wordt doorgegeven, is hoofdlettergevoelig. Gebruik de juiste naamruimte-id om onvolledige gegevensverzameling te voorkomen.

Elk identiteitsobject in de array identities bevat de volgende eigenschappen:

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `id` | String | **(Vereist)** identiteitskaart die u voor bepaalde namespace wilt plaatsen. |
| `authenticatedState` | String | **(Vereist)** De authentificatiestatus van identiteitskaart Mogelijke waarden zijn `ambiguous` , `authenticated` en `loggedOut` . |
| `primary` | Boolean | Hiermee wordt bepaald of deze identiteit moet worden gebruikt als primair fragment in het profiel. Standaard wordt de ECID ingesteld als de primaire id voor de gebruiker. Als deze waarde wordt weggelaten, wordt deze standaard ingesteld op `false` . |

Als u het veld `identityMap` gebruikt om apparaten of gebruikers te identificeren, leidt dit tot hetzelfde resultaat als wanneer u de methode [`setCustomerIDs` ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) van de [!DNL ID Service API] . Zie de [ API documentatie van de Dienst van identiteitskaart ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) voor meer details.

## Migreren van Bezoeker-API naar ECID {#migrating-visitor-api-ecid}

Wanneer u migreert vanuit de Bezoeker-API, kunt u ook bestaande AMCV-cookies migreren. Als u ECID-migratie wilt inschakelen, stelt u de parameter `idMigrationEnabled` in de configuratie in. Bij ID-migratie zijn de volgende gebruiksgevallen mogelijk:

* Wanneer sommige pagina&#39;s van een domein de bezoeker-API gebruiken en andere pagina&#39;s deze SDK gebruiken. Ter ondersteuning van dit geval leest de SDK bestaande AMCV-cookies en schrijft een nieuwe cookie met de bestaande ECID. Bovendien schrijft de SDK de cookies van AMCV zodanig dat als de ECID als eerste wordt verkregen op een pagina die van instrumenten is voorzien met de SDK, de volgende pagina&#39;s die van instrumenten voorzien zijn met de API van de Bezoeker dezelfde ECID hebben.
* Als Adobe Experience Platform Web SDK is ingesteld op een pagina die ook de Bezoeker-API heeft. Ter ondersteuning van dit geval zoekt de SDK op de pagina naar de Bezoeker-API en roept deze op om de ECID op te halen als het AMCV-cookie niet is ingesteld.
* Wanneer de hele site Adobe Experience Platform Web SDK gebruikt en geen API voor bezoekers heeft, is het handig om de ECID&#39;s te migreren zodat de informatie van de geretourneerde bezoeker behouden blijft. Nadat de SDK gedurende een tijd is geïmplementeerd met `idMigrationEnabled` , zodat de meeste cookies van de bezoeker worden gemigreerd, kan de instelling worden uitgeschakeld.

### Functies voor migratie bijwerken

Wanneer gegevens met XDM-indeling naar Audience Manager worden verzonden, moeten deze gegevens tijdens het migreren naar signalen worden geconverteerd. Uw kenmerken moeten worden bijgewerkt om de nieuwe sleutels te weerspiegelen die XDM verstrekt. Dit proces wordt gemakkelijker gemaakt door het [ hulpmiddel BAAAM ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) te gebruiken dat de Audience Manager heeft gecreeerd.

## Gebruiken in gebeurtenis door:sturen

Als u momenteel [ gebeurtenis door:sturen ](../../tags/ui/event-forwarding/overview.md) toegelaten hebt en `appmeasurement.js` en `visitor.js` gebruikt, kunt u toegelaten gebeurtenis-door:sturen eigenschap houden en dit zal geen kwesties veroorzaken. Op het achterste eind, haalt de Adobe om het even welke AAM segmenten en voegt hen aan de vraag aan Analytics toe. Als de vraag aan Analytics die segmenten bevat, zal Analytics geen Audience Manager roepen om het even welke gegevens door:sturen, zodat is er geen dubbele gegevensinzameling. Er is ook geen behoefte aan de Hint van de Plaats wanneer het gebruiken van het Web SDK omdat de zelfde segmentatie eindpunten in het achterste eind worden geroepen.
