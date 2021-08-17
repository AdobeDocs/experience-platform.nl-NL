---
title: 'Toegang tot de ECID '
description: Adobe Experience Platform Web SDK Extension Leveraging ECID in tags
source-git-commit: befe1efa884706165b8d65803d06f6370a8a60f2
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Toegang tot de ECID

De [!DNL Experience Cloud Identity (ECID)] is een permanente id voor een bezoeker van uw website. In bepaalde omstandigheden hebt u wellicht liever toegang tot de ECID (bijvoorbeeld om deze naar een derde te verzenden).

Adobe raadt het volgende aan om toegang te krijgen tot de ECID binnen tags:

1. Zorg ervoor dat uw eigenschap is geconfigureerd met [regelcomponent-sequencing](../../tags/ui/managing-resources/rules.md#sequencing) ingeschakeld.
1. Maak een nieuwe regel.
1. Voeg een [!UICONTROL Library Loaded] gebeurtenis aan de regel toe.
1. Voeg een [!UICONTROL Custom Condition] actie aan de regel met de volgende code toe (veronderstellend de naam u voor de instantie van SDK hebt gevormd `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Sla de regel op.

U zou dan tot ECID in verdere regels moeten kunnen toegang hebben gebruikend `%ECID%` of `_satellite.getVar("ECID")` zoals u een ander gegevenselement.
