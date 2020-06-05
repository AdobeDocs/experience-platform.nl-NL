---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Aan de slag met Customer AI
topic: Getting started
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Aan de slag met Customer AI

De gidsen voor AI van de Klant vereisen een werkend inzicht in de diverse diensten van het Platform betrokken bij het gebruiken van AI van de Klant. Lees de volgende documenten voordat u begint:

- [XDM-systeemoverzicht](../../xdm/home.md)(Experience Data Model): XDM is het grondkader dat, [!DNL Adobe Experience Cloud]aangedreven door het Platform van de Ervaring, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op precies het juiste moment te leveren. De methodologie waarop het Platform van de Ervaring wordt gebouwd, het Systeem van XDM, exploiteert de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform.
- [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Dit document verstrekt een inleiding aan de schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) en de bouwstenen, beginselen, en beste praktijken voor het samenstellen van schema&#39;s die binnen moeten worden gebruikt [!DNL Adobe Experience Platform].
- [Gebouwenschema&#39;s](../../xdm/tutorials/create-schema-ui.md): Deze zelfstudie behandelt de stappen voor het maken van een schema met behulp van de Schema-editor in het Experience Platform.
- [Overzicht](../../rtcdp/overview.md)van realtime-klantprofiel: Gebaseerd op [!DNL Adobe Experience Platform], [!DNL Adobe Real-time Customer Data Platform] (In real time CDP) helpt bedrijven bekende en onbekende gegevens samenbrengen om klantenprofielen met intelligente besluitvorming door de klantenreis te activeren. CDP in real time combineert veelvoudige bronnen van ondernemingsgegevens om verenigde profielen in real time tot stand te brengen die kunnen worden gebruikt om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.
- [Overzicht](../../segmentation/home.md)van de segmentatieservice: De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van profielen van uw profielopslag worden gedeeld om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. In een e-mailcampagne met de naam &quot;Hebt u vergeten uw gulders te kopen?&quot; wilt u bijvoorbeeld een publiek van alle gebruikers die in de afgelopen 30 dagen naar schoenen hebben gezocht, maar die geen aankoop hebben gedaan. Met behulp van verschillende segmenten kunt u zich richten op uw verschillende doelgroepen en een meer aangepaste marketingervaring bieden.
- [Gebruikershandleiding voor](../../segmentation/tutorials/create-a-segment.md)Segment Builder: Met Platform kunt u eenvoudig segmenten maken en openen en kunt u verschillende bouwstenen gebruiken om uw segmenten verder te karakteriseren.

## AI-scores van klanten downloaden

>[!NOTE] Als u geen onbewerkte scores hoeft te downloaden, kunt u deze stap overslaan en doorgaan naar de [configuratiegids](./user-guide/configure.md).

Het downloaden van AI-scores van de Klant gebeurt via een combinatie van API-aanroepen. Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

## Volgende stappen

Nadat u de in het bovenstaande document beschreven stappen hebt uitgevoerd, gaat u naar de documentatie bij [Invoer en Uitvoer](./input-output.md) . In dit document wordt een kort overzicht gegeven van de soorten gegevens die in de AI van de Klant worden gebruikt en geproduceerd.