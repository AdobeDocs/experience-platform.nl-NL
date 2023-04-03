---
title: Adobe Analytics View in Assurance
description: In deze handleiding wordt uitgelegd hoe u Adobe Analytics kunt gebruiken met Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Adobe Analytics View in Assurance

De integratie van Adobe Experience Platform Assurance met Adobe Analytics biedt gebruikers die fouten opsporen en hun Adobe Analytics-implementatie valideren een rijkere weergave van SDK-gebeurtenissen. In de weergave worden nu de levenscyclus en actie-/statusgebeurtenissen weergegeven die vanuit de [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). De weergave bevat ook &quot;response&quot;-details die informatie geven over hoe de gebeurtenissen zijn verwerkt na de toepassing van de verwerkingsregels van elke rapportsuite.

![](./images/adobe-analytics/overview.png)

## Aan de slag

Controleer voordat je doorgaat of je de volgende services hebt:

- De [UI voor gegevensverzameling van Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Als u wilt weten hoe u Verzekering in uw toepassing installeert, leest u de [Implementatie van de betrouwbaarheidsgids](../tutorials/implement-assurance.md).

## Status na verwerking

Nadat SDK een netwerkverzoek indient met Adobe Analytics, zal de status u vertellen als de Verzekering de naverwerkingsinformatie voor het verzoek van Adobe Analytics kon terugwinnen.

Houd er rekening mee dat de aangemelde gebruiker toegang moet hebben tot de bijbehorende rapportsuite om informatie na de verwerking op te halen.

| Status | Beschrijving |
| :----- | :---------- |
| `Queued` | Het netwerkverzoek haalt de post-verwerkingsinformatie op. |
| `Processed` | Het netwerkverzoek is gelukt en de naverwerkingsgegevens zijn ontvangen. |
| `Delayed` | Het maximumaantal verzoeken om de naverwerkingsgegevens op te halen is overschreden. |
| `Error` | Een fout veroorzaakte het netwerkverzoek om te ontbreken. Meer informatie over de fout wordt weergegeven in de weergave met gebeurtenisdetails. |
| `Unauthorized` | De gebruiker heeft geen toegang tot de Adobe Analytics-rapportsuite. |
| `Unavailable` | Het Adobe Analytics-verzoek heeft geen overeenkomende `AnalyticsResponse` gebeurtenis. |
| `No Debug Flag` | De huidige Adobe Analytics- of Assurance SDK-versie biedt mogelijk geen ondersteuning voor de functie Foutopsporing bij analyse. Lees voor meer informatie de [Handleiding voor probleemoplossing](../troubleshooting.md). |
| `Expired` | De `AnalyticsTrack` of `LifecycleStart` de gebeurtenis is ouder dan 24 uur. |

## Weergave Gebeurtenisdetails

Voor een gebeurtenis in het vak Analytics track bevat de gedetailleerde weergave de volgende waardevolle onderdelen:

- Een oorspronkelijke SDK Analytics-aanvraaggebeurtenis.
- OOTB-meta- en contextgegevens uit de aanvraag, zoals id van de rapportsuite, SDK-extensieversies, OOTB-contextgegevens, enzovoort.
- Nabewerkte informatie over de gebeurtenis Analytics die het in kaart brengen van terugval, gebeurtenissen, steunen, etc. bevat.
