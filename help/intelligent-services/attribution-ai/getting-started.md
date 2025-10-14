---
keywords: Experience Platform;aan de slag;attributie ai;populaire onderwerpen
feature: Attribution AI
title: Aan de slag met Kenmerken AI
description: De volgende handleidingen vereisen inzicht in de verschillende Adobe Experience Platform-services die betrokken zijn bij het gebruik van Attribution AI. Lees de volgende documenten voordat u de zelfstudies start.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Aan de slag met Kenmerken AI

De volgende handleidingen vereisen inzicht in de verschillende [!DNL Adobe Experience Platform] -services die betrokken zijn bij het gebruik van Attribution AI. Lees de volgende documenten voordat u de zelfstudies start:

- [&#x200B; het overzicht van het Systeem van Gegevens van de Ervaring Model (XDM) &#x200B;](../../xdm/home.md): XDM is het basiskader dat [!DNL Adobe Experience Cloud], aangedreven door Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op precies het juiste moment te leveren. De methodologie waarop Experience Platform, het Systeem van XDM, wordt gebouwd exploiteert de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van Experience Platform.
- [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../xdm/schema/composition.md): Dit document verstrekt een inleiding aan de schema&#39;s van het Model van Gegevens van de Ervaring (XDM) en de bouwstenen, de principes, en beste praktijken voor het samenstellen van schema&#39;s die in [!DNL Adobe Experience Platform] moeten worden gebruikt.
- [&#x200B; de schema&#39;s van de Bouw &#x200B;](../../xdm/tutorials/create-schema-ui.md): Dit leerprogramma behandelt de stappen voor het creëren van een schema gebruikend de Redacteur van het Schema binnen Experience Platform.

Attributie AI vereist datasets om met het schema van de Gebeurtenissen van de Ervaring van de Consumenten (CEE) in overeenstemming te zijn, dat een [&#x200B; Model van de Gegevens van de Ervaring (XDM) &#x200B;](../../xdm/home.md) schemagebiedgroep is. Neem contact op met de ondersteuning van Adobe op attributionai-support@adobe.com om deze gegevens te implementeren of te wijzigen. Als er gegevens over mediaconcentages aanwezig zijn, kunt u verdere analyses uitvoeren, zoals incrementele inkomsten en ROI. Als de gegevens van het klantenprofiel beschikbaar zijn, kunt u kredieten aan het niveau van het klantenprofiel verder toeschrijven.

## Terminologie

- **gebeurtenis van de Omzetting:** Om het even welke digitale gebeurtenis of digitale interactie die de klanten doen om op een mijlpaal naar een doel, zoals conferentieregistraties te wijzen. Tot de extra voorbeelden behoren betaalde conversies, gratis accountaanmeldingen of het in aanmerking komen voor een doel.

- **Aanraakpunt:** Om het even welke digitale gebeurtenis of digitale interactie die de klanten in de weg naar een doel doen. Voorbeelden hiervan zijn marketingactiviteiten vóór de aankoop, weergave van bekeken advertenties en betaalde zoekopdrachten.

## Kenmerken van AI-scores downloaden

>[!NOTE]
>
>Als u geen ruwe scores moet downloaden, kunt u deze stap overslaan en aan de [&#x200B; volgende stappen &#x200B;](#next-steps) te werk gaan.

Het downloaden van AI-scores van kenmerk wordt uitgevoerd via een combinatie van API-aanroepen. Om vraag aan Experience Platform APIs te maken, moet u het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen aan Experience Platform API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in Experience Platform, zie de [&#x200B; documentatie van het zandbakoverzicht &#x200B;](../../sandboxes/home.md).

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [&#x200B; hoe te om voorbeeld API vraag &#x200B;](../../landing/troubleshooting.md) in de het oplossen van problemengids van Experience Platform te lezen.

## Toegangsbeheer {#access-control}

Wanneer het gebruiken van op rol-gebaseerd toegangsbeheer, verlenen de **Eigenschappen AI van de Attributie van de Mening** en **de voorrechten van AI van de Attributie** toegang tot verschillende functies van Attributie AI. **beheert Attributie AI** laat u **&#x200B;**&#x200B;creëren, **kloon**, **uitgeven**, **schrapping**, **toelaten**, of **onbruikbaar maken** een instantie terwijl **de Attributie AI van de Mening** u **laat lezen of** mening **het.** **creeer**, **geef** uit en **schrap** acties worden geregistreerd door controlelogboeken.

Zie de documentatie om [&#x200B; te leren toewijzend toestemmingen voor toegangscontrole &#x200B;](../../../help/access-control/home.md) of hoe te [&#x200B; controlelogboeken gebruiken om toegang en activiteit &#x200B;](../../../help/landing/governance-privacy-security/audit-logs/overview.md) te controleren.

## Volgende stappen {#next-steps}

Zodra u klaar bent en al uw geloofsbrieven en schema&#39;s op zijn plaats hebt, begin door de [&#x200B; gebruikersinterfacegids van de Attributie AI &#x200B;](./user-guide.md) te volgen. Deze gids begeleidt u door het creëren van een geval en het voorleggen van het voor opleiding en het scoren.
