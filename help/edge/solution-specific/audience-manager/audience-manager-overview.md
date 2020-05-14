---
title: Gegevens verzenden naar Adobe Auditions Manager
seo-title: Gegevens verzenden naar Adobe Audience Manager met Adobe Experience Platform Web SDK
description: Leer hoe u gegevens naar Adobe Audience Manager kunt verzenden met Experience Platform Web SDK
seo-description: Leer hoe u gegevens naar Adobe Audience Manager kunt verzenden met Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 4bea14d18ce119bdec0d428f885d240f92244cfc
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Publiek Manager op het Edge-netwerk van het Experience Platform

De SDK van het Adobe Experience Platform Web is geïntegreerd met Adobe Audience Manager en ondersteunt het verzenden en ontvangen van gegevens van Audience Manager, Cookie- en URL-doelen en het synchroniseren van id&#39;s.

## Auditiebeheer inschakelen

Als u Audience Manager wilt inschakelen, moet u het volgende doen:

- Schakel Audience Manager in uw [randconfiguratie](../../fundamentals/edge-configuration.md)in.
- U kunt cookies en URL-doelen in- of uitschakelen.
- De container voor id-synchronisatie opgeven voor syncs van externe partners (optioneel)

## Identiteiten synchroniseren

De Adobe Experience Platform Web SDK ondersteunt de mogelijkheid om klant-id&#39;s en hun verificatiestatus te declareren via de [opdracht SyncIdentity](../../fundamentals/identity.md) .

De syncIdentity methode gebruikt Namespaces [van de Dienst van de](../../../identity/../identity-service/namespaces.md) Identiteit om op de context te wijzen waarop een identiteit betrekking heeft. Als klant van de Manager van het Publiek, al uw bestaande Gegevensbronnen die het Type van identiteitskaart gebruiken: Cross-Device krijgt automatisch een overeenkomende naamruimte. Als u de bijbehorende naamruimte voor de gegevensbron van Audience Manager wilt zoeken, meldt u zich aan bij het Adobe Experience Platform en navigeert u naar de sectie Identiteiten.

![Weergave van de interface Namespaces](../../../assets/edge_configuration_identity.png)

Hier kunt u naar uw Gegevensbron van de Manager van de Publiek zoeken door Naam. De methode syncIdentity gebruikt het Symbool van de Identiteit om Namespace te verklaren.

Om het even welke nieuwe Gegevensbron van de Manager van de Auditie die het Type van identiteitskaart gebruikt: Op meerdere apparaten wordt een overeenkomende naamruimte gegenereerd. Cookie- en advertentie-id&#39;s voor gegevensbronid&#39;s worden momenteel niet ondersteund. Bovendien wordt bij elke Naamruimte voor identiteit die in het Adobe Experience Platform wordt gemaakt, een overeenkomstige gegevensbron voor het beheer van de doelgroep gegenereerd. De methode syncIdentity ondersteunt echter alleen Naamruimten-identiteitssymbolen.
