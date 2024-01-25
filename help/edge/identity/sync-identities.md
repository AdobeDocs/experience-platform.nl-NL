---
title: Identiteiten synchroniseren tussen Audience Manager en Adobe Experience Platform met de Platform Web SDK
description: Leer hoe u identiteiten tussen Audience Manager en Adobe Experience Platform synchroniseert met de Platform Web SDK
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: publieksmanager;naam;identiteiten;synchronisatieidentiteiten;naamruimte;
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Identiteiten synchroniseren tussen Audience Manager en Experience Platform

Adobe Experience Platform Web SDK ondersteunt de mogelijkheid om klant-id&#39;s en hun verificatiestatus te declareren via de [sendEvent](./overview.md#syncing-identities) gebruiken.

Kies uw naamruimten in het menu [Naamruimten van identiteitsservice](../../identity/../identity-service/features/namespaces.md) om de context aan te geven waarop een identiteit betrekking heeft, door de waarden in de kolom Identiteitssymbool te gebruiken:

![Weergave van de interface Namespaces](../assets/identity/edge_namespaceUI_identity-symbol.png)

Als klant van de Audience Manager, al uw bestaande Gegevensbronnen die het Type van identiteitskaart gebruiken: Het dwars-Apparaat heeft automatisch een overeenkomstige Namespace van de Identiteit. Als u de overeenkomende naamruimte voor de gegevensbron van uw Audience Manager wilt zoeken, meldt u zich aan bij Adobe Experience Platform en navigeert u naar de sectie Identiteiten.

Nieuwe [!DNL Audience Manager] Gegevensbron die gebruikmaakt van ID-type: op meerdere apparaten wordt een overeenkomende naamruimte gegenereerd. Cookie- en advertentie-id&#39;s voor gegevensbronid&#39;s worden momenteel niet ondersteund. Bovendien wordt bij elke naamruimte die in Adobe Experience Platform wordt gemaakt, een overeenkomende naamruimte gegenereerd [!DNL Audience Manager] Gegevensbron, maar de methode syncIdentity ondersteunt alleen Namespace Identity Symbols.
