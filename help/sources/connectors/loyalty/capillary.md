---
title: Overzicht van Capillary Streaming-gebeurtenissen
description: Leer hoe u gegevens kunt streamen van Capillary naar Experience Platform.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>De bron [!DNL Capillary Streaming Events] is in bèta. Lees de [ termijnen en voorwaarden ](../../home.md#terms-and-conditions) in het bronoverzicht voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

[!DNL Capillary Technologies] is een toonaangevend platform voor loyaliteit en betrokkenheid dat door meer dan 300 merken over de hele wereld wordt vertrouwd. Gebruik de [!DNL Capillary Streaming Events] -bron om uw bedrijf in staat te stellen probleemloos klantenprofielen, loyaliteitsgegevens en transactionele gebeurtenissen van [!DNL Capillary] naar Adobe Experience Platform te streamen. Sluit de [!DNL Capillary] -bron aan om realtime personalisatie, geavanceerde publiekssegmentatie en omnichannel campagneorchestratie mogelijk te maken.

Door [!DNL Capillary] te integreren met Experience Platform kunt u:

* Synchroniseer **loyaliteitpunten, rijen, en beloningen** in real time.
* Verzend **transactiegegevens** in Experience Platform voor analyse en activering.
* Gebruik Real-Time CDP, Experience Platform en Adobe Journey Optimizer voor segmentatie, reisorchestratie en personalisatie.

## Vereisten

Voordat u verbinding maakt met Adobe Experience Platform, moet u controleren of u:[!DNL Capillary]

* Een geldige **identiteitskaart van de Organisatie van Adobe** en toegang tot een toegelaten zandbak van Experience Platform.
* **[!DNL Capillary]brongeloofsbrieven** (identiteitskaart van de Cliënt en Geheime cliënt).
* De benodigde machtigingen in de Adobe Admin Console om bronnen en gegevensstromen te maken.

### Vereiste referenties verzamelen

U moet waarden opgeven voor de volgende referenties om uw [!DNL Capillary] -account aan Experience Platform te koppelen:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Client-id | De client-id voor de [!DNL Capillary] -bron. | `321c8a8fee0d4a06838d46f9d3109e8a` |
| Clientgeheim | Het clientgeheim dat is uitgegeven met de client-id | `xxxxxxxxxxxxxxxxxx` |
| Org-id | Je Adobe-organisatie-id | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

Voor meer informatie bij het produceren van toegangstokens, lees de [ de authentificatiegids van Adobe ](https://developer.adobe.com/developer-console/docs/guides/authentication/).

### Een toegangstoken genereren

Gebruik vervolgens uw client-id en clientgeheim om een toegangstoken te genereren vanuit Adobe.

**Verzoek**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**Reactie**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## Volgende stappen

Als u de vereiste instellingen voor [!DNL Capillary] hebt voltooid, leest u de volgende documentatie voor informatie over hoe u verbinding kunt maken met uw account en hoe u kunt beginnen met het streamen van gegevens van [!DNL Capillary] naar Experience Platform.

* [Verbind  [!DNL Capillary Streaming Events]  met Experience Platform gebruikend API](../../tutorials/api/create/loyalty/capillary.md)
* [Verbind  [!DNL Capillary Streaming Events]  met Experience Platform gebruikend UI](../../tutorials/ui/create/loyalty/capillary.md)
