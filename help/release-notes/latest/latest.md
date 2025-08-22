---
title: Aanvullende informatie van augustus 2025 voor Adobe Experience Platform
description: Aanvullende informatie van augustus 2025 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: cb32846bcbd917f267cba587b60dc323f6bc7d96
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 38%

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

**Releasedatum: woensdag 19 augustus 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [Catalogusservice](#catalog-service)
- [Bestemmingen](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Realtime-klantenprofiel](#profile)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Waarschuwing over streamingdoorvoer | Met drie nieuwe waarschuwingen kunnen gebruikers zich abonneren op en waarschuwingen configureren om de prestaties van streaming doorvoercapaciteit proactief te beheren en te bewaken. Nieuwe waarschuwingen zijn onder andere wanneer de streamingdoorvoer 80%, 90% of meer bedraagt dan de capaciteitslimiet. Voor meer informatie, lees de [ gids van de capaciteitsalarm regels ](../../observability/alerts/rules.md#capacity). |

Raadpleeg het [[!DNL Observability Insights] overzicht](../../observability/home.md) voor meer informatie over meldingen.

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie en herkomst van gegevens binnen Adobe Experience Platform. Alle gegevens die in Experience Platform worden opgenomen, worden in een datalake opgeslagen als bestanden en mappen. De catalogus bevat daarentegen de metagegevens en beschrijvingen van die bestanden en mappen voor opzoek- en controledoeleinden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bewaren van gegevens voor realtime klantprofiel | U kunt **slechts** de periode van het gegevensbehoud voor het Profiel van de Klant in real time eens om de 30 dagen bijwerken. |

Voor meer informatie over de Dienst van de Catalogus, lees het [ overzicht van de Dienst van de Catalogus ](../../catalog/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

>[!IMPORTANT]
>
>**de uitvoerprogrammauitbreiding van de Dataset**
>
>Als uw organisatie dataflows van de gegevenssetuitvoer heeft die vóór November 2024 worden gecreeerd, zullen deze dataflows ophouden werkend op **1 September, 2025**. Als u de dataflows nodig hebt om het uitvoeren van gegevens na 1 september, 2025 te houden, moet u hun programma&#39;s voor elke bestemming uitbreiden waarnaar u datasets uitvoert, door de stappen in [ te volgen deze gids ](../../destinations/ui/dataset-expiration-update.md).

>[!IMPORTANT]
>
>{de update van de lijst van gewenste personen van 0} IP die voor op API-Gebaseerde bestemmingen wordt vereist **&#x200B;**
>
>Wegens verbeteringen aan de het stromen motor van de bestemmingenuitvoer, moeten de organisaties die [ IP gebruiken lijsten van gewenste personen ](../../destinations/catalog/streaming/ip-address-allow-list.md) voor op API-Gebaseerde bestemmingen de volgende IP adressen aan hun lijsten van gewenste personen **vóór 15 September, 2025** toevoegen:
>
>**Vereiste IP adressen:**
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
>**Deze verandering is op de volgende bestemmingstypes van toepassing:**
>
>- [ het stromen publiek exporteert bestemmingen ](../../destinations/destination-types.md#streaming-destinations) ([ PegCDH Realtime Publiek ](/help/destinations/catalog/personalization/pega-v2.md), op API-Gebaseerde integratie met [ Salesforce Marketing Cloud ](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) en [ Oracle Eloqua ](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Openbare of privé bestemmingen die door [ Destination SDK ](../../destinations/destination-sdk/getting-started.md) worden gebouwd
>
>**vereiste Actie:** als u met Adobe hebt gewerkt om het even welke IP adressen aan op API-Gebaseerde het stromen bestemmingen te lijsten van gewenste personen, moet u de IP adressen hierboven aan uw lijst van gewenste personen toevoegen om ononderbroken dataflows aan uw op API-Gebaseerde bestemmingen te verzekeren.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) doel | Gebruik de [!DNL Acxiom Real ID Audience Connection] bestemming om publiek met [!DNL Acxiom's] [ Echte identiteitskaart ](https://www.acxiom.com/real-id/real-id/) technologie te verbeteren en publiek aan veelvoudige platforms, zoals [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], en meer te activeren. |

**Bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) interne upgrade | Vanaf 11 augustus 2025 hebt u gedurende een korte periode twee **[!DNL Microsoft Bing]** kaarten naast elkaar gezien in de lijst met doelen. Dit komt door een interne upgrade van de bestemmingsservice. De naam van de bestaande bestemmingsconnector **[!DNL Microsoft Bing]** is gewijzigd in **[!UICONTROL (Deprecated) Microsoft Bing]** en er is nu een nieuwe kaart met de naam **[!UICONTROL Microsoft Bing]** voor u beschikbaar. <br> De upgrade is voltooid en de verouderde kaart is verwijderd uit de doelcatalogus. Gebruik de **[!UICONTROL Microsoft Bing]** -verbinding in de catalogus voor nieuwe gegevensstromen voor activering. Als u actieve gegevens naar de **[!UICONTROL (Deprecated) Microsoft Bing]** bestemming had, zullen zij automatisch worden bijgewerkt, zodat wordt geen actie van u vereist. <br><br>Als u gegevensstromen maakt via de [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/), moet u uw [!DNL flow spec ID] en [!DNL connection spec ID] bijwerken naar de volgende waarden:<ul><li>Stroomspecificatie-ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Verbindingsspecificatie-ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Na deze verbetering, kunt u a **daling in het aantal geactiveerde profielen** in uw dataflows [!DNL Microsoft Bing] ervaren. Dit daling wordt veroorzaakt door de introductie van het **ECID afbeeldingsvereiste** voor alle activiteiten aan dit bestemmingsplatform. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde mogelijkheden voor zoeken, filteren en labelen voor doelen | Verbeter uw werkschema van het bestemmingsbeheer met verbeterd onderzoek, het filtreren, en het etiketteren mogelijkheden over [ doorbladeren ](../../destinations/ui/destinations-workspace.md#browse) en [ Rekeningen ](../../destinations/ui/destinations-workspace.md#accounts) lusjes. <br> U kunt nu naar specifieke gegevensstromen en rekeningen door naam zoeken, filtreren door diverse criteria met inbegrip van bestemmingsplatform, status, en data, en douanetags creëren om uw bestemmingen te organiseren. Kolomsortering is ook beschikbaar voor belangrijke velden, zoals de laatste dataflow-runtime, zodat u de doelverbindingen gemakkelijker kunt identificeren en beheren. <br> ![ Geanimeerde demonstratie van het zoeken naar een bestemmingsdataflow in het Browse lusje ](../../destinations/assets/ui/workspace/search.gif) |


## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Experience Platform worden gebracht. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Op modellen gebaseerde schema&#39;s | Vereenvoudig uw gegevensmodellering met Model-Gebaseerde Schema&#39;s. U kunt schema&#39;s nu gemakkelijker met uitvoerige hoe te voorbeelden en begeleiding tot stand brengen. Deze functie is momenteel beschikbaar voor Campaign Orchestration-licentiehouders en zal worden uitgebreid naar Distiller-klanten van Data bij GA, waardoor gegevensmodellering toegankelijker en efficiënter wordt. |

Voor meer informatie, lees het [ XDM overzicht ](../../xdm/home.md).

## Realtime-klantenprofiel {#profile}

Het profiel van de Klant in real time verstrekt een verenigde, actionable mening van elke klant door gegevens van alle kanalen in één enkel profiel te consolideren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde opzoekfunctionaliteit in de Entiteiten-API | De Entities API ondersteunt nu het volgende: <ul><li>Persoon (profiel)</li><li>Experience Events</li><li>Account</li><li>Opportunity</li></ul> Deze update vereenvoudigt het gebruik van API&#39;s en helpt optimale prestaties en betrouwbaarheid te garanderen. Als u eerder raadplegingen voor andere entiteittypes-met inbegrip van zich aansluit bij lijsten en douane multi-Entiteit types-nu gebruikt is een grote kans om uw API gebruik te herzien en uit de betere ervaring voordeel te halen. Voor meer informatie, leest de [ Real-Time CDB B2B edition architectuurverbeteringsgids ](../../rtcdp/b2b-architecture-upgrade.md). |

Voor meer informatie over het Profiel van de Klant in real time, lees het [ overzicht van het Profiel ](../../profile/home.md).

## Sandboxes {#sandboxes}

Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Dependency object deduplicatie in importworkflow | Sandboxgereedschappen gebruiken nu altijd bestaande objecten opnieuw als objecten met dezelfde naam worden gedetecteerd, om objectproliferatie te voorkomen. Deze wijziging is van toepassing op de volgende objecten: <ul><li>Schema</li><li>Veldgroep</li><li>Doelgroep</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Raadpleeg voor meer informatie de [gids over objecten die worden ondersteund voor sandboxtooling](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Volledige ondersteuning van sandboxen voor delen van orgs-pakketten | Sandbox het tooling steunt nu **Volledige zandbak** type in over org pakket het delen. U kunt nu pakketten met zowel volledige sandboxen als meerdere objecten delen tussen instanties. Voor meer informatie raadpleegt u de [handleiding over voorwerpen die voor sandboxgereedschappen](../../sandboxes/ui/sharing-packages-across-orgs.md) worden ondersteund. |

Voor meer informatie over sandboxes, lees het [ overzicht van sandboxes](../../sandboxes/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Publiek schattingen | De schattingen van het publiek worden nu automatisch gegenereerd binnen Segment Builder. Deze waarde wordt bijgewerkt wanneer u het publiek wijzigt en weerspiegelt altijd de meest recente publieksregels. Bovendien, zal de schatting nu als a **waaier** worden getoond, die op het betrouwbaarheidsinterval van de steekproefgegevens gebaseerd is. |

Voor meer informatie, lees het [[!DNL Segmentation Service]  overzicht ](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE &#x200B; Beta &#x200B;]{type=Informative} Steun voor [!DNL Azure Private Links] in UI | U kunt [!DNL Azure Private Links] nu gebruiken voor een geselecteerde groep bronnen in de gebruikersinterface. Gebruik deze eigenschap om een privé eindpunt tot stand te brengen dat uw bron met kan verbinden. Met privé eindpunten, kunt u opstellingsverbindingen en gegevensstromen die openbaar Internet overslaan, die u verbeterde veiligheid en netwerkisolatie voor uw gevoelige gegevens geven. Ondersteuning voor [!DNL Azure Private Links] is beschikbaar voor de volgende bronnen: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> Lees de handleiding op [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md) voor meer informatie. |
| Verbeterde verificatie voor [!DNL Azure Blob Storage] | U kunt nu op service principal gebaseerde verificatie gebruiken om uw [!DNL Azure Blob Storage] -bron te verbinden met Experience Platform. De dienst belangrijkste gebaseerde authentificatie van het gebruik voor verbeterde veiligheid, gemakkelijkere credentiële omwenteling, en een meer korrelige toegangsbeheer voor uw rekening. Voor meer informatie, lees het [[!DNL Azure Blob Storage]  overzicht ](../../sources/connectors/cloud-storage/blob.md). |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).