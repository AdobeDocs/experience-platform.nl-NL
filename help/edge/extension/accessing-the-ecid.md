---
title: Toegang tot de ECID
description: Leer hoe u toegang krijgt tot de Experience Cloud-id (ECID) in Adobe Experience Platform-tags
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Toegang tot de ECID

De [!DNL Experience Cloud ID (ECID)] is een permanente Experience Cloud-id waarmee u bezoekers van uw website kunt identificeren. In bepaalde omstandigheden, zoals het verzenden van het herkenningsteken naar een derdeplatform, zou u toegang tot kunnen nodig hebben [!DNL ECID].

Om toegang te krijgen tot [!DNL ECID] Voer binnen de tags de onderstaande stappen uit:

1. Verzeker uw bezit met wordt gevormd [regelcomponentvolgorde](../../tags/ui/managing-resources/rules.md#sequencing) ingeschakeld.
2. Maak een nieuwe regel.
3. Voeg een [!UICONTROL Library Loaded] aan de regel.
4. Voeg een [!UICONTROL Custom Condition] actie aan de regel, met de volgende code (veronderstellend de naam u voor de instantie van SDK hebt gevormd is `alloy`):

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. Sla de regel op.

U moet nu toegang hebben tot de [!DNL ECID] in volgende regels, gebruiken `%ECID%` of `_satellite.getVar("ECID")`, vergelijkbaar met hoe u toegang krijgt tot andere gegevenselementen.
