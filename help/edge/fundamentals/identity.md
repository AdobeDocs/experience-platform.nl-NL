---
title: Experience Cloud ID ophalen
seo-title: Adobe Experience Platform Web SDK Experience Cloud ID ophalen
description: Leer hoe u Adobe Experience Cloud ID kunt ophalen.
seo-description: Leer hoe u Adobe Experience Cloud ID kunt ophalen.
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# Experience Cloud ID ophalen

De Adobe Experience Platform Web SDK maakt gebruik van de [Adobe Identity Service](../../identity-service/ecid.md). Dit zorgt ervoor dat elk apparaat een unieke id heeft die op het apparaat blijft bestaan, zodat de activiteit tussen pagina&#39;s aan elkaar kan worden gekoppeld.

## Identiteit eerste partij

De dienst van identiteitskaart slaat de identiteit in een koekje in een eerste partijdomein op. De diensten van identiteitskaart proberen om het koekje te plaatsen gebruikend een kopbal van HTTP op het domein als dat ontbreekt de dienst van identiteitskaart zal terug naar het plaatsen van koekjes via Javascript vallen. Adobe raadt u aan een CNAME in te stellen om ervoor te zorgen dat uw cookies niet worden beperkt door ITP-beperkingen aan de clientzijde.

## Identiteit derde partij

De diensten van identiteitskaart hebben de capaciteit om identiteitskaart met een derdedomein (demdex.net) te synchroniseren om het volgen over plaats toe te laten. Wanneer dit wordt toegelaten zal het eerste verzoek voor een bezoeker (b.v. iemand zonder ECID) aan demdex.net worden gedaan. Dit zal slechts op browsers worden gedaan die het toestaan (b.v. Chrome) en door de `thirdPartyCookiesEnabled` parameter in de configuratie gecontroleerd. Als u deze functie wilt uitschakelen, worden deze allemaal samen ingesteld `thirdPartyCookiesEnabled` op false.

## De bezoeker-id ophalen

Gebruik de `getIdentity` opdracht als u deze unieke id wilt gebruiken. `getIdentity` retourneert de bestaande ECID voor de huidige bezoeker. Voor nieuwe bezoekers die nog geen ECID hebben, genereert deze opdracht een nieuwe ECID.

>[!NOTE]
>
>Deze methode wordt meestal gebruikt met aangepaste oplossingen waarvoor de Experience Cloud-id moet worden gelezen. Het wordt niet gebruikt door een standaardimplementatie.

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

Daarnaast kunt u met de identiteitsservice uw eigen id&#39;s synchroniseren met de ECID via de `syncIdentity` opdracht.

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
      }
    }
})
```

### Opties voor synchronisatie-identiteiten

#### Naamruimtesymbool identiteit

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| String | Ja | none |

De sleutel voor het object is het symbool [Identiteitsnaamruimte](../../identity-service/namespaces.md) . U vindt dit in de gebruikersinterface van het Adobe Experience Platform onder Identiteiten.

#### `id`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| String | Ja | none |

Dit is de id die u voor de opgegeven naamruimte wilt synchroniseren.

#### `primary`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | optioneel | false |

Moet deze identiteit worden gebruikt als primair fragment in het verenigde profiel. Standaard wordt de ECID ingesteld als primaire id voor de gebruiker.

#### `hashEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | optioneel | false |

Als deze optie is ingeschakeld, wordt de identiteit verborgen met behulp van SHA256-hashing.