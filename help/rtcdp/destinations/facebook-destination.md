---
title: Facebook-bestemming
seo-title: Facebook-bestemming
description: Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
seo-description: Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (bèta) Facebook-bestemming

>[!IMPORTANT]
>
>De Facebook-bestemming in Adobe Real-time CDP bevindt zich momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht

Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.

## Doelspecificaties

### Activeringstype

Segmentexport - u exporteert alle leden van een segment (publiek) met hun id&#39;s (naam, telefoonnummer, enz.) gebruikt in de Facebook-bestemming

## Vereisten

Voordat u publiekssegmenten kunt verzenden naar [!DNL Facebook], moet u controleren of aan de volgende vereisten wordt voldaan:

1. Voor uw [!DNL Facebook] gebruikersaccount moet de machtiging **Campagnes** beheren zijn ingeschakeld voor de advertentieaccount die u wilt gebruiken.
2. Voeg het **Adobe Experience Cloud** -bedrijfsaccount toe als een advertentiepartner in uw [!DNL Facebook Ad Account]. Gebruik `business ID=206617933627973`. Zie Partners [toevoegen aan uw Business Manager](https://www.facebook.com/business/help/1717412048538897) voor meer informatie.
   >[!IMPORTANT]
   > Wanneer u de machtigingen voor Adobe Experience Cloud configureert, moet u de machtiging **Campagnes** beheren inschakelen. Dit is nodig voor de [!DNL Adobe Real-time CDP] integratie.
3. Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Om dit te doen, ga naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, waar `accountID` is je [!DNL Facebook Ad Account ID].


## Connect-doel

Raadpleeg de verificatieworkflow [voor bestemmingen van](/help/rtcdp/destinations/social-network-destinations-workflow.md)sociale netwerken om verbinding te maken met de Facebook-bestemming.


## Segmenten activeren op Facebook

Zie Gegevens [naar doelen](/help/rtcdp/destinations/activate-destinations.md)activeren voor instructies over het activeren van segmenten op Facebook.