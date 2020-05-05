---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Aan de slag met Kenmerken AI
topic: Getting started
translation-type: tm+mt
source-git-commit: 6161f5a9ca0df341272a96a8a19ce6c34f6d5d3e

---


# Aan de slag met Kenmerken AI

De volgende handleidingen vereisen inzicht in de verschillende services van het Adobe Experience Platform die betrokken zijn bij het gebruik van Attribution AI. Lees de volgende documenten voordat u de zelfstudies start:

- [XDM-systeemoverzicht](../../xdm/home.md)(Experience Data Model): XDM is het basisraamwerk dat Adobe Experience Cloud, aangedreven door Experience Platform, in staat stelt de juiste boodschap af te geven aan de juiste persoon, op het juiste kanaal, op precies het juiste moment. De methodologie waarop het Platform van de Ervaring wordt gebouwd, het Systeem van XDM, exploiteert de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform.
- [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Dit document biedt een inleiding tot de schema&#39;s van het Gegevensmodel van de Ervaring (XDM) en de bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s die in het Platform van de Ervaring van Adobe moeten worden gebruikt.
- [Gebouwenschema&#39;s](../../xdm/tutorials/create-schema-ui.md): Deze zelfstudie behandelt de stappen voor het maken van een schema met behulp van de Schema-editor in het Experience Platform.

Kenmerk AI vereist datasets om met het schema van de Gebeurtenissen van de Ervaring van de Consumenten (CEE) in overeenstemming te zijn, dat een mengeling in het Model [van de Gegevens van de](../../xdm/home.md) Ervaring (XDM) is. Neem contact op met de ondersteuning van Adobe op attributionai-support@adobe.com als u deze gegevens wilt implementeren of wijzigen. Als er gegevens over mediaconcentages aanwezig zijn, kunt u verdere analyses uitvoeren, zoals incrementele inkomsten en ROI. Als de gegevens van het klantenprofiel beschikbaar zijn, kunt u kredieten aan het niveau van het klantenprofiel verder toeschrijven.

## Terminologie

- **Conversiegebeurtenis:** Elke digitale gebeurtenis of digitale interactie die klanten uitvoeren om een mijlpaal in de richting van een doel aan te geven, zoals conferentieregistraties. Tot de extra voorbeelden behoren betaalde conversies, gratis accountaanmeldingen of het in aanmerking komen voor een doel.

- **Aanraakpunt:** Elke digitale gebeurtenis of digitale interactie die klanten uitvoeren op het pad naar een doel. Voorbeelden hiervan zijn marketingactiviteiten vóór de aankoop, weergave van bekeken advertenties en betaalde zoekopdrachten.

## Kenmerken van AI-scores downloaden

>[!NOTE] Als u geen onbewerkte scores wilt downloaden, kunt u deze stap overslaan en doorgaan met de [volgende stappen](#next-steps).

Het downloaden van AI-scores van kenmerk wordt uitgevoerd via een combinatie van API-aanroepen. Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

## Volgende stappen {#next-steps}

Zodra u klaar bent en al uw geloofsbrieven en schema&#39;s op zijn plaats hebt, begin door de gebruikersinterfacegids [van](./user-guide.md)Attributie AI te volgen. Deze gids begeleidt u door het creëren van een geval en het voorleggen van het voor opleiding en het scoren.