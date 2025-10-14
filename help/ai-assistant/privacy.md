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
* Al bestaand [&#x200B; toegangsbeheer &#x200B;](../access-control/home.md) beleid zal door AI Medewerker worden gerespecteerd.
   * Om het even welk nieuw op attributen-gebaseerd toegangsbeheerbeleid wordt weerspiegeld in AI Medewerker na een maximum van 24 uren*
* U moet expliciete toestemming worden verleend om met AI Medewerker in wisselwerking te staan.
   * U kunt toestemmingen voor Experience Platform en Journey Optimizer verschillend plaatsen gebruikend [&#x200B; Toestemmingen UI &#x200B;](../access-control/abac/ui/permissions.md) en u kunt de [&#x200B; Admin Console &#x200B;](../access-control/ui/browse.md) gebruiken om toestemmingen voor Customer Journey Analytics toe te wijzen.
   * De toestemmingen zijn korrelig en uw zandbakbeheerder kan vormen welke van uw gebruikers verschillende vraagcategorieën (product kennisgebaseerde vragen met AI Medewerker of vragen over operationele inzichten) kunnen stellen.
* AI Assistant is een functie die gereed is voor HIPAA in combinatie met het Adobe Experience Platform Healthcare Shield.
* U kunt een logboek van uw vorige interactie met AI Medewerker met een beleid van het 30 dagbehoud bekijken.
* AI Assistant wordt geaard in sandboxspecifieke gegevens en documentatie over openbare Adoben wanneer wordt geantwoord op vragen van gebruikers. Gegevens worden niet gedeeld door sandboxen.
* Prompts die u aan AI Assistant verstrekt, worden niet gedeeld met andere klanten.

**dit impliceert dat als om het even welke nieuwe etiketten aan gebieden en voorwerpen worden toegevoegd of om het even welk nieuw beleid wordt gecreeerd, dan zal het AI Medewerker tot 24 uren nemen om hen te respecteren. Tijdens die 24 uren, kunnen de gebruikers met onlangs beperkte toegang tot die gebieden en voorwerpen nog toegang hebben.*
