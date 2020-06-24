---
title: Gegevens verzenden naar Adobe Audience Manager
seo-title: Gegevens verzenden naar Adobe Audience Manager met Web SDK van Adobe Experience Platform
description: Leer hoe te om Gegevens naar Adobe Audience Manager met het Web SDK van het Experience Platform te verzenden
seo-description: Leer hoe te om Gegevens naar Adobe Audience Manager met het Web SDK van het Experience Platform te verzenden
translation-type: tm+mt
source-git-commit: 6a83ab1c6405f45700f4f8899139010d50010b0c
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Audience Manager op het Netwerk van de Rand van het Experience Platform

De SDK van het Web van de Adobe Experience Platform is geïntegreerd met Adobe Audience Manager en steunt het verzenden van en het ontvangen van gegevens van Audience Manager, Koekje &amp; bestemmingen URL en identiteitskaart het synchroniseren.

## Audience Manager inschakelen

Om Audience Manager toe te laten zult u het volgende moeten doen:

- Schakel Audience Manager in uw [randconfiguratie](../../fundamentals/edge-configuration.md)in.
- U kunt cookies en URL-doelen in- of uitschakelen.
- De container voor id-synchronisatie opgeven voor syncs van externe partners (optioneel)

## Identiteiten synchroniseren

De SDK van het Web van het Adobe Experience Platform steunt de capaciteit om klant IDs en hun authentificatiestatus via het bevel [SyncIdentity](../../fundamentals/identity.md) te verklaren.

De syncIdentity methode gebruikt Namespaces [van de Dienst van de](../../../identity/../identity-service/namespaces.md) Identiteit om op de context te wijzen waarop een identiteit betrekking heeft. Als klant van de Audience Manager, al uw bestaande Gegevensbronnen die het Type van identiteitskaart gebruiken: Cross-Device krijgt automatisch een overeenkomende naamruimte. Om de overeenkomstige Namespace van de Identiteit voor uw Gegevensbron van de Audience Manager te vinden, login aan het Adobe Experience Platform en navigeer aan de sectie van Identiteiten.

![Weergave van de interface Namespaces](../../../assets/edge_configuration_identity.png)

Hier kunt u naar uw Gegevensbron van de Audience Manager door Naam zoeken. De methode syncIdentity gebruikt het Symbool van de Identiteit om Namespace te verklaren.

Een nieuwe gegevensbron voor Audience Managers die gebruikmaakt van het type ID: Op meerdere apparaten wordt een overeenkomende naamruimte gegenereerd. Cookie- en advertentie-id&#39;s voor gegevensbronid&#39;s worden momenteel niet ondersteund. Bovendien zal om het even welke Namespace van de Identiteit die in Adobe Experience Platform wordt gecreeerd een overeenkomstige Gegevensbron van de Audience Manager produceren maar merk op dat de syncIdentity methode slechts Symbolen van de Identiteit Namespace steunt.
