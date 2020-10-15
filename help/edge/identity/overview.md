---
title: Experience Cloud-id ophalen
seo-title: Adobe Experience Platform Web SDK Experience Cloud-id ophalen
description: Meer weten over Adobe Experience Cloud-id?
seo-description: Meer weten over Adobe Experience Cloud-id?
keywords: Identity;First Party Identity;Identity Service;3rd Party Identity;ID Migration;Visitor ID;third party identity;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identities;syncIdentity;sendEvent;identityMap;primary;ecid;Identity Namespace;namespace id;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: d069b3007265406367ca9de2b85540b2a070cf36
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---


# Identiteit - De Experience Cloud-id wordt opgehaald

De Adobe Experience Platform [!DNL Web SDK] gebruikt de [Adobe Identity Service](../../identity-service/ecid.md). Dit zorgt ervoor dat elk apparaat een unieke id heeft die op het apparaat blijft bestaan, zodat de activiteit tussen pagina&#39;s aan elkaar kan worden gekoppeld.

## Identiteit eerste partij

De identiteit wordt in een cookie in een domein van de eerste partij [!DNL Identity Service] opgeslagen. De [!DNL Identity Service] methode probeert het cookie in te stellen met een HTTP-header op het domein. Als dat mislukt, [!DNL Identity Service] worden cookies weer ingesteld via JavaScript. Adobe raadt u aan een CNAME in te stellen om ervoor te zorgen dat uw cookies niet worden beperkt door ITP-beperkingen aan de clientzijde.

## Identiteit van derden

De [!DNL Identity Service] heeft de capaciteit om een identiteitskaart met een derdedomein (demdex.net) te synchroniseren om het volgen over plaatsen toe te laten. Wanneer dit wordt toegelaten zal het eerste verzoek voor een bezoeker (b.v. iemand zonder ECID) aan demdex.net worden gedaan. Dit zal slechts op browsers worden gedaan die het toestaan (b.v. Chrome) en door de `thirdPartyCookiesEnabled` parameter in de configuratie gecontroleerd. Als u deze functie samen wilt uitschakelen, stelt u deze in `thirdPartyCookiesEnabled` op false.

## ID-migratie

Wanneer u migreert vanuit de Bezoeker-API, kunt u ook bestaande AMCV-cookies migreren. Stel de `idMigrationEnabled` parameter in de configuratie in om ECID-migratie in te schakelen. De migratie van id is opstelling om sommige gebruiksgevallen toe te laten:

* Wanneer sommige pagina&#39;s van een domein de bezoeker-API gebruiken en andere pagina&#39;s deze SDK gebruiken. Ter ondersteuning van dit geval leest de SDK bestaande AMCV-cookies en schrijft hij een nieuw cookie met de bestaande ECID. Bovendien schrijft de SDK AMCV-cookies zodat, als de ECID eerst wordt verkregen op een pagina die van instrumenten is voorzien met de AEP Web SDK, de volgende pagina&#39;s die van instrumenten zijn voorzien met de Bezoeker-API dezelfde ECID hebben.
* Wanneer de AEP Web SDK opstelling op een pagina is die ook bezoeker API heeft. Ter ondersteuning van dit geval zoekt de SDK, als het AMCV-cookie niet is ingesteld, naar de Bezoeker-API op de pagina en roept deze aan om de ECID op te halen.
* Wanneer de hele site de SDK van AEP Web gebruikt en geen API voor bezoekers heeft, is het handig om de ECID&#39;s te migreren zodat de informatie van de retourbezoeker behouden blijft. Nadat de SDK gedurende een bepaalde periode is geïmplementeerd, zodat de meeste cookies van de bezoeker worden gemigreerd, kan de instelling worden uitgeschakeld. `idMigrationEnabled`

## De bezoeker-id ophalen

Gebruik de `getIdentity` opdracht als u deze unieke id wilt gebruiken. `getIdentity` retourneert de bestaande ECID voor de huidige bezoeker. Voor nieuwe bezoekers die nog geen ECID hebben, genereert deze opdracht een nieuwe ECID.

>[!NOTE]
>
>Deze methode wordt typisch gebruikt met douaneoplossingen die het lezen van [!DNL Experience Cloud] identiteitskaart vereisen. Het wordt niet gebruikt door een standaardimplementatie.

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## Identiteiten synchroniseren

>[!NOTE]
>
>De `syncIdentity` methode is, naast de hash-functie, verwijderd uit versie 2.1.0. Als u versie 2.1.0+ gebruikt en identiteiten wilt synchroniseren, kunt u ze rechtstreeks via de `xdm` optie van de `sendEvent` opdracht onder het `identityMap` veld verzenden.

Daarnaast [!DNL Identity Service] `syncIdentity` kunt u met de opdracht uw eigen id&#39;s synchroniseren met de ECID.

>[!NOTE]
>
>Het wordt ten zeerste aanbevolen alle beschikbare identiteiten door te geven voor elke `sendEvent` opdracht. Dit ontgrendelt een reeks gebruiksgevallen, waaronder personalisatie. Nu u die identiteiten in het `sendEvent` bevel kunt overgaan, kunnen zij direct in uw DataLayer worden geplaatst.

Door identiteiten te synchroniseren kunt u een apparaat/gebruiker identificeren met behulp van meerdere identiteiten, de verificatiestatus instellen en bepalen welke id als de primaire id wordt beschouwd. Als er geen id is ingesteld als `primary`, worden de primaire standaardinstellingen ingesteld als `ECID`id.

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
})
```


### Opties voor het synchroniseren van identiteiten

#### Naamruimtesymbool voor identiteit

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Tekenreeks | Ja | none |

De sleutel voor het object is het symbool [Identiteitsnaamruimte](../../identity-service/namespaces.md) . U vindt dit in de gebruikersinterface van Adobe Experience Platform onder &quot;[!UICONTROL Identiteiten]&quot;.

#### `id`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Tekenreeks | Ja | none |

Dit is de id die u voor de opgegeven naamruimte wilt synchroniseren.

#### `authenticationState`

| **Type** | **Vereist** | **Standaardwaarde** | **Mogelijke waarden** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Tekenreeks | Ja | dubbelzinnig | ambigu, geverifieerd en gelogd |

De verificatiestatus van de id.

#### `primary`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | optioneel | false |

Hiermee wordt bepaald of deze identiteit moet worden gebruikt als primair fragment in het verenigde profiel. Standaard wordt de ECID ingesteld als de primaire id voor de gebruiker.

#### `hashEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | optioneel | false |

Als deze optie is ingeschakeld, wordt de identiteit verborgen met behulp van SHA256-hashing.
