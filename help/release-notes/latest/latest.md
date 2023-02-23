---
title: Aanvullende informatie over Adobe Experience Platform
description: In de release van februari 2023 staat Adobe Experience Platform vermeld.
source-git-commit: ff276de35ca2aaeec168f4c4386d849f3352ad57
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 22 februari 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Query-service](#query-service)
- [Gerelateerde accounts in Real-Time CDP B2B Edition](#related-accounts)
- [Bronnen](#sources)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functies** {#destinations-new-updated-features}

| Functie | Beschrijving |
| ----------- | ----------- |
| [Verbetering van beleid voor goedkeuring](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) voor integratie met [bestandsgebaseerde (batch) doelen](/help/destinations/destination-types.md#file-based) | <p> Wanneer de profielen niet meer voor een toestemmingsbeleid gekwalificeerd zijn, deelt Experience Platform nu proactief hun beleidsuitgang aan op dossier-gebaseerde bestemmingen mee. Dit volgt op [release in februari 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) van dezelfde functionaliteit voor streamingdoelen. </p> <p> <b>Opmerking</b>: Deze functionaliteit is alleen beschikbaar voor klanten van **[!UICONTROL Privacy and Security Shield]** en de **[!UICONTROL Healthcare Shield]**. </p> |

{style=&quot;table-layout:auto&quot;}

**Nieuwe of bijgewerkte documentatie** {#destinations-new-updated-documentation}

| Documentatie | Beschrijving |
| ----------- | ----------- |
| Hoe werken de bestemmingen documentatie | <p>We hebben drie nieuwe artikelen gepubliceerd waarin wordt uitgelegd hoe bestemmingen werken, op basis van gemeenschappelijke vragen van gebruikers:</p> <p><ul><li>[Configureerbare en algemene exportinstellingen in doelen](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Profielexportgedrag voor verschillende doeltypen](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Identiteitsverwerking in de workflow voor doelactivering](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte functies**
&#x200B; | Functie | Beschrijving | | — | — | | Veldverval via de gebruikersinterface | U kunt nu velden uit uw schema&#39;s verwijderen nadat u gegevens hebt ingevoerd. Met XDM-veldafleiding kunt u velden verwijderen uit de UI-weergave en deze voor gebruik behouden. Indien nodig kunt u afgekeurde velden opnieuw tonen en worden alle segmenten, query&#39;s of downstreamoplossingen die verwijzen naar de velden, op de gebruikelijke wijze uitgevoerd. |

&#x200B; Voor meer informatie over XDM in Platform leest u de [XDM System, overzicht](../../xdm/home.md). &#x200B;
<!-- Field deprecation: https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/field-deprecation.html -->

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL Data Lake]. U kunt zich bij om het even welke datasets van gegevens aansluiten meer en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte functies**
&#x200B; | Functie | Beschrijving | | — | — | | Gegevenssets inschakelen voor profiel met SQL | ETIKETTEN van het gebruik in vragen CTAS om een dataset &quot;toegelaten profiel&quot;te maken, of gebruik ALTER om bestaande datasets bij te werken om voor profiel worden toegelaten. | | Geplande query&#39;s controleren | Gebruik het Geplande lusje van Vragen om belangrijke informatie over uw vraaglooppas te vinden en aan alarm in te schrijven. De vragen van de monitor voor planningsdetails, status, en foutenmeldingen/codes zouden moeten ontbreken.  | | Automatisch aanvullen in-/uitschakelen | Verwijder bepaalde metagegevensopdrachten en verbeter de verwerkingstijd door de functie voor automatisch aanvullen in of uit te schakelen in de Query Editor. Deze functie stelt automatisch potentiële SQL sleutelwoorden en lijstdetails voor de vraag voor aangezien u het schrijft. | | Gegevensverzameling | Geef een bemonsteringsfrequentie op in uw query en gebruik gegevenssetvoorbeelden om een uniforme willekeurige steekproef te maken, of maak voorwaardelijke voorbeelden op basis van specifieke criteria. |

&#x200B; Raadpleeg voor meer informatie over Query Services de [Overzicht van Query Service](../../query-service/home.md). &#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Gerelateerde accounts in Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>De functie Verwante accounts is alleen beschikbaar voor klanten van de Real-Time CDP B2B Edition.

Verwante rekeningen [!DNL Real-Time CDP B2B] Hiermee kunt u een lijst weergeven met accounts die lijken op de account waarin u bladert. U kunt de verwante rekeningen in uw segmentdefinities omvatten om uw bereik uit te breiden of bredere criteria in uw segmenten toe te passen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gerelateerde accountservice inschakelen | Met de nieuwe schakelfunctie kunt u de verwante accountservice op uw account inschakelen. Lees voor meer informatie de handleiding op [inschakelen van de gerelateerde accountantsdienst](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Meer informatie over de functies van verwante accounts vindt u op de volgende documentatiepagina&#39;s:

- [Gerelateerde accounts in Real-Time CDP B2B Edition overzicht](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Het tabblad Verwante accounts in de gebruikersinterface voor het accountprofiel](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Hoe verwant rekeningen in segmentdefinities gebruiken](../../rtcdp/segmentation/b2b.md#related-accounts)

Lees voor meer informatie over de Real-Time CDP B2B Edition de [Overzicht van Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Wijs toegang op abonnementsniveau aan met [!DNL Google PubSub] | U kunt toegang tot een specifiek onderwerpabonnement nu bepalen wanneer het gebruiken van [!DNL Google PubSub] bron door de abonnement-id op te geven wanneer u de verificatie uitvoert. Lees voor meer informatie de [!DNL Google PubSub] verificatiezelfstudie [de Flow Service API gebruiken](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) of [UI Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Aangepaste activiteitsgegevens verzamelen van [!DNL Marketo] | U kunt nu aangepaste activiteitsgegevens van uw [!DNL Marketo] -instantie naar Experience Platform. Om de gegevens van de douaneactiviteit in te voeren, moet u de groepen van het gebied van douaneactiviteiten in het B2B schema van Activiteiten opzetten en een dataflow creëren gebruikend de activiteitendataset. Zodra dataflow volledig is, zal de ingesloten dataset zowel standaard als douaneactiviteiten van uw bevatten [!DNL Marketo] -instantie. U kunt vervolgens [Query-service](../../query-service/home.md) voor toegang tot uw aangepaste activiteitenrecords op het Platform. Lees voor meer informatie de handleiding op [een gegevensstroom maken voor aangepaste activiteitsgegevens](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Niet-geclaimde accounts uitsluiten van [!DNL Marketo] | U kunt nu configureren of u niet-geclaimde accounts wilt uitsluiten of opnemen in de opname wanneer u een gegevensstroom voor bedrijfsgegevens maakt. Lees voor meer informatie de handleiding op [een bronverbinding en gegevensstroom maken voor [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
