---
title: Analytische gebeurtenissen 2.0 in betrouwbaarheid
description: In deze handleiding wordt uitgelegd hoe u de weergave Adobe Analytics en Analytics Edge kunt gebruiken met Adobe Experience Platform Assurance.
badgeBeta: label="Beta" type="Informative"
exl-id: faaa2c1d-3471-4d86-9a25-03265b996e31
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# Analytische gebeurtenissen 2.0 in betrouwbaarheid

Analytics Events 2.0 verstrekken een rijkere mening van gebeurtenissen SDK aan gebruikers die en hun implementatie van Adobe Analytics zuiveren valideren. De mening toont gebeurtenissen die naar Adobe Analytics van [ worden verzonden Mobiele SDK van Adobe Experience Platform ](https://developer.adobe.com/client-sdks/solution/adobe-analytics/) evenals [ Adobe Experience Platform Edge Network SDK ](https://developer.adobe.com/client-sdks/edge/edge-network/). De weergave bevat ook een deelvenster met details waarin wordt uitgelegd hoe de gebeurtenis is verwerkt door de client-SDK en door de upstreamservices nadat deze het apparaat hebben verlaten.

## Aan de slag

Voer de volgende stappen uit om deze weergave te gebruiken:

1. [ de Verzekering van Adobe Experience Platform van de Opstelling ](../tutorials/implement-assurance.md).
2. [ creeer en verbind met een zitting van de Verzekering ](../tutorials/using-assurance.md).
3. In de Verzekering UI van het linkernavigatie **1} meningsmenu van het Huis {, uitgezochte** Gebeurtenissen 2.0 van de Analyse (Beta) **.** Als u deze optie niet ziet, vormt de uitgezochte **** in de bodem linksonder van het venster, voegt de **Gebeurtenissen 2.0 van de Analyse toe (Beta)**, en selecteert **sparen**.

## Weergave Analytische gebeurtenissen

Gebruik de Mening van de Gebeurtenis van de Analyse als u de **mobiele uitbreiding van Adobe Analytics** gebruikt. In deze weergave kunt u gemakkelijk de gebeurtenissen Analytics weergeven die u van de verbonden client hebt verzonden, zoals gebeurtenissen Track Action, Track State en Lifecycle. Als u een van de Analytics-gebeurtenissen in de tabel selecteert, kunt u in het rechterdeelvenster details bekijken over de manier waarop de gebeurtenis is verwerkt.

![ een beeld dat verschillende componenten in de Mening van de Gebeurtenissen van Analytics aantoont.](./images/adobe-analytics-edge/analytics-events.png)

### Post-status

Nadat SDK een netwerkverzoek indient met Adobe Analytics, zal de status u vertellen als de Verzekering de naverwerkingsinformatie voor het verzoek van Adobe Analytics kon terugwinnen. De weergave Analytische gebeurtenissen moet actief blijven terwijl de status nabewerking actief is nadat het verzoek is geactiveerd.

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

### Weergave Gebeurtenisdetails

Voor een gebeurtenis in de track Analytics bevat de gedetailleerde weergave de volgende onderdelen:

- Een oorspronkelijke SDK Analytics-aanvraaggebeurtenis.
- Meta- en contextgegevens van de aanvraag, zoals id van de rapportsuite, SDK-extensieversies en contextgegevens.
- Post-verwerkte informatie over de gebeurtenis Analytics die het in kaart brengen van revars, evars, en props bevat.

### Validatie van analyseweergave

In de validatieweergave kunt u gemakkelijk de resultaten bekijken van validatiescripts die betrekking hebben op Analytics. Fouten die door validators worden weergegeven, kunnen koppelingen bevatten naar de locatie waar ze moeten worden hersteld of naar weergavegebeurtenissen in een foutstatus.

![ een beeld dat het validatorlusje in de mening van Analytics toont.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Analyse Edge

Gebruik de mening van Edge van Analytics als u **Edge Network** of **Edge Bridge** mobiele uitbreidingen gebruikt. U schakelt deze weergave in door de schakeloptie &quot;Analytics Edge (Beta)&quot; in de rechterbovenhoek te selecteren om de Analytics-gebeurtenissen te bekijken die via het Edge-netwerk in de huidige sessie zijn verzonden. Dit omvat alle gebeurtenissen die zijn geactiveerd door de Lifecycle-extensie, Edge-verzoeken en/of Edge Bridge-gebeurtenissen op basis van Actie bijhouden en Status bijhouden.

![ een beeld dat knevel toont die voor omschakeling tussen de Mening van de Analyse en de Mening van Edge van Analytics gebruikte.](./images/adobe-analytics-edge/analytics-view-toggle.png)

De weergave Analytics Edge bevat informatie over Edge-verzoeken en levenscyclusmethoden die door de client worden verzonden en die betrekking hebben op Analytics. Door een gebeurtenis in de lijst te kiezen, toont het juiste paneel de gebeurtenissen die door de cliënt SDK, evenals door de stroomopwaartse dienst werden verwerkt nadat zij het apparaat verlieten, zodat kunt u de ketting van gebeurtenissen gemakkelijk bekijken die uit een vraag voortkwamen.

![ een beeld dat verschillende componenten in de Mening van Edge van Analytics aantoont.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Analytics Edge Validation

In de validatieweergave van Analytics Edge kunt u de resultaten van validatiescripts voor Analytics Edge eenvoudig bekijken. Fouten die door validators worden weergegeven, kunnen koppelingen bevatten naar de locatie waar ze moeten worden hersteld of naar weergavegebeurtenissen in een foutstatus.

![ een beeld dat het validatorlusje in de mening van Edge van Analytics toont.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
