---
title: Identiteitsinstellingen
description: Bepaal hoe bezoekers door de tagextensie worden geïdentificeerd.
exl-id: 12e707f4-c37b-4c02-bfec-5ef7b98c2d3b
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Identiteitsinstellingen {#identity}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_identity"
>title="Identiteit"
>abstract="Bepaal hoe bezoekers door de tagextensie worden geïdentificeerd."

Deze configuratiesectie staat u toe om het gedrag van het Web SDK te bepalen wanneer het over de behandeling van gebruikersidentificatie komt.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Identity]** .

![ Beeld dat de identiteitsmontages van de de markeringsuitbreiding van SDK van het Web in de markeringen UI toont ](../assets/web-sdk-ext-identity.png)

De volgende opties zijn beschikbaar:

## [!UICONTROL Migrate ECID from VisitorAPI]

Een selectievakje waarmee de Web SDK de cookies `AMCV` en `s_ecid` kan lezen en het cookie `AMCV` kan instellen dat door `Visitor.js` wordt gebruikt. Deze functie is belangrijk wanneer u migreert van bibliotheken die `VisitorAPI.js` gebruiken naar de Web SDK, omdat sommige pagina&#39;s `Visitor.js` nog steeds gebruiken. Met deze optie kan de SDK dezelfde ECID blijven gebruiken, zodat gebruikers niet als twee aparte gebruikers worden geïdentificeerd. Het JavaScript-bibliotheekequivalent aan dit selectievakje is [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md) .

## [!UICONTROL Use third-party cookies]

Als deze optie is ingeschakeld, probeert de Web SDK een gebruikers-id op te slaan in een cookie van een andere fabrikant. Als dit gelukt is, wordt de gebruiker geïdentificeerd als één gebruiker terwijl deze in meerdere domeinen navigeert en niet als een afzonderlijke gebruiker op elk domein wordt geïdentificeerd. Als deze optie is ingeschakeld, kan de SDK de gebruikersnaam nog steeds niet opslaan in een cookie van een andere fabrikant als de browser cookies van derden niet ondersteunt of door de gebruiker is geconfigureerd om cookies van derden niet toe te staan. In dit geval slaat de SDK de id alleen op in het domein van de eerste partij. Het JavaScript-bibliotheekequivalent aan dit selectievakje is [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) .

>[!IMPORTANT]
>
>De koekjes van de derde zijn niet compatibel met de [ functionaliteit 1} van identiteitskaart van het eerste apparaat in SDK van het Web. ](/help/collection/use-cases/identity/first-party-device-ids.md) U kunt apparaat-id&#39;s van de eerste fabrikant gebruiken of cookies van derden gebruiken; u kunt beide functies niet gelijktijdig gebruiken.
