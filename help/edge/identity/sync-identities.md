---
title: Identiteiten synchroniseren tussen Audience Manager en Adobe Experience Platform met de SDK van het Web Platform
description: Leer hoe te om identiteiten tussen Audience Manager en Adobe Experience Platform te synchroniseren gebruikend het Web SDK van het Platform
seo-description: Leer hoe u identiteiten kunt synchroniseren met Adobe Audience Manager met Experience Platform Web SDK
keywords: publieksmanager;naam;identiteiten;synchronisatieidentiteiten;naamruimte;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Identiteiten synchroniseren tussen Audience Manager en Experience Platform

Adobe Experience Platform Web SDK ondersteunt de mogelijkheid om klant-id&#39;s en hun verificatiestatus te declareren via de opdracht [sendEvent](./overview.md#syncing-identities).

Kies uw naamruimten in de naamruimten [Identiteitsservice](../../identity/../identity-service/namespaces.md) om de context aan te geven waarop een identiteit betrekking heeft, door de waarden in de kolom Identiteitssymbool te gebruiken:

![Weergave van de interface Namespaces](../../assets/edge_namespaceUI_identity-symbol.png)

Als klant van de Audience Manager, al uw bestaande Gegevensbronnen die het Type van identiteitskaart gebruiken: Apparaatoverschrijdend heeft automatisch een overeenkomende naamruimte voor identiteit. Als u de overeenkomende naamruimte voor de gegevensbron van uw Audience Manager wilt zoeken, meldt u zich aan bij Adobe Experience Platform en navigeert u naar de sectie Identiteiten.

Nieuwe [!DNL Audience Manager] gegevensbron die gebruikmaakt van id-type: Op meerdere apparaten wordt een overeenkomende naamruimte gegenereerd. Cookie- en advertentie-id&#39;s voor gegevensbronid&#39;s worden momenteel niet ondersteund. Daarnaast wordt bij elke naamruimte in Adobe Experience Platform een corresponderende gegevensbron [!DNL Audience Manager] gegenereerd, maar de methode syncIdentity ondersteunt alleen Naamruimten-symbolen.
