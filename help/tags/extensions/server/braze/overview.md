---
keywords: gebeurtenis door:sturen uitbreiding;breze;breze gebeurtenis door:sturen uitbreiding
title: Braze Event Forwarding Extension
description: Deze Adobe Experience Platform-extensie voor het doorsturen van gebeurtenissen verzendt Adobe Experience Edge Network-gebeurtenissen naar Braze.
source-git-commit: e48e7185f16a9572f2d61610b812d2ad27b7cb7f
workflow-type: tm+mt
source-wordcount: '2593'
ht-degree: 0%

---

# [!DNL Braze Track Events API] extensie voor doorsturen van gebeurtenissen

[[!DNL Braze]](https://www.braze.com) is een platform van de klantenovereenkomst dat klant-gerichte interactie tussen consumenten en merken in real time drijft. Gebruiken [!DNL Braze]kunt u het volgende doen:

* Gegevens (zoals marketingberichten) leveren aan doelgebruikers op basis van hun taalvoorkeur, voorkeur voor locaties en meer, om de conversietarieven te verhogen en belangrijke bedrijfsdoelstellingen te ondersteunen.
* Verzend klanten gepersonaliseerde berichten over veelvoudige kanalen, met inbegrip van e-mail, dupberichten, en in-app berichten, op enkel de juiste tijd en in hun aangewezen talen.
* Doelspecifieke gebruikers voor marketing- en promotiecampagnes om het aantal herhaalde klanten te vergroten.
* Het gebruikersgedrag en de patronen van de studie om specifieke doelgroepen met aangepaste berichten te richten, die zouden kunnen helpen opbrengst verhogen.

De [!DNL Braze Track Events API] [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) kunt u gegevens die zijn vastgelegd in het Adobe Experience Platform Edge Network gebruiken en verzenden naar [!DNL Braze] in de vorm van server-side-gebeurtenissen die de [[!DNL Braze User Identify]](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify) en [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API&#39;s.

Dit document behandelt de gebruiksgevallen van de uitbreiding, hoe te om het in uw gebeurtenis te installeren die bibliotheken door:sturen, en hoe te om zijn mogelijkheden in een gebeurtenis aan te wenden die door:sturen [regel](../../../ui/managing-resources/rules.md).

## Gebruiksscenario’s

Deze extensie moet worden gebruikt als u gegevens van het Edge-netwerk wilt gebruiken in [!DNL Braze] om voordeel te halen uit zijn klantenanalyses en gerichte mogelijkheden.

Neem bijvoorbeeld een detailhandelsorganisatie die een multikanaalaanwezigheid (website en mobiel) heeft en die transactie- of gespreksinvoer vastlegt als gebeurtenisgegevens van hun website en mobiele platforms. Diverse gebruiken [tag](../../../home.md) regels, worden deze gegevens verzonden naar het Netwerk van de Rand in echt - tijd. Van hier, [!DNL Braze] gebeurtenis die uitbreiding door:sturen verzendt automatisch relevante gebeurtenissen naar [!DNL Braze] aan de serverzijde.

Zodra de gegevens zijn verzonden, kunnen de analyseteams van de organisatie vervolgens gebruikmaken van [!DNL Braze's] mogelijkheden om de datasets te verwerken en bedrijfsinzichten af te leiden om grafieken, dashboards, of andere visualisaties te produceren om bedrijfsbelanghebbenden te informeren. Zie de [[!DNL Braze] klanten](https://www.braze.com/customers) pagina voor meer informatie over de verschillende gebruiksgevallen van het platform.

## [!DNL Braze] voorwaarden en waarborgen {#prerequisites}

U moet beschikken over een [!DNL Braze] rekening te houden met haar technologieën. Als u geen account hebt, navigeert u naar de [Aan de slag-pagina](https://www.braze.com/get-started/) op [!DNL Braze] om verbinding te maken met [!DNL Braze Sales] en start het accountaanmaakproces.

### API-handleidingen

De extensie gebruikt twee van [!DNL Braze]API&#39;s en de bijbehorende beperkingen worden hieronder beschreven:

| API | Snelheidslimieten |
| --- | --- |
| [!DNL User Track] | 50.000 verzoeken per minuut. <br>Zie de [[!DNL User Track] API-documentatie](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) voor meer informatie. |
| [!DNL User Identify] | 20.000 verzoeken per minuut. <br>Zie de [[!DNL User Identify] API-documentatie](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) voor meer informatie. |

>[!NOTE]
>
>Raadpleeg de handleiding op [[!DNL Braze] API-limieten](https://www.braze.com/docs/api/api_limits/) voor nadere bijzonderheden over de beperkingen die zij opleggen .

### Werken met de levenscyclus van het gebruikersprofiel

[!DNL Braze] anonieme gebruikersprofielen maakt met de unieke id; `deviceId`, ingesteld door [!DNL Braze]. Wanneer een gebruiker is geïdentificeerd door een gebruikersnaam op te geven, wordt een geïdentificeerd gebruikersprofiel gemaakt.

In de eerste instantie wordt een `external_id` naar een onbekend gebruikersprofiel, worden alle bestaande gebruikersprofielgegevens en eventuele anonieme gebeurtenissen gemigreerd naar het nieuwe gebruikersprofiel. De anonieme gebruikersprofielen die het zelfde delen `deviceId` zijn ook aliased aan het geïdentificeerde gebruikersprofiel.

[!DNL Braze] worden alle gegevens die aan het profiel met alleen een alias zijn gekoppeld, samengevoegd en behouden. Eventuele volgende anonieme gebruikersgegevens worden echter weeshuis. Zie de [!DNL Braze] documentatiepagina&#39;s op [geïdentificeerde gebruikersprofielen](https://www.braze.com/docs/user_guide/data_and_analytics/user_data_collection/user_profile_lifecycle/#identified-user-profiles) en [best practices voor gegevensverzameling](https://www.braze.com/docs/user_guide/data_and_analytics/user_data_collection/best_practices/#overview) voor meer informatie .

### Billable data points

Extra aangepaste kenmerken verzenden naar [!DNL Braze] kan uw [!DNL Braze] verbruik van gegevenspunten. Raadpleeg uw [!DNL Braze] accountmanager voordat aanvullende aangepaste kenmerken worden verzonden. Zie de [!DNL Braze] documentatie over [factureerbare gegevenspunten](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) voor meer informatie .

### Verzamel vereiste configuratiedetails {#configuration-details}

Als u het Edge-netwerk wilt verbinden met [!DNL Braze]zijn de volgende gegevens vereist:

| Type toets | Beschrijving | Voorbeeld |
| --- | --- | --- |
| [!DNL Braze] Instantie | Het REST-eindpunt is gekoppeld aan het [!DNL Braze] account. Zie de [!DNL Braze] documentatie over [instances](https://www.braze.com/docs/user_guide/administrative/access_braze/braze_instances) ter begeleiding. | `rest.iad-03.braze.com` |
| API-sleutel | De [!DNL Braze] API-sleutel gekoppeld aan de [!DNL Braze] account. <br/>Zie de [!DNL Braze] documentatie over de [REST API-sleutel](https://www.braze.com/docs/api/basics/#rest-api-key) ter begeleiding. | `YOUR-BRAZE-REST-API-KEY` |

## Experience Cloud-voorwaarden

In deze sectie worden de vereiste stappen in Experience Cloud voor alle implementaties beschreven. Afhankelijk van uw individuele implementatiebehoeften kan het nuttig zijn om de volgende constructies in te stellen voordat u de extensie configureert:

1. A [schema](../../../../xdm/schema/composition.md) om de structuur van de gegevens te beschrijven die u in Experience Cloud invoert
1. A [datastream](https://experienceleague.adobe.com/docs/platform-learn/data-collection/event-forwarding/set-up-a-datastream.html) om inkomende gegevens naar aangewezen toepassingen van Adobe Experience Cloud te leiden
1. A [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) om de verzamelde gegevens op te slaan

Voor alle implementaties is het volgende vereist aan de zijde Experience Cloud:

1. [Een geheim maken](#create-a-secret)
1. [Tageigenschappen instellen](#set-up-tag-properties)
1. [Gegevenselementen toevoegen binnen tag-eigenschappen](#add-data-elements-within-tag-properties)
1. [Regels toevoegen binnen eigenschappen van tags](#add-rules-within-tag-properties)

### Een geheim maken

Een nieuwe [gebeurtenis die geheim door:sturen](../../../ui/event-forwarding/secrets.md) en stel de waarde in op uw [[!DNL Braze] API-sleutel](#configuration-details). Hiermee wordt de verbinding met uw account geverifieerd, maar blijft de waarde veilig.

### Tageigenschappen instellen

[Een tag-eigenschap maken](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=en) of kies een bestaande eigenschap die u wilt bewerken. Dit bezit zal worden gevormd om de noodzakelijke gegevensstructuren voor te verzamelen [!DNL Braze] aangezien zij in het Netwerk van de Rand worden gebracht alvorens wordt verzonden gebruikend gebeurtenis door:sturen.

### Gegevenselementen toevoegen binnen tag-eigenschappen

Als uw website de [!DNL Braze] SDK, u moet [een gegevenselement maken](../../../ui/managing-resources/data-elements.md) die het **[!UICONTROL Cookie]** type (verstrekt door [[!UICONTROL Core] tagextensie](../../client/core/overview.md)) zodat de [!DNL Braze] `deviceId` kan uit het cookie worden gelezen.

De **[!UICONTROL Cookie Name]** waarde moet overeenkomen met [!DNL Braze] naam van cookie voor de website. De naam moet een notatie hebben die vergelijkbaar is met `ab.storage.deviceId.{BRAZE_PROJECT_TOKEN_FOR_WEBSITE}`. Selecteren **[!UICONTROL Save]** wanneer gereed.

![data-element deviceid in Tag-eigenschappen.](../../../images/extensions/server/braze/deviceId-data-element.png)

Stel voor het tweede gegevenselement het type in op **[!UICONTROL XDM Object]** (van de [Adobe Experience Platform Web SDK-extensie](../../client/sdk/overview.md)) en deze toewijzen aan het eerder gemaakte schema. Terwijl u de gegevens toewijst, moet u ervoor zorgen dat de waarde van de `deviceId` gegevenselement (dat de [!DNL Braze] `deviceId` De waarde van het cookie) wordt als een waarde in een van uw schemavelden vermeld.

![XDM-objectelement dat deviceId bindt van het cookie naar het schema in Tag-eigenschappen.](../../../images/extensions/server/braze/xdm-object-deviceid.png)

>[!NOTE]
>
>Als uw website niet wordt uitgevoerd, [!DNL Braze] SDK, een Adobe Experience Cloud-id (ECID) wordt gebruikt als fallback `deviceId` waarde die moet worden doorgegeven met de gebeurtenis die wordt verzonden naar [!DNL Braze].

Afhankelijk van uw scenario, kunt u een ander gegevenselement moeten tot stand brengen dat aan de gebeurtenisnaam in het schema kan worden gebruikt in kaart te brengen. Dit kan worden gedaan gebruikend **[!UICONTROL Constant]** door de [!UICONTROL Core] extensie.

![GebeurtenisNameForRegistration voor gegevenselement in tageigenschappen.](../../../images/extensions/server/braze/constant-registration.png)

### Regels toevoegen binnen eigenschappen van tags


De laatste stap voordat u de [!DNL Braze] extensie moet een tag maken [regel](../../../ui/managing-resources/rules.md) (of meerdere tagregels) die worden geactiveerd voor de gebruikersidentificatiegebeurtenissen die worden bijgehouden, zoals logins, aanmeldingsgegevens, registraties enzovoort.

![Een registratieregel in Tageigenschappen.](../../../images/extensions/server/braze/tags-rule-complete.png)

Wanneer het vormen van **[!UICONTROL Events]** voor de regel, selecteer de aangewezen gebeurtenistypen die de regel zullen teweegbrengen. Hieronder ziet u een voorbeeld van een gebeurtenis die de aanmeldingsregel voor een klik door de gebruiker activeert:

![Gebeurtenisconfiguratie voor een aanmeldingsregel in Tageigenschappen.](../../../images/extensions/server/braze/tags-rule-event-config.png)

Tot slot wanneer het selecteren van **[!UICONTROL Actions]** voor de regel selecteert u de optie **[!UICONTROL Send event]** actietype dat door de uitbreiding van SDK van het Web wordt verstrekt. Onder **[!UICONTROL XDM data]**, selecteert u de [!UICONTROL XDM Object] gegevenstype dat u hebt gemaakt [eerder](#add-data-elements-within-tag-properties).

![Configuratie van handeling voor een aanmeldingsregel in Tageigenschappen.](../../../images/extensions/server/braze/tags-rule-action-config.png)

## Installeer en configureer de [!DNL Braze] extension {#install}

Als u de extensie wilt installeren, [een eigenschap voor het doorsturen van gebeurtenissen maken](../../../ui/event-forwarding/overview.md#properties) of kies een bestaande eigenschap die u wilt bewerken.

Selecteren **[!UICONTROL Extensions]** in de linkernavigatie. In de **[!UICONTROL Catalog]** tab, selecteert u **[!UICONTROL Install]** op de kaart voor de [!DNL Braze] extensie.

![Installeer de [!DNL Braze] extensie.](../../../images/extensions/server/braze/install-extension.png)

Voer in het volgende scherm het volgende in [configuratiewaarden](#configuration-details) dat u eerder hebt verzameld van [!DNL Braze]:

* **[!UICONTROL Braze Rest Endpoint URL]**: U kunt de waarde van uw [!DNL Braze] rest eindpunt URL als gewone tekst in de verstrekte input.
* **[!UICONTROL API Key]**: Selecteer [element met geheime gegevens](#create-a-secret) die u eerder hebt gemaakt en die uw [!DNL Braze] API-sleutel.

Selecteren **[!UICONTROL Save]** wanneer gereed.

![De [!DNL Braze] extensieconfiguratiepagina.](../../../images/extensions/server/braze/configure-extension.png)

## Gebeurtenis instellen die gegevenselementen doorstuurt

Na het installeren van en het vormen van de uitbreiding, moet de volgende stap gebeurtenis tot stand brengen die gegevenselementen door:sturen die de noodzakelijke gegevensconstructies zullen vangen die zullen worden verzonden naar [!DNL Braze].

### Een `deviceId` gegevenselement

Als uw site is geconfigureerd met de [!DNL Braze] SDK, dan hebt u al een [element met geheime gegevens](#add-data-elements-within-tag-properties) die de [!DNL Braze] `deviceId` op uw eigenschap tag. Nu moet u opstelling een afzonderlijk gegevenselement onder gebeurtenis door:sturen die aan deze waarde zal richten wanneer het in formaat XDM wordt verzonden.

Selecteer bij het maken van het gegevenselement **[!UICONTROL Core]** voor de extensie selecteert u vervolgens **[!UICONTROL Path]** voor het gegevenstype data. Voer voor de waarde het pad met de puntnotatie in op het `deviceId` in uw schema. Selecteren **[!UICONTROL Save]** wanneer gereed.

![De `devideId` configuratie gegevenselement.](../../../images/extensions/server/braze/ef-data-element.png)

### Een `EventName` gegevenselement

In uw gebeurtenis die bezit door:sturen, creeer een gegevenselement dat gebruikt **[!UICONTROL Path]** tekst uit de **[!UICONTROL Core]** extensie. Voor de waarde voert u het pad met de puntnotatie in op de naam van de gebeurtenis zoals deze in het schema staat.

![De `EventName` configuratie gegevenselement.](../../../images/extensions/server/braze/ef-data-element-2.png)

### Gegevenselementen maken voor gebeurtenissen en aankopen

De [[!DNL Braze User Track] API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) ondersteunt twee afzonderlijke acties: aangepast [gebeurtenissen](https://www.braze.com/docs/api/objects_filters/event_object/#what-is-the-event-object) en [aankopen](https://www.braze.com/docs/api/objects_filters/purchase_object/#what-is-a-purchase-object). De API biedt ook ondersteuning voor [attributes](https://www.braze.com/docs/api/objects_filters/user_attributes_object/) die overeenkomen met [!DNL Braze] gegevenspunten.

De gegevenselementen voor `deviceId` en `EventName` zijn vereist voor zowel aangepaste gebeurtenissen als aankopen, maar er zijn aanvullende gegevenselementen die kunnen worden opgenomen voor beide gebeurtenistypen. Deze worden hieronder weergegeven.

>[!NOTE]
>
>Alle hieronder vermelde gegevenselementen moeten de **[!UICONTROL Path]** typen zodat zij zich kunnen toewijzen aan specifieke velden in uw schema zoals aangegeven in het dialoogvenster **Schemapad** kolom.

#### Aangepaste gebeurtenissen

| [!DNL Braze] key | Schemapad | Beschrijving | Verplicht |
| --- | --- | --- | --- |
| [!DNL Braze] Apparaat-id | `arc.event.xdm._extconndev.brazeDeviceId` | `deviceId` identificeert de gebruiker die de gebeurtenis heeft uitgevoerd. `deviceId` moeten op elk evenement worden gespecificeerd, aangezien het van cruciaal belang is voor [!DNL Braze] om de analyse uit te voeren. | Ja |
| Type gebeurtenis | `arc.event.xdm._extconndev.event_Type` | De naam van de gebeurtenis. | Ja |
| Gebruiker-id | `arc.event.xdm._extconndev.userId` | De e-mail- of aanmeldings-id van de gebruiker, indien beschikbaar. |  |
| Toepassings-id | `arc.event.xdm._extconndev.appId` | Een tekenreeks die aangeeft waar de gebeurtenis is geactiveerd. |  |
| Gebeurtenisvelden | `arc.event.xdm._extconndev.event_Properties` | Een JSON-object dat alle kenmerken van de gebeurtenis vertegenwoordigt. |  |

{style="table-layout:auto"}

#### Aankopen

| [!DNL Braze] key | Schemapad | Beschrijving | Verplicht |
| --- | --- | --- | --- |
| [!DNL Braze] Apparaat-id | `arc.event.xdm._extconndev.brazeDeviceId` | `deviceId` identificeert de gebruiker die de gebeurtenis heeft uitgevoerd. `deviceId` moeten op elk evenement worden gespecificeerd, aangezien het van cruciaal belang is voor [!DNL Braze] om de analyse uit te voeren. | Ja |
| Type gebeurtenis | `arc.event.xdm._extconndev.event_Type` | De naam van de gebeurtenis. | Ja |
| Gebruiker-id | `arc.event.xdm._extconndev.userId` | De e-mail- of aanmeldings-id van de gebruiker, indien beschikbaar. |  |
| Toepassings-id | `arc.event.xdm._extconndev.appId` | Een tekenreeks die aangeeft waar de gebeurtenis is geactiveerd. |  |
| Product-id | `arc.event.xdm._extconndev.product_Id` | Een id voor de aankoop, zoals UPC, ISBN, productcategorie of productnaam. | Ja |
| Valuta | `arc.event.xdm._extconndev.currency` | De voor de aankoop gebruikte valuta, in [ISO 4217-code-indeling](https://www.iso.org/iso-4217-currency-codes.html). | Ja |
| Prijs | `arc.event.xdm._extconndev.price` | De waarde van de aankoop in cijfers. | Ja |
| Aantal | `arc.event.xdm._extconndev.quantity` | De aangekochte hoeveelheid product. | Ja |
| Aanvullende velden | `arc.event.xdm._extconndev.event_Properties` | Een JSON-object dat aanvullende kenmerken over de gebeurtenis vertegenwoordigt. Zie de [[!DNL Braze] documentatie](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) voor details over welke gegevenspunten worden gefactureerd. |  |

{style="table-layout:auto"}

## Regels voor het doorsturen van gebeurtenissen instellen

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis beginnen tot stand te brengen door:sturen regels die bepalen wanneer en hoe uw douanegebeurtenissen en aankopen zullen worden verzonden naar [!DNL Braze].

Aangezien [!DNL Braze User Track] API ondersteunt aangepaste gebeurtenissen en aankopen als twee afzonderlijke handelingen, u moet ten minste twee regels maken zodat [!DNL Braze's] de analyses voor elk van hen kunnen op passende wijze worden benut.

Als gevolg hiervan [!DNL Braze] Met de extensie kunt u de volgende actietypen aan uw regels toevoegen:

* **[!UICONTROL Braze Event]**
* **[!UICONTROL Braze Purchase Event]**

>[!IMPORTANT]
>
>U moet ten minste één regel hebben met een handelingstype van **[!UICONTROL Braze Event]**. Zonder deze regel verzendt het Edge-netwerk geen gebeurtenissen naar [!DNL Braze].

### Een [!DNL Track Event] regel {#tracking-rule}

Begin creërend een nieuwe regel in uw gebeurtenis door:sturen bezit. Onder **[!UICONTROL Conditions]**, voegt u een **[!UICONTROL Value Comparison]** voorwaardetype (verstrekt door [!UICONTROL Core] extensie) om te controleren dat `EventName` is niet `Purchase`. Zo zorgt u ervoor dat de gebeurtenissen met de juiste objectlading naar de [!DNL Braze] API.

![Voeg een gebeurtenis toe die de configuratie van de regelactie door:sturen.](../../../images/extensions/server/braze/ef-rule-condition.png)

Onder **[!UICONTROL Actions]** voegt u een nieuwe handeling toe en stelt u de extensie in op **[!UICONTROL Braze]**. Stel vervolgens het handelingstype in op **[!UICONTROL Braze Event]** om Adobe Experience Edge Network-gebeurtenissen naar [!DNL Braze].

Van hier, moet u in kaart brengen **[!UICONTROL Event Name]** veld naar de binnenkomende eigenschap van de gebeurtenisnaam, en **[!UICONTROL Event Time]**. Andere optionele velden zijn inclusief [!UICONTROL External User ID], [!UICONTROL Braze User ID], [!UICONTROL Alias Label], [!UICONTROL Alias Name], en [!UICONTROL App Identifier].

![Voeg een gebeurtenis toe die de configuratie van de regelactie door:sturen.](../../../images/extensions/server/braze/braze-event-action.png)

>[!NOTE]
>
>De **[!UICONTROL Braze Event]** actie vereist slechts **[!UICONTROL Event Name]** en **[!UICONTROL Event Time]** op te geven, maar u dient zoveel mogelijk informatie op te nemen in de overige velden. Voor meer informatie over de [!DNL Braze] gebeurtenisobject, verwijzen naar de [officiële documentatie](https://www.braze.com/docs/api/objects_filters/event_object/).

Wanneer de [!UICONTROL Braze Event] handeling wordt toegevoegd aan de regel. U kunt ook een **[!UICONTROL Braze Purchase]** actie als de gebeurtenis die u volgt, een aankoopgebeurtenis is. Hieronder ziet u een voorbeeldconfiguratie voor de aankoopactie:

![Voeg een de actietype gebeurtenis toe van het handelingstype van de Aankoop van de Stem door:sturen van de actieconfiguratie van de regelactie.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

>[!NOTE]
>
>Voor meer informatie over de [!DNL Braze] koopobject, verwijzen naar de [officiële documentatie](https://www.braze.com/docs/api/objects_filters/purchase_object/).

De [!DNL Track Event] Deze regel is voltooid en moet er ongeveer zo uitzien als de onderstaande afbeelding. Selecteren **[!UICONTROL Save]** om de regel aan de bibliotheek toe te voegen.

![Voeg een gebeurtenis toe door:sturen regel.](../../../images/extensions/server/braze/track-rule-complete.png)

>[!IMPORTANT]
>
>Als uw website de [!DNL Braze] SDK, kunt u aan de volgende stap van verdergaan [valideren, uw gegevens binnen [!DNL Braze]](#validate). Als u het [!DNL Braze] SDK, u moet [een afzonderlijke regel voor het bijhouden van identiteiten maken](#create-an-identity-tracking-rule) ervoor te zorgen dat passende gebeurtenissen en `deviceId` waarden worden verzonden naar [!DNL Braze] wanneer een gebruikersidentificatie-gebeurtenis plaatsvindt.

### Een regel voor het bijhouden van identiteiten maken

Als u het [!DNL Braze SDK]De volgende stap bestaat uit het maken van een andere regel die gebruikmaakt van zowel de **[!UICONTROL Braze Event]** en **[!UICONTROL Braze Alias]** actietypen. Deze regel zorgt ervoor dat telkens wanneer een gebruikersidentificatiegebeurtenis op de website (zoals login, login, registratie, etc.) voorkomt, de aangewezen gebeurtenissen en `deviceId` waarden worden verzonden naar [!DNL Braze].

Begin bepalend een nieuwe regel om identiteitsgebeurtenissen te volgen. In dit voorbeeld wordt een regel specifiek gedefinieerd voor een registratiegebeurtenis.

Vergelijkbaar met de [!DNL Track Event] regel, onder **[!UICONTROL Conditions]**, inclusief een **[!UICONTROL Value Comparison]** voorwaardetype dat controleert `EventName` equals `Registration`. Dit zorgt ervoor dat deze gebeurtenis alleen wordt geactiveerd voor registratiegebeurtenissen.

![Configuratie van handeling voor [!DNL Braze] actietypen Alias en Identify.](../../../images/extensions/server/braze/ef-registration-condition.png)

Om ervoor te zorgen dat [!DNL Braze] U kunt de gebruikersidentiteiten automatisch samenvoegen, moet u de volgende handelingstypen aan de regel toevoegen, die allebei door worden verstrekt [!DNL Braze] extensie:

* **[!UICONTROL Braze Event]**
* **[!UICONTROL Braze Alias Event]**

Configureer de **[!UICONTROL Braze Event]** op dezelfde manier als de [regel voor bijhouden van gebeurtenissen](#tracking-rule), met inbegrip van zoveel mogelijk informatie op de beschikbare velden.

![De configuratie van [!DNL Braze] Gebeurtenis, actie](../../../images/extensions/server/braze/registration-braze-event.png)

De  **[!UICONTROL Braze Alias Event]** handeling vereist een [gebruikersnaam](https://www.braze.com/docs/api/objects_filters/aliases_to_identify)en u kunt optioneel een [toepassings-id](https://www.braze.com/docs/api/identifier_types/) in voorkomend geval.

![De configuratie van [!DNL Braze] Alias, actie](../../../images/extensions/server/braze/registration-braze-alias.png)

Als beide handelingen aan de regel zijn toegevoegd, selecteert u **[!UICONTROL Save]** om de regel aan uw werkende bibliotheek toe te voegen. Van hieruit kunt u de bibliotheek in een van uw omgevingen samenstellen om te controleren of deze naar behoren functioneert.

![Beide [!DNL Braze] acties worden toegevoegd aan de regel](../../../images/extensions/server/braze/registration-rule-complete.png)

## Gegevens valideren binnen [!DNL Braze] {#validate}

Als de gebeurtenisinzameling en [!DNL Adobe Experience Platform] de integratie is voltooid, u ziet de gebeurtenissen in het [!DNL Braze] console wanneer [gebruikersprofielen weergeven](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). De nieuwe gebeurtenisgegevens die worden verzonden naar [!DNL Braze] wordt weerspiegeld in de [!DNL Purchases] van een bepaalde gebruiker [overzicht, tabblad](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Volgende stappen

In deze handleiding wordt beschreven hoe conversiegebeurtenissen naar [!DNL Braze] het gebruiken van gebeurtenis door:sturen. Voor meer informatie over downstreamtoepassingen voor gebeurtenisgegevens die worden verzonden naar [!DNL Braze], verwijst u naar de [officiële documentatie](https://www.braze.com/docs).

Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar [overzicht van gebeurtenissen doorsturen](../../../ui/event-forwarding/overview.md).