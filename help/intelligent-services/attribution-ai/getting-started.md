---
keywords: Experience Platform;aan de slag;attributie ai;populaire onderwerpen
solution: Experience Platform, Intelligent Services
title: Aan de slag in de Attribution AI
topic: Getting started
description: De volgende gidsen vereisen een inzicht in de diverse diensten van Adobe Experience Platform betrokken bij het gebruiken van Attribution AI. Lees de volgende documenten voordat u de zelfstudies start.
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Aan de slag met Attribution AI

De volgende gidsen vereisen een inzicht in de diverse [!DNL Adobe Experience Platform] diensten betrokken bij het gebruiken van Attribution AI. Lees de volgende documenten voordat u de zelfstudies start:

- [XDM-systeemoverzicht](../../xdm/home.md) (Experience Data Model): XDM is het grondkader dat,  [!DNL Adobe Experience Cloud]aangedreven door Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op precies het juiste moment te leveren. De methodologie waarop het Experience Platform wordt gebouwd, het Systeem van XDM, stelt de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform in werking.
- [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Dit document verstrekt een inleiding aan de schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) en de bouwstenen, beginselen, en beste praktijken voor het samenstellen van schema&#39;s die binnen moeten worden gebruikt  [!DNL Adobe Experience Platform].
- [Gebouwenschema&#39;s](../../xdm/tutorials/create-schema-ui.md): Deze zelfstudie behandelt de stappen voor het maken van een schema met de Schema-editor in het Experience Platform.

Attribution AI vereist datasets om met het schema van de Gebeurtenissen van de Ervaring van de Consumenten (CEE) in overeenstemming te zijn, dat een mengeling in [het Model van de Gegevens van de Ervaring ](../../xdm/home.md) (XDM) is. Neem contact op met de ondersteuning van Adobe op attributionai-support@adobe.com om deze gegevens te implementeren of te wijzigen. Als er gegevens over mediaconcentages aanwezig zijn, kunt u verdere analyses uitvoeren, zoals incrementele inkomsten en ROI. Als de gegevens van het klantenprofiel beschikbaar zijn, kunt u kredieten aan het niveau van het klantenprofiel verder toeschrijven.

## Terminologie

- **Conversiegebeurtenis:** elke digitale gebeurtenis of digitale interactie die klanten uitvoeren om een mijlpaal voor een doel aan te geven, zoals conferentieregistraties. Tot de extra voorbeelden behoren betaalde conversies, gratis accountaanmeldingen of het in aanmerking komen voor een doel.

- **Aanraakpunt:** Elke digitale gebeurtenis of digitale interactie die klanten uitvoeren op het pad naar een doel. Voorbeelden hiervan zijn marketingactiviteiten vóór de aankoop, weergave van bekeken advertenties en betaalde zoekopdrachten.

## Attribution AI-scores downloaden

>[!NOTE]
>
>Als u geen onbewerkte scores hoeft te downloaden, kunt u deze stap overslaan en doorgaan naar [volgende stappen](#next-steps).

Het downloaden van de scores van Attribution AI wordt gedaan door een combinatie API vraag. Om vraag aan Platform APIs te maken, moet u [authentificatieleerprogramma](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Zie de [sandbox overzichtsdocumentatie](../../sandboxes/home.md) voor meer informatie over sandboxen in Platform.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md) in de het oplossen van problemengids van de Experience Platform te lezen.

## Volgende stappen {#next-steps}

Zodra u klaar bent en al uw geloofsbrieven en schema&#39;s op zijn plaats hebt, begin door [Attribution AI te volgen gebruikersinterfacegids](./user-guide.md). Deze gids begeleidt u door het creëren van een geval en het voorleggen van het voor opleiding en het scoren.