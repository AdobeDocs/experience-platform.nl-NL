---
title: Analytische gebeurtenissen 2.0 in betrouwbaarheid
description: In deze handleiding wordt uitgelegd hoe u de Adobe Analytics- en Analytics Edge-weergave kunt gebruiken met Adobe Experience Platform Assurance.
badgeBeta: label="Beta" type="Informative"
source-git-commit: f707554ea89731fbd3f013d6065fde27ba7fa811
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# Analytische gebeurtenissen 2.0 in betrouwbaarheid

Analytics Events 2.0 verstrekken een rijkere mening van gebeurtenissen SDK aan gebruikers die en hun implementatie van Adobe Analytics zuiveren valideren. In de weergave worden gebeurtenissen weergegeven die vanuit de [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/solution/adobe-analytics/) en de [Adobe Experience Platform Edge Network SDK](https://developer.adobe.com/client-sdks/edge/edge-network/). De weergave bevat ook een deelvenster met details waarin wordt uitgelegd hoe de gebeurtenis is verwerkt door de client-SDK en door de upstreamservices nadat deze het apparaat hebben verlaten.

## Aan de slag

Voer de volgende stappen uit om deze weergave te gebruiken:

1. [Adobe Experience Platform Assurance instellen](../tutorials/implement-assurance.md).
2. [Een betrouwbaarheidssessie maken en er verbinding mee maken](../tutorials/using-assurance.md).
3. In de UI van de Verzekering van de linkernavigatie **Home** weergavemenu, selecteert u **Analytics Events 2.0 (bèta)**. Als deze optie niet wordt weergegeven, selecteert u **Configureren** linksonder in het venster voegt u de opdracht **Analytics Events 2.0 (bèta)** en selecteert u **Opslaan**.

## Weergave Analytische gebeurtenissen

Gebruik de weergave Analyse-gebeurtenis als u de optie **Adobe Analytics** mobiele extensie. In deze weergave kunt u gemakkelijk de gebeurtenissen Analytics weergeven die u van de verbonden client hebt verzonden, zoals gebeurtenissen Track Action, Track State en Lifecycle. Als u een van de Analytics-gebeurtenissen in de tabel selecteert, kunt u in het rechterdeelvenster details bekijken over de manier waarop de gebeurtenis is verwerkt.

![Een afbeelding die verschillende componenten aantoont in de weergave Analytische gebeurtenissen.](./images/adobe-analytics-edge/analytics-events.png)

### Status na verwerking

Nadat SDK een netwerkverzoek indient met Adobe Analytics, zal de status u vertellen als de Verzekering de naverwerkingsinformatie voor het verzoek van Adobe Analytics kon terugwinnen. De weergave Analytische gebeurtenissen moet actief blijven terwijl de status nabewerking actief is nadat het verzoek is geactiveerd.

Houd er rekening mee dat de aangemelde gebruiker toegang moet hebben tot de bijbehorende rapportsuite om informatie na de verwerking op te halen.

| Status | Beschrijving |
| :----- | :---------- |
| `Queued` | Het netwerkverzoek haalt de postverwerkingsinformatie op. |
| `Processed` | Het netwerkverzoek is gelukt en de naverwerkingsgegevens zijn ontvangen. |
| `Delayed` | Het maximumaantal verzoeken om de naverwerkingsgegevens op te halen is overschreden. |
| `Error` | Een fout veroorzaakte het netwerkverzoek om te ontbreken. Meer informatie over de fout wordt weergegeven in de weergave met gebeurtenisdetails. |
| `Unauthorized` | De gebruiker heeft geen toegang tot de Adobe Analytics-rapportsuite. |
| `Unavailable` | Het Adobe Analytics-verzoek heeft geen overeenkomende `AnalyticsResponse` gebeurtenis. |
| `No Debug Flag` | De huidige Adobe Analytics- of Assurance SDK-versie biedt mogelijk geen ondersteuning voor de functie Foutopsporing bij analyse. Lees voor meer informatie de [Handleiding voor probleemoplossing](../troubleshooting.md). |
| `Expired` | De `AnalyticsTrack` of `LifecycleStart` de gebeurtenis is ouder dan 24 uur. |

### Weergave Gebeurtenisdetails

Voor een gebeurtenis in de track Analytics bevat de gedetailleerde weergave de volgende onderdelen:

- Een oorspronkelijke SDK Analytics-aanvraaggebeurtenis.
- Meta- en contextgegevens van de aanvraag, zoals id van de rapportsuite, SDK-extensieversies en contextgegevens.
- Nabewerkte informatie over de gebeurtenis Analytics die het in kaart brengen van revars, evars, en props bevat.

### Validatie van analyseweergave

In de validatieweergave kunt u gemakkelijk de resultaten bekijken van validatiescripts die betrekking hebben op Analytics. Fouten die door validators worden weergegeven, kunnen koppelingen bevatten naar de locatie waar ze moeten worden hersteld of naar weergavegebeurtenissen in een foutstatus.

![Een afbeelding waarin het tabblad Validators wordt weergegeven in de weergave Analytics.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Analyserand, weergave

Gebruik de weergave Analyserand als u **Edge Network** of **Edge Bridge** mobiele extensies. U schakelt deze weergave in door de schakeloptie &quot;Analytics Edge (Beta)&quot; in de rechterbovenhoek te selecteren om de Analytics-gebeurtenissen te bekijken die via het Edge-netwerk in de huidige sessie zijn verzonden. Dit omvat alle gebeurtenissen die zijn geactiveerd door de Lifecycle-extensie, Edge-verzoeken en/of Edge Bridge-gebeurtenissen op basis van Handeling bijhouden en Status track.

![Een afbeelding die schakelt tussen Analytics View en Analytics Edge View.](./images/adobe-analytics-edge/analytics-view-toggle.png)

De weergave Analytics Edge bevat informatie over Edge-verzoeken en levenscyclusmethoden die door de client worden verzonden en die betrekking hebben op Analytics. Door een gebeurtenis in de lijst te kiezen, toont het juiste paneel de gebeurtenissen die door de cliënt SDK, evenals door de stroomopwaartse dienst werden verwerkt nadat zij het apparaat verlieten, zodat kunt u de ketting van gebeurtenissen gemakkelijk bekijken die uit een vraag voortkwamen.

![Een afbeelding die verschillende componenten aantoont in de Edge View van Analytics.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Analytics Edge Validation

In de validatieweergave Analytics Edge kunt u de resultaten van validatiescripts voor Analytics Edge eenvoudig bekijken. Fouten die door validators worden weergegeven, kunnen koppelingen bevatten naar de locatie waar ze moeten worden hersteld of naar weergavegebeurtenissen in een foutstatus.

![Een afbeelding waarin het tabblad validators wordt weergegeven in de weergave Rand van Analytics.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
