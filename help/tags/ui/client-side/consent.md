---
title: JavaScript-tags gebruiken om de toestemming van de klant te beheren
description: Leer hoe u in Adobe Experience Platform de keuze- en opt-outsignalen van klanten voor verschillende Adobe-oplossingen kunt beheren.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# JavaScript-tags gebruiken om de toestemming van de klant te beheren

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

De combinatie van de [Algemene Verordening inzake gegevensbescherming (GDPR)](https://gdpr-info.eu/art-7-gdpr/) en [ePrivacy](https://medium.com/mydata/consent-lost-gdpr-and-found-eprivacy-e85cf881ffb) wetgeving vereist dat bedrijven toestemming voor hun gebruikers kunnen beheren. Adobe-klanten kunnen bezoekers vragen zich aan te melden voordat Adobe-oplossingen voor een bepaalde bezoeker worden uitgevoerd. Bezoekers moeten hun opt-in- en opt-out-status kunnen beheren.

Adobe Experience Cloud-klanten hebben verschillende implementaties van deze vereisten nodig. Sommigen gebruiken toestemmingsmanagers op bedrijfsniveau en anderen bouwen hun eigen.

Ontwikkelaars van Adobe Experience Platform-extensies gebruiken extensies en de builder van regels om opt-in- en opt-out-oplossingen te definiëren.

Dit document bevat informatie over hoe u kunt voorkomen dat Adobe-tags worden geactiveerd totdat de toestemming is verkregen.

## Advertising Cloud

Adobe Experience Platform wordt niet automatisch [!DNL Advertising Cloud] geactiveerd. [!DNL Advertising Cloud] wordt alleen geactiveerd als u dit specifiek in een regelhandeling opgeeft. Gebruik de regelvoorwaarden om te bepalen wanneer en wat er moet worden afgegaan. Bijvoorbeeld, om koekjes te gebruiken om opt-in status te bepalen, plaats een gegevenselement om dat koekje te lezen en het als voorwaarde in de regel te gebruiken om te bepalen wanneer om de actie van de Omzetting van het Spoor in werking te stellen.

De integratie met toestemmingsmanagers (zoals OneTrust) kan de toestemmingskoekjes voor klanten plaatsen en volgen, die dan in de regelbouwer kunnen worden gebruikt.

## Analytics

In de sectie van het Volgen van de Verbinding van de [!DNL Analytics] de configuratiemontages van de uitbreiding, zorg ervoor het volgende *not* wordt geselecteerd:

* Download-koppelingen volgen
* Uitgaande koppelingen bijhouden

Als deze instellingen niet zijn geselecteerd, wordt het Platform niet automatisch [!DNL Adobe Analytics] geactiveerd. [!DNL Analytics] wordt alleen geactiveerd als u dit specifiek in een regelactie zegt. Gebruik de regelvoorwaarden om te bepalen wanneer en wat er moet worden afgegaan. Bijvoorbeeld, om koekjes te gebruiken om opt-in status te bepalen, plaats een gegevenselement om dat koekje te lezen en het als voorwaarde in de regel te gebruiken om te bepalen wanneer te om de Send actie van het Bandje in werking te stellen.

U kunt afzonderlijk overwegen het [Adobe opt-in-object](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) te gebruiken om het vuren van deze tag te besturen in overleg met uw platform voor toestemmingsbeheer.

De integratie met toestemmingsmanagers (zoals OneTrust) kan de toestemmingskoekjes voor klanten plaatsen en volgen, die dan in de regelbouwer kunnen worden gebruikt.

## Audience Manager

DIL wordt momenteel automatisch geactiveerd als deze op een klantpagina is geplaatst. Overweeg het gebruik van het [Adobe opt-in-object](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) om het vuren van deze tag te controleren in overleg met uw platform voor toestemmingsbeheer.

[!DNL Adobe] adviseert dat u server-kant het door:sturen binnen gebruikt  [!DNL Analytics].

## Experience Cloud-id

[!DNL Experience Cloud ID] wordt momenteel automatisch geactiveerd als het op een klantenpagina wordt geplaatst.

Overweeg het gebruik van het [Adobe opt-in-object](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) om het vuren van deze tag te controleren in overleg met uw platform voor toestemmingsbeheer.

## Target

Adobe Experience Platform wordt niet automatisch [!DNL Target] geactiveerd. [!DNL Target] wordt alleen geactiveerd als u dit specifiek in een regelactie zegt. Gebruik de regelvoorwaarden om te bepalen wanneer en wat er moet worden afgegaan. Als u bijvoorbeeld cookies wilt gebruiken om de status opt-in te bepalen, stelt u een gegevenselement in om dat cookie te lezen en gebruikt u dit als een voorwaarde in de regel om te bepalen wanneer de handeling [!DNL Target] laden moet worden uitgevoerd.

U kunt afzonderlijk overwegen het [Adobe opt-in-object](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) te gebruiken om het vuren van deze tag te besturen in overleg met uw platform voor toestemmingsbeheer.

De integratie met toestemmingsmanagers (zoals OneTrust) kan de toestemmingskoekjes voor klanten plaatsen en volgen, die dan in de regelbouwer kunnen worden gebruikt.
