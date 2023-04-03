---
title: Weergave Gebeurtenistransformaties
description: Deze handleiding bevat informatie over de weergave Gebeurtenistransacties in Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---


# Gebeurtenistransformaties, weergave

Met de weergave Gebeurtenistransformaties in Adobe Experience Platform Assurance kunt u de implementatie van uw Edge Network-client valideren en er fouten in opsporen. De resultaten van upstreamvalidatie worden dan in real-time weergegeven.

## De Verzekering van de opstelling voor het werkschema van het Netwerk van de Rand

Na [Betrouwbaarheid instellen](../tutorials/implement-assurance.md), dient u ervoor te zorgen dat u de nieuwste versies van de extensies voor Betrouwbaarheid en Edge Network hebt geïmplementeerd in uw app.

Selecteer in het linkermenu de optie **[!UICONTROL Event Transactions]** onder de **[!UICONTROL Adobe Experience Platform Edge]** sectie.

Als deze optie niet wordt weergegeven, selecteert u **[!UICONTROL Configure]** linksonder in het venster voegt u de opdracht **[!UICONTROL Event Transactions]** weergeven en selecteren **[!UICONTROL Save]**.

## Aan de slag met de weergave Gebeurtenistransformaties

In deze sectie leert u vertrouwd te raken met de weergave Gebeurtenistransactie en hoe u deze efficiënt kunt gebruiken voor end-to-end validatie in Edge Network-workflows.

### Stroom van gebeurtenisverwerking

![Weergave Gebeurtenistransacties](./images/event-transactions/event-transactions-view.png)

In de weergave Gebeurtenistransformaties worden drie kolommen weergegeven in de volgorde van de gebeurtenisverwerkingsstroom:

- **[!UICONTROL Client-side]**: In deze kolom worden de verwerkte of ontvangen gebeurtenissen weergegeven die toegankelijk zijn voor de mobiele SDK. Dit omvat de gebeurtenissen die zijn gemaakt met een API-aanroep, zoals `Edge.sendEvent`en de gebeurtenishandgrepen voor reacties die de client van de Edge Network-server heeft ontvangen, indien aanwezig. Voorbeelden van gebeurtenissen aan de clientzijde:
   - De AEP-aanvraaggebeurtenis is de gebeurtenis die via de Edge-extensie wordt verzonden en bevat de XDM en optionele vrije-formuliergegevens.
   - AEP Response Event Handle is de gebeurtenisgreep die van Edge Network wordt ontvangen als reactie op een AEP Request-gebeurtenis. Een aanvraaggebeurtenis kan geen, één of meerdere handvatten van de reactiegebeurtenis ontvangen.
   - De Respons van de Fout van AEP kan in het geval van een fout worden gezien, bijvoorbeeld als de nuttige lading XDM niet kon worden verwerkt of als één van de stroomopwaartse diensten een fout of een waarschuwing teruggaf.
- **[!UICONTROL Edge Network]**: Deze kolom toont de gebeurtenis die server-kant door het Netwerk van de Rand door een netwerkverzoek wordt ontvangen en welke gegevens en meta-gegevens de gebeurtenis bevatte.
- **[!UICONTROL Upstream]**: Deze kolom toont de gebeurtenissen die door de gevormde stroomopwaartse diensten, met inbegrip van gedetailleerde informatie over de verwerking en/of bevestigingsresultaten voor de inkomende gebeurtenis worden ontvangen.
Deze kolom is dynamisch en kan verschillende soorten informatie weergeven, afhankelijk van twee belangrijke factoren:
   - De configuratie van de gegevensstroom en de diensten die op het worden toegelaten.
   - Het type gebeurtenis dat naar het Edge-netwerk wordt verzonden.

### Inspect-gebeurtenissen

De gebeurtenissen die worden weergegeven in de weergave Gebeurtenistransacties bieden informatie over de indeling en inhoud van de gegevens die worden verwerkt in elk frame, en bevatten inzichtelijke details over waarschuwingen of fouten die optreden wanneer de gegevens upstream worden verwerkt. De weergave helpt de foutopsporingsinformatie op het niveau van de gebeurtenis/aanvraag te vernauwen en fouten in een vroeg stadium in de ontwikkelingscyclus te identificeren.

#### De gebeurtenisdetails uitvouwen

Als u een gebeurtenis wilt inspecteren, selecteert u de gewenste gebeurtenis in de weergave. Met deze handeling breidt u de **[!UICONTROL Event Details]** aan de rechterkant van het scherm.
Geneste gegevens worden weergegeven in een boomstructuur. U kunt geneste toetswaarden controleren door de optie **+** (plus) links van de sleutelnaam.

![Gebeurtenisdetails](./images/event-transactions/event-details.png)

#### Inspect-waarschuwingen of -fouten

Elke gebeurtenisnaam wordt voorafgegaan door een pictogram dat de status op hoog niveau van de verwerking voor die gebeurtenis aangeeft:

- Als de gebeurtenis correct is verwerkt, wordt een groen vinkje weergegeven.
- Als er waarschuwingen of fouten zijn gedetecteerd, wordt een waarschuwingsteken weergegeven. Selecteer de gerelateerde gebeurtenis voor meer informatie over de oorzaak van de waarschuwing of fout in het dialoogvenster **[!UICONTROL Event Details]** weergeven.

### Configuratie-instellingen

U kunt de huidige ID van de gegevensstroom controleren door info tooltip naast te selecteren **[!UICONTROL Edge Network]** kolomkop.

![De gegevensstroom-id weergeven](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>Wanneer de veelvoudige cliënten met de zelfde zitting van de Verzekering en verschillende datastream IDs verbinden wordt gebruikt, zult u alle hier getoond hen zien. Nochtans, betekent dit niet dat uw huidige implementatie veelvoudige gegevensstromen gebruikt. Alleen de huidige gegevensstroom-id die is ingesteld in de tag (eigenschap mobile) die door de app wordt gebruikt, wordt gebruikt voor het verwerken van nieuwe gebeurtenissen van die client. Wanneer het testen van meer gecompliceerde gebruik-gevallen met verschillende configuratiemontages en veelvoudige verbonden cliënten, kan het nuttig zijn om afzonderlijke zittingen van de Verzekering te gebruiken om het bevestigingsproces te vereenvoudigen.
