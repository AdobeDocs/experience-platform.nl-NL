---
keywords: Experience Platform;aan de slag;attributie ai;populaire onderwerpen
feature: Attribution AI
title: Aan de slag in de Attribution AI
description: De volgende gidsen vereisen een inzicht in de diverse diensten van Adobe Experience Platform betrokken bij het gebruiken van Attribution AI. Lees de volgende documenten voordat u de zelfstudies start.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# Aan de slag met Attribution AI

De volgende handleidingen vereisen inzicht in de verschillende [!DNL Adobe Experience Platform] -services die bij het gebruik van Attribution AI worden gebruikt. Lees de volgende documenten voordat u de zelfstudies start:

- [ het overzicht van het Systeem van Gegevens van de Ervaring Model (XDM) ](../../xdm/home.md): XDM is het basiskader dat [!DNL Adobe Experience Cloud], aangedreven door Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op precies het juiste moment te leveren. De methodologie waarop het Experience Platform wordt gebouwd, het Systeem van XDM, stelt de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform in werking.
- [ Grondbeginselen van schemacompositie ](../../xdm/schema/composition.md): Dit document verstrekt een inleiding aan de schema&#39;s van het Model van Gegevens van de Ervaring (XDM) en de bouwstenen, de principes, en beste praktijken voor het samenstellen van schema&#39;s die in [!DNL Adobe Experience Platform] moeten worden gebruikt.
- [ de schema&#39;s van de Bouw ](../../xdm/tutorials/create-schema-ui.md): Dit leerprogramma behandelt de stappen voor het creëren van een schema gebruikend de Redacteur van het Schema binnen Experience Platform.

Attribution AI vereist datasets om met het schema van de Gebeurtenissen van de Ervaring van de consument (CEE) in overeenstemming te zijn, dat een [ Model van de Gegevens van de Ervaring (XDM) ](../../xdm/home.md) schemagebiedgroep is. Neem contact op met de ondersteuning van de Adobe op attributionai-support@adobe.com als u deze gegevens wilt implementeren of wijzigen. Als er gegevens over mediaconcentages aanwezig zijn, kunt u verdere analyses uitvoeren, zoals incrementele inkomsten en ROI. Als de gegevens van het klantenprofiel beschikbaar zijn, kunt u kredieten aan het niveau van het klantenprofiel verder toeschrijven.

## Terminologie

- **gebeurtenis van de Omzetting:** Om het even welke digitale gebeurtenis of digitale interactie die de klanten doen om op een mijlpaal naar een doel, zoals conferentieregistraties te wijzen. Tot de extra voorbeelden behoren betaalde conversies, gratis accountaanmeldingen of het in aanmerking komen voor een doel.

- **Aanraakpunt:** Om het even welke digitale gebeurtenis of digitale interactie die de klanten in de weg naar een doel doen. Voorbeelden hiervan zijn marketingactiviteiten vóór de aankoop, weergave van bekeken advertenties en betaalde zoekopdrachten.

## Attribution AI-scores downloaden

>[!NOTE]
>
>Als u geen ruwe scores moet downloaden, kunt u deze stap overslaan en aan de [ volgende stappen ](#next-steps) te werk gaan.

Het downloaden van de scores van Attribution AI wordt gedaan door een combinatie API vraag. Om vraag aan Platform APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in Platform, zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md) in de het oplossen van problemengids van het Experience Platform te lezen.

## Toegangsbeheer {#access-control}

Wanneer het gebruiken van op rol-gebaseerd toegangsbeheer, de **Attribution AI van de Mening** en **leiden Attribution AI** voorrechten verlenen toegang tot verschillende functies van Attribution AI. **beheert Attribution AI** laat u **** creëren, **kloon**, **uitgeven**, **schrapping**, **toelaten**, of **onbruikbaar maken** een instantie terwijl **Attribution AI van de Mening** u **of** laat lezen 8} mening **het.** **creeer**, **geef** uit en **schrap** acties worden geregistreerd door controlelogboeken.

Zie de documentatie om [ te leren toewijzend toestemmingen voor toegangscontrole ](../../../help/access-control/home.md) of hoe te [ controlelogboeken gebruiken om toegang en activiteit ](../../../help/landing/governance-privacy-security/audit-logs/overview.md) te controleren.

## Volgende stappen {#next-steps}

Zodra u klaar bent en al uw geloofsbrieven en schema&#39;s op zijn plaats hebt, begin door de [ gids van het gebruikersinterface van de Attribution AI te volgen ](./user-guide.md). Deze gids begeleidt u door het creëren van een geval en het voorleggen van het voor opleiding en het scoren.
