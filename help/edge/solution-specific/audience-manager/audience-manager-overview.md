---
title: Gegevens verzenden naar Adobe Audience Manager
seo-title: Gegevens verzenden naar Adobe Audience Manager met Adobe Experience Platform Web SDK
description: Meer informatie over het verzenden van gegevens naar Adobe Audience Manager met Web SDK van Experience Platform
seo-description: Meer informatie over het verzenden van gegevens naar Adobe Audience Manager met Web SDK van Experience Platform
translation-type: tm+mt
source-git-commit: b87b1f8a979e028c5ebf57cecf0213a075df90a6
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Audience Manager] op de [!DNL Experience Platform Edge Network]

De Adobe Experience Platform [!DNL Web SDK] is geïntegreerd met Adobe Audience Manager en biedt ondersteuning voor het verzenden en ontvangen van gegevens van [!DNL Audience Manager], Cookie- en URL-doelen en het synchroniseren van id&#39;s.

## Inschakelen [!DNL Audience Manager]

Om in te schakelen moet [!DNL Audience Manager] u het volgende doen:

- Schakel deze optie [!DNL Audience Manager] in uw [randconfiguratie](../../fundamentals/edge-configuration.md)in.
- U kunt cookies en URL-doelen in- of uitschakelen.
- De container voor id-synchronisatie opgeven voor syncs van externe partners (optioneel)

## Identiteiten synchroniseren

De SDK van het Web van Adobe Experience Platform ondersteunt de mogelijkheid om klant-id&#39;s en hun verificatiestatus te declareren via de opdracht [sendEvent](../../fundamentals/identity.md#syncing-identities) .

Kies uw naamruimten in de naamruimten [van de](../../../identity/../identity-service/namespaces.md) identiteitsdienst om de context aan te geven waarop een identiteit betrekking heeft, door de waarden in de kolom Identiteitssymbool te gebruiken:

![Weergave van de interface Namespaces](../../../assets/edge_namespaceUI_identity-symbol.png)

Als klant van de Audience Manager, al uw bestaande Gegevensbronnen die het Type van identiteitskaart gebruiken: Apparaatoverschrijdend heeft automatisch een overeenkomende naamruimte voor identiteit. Als u de overeenkomende naamruimte voor de gegevensbron van uw Audience Manager wilt zoeken, meldt u zich aan bij de Adobe Experience Platform en navigeert u naar de sectie Identiteiten.

Een nieuwe [!DNL Audience Manager] gegevensbron die gebruikmaakt van id-type: Op meerdere apparaten wordt een overeenkomende naamruimte gegenereerd. Cookie- en advertentie-id&#39;s voor gegevensbronid&#39;s worden momenteel niet ondersteund. Bovendien wordt bij elke naamruimte in Adobe Experience Platform een bijbehorende [!DNL Audience Manager] gegevensbron gegenereerd. De methode syncIdentity ondersteunt echter alleen Naamruimten-symbolen.
