---
title: Opmerkingen bij de release Experience Platform
description: Een voorvertoning van de meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 491e0881167e3fb383a5a611924bd0d1df07b441
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 43%

---

# Opmerkingen bij de release Adobe Experience Platform

>[!IMPORTANT]
>
>Dit document is voorgenomen als a **voorproef** van de versienota&#39;s voor de huidige maand. Release-items kunnen worden gewijzigd en worden toegevoegd of verwijderd in de definitieve versie.

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/pre-release-notes)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Datum van de Versie: September 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [AI-assistent](#ai-assistant)
- [Waarschuwingen](#alerts)
- [Bestemmingen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Query-service](#query-service)
- [Realtime-klantenprofiel](#profile)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## AI-assistent {#ai-assistant}

Adobe Experience Platform AI Assistant is een conversatie-ervaring die u kunt gebruiken om workflows in Adobe Experience Cloud-toepassingen te versnellen en te optimaliseren.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator is uw intelligente assistent voor Experience Cloud-toepassingen. Wanneer u vragen stelt of hulp vraagt, roept Agent Orchestrator automatisch op gespecialiseerde agenten om u de juiste antwoorden te krijgen. Agent Orchestrator herinnert uw gespreksgeschiedenis, toelatend u om op vorige vragen te bouwen natuurlijk zonder herhalende context, en combineert inzichten van veelvoudige agenten om u met duidelijke, verenigde reacties te presenteren. U kunt gebruikmaken van de Agent Orchestrator-mogelijkheden via de conversatie-interface van AI Assistant. |
| Audience Agent | In de Audience Agent kunt u inzichten weergeven over het publiek, zoals het detecteren van belangrijke wijzigingen in de publieksgrootte, het detecteren van dubbele doelgroepen, het verkennen van uw publieksoverzicht en het ophalen van de grootte van uw publiek. |
| Field Discovery Agent | De agent van de Ontdekking van het Gebied helpt gebruikers automatisch gegevensgebieden binnen hun schema&#39;s en datasets ontdekken en begrijpen. Deze intelligente agent analyseert uw gegevensstructuur en verstrekt inzicht over gebiedsgebruik, verhoudingen, en aanbevelingen voor optimalisering. |

Voor meer informatie, raadpleegt u het [overzicht van de AI-assistent](../ai-assistant/home.md).

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Waarschuwing bij opnemen van streaming profiel | U kunt zich nu abonneren op twee nieuwe waarschuwingen voor het streamen van opname op gegevensstroomniveau: <ul><li>Streaming-insluitingsfout overschreden</li><li>Streaming inscriptie overgeslagen snelheid</li></ul> Waarschuwingen op het platform of in e-mailberichten geven een melding wanneer de drempelwaarden voor de standaarddrempel worden overschreden, of als er een aangepaste drempel wordt opgegeven. Voor meer informatie, lees het [ alarm van het Profiel ](../observability/alerts/rules.md#profile) gids. |

{style="table-layout:auto"}

Raadpleeg het [[!DNL Observability Insights] overzicht](../observability/home.md) voor meer informatie over meldingen.

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [!BADGE &#x200B; Beta &#x200B;]{type=Informative} [!DNL Snowflake Batch] schakelaar | Er is nu een nieuwe [!DNL Snowflake Batch] -connector beschikbaar die een alternatief biedt voor de streamingconnector voor specifieke gebruiksgevallen. |
| [!DNL Adform]-bestemming | [!DNL Adform] is een toonaangevende aanbieder van koop- en verkoopoplossingen voor programmatische media. Als u Adobe verbindt met de Adobe Experience Platform, kunt u uw eerste publiek activeren via Adform, op basis van de Experience Cloud-id (ECID). |
| [!DNL Data Landing Zone] ondersteuning voor codering | U kunt nu openbare sleutels met RSA-indeling koppelen om uw geëxporteerde bestanden te coderen, zodat u over hetzelfde beveiligingsniveau beschikt als andere bestemmingen voor cloudopslag voor uw vertrouwelijke gegevens. |
| Gegevens over vervaldatum van verificatie voor [!DNL Pinterest] doelen | Informatie over de verloopdatum van de verificatie voor [!DNL Pinterest]-bestemmingen is nu rechtstreeks zichtbaar in de Experience Platform-interface. Zo kunt u zien wanneer uw verificatie verloopt en deze vernieuwen voordat er verstoringen in uw gegevensstromen ontstaan. U kunt de vervaldatums van uw tokens controleren in de kolom **[!UICONTROL Account expiration date]** op de tabbladen **[[!UICONTROL Accounts]](../destinations/ui/destinations-workspace.md#accounts)** of **[[!UICONTROL Browse]](../destinations/ui/destinations-workspace.md#browse)** . |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde mogelijkheden voor bestemmingsbeheer in de gebruikersinterface van Experience Platform | Verbeter uw workflow voor bestemmingsbeheer met nieuwe sorteermogelijkheden op de tabbladen [[!UICONTROL Browse]](../destinations/ui/destinations-workspace.md#browse) en [[!UICONTROL Accounts]](../destinations/ui/destinations-workspace.md#accounts) . U kunt nu ook een visuele indicator zien wanneer uw accountverificatie bijna verloopt. |

Voor meer informatie leest u het [overzicht van bestemmingen](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Op modellen gebaseerde schema&#39;s | Vereenvoudig uw gegevensmodellering met op modellen gebaseerde schema&#39;s. U kunt nu eenvoudiger schema&#39;s maken met uitgebreide voorbeelden en richtlijnen. Deze functie is momenteel beschikbaar voor Campaign Orchestration-licentiehouders en zal worden uitgebreid naar Distiller-klanten van Data bij GA, waardoor gegevensmodellering toegankelijker en efficiënter wordt. De functie biedt ondersteuning voor gegevens uit tijdreeksen en mogelijkheden voor het vastleggen van gegevens wijzigen. |

Voor meer informatie raadpleegt u het [overzicht van XDM](../xdm/home.md).

## Real-Time Customer Profile {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met Profile kunt u klantgegevens samenvoegen tot één overzichtelijk overzicht, dat een bruikbaar overzicht met tijdstempel biedt van elke klantinteractie.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen voor profielviewer | In de release van september 2025 zijn de volgende verbeteringen aangebracht in de profielviewer. <ul><li>**Gecombineerde mening**: Attributen, gebeurtenissen, en inzichten zijn gecombineerd in één enkele mening.</li><li>**AI-Gegenereerde inzichten**: De pagina van profieldetails toont nu AI-Gegenereerde inzichten, latend u details die van uw profiel worden geproduceerd. Deze inzichten kunnen informatie omvatten zoals protiliteitsscores en trendanalyse.</li><li>**update van de Stijl**: De pagina van profieldetails is visueel verfrist.</li><li>**doorbladert**: U kunt uw profielen door een interactieve kaart-gebaseerde carrousel met onderzoek en aanpassing nu onderzoeken.</li></ul> |

Voor meer informatie, lees het [ overzicht van het Profiel van de Klant in real time ](../profile/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Accountpubliek met veroudering van ervaringsgebeurtenissen | Na de upgrade van de B2B-architectuur wordt het accountpubliek met ervaringsgebeurtenissen niet meer ondersteund. Gebruik in plaats daarvan het nieuwe segment van de segmentbenadering: maak een publiek Personen met Experience Events en verwijs naar het publiek Personen wanneer u een accountpubliek maakt. Dit biedt een flexibelere en onderhoudsvriendelijkere benadering van het creëren van B2B-publiek. |

**Belangrijke updates**

| Bijwerken | Beschrijving |
| ------- | ----------- |
| Audience schat auto-refresh revert | De auto-verfrissingsverhoging voor publieksramingen is teruggekeerd. De schattingen van het publiek zullen binnen de Bouwer van het Segment verder worden geproduceerd, maar de automatische verfrissingsfunctionaliteit is verwijderd. |

Voor meer informatie raadpleegt u het [[!DNL Segmentation Service] overzicht](../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe bronnen in algemene beschikbaarheid | De volgende bronnen zijn nu beschikbaar in algemene beschikbaarheid: verschillende bronconnectors zijn bijgewerkt van Beta naar GA: <ul><li>[ de Ingestie van Gegevens van Acxiom ](../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[ de Ingestie van Gegevens van het Vooruitzicht van Acxiom ](../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[ Merkury Onderneming ](../sources/connectors/data-partners/merkury.md)</li><li>[ SAP Commerce ](../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. Deze bronnen worden nu volledig ondersteund en zijn klaar voor gebruik bij de productie. |
| [!DNL Snowflake] ondersteuning voor sleutelpaarverificatie | Uitgebreide beveiliging voor Snowflake-verbindingen met ondersteuning voor sleutelpaarverificatie. De basisauthentificatie (gebruikersbenaming/wachtwoord) zal tegen November 2025 worden afgekeurd, zodat worden de klanten aangemoedigd om aan zeer belangrijk-paarauthentificatie voor betere veiligheid te migreren. |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../sources/home.md).