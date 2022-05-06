---
keywords: Experience Platform;aan de slag;attributie ai;populaire onderwerpen
feature: Attribution AI
title: Aan de slag in de Attribution AI
topic-legacy: Getting started
description: De volgende gidsen vereisen een inzicht in de diverse diensten van Adobe Experience Platform betrokken bij het gebruiken van Attribution AI. Lees de volgende documenten voordat u de zelfstudies start.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Aan de slag met Attribution AI

De volgende hulplijnen vereisen een goed begrip van de verschillende [!DNL Adobe Experience Platform] diensten in verband met het gebruik van Attribution AI. Lees de volgende documenten voordat u de zelfstudies start:

- [Overzicht van XDM (Experience Data Model)](../../xdm/home.md): XDM is het basiskader dat toestaat [!DNL Adobe Experience Cloud], aangedreven door Experience Platform, om het juiste bericht te leveren aan de juiste persoon, op het juiste kanaal, op precies het juiste moment. De methodologie waarop het Experience Platform wordt gebouwd, het Systeem van XDM, stelt de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform in werking.
- [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Dit document verstrekt een inleiding aan de schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) en de bouwstenen, de beginselen, en beste praktijken voor het samenstellen van schema&#39;s die in moeten worden gebruikt [!DNL Adobe Experience Platform].
- [Bouwschema&#39;s](../../xdm/tutorials/create-schema-ui.md): Deze zelfstudie behandelt de stappen voor het maken van een schema met de Schema-editor in het Experience Platform.

Attribution AI vereist datasets om met het schema van de Gebeurtenissen van de Ervaring van de Consumenten (CEE) in overeenstemming te zijn, dat een [Experience Data Model (XDM)](../../xdm/home.md) schemaveldgroep. Neem contact op met de ondersteuning van Adobe op attributionai-support@adobe.com om deze gegevens te implementeren of te wijzigen. Als er gegevens over mediaconcentages aanwezig zijn, kunt u verdere analyses uitvoeren, zoals incrementele inkomsten en ROI. Als de gegevens van het klantenprofiel beschikbaar zijn, kunt u kredieten aan het niveau van het klantenprofiel verder toeschrijven.

## Terminologie

- **Conversiegebeurtenis:** Elke digitale gebeurtenis of digitale interactie die klanten uitvoeren om een mijlpaal in de richting van een doel aan te geven, zoals conferentieregistraties. Tot de extra voorbeelden behoren betaalde conversies, gratis accountaanmeldingen of het in aanmerking komen voor een doel.

- **Aanraakpunt:** Elke digitale gebeurtenis of digitale interactie die klanten uitvoeren op het pad naar een doel. Voorbeelden hiervan zijn marketingactiviteiten vóór de aankoop, weergave van bekeken advertenties en betaalde zoekopdrachten.

## Attribution AI-scores downloaden

>[!NOTE]
>
>Als u geen RAW-scores hoeft te downloaden, kunt u deze stap overslaan en doorgaan naar de [volgende stappen](#next-steps).

Het downloaden van de scores van Attribution AI wordt gedaan door een combinatie API vraag. Als u aanroepen wilt uitvoeren naar Platform-API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

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

## Volgende stappen {#next-steps}

Zodra u klaar bent en al uw geloofsbrieven en schema&#39;s op zijn plaats hebt, begin door te volgen [Handleiding voor de gebruikersinterface van Attribution AI](./user-guide.md). Deze gids begeleidt u door het creëren van een geval en het voorleggen van het voor opleiding en het scoren.
