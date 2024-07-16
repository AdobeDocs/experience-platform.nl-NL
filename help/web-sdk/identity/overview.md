---
title: Identiteitsgegevens in Web SDK
description: Leer hoe u Adobe Experience Cloud-id's (ECID's) kunt ophalen en beheren met de Adobe Experience Platform Web SDK.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: b8c38108e7481a5c4e94e4122e0093fa6f00b96c
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 0%

---

# Identiteitsgegevens in Web SDK

Het Web SDK van Adobe Experience Platform gebruikt [ Adobe Experience Cloud IDs (ECIDs) ](../../identity-service/features/ecid.md) om bezoekersgedrag te volgen. Met behulp van ECID&#39;s kunt u ervoor zorgen dat elk apparaat een unieke id heeft die tijdens meerdere sessies kan blijven bestaan. Hierdoor worden alle treffers die tijdens en tussen websessies plaatsvinden, aan een specifiek apparaat gekoppeld.

Dit document biedt een overzicht van hoe u ECID&#39;s kunt beheren met de Platform Web SDK.

## ECID&#39;s bijhouden met de SDK

De SDK van het Web van het Platform wijst ECIDs toe en volgt door koekjes te gebruiken, met veelvoudige beschikbare methodes om te vormen hoe deze koekjes worden geproduceerd.

