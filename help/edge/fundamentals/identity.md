---
title: Experience Cloud-id ophalen
seo-title: Adobe Experience Platform Web SDK Experience Cloud-id ophalen
description: Meer weten over Adobe Experience Cloud-id?
seo-description: Meer weten over Adobe Experience Cloud-id?
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# Identiteit - De Experience Cloud-id wordt opgehaald

Het Adobe Experience Platform [!DNL Web SDK] gebruikt de [Adobe Identity Service](../../identity-service/ecid.md). Dit zorgt ervoor dat elk apparaat een unieke id heeft die op het apparaat blijft bestaan, zodat de activiteit tussen pagina&#39;s aan elkaar kan worden gekoppeld.

## Identiteit eerste partij

De identiteit wordt in een cookie in een domein van de eerste partij [!DNL Identity Service] opgeslagen. De [!DNL Identity Service] methode probeert het cookie in te stellen met een HTTP-header op het domein. Als dat mislukt, [!DNL Identity Service] worden cookies weer ingesteld via JavaScript. Adobe raadt u aan een CNAME in te stellen om ervoor te zorgen dat uw cookies niet worden beperkt door ITP-beperkingen aan de clientzijde.

## Identiteit derde partij

De [!DNL Identity Service] heeft de capaciteit om een identiteitskaart met een derdedomein (demdex.net) te synchroniseren om het volgen over plaatsen toe te laten. Wanneer dit wordt toegelaten zal het eerste verzoek voor een bezoeker (b.v. iemand zonder ECID) aan demdex.net worden gedaan. Dit zal slechts op browsers worden gedaan die het toestaan (b.v. Chrome) en door de `thirdPartyCookiesEnabled` parameter in de configuratie gecontroleerd. Als u deze functie samen wilt uitschakelen, stelt u deze in `thirdPartyCookiesEnabled` op false.

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

Daarnaast [!DNL Identity Service] `syncIdentity` kunt u met de opdracht uw eigen id&#39;s synchroniseren met de ECID.

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

De sleutel voor het object is het symbool [Identiteitsnaamruimte](../../identity-service/namespaces.md) . U vindt dit in de gebruikersinterface van het Adobe Experience Platform onder [!UICONTROL Identiteiten].

#### `id`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| String | Ja | none |

Dit is de id die u voor de opgegeven naamruimte wilt synchroniseren.

#### `authenticationState`

| **Type** | **Vereist** | **Standaardwaarde** | **Mogelijke waarden** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| String | Ja | dubbelzinnig | ambigu, geverifieerd en gelogd |

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
