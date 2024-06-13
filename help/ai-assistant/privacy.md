---
title: Privacy, beveiliging en bestuur in AI Assistant
description: Meer informatie over privacy, beveiliging en governance-praktijken voor AI Assistant.
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: e14bf4191319d646c6c4bfd55656fc6de141e9ca
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Privacy, beveiliging en bestuur in AI Assistant

AI Assistant in Adobe Experience Platform is gebouwd met privacy, beveiliging en bestuur als vooraanstaande positie.

Lees dit document voor meer informatie over de vertrouwensgerichte mogelijkheden van de klant die u van AI Assistant kunt verwachten:

* De AI Assistant gebruikt momenteel geen persoonsgegevens, zelfs niet voor opleidingsdoeleinden.
* AI Assistant is niet op de hoogte van consumentengegevens.
* Alle bestaande [toegangsbeheer](../access-control/home.md) Het beleid wordt nageleefd door AI Assistant.
   * Om het even welk nieuw op attributen-gebaseerd toegangsbeheerbeleid wordt weerspiegeld in AI Medewerker na een maximum van 24 uren*
* U moet expliciete toestemming worden verleend om met AI Medewerker in wisselwerking te staan.
   * U kunt machtigingen voor Experience Platform en Journey Optimizer op een andere manier instellen met de [Gebruikersinterface voor machtigingen](../access-control/abac/ui/permissions.md) en u kunt de [Admin Console](../access-control/ui/browse.md) om machtigingen voor Customer Journey Analytics toe te wijzen.
   * De toestemmingen zijn korrelig en uw zandbakbeheerder kan vormen welke van uw gebruikers verschillende vraagcategorieën (product kennisgebaseerde vragen met AI Medewerker of vragen over operationele inzichten) kunnen stellen.
* AI Assistant is een functie die gereed is voor HIPAA in combinatie met het Adobe Experience Platform Healthcare Shield.
* U kunt een logboek van uw vorige interactie met AI Medewerker met een beleid van het 30 dagbehoud bekijken.
* AI Assistant wordt geaard in sandboxspecifieke gegevens en documentatie over openbare Adoben wanneer wordt geantwoord op vragen van gebruikers. Gegevens worden niet gedeeld door sandboxen.
* Prompts die u aan AI Assistant verstrekt, worden niet gedeeld met andere klanten.

**Dit houdt in dat als er nieuwe labels worden toegevoegd aan velden en objecten of als er nieuwe beleidsregels worden gemaakt, het maximaal 24 uur duurt voordat de AI Assistant wordt uitgevoerd. Tijdens die 24 uren, kunnen de gebruikers met onlangs beperkte toegang tot die gebieden en voorwerpen nog toegang hebben.*