Wanneer een nieuwe gebruiker op uw website arriveert, probeert de Adobe Experience Cloud Identity Service een apparaatidentificatiecookie voor die gebruiker in te stellen. Voor nieuwe bezoekers wordt een ECID gegenereerd en geretourneerd in de eerste reactie van de Adobe Experience Platform-Edge Network. Voor herhaalde bezoekers wordt de ECID opgehaald uit het `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -cookie en door de Edge Network toegevoegd aan de payload.

Nadat het cookie met de ECID is ingesteld, bevat elke volgende aanvraag die door de Web SDK wordt gegenereerd, een gecodeerde ECID in het `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` -cookie.

Wanneer u cookies gebruikt voor apparaatidentificatie, hebt u twee opties voor interactie met de Edge Network:

1. Gegevens rechtstreeks verzenden naar het domein Edge Network `adobedc.net` . Deze methode wordt bedoeld als [ de inzameling van derdegegevens ](#third-party).
1. Creeer een NAAM op uw eigen domein dat aan `adobedc.net` richt. Deze methode wordt bedoeld als [ de inzameling van eerste partijgegevens ](#first-party).

Zoals in de onderstaande secties wordt uitgelegd, heeft de methode voor gegevensverzameling die u kiest, een directe invloed op de levensduur van cookies in verschillende browsers.

### Gegevensverzameling van derden {#third-party}

Bij gegevensverzameling van derden worden gegevens rechtstreeks naar het domein van de Edge Network verzonden `adobedc.net` .

De afgelopen jaren zijn webbrowsers steeds restrictiever geworden bij het verwerken van door derden ingestelde cookies. Sommige browsers blokkeren cookies van derden standaard. Als u cookies van derden gebruikt om sitebezoekers te identificeren, is de levensduur van deze cookies vrijwel altijd korter dan wat anders beschikbaar zou zijn in plaats daarvan met cookies van de eerste fabrikant. Soms verloopt een cookie van een andere fabrikant binnen maar liefst zeven dagen.

Ook, wanneer de derdegegevensinzameling wordt gebruikt, beperken sommige en blokkeerders verkeer tot eindpunten van de gegevensinzameling van de Adobe.

### Gegevensverzameling van eerste partijen {#first-party}

De gegevensinzameling van de eerste partij impliceert het plaatsen van koekjes door een CNAME op uw eigen domein dat aan `adobedc.net` richt.

Terwijl browsers lange behandelde koekjes hebben die door eindpunten van CNAME op een gelijkaardige manier aan die worden geplaatst door plaats-eigenlijke eindpunten worden geplaatst, hebben de recente veranderingen die door browsers worden uitgevoerd een onderscheid in gemaakt hoe de koekjes van CNAME worden behandeld. Hoewel er geen browsers zijn die CNAME-cookies van de eerste partij standaard blokkeren, beperken sommige browsers de levensduur van cookies die met een CNAME zijn ingesteld tot slechts zeven dagen.

### Effecten van de levensduur van cookies op Adobe Experience Cloud-toepassingen {#lifespans}

Ongeacht of u gegevensverzameling van de eerste of van de derde partij kiest, heeft de tijdsduur dat een cookie kan aanhouden een directe invloed op het aantal bezoekers in Adobe Analytics en Customer Journey Analytics. Ook kunnen eindgebruikers inconsistente personalisatieervaringen ervaren wanneer Adobe Target of Offer decisioning op de site wordt gebruikt.

Neem bijvoorbeeld een situatie waarin u een personaliseringservaring hebt gemaakt waarmee elk item op de homepage wordt bevorderd als een gebruiker dit de afgelopen zeven dagen drie keer heeft bekeken.

Als een eindgebruiker drie keer per week bezoekt en vervolgens zeven dagen niet terugkeert naar de site, kan die gebruiker worden beschouwd als een nieuwe gebruiker wanneer hij of zij terugkeert naar de site omdat de cookies zijn verwijderd door een browserbeleid (afhankelijk van de browser die hij of zij gebruikte toen hij of zij de site bezocht). Als dit gebeurt, behandelt uw Analyse-hulpprogramma de bezoeker als een nieuwe gebruiker, ook al hebben ze de site iets meer dan zeven dagen geleden bezocht. Bovendien begint elke poging om de gebruikerservaring aan te passen opnieuw.

### Apparaat-id&#39;s van eerste partij

Om rekening te houden met de effecten van de bovenstaande cookie levensduur, kunt u ervoor kiezen om uw eigen apparaat-id&#39;s in te stellen en te beheren. Zie de gids op [ eerste-partijapparaat IDs ](./first-party-device-ids.md) voor meer informatie.

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
| `authenticationState` | String | **(Vereist)** De authentificatiestatus van identiteitskaart Mogelijke waarden zijn `ambiguous` , `authenticated` en `loggedOut` . |
| `primary` | Boolean | Hiermee wordt bepaald of deze identiteit moet worden gebruikt als primair fragment in het profiel. Standaard wordt de ECID ingesteld als de primaire id voor de gebruiker. Als deze waarde wordt weggelaten, wordt deze standaard ingesteld op `false` . |

Als u het veld `identityMap` gebruikt om apparaten of gebruikers te identificeren, leidt dit tot hetzelfde resultaat als wanneer u de methode [`setCustomerIDs` ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) van de [!DNL ID Service API] . Zie de [ API documentatie van de Dienst van identiteitskaart ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) voor meer details.

## Migreren van Bezoeker-API naar ECID

Wanneer u migreert vanuit de Bezoeker-API, kunt u ook bestaande AMCV-cookies migreren. Als u ECID-migratie wilt inschakelen, stelt u de parameter `idMigrationEnabled` in de configuratie in. Bij ID-migratie zijn de volgende gebruiksgevallen mogelijk:

* Wanneer sommige pagina&#39;s van een domein de bezoeker-API gebruiken en andere pagina&#39;s deze SDK gebruiken. Ter ondersteuning van dit geval leest de SDK bestaande AMCV-cookies en schrijft hij een nieuw cookie met de bestaande ECID. De SDK schrijft ook AMCV-cookies zodat, als de ECID als eerste wordt verkregen op een pagina die van instrumenten is voorzien met de SDK, de volgende pagina&#39;s die van instrumenten zijn voorzien met de Bezoeker-API dezelfde ECID hebben.
* Wanneer de SDK van het Web van Adobe Experience Platform opstelling op een pagina is die ook bezoeker API heeft. Ter ondersteuning van dit geval zoekt de SDK, als het AMCV-cookie niet is ingesteld, naar de Bezoeker-API op de pagina en roept deze aan om de ECID op te halen.
* Wanneer de hele site gebruikmaakt van Adobe Experience Platform Web SDK en geen API voor bezoekers heeft, is het handig om de ECID&#39;s te migreren zodat de geretourneerde bezoekersinformatie behouden blijft. Nadat de SDK gedurende een tijd is geïmplementeerd met `idMigrationEnabled` , zodat het merendeel van de cookies van de bezoeker wordt gemigreerd, kan de instelling worden uitgeschakeld.

### Functies voor migratie bijwerken

Wanneer gegevens met XDM-indeling naar Audience Manager worden verzonden, moeten deze gegevens tijdens het migreren naar signalen worden geconverteerd. Uw kenmerken moeten worden bijgewerkt om de nieuwe sleutels te weerspiegelen die XDM verstrekt. Dit proces wordt gemakkelijker gemaakt door het [ hulpmiddel BAAAM ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) te gebruiken dat de Audience Manager heeft gecreeerd.

## Gebruiken in gebeurtenis door:sturen

Als u momenteel [ gebeurtenis door:sturen ](../../tags/ui/event-forwarding/overview.md) toegelaten hebt en `appmeasurement.js` en `visitor.js` gebruikt, kunt u toegelaten gebeurtenis-door:sturen eigenschap houden en dit zal geen kwesties veroorzaken. Op het achterste eind, haalt de Adobe om het even welke AAM segmenten en voegt hen aan de vraag aan Analytics toe. Als de vraag aan Analytics die segmenten bevat, zal Analytics geen Audience Manager roepen om het even welke gegevens door:sturen, zodat is er geen dubbele gegevensinzameling. Er is ook geen behoefte aan de Hint van de Plaats wanneer het gebruiken van SDK van het Web omdat de zelfde segmentatie eindpunten in het achtereind worden geroepen.
