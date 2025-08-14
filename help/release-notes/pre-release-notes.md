---
title: Opmerkingen bij de release Experience Platform
description: Een voorvertoning van de meest recente releaseopmerkingen voor Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: bcf3045fbbf4f9673e954a5ebf95d1225d4cdcd7
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 40%

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

**Datum van de Versie: Augustus 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [Bestemmingen](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Waarschuwing over streamingdoorvoer | Met drie nieuwe waarschuwingen kunnen gebruikers zich abonneren op en waarschuwingen configureren om de prestaties van streaming doorvoercapaciteit proactief te beheren en te bewaken. Nieuwe waarschuwingen zijn onder andere wanneer de streamingdoorvoer 80%, 90% of meer bedraagt dan de capaciteitslimiet. Voor meer informatie, lees de [ gids van de capaciteitsalarm regels ](../observability/alerts/rules.md#capacity). |

Raadpleeg het [[!DNL Observability Insights] overzicht](../observability/home.md) voor meer informatie over meldingen.

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

>[!IMPORTANT]
>
>**de uitvoerprogrammauitbreiding van de Dataset**
>
>Als uw organisatie dataflows van de gegevenssetuitvoer heeft die vóór November 2024 worden gecreeerd, zullen deze dataflows ophouden werkend op **1 September, 2025**. Als u de dataflows nodig hebt om het uitvoeren van gegevens na 1 september, 2025 te houden, moet u hun programma&#39;s voor elke bestemming uitbreiden waarnaar u datasets uitvoert, door de stappen in [ te volgen deze gids ](../destinations/ui/dataset-expiration-update.md).

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [!DNL Acxiom Real ID Audience] doel | Gebruik de [!DNL Acxiom Real ID Audience Connection] bestemming om publiek met [!DNL Acxiom's] [ Echte ID™ ](https://www.acxiom.com/real-id/real-id/) technologie te verbeteren en publiek aan veelvoudige platforms, zoals [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], en meer te activeren. |

**Bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| Gegevens over het verlopen van verificatie voor [!DNL LinkedIn] - en [!DNL Pinterest] -doelen | De vervalgegevens van accounts zijn nu rechtstreeks zichtbaar in de Experience Platform-interface, zodat u kunt zien wanneer de verificatie van [!DNL LinkedIn] en [!DNL Pinterest] verloopt en wordt vernieuwd voordat de gegevensstroom wordt onderbroken. |
| Coderingsondersteuning voor [!DNL Data Landing Zone] -doelen | Bescherm de geëxporteerde gegevens met codering. U kunt nu openbare sleutels met RSA-indeling koppelen om uw geëxporteerde bestanden te coderen, zodat u over hetzelfde beveiligingsniveau beschikt als andere bestemmingen voor cloudopslag voor uw vertrouwelijke gegevens. |
| [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) interne upgrade | Vanaf dinsdag 11 augustus 2025 kunt u twee **[!DNL Microsoft Bing]**-kaarten naast elkaar zien in de bestemmingencatalogus. Dit komt door een interne upgrade van de bestemmingsservice. De naam van de bestaande bestemmingsconnector **[!DNL Microsoft Bing]** is gewijzigd in **[!UICONTROL (Deprecated) Microsoft Bing]** en er is nu een nieuwe kaart met de naam **[!UICONTROL Microsoft Bing]** voor u beschikbaar. Gebruik de nieuwe **[!UICONTROL Microsoft Bing]**-verbinding in de catalogus voor nieuwe activeringsgegevensstromen. Als u actieve gegevensstromen naar de bestemming **[!UICONTROL (Deprecated) Microsoft Bing]** hebt, worden deze automatisch bijgewerkt. U hoeft dus niets te doen. <br><br>Als u gegevensstromen maakt via de [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/), moet u uw [!DNL flow spec ID] en [!DNL connection spec ID] bijwerken naar de volgende waarden:<ul><li>Stroomspecificatie-ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Verbindingsspecificatie-ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Na deze verbetering, kunt u a **daling in het aantal geactiveerde profielen** in uw dataflows [!DNL Microsoft Bing] ervaren. Dit daling wordt veroorzaakt door de introductie van het **ECID afbeeldingsvereiste** voor alle activiteiten aan dit bestemmingsplatform. |
| [!DNL Marketo] consolidatie van doelkaarten | Vereenvoudig uw [!DNL Marketo] doelinstelling met onze geïntegreerde doelkaart. We hebben [!DNL Marketo] V2- en V3-kaarten samengevoegd tot één gestroomlijnde optie, waardoor het eenvoudiger is om de juiste bestemming te kiezen en snel aan de slag te gaan. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde mogelijkheden voor zoeken, filteren en labelen voor doelen | Verbeter uw workflow voor bestemmingsbeheer met verbeterde mogelijkheden voor zoeken, filteren en labelen op de tabbladen Bladeren en Accounts. U kunt nu zoeken naar specifieke gegevensstromen en rekeningen door naam, filter door diverse criteria met inbegrip van bestemmingsplatform, status, en data, en douanetags tot stand brengen om uw bestemmingen te organiseren. Kolomsortering is ook beschikbaar voor belangrijke velden, zoals de laatste dataflow-runtime, zodat u de doelverbindingen gemakkelijker kunt identificeren en beheren. |

Voor meer informatie leest u het [overzicht van bestemmingen](../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Experience Platform worden gebracht. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Op modellen gebaseerde schema&#39;s | Vereenvoudig uw gegevensmodellering met Model-Gebaseerde Schema&#39;s. U kunt schema&#39;s nu gemakkelijker met uitvoerige hoe te voorbeelden en begeleiding tot stand brengen. Deze functie is momenteel beschikbaar voor Campaign Orchestration-licentiehouders en zal worden uitgebreid naar Distiller-klanten van Data bij GA, waardoor gegevensmodellering toegankelijker en efficiënter wordt. |

Voor meer informatie, lees het [ XDM overzicht ](../xdm/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Publiek schattingen | De schattingen van het publiek worden nu automatisch gegenereerd binnen Segment Builder. Deze waarde wordt bijgewerkt wanneer u het publiek wijzigt en weerspiegelt altijd de meest recente publieksregels. |

Voor meer informatie, lees het [[!DNL Segmentation Service]  overzicht ](../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE &#x200B; Beta &#x200B;]{type=Informative} Azure Steun van de Privé Verbinding in UI | Houd uw gegevens veilig met privé netwerkverbindingen. U kunt nu persoonlijke eindpunten maken en gegevensstromen instellen die het openbare internet omzeilen, waardoor u betere beveiliging en netwerkisolatie krijgt voor uw vertrouwelijke gegevens. |
| [!DNL Marketo] updates van brondocumentatie | Volledige zichtbaarheid in de manier waarop uw [!DNL Marketo] -gegevens worden getransformeerd wanneer deze in Experience Platform worden ingevoerd. Alle veldtoewijzingen bevatten nu gedetailleerde uitleg van gegevenstransformaties, zodat u precies kunt zien hoe de `PersonID` wordt `leadID` en `eventType` wordt `activityType` . |
| Ondersteuning voor service principal-verificatie voor [!DNL Azure Blob Storage] | U kunt uw [!DNL Azure Blob Storage] -account nu verbinden met Experience Platform met de belangrijkste verificatie van de service. |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../sources/home.md).

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
