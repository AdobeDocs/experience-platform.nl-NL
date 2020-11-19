---
title: Identiteiten synchroniseren met Audience Manager en Adobe Experience Platform
seo-title: Identiteiten synchroniseren met Audience Manager en Adobe Experience Platform met Adobe Experience Platform Web SDK
description: Leer hoe u identiteiten kunt synchroniseren met Adobe Audience Manager met Experience Platform Web SDK
seo-description: Leer hoe u identiteiten kunt synchroniseren met Adobe Audience Manager met Experience Platform Web SDK
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Identiteiten synchroniseren

Adobe Experience Platform Web SDK steunt de capaciteit om klant IDs en hun authentificatiestatus via het [sendEvent](./overview.md#syncing-identities) bevel te verklaren.

Kies uw naamruimten in de naamruimten [van de](../../identity/../identity-service/namespaces.md) identiteitsdienst om de context aan te geven waarop een identiteit betrekking heeft, door de waarden in de kolom Identiteitssymbool te gebruiken:

![Weergave van de interface Namespaces](../../assets/edge_namespaceUI_identity-symbol.png)

Als klant van de Audience Manager, al uw bestaande Gegevensbronnen die het Type van identiteitskaart gebruiken: Apparaatoverschrijdend heeft automatisch een overeenkomende naamruimte voor identiteit. Als u de overeenkomende naamruimte voor de gegevensbron van uw Audience Manager wilt zoeken, meldt u zich aan bij Adobe Experience Platform en navigeert u naar de sectie Identiteiten.

Een nieuwe [!DNL Audience Manager] gegevensbron die gebruikmaakt van id-type: Op meerdere apparaten wordt een overeenkomende naamruimte gegenereerd. Cookie- en advertentie-id&#39;s voor gegevensbronid&#39;s worden momenteel niet ondersteund. Bovendien wordt bij elke naamruimte in Adobe Experience Platform een bijbehorende [!DNL Audience Manager] gegevensbron gegenereerd. De methode syncIdentity ondersteunt echter alleen Naamruimten-symbolen.
