---
title: Experience Cloud-id's ophalen met de SDK van Adobe Experience Platform Web
description: Leer hoe u Adobe Experience Cloud-id's (ECID's) ophaalt met de Adobe Experience Platform Web SDK.
seo-description: Meer weten over Adobe Experience Cloud-id?
keywords: Identiteit;Identiteit eerste partij;Identiteitsdienst;Identiteit derde partij;Identiteitsmigratie;Identiteitskaart van de Bezoeker;Identiteitskaart;Identiteitskaart van derdePartijCookiesEnabled;idMigrationEnabled;getIdentiteit;syncIdentiteitskaart;Identiteitskaart;primaire;Identiteitskaart Namespace;Naamruimte ID;AuthentificatieStaat;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: d753cfca6f518dfe2cafa1cb30ad26bd0b591c54
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 0%

---

# Adobe Experience Cloud-id&#39;s

Adobe Experience Platform Web SDK gebruikt [Adobe Identity Service](../../identity-service/ecid.md). Dit zorgt ervoor dat elk apparaat een unieke id heeft die op het apparaat blijft bestaan, zodat de activiteit tussen pagina&#39;s aan elkaar kan worden gekoppeld.

## Identiteit van eerste partij

[!DNL Identity Service] slaat de identiteit in een koekje in een eerstepartijdomein op. De [!DNL Identity Service] probeert om het koekje te plaatsen gebruikend een kopbal van HTTP op het domein. Als dat mislukt, valt [!DNL Identity Service] terug naar het instellen van cookies met JavaScript. Men adviseert dat u opstelling een NAAM voor uw [Domein van de Rand config](../fundamentals/configuring-the-sdk.md#edgeConfigId).

Elke klap die uit SDK van het Web van het Platform komt heeft ECID toegevoegd aan het door de Dienst van de Identiteit op het Netwerk van de Rand. Voor nieuwe bezoekers wordt de ECID gegenereerd en toegevoegd aan de lading. Voor herhaalde bezoekers wordt de ECID opgehaald uit het cookie `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` en toegevoegd aan de payload.

De ECID wordt toegevoegd onder het veld `identityMap` in uw `xdm`. Met het hulpprogramma dev van de browser kunt u de ECID in het antwoord onder de payload bekijken met het type: `identity:result`, maar u kunt ECID niet in het verzoek zien.

De implementaties van CNAME staan u toe om het inzamelingsdomein aan te passen dat door Adobe wordt gebruikt zodat zij uw eigen domein aanpassen. Op deze manier kan Adobe cookies van de eerste partij op de server instellen in plaats van op de client via JavaScript. In het verleden golden voor deze eersteklas cookies aan de serverzijde geen beperkingen die waren opgelegd in het ITP-beleid (Intelligent Tracking Prevention, intelligente traceringspreventie) van Apple voor Safari-browsers. In november 2020 heeft Apple echter het beleid bijgewerkt, zodat deze beperkingen ook werden toegepast op cookies die via CNAME zijn ingesteld. Momenteel geldt dat zowel cookies die door CNAME op de server zijn ingesteld als cookies die door JavaScript op de client zijn ingesteld, beperkt zijn tot een vervaldatum van 7 dagen of 24 uur onder ITP. Voor meer informatie over het beleid ITP, zie dit document van Apple over [het volgen preventie](https://webkit.org/tracking-prevention/#intelligent-tracking-prevention-itp).

Terwijl een implementatie CNAME geen voordelen in termen van koekjesleven verstrekt, kunnen er sommige andere voordelen zoals ad blokkers en minder gemeenschappelijke browsers zijn die gegevens verhinderen worden verzonden naar domeinen die zij als Trackers classificeren. In die gevallen, zou het gebruiken van een NAAM uw gegevensinzameling voor gebruikers kunnen verhinderen worden verstoord die deze hulpmiddelen gebruiken.

## Identiteit van derden

[!DNL Identity Service] heeft de capaciteit om een identiteitskaart met een derdedomein (demdex.net) te synchroniseren om het volgen over plaatsen toe te laten. Wanneer dit wordt toegelaten zal het eerste verzoek voor een bezoeker (bijvoorbeeld, iemand zonder ECID) aan demdex.net worden gemaakt. Dit zal slechts op browsers worden gedaan die het (zoals Chrome) toestaan en door de `thirdPartyCookiesEnabled` parameter in de configuratie wordt gecontroleerd. Als u deze eigenschap allen samen zou willen onbruikbaar maken, plaats `thirdPartyCookiesEnabled` aan vals.

## ID-migratie

Wanneer u migreert vanuit de Bezoeker-API, kunt u ook bestaande AMCV-cookies migreren. Om migratie toe te laten ECID, plaats de `idMigrationEnabled` parameter in de configuratie. Bij ID-migratie zijn de volgende gebruiksgevallen mogelijk:

* Wanneer sommige pagina&#39;s van een domein de bezoeker-API gebruiken en andere pagina&#39;s deze SDK gebruiken. Ter ondersteuning van dit geval leest de SDK bestaande AMCV-cookies en schrijft hij een nieuw cookie met de bestaande ECID. Daarnaast schrijft de SDK AMCV-cookies zodat, als de ECID als eerste wordt verkregen op een pagina die van instrumenten is voorzien met de SDK, de volgende pagina&#39;s die van instrumenten zijn voorzien met de Bezoeker-API dezelfde ECID hebben.
* Wanneer de SDK van het Web van Adobe Experience Platform opstelling op een pagina is die ook bezoeker API heeft. Ter ondersteuning van dit geval zoekt de SDK, als het AMCV-cookie niet is ingesteld, naar de Bezoeker-API op de pagina en roept deze aan om de ECID op te halen.
* Wanneer de hele site gebruikmaakt van Adobe Experience Platform Web SDK en geen API voor bezoekers heeft, is het handig om de ECID&#39;s te migreren zodat de informatie van de retourbezoeker behouden blijft. Nadat de SDK gedurende een bepaalde periode is geïmplementeerd met `idMigrationEnabled`, zodat de meeste cookies van de bezoeker worden gemigreerd, kan de instelling worden uitgeschakeld.

## Functies voor migratie bijwerken

Wanneer gegevens met XDM-indeling naar Audience Manager worden verzonden, moeten deze gegevens tijdens het migreren worden omgezet in signalen. Uw kenmerken moeten worden bijgewerkt met de nieuwe sleutels die XDM biedt. Dit proces wordt gemakkelijker gemaakt door het [hulpmiddel BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) te gebruiken die Audience Manager heeft gecreeerd.

## Server Side Forwarding

Als u momenteel server side door:sturen toegelaten hebt en `appmeasurement.js` gebruikt. en `visitor.js` kunt u de functie voor het doorsturen aan de serverzijde ingeschakeld houden, wat geen problemen veroorzaakt. In het achterste eind, haalt Adobe om het even welke AAM segmenten en voegt hen aan de vraag aan Analytics toe. Als de aanroep naar Analytics deze segmenten bevat, roept Analytics geen Audience Manager aan om gegevens door te sturen, zodat er geen dubbele gegevensverzameling is. Er is ook geen behoefte aan de Hint van de Plaats wanneer het gebruiken van SDK van het Web omdat de zelfde segmentatie eindpunten in het achtereind worden geroepen.

## De bezoeker-id en regio-id ophalen

Als u de unieke bezoekersidentiteitskaart wilt gebruiken, gebruik `getIdentity` bevel. `getIdentity` retourneert de bestaande ECID voor de huidige bezoeker. Voor nieuwe bezoekers die nog geen ECID hebben, genereert deze opdracht een nieuwe ECID. `getIdentity` retourneert ook de regio-id voor de bezoeker. Zie [Adobe Audience Manager User Guide](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html) voor meer informatie.

>[!NOTE]
>
>Deze methode wordt doorgaans gebruikt met aangepaste oplossingen die het lezen van de [!DNL Experience Cloud]-id vereisen of die de Adobe Audience Manager-locatiehint nodig hebben. Het wordt niet gebruikt door een standaardimplementatie.

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

## Identiteiten synchroniseren

>[!NOTE]
>
>De methode `syncIdentity` is verwijderd in versie 2.1.0, naast de hash eigenschap. Als u versie 2.1.0+ gebruikt en identiteiten wilt synchroniseren, kunt u hen direct in de `xdm` optie van `sendEvent`, onder het `identityMap` gebied verzenden.

Daarnaast kunt u met de opdracht [!DNL Identity Service] uw eigen id&#39;s synchroniseren met de ECID.`syncIdentity`

>[!NOTE]
>
>Het wordt hoogst geadviseerd om alle beschikbare identiteiten op elk `sendEvent` bevel over te gaan. Dit ontgrendelt een reeks gebruiksgevallen, waaronder personalisatie. Nu u die identiteiten in het `sendEvent` bevel kunt overgaan, kunnen zij direct in uw DataLayer worden geplaatst.

Door identiteiten te synchroniseren kunt u een apparaat/gebruiker identificeren met behulp van meerdere identiteiten, de verificatiestatus instellen en bepalen welke id als de primaire id wordt beschouwd. Als er geen id is ingesteld als `primary`, worden de primaire standaardinstellingen `ECID`.

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

Elke eigenschap in `identityMap` vertegenwoordigt identiteiten die behoren tot een bepaalde [naamruimte](../../identity-service/namespaces.md). De eigenschapnaam moet het naamruimtesymbool voor de identiteit zijn. Dit wordt weergegeven in de Adobe Experience Platform-gebruikersinterface onder &quot;[!UICONTROL Identities]&quot;. De eigenschapswaarde moet een array zijn met identiteiten die betrekking hebben op die naamruimte identity.

Elk identiteitsobject in de array identities is als volgt gestructureerd:

### `id`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Tekenreeks | Ja | none |

Dit is de id die u voor de opgegeven naamruimte wilt synchroniseren.

### `authenticationState`

| **Type** | **Vereist** | **Standaardwaarde** | **Mogelijke waarden** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Tekenreeks | Ja | dubbelzinnig | ambigu, geverifieerd en gelogd |

De verificatiestatus van de id.

### `primary`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | optioneel | false |

Hiermee wordt bepaald of deze identiteit moet worden gebruikt als primair fragment in het verenigde profiel. Standaard wordt de ECID ingesteld als de primaire id voor de gebruiker.
