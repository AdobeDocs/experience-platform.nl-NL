---
title: JavaScript-tags gebruiken om de toestemming van de klant te beheren
description: Leer hoe u in Adobe Experience Platform de keuze- en opt-outsignalen van klanten voor verschillende Adobe-oplossingen kunt beheren.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# JavaScript-tags gebruiken om de toestemming van de klant te beheren

Wettelijke privacyregels zoals de algemene gegevensbeschermingsverordening (GDPR) vereisen dat bedrijven toestemming voor hun gebruikers kunnen beheren. Adobe-klanten kunnen bezoekers vragen zich aan te melden voordat Adobe-oplossingen voor een bepaalde bezoeker worden uitgevoerd. Bezoekers moeten hun opt-in- en opt-out-status kunnen beheren.

Adobe Experience Cloud-klanten hebben verschillende implementaties van deze vereisten nodig. Sommigen gebruiken toestemmingsmanagers op bedrijfsniveau en anderen bouwen hun eigen.

Ontwikkelaars van Adobe Experience Platform-extensies gebruiken extensies en de builder van regels om opt-in- en opt-out-oplossingen te definiëren.

Dit document bevat informatie over hoe u kunt voorkomen dat Adobe-tags worden geactiveerd totdat de toestemming is verkregen.

## Advertising Cloud

Adobe Experience Platform wordt niet automatisch geactiveerd [!DNL Advertising Cloud] . [!DNL Advertising Cloud] wordt alleen geactiveerd als u dit specifiek in een regelactie opgeeft. Gebruik de regelvoorwaarden om te bepalen wanneer en wat er moet worden afgegaan. Bijvoorbeeld, om koekjes te gebruiken om opt-in status te bepalen, plaats een gegevenselement om dat koekje te lezen en het als voorwaarde in de regel te gebruiken om te bepalen wanneer om de actie van de Omzetting van het Spoor in werking te stellen.

De integratie met toestemmingsmanagers (zoals OneTrust) kan de toestemmingskoekjes voor klanten plaatsen en volgen, die dan in de regelbouwer kunnen worden gebruikt.

## Analytics

In de sectie van het Volgen van de Verbinding van de [!DNL Analytics] configuratiemontages van de uitbreiding, zorg ervoor het volgende ** niet wordt geselecteerd:

* Download-koppelingen volgen
* Uitgaande koppelingen bijhouden

Als deze instellingen niet zijn geselecteerd, wordt Experience Platform niet automatisch geactiveerd [!DNL Adobe Analytics] . [!DNL Analytics] wordt alleen geactiveerd als u dit specifiek in een regelactie opgeeft. Gebruik de regelvoorwaarden om te bepalen wanneer en wat er moet worden afgegaan. Bijvoorbeeld, om koekjes te gebruiken om opt-in status te bepalen, plaats een gegevenselement om dat koekje te lezen en het als voorwaarde in de regel te gebruiken om te bepalen wanneer te om de Send actie van het Bandje in werking te stellen.

Afzonderlijk, kon u het gebruiken van het [&#x200B; Adobe opt-in voorwerp &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=nl-NL) overwegen om het vuren van deze markering in overleg met uw platform van het toestemmingsbeheer te controleren.

De integratie met toestemmingsmanagers (zoals OneTrust) kan de toestemmingskoekjes voor klanten plaatsen en volgen, die dan in de regelbouwer kunnen worden gebruikt.

## Audience Manager

DIL wordt momenteel automatisch geactiveerd als het op een klantpagina is geplaatst. Gelieve te overwegen gebruikend het [&#x200B; Adobe opt-in voorwerp &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=nl-NL) om het vuren van deze markering in overleg met uw platform van het toestemmingsbeheer te controleren.

[!DNL Adobe] raadt u aan om het doorsturen van de server te gebruiken binnen [!DNL Analytics] .

## Experience Cloud-id

[!DNL Experience Cloud ID] wordt momenteel automatisch geactiveerd als het op een klantpagina is geplaatst.

Gelieve te overwegen gebruikend het [&#x200B; Adobe opt-in voorwerp &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=nl-NL) om het vuren van deze markering in overleg met uw platform van het toestemmingsbeheer te controleren.

## Target

Adobe Experience Platform wordt niet automatisch geactiveerd [!DNL Target] . [!DNL Target] wordt alleen geactiveerd als u dit specifiek in een regelactie opgeeft. Gebruik de regelvoorwaarden om te bepalen wanneer en wat er moet worden afgegaan. Als u bijvoorbeeld cookies wilt gebruiken om de status van aanmelden te bepalen, stelt u een gegevenselement in om dat cookie te lezen en gebruikt u dit als een voorwaarde in de regel om te bepalen wanneer de handeling Laden [!DNL Target] moet worden uitgevoerd.

Afzonderlijk, kon u het gebruiken van het [&#x200B; Adobe opt-in voorwerp &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=nl-NL) overwegen om het vuren van deze markering in overleg met uw platform van het toestemmingsbeheer te controleren.

De integratie met toestemmingsmanagers (zoals OneTrust) kan de toestemmingskoekjes voor klanten plaatsen en volgen, die dan in de regelbouwer kunnen worden gebruikt.
