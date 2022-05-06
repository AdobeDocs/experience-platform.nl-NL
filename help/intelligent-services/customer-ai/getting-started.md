---
keywords: Experience Platform;aan de slag;klantenservice;populaire onderwerpen
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Aan de slag met Customer AI
topic-legacy: Getting started
description: Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Aan de slag met Customer AI

De gidsen voor AI van de Klant vereisen een werkend inzicht in de diverse diensten van het Platform betrokken bij het gebruiken van AI van de Klant. Lees de volgende documenten voordat u begint:

- [Overzicht van XDM (Experience Data Model)](../../xdm/home.md): XDM is het basiskader dat toestaat [!DNL Adobe Experience Cloud], aangedreven door Experience Platform, om het juiste bericht te leveren aan de juiste persoon, op het juiste kanaal, op precies het juiste moment. De methodologie waarop het Experience Platform wordt gebouwd, het Systeem van XDM, stelt de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform in werking.
- [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Dit document verstrekt een inleiding aan de schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) en de bouwstenen, de beginselen, en beste praktijken voor het samenstellen van schema&#39;s die in moeten worden gebruikt [!DNL Adobe Experience Platform].
- [Bouwschema&#39;s](../../xdm/tutorials/create-schema-ui.md): Deze zelfstudie behandelt de stappen voor het maken van een schema met de Schema-editor in het Experience Platform.
- [Overzicht van het realtime klantprofiel](../../rtcdp/overview.md): Gebaseerd op [!DNL Adobe Experience Platform]Real-time Customer Data Platform (Real-time CDP) helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen met intelligente besluitvorming tijdens de reis van de klant te activeren. CDP in real time combineert veelvoudige bronnen van ondernemingsgegevens om verenigde profielen in real time tot stand te brengen die kunnen worden gebruikt om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.
- [Overzicht van segmentatieservice](../../segmentation/home.md): De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van profielen van uw profielopslag worden gedeeld om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. In een e-mailcampagne met de naam &quot;Hebt u vergeten uw gulders te kopen?&quot; wilt u bijvoorbeeld een publiek van alle gebruikers die in de afgelopen 30 dagen naar schoenen hebben gezocht, maar die geen aankoop hebben gedaan. Met behulp van verschillende segmenten kunt u zich richten op uw verschillende doelgroepen en een meer aangepaste marketingervaring bieden.
- [Gebruikershandleiding voor Segment Builder](../../segmentation/tutorials/create-a-segment.md): Met Platform kunt u eenvoudig segmenten maken en openen en kunt u verschillende bouwstenen gebruiken om uw segmenten verder te karakteriseren.

## AI-scores van klanten downloaden

>[!NOTE]
>
>Als u geen RAW-scores hoeft te downloaden, kunt u deze stap overslaan en doorgaan naar de [configuratiegids](./user-guide/configure.md).

Het downloaden van AI-scores van de Klant gebeurt via een combinatie van API-aanroepen. Als u aanroepen wilt uitvoeren naar Platform-API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in Platform raadpleegt u de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md) in de gids voor het oplossen van problemen met Experience Platforms.

## Volgende stappen

Als u de in het bovenstaande document beschreven stappen hebt uitgevoerd, gaat u naar de [Invoer en uitvoer](./input-output.md) documentatie. In dit document wordt een kort overzicht gegeven van de soorten gegevens die in de AI van de Klant worden gebruikt en geproduceerd.
