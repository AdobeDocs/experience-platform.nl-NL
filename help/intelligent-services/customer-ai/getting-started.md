---
keywords: Experience Platform;aan de slag;klantenservice;populaire onderwerpen
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Aan de slag met Customer AI
description: Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Aan de slag met Customer AI

De gidsen voor AI van de Klant vereisen een werkend inzicht in de diverse diensten van Experience Platform betrokken bij het gebruiken van AI van de Klant. Lees de volgende documenten voordat u begint:

- [ het overzicht van het Systeem van Gegevens van de Ervaring Model (XDM) ](../../xdm/home.md): XDM is het basiskader dat [!DNL Adobe Experience Cloud], aangedreven door Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op precies het juiste moment te leveren. De methodologie waarop Experience Platform, het Systeem van XDM, wordt gebouwd exploiteert de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van Experience Platform.
- [ Grondbeginselen van schemacompositie ](../../xdm/schema/composition.md): Dit document verstrekt een inleiding aan de schema&#39;s van het Model van Gegevens van de Ervaring (XDM) en de bouwstenen, de principes, en beste praktijken voor het samenstellen van schema&#39;s die in [!DNL Adobe Experience Platform] moeten worden gebruikt.
- [ de schema&#39;s van de Bouw ](../../xdm/tutorials/create-schema-ui.md): Dit leerprogramma behandelt de stappen voor het creëren van een schema gebruikend de Redacteur van het Schema binnen Experience Platform.
- [ Real-Time overzicht van het Profiel van de Klant ](../../rtcdp/overview.md): Voortgebouwd op [!DNL Adobe Experience Platform], helpt Adobe Real-Time Customer Data Platform (Real-Time CDP) bedrijven bekende en onbekende gegevens samenbrengen om klantenprofielen met intelligente besluiten door de klantenreis te activeren. Real-Time CDP combineert meerdere bedrijfsgegevensbronnen om uniforme profielen in real-time te maken die kunnen worden gebruikt om een-op-een gepersonaliseerde klantenervaring op alle kanalen en apparaten te bieden.
- [ Overzicht van de Dienst van de Segmentatie ](../../segmentation/home.md): De segmentatie is het proces om specifieke attributen of gedrag te bepalen dat door een ondergroep van profielen van uw opslag van het Profiel wordt gedeeld om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. In een e-mailcampagne met de naam &quot;Hebt u vergeten uw gulders te kopen?&quot; wilt u bijvoorbeeld een publiek van alle gebruikers die in de afgelopen 30 dagen naar schoenen hebben gezocht, maar die geen aankoop hebben gedaan. Met behulp van verschillende segmenten kunt u zich richten op uw verschillende doelgroepen en een meer aangepaste marketingervaring bieden.
- [ de gebruikersgids van de Bouwer van het Segment ](../../segmentation/tutorials/create-a-segment.md): Experience Platform staat u toe om tot segmenten gemakkelijk tot stand te brengen en toegang te hebben, evenals verschillende bouwstenen te gebruiken om uw segmenten verder te karakteriseren.

## AI-scores van klanten downloaden

>[!NOTE]
>
>Als u geen ruwe scores moet downloaden, kunt u deze stap overslaan en aan de [ configuratiegids ](./user-guide/configure.md) te werk gaan.

Het downloaden van AI-scores van de Klant gebeurt via een combinatie van API-aanroepen. Om vraag aan Experience Platform APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen aan Experience Platform API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in Experience Platform, zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md) in de het oplossen van problemengids van Experience Platform te lezen.

## Volgende stappen

Zodra u de stappen hebt voltooid die in het document hierboven worden geschetst, bezoek de [ input en documentatie van de Output ](./data-requirements.md). In dit document wordt een kort overzicht gegeven van de soorten gegevens die in de AI van de Klant worden gebruikt en geproduceerd.
