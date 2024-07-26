---
title: Analytische gebeurtenissen 2.0 in betrouwbaarheid
description: In deze handleiding wordt uitgelegd hoe u de weergave Adobe Analytics en Analytics Edge kunt gebruiken met Adobe Experience Platform Assurance.
badgeBeta: label="Beta" type="Informative"
exl-id: faaa2c1d-3471-4d86-9a25-03265b996e31
source-git-commit: fcef41a1cf3f082a437e2ceeb9203793c6a20c36
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 0%

---

# Analytische gebeurtenissen 2.0 in betrouwbaarheid

Analytics Events 2.0 verstrekt een rijkere mening van gebeurtenissen SDK aan gebruikers die en hun implementatie van Adobe Analytics zuiveren bevestigen. De mening toont gebeurtenissen die naar Adobe Analytics van [ worden verzonden de Edge Network SDK van Adobe Experience Platform ](https://developer.adobe.com/client-sdks/edge/edge-network/) evenals [ Mobiele SDK van Adobe Experience Platform ](https://developer.adobe.com/client-sdks/solution/adobe-analytics/). De weergave bevat ook een deelvenster met details waarin wordt uitgelegd hoe de gebeurtenis is verwerkt door de client-SDK en door de upstream-services nadat het apparaat is verlaten.

## Aan de slag

Voer de volgende stappen uit om deze weergave te gebruiken:

1. [ de Verzekering van Adobe Experience Platform van de Opstelling ](../tutorials/implement-assurance.md).
2. [ creeer en verbind met een zitting van de Verzekering ](../tutorials/using-assurance.md).
3. In de Verzekering UI van het linkernavigatie **1} meningsmenu van het Huis {, uitgezochte** Gebeurtenissen 2.0 van de Analyse (Beta) **.** Als u deze optie niet ziet, vormt de uitgezochte **** in de bodem linksonder van het venster, voegt de **Gebeurtenissen 2.0 van de Analyse toe (Beta)**, en selecteert **sparen**.

## Analyse Edge

Gebruik de mening van Edge van Analytics als u **Edge Network** of **Edge Bridge** mobiele uitbreidingen gebruikt. Deze weergave wordt ingeschakeld wanneer de schakeloptie &quot;Analytics Edge (Beta)&quot; rechtsboven wordt geactiveerd en de Analytics-gebeurtenissen worden weergegeven die in de huidige sessie via het Edge-netwerk worden verzonden. Dit omvat alle gebeurtenissen die zijn geactiveerd door de extensie Lifecycle, Edge en/of Edge Bridge.

![ een beeld dat knevel toont die aan de Mening van Edge van Analytics schakelde.](./images/adobe-analytics-edge/edge-analytics-view-toggle.png)

De Edge-weergave Analytics bevat informatie over aan Analytics gerelateerde Edge-gebeurtenissen en Lifecycle-gebeurtenissen die door de client worden verzonden. Door een gebeurtenis in de lijst te kiezen, toont het paneel van de mening van het gebeurtenisdetail op het recht de gebeurtenissen die door de cliënt SDK en door de stroomopwaartse dienst werden verwerkt nadat zij het apparaat verlieten. Dit staat u toe om de ketting van gebeurtenissen gemakkelijk te bekijken die uit een vraag voortvloeiden.

![ een beeld dat verschillende componenten in de Mening van Edge van Analytics voor het scenario van Bridge van Edge aantoont.](./images/adobe-analytics-edge/edgebridge-analytics-events.png)

De **post-Verwerkte gebeurtenis van Gegevens** in de lijst bevestigt dat de gegevens met succes zijn verwerkt en naar Adobe Analytics verzonden. Als deze gebeurtenis of verwerkte gegevens ontbreken, kunnen gebruikers elke gebeurtenis in de lijst uitvouwen om gedetailleerde foutopsporingsinformatie weer te geven.

### De gedetailleerde weergave van Edge-gebeurtenissen analyseren

Voor een Edge request-gebeurtenis of een Analytics-trackgebeurtenis bevat de gedetailleerde weergave de volgende onderdelen:

* Gebeurtenisdetails: een oorspronkelijke SDK-gebeurtenis voor randverzoeken.
* Edge Bridge Request: een gebeurtenis die uitsluitend bedoeld is voor de Edge Bridge Extension-workflow.
* DataStream: een gebeurtenis die voor datastream voor deze sessie wordt vertegenwoordigd.
* Edge Hit Received: Vertegenwoordig de hit die van Edge is ontvangen.
* Edge Hit Verwerkt: vertegenwoordigt de hit die in Edge is verwerkt.
* Analytics Hit: Vertegenwoordigt de hit die is ontvangen van Analytics.
* Analytische toewijzing: de status van de gegevenstoewijzing in Analytics.
* Analytics Responsed: The response status from Analytics.
* Nabewerkingsgegevens: informatie over de gebeurtenis die het in kaart brengen van revars, evars en props bevat.

### Analytics Edge Validation

In de validatieweergave van Analytics Edge kunt u de resultaten van validatiescripts voor Analytics Edge eenvoudig zien. Fouten die door validators worden weergegeven, kunnen koppelingen bevatten naar de locatie waar ze moeten worden hersteld of naar weergavegebeurtenissen in een foutstatus.

![ een beeld dat het validatorlusje in de mening van Edge van Analytics toont.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)

## Weergave Analytische gebeurtenissen

Gebruik de Mening van de Gebeurtenis van de Analyse als u de **mobiele uitbreiding van Adobe Analytics** gebruikt. In deze weergave kunt u gemakkelijk de gebeurtenissen Analytics zien die van uw verbonden client zijn verzonden, waaronder gebeurtenissen Track Action, Track State en Lifecycle. Deze weergave is actief terwijl de schakeloptie Analytics Edge (Beta) rechtsboven is uitgeschakeld.

![ een beeld dat knevel toont die aan de Mening van Analytics schakelde.](./images/adobe-analytics-edge/direct-analytics-view-toggle-button.png)

Als u een van de Analytics-gebeurtenissen in de gebeurtenissentabel selecteert, kunt u in het rechterdeelvenster details bekijken over de manier waarop de gebeurtenis is verwerkt.

![ een beeld dat verschillende componenten in de Mening van de Gebeurtenissen van Analytics aantoont.](./images/adobe-analytics-edge/analytics-events.png)

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
| `Unavailable` | De Adobe Analytics-aanvraag heeft geen overeenkomende `AnalyticsResponse` -gebeurtenis. |
| `No Debug Flag` | De huidige Adobe Analytics- of Assurance SDK-versie biedt mogelijk geen ondersteuning voor de functie Foutopsporing bij analyse. Voor meer informatie, te lezen gelieve de [ gids van het Oplossen van problemen ](../troubleshooting.md). |
| `Expired` | De gebeurtenis `AnalyticsTrack` of `LifecycleStart` is ouder dan 24 uur. |

### Weergave Gebeurtenisdetails

Voor een gebeurtenis in de track Analytics bevat de gedetailleerde weergave de volgende onderdelen:

* Een oorspronkelijke SDK Analytics-aanvraaggebeurtenis.
* Meta- en contextgegevens van de aanvraag, zoals id van de rapportsuite, SDK-extensieversies en contextgegevens.
* Nabewerkte informatie over de gebeurtenis Analytics die het in kaart brengen van revars, evars, en props bevat.

### Validatie van analyseweergave

In de validatieweergave kunt u gemakkelijk de resultaten bekijken van validatiescripts die betrekking hebben op Analytics. Fouten die door validators worden weergegeven, kunnen koppelingen bevatten naar de locatie waar ze moeten worden hersteld of naar weergavegebeurtenissen in een foutstatus.

![ een beeld dat het validatorlusje in de mening van Analytics toont.](./images/adobe-analytics-edge/analytics-validation-view.png)