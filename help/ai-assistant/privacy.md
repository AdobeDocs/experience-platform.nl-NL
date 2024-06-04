---
title: Privacy, beveiliging en bestuur in AI Assistant
description: Meer informatie over privacy, beveiliging en governance-praktijken voor AI Assistant.
source-git-commit: 0820ba0f14e9eae5d89cd48490b1af5f9afcda70
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Privacy, beveiliging en bestuur in AI Assistant

AI Assistant in Adobe Experience Platform is gebouwd met privacy, beveiliging en bestuur als vooraanstaande positie.

Lees dit document voor meer informatie over de vertrouwensgerichte mogelijkheden van de klant die u van AI Assistant kunt verwachten:

* De AI Assistant gebruikt momenteel geen persoonsgegevens, zelfs niet voor opleidingsdoeleinden.
* AI Assistant is niet op de hoogte van consumentengegevens.
* Alle bestaande [toegangsbeheer](../access-control/home.md) Het beleid wordt nageleefd door AI Assistant.
   * Toegangsbeheer op objectniveau wordt ondersteund voor objecten. Ondersteuning voor toegangsbeheer op objectniveau voor kenmerken komt binnenkort beschikbaar.
   * Om het even welk nieuw op attributen-gebaseerd toegangsbeheerbeleid wordt weerspiegeld in AI Medewerker na een maximum van 24 uren*
* U moet expliciete toestemming worden verleend om met AI Medewerker in wisselwerking te staan.
   * U kunt machtigingen voor Experience Platform en Journey Optimizer op een andere manier instellen met de [Gebruikersinterface voor machtigingen](../access-control/abac/ui/permissions.md) en u kunt de [Admin Console](../access-control/ui/browse.md) om machtigingen voor Customer Journey Analytics toe te wijzen.
   * De toestemmingen zijn korrelig en uw zandbakbeheerder kan vormen welke van uw gebruikers verschillende vraagcategorieën (product kennisgebaseerde vragen met AI Medewerker of vragen over operationele inzichten) kunnen stellen.
* AI Assistant is een functie die klaar is voor HIPAA en voldoet aan HIPAA-vereisten met betrekking tot de verwerking en het gebruik van Protected Health Information (PHI).
* U kunt een logboek van uw vorige interactie met AI Medewerker met een beleid van het 30 dagbehoud bekijken.
* AI Assistant wordt geaard in sandboxspecifieke gegevens en documentatie over openbare Adoben wanneer wordt geantwoord op vragen van gebruikers. Gegevens worden niet gedeeld door sandboxen.
* Prompts die u aan AI Assistant verstrekt, worden niet gedeeld met andere klanten.


**Dit houdt in dat als er nieuwe labels worden toegevoegd aan velden en objecten of als er nieuwe beleidsregels worden gemaakt, het maximaal 24 uur duurt voordat de AI Assistant wordt uitgevoerd. Tijdens die 24 uren, kunnen de gebruikers met onlangs beperkte toegang tot die gebieden en voorwerpen nog toegang hebben.*