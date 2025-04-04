---
title: Identiteiten synchroniseren tussen Audience Manager en Adobe Experience Platform met Experience Platform Web SDK
description: Leer hoe u identiteiten tussen Audience Manager en Adobe Experience Platform kunt synchroniseren met de Experience Platform Web SDK
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: publieksmanager;naam;identiteiten;synchronisatieidentiteiten;naamruimte;
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Identiteiten synchroniseren tussen Audience Manager en Experience Platform

Adobe Experience Platform Web SDK steunt de capaciteit om klant IDs en hun authentificatiestatus via het [ te verklaren sendEvent ](./overview.md#syncing-identities) bevel.

Kies uw namespaces van de [ Namespaces van de Dienst van de Identiteit ](../../identity/../identity-service/features/namespaces.md) om op de context te wijzen waarop een identiteit betrekking heeft, door de waarden in de kolom van het Symbool van de Identiteit te gebruiken:

![ Mening van Namespaces UI ](../assets/identity/edge_namespaceUI_identity-symbol.png)

Als klant van Audience Manager, al uw bestaande Gegevensbronnen die het Type van identiteitskaart gebruiken: Het dwars-Apparaat heeft automatisch een overeenkomstige Namespace van de Identiteit. Als u de overeenkomende naamruimte voor uw Audience Manager Data Source wilt zoeken, meldt u zich aan bij Adobe Experience Platform en navigeert u naar de sectie Identiteiten.

Nieuwe [!DNL Audience Manager] Data Source die ID-type gebruikt: Cross-Device genereert een overeenkomende Identity-naamruimte. Gegevens Source ID Types Cookie en Device Advertising ID worden momenteel niet ondersteund. Daarnaast wordt bij elke naamruimte die in Adobe Experience Platform wordt gemaakt, een overeenkomende [!DNL Audience Manager] Data Source gegenereerd, maar de methode syncIdentity ondersteunt alleen Naamruimten-symbolen.
