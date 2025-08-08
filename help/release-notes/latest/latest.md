---
title: Aanvullende informatie van juli 2025 voor Adobe Experience Platform
description: Aanvullende informatie van juli 2025 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 90%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/pre-release-notes)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: woensdag 29 juli 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Capaciteit](#capacity)
- [Bestemmingen](#destinations)
- [Data-opname](#data-ingestion)
- [Real-Time CDP B2B Edition](#b2b)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)


## Capaciteit {#capacity}

>[!AVAILABILITY]
>
>De beschikbaarheid van deze functie is afhankelijk van uw regio. Voor gebruikers in Amerika is de functie beschikbaar vanaf 11 augustus. Voor gebruikers in Europa is de functie beschikbaar vanaf 25 augustus. Voor gebruikers in Azië is de functie beschikbaar vanaf 8 september.

Capaciteit biedt een uitgebreide weergave van de [guardrails](../../rtcdp/guardrails/overview.md) van uw organisatie en geeft aanbevelingen om potentiële capaciteitsschendingen op te lossen door uw capaciteiten toe te wijzen op sandboxniveau. Met deze release kunt u uw capaciteit voor zowel streamingopname als streamingsegmentatie bekijken.

Voor meer informatie, te lezen gelieve het [ overzicht van de Capaciteit ](../../landing/license-usage-and-guardrails/capacity.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| Beperkte beschikbaarheid van de verbinding [Google Customer Match + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) | Nadat deze in juni kort beschikbaar was voor alle klanten, heeft Adobe de integratie teruggezet naar beperkte beschikbaarheid. Momenteel is de toegang tot deze bestemming beperkt tot klanten voor wie deze al was ingeschakeld, terwijl Adobe en Google werken aan het oplossen van implementatieproblemen. Als u geïnteresseerd bent in deze integratie wanneer de bredere uitrol wordt hervat, kunt u contact opnemen met de Adobe-vertegenwoordiger om uw interesse kenbaar te maken. |
| [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) interne upgrade | Vanaf vrijdag 31 juli 2025 kunt u twee [!DNL The Trade Desk]-kaarten naast elkaar zien in de bestemmingencatalogus. Dit komt door een interne upgrade van de bestemmingsservice. <br><br> De bestaande [!DNL The Trade Desk] bestemmingsschakelaar is anders genoemd aan **[!UICONTROL (Deprecated) The Trade Desk]** en een nieuwe kaart met de naam **[!UICONTROL The Trade Desk]** is nu beschikbaar. Gebruik de nieuwe **[!UICONTROL The Trade Desk]** -verbinding in de catalogus voor nieuwe gegevensstromen voor activering. <br><br> als u om het even welke actieve dataflows aan de **[!UICONTROL (Deprecated) The Trade Desk]** bestemming hebt, zullen zij automatisch worden bijgewerkt, zodat wordt geen actie vereist van u. <br><br> als u dataflows door de [ Dienst API van de Stroom ](https://developer.adobe.com/experience-platform-apis/references/destinations/) creeert, moet u uw [!DNL flow spec ID] en [!DNL connection spec ID] aan de volgende waarden bijwerken:<ul><li>Stroomspecificatie-ID: `86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>Verbindingsspecificatie-ID: `1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Accountnamen en beschrijvingen voor bestemmingsverbindingen | U kunt [accountnamen en beschrijvingen ](/help/destinations/ui/connect-destination.md) nu toevoegen bij het verbinden met bestemmingen, waardoor bestemmingen met meerdere accounts beter beheerd kunnen worden. |
| Verbeterde gegevensstroominformatie voor Edge-bestemmingen | De informatie in de rechterrail voor [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md)- en [Custom Personalization](/help/destinations/catalog/personalization/custom-personalization.md)-bestemmingen is verbeterd zodat de naam van de gegevensstroom wordt weergegeven. Dit biedt een duidelijker inzicht in de bijbehorende gegevensstroomconfiguraties en helpt verwarring te verminderen bij het herzien van bestaande gegevensstromen. De **[!UICONTROL Datastream ID]**-kiezer in het configuratiescherm voor de bestemming is bijgewerkt naar **[!UICONTROL Datastream]** voor meer duidelijkheid in de gebruikersinterface. |
| Zichtbaarheid van marketingacties in bestemmingsselectie | Marketingacties worden nu weergegeven in de rechterrail van het tabblad **[[!UICONTROL Browse]](/help/destinations/ui/destinations-workspace.md#browse)** in de werkruimte Bestemmingen en op de pagina **[[!UICONTROL Dataflow runs]](/help/dataflows/ui/monitor-destinations.md)**, waardoor wijzigingen in marketingacties direct zichtbaar zijn zonder dat u naar de weergavepagina hoeft te navigeren. Deze aanpassing verbetert de gebruikerservaring door het eenvoudiger te maken om marketingactieconfiguraties te controleren tijdens het instellen van bestemmingen. |
| [!BADGE Beperkte bèta]{type=Informative} Marketingacties voor bestemmingen bewerken | U kunt [ marketing acties ](/help/destinations/ui/edit-activation.md#edit-marketing-actions) voor bestaande bestemmingen nu uitgeven. Deze functie is momenteel in beperkte bèta. Neem contact op met uw Adobe-vertegenwoordiger om toegang aan te vragen. |
| [!BADGE Beperkte bèta]{type=Informative} Bestemmingen bewerken | U kunt [ uw bestemmingsconfiguratie ](/help/destinations/ui/edit-destination.md) nu uitgeven nadat het is gecreeerd. Deze functie is momenteel in beperkte bèta. Neem contact op met uw Adobe-vertegenwoordiger om toegang aan te vragen. |

**Oplossingen**

| Probleem | Beschrijving |
| --- | --- |
| Scrolfunctionaliteit in categorieën | Er is een probleem opgelost waarbij het zijmenu met categorieën in de catalogus met bestemmingen en bronnen niet goed scrolde bij muisbewegingen. Hierdoor is de navigatie voor gebruikers die door bestemmingscategorieën bladeren, beter bruikbaar. |

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Data-opname {#ingestion}

Experience Platform biedt een uitgebreid raamwerk voor gegevensinvoer dat zowel batch- als streaming-data-opname uit verschillende bronnen ondersteunt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor het monitoren van de opname van streamingprofielen | Real-time monitoring voor streamingprofielopname is nu beschikbaar en biedt transparantie in doorvoer, latentie en gegevenskwaliteit. Dit ondersteunt proactieve waarschuwingen en bruikbare inzichten om data-engineers te helpen bij het identificeren van capaciteitsschendingen en problemen met de opname. Lees de gids over [opname van streamingprofielen bewaken](../../dataflows/ui/monitor-streaming-profile.md) voor meer informatie. |

Lees voor meer informatie het [overzicht van data-opname](../../ingestion/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B Edition biedt uitgebreide mogelijkheden voor het beheer van B2B-klantgegevens, waarmee organisaties uniforme klantprofielen kunnen opbouwen, geavanceerde B2B-groepen kunnen maken en gegevens kunnen activeren via verschillende marketingkanalen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| B2B-architectuurupgrade | Experience Platform wordt geüpgraded naar een nieuwe B2B-architectuur die aanzienlijke verbeteringen introduceert voor doelgroepen met meerdere entiteiten met B2B-kenmerken. Deze upgrade consolideert ondersteuning voor samenvoegbeleid, verbetert de nauwkeurigheid van publiekstellingen en verbetert de mogelijkheden voor het oplossen van entiteiten. Lees het [upgrade-overzicht van Real-Time CDP B2B Edition-architectuur](../../rtcdp/b2b-architecture-upgrade.md) voor een uitgebreid overzicht van de wijzigingen. |
| Consolidatie van samenvoegbeleid voor meerdere entiteiten | Doelgroepen met meerdere entiteiten en B2B-attributen ondersteunen nu slechts één samenvoegbeleid - het standaard samenvoegbeleid - in plaats van meerdere samenvoegbeleidsregels. Deze wijziging zorgt voor een consistente samenstelling van de doelgroep en vereenvoudigt het beheer van de samenvoeglogica. Voor meer informatie raadpleegt u het [Samenvoegbeleidsoverzicht](../../profile/merge-policies/overview.md). |
| Verbeterde doelgroepcijfers voor B2B-entiteiten | Schattingen van de grootte van doelgroepen voor B2B-entiteiten zoals Accounts en mogelijkheden zijn nu exact, gebaseerd op realtime segmentatieresultaten. Deze verbetering zorgt voor nauwkeurigere en betrouwbaardere schattingen voor doelgroepen met complexe B2B-relaties. |
| Account-momentopnamen voor doelgroeplidmaatschap | Doelgroep-lidmaatschapsgegevens worden nu opgenomen voor Account-entiteiten in momentopname-exports, waardoor toegang mogelijk is tot doelgroepstatus, tijdstempels en lidmaatschapsindicatoren op accountniveau. Dit zorgt voor functiepariteit tussen Profiel- (persoon) en Accountsegmentatiemodellen. |
| Wijzigingen in de Sandbox-tools voor gebruikers met meerdere entiteiten | Het importeren van doelgroepen met meerdere entiteiten met B2B-entiteiten en Experience-gebeurtenissen die vóór de migratie zijn geëxporteerd, wordt niet langer ondersteund. Deze doelgroepen zullen de importvalidatie niet doorstaan en kunnen niet automatisch worden geconverteerd naar de nieuwe architectuur. Doelgroepen moeten na de migratie opnieuw worden geëxporteerd voordat ze in doel-sandboxes worden geïmporteerd. Raadpleeg voor meer informatie de [gids over objecten die worden ondersteund voor sandboxtooling](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| B2B-entiteit API-afwaarderingen | [!DNL Profile Access] API-look-up-bewerkingen voor B2B-entiteiten (Account-Person Relation, Opportunity Person-Relation, Campaign, Campaign Member, Marketing List en Marketing List Members) zijn nu afgeschaft. Bovendien zijn [!DNL Profile Access] API-verwijderingshandelingen voor B2B-entiteiten (Account, Account-Person Relation, Opportunity, Opportunity Person-Relation, Campaign, Campaign Member, Marketing List, en Marketing List Members) ook niet meer nodig. Voor meer informatie, raadpleegt u de [gids over eindpunt-API voor entiteiten](../../profile/api/entities.md). |
| Updates van Identity-naamruimte voor entiteitsoplossing | Account- en Opportunity-entiteiten maken nu gebruik van samenvoegen op basis van tijdvoorrang met specifieke Identity-naamruimten (`b2b_account` voor Account, `b2b_opportunity` voor Opportunity). Alle andere entiteiten zijn verenigd met primaire identiteitsoverlappingen die worden samengevoegd op basis van tijdvoorrang. Voor meer informatie over entiteitresolutie raadpleegt u de [handleiding over eindpunt-API van entiteiten](../../profile/api/entities.md). |

Voor meer informatie raadpleegt u het [overzicht van Real-Time CDP B2B Edition](../../rtcdp/b2b-overview.md).

## Sandboxes {#sandboxes}

Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Wijzigingen in de import van doelgroepen met meerdere entiteiten | Sandboxtooling is bijgewerkt om de nieuwe B2B-architectuurverbetering te ondersteunen. Doelgroepen met meerdere entiteiten die B2B-entiteiten en Experience Events bevatten, moeten na de architectuurupgrade opnieuw worden geëxporteerd voordat ze via sandboxgereedschappen in doelsandboxen kunnen worden geïmporteerd. De validatie van het importeren van pre-upgradeversies zal mislukken. Voor meer informatie raadpleegt u de [handleiding over voorwerpen die voor sandboxgereedschappen](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) worden ondersteund. |

Voor meer informatie over sandboxes, lees het [ overzicht van sandboxes](../../sandboxes/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Externe doelgroep-API | Met de Externe doelgroep-API kunt u extern gegenereerde soorten doelgroepen programmatisch importeren in Adobe Experience Platform. Voor meer informatie raadpleegt u de [handleiding voor externe doelgroepeindpunten](../../segmentation/api/external-audiences.md). |

Voor meer informatie over segmentatie raadpleegt u het [Overzicht van de segmentatieservice](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe bronnen**

| Bron | Beschrijving |
| --- | --- |
| [!BADGE &#x200B; Beta &#x200B;]{type=Informative} Steun voor [!DNL Didomi] (het stromen SDK) | Gebruik de [!DNL Didomi]-bron om gegevens over toestemming en voorkeurenbeheer toe te voegen uit [!DNL Didomi], ter ondersteuning van de naleving van privacyregels en op toestemming gebaseerde marketingstrategieën. Raadpleeg het [[!DNL Didomi] bronoverzicht](../../sources/connectors/consent-and-preferences/didomi.md) voor informatie over hoe u aan de slag kunt gaan. Raadpleeg de [[!DNL Didomi] handleiding bronverbinding](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md) voor stappen over het maken van een bronverbinding. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het vastleggen van wijzigingsgegevens in bepaalde bronnen met de [!DNL Flow Service]-API | U kunt nu dataflows maken die het vastleggen van wijzigingsgegevens mogelijk maken voor incrementele invoer met behulp van bronconnectoren. Deze mogelijkheid stelt klanten in staat om gegevenstype te wijzigen voor incrementele opname, waardoor de versheid van gegevens wordt verbeterd en de verwerkingsoverhead wordt verminderd. Lees voor meer informatie de documentatie over het [vastleggen van wijzigingsgegevens gebruiken voor bronnen](../../sources/tutorials/api/change-data-capture.md) |
| Ondersteuning voor zachte verwijdering van records in [!DNL Salesforce] | De [!DNL Salesforce] -bron ondersteunt nu het opnemen van schermverwijderde records via een optionele `includeDeletedObjects` -parameter. Wanneer deze waarde is ingesteld op true, kunnen klanten geneste verwijderde records opnemen in hun [!DNL Salesforce] query&#39;s en deze records naar Experience Platform overbrengen. Lees de [[!DNL Salesforce]  brondocumentatie ](../../sources/connectors/crm/salesforce.md) voor meer informatie. |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).
