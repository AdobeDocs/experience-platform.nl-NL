---
keywords: gebeurtenis door:sturen uitbreiding;breze;breze gebeurtenis door:sturen uitbreiding
title: Braze Event Forwarding Extension
description: Deze Adobe Experience Platform gebeurtenis die uitbreiding door:sturen verzendt de gebeurtenissen van de Edge Network naar Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---

# [!DNL Braze Track Events API] -gebeurtenis, extensie doorsturen

[[!DNL Braze] &#x200B;](https://www.braze.com) is een platform van de klantenovereenkomst dat klant-centric interactie tussen consumenten en merken in real time drijft. Met [!DNL Braze] kunt u het volgende doen:

- Gegevens (zoals marketingberichten) leveren aan doelgebruikers op basis van hun taalvoorkeur, voorkeur voor locaties en meer, om de conversietarieven te verhogen en belangrijke bedrijfsdoelstellingen te ondersteunen.
- Verzend klanten gepersonaliseerde berichten over veelvoudige kanalen, met inbegrip van e-mail, dupberichten, en in-app berichten, op enkel de juiste tijd en in hun aangewezen talen.
- Doelspecifieke gebruikers voor marketing- en promotiecampagnes om het aantal herhaalde klanten te vergroten.
- Het gebruikersgedrag en de patronen van de studie om specifieke doelgroepen met aangepaste berichten te richten, die zouden kunnen helpen opbrengst verhogen.

De [!DNL Braze Track Events API] [&#x200B; gebeurtenis die &#x200B;](../../../ui/event-forwarding/overview.md) uitbreiding door:sturen staat u toe aan hefboomwerkingsgegevens in de Edge Network van Adobe Experience Platform worden gevangen en verzendt het naar [!DNL Braze] in de vorm van server-zijgebeurtenissen die [[!DNL Braze User Track] &#x200B;](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API gebruiken.

Dit document behandelt de gebruiksgevallen van de uitbreiding, hoe te om het in uw gebeurtenis te installeren die bibliotheken door:sturen, en hoe te om zijn mogelijkheden in een gebeurtenis aan te wenden die [&#x200B; regel &#x200B;](../../../ui/managing-resources/rules.md) door:sturen.

## Gebruiksscenario’s

Deze extensie moet worden gebruikt als u gegevens van de Edge Network in [!DNL Braze] wilt gebruiken om te profiteren van de analysemogelijkheden van de klant en de doelmogelijkheden.

Neem bijvoorbeeld een detailhandelsorganisatie die een multikanaalaanwezigheid (website en mobiel) heeft en die transactie- of gespreksinvoer vastlegt als gebeurtenisgegevens van hun website en mobiele platforms. Gebruikend diverse [&#x200B; markering &#x200B;](../../../home.md) regels, wordt dit gegeven verzonden naar de Edge Network in echt - tijd. Vanaf hier verzendt de [!DNL Braze] -gebeurtenis die de extensie doorstuurt, automatisch relevante gebeurtenissen naar [!DNL Braze] vanaf de serverzijde.

Nadat de gegevens zijn verzonden, kunnen de analyseteams van de organisatie vervolgens gebruikmaken van [!DNL Braze's] -mogelijkheden om de gegevenssets te verwerken en bedrijfsinzichten af te leiden om grafieken, dashboards of andere visualisaties te genereren om zakelijke belanghebbenden te informeren. Verwijs naar de [[!DNL Braze]  klanten &#x200B;](https://www.braze.com/customers) pagina voor meer details van de diverse gebruiksgevallen van het platform.

## [!DNL Braze] voorwaarden en instructies {#prerequisites}

U moet een [!DNL Braze] account hebben om de technologieën ervan te kunnen gebruiken. Als u geen rekening hebt, navigeer aan [&#x200B; krijg Begonnen pagina &#x200B;](https://www.braze.com/get-started/) op [!DNL Braze] om met [!DNL Braze Sales] te verbinden en het proces van de rekeningsverwezenlijking te beginnen.

### API-handleidingen

De extensie gebruikt twee van de API&#39;s van [!DNL Braze] en de bijbehorende beperkingen worden hieronder beschreven:

| API | Snelheidslimieten |
| --- | --- |
| [!DNL User Track] | 50.000 verzoeken per minuut. <br> verwijs naar de [[!DNL User Track]  API documentatie &#x200B;](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) voor details. |
| [!DNL User Identify] | 20.000 verzoeken per minuut. <br> verwijs naar de [[!DNL User Identify]  API documentatie &#x200B;](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) voor details. |

>[!NOTE]
>
> Verwijs naar de gids over [[!DNL Braze]  API grenzen &#x200B;](https://www.braze.com/docs/api/api_limits/) voor verdere details over de grenzen zij opleggen.

### Billable data points

Als u extra aangepaste kenmerken naar [!DNL Braze] verzendt, neemt het verbruik van [!DNL Braze] -gegevenspunten mogelijk toe. Vraag uw accountmanager van [!DNL Braze] om advies voordat u aanvullende aangepaste kenmerken verzendt. Verwijs naar de [!DNL Braze] documentatie over [&#x200B; factureerbare gegevenspunten &#x200B;](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable) voor meer informatie.

### Verzamel vereiste configuratiedetails {#configuration-details}

Als u de Edge Network wilt verbinden met [!DNL Braze] , hebt u de volgende invoeren nodig:

| Type toets | Beschrijving | Voorbeeld |
| --- | --- | --- |
| [!DNL Braze] Instantie | Het REST-eindpunt dat aan de account [!DNL Braze] is gekoppeld. Verwijs naar de [!DNL Braze] documentatie over [&#x200B; instanties &#x200B;](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) voor begeleiding. | `https://rest.iad-03.braze.com` |
| API-sleutel | De API-sleutel van [!DNL Braze] die is gekoppeld aan het [!DNL Braze] -account. <br/> verwijs naar de [!DNL Braze] documentatie over de [&#x200B; REST API sleutel &#x200B;](https://www.braze.com/docs/api/basics/#rest-api-key) voor begeleiding. | `YOUR-BRAZE-REST-API-KEY` |

### Een geheim maken

Creeer een nieuwe [&#x200B; gebeurtenis door:sturen geheim &#x200B;](../../../ui/event-forwarding/secrets.md) en plaats de waarde aan uw [[!DNL Braze]  API Sleutel &#x200B;](#configuration-details). Dit wordt gebruikt om de verbinding met uw account te verifiëren en de waarde veilig te houden.

## De extensie [!DNL Braze] installeren en configureren {#install}

Om de uitbreiding te installeren, [&#x200B; creeer een gebeurtenis door:sturen bezit &#x200B;](../../../ui/event-forwarding/overview.md#properties) of kies een bestaand bezit in plaats daarvan uit te geven.

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie. Selecteer op het tabblad **[!UICONTROL Catalog]** **[!UICONTROL Install]** op de kaart voor de extensie [!DNL Braze] .

![&#x200B; installeer de [!DNL Braze] uitbreiding.](../../../images/extensions/server/braze/install-extension.png)

Op het volgende scherm, input de volgende [&#x200B; configuratiewaarden &#x200B;](#configuration-details) die u eerder van [!DNL Braze] verzamelde:

- **[!UICONTROL Braze Rest Endpoint URL]**: U kunt de waarde van de URL van het [!DNL Braze] rest-eindpunt als onbewerkte tekst invoeren in de opgegeven invoer.
- **[!UICONTROL API Key]**: Selecteer het [&#x200B; geheime gegevenselement &#x200B;](#create-a-secret) dat u vroeger creeerde, dat uw [!DNL Braze] API sleutel bevat.

Selecteer **[!UICONTROL Save]** wanneer u klaar bent.

![&#x200B; de [!DNL Braze] pagina van de uitbreidingsconfiguratie.](../../../images/extensions/server/braze/configure-extension.png)

## Een [!DNL Send Event] -regel maken {#tracking-rule}

Na het installeren van de uitbreiding, creeer een nieuwe gebeurtenis door:sturen [&#x200B; regel &#x200B;](../../../ui/managing-resources/rules.md) en vorm zijn voorwaarden zoals gewenst. Wanneer u de handelingen voor de regel configureert, selecteert u de extensie **[!UICONTROL Braze]** en vervolgens **[!UICONTROL Send Event]** voor het actietype.

![&#x200B; voeg een gebeurtenis toe door:sturen de configuratie van de regelactie.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL User Identification]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL External User ID] | Lang, willekeurig en goed verdeeld UUID of GUID. Als u een andere methode kiest om uw gebruikers-id&#39;s een naam te geven, moeten deze ook lang, willekeurig en goed gedistribueerd zijn. Leer meer over [&#x200B; gesuggereerde gebruiker - identiteitskaart noemende overeenkomst &#x200B;](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze User ID] | Gebruikersidentificatie &#39;Braze&#39;. |
| [!UICONTROL User Alias] | Een alias fungeert als alternatieve unieke gebruikersnaam. Gebruik aliassen om gebruikers met verschillende afmetingen te identificeren dan de gebruikers-id die u als hoofdgebruiker gebruikt. <br><br> Het alias-object voor de gebruiker bestaat uit twee delen: een alias_naam voor de id zelf en een alias_label die het type alias aangeven. Gebruikers kunnen meerdere aliassen met verschillende labels hebben, maar slechts één alias_naam per alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Als u de gebeurtenis aan een gebruiker wilt koppelen, moet u het veld [!UICONTROL External User ID] of het veld [!UICONTROL Braze User Identifier] of de sectie [!UICONTROL User Alias] invullen.

**[!UICONTROL Event Data]**

| Invoer | Beschrijving | Vereist |
| --- | --- | --- |
| [!UICONTROL Event Name &#x200B;] | Naam van de gebeurtenis. | Ja |
| [!UICONTROL Event Time] | Datum en tijd als tekenreeks in ISO 8601 of in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` indeling. | Ja |
| [!UICONTROL App Identifier] | App Identifier of <strong> app_id </strong> is een parameter associerend activiteit met een specifieke app in uw toepassingsgroep. Hiermee wordt aangegeven met welke app in de toepassingsgroep u werkt. Leer meer over de [&#x200B; API herkenningstekenttypes &#x200B;](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Event Properties &#x200B;] | Een JSON-object dat aangepaste eigenschappen van de gebeurtenis bevat. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> De handeling **[!UICONTROL Braze Send Event]** vereist dat alleen een **[!UICONTROL Event Name]** en **[!UICONTROL Event Time]** worden opgegeven, maar u moet zoveel mogelijk informatie opnemen in het veld met aangepaste eigenschappen. Voor details op het [!DNL Braze] gebeurtenisvoorwerp, verwijs naar de [&#x200B; officiële documentatie &#x200B;](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL User Attributes]**

Gebruikerskenmerken kunnen een JSON-object zijn dat velden bevat waarmee een kenmerk met de opgegeven naam en waarde in het opgegeven gebruikersprofiel wordt gemaakt of bijgewerkt. De volgende eigenschappen worden ondersteund:

| Gebruikerskenmerk | Beschrijving |
| --- | --- |
| [!UICONTROL First Name] | |
| [!UICONTROL Last Name] | |
| [!UICONTROL Phone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gender] | Een van de volgende tekenreeksen: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (overige), &quot;N&quot; (niet van toepassing), &quot;P&quot; (niet van toepassing). |
| [!UICONTROL City] | |
| [!UICONTROL Country] | Land als koord in [&#x200B; ISO-3166-1 alpha-2 &#x200B;](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formaat. |
| [!UICONTROL Language] | Taal als koord in [&#x200B; ISO-639-1 &#x200B;](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formaat. |
| [!UICONTROL Date of Birth] | Tekenreeks in de notatie &quot;YYYY-MM-DD&quot; (bijvoorbeeld 1980-12-21). |
| [!UICONTROL Time Zone] | De naam van de tijdzone van [&#x200B; Gegevensbestand van de Tijdzone van IANA &#x200B;](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (b.v., &quot;Amerika/New_York&quot;of &quot;Oost Tijd (V.S. &amp; Canada)&quot;). |
| [!UICONTROL Facebook] | Hash met id (string), like (array of strings), num_friends (integer). |
| [!UICONTROL Twitter] | Hash met id (integer), screen_name (string, Twitter handle), followers_count (integer), friends_count (integer), statuses_count(integer). |

{style="table-layout:auto"}

## Een [!DNL Send Purchase Event] -regel maken {#purchase-rule}

Na het installeren van de uitbreiding, creeer een nieuwe gebeurtenis door:sturen [&#x200B; regel &#x200B;](../../../ui/managing-resources/rules.md) en vorm zijn voorwaarden zoals gewenst. Wanneer u de handelingen voor de regel configureert, selecteert u de extensie **[!UICONTROL Braze]** en vervolgens **[!UICONTROL Send Purchase Event]** voor het actietype.

![&#x200B; voeg een gebeurtenis toe van het actietype van de Aankoop van de Stem het door:sturen van de configuratie van de regelactie.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL User Identification]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL External User ID] | Lang, willekeurig en goed verdeeld UUID of GUID. Als u een andere methode kiest om uw gebruikers-id&#39;s een naam te geven, moeten deze ook lang, willekeurig en goed gedistribueerd zijn. Leer meer over [&#x200B; gesuggereerde gebruiker - identiteitskaart noemende overeenkomst &#x200B;](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze User ID] | Gebruikersidentificatie &#39;Braze&#39;. |
| [!UICONTROL User Alias] | Een alias fungeert als alternatieve unieke gebruikersnaam. Gebruik aliassen om gebruikers met verschillende afmetingen te identificeren dan de gebruikers-id die u als hoofdgebruiker gebruikt. <br><br> Het alias-object voor de gebruiker bestaat uit twee delen: een alias_naam voor de id zelf en een alias_label die het type alias aangeven. Gebruikers kunnen meerdere aliassen met verschillende labels hebben, maar slechts één alias_naam per alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Als u de gebeurtenis aan een gebruiker wilt koppelen, moet u het veld [!UICONTROL External User ID] , het veld [!UICONTROL Braze User Identifier] of de sectie [!UICONTROL User Alias] invullen.

**[!UICONTROL Purchase Data]**

| Invoer | Beschrijving | Vereist |
| --- | --- | --- |
| [!UICONTROL Product ID &#x200B;] | Identificatiecode voor de aankoop. (bv. productnaam of productcategorie) | Ja |
| [!UICONTROL Purchase Time] | Datum en tijd als tekenreeks in ISO 8601 of in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` indeling. | Ja |
| [!UICONTROL Currency &#x200B;] | Valuta als koord in [&#x200B; ISO 4217 &#x200B;](https://en.wikipedia.org/wiki/ISO_4217) Alfabetische formaat van de Code van de Valuta. | Ja |
| [!UICONTROL Price &#x200B;] | Prijs. | Ja |
| [!UICONTROL Quantity &#x200B;] | Indien niet opgegeven, is de standaardwaarde 1. De maximumwaarde moet lager zijn dan 100. | |
| [!UICONTROL App Identifier] | App Identifier of <strong> app_id </strong> is een parameter associerend activiteit met een specifieke app in uw toepassingsgroep. Hiermee wordt aangegeven met welke app in de toepassingsgroep u werkt. Leer meer over de [&#x200B; API herkenningstekenttypes &#x200B;](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Purchase Properties &#x200B;] | Een JSON-object dat aangepaste eigenschappen van de aankoop bevat. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> De handeling **[!UICONTROL Braze Send Event]** vereist dat alleen een **[!UICONTROL Event Name]** en **[!UICONTROL Event Time]** worden opgegeven, maar u moet zoveel mogelijk informatie opnemen in het veld met aangepaste eigenschappen. Voor details op het [!DNL Braze] gebeurtenisvoorwerp, verwijs naar de [&#x200B; officiële documentatie &#x200B;](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL User Attributes]**

Gebruikerskenmerken kunnen een JSON-object zijn dat velden bevat waarmee een kenmerk met de opgegeven naam en waarde in het opgegeven gebruikersprofiel wordt gemaakt of bijgewerkt. De volgende eigenschappen worden ondersteund:

| Gebruikerskenmerk | Beschrijving |
| --- | --- |
| [!UICONTROL First Name] | |
| [!UICONTROL Last Name] | |
| [!UICONTROL Phone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gender] | Een van de volgende tekenreeksen: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (overige), &quot;N&quot; (niet van toepassing), &quot;P&quot; (niet van toepassing). |
| [!UICONTROL City] | |
| [!UICONTROL Country] | Land als koord in [&#x200B; ISO-3166-1 alpha-2 &#x200B;](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formaat. |
| [!UICONTROL Language] | Taal als koord in [&#x200B; ISO-639-1 &#x200B;](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formaat. |
| [!UICONTROL Date of Birth] | Tekenreeks in de notatie &quot;YYYY-MM-DD&quot; (bijvoorbeeld 1980-12-21). |
| [!UICONTROL Time Zone] | De naam van de tijdzone van [&#x200B; Gegevensbestand van de Tijdzone van IANA &#x200B;](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (b.v., &quot;Amerika/New_York&quot;of &quot;Oost Tijd (V.S. &amp; Canada)&quot;). |
| [!UICONTROL Facebook] | Hash met id (string), like (array of strings), num_friends (integer). |
| [!UICONTROL Twitter] | Hash met id (integer), screen_name (string, Twitter handle), followers_count (integer), friends_count (integer), statuses_count(integer). |

{style="table-layout:auto"}

## Gegevens valideren binnen [!DNL Braze] {#validate}

Als de gebeurtenisinzameling en [!DNL Adobe Experience Platform] integratie succesvol waren, zult u gebeurtenissen binnen de [!DNL Braze] console zien wanneer [&#x200B; het bekijken gebruikersprofielen &#x200B;](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Specifiek, worden de nieuwe gebeurtenisgegevens die naar [!DNL Braze] worden verzonden weerspiegeld in de [!DNL Purchases] sectie van het 2&rbrace; overzicht tabel van een bepaalde gebruiker [&#128279;](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Volgende stappen

In deze handleiding wordt beschreven hoe conversiegebeurtenissen naar [!DNL Braze] kunnen worden verzonden via het doorsturen van gebeurtenissen. Voor meer details op stroomafwaartse toepassingen voor gebeurtenisgegevens die naar [!DNL Braze] worden verzonden, verwijs naar de [&#x200B; officiële documentatie &#x200B;](https://www.braze.com/docs).

Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar de [&#x200B; gebeurtenis die overzicht &#x200B;](../../../ui/event-forwarding/overview.md) door:sturen.
