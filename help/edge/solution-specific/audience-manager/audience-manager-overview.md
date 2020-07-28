---
title: Gegevens verzenden naar Adobe Audience Manager
seo-title: Gegevens verzenden naar Adobe Audience Manager met Web SDK van Adobe Experience Platform
description: Leer hoe te om Gegevens naar Adobe Audience Manager met het Web SDK van het Experience Platform te verzenden
seo-description: Leer hoe te om Gegevens naar Adobe Audience Manager met het Web SDK van het Experience Platform te verzenden
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] op de [!DNL Experience Platform Edge Network]

Het Adobe Experience Platform [!DNL Web SDK] is geïntegreerd met Adobe Audience Manager en ondersteunt het verzenden en ontvangen van gegevens van [!DNL Audience Manager], Cookie- en URL-doelen en het synchroniseren van id&#39;s.

## Inschakelen [!DNL Audience Manager]

Om in te schakelen moet [!DNL Audience Manager] u het volgende doen:

- Schakel deze optie [!DNL Audience Manager] in uw [randconfiguratie](../../fundamentals/edge-configuration.md)in.
- U kunt cookies en URL-doelen in- of uitschakelen.
- De container voor id-synchronisatie opgeven voor syncs van externe partners (optioneel)

## Identiteiten synchroniseren

Het Adobe Experience Platform [!DNL Web SDK] steunt de capaciteit om klant IDs en hun authentificatiestatus via het bevel [SyncIdentity](../../fundamentals/identity.md) te verklaren.

De syncIdentity methode gebruikt Namespaces [van de Dienst van de](../../../identity/../identity-service/namespaces.md) Identiteit om op de context te wijzen waarop een identiteit betrekking heeft. Als [!DNL Audience Manager] klant, al uw bestaande Gegevensbronnen die het Type van identiteitskaart gebruiken: Cross-Device heeft automatisch een overeenkomend item [!DNL Identity Namespace]. Als u het overeenkomende item wilt zoeken [!DNL Identity Namespace] voor uw [!DNL Audience Manager Data Source]toepassing, meldt u zich aan bij het Adobe Experience Platform en navigeert u naar de [!DNL Identities] sectie.

![Weergave van de interface Namespaces](../../../assets/edge_configuration_identity.png)

Hier kunt u naar uw [!DNL Audience Manager] Gegevensbron door Naam zoeken. De methode syncIdentity gebruikt het Symbool van de Identiteit om Namespace te verklaren.

Een nieuwe [!DNL Audience Manager] gegevensbron die gebruikmaakt van id-type: Op meerdere apparaten wordt een overeenkomende naamruimte gegenereerd. Cookie- en advertentie-id&#39;s voor gegevensbronid&#39;s worden momenteel niet ondersteund. Bovendien wordt bij elke naamruimte in een Adobe Experience Platform een bijbehorende [!DNL Audience Manager] gegevensbron gegenereerd. De methode syncIdentity ondersteunt echter alleen Naamruimten-symbolen.
