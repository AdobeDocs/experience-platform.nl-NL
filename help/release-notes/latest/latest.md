---
title: Aanvullende informatie over Adobe Experience Platform
description: In de release van maart 2023 staat Adobe Experience Platform vermeld.
source-git-commit: 582305583aa5869d8cc29f871aeb3fa0ef0b6ab1
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 29 maart 2023**

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

**Nieuwe of bijgewerkte functies** {#dashboards-new-updated-features}

| Functie | Beschrijving |
| --- | --- |
| Door gebruiker gedefinieerde dashboards | U kunt nu **kenmerkwaarden van voorbeeld** voordat u een kenmerk aan een widget toevoegt in de door de gebruiker gedefinieerde dashboards-widgetcomposer. Er zijn enkele voorbeeldwaarden uit die kenmerkkolom beschikbaar voor afzonderlijke kenmerken wanneer u een widget maakt.<br>U kunt nu **X- en Y-as omwisselen** op uw widget met de knop voor wisselen van as. Dit bespaart tijd en biedt een ergonomische ervaring wanneer u kenmerken toevoegt aan uw widgets. Op deze manier kunt u beide kenmerken opnieuw zoeken in het deelvenster Kenmerken.<br>U kunt nu **de locatie en titel van de legenda wijzigen** binnen uw widgets. Nadat een legenda op een widget aanwezig is, kunt u die legenda overal om het diagram verplaatsen en ook de legenda titel hernoemen, zoals u met asetiketten en de widgettitel kunt. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanewidgets tot stand te brengen, begin door te lezen [overzicht van dashboards](../../dashboards/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe snelstartworkflow voor Meta Conversions API (Bèta) | Toegang tot nieuwe snelstartworkflows onder &quot;Aan de slag&quot; vanuit het startscherm van de gegevensverzameling. De [quick start workflow voor Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) biedt klanten de mogelijkheid om gebeurtenisgegevens snel te verzamelen en door te sturen, servergegevens naar Meta voor conversie van advertenties in een paar eenvoudige stappen. |
| [!DNL Braze] extensie voor doorsturen van gebeurtenissen | De [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Met de extensie voor het doorsturen van gebeurtenissen kunt u gegevens die zijn vastgelegd in het Adobe Experience Platform Edge-netwerk, benutten en verzenden naar [!DNL Braze] in de vorm van server-side-gebeurtenissen die de [!DNL Braze] Gebruikerstrack-API&#39;s. |
| [!DNL Mixpanel] extensie voor doorsturen van gebeurtenissen | De [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Met de extensie kunnen klanten gebeurtenisberichten gebruiken om gebeurtenisgegevens vast te leggen in het Adobe Experience Platform Edge-netwerk en deze via de API Gebeurtenissen bijhouden naar Mixpanel te verzenden. |

{style="table-layout:auto"}

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van filters voor Adobe Analytics-gegevens | U kunt nu de functies van Data Prep gebruiken om regels en voorwaarden toe te passen om uw analysegegevens te filteren alvorens hen in het Profiel van de Klant in real time op te nemen. Lees voor meer informatie de handleiding op [filteren, analysegegevens voor profielopname](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nieuwe functies voor het coderen en decoderen van URL-tekenreeksen | <ul><li>De `get_url_encoded` Deze functie neemt een URL als invoer en vervangt of codeert speciale tekens door ASCII-tekens.</li><li>De `get_url_decoded` De functie neemt een URL als input en decodeert ASCII karakters in speciale karakters.</li></ul> Lees voor meer informatie de [Handleiding voor functies Data Prep](../../data-prep/functions.md). Lees de handleiding voor een uitgebreide lijst met gereserveerde tekens en de bijbehorende gecodeerde tekens [speciale tekens](../../data-prep/functions.md#special-characters). |

Voor meer informatie over Data Prep, gelieve te lezen [Overzicht van Data Prep](../../data-prep/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] aansluiting voor GA](../../destinations/catalog/personalization/adobe-commerce.md) | De [!DNL Adobe Commerce] met de doelconnector (nu algemeen beschikbaar) kunt u een of meer Real-Time CDP-soorten selecteren die u voor uw [!DNL Adobe Commerce] -account voor een dynamische, op maat gesneden ervaring voor kopers. |
| [[!DNL Snap Inc] aansluiting voor GA](../../destinations/catalog/advertising/snap-inc.md) | De [!DNL Snap Inc] bestemmingsschakelaar (nu algemeen beschikbaar) staat marketers toe om gebruikerssegmenten die in Experience Platform worden gecreeerd in te voeren [!DNL Snapchat Ads] en gebruik ze om hun advertenties te richten. |
| [(API) Oracle Eloqua-verbinding](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | De op API gebaseerde verbinding gebruiken voor [!DNL Oracle Eloqua] om campagnes te plannen en uit te voeren terwijl het leveren van een gepersonaliseerde klantenervaring voor hun vooruitzichten in [!DNL Oracle Eloqua]. |
| [(bèta) [!DNL Amazon Ads] verbinding](../../destinations/catalog/advertising/amazon-ads.md) | De [!DNL Amazon Ads] integratie met Adobe Experience Platform biedt een sleutelintegratie voor [!DNL Amazon Ads] producten, met inbegrip van [!DNL Amazon DSP (ADSP)]. Met de [!DNL Amazon Ads] doel in Adobe Experience Platform, kunnen gebruikers adverteerderspubliek voor doelgericht en activering op het [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] verbinding](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (voorheen Bizible) geeft marketeers inzicht in welke marketinginspanningen het meest effectief zijn in het aansturen van inkomsten en het maximaliseren van het rendement van investeringen voor hun bedrijf. De bestemming laat de zaken-aan-zaken (B2B) gegevensstromen van Adobe Experience Platform aan toe [!DNL Marketo Measure]. De kaart is alleen beschikbaar voor [!DNL Marketo Measure Ultimate] klanten. |
| [TikTok-verbinding](../../destinations/catalog/social/tiktok.md) | Bouw een aangepast publiek op TikTok met uw gegevens voor doelgerichte advertentiecampagnes. |
| [Zendesk-verbinding](../../destinations/catalog/crm/zendesk.md) | Gebruik deze bestemming om identiteiten binnen een segment als contacten binnen tot stand te brengen en bij te werken [!DNL Zendesk]. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Nieuwe toegangsbeheermachtigingen voor bestemmingen: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | De nieuwe toestemming geeft gebruikers de capaciteit om segmenten aan bestaande bestemmingen te activeren, zonder het tonen van [toewijzingsstap](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Gebruikers kunnen segmenten toevoegen en verwijderen in activeringsworkflows, maar kunnen toegewezen kenmerken of identiteiten niet toevoegen of verwijderen. |

{style="table-layout:auto"}

**Oplossingen en verbeteringen** {#destinations-fixes-and-enhancements}

Wij geven een insectenmoeilijke situatie voor encryptie PGP/GPG in op dossier-gebaseerde bestemmingen voor CDP in real time vrij. Met deze wijziging genereren bestaande op bestanden gebaseerde doelen die momenteel codering gebruiken een bestandsnaam met een andere extensie dan voorheen.

- Huidige extensie bij gebruik van codering: `filename.csv`
- Toekomstige extensie bij gebruik van codering: `filename.csv.gpg`

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| CSV naar schemaaanbeveling | U kunt nu uw lokale bestanden uploaden om via een computer opgeleide schema&#39;s te maken die het niet nodig maken om handmatig een schema te maken. Van de [!UICONTROL Sources] werkruimte, uploadt u een CSV-voorbeeldbestand en leert u algoritmes voor Adobe-computers een schema voor u op basis van de doelvelden. Zie de [documentatie](../../ingestion/tutorials/map-csv/recommendations.md) voor meer informatie.&quot; |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, lees [XDM System, overzicht](../../xdm/home.md).

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL Data Lake]. U kunt zich bij om het even welke datasets van gegevens aansluiten meer en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Kenmerk gebaseerd toegangsbeheer op de versnelde opslag | Het op attributen-gebaseerde Toegangsbeheer van het gebruik met Gegevens Distiller om toegangsbeheer op alle datasets op de versnelde opslag te bepalen. Dit controleert toegang tot de modellen van douanegegevens die door gebruikers worden gecreeerd en op een versnelde opslag worden opgeslagen om douanedashboards te aandrijven. |

{style="table-layout:auto"}

Voor meer informatie over de Diensten van de Vraag, verwijs naar [Overzicht van Query Service](../../query-service/home.md).

## Real-Time Customer Data Platform B2B Edition {#b2b}

Real-Time CDP B2B Edition is gebaseerd op Real-time Customer Data Platform (Real-Time CDP) en is speciaal ontworpen voor marketers die werken in een servicemodel voor bedrijven. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen te betrekken.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| rugvoegsel | Voor een nauwkeurigere weergave van profielen in uw systeem bevat het systeem geen interne profielen meer in het totale aantal profielen of de meetwaarde voor het adresseerbare publiek voor de Real-time Customer Data Platform B2B Edition. Vanaf vandaag is het mogelijk dat het totale aantal profielen/adresseerbare publiek slechts één keer daalt. Geen van uw gegevens is gewist, dit is gewoon een wijziging in de telling. Neem contact op met uw Adobe-medewerker voor eventuele problemen |

{style="table-layout:auto"}

Lees voor meer informatie over de Real-Time CDP B2B Edition de [Overzicht van Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Profielafmetingen | Om u een nauwkeurigere vertegenwoordiging van profielmetriek te geven, worden de lidmaatschapsuitsplitsing en de cijfers van de kroon gecombineerd en nu berekend over een periode van 24 uur. Meer informatie is beschikbaar in het dialoogvenster [Handleiding voor segmenteringsinterface](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Beta beschikbaarheid van [!DNL Chatlio] | De [!DNL Chatlio] De bron is nu beschikbaar in bèta. Gebruik de [!DNL Chatlio] bron om uw [!DNL Chatlio] gebeurtenisgegevens naar Experience Platform. Lees voor meer informatie de [[!DNL Chatlio] overzicht](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Beta beschikbaarheid van [!DNL Customer.io] | De [!DNL Customer.io] De bron is nu beschikbaar in bèta. Gebruik de [!DNL Customer.io] bron om gegevens van klantgebeurtenissen naar Experience Platform te streamen. Lees voor meer informatie de [[!DNL Customer.io] overzicht](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Beta beschikbaarheid van [!DNL Pendo] | De [!DNL Pendo] De bron is nu beschikbaar in bèta. Gebruik de [!DNL Pendo] bron om de analysegegevens van uw product naar het Experience Platform te streamen. Lees voor meer informatie de [[!DNL Pendo] overzicht](../../sources/connectors/analytics/pendo-webhook.md). |
| Ondersteuning voor conceptgegevensstromen | U kunt nu de Flow Service API gebruiken om uw gegevensstromen in te stellen op een conceptstatus. Tekeningen van gegevensstromen kunnen later met nieuwe informatie worden bijgewerkt en worden gepubliceerd. Lees voor meer informatie de handleiding op [gegevensstromen van bronnen instellen als concepten](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
