---
title: JavaScript-tags gebruiken om de toestemming van de klant te beheren
description: Leer hoe u in Adobe Experience Platform de keuze- en opt-outsignalen van klanten voor verschillende Adobe-oplossingen kunt beheren.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# JavaScript-tags gebruiken om de toestemming van de klant te beheren

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Wettelijke privacyregels zoals de algemene gegevensbeschermingsverordening (GDPR) vereisen dat bedrijven toestemming voor hun gebruikers kunnen beheren. Adobe-klanten kunnen bezoekers vragen zich aan te melden voordat Adobe-oplossingen voor een bepaalde bezoeker worden uitgevoerd. Bezoekers moeten hun opt-in- en opt-out-status kunnen beheren.

Adobe Experience Cloud-klanten hebben verschillende implementaties van deze vereisten nodig. Sommigen gebruiken toestemmingsmanagers op bedrijfsniveau en anderen bouwen hun eigen.

Ontwikkelaars van Adobe Experience Platform-extensies gebruiken extensies en de builder van regels om opt-in- en opt-out-oplossingen te definiëren.

Dit document bevat informatie over hoe u kunt voorkomen dat Adobe-tags worden geactiveerd totdat de toestemming is verkregen.

## Advertising Cloud

Adobe Experience Platform wordt niet geactiveerd [!DNL Advertising Cloud] automatisch. [!DNL Advertising Cloud] wordt alleen geactiveerd als u dit specifiek in een regelhandeling opgeeft. Gebruik de regelvoorwaarden om te bepalen wanneer en wat er moet worden afgegaan. Bijvoorbeeld, om koekjes te gebruiken om opt-in status te bepalen, plaats een gegevenselement om dat koekje te lezen en het als voorwaarde in de regel te gebruiken om te bepalen wanneer om de actie van de Omzetting van het Spoor in werking te stellen.

De integratie met toestemmingsmanagers (zoals OneTrust) kan de toestemmingskoekjes voor klanten plaatsen en volgen, die dan in de regelbouwer kunnen worden gebruikt.

## Analytics

In het gedeelte Koppeling bijhouden van het dialoogvenster [!DNL Analytics] van de uitbreiding configuratiemontages, zorg ervoor het volgende zijn *niet* geselecteerd:

* Download-koppelingen volgen
* Uitgaande koppelingen bijhouden

Als deze instellingen niet zijn geselecteerd, wordt het Platform niet geactiveerd [!DNL Adobe Analytics] automatisch. [!DNL Analytics] wordt alleen geactiveerd als u dit specifiek in een regelactie zegt. Gebruik de regelvoorwaarden om te bepalen wanneer en wat er moet worden afgegaan. Bijvoorbeeld, om koekjes te gebruiken om opt-in status te bepalen, plaats een gegevenselement om dat koekje te lezen en het als voorwaarde in de regel te gebruiken om te bepalen wanneer te om de Send actie van het Bandje in werking te stellen.

U kunt overwegen om de [Adobe-opt-in-object](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) om te controleren of deze tag wordt afgevuurd in overleg met uw platform voor toestemmingsbeheer.

De integratie met toestemmingsmanagers (zoals OneTrust) kan de toestemmingskoekjes voor klanten plaatsen en volgen, die dan in de regelbouwer kunnen worden gebruikt.

## Audience Manager

DIL wordt momenteel automatisch geactiveerd als deze op een klantpagina is geplaatst. Gebruik de [Adobe-opt-in-object](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) om te controleren of deze tag wordt afgevuurd in overleg met uw platform voor toestemmingsbeheer.

[!DNL Adobe] adviseert u server-kant het door:sturen binnen gebruikt [!DNL Analytics].

## Experience Cloud-id

[!DNL Experience Cloud ID] wordt momenteel automatisch geactiveerd als het op een klantenpagina wordt geplaatst.

Gebruik de [Adobe-opt-in-object](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) om te controleren of deze tag wordt afgevuurd in overleg met uw platform voor toestemmingsbeheer.

## Target

Adobe Experience Platform wordt niet geactiveerd [!DNL Target] automatisch. [!DNL Target] wordt alleen geactiveerd als u dit specifiek in een regelactie zegt. Gebruik de regelvoorwaarden om te bepalen wanneer en wat er moet worden afgegaan. Als u bijvoorbeeld cookies wilt gebruiken om de status van aanmelden te bepalen, stelt u een gegevenselement in om dat cookie te lezen en gebruikt u het als een voorwaarde in de regel om te bepalen wanneer het laden moet worden uitgevoerd [!DNL Target] handeling.

U kunt overwegen om de [Adobe-opt-in-object](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) om te controleren of deze tag wordt afgevuurd in overleg met uw platform voor toestemmingsbeheer.

De integratie met toestemmingsmanagers (zoals OneTrust) kan de toestemmingskoekjes voor klanten plaatsen en volgen, die dan in de regelbouwer kunnen worden gebruikt.
