---
title: Aanvullende informatie van maart 2023 voor Adobe Experience Platform
description: Aanvullende informatie van maart 2023 voor Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 26%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum:donderdag 29 maart 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Dataverzameling](#data-collection)
- [Gegevensvoorbereiding](#data-prep)
- [Bestemmingen](#destinations)
- [Experience Data Model](#xdm)
- [Query-service](#query-service)
- [Real-Time Customer Data Platform B2B Edition](#b2b)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten kunt bekijken over de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte eigenschappen** {#dashboards-new-updated-features}

| Functie | Beschrijving |
| --- | --- |
| Door gebruiker gedefinieerde dashboards | U kunt **waarden van steekproefattributen** nu toevoegen alvorens een attribuut aan een widget in de user-defined composer van dashboards toe te voegen widget. Er zijn enkele voorbeeldwaarden uit die kenmerkkolom beschikbaar voor afzonderlijke kenmerken wanneer u een widget maakt.<br> u kunt **de as van X en van Y** op uw widget met de ruilmiddelknoop nu ruilen. Dit bespaart tijd en biedt een ergonomische ervaring wanneer u kenmerken toevoegt aan uw widgets. Op deze manier kunt u beide kenmerken opnieuw zoeken in het deelvenster Kenmerken.<br> u kunt **de plaats en de titel van de legenda** binnen uw widgets nu veranderen. Nadat een legenda op een widget aanwezig is, kunt u die legenda overal om het diagram verplaatsen en ook de legenda titel hernoemen, zoals u met asetiketten en de widgettitel kunt. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, inclusief het verlenen van toegangsrechten en het maken van aangepaste widgets, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe snelstartworkflow voor Meta Conversions API (Beta) | Krijg toegang tot nieuwe snelstartworkflows onder Aan de slag vanuit het startscherm voor gegevensverzameling. Het [&#x200B; snelle beginwerkschema voor de Conversies van Meta API &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=nl-NL#quick-start) laat klanten toe om gebeurtenisgegevens, server-kant aan Meta voor advertentieconversies in enkel een paar eenvoudige stappen snel te verzamelen en door:sturen. |
| Nieuwe snelstartworkflow voor Mobile SDK (Beta) | Krijg toegang tot nieuwe snelstartworkflows onder Aan de slag vanuit het startscherm voor gegevensverzameling. Het [&#x200B; snelle beginwerkschema voor Mobiele SDK &#x200B;](https://developer.adobe.com/client-sdks/documentation/) laat u toe om Mobiele SDK snel uit te voeren en fundamentele mobiele gebeurtenissen in enkel een paar eenvoudige stappen te bevestigen. |
| [!DNL Braze] -gebeurtenis, extensie doorsturen | Met de [[!DNL Braze Track Events API] &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=nl-NL) -extensie voor het doorsturen van gebeurtenissen kunt u gegevens die zijn vastgelegd in de Adobe Experience Platform Edge Network, gebruiken en verzenden naar [!DNL Braze] in de vorm van gebeurtenissen aan de serverzijde met behulp van de [!DNL Braze] User Track API&#39;s. |
| [!DNL Epsilon] -gebeurtenis, extensie doorsturen | Met de extensie [[!DNL Epsilon Events API] &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html?lang=nl-NL) kunt u gebeurtenissen doorsturen om gebeurtenisinformatie vast te leggen in de Adobe Experience Platform Edge Network en deze naar [!DNL Epsilon] te verzenden met de [!DNL Epsilon] Event-API. |
| [!DNL Mixpanel] -gebeurtenis, extensie doorsturen | Met de extensie [[!DNL Mixpanel Track Events API] &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=nl-NL) kunnen klanten gebeurtenissen doorsturen om gebeurtenisinformatie vast te leggen in de Adobe Experience Platform Edge Network en deze naar Mixpanel te verzenden met de API voor gebeurtenissen bijhouden. |

{style="table-layout:auto"}

## Gegevensvoorbereiding {#data-prep}

Met gegevensvoorbereiding kunnen gegevenstechnici gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience-datamodel).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van filters voor Adobe Analytics-gegevens | U kunt nu de functies van Data Prep gebruiken om regels en voorwaarden toe te passen om uw analysegegevens te filteren alvorens hen in het Profiel van de Klant in real time op te nemen. Voor meer informatie, lees de gids over [&#x200B; het filtreren gegevens van Analytics voor het opnemen van het Profiel &#x200B;](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nieuwe functies voor het coderen en decoderen van URL-tekenreeksen | <ul><li>De functie `get_url_encoded` neemt een URL als invoer en vervangt of codeert speciale karakters met karakters ASCII.</li><li>De functie `get_url_decoded` neemt een URL als invoer en decodeert ASCII-tekens tot speciale tekens.</li></ul> Voor meer informatie, lees de [&#x200B; Prep functies van Gegevens gids &#x200B;](../../data-prep/functions.md). Voor een uitvoerige lijst van gereserveerde karakters en hun overeenkomstige gecodeerde karakters, lees de gids op [&#x200B; speciale karakters &#x200B;](../../data-prep/functions.md#special-characters). |

Voor meer informatie over Prep van Gegevens, gelieve het [&#x200B; overzicht van de Prep van Gegevens &#x200B;](../../data-prep/home.md) te lezen.

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe bestemmingen** {#new-destinations}

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Adobe Commerce]  verbinding GA &#x200B;](../../destinations/catalog/personalization/adobe-commerce.md) | Met de [!DNL Adobe Commerce] doelconnector (nu algemeen beschikbaar) kunt u een of meer Real-Time CDP-soorten publiek selecteren om te activeren naar uw [!DNL Adobe Commerce] -account voor een dynamische, gepersonaliseerde ervaring voor uw klanten. |
| [[!DNL Snap Inc]  verbinding GA &#x200B;](../../destinations/catalog/advertising/snap-inc.md) | Met de [!DNL Snap Inc] doelconnector (nu algemeen beschikbaar) kunnen marketers gebruikerssegmenten die in Experience Platform zijn gemaakt, importeren in [!DNL Snapchat Ads] en deze gebruiken om hun advertenties te activeren. |
| [&#x200B; (API) Oracle Eloqua-verbinding &#x200B;](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Gebruik de op API gebaseerde verbinding met [!DNL Oracle Eloqua] om campagnes te plannen en uit te voeren terwijl een persoonlijke klantervaring wordt geboden voor hun vooruitzichten in [!DNL Oracle Eloqua] . |
| [&#x200B; (Beta)  [!DNL Amazon Ads]  verbinding &#x200B;](../../destinations/catalog/advertising/amazon-ads.md) | De [!DNL Amazon Ads] -integratie met Adobe Experience Platform biedt kant-en-klare integratie voor [!DNL Amazon Ads] -producten, inclusief de [!DNL Amazon DSP (ADSP)] -producten. Met behulp van de [!DNL Amazon Ads] -bestemming in Adobe Experience Platform kunnen gebruikers adverteerdersoorten definiëren voor activering en doelversie op de [!DNL Amazon DSP] . |
| [[!DNL Marketo Measure Ultimate] verbinding](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (voorheen Bizible) biedt marketers insight de mogelijkheid om marketingactiviteiten te ontplooien die de meest efficiënte manier zijn om inkomsten te genereren en het rendement van investeringen voor hun bedrijf te maximaliseren. De bestemming laat de zaken-aan-zaken (B2B) gegevensstromen van Adobe Experience Platform aan [!DNL Marketo Measure] toe. De kaart is alleen beschikbaar voor [!DNL Marketo Measure Ultimate] klanten. |
| [&#x200B; verbinding van TikTok &#x200B;](../../destinations/catalog/social/tiktok.md) | Bouw een aangepast publiek op TikTok met uw gegevens voor doelgerichte advertentiecampagnes. |
| [&#x200B; verbinding van Zendesk &#x200B;](../../destinations/catalog/crm/zendesk.md) | Gebruik deze bestemming om identiteiten binnen een segment als contacten binnen [!DNL Zendesk] tot stand te brengen en bij te werken. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Nieuwe toegangsbeheermachtigingen voor doelen: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | De nieuwe toestemming geeft gebruikers de capaciteit om segmenten aan bestaande bestemmingen te activeren, zonder de [&#x200B; toewijzingsstap &#x200B;](../../destinations/ui/activate-batch-profile-destinations.md#mapping) te tonen. Gebruikers kunnen segmenten toevoegen en verwijderen in activeringsworkflows, maar kunnen toegewezen kenmerken of identiteiten niet toevoegen of verwijderen. |

{style="table-layout:auto"}

**Opgeloste problemen en verbeteringen** {#destinations-fixes-and-enhancements}

Er wordt een foutopsporing voor PGP/GPG-codering vrijgegeven in bestandsgebaseerde doelen voor Real-Time CDP. Met deze wijziging genereren bestaande op bestanden gebaseerde doelen die momenteel codering gebruiken een bestandsnaam met een andere extensie dan voorheen.

- Huidige extensie bij gebruik van codering: `filename.csv`
- Future extension when using encryption: `filename.csv.gpg`

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| CSV naar schemaaanbeveling | U kunt nu uw lokale bestanden uploaden om via een computer opgeleide schema&#39;s te maken die het niet nodig maken om handmatig een schema te maken. Upload vanuit de werkruimte van [!UICONTROL Sources] een voorbeeld-CSV-bestand en Adobe-algoritmen voor machinetaken stellen een schema voor u voor op basis van de doelvelden. Zie de [&#x200B; documentatie &#x200B;](../../ingestion/tutorials/map-csv/recommendations.md) voor meer informatie.&quot; |

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
| Veldgroep | (Meerdere) | Verschillende velden toegevoegd voor [[!UICONTROL Journey Orchestration Step Event Common Fields] &#x200B;](https://github.com/adobe/xdm/pull/1671/files) |
| Veldgroep | (Meerdere) | [&#x200B; toegevoegde verscheidene XDM gebeurtenistypen voor [!UICONTROL Media Reporting] &#x200B;](https://github.com/adobe/xdm/pull/1670/files). |
| Veldgroep | [!UICONTROL Workfront Change Event] | De veldgroepen `Full Record` en `Accessor Employee Ids` zijn toegevoegd. |
| Gegevenstype | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Refund Amount] is toegevoegd om het bedrag aan te geven dat voor het item is terugbetaald, indien van toepassing. |
| Gegevenstype | [[!UICONTROL Order &#x200B;]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Refunds List] is toegevoegd aan de lijst met terugbetalingen voor deze bestelling. |
| Gegevenstype | [[!UICONTROL Product List Item &#x200B;]](https://github.com/adobe/xdm/pull/1677/files) | Productcategorieën zijn toegevoegd aan de lijst met categoriegegevens van dit product. |
| Gegevenstype | [!UICONTROL Session details information] | Toegevoegd het `pev3` koordgebied dat [&#x200B; op het type van de media stroom wijst die voor het melden van &#x200B;](https://github.com/adobe/xdm/pull/1676/files) wordt gebruikt. De eigenschap `pccr` wordt ook toegevoegd om aan te geven of een omleiding heeft plaatsgevonden. |
| Gegevenstype | [!UICONTROL Requisition List] | Verstrekt de [&#x200B; eigenschappen van de verzoeklijst &#x200B;](https://github.com/adobe/xdm/pull/1675/files). Deze bevatten naam, id en beschrijving. |
| Gegevenstype | [!UICONTROL Commerce] | Het [&#x200B; gegevenstype van Commerce werd bijgewerkt &#x200B;](https://github.com/adobe/xdm/pull/1675/files) om `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`, en `requisitionList` te omvatten. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Experience Platform, lees het [&#x200B; XDM overzicht van het Systeem &#x200B;](../../xdm/home.md).

## Query-service {#query-service}

Met de Query-service kunt u standaard SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake]. U kunt alle datasets uit Data Lake samenvoegen en de queryresultaten vastleggen als een nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Kenmerk gebaseerd toegangsbeheer op de versnelde opslag | Het op attributen-gebaseerde Toegangsbeheer van het gebruik met Gegevens Distiller om toegangsbeheer op alle datasets op de versnelde opslag te bepalen. Dit controleert toegang tot de modellen van douanegegevens die door gebruikers worden gecreeerd en op een versnelde opslag worden opgeslagen om douanedashboards te aandrijven. |

{style="table-layout:auto"}

Voor meer informatie over Query-services raadpleegt u het [overzicht van Query-services](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP B2B edition is gebaseerd op Real-Time Customer Data Platform (Real-Time CDP) en is speciaal ontworpen voor marketers die werken in een servicemodel voor bedrijven. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen in dienst te nemen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| rugvoegsel | Voor een nauwkeurigere weergave van profielen in uw systeem bevat het systeem geen interne profielen meer in het totale aantal profielen of de meetwaarde voor het adresseerbare publiek voor de Real-Time Customer Data Platform B2B edition. Vanaf vandaag is het mogelijk dat het totale aantal profielen/adresseerbare publiek slechts één keer daalt. Geen van uw gegevens is gewist, dit is gewoon een wijziging in de telling. Neem contact op met uw Adobe-medewerker voor eventuele problemen |

{style="table-layout:auto"}

Meer over Real-Time CDP B2B edition leren, lees het [&#x200B; overzicht van B2B edition van Real-Time CDP &#x200B;](../../rtcdp/overview.md).

## Segmentatieservice {#segmentation}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Profielafmetingen | Om u een nauwkeurigere vertegenwoordiging van profielmetriek te geven, worden de lidmaatschapsuitsplitsing en de cijfers van de kroon gecombineerd en nu berekend over een periode van 24 uur. Meer informatie is beschikbaar in de [&#x200B; gids van de Segmentatie UI &#x200B;](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Beta-beschikbaarheid van [!DNL Chatlio] | De bron [!DNL Chatlio] is nu beschikbaar in bèta. Gebruik de [!DNL Chatlio] -bron om uw [!DNL Chatlio] -gebeurtenisgegevens te streamen naar Experience Platform. Voor meer informatie, lees het [[!DNL Chatlio]  overzicht &#x200B;](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Beta-beschikbaarheid van [!DNL Customer.io] | De bron [!DNL Customer.io] is nu beschikbaar in bèta. Gebruik de [!DNL Customer.io] -bron om de gegevens van klantgebeurtenissen te streamen naar Experience Platform. Voor meer informatie, lees het [[!DNL Customer.io]  overzicht &#x200B;](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Beta-beschikbaarheid van [!DNL Pendo] | De bron [!DNL Pendo] is nu beschikbaar in bèta. Gebruik de bron [!DNL Pendo] om de analysegegevens van uw product naar Experience Platform te streamen. Voor meer informatie, lees het [[!DNL Pendo]  overzicht &#x200B;](../../sources/connectors/analytics/pendo-webhook.md). |
| Ondersteuning voor conceptgegevensstromen | U kunt nu de Flow Service API gebruiken om uw gegevensstromen in te stellen op een conceptstatus. Tekenstromen kunnen later worden bijgewerkt en gepubliceerd met nieuwe informatie. Voor meer informatie, lees de gids bij [&#x200B; plaatsend uw brongegevens als concepten &#x200B;](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u het [overzicht van bronnen](../../sources/home.md).
