---
title: Adobe Analytics View in Assurance
description: In deze handleiding wordt uitgelegd hoe u Adobe Analytics kunt gebruiken met Adobe Experience Platform Assurance.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 515f58175a8ccba03581ce4d7faf23fdfed3571e
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# Adobe Analytics View in Assurance

>[!IMPORTANT]
>
>De mening van de Gebeurtenissen van Analytics wordt geconsolideerd in de **Gebeurtenissen 2.0 van de Analyse (Beta) stop**.  Het zal in de toekomst uit de betrouwbaarheidsverklaring worden geschrapt. Wij adviseren om de **Gebeurtenissen 2.0 van de Analyse (Beta) stop** voor uw Analytics te gebruiken zuiverend voor de zittingen van de Verzekering.

De integratie van Adobe Experience Platform Assurance met Adobe Analytics biedt gebruikers die fouten opsporen en hun Adobe Analytics-implementatie valideren een rijkere weergave van SDK-gebeurtenissen. De mening toont nu levenscyclus en actie/staatsgebeurtenissen die naar Adobe Analytics van [ worden verzonden SDK van Adobe Experience Platform ](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). De weergave bevat ook &quot;response&quot;-details die informatie geven over hoe de gebeurtenissen zijn verwerkt na de toepassing van de verwerkingsregels van elke rapportsuite.

![](./images/adobe-analytics/overview.png)

## Aan de slag

Controleer voordat je doorgaat of je over de volgende services beschikt:

- De [ UI van de Inzameling van Gegevens van Adobe Experience Platform ](https://experience.adobe.com/#/data-collection/)
- [ de Verzekering van Adobe Experience Platform ](https://experience.adobe.com/assurance)

Leren hoe te om Verzekering in uw toepassing te installeren, te lezen gelieve de [ het uitvoeren gids van de Verzekering ](../tutorials/implement-assurance.md).

## Status na verwerking

Nadat SDK een netwerkverzoek indient met Adobe Analytics, zal de status u vertellen als de Verzekering de naverwerkingsinformatie voor het verzoek van Adobe Analytics kon terugwinnen.

Houd er rekening mee dat de aangemelde gebruiker toegang moet hebben tot de bijbehorende rapportsuite om informatie na de verwerking op te halen.

| Status | Beschrijving |
| :----- | :---------- |
| `Queued` | Het netwerkverzoek haalt de postverwerkingsinformatie op. |
| `Processed` | Het netwerkverzoek is gelukt en de naverwerkingsgegevens zijn ontvangen. |
| `Delayed` | Het maximumaantal verzoeken om de naverwerkingsgegevens op te halen is overschreden. |
| `Error` | Een fout veroorzaakte het netwerkverzoek om te ontbreken. Meer informatie over de fout wordt weergegeven in de weergave met gebeurtenisdetails. |
| `Unauthorized` | De gebruiker heeft geen toegang tot de Adobe Analytics-rapportsuite. |
| `Unavailable` | De Adobe Analytics-aanvraag heeft geen overeenkomende `AnalyticsResponse` -gebeurtenis. |
| `No Debug Flag` | De huidige Adobe Analytics- of Assurance SDK-versie biedt mogelijk geen ondersteuning voor de functie Foutopsporing bij analyse. Voor meer informatie, te lezen gelieve de [ gids van het Oplossen van problemen ](../troubleshooting.md). |
| `Expired` | De gebeurtenis `AnalyticsTrack` of `LifecycleStart` is ouder dan 24 uur. |

## Weergave Gebeurtenisdetails

Voor een gebeurtenis in het vak Analytics track bevat de gedetailleerde weergave de volgende waardevolle onderdelen:

- Een oorspronkelijke SDK Analytics-aanvraaggebeurtenis.
- OOTB-meta- en contextgegevens uit de aanvraag, zoals id van de rapportsuite, SDK-extensieversies, OOTB-contextgegevens, enzovoort.
- Nabewerkte informatie over de gebeurtenis Analytics die het in kaart brengen van terugval, gebeurtenissen, steunen, etc. bevat.
