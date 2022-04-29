---
title: Identiteitsgegevens in het Web SDK van het Platform
description: Leer hoe u Adobe Experience Cloud-id's (ECID's) kunt ophalen en beheren met de Adobe Experience Platform Web SDK.
keywords: Identiteit;Identiteit eerste partij;Identiteitsdienst;Identiteit derde partij;Identiteitsmigratie;Identiteitskaart van de Bezoeker;Identiteitskaart;Identiteitskaart van derdePartijCookiesEnabled;idMigrationEnabled;getIdentiteit;syncIdentiteitskaart;Identiteitskaart;Primaire;Identiteitskaart Namespace;Naamruimte id;AuthenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 85ff35e0e7f7e892de5252e8f3ad069eff83aa15
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 0%

---

# Identiteitsgegevens in het Web SDK van het Platform

De Adobe Experience Platform Web SDK gebruikt [Adobe Experience Cloud-id&#39;s (ECID&#39;s)](../../identity-service/ecid.md) om het gedrag van de bezoeker bij te houden. Met behulp van ECID&#39;s kunt u ervoor zorgen dat elk apparaat een unieke id heeft die tijdens meerdere sessies kan blijven bestaan. Hierdoor worden alle treffers die tijdens en tussen websessies plaatsvinden, aan een specifiek apparaat gekoppeld.

Dit document biedt een overzicht van hoe u ECID&#39;s kunt beheren met de SDK van het Web Platform.

## ECID&#39;s bijhouden met de SDK

De SDK van het Web van de Platform wijst ECIDs door het gebruik van koekjes toe en volgt, met veelvoudige beschikbare methodes om te vormen hoe deze koekjes worden geproduceerd.

Wanneer een nieuwe gebruiker op uw website arriveert, probeert de Adobe Experience Cloud Identity Service een apparaatidentificatiecookie voor die gebruiker in te stellen. Voor nieuwe bezoekers wordt een ECID gegenereerd en geretourneerd in de eerste reactie van het Adobe Experience Platform Edge Network. Voor herhaalde bezoekers wordt de ECID opgehaald uit de `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` koekje en toegevoegd aan de lading door het Netwerk van de Rand.

Nadat het cookie met de ECID is ingesteld, bevat elk volgend verzoek dat door de Web SDK wordt gegenereerd, een gecodeerde ECID in het dialoogvenster `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie.

Wanneer het gebruiken van koekjes voor apparatenidentificatie, hebt u twee opties om met het Netwerk van de Rand in wisselwerking te staan:

1. Gegevens rechtstreeks verzenden naar het Edge Network-domein `adobedc.net`. Deze methode wordt [gegevensverzameling van derden](#third-party).
1. Creeer een NAAM op uw eigen domein dat richt aan `adobedc.net`. Deze methode wordt [eerste-partijgegevens verzamelen](#first-party).

Zoals in de onderstaande secties wordt uitgelegd, heeft de methode voor gegevensverzameling die u kiest, een directe invloed op de levensduur van cookies in verschillende browsers.

### Gegevensverzameling van derden {#third-party}

De gegevensinzameling van de derde impliceert het verzenden van gegevens rechtstreeks naar het domein van het Netwerk van de Rand `adobedc.net`.

De afgelopen jaren zijn webbrowsers steeds restrictiever geworden bij het verwerken van door derden ingestelde cookies. Sommige browsers blokkeren cookies van derden standaard. Als u cookies van derden gebruikt om sitebezoekers te identificeren, is de levensduur van deze cookies vrijwel altijd korter dan wat anders beschikbaar zou zijn in plaats daarvan met cookies van de eerste fabrikant. In sommige gevallen verloopt een cookie van een andere fabrikant over maar liefst zeven dagen.

Bovendien, wanneer de derdegegevensinzameling wordt gebruikt, beperken sommige en blokkeerders verkeer tot eindpunten van de Adobe- gegevensinzameling.

### Gegevensverzameling van eerste partijen {#first-party}

De eerste partij gegevensinzameling impliceert het plaatsen van koekjes door een CNAME op uw eigen domein dat aan richt `adobedc.net`.

Terwijl browsers lange behandelde koekjes hebben die door eindpunten van CNAME op een gelijkaardige manier aan die worden geplaatst door plaats-eigenlijke eindpunten worden geplaatst, hebben de recente veranderingen die door browsers worden uitgevoerd een onderscheid in gemaakt hoe de koekjes van CNAME worden behandeld. Hoewel er geen browsers zijn die CNAME-cookies van de eerste partij standaard blokkeren, beperken sommige browsers de levensduur van cookies die met een CNAME zijn ingesteld tot slechts zeven dagen.

### Effecten van de levensduur van cookies op Adobe Experience Cloud-toepassingen {#lifespans}

Ongeacht of u gegevensverzameling van de eerste of van derden kiest, heeft de tijdsduur dat een cookie kan aanhouden een directe invloed op het aantal bezoekers in Adobe Analytics en Customer Journey Analytics. Bovendien kunnen eindgebruikers inconsistente personalisatieervaringen ervaren wanneer Adobe Target of Offer decisioning op de site wordt gebruikt.

Neem bijvoorbeeld een situatie waarin u een verpersoonlijkingservaring hebt gemaakt waarmee elk artikel naar de homepage wordt gepromoot als een gebruiker het de afgelopen zeven dagen drie keer heeft bekeken.

Als een eindgebruiker drie keer per week bezoekt en vervolgens zeven dagen niet terugkeert naar de site, kan dat gebruik worden beschouwd als een nieuwe gebruiker wanneer hij of zij terugkeert naar de site omdat de cookies zijn verwijderd door een browserbeleid (afhankelijk van de browser die hij of zij gebruikte toen hij of zij de site bezocht). Als dit gebeurt, behandelt uw Analyse-hulpprogramma de bezoeker als een nieuwe gebruiker, ook al hebben ze de site iets meer dan zeven dagen geleden bezocht. Bovendien zal elke poging om de ervaring voor de gebruiker te personaliseren opnieuw beginnen.

### Apparaat-id&#39;s van eerste partij

Om rekening te houden met de effecten van de bovenstaande cookie levensduur, kunt u ervoor kiezen om uw eigen apparaat-id&#39;s in te stellen en te beheren. Zie de handleiding op [apparaat-id&#39;s van eerste partij](./first-party-device-ids.md) voor meer informatie .

## De ECID en het gebied voor de huidige gebruiker ophalen

Om unieke ECID voor de huidige bezoeker terug te winnen, gebruik `getIdentity` gebruiken. Voor nieuwe bezoekers die nog geen ECID hebben, genereert deze opdracht een nieuwe ECID. `getIdentity` retourneert ook de regio-id voor de bezoeker.

>[!NOTE]
>
>Deze methode wordt doorgaans gebruikt met aangepaste oplossingen die het lezen van de [!DNL Experience Cloud] ID of heb een locatietip nodig voor Adobe Audience Manager. Het wordt niet gebruikt door een standaardimplementatie.

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

## Gebruiken `identityMap`

Een XDM gebruiken [`identityMap` field](../../xdm/schema/composition.md#identityMap), kunt u een apparaat/gebruiker identificeren die veelvoudige identiteiten gebruikt, hun authentificatiestatus plaatsen, en beslissen welke herkenningsteken als primaire wordt beschouwd. Als er geen id is ingesteld als `primary`de primaire standaardinstellingen `ECID`.

`identityMap` velden worden bijgewerkt met de `sentEvent` gebruiken.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
});
```

Elke eigenschap binnen `identityMap` staat voor identiteiten die tot een bepaalde [naamruimte identity](../../identity-service/namespaces.md). De eigenschapsnaam moet het naamruimtesymbool voor de identiteit zijn. Dit symbool staat in de Adobe Experience Platform-gebruikersinterface onder &quot;[!UICONTROL Identities]&quot;. De eigenschapswaarde moet een array zijn met identiteiten die betrekking hebben op die naamruimte identity.

Elk identiteitsobject in de array identities bevat de volgende eigenschappen:

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `id` | Tekenreeks | **(Vereist)** De id die u voor de opgegeven naamruimte wilt instellen. |
| `authenticationState` | Tekenreeks | **(Vereist)** De verificatiestatus van de id. Mogelijke waarden zijn `ambiguous`, `authenticated`, en `loggedOut`. |
| `primary` | Boolean | Hiermee wordt bepaald of deze identiteit moet worden gebruikt als primair fragment in het profiel. Standaard wordt de ECID ingesteld als de primaire id voor de gebruiker. Indien weggelaten, wordt deze waarde standaard ingesteld op `false`. |

## Migreren van Bezoeker-API naar ECID

Wanneer u migreert vanuit de Bezoeker-API, kunt u ook bestaande AMCV-cookies migreren. Als u ECID-migratie wilt inschakelen, stelt u de `idMigrationEnabled` in de configuratie. Bij ID-migratie zijn de volgende gebruiksgevallen mogelijk:

* Wanneer sommige pagina&#39;s van een domein de bezoeker-API gebruiken en andere pagina&#39;s deze SDK gebruiken. Ter ondersteuning van dit geval leest de SDK bestaande AMCV-cookies en schrijft hij een nieuw cookie met de bestaande ECID. Daarnaast schrijft de SDK AMCV-cookies zodat, als de ECID als eerste wordt verkregen op een pagina die van instrumenten is voorzien met de SDK, de volgende pagina&#39;s die van instrumenten zijn voorzien met de Bezoeker-API dezelfde ECID hebben.
* Wanneer de SDK van het Web van Adobe Experience Platform opstelling op een pagina is die ook bezoeker API heeft. Ter ondersteuning van dit geval zoekt de SDK, als het AMCV-cookie niet is ingesteld, naar de Bezoeker-API op de pagina en roept deze aan om de ECID op te halen.
* Wanneer de hele site gebruikmaakt van Adobe Experience Platform Web SDK en geen API voor bezoekers heeft, is het handig om de ECID&#39;s te migreren zodat de informatie van de retourbezoeker behouden blijft. Nadat SDK wordt opgesteld met `idMigrationEnabled` gedurende een bepaalde periode, zodat de meeste bezoekerscookies worden gemigreerd, kan de instelling worden uitgeschakeld.

### Functies voor migratie bijwerken

Wanneer gegevens met XDM-indeling naar Audience Manager worden verzonden, moeten deze gegevens tijdens het migreren worden omgezet in signalen. Uw kenmerken moeten worden bijgewerkt met de nieuwe sleutels die XDM biedt. Dit proces wordt vergemakkelijkt door gebruik te maken van de [BAAAM, gereedschap](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) die Audience Manager heeft gecreëerd.

## Gebruiken in gebeurtenis door:sturen

Als u momenteel [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) ingeschakeld en gebruikt `appmeasurement.js` en `visitor.js`, kunt u gebeurtenis-door:sturen toegelaten eigenschap houden en dit zal geen kwesties veroorzaken. Op het achterste eind, haalt Adobe om het even welke AAM segmenten en voegt hen aan de vraag aan Analytics toe. Als de aanroep naar Analytics deze segmenten bevat, roept Analytics geen Audience Manager aan om gegevens door te sturen, zodat er geen dubbele gegevensverzameling is. Er is ook geen behoefte aan de Hint van de Plaats wanneer het gebruiken van SDK van het Web omdat de zelfde segmentatie eindpunten in het achtereind worden geroepen.
