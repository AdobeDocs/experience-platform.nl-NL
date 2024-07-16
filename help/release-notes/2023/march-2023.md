---
title: Opmerkingen bij de release van Adobe Experience Platform, maart 2023
description: Aanvullende informatie van maart 2023 voor Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 29 maart 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Gegevensverzameling](#data-collection)
- [Gegevensvoorbereiding](#data-prep)
- [Doelen](#destinations)
- [Experience Data Model](#xdm)
- [Query-service](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte eigenschappen** {#dashboards-new-updated-features}

| Functie | Beschrijving |
| --- | --- |
| Door gebruiker gedefinieerde dashboards | U kunt **waarden van steekproefattributen** nu toevoegen alvorens een attribuut aan een widget in de user-defined composer van dashboards toe te voegen widget. Er zijn enkele voorbeeldwaarden uit die kenmerkkolom beschikbaar voor afzonderlijke kenmerken wanneer u een widget maakt.<br> u kunt **de as van X en van Y** op uw widget met de ruilmiddelknoop nu ruilen. Dit bespaart tijd en biedt een ergonomische ervaring wanneer u kenmerken toevoegt aan uw widgets. Op deze manier kunt u beide kenmerken opnieuw zoeken in het deelvenster Kenmerken.<br> u kunt **de plaats en de titel van de legenda** binnen uw widgets nu veranderen. Nadat een legenda op een widget aanwezig is, kunt u die legenda overal om het diagram verplaatsen en ook de legenda titel hernoemen, zoals u met asetiketten en de widgettitel kunt. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanegidgets tot stand te brengen, begin door het [ overzicht van dashboards ](../../dashboards/home.md) te lezen.

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Adobe Experience Platform-Edge Network kunt sturen waar deze verrijkt, getransformeerd en gedistribueerd kan worden naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe snelstartworkflow voor Meta Conversions API (Beta) | Toegang tot nieuwe snelstartworkflows onder &quot;Aan de slag&quot; vanuit het startscherm van de gegevensverzameling. Het [ snelle beginwerkschema voor de Conversies van Meta API ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start) laat klanten toe om gebeurtenisgegevens, server-kant aan Meta voor advertentieconversies in enkel een paar eenvoudige stappen snel te verzamelen en door:sturen. |
| Nieuwe snelstartworkflow voor Mobile SDK (Beta) | Toegang tot nieuwe snelstartworkflows onder &quot;Aan de slag&quot; vanuit het startscherm van de gegevensverzameling. Het [ snelle beginwerkschema voor Mobiele SDK ](https://developer.adobe.com/client-sdks/documentation/) laat u toe om Mobiele SDK snel uit te voeren en fundamentele mobiele gebeurtenissen in enkel een paar eenvoudige stappen te bevestigen. |
| [!DNL Braze] -gebeurtenis, extensie doorsturen | Met de [[!DNL Braze Track Events API] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) -extensie voor het doorsturen van gebeurtenissen kunt u gegevens die zijn vastgelegd in de Adobe Experience Platform-Edge Network, gebruiken en verzenden naar [!DNL Braze] in de vorm van gebeurtenissen aan de serverzijde met behulp van de [!DNL Braze] User Track API&#39;s. |
| [!DNL Epsilon] -gebeurtenis, extensie doorsturen | Met de extensie [[!DNL Epsilon Events API] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) kunt u gebeurtenissen doorsturen om gebeurtenisinformatie vast te leggen in de Adobe Experience Platform-Edge Network en deze naar [!DNL Epsilon] te verzenden met de [!DNL Epsilon] Event API. |
| [!DNL Mixpanel] -gebeurtenis, extensie doorsturen | Met de extensie [[!DNL Mixpanel Track Events API] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) kunnen klanten gebeurtenissen doorsturen om gebeurtenisinformatie vast te leggen in de Adobe Experience Platform-Edge Network en deze via de API Gebeurtenissen bijhouden naar Mixpanel te verzenden. |

{style="table-layout:auto"}

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van filters voor Adobe Analytics-gegevens | U kunt nu de functies van Data Prep gebruiken om regels en voorwaarden toe te passen om uw analysegegevens te filteren alvorens hen in het Profiel van de Klant in real time op te nemen. Voor meer informatie, lees de gids over [ het filtreren gegevens van Analytics voor het opnemen van het Profiel ](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nieuwe functies voor het coderen en decoderen van URL-tekenreeksen | <ul><li>De functie `get_url_encoded` neemt een URL als invoer en vervangt of codeert speciale karakters met karakters ASCII.</li><li>De functie `get_url_decoded` neemt een URL als invoer en decodeert ASCII-tekens tot speciale tekens.</li></ul> Voor meer informatie, lees de [ Prep functies van Gegevens gids ](../../data-prep/functions.md). Voor een uitvoerige lijst van gereserveerde karakters en hun overeenkomstige gecodeerde karakters, lees de gids op [ speciale karakters ](../../data-prep/functions.md#special-characters). |

Voor meer informatie over Prep van Gegevens, gelieve het [ overzicht van de Prep van Gegevens ](../../data-prep/home.md) te lezen.

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Doel | Beschrijving |
| ----------- | ----------- |
| [[!DNL Adobe Commerce]  verbinding GA ](../../destinations/catalog/personalization/adobe-commerce.md) | Met de [!DNL Adobe Commerce] doelconnector (nu algemeen beschikbaar) kunt u een of meer Real-Time CDP-soorten publiek selecteren om te activeren naar uw [!DNL Adobe Commerce] -account voor een dynamische, gepersonaliseerde ervaring voor uw klanten. |
| [[!DNL Snap Inc]  verbinding GA ](../../destinations/catalog/advertising/snap-inc.md) | Met de [!DNL Snap Inc] doelconnector (nu algemeen beschikbaar) kunnen marketers gebruikerssegmenten die in het Experience Platform zijn gemaakt, importeren in [!DNL Snapchat Ads] en deze gebruiken om hun advertenties te activeren. |
| [ (API) Oracle Eloqua-verbinding ](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Gebruik de op API gebaseerde verbinding met [!DNL Oracle Eloqua] om campagnes te plannen en uit te voeren terwijl een persoonlijke klantervaring wordt geboden voor hun vooruitzichten in [!DNL Oracle Eloqua] . |
| [ (Beta)  [!DNL Amazon Ads]  verbinding ](../../destinations/catalog/advertising/amazon-ads.md) | De [!DNL Amazon Ads] -integratie met Adobe Experience Platform biedt kant-en-klare integratie voor [!DNL Amazon Ads] -producten, inclusief de [!DNL Amazon DSP (ADSP)] -producten. Met behulp van de [!DNL Amazon Ads] -bestemming in Adobe Experience Platform kunnen gebruikers adverteerdersoorten definiëren voor activering en doelversie op de [!DNL Amazon DSP] . |
| [[!DNL Marketo Measure Ultimate]  verbinding ](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (voorheen Bizible) geeft marketeers inzicht in welke marketinginspanningen het meest effectief zijn in het aansturen van inkomsten en het maximaliseren van het rendement van investeringen voor hun bedrijf. De bestemming laat de zaken-aan-zaken (B2B) gegevensstromen van Adobe Experience Platform aan [!DNL Marketo Measure] toe. De kaart is alleen beschikbaar voor [!DNL Marketo Measure Ultimate] klanten. |
| [ verbinding van TikTok ](../../destinations/catalog/social/tiktok.md) | Bouw een aangepast publiek op TikTok met uw gegevens voor doelgerichte advertentiecampagnes. |
| [ verbinding van Zendesk ](../../destinations/catalog/crm/zendesk.md) | Gebruik deze bestemming om identiteiten binnen een segment als contacten binnen [!DNL Zendesk] tot stand te brengen en bij te werken. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Nieuwe toegangsbeheermachtigingen voor doelen: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | De nieuwe toestemming geeft gebruikers de capaciteit om segmenten aan bestaande bestemmingen te activeren, zonder de [ toewijzingsstap ](../../destinations/ui/activate-batch-profile-destinations.md#mapping) te tonen. Gebruikers kunnen segmenten toevoegen en verwijderen in activeringsworkflows, maar kunnen toegewezen kenmerken of identiteiten niet toevoegen of verwijderen. |

{style="table-layout:auto"}

**Correcties en verhogingen** {#destinations-fixes-and-enhancements}

Er wordt een foutopsporing voor PGP/GPG-codering vrijgegeven in bestandsgebaseerde doelen voor Real-Time CDP. Met deze wijziging genereren bestaande op bestanden gebaseerde doelen die momenteel codering gebruiken een bestandsnaam met een andere extensie dan voorheen.

- Huidige extensie bij gebruik van codering: `filename.csv`
- Future extension when using encryption: `filename.csv.gpg`

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| CSV naar schemaaanbeveling | U kunt nu uw lokale bestanden uploaden om via een computer opgeleide schema&#39;s te maken die het niet nodig maken om handmatig een schema te maken. Vanuit de werkruimte van [!UICONTROL Sources] uploadt u een voorbeeld-CSV-bestand. Leeralgoritmen voor Adobe-apparaten stellen een schema voor u voor op basis van de doelvelden. Zie de [ documentatie ](../../ingestion/tutorials/map-csv/recommendations.md) voor meer informatie.&quot; |

{style="table-layout:auto"}

**Nieuwe componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Klasse | [[!UICONTROL Offer Item]](https://github.com/adobe/xdm/pull/1678/files) | Klasse die een voorstel vertegenwoordigt. |
| Klasse | [[!UICONTROL Decision Item]](https://github.com/adobe/xdm/pull/1678/files) | Een punt dat aan een beslissing kan worden onderworpen. De output van een besluitvormingsproces is één of meerdere besluitvormingspunten. |
| Klasse | [[!UICONTROL Media Session Server Timeout]](https://github.com/adobe/xdm/pull/1676/files) | Dit wijst op de hoeveelheid tijd, in seconden, die tussen de laatste bekende interactie van de gebruiker en het ogenblik inging de zitting werd gesloten. |
| Veldgroep | [[!UICONTROL XDM Profile Computed Attributes]](https://github.com/adobe/xdm/pull/1686/files) | Hiermee voegt u berekende kenmerken van interne Adobe-services toe aan inkomende klantgegevens. Dit zou niet door klanten moeten worden gebruikt om gegevens in te voeren. |
| Gegevenstype | [[!UICONTROL Refund Item]](https://github.com/adobe/xdm/pull/1685/files) | Hiermee wordt aangegeven of een restitutie aan een bestelling is gekoppeld en wordt het type restitutie, het bedrag en de bijbehorende valuta gedefinieerd. |
| Gegevenstype | [[!UICONTROL Category data]](https://github.com/adobe/xdm/pull/1677/files) | Dit nieuwe datatype vertegenwoordigt de categorie van een product. |
| Schema | [[!UICONTROL Adobe Target Classification Fields]](https://github.com/adobe/xdm/pull/1682/files) | Er is een nieuw XDM-schema gemaakt voor de gegevenssets van de doelclassificatie. Het bevat een reeks meta-gegevensgebieden die de activiteiten en de ervaringen van het Doel classificeren. |

{style="table-layout:auto"}

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [[!UICONTROL Content Component Details]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` is verwijderd uit [!UICONTROL Content Component Details] |
| Veldgroep | [[!UICONTROL AJO Entity tags]](https://github.com/adobe/xdm/pull/1672/files) | AJO Entiteitscodes toegevoegd aan [!UICONTROL AJO Entity Fields] die overeenkomen met een reis of campagne |
| Veldgroep | (Meerdere) | Verschillende velden toegevoegd voor [[!UICONTROL Journey Orchestration Step Event Common Fields] ](https://github.com/adobe/xdm/pull/1671/files) |
| Veldgroep | (Meerdere) | [ toegevoegde verscheidene XDM gebeurtenistypen voor [!UICONTROL Media Reporting] ](https://github.com/adobe/xdm/pull/1670/files). |
| Veldgroep | [!UICONTROL Workfront Change Event] | De veldgroepen `Full Record` en `Accessor Employee Ids` zijn toegevoegd. |
| Gegevenstype | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Refund Amount] is toegevoegd om het bedrag aan te geven dat voor het item is terugbetaald, indien van toepassing. |
| Gegevenstype | [[!UICONTROL Order ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Refunds List] is toegevoegd aan de lijst met terugbetalingen voor deze bestelling. |
| Gegevenstype | [[!UICONTROL Product List Item ]](https://github.com/adobe/xdm/pull/1677/files) | Productcategorieën zijn toegevoegd aan de lijst met categoriegegevens van dit product. |
| Gegevenstype | [!UICONTROL Session details information] | Toegevoegd het `pev3` koordgebied dat [ op het type van de media stroom wijst die voor het melden van ](https://github.com/adobe/xdm/pull/1676/files) wordt gebruikt. De eigenschap `pccr` wordt ook toegevoegd om aan te geven of een omleiding heeft plaatsgevonden. |
| Gegevenstype | [!UICONTROL Requisition List] | Verstrekt de [ eigenschappen van de verzoeklijst ](https://github.com/adobe/xdm/pull/1675/files). Deze bevatten naam, id en beschrijving. |
| Gegevenstype | [!UICONTROL Commerce] | Het [ gegevenstype van Commerce werd bijgewerkt ](https://github.com/adobe/xdm/pull/1675/files) om `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`, en `requisitionList` te omvatten. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, lees het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Query-service {#query-service}

Met Query Service kunt u standaard-SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake] . U kunt zich bij om het even welke datasets van gegevens aansluiten meer en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Wetenschap van Gegevens Workspace, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Kenmerk gebaseerd toegangsbeheer op de versnelde opslag | Het op attributen-gebaseerde Toegangsbeheer van het gebruik met Gegevens Distiller om toegangsbeheer op alle datasets op de versnelde opslag te bepalen. Dit controleert toegang tot de modellen van douanegegevens die door gebruikers worden gecreeerd en op een versnelde opslag worden opgeslagen om douanedashboards te aandrijven. |

{style="table-layout:auto"}

Voor meer informatie over de Diensten van de Vraag, verwijs naar het [ overzicht van de Dienst van de Vraag ](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP B2B Edition is gebaseerd op Real-time Customer Data Platform (Real-Time CDP) en is speciaal ontworpen voor marketers die werken in een servicemodel voor bedrijven. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen in dienst te nemen.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| rugvoegsel | Voor een nauwkeurigere weergave van profielen in uw systeem bevat het systeem geen interne profielen meer in het totale aantal profielen of de meetwaarde voor het adresseerbare publiek voor de Real-time Customer Data Platform B2B Edition. Vanaf vandaag is het mogelijk dat het totale aantal profielen/adresseerbare publiek slechts één keer daalt. Geen van uw gegevens is gewist, dit is gewoon een wijziging in de telling. Neem contact op met uw Adobe-medewerker voor eventuele problemen |

{style="table-layout:auto"}

Meer over de Uitgave van Real-Time CDP B2B leren, lees het [ overzicht van de Uitgave van Real-Time CDP B2B ](../../rtcdp/overview.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Profielafmetingen | Om u een nauwkeurigere vertegenwoordiging van profielmetriek te geven, worden de lidmaatschapsuitsplitsing en de cijfers van de kroon gecombineerd en nu berekend over een periode van 24 uur. Meer informatie is beschikbaar in de [ gids van de Segmentatie UI ](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], gelieve te zien het [ overzicht van de Segmentatie ](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en stelt u in staat die gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Beta-beschikbaarheid van [!DNL Chatlio] | De bron [!DNL Chatlio] is nu beschikbaar in bèta. Gebruik de [!DNL Chatlio] -bron om uw [!DNL Chatlio] -gebeurtenisgegevens te streamen naar het Experience Platform. Voor meer informatie, lees het [[!DNL Chatlio]  overzicht ](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Beta-beschikbaarheid van [!DNL Customer.io] | De bron [!DNL Customer.io] is nu beschikbaar in bèta. Gebruik de [!DNL Customer.io] -bron om de gegevens van klantgebeurtenissen te streamen naar het Experience Platform. Voor meer informatie, lees het [[!DNL Customer.io]  overzicht ](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Beta-beschikbaarheid van [!DNL Pendo] | De bron [!DNL Pendo] is nu beschikbaar in bèta. Gebruik de [!DNL Pendo] -bron om de analysegegevens van uw product naar het Experience Platform te streamen. Voor meer informatie, lees het [[!DNL Pendo]  overzicht ](../../sources/connectors/analytics/pendo-webhook.md). |
| Ondersteuning voor conceptgegevensstromen | U kunt nu de Flow Service API gebruiken om uw gegevensstromen in te stellen op een conceptstatus. Tekenstromen kunnen later worden bijgewerkt en gepubliceerd met nieuwe informatie. Voor meer informatie, lees de gids bij [ plaatsend uw brongegevens als concepten ](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Meer over bronnen leren, lees het [ overzicht van bronnen ](../../sources/home.md).
