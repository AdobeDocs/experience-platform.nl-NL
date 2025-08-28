---
title: Aanvullende informatie van augustus 2025 voor Adobe Experience Platform
description: Aanvullende informatie van augustus 2025 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: d2b605925a8fd7ea06f198ba8a9f85747a2e585b
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 82%

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

**Releasedatum: 19 augustus 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [Catalogusservice](#catalog-service)
- [Bestemmingen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Real-Time Customer Profile](#profile)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Waarschuwingen over de capaciteit van streamingdoorvoer | Met drie nieuwe waarschuwingen kunnen gebruikers zich abonneren op waarschuwingen en deze configureren om de prestaties van de streamingdoorvoercapaciteit proactief te beheren en te bewaken. De nieuwe waarschuwingen worden bijvoorbeeld gegeven wanneer de streamingdoorvoer 80% of 90% bereikt of de capaciteitslimieten overschrijdt. Voor meer informatie raadpleegt u de handleiding voor [capaciteitswaarschuwingsregels](../../observability/alerts/rules.md#capacity). |

Raadpleeg het [[!DNL Observability Insights] overzicht](../../observability/home.md) voor meer informatie over meldingen.

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie en herkomst van gegevens binnen Adobe Experience Platform. Alle gegevens die in Experience Platform worden opgenomen, worden in een datalake opgeslagen als bestanden en mappen. De catalogus bevat daarentegen de metagegevens en beschrijvingen van die bestanden en mappen voor opzoek- en controledoeleinden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gegevensbewaring voor Real-Time Customer Profile | U kunt de termijn voor gegevensbewaring voor Real-Time Customer Profile **slechts** één keer per 30 dagen bijwerken. |

Voor meer informatie over de catalogusservice raadpleegt u het [overzicht van de catalogusservice](../../catalog/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

>[!IMPORTANT]
>
>**Extensie voor het exportschema voor datasets**
>
>Als uw organisatie gegevensstromen voor het exporteren van datasets heeft die vóór november 2024 zijn gemaakt, werken deze gegevensstromen vanaf **1 september 2025** niet meer. Als u wilt dat de gegevensstromen ook na 1 september 2025 gegevens blijven exporteren, moet u de schema&#39;s voor elke bestemming waarnaar u datasets exporteert, verlengen door de stappen in [deze handleiding](../../destinations/ui/dataset-expiration-update.md) te volgen.

>[!IMPORTANT]
>
>**Update van de lijst met IP&#39;s van gewenste personen vereist voor API-gebaseerde bestemmingen**
>
>Wegens verbeteringen aan de exportengine voor streamingbestemmingen moeten organisaties die voor API-gebaseerde bestemmingen [lijsten met IP&#39;s van gewenste personen](../../destinations/catalog/streaming/ip-address-allow-list.md) gebruiken, **vóór 15 september 2025** de volgende IP-adressen aan hun lijsten met gewenste personen toevoegen:
>
>**Vereiste IP-adressen:**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**Deze wijziging geldt voor de volgende bestemmingstypen:**
>
>- [Exportbestemmingen voor streamingdoelgroepen](../../destinations/destination-types.md#streaming-destinations) ([Pega CDH Realtime Audience](/help/destinations/catalog/personalization/pega-v2.md), API-gebaseerde integraties met [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) en [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Openbare of privébestemmingen die via [Destination SDK](../../destinations/destination-sdk/getting-started.md) zijn opgebouwd
>
>**Vereiste actie:** Als u met Adobe hebt samengewerkt om IP-adressen voor API-gebaseerde streamingbestemmingen op de lijst met gewenste personen te plaatsen, moet u de bovenstaande IP-adressen aan uw lijst met gewenste personen toevoegen om ononderbroken gegevensstromen naar uw API-gebaseerde bestemmingen te garanderen.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md)-bestemming | Gebruik de [!DNL Acxiom Real ID Audience Connection]-bestemming om uw doelgroepen te verbeteren met [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/)-technologie en doelgroepen activeren op meerdere platforms, zoals [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] en meer. |
| Verbeterd doel [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) | Het verbeterde doel van [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) is een geüpgrade versie van de bestaande [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) -connector. Deze nieuwe connector biedt niet alleen de bestaande publiekssynchronisatiemogelijkheden van de oudere connector, maar zorgt ook voor een betere integratie met [!DNL Marketo Engage] . <br> De [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) schakelaar zal in **Maart 2026** worden afgekeurd. Voor een vloeiende overgang naar het nieuwe **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)** -doel bekijkt u de volgende belangrijke punten en vereiste handelingen: <ul><li>Alle gebruikers van de bestaande **[!UICONTROL (Legacy) (V2) Marketo Engage]** moeten tegen maart 2026 migreren naar de nieuwe **[!UICONTROL Marketo Engage]** -bestemming.</li><li> **Bestaande gegevensstromen zullen niet automatisch worden gemigreerd.** u moet [ opstelling een nieuwe verbinding ](../../destinations/ui/connect-destination.md) aan de nieuwe **[!UICONTROL Marketo Engage]** bestemming en uw publiek daar activeren.</li></ul> |

**Bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| Interne [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md)-upgrade | Vanaf 11 augustus 2025 hebt u gedurende een korte periode twee **[!DNL Microsoft Bing]** kaarten naast elkaar gezien in de lijst met doelen. Dit komt door een interne upgrade van de bestemmingsservice. De naam van de bestaande bestemmingsconnector **[!DNL Microsoft Bing]** is gewijzigd in **[!UICONTROL (Deprecated) Microsoft Bing]** en er is nu een nieuwe kaart met de naam **[!UICONTROL Microsoft Bing]** voor u beschikbaar. <br> De upgrade is voltooid en de verouderde kaart is verwijderd uit de doelcatalogus. Gebruik de **[!UICONTROL Microsoft Bing]** -verbinding in de catalogus voor nieuwe gegevensstromen voor activering. Als u actieve gegevens naar de **[!UICONTROL (Deprecated) Microsoft Bing]** bestemming had, zullen zij automatisch worden bijgewerkt, zodat wordt geen actie van u vereist. <br><br>Als u gegevensstromen maakt via de [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/), moet u uw [!DNL flow spec ID] en [!DNL connection spec ID] bijwerken naar de volgende waarden:<ul><li>Stroomspecificatie-ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Verbindingsspecificatie-ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Na deze upgrade kunt u in uw gegevensstromen naar [!DNL Microsoft Bing] een **daling in het aantal geactiveerde profielen** ervaren. Deze daling wordt veroorzaakt door de introductie van de **ECID-toewijzingsvereiste** voor alle activeringen op dit bestemmingsplatform. |
| De vervaldatum van de authentificatie details voor [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md) en [ LinkedIn Gelijke Publiek ](../../destinations/catalog/social/linkedin-b2b.md) bestemmingen | De vervalinformatie van de authentificatie voor [!DNL LinkedIn] bestemmingen is nu zichtbaar direct in de interface van Experience Platform, zodat kunt u zien wanneer uw authentificatie zal verlopen en het vernieuwen alvorens het om het even welke verstoringen aan uw gegevensstromen veroorzaakt. U kunt de vervaldatums van uw token vanaf de kolom **[!UICONTROL Account expiration date]** controleren op de tabbladen **[[!UICONTROL Accounts]](../../destinations/ui/destinations-workspace.md#accounts)** of **[[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse)** . |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde zoek-, filter- en tagmogelijkheden voor bestemmingen | Verbeter uw workflow voor bestemmingsbeheer met verbeterde zoek-, filter- en tagmogelijkheden op de tabbladen [Verkennen](../../destinations/ui/destinations-workspace.md#browse) en [Accounts](../../destinations/ui/destinations-workspace.md#accounts). <br> U kunt nu naar specifieke gegevensstromen en rekeningen door naam zoeken, filtreren door diverse criteria met inbegrip van bestemmingsplatform, status, en data, en douanetags creëren om uw bestemmingen te organiseren. Kolomsortering is ook beschikbaar voor belangrijke velden, zoals de laatste dataflow-runtime, zodat u de doelverbindingen gemakkelijker kunt identificeren en beheren. <br> ![ Geanimeerde demonstratie van het zoeken naar een bestemmingsdataflow in het Browse lusje ](../../destinations/assets/ui/workspace/search.gif) |


## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Op modellen gebaseerde schema&#39;s | Vereenvoudig uw gegevensmodellering met op modellen gebaseerde schema&#39;s. U kunt nu eenvoudiger schema&#39;s maken met uitgebreide voorbeelden en richtlijnen. Deze functie is momenteel beschikbaar voor Campaign Orchestration-licentiehouders en zal worden uitgebreid naar Data Distiller-klanten bij GA, waardoor gegevensmodellering toegankelijker en efficiënter wordt. |

Voor meer informatie raadpleegt u het [overzicht van XDM](../../xdm/home.md).

## Real-Time Customer Profile {#profile}

Real-Time Customer Profile biedt een uniform, bruikbaar overzicht van elke klant door gegevens uit alle kanalen te consolideren in één profiel.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde zoekfunctionaliteit in de Entities-API | De Entities-API ondersteunt nu het volgende: <ul><li>Persoon (profiel)</li><li>Experience-gebeurtenissen</li><li>Account</li><li>Kans</li></ul> Deze update vereenvoudigt het gebruik van API&#39;s en helpt optimale prestaties en betrouwbaarheid te garanderen. Als u eerder opzoekacties voor andere entiteitstypen hebt gebruikt, zoals samenvoegtabellen en aangepaste multi-entiteitstypen, is dit een goed moment om uw API-gebruik te evalueren en te profiteren van de verbeterde ervaring. Voor meer informatie raadpleegt u de [handleiding voor de Real-Time CDB B2B Edition-architectuurupgrade](../../rtcdp/b2b-architecture-upgrade.md). |

Voor meer informatie over Real-Time Customer Profile raadpleegt u het [profieloverzicht](../../profile/home.md).

## Sandboxes {#sandboxes}

Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Deduplicatie van afhankelijkheidsobjecten in de importworkflow | Sandboxtools gebruiken voortaan altijd, als er objecten met dezelfde naam worden gedetecteerd, die bestaande objecten opnieuw om objectproliferatie te voorkomen. Deze wijziging is van toepassing op de volgende objecten: <ul><li>Schema</li><li>Veldgroepen</li><li>Doelgroep</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Raadpleeg voor meer informatie de [handleiding voor objecten die worden ondersteund voor sandboxtooling](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Volledige sandboxondersteuning voor het delen van pakketten tussen organisaties | Sandboxtools ondersteunen nu bij het delen van pakketten tussen organisaties het type **Gehele sandbox**. U kunt nu pakketten met zowel volledige sandboxen als meerdere objecten tussen organisaties delen. Voor meer informatie raadpleegt u de [handleiding over voorwerpen die voor sandboxgereedschappen](../../sandboxes/ui/sharing-packages-across-orgs.md) worden ondersteund. |

Voor meer informatie over sandboxes, lees het [ overzicht van sandboxes](../../sandboxes/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Doelgroepinschattingen | Doelgroepinschattingen worden binnen Segment Builder nu automatisch gegenereerd. Deze waarde wordt bijgewerkt wanneer u de doelgroep wijzigt en weerspiegelt altijd de nieuwste doelgroepregels. Bovendien wordt de schatting nu weergegeven als een **bereik** dat is gebaseerd op het vertrouwensinterval van de steekproefgegevens. |

Voor meer informatie raadpleegt u het [[!DNL Segmentation Service] overzicht](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative}-ondersteuning voor [!DNL Azure Private Links] in de gebruikersinterface | U kunt [!DNL Azure Private Links] nu gebruiken voor een geselecteerde groep bronnen in de gebruikersinterface. Met deze functie kunt u een privé-eindpunt maken waarmee uw bron verbinding kan maken. Met privé-eindpunten kunt u verbindingen en gegevensstromen instellen die het openbare internet omzeilen. Zo profiteert u van een betere beveiliging en netwerkisolatie voor uw gevoelige gegevens. Ondersteuning voor [!DNL Azure Private Links] is beschikbaar voor de volgende bronnen: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> Voor meer informatie raadpleegt u de handleiding op [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |
| Verbeterde verificatie voor [!DNL Azure Blob Storage] | U kunt nu verificatie op basis van de belangrijkste service gebruiken om uw [!DNL Azure Blob Storage]-bron met Experience Platform te verbinden. U kunt nu verificatie op basis van de belangrijkste service gebruiken voor verbeterde veiligheid, eenvoudigere rotatie van aanmeldingsgegevens en een nauwkeurigere toegangscontrole voor uw account. Voor meer informatie raadpleegt u het [[!DNL Azure Blob Storage] overzicht](../../sources/connectors/cloud-storage/blob.md). |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).