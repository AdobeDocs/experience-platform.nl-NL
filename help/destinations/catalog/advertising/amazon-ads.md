---
title: Amazon Adds
description: Amazon Ads biedt verschillende opties om geregistreerde verkopers, verkopers, verkopers van boeken, Kindle Direct Publishing-auteurs (KDP), ontwikkelaars van apps en/of bureaus te helpen uw reclamedoelstellingen te bereiken. De integratie van Amazon Ads met Adobe Experience Platform biedt kant-en-klare integratie voor Amazon Ads-producten, waaronder de Amazon DSP (ADSP). Met de Amazon Ads-bestemming in Adobe Experience Platform kunnen gebruikers adverteerdersoorten definiëren voor doelwitten en activering op de Amazon DSP.
last-substantial-update: 2025-01-07T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1771'
ht-degree: 1%

---

# Amazon Ads-verbinding {#amazon-ads}

## Overzicht {#overview}

[!DNL Amazon Ads] biedt een aantal opties waarmee u uw reclamedoelstellingen kunt bereiken voor geregistreerde verkopers, verkopers, boekverkopers, Kindle Direct Publishing-auteurs (KDP), ontwikkelaars van apps en/of agentschappen.

De [!DNL Amazon Ads] -integratie met Adobe Experience Platform biedt kant-en-klare integratie voor [!DNL Amazon Ads] -producten, waaronder de Amazon DSP (ADSP) en Amazon Marketing Cloud (AMC).

Met de [!DNL Amazon Ads] -bestemming in Adobe Experience Platform kunnen gebruikers adverteerdersoorten definiëren voor activering en doelversie op de Amazon DSP.  Bovendien kunnen gebruikers hun gegevens uploaden naar [!DNL Amazon Marketing Cloud] om de prestaties per publiek te begrijpen, door adverteerders opgegeven dimensies, het lidmaatschap van Amazon-segmenten of andere signalen die beschikbaar zijn in AMC. Na het uploaden van adverteerders naar AMC, kunnen gebruikers [!DNL Amazon Marketing Cloud] gebruiken om leden van het publiek te wijzigen, te verbeteren of toe te voegen met Amazon-signalen vanuit [!DNL Amazon Marketing Cloud] .

AMC verenigt unieke signalen van Amazon-eigendommen en -bediende eigenschappen die zich uitstrekken over verschillende media, waaronder display, video, streaming TV, audio en gesponsorde advertenties. Gebruikers kunnen eenvoudig curated segments van Adobe Experience Platform naar AMC verzenden om het leren te verbeteren, zoals in-market groepen van het publiek, levensstijlcohorten en merkbetrokkenheidspatronen. De Augmented segmenten kunnen dan worden gebruikt om media activering in Amazon DSP te optimaliseren.

>[!IMPORTANT]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van *[!DNL Amazon Ads]* . Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *`amc-support@amazon.com`.*

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de *[!DNL Amazon Ads]* bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Activering en doelversie {#activation-and-targeting}

Dankzij deze integratie met Amazon DSP kunnen [!DNL Amazon Ads] -adverteerders CDP-advertenties doorgeven van Adobe Experience Platform naar Amazon DSP om adverteerders te maken die adverteerders promoten. In de Amazon DSP kunnen doelgroepen worden geselecteerd voor positieve doelgerichtheid en voor negatieve doelgerichtheid (onderdrukking).

### Analyse en meting {#analytics-and-measurement}

Dankzij deze integratie met [!DNL Amazon Marketing Cloud] (AMC) kunnen [!DNL Amazon Ads] -adverteerders CDP-segmenten doorgeven van het Adobe Experience Platform-formulier naar AMC. Adverteerders kunnen zich dan bij de CDP-invoer aansluiten met [!DNL Amazon Ads] signalen en aangepaste analyses uitvoeren over onderwerpen zoals mediakrukken, publiekssegmenten en klantritten in privacyconforme indeling. Een adverteerder kan bijvoorbeeld een lijst met zijn bestaande klanten uploaden om inzicht te krijgen in de geaggregeerde prestaties van advertentiecampagnes, of geaggregeerde statistieken van conversiegebeurtenissen in Amazon, zoals het weergeven van een productdetailpagina, het toevoegen van een product aan een winkelwagentje of de aankoop van een product.

### Advertising optimaliseren

Dankzij deze integratie met [!DNL Amazon Marketing Cloud] (AMC) kunnen adverteerders hun eigen klantlijsten uploaden en met [!DNL Amazon Marketing Cloud] SQL overlappende analyses, onderdrukkingen, toevoegingen of optimalisaties voor het publiek uitvoeren op een terugkerende basis voordat ze een publiek maken dat klaar is voor activering in Amazon DSP voor het opgeven van doelen.

## Vereisten {#prerequisites}

Als u de [!DNL Amazon Ads] -verbinding met Adobe Experience Platform wilt gebruiken, moeten gebruikers eerst toegang hebben tot een Amazon DSP Advertiser-account of een [!DNL Amazon Marketing Cloud] -instantie. Ga naar de volgende pagina op de [!DNL Amazon Ads] -website om deze instanties op te geven:

* [ worden begonnen met Amazon DSP ](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [ worden begonnen met Amazon Marketing Cloud ](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Ondersteunde identiteiten {#supported-identities}

De *[!DNL Amazon Ads]* -verbinding ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service//features/namespaces.md). Voor meer details over de identiteiten die door [!DNL Amazon Ads] worden gesteund, bezoek het [ Centrum van de Steun van DSP van Amazon ](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de *[!DNL Amazon Ads]* -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

U gaat naar de verbindingsinterface van [!DNL Amazon Ads] waar u eerst de adverteerderaccounts selecteert waarmee u verbinding wilt maken. Als er verbinding is, wordt u weer omgeleid naar Adobe Experience Platform met een nieuwe verbinding, die wordt geleverd met de id van het door u geselecteerde Advertiser-account. Selecteer de juiste Advertiser-account op het scherm met de doelconfiguratie om door te gaan.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Amazon Ads Connection]**: selecteer de id voor de doelaccount van [!DNL Amazon Ads] die voor de bestemming wordt gebruikt.

>[!NOTE]
>
>Nadat u de doelconfiguratie hebt opgeslagen, kunt u de [!DNL Amazon Ads] Advertiser-id niet meer wijzigen, zelfs niet als u de verificatie opnieuw uitvoert via uw Amazon-account. Als u een andere [!DNL Amazon Ads] Advertiser-id wilt gebruiken, moet u een nieuwe doelverbinding maken. Adverteerders die al zijn ingesteld op een integratie met ADSP moeten een nieuwe doelstroom maken als zij willen dat hun publiek wordt geleverd aan AMC of aan een andere ADSP-account.

* **[!UICONTROL Advertiser Region]**: selecteer het juiste gebied waarin uw adverteerder wordt gehost. Voor meer informatie over de markten die door elk gebied worden gesteund, bezoek de [ documentatie van Amazon Ads ](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).

* **[!UICONTROL Amazon Ads Consent Signal]**: Bevestig dat alle gegevens die via deze verbinding worden verzonden, hebben ingestemd met het gebruik van persoonsgegevens voor reclamedoeleinden. &quot;GRANTED&quot; geeft aan dat Amazon ermee instemt de persoonsgegevens van de klant te gebruiken voor reclame. De toegestane waarden zijn &quot;GRANTED&quot; en &quot;DENIED&quot;. Alle records die via verbindingen met &quot;DENIED&quot; worden verzonden, worden geweigerd voor verder gebruik in Amazon Ads.

![ vorm nieuwe bestemming ](../../assets/catalog/advertising/amazon-ads/amazon_ads_consent_input.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

De verbinding van [!DNL Amazon Ads] steunt gehakt e-mailadres en gehashte telefoonaantallen voor overeenstemmende identiteit. In de onderstaande schermafbeelding ziet u een voorbeeld dat overeenkomt met de [!DNL Amazon Ads] -verbinding:

![ Adobe aan de afbeelding van Advertenties van Amazon ](../../assets/catalog/advertising/amazon-ads/amazon_ads_image_2.png)

* Als u gehashte e-mailadressen wilt toewijzen, selecteert u de naamruimte `Email_LC_SHA256` identity als bronveld.
* Als u gehashte telefoonnummers wilt toewijzen, selecteert u de naamruimte `Phone_SHA256` identity als bronveld.
* Als u ongehashte e-mailadressen of telefoonnummers wilt toewijzen, selecteert u de bijbehorende naamruimten als bronvelden en schakelt u de optie `Apply Transformation` in om Experience Platform de identiteiten bij activering te laten hashen.
* *NIEUW die met de versie van September 2024* begint: Amazon Ads vereist u om een gebied in kaart te brengen dat een `countryCode` waarde in het 2 karakterISO formaat bevat om het proces van de identiteitsresolutie (bijvoorbeeld: US, GB, MX, CA, etc.) te vergemakkelijken. Verbindingen zonder `countryCode` toewijzingen hebben een negatief effect op overeenkomende identiteiten.

U selecteert slechts één keer een bepaald doelgebied in een bestemmingsconfiguratie van de [!DNL Amazon Ads] schakelaar.  Als u bijvoorbeeld bedrijfs-e-mail verzendt, kunt u persoonlijke e-mail niet ook toewijzen in dezelfde doelconfiguratie.

U wordt ten zeerste aangeraden om zoveel velden in kaart te brengen als u hebt. Als er slechts één bronkenmerk beschikbaar is, kunt u één veld toewijzen. Het doel [!DNL Amazon Ads] gebruikt alle toegewezen velden voor toewijzingsdoeleinden, wat hogere overeenkomende snelheden oplevert als er meer velden zijn opgegeven. Voor meer informatie over de toegelaten herkenningstekens, bezoek de [ Amazon Ads hakte pagina van de publiekshulp ](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat u het publiek hebt geüpload, kunt u controleren of het publiek correct is gemaakt en geüpload door de volgende stappen uit te voeren:

**voor Amazon DSP**

Navigeer naar uw **[!UICONTROL Advertiser ID]** > **[!UICONTROL Audiences]** > **[!UICONTROL Advertiser Audiences]** . Als het publiek is gemaakt en het minimale aantal publieksleden bereikt, wordt de status `Active` weergegeven. Meer informatie over de grootte en het bereik van uw publiek vindt u in het deelvenster Voorspelde resultaten rechts van de Amazon DSP-gebruikersinterface.

![ de bevestiging van de het publieksverwezenlijking van Amazon DSP ](../../assets/catalog/advertising/amazon-ads/amazon_ads_image_3.png)

**Voor[!DNL Amazon Marketing Cloud]**

Zoek in de linkerschemabrowser naar uw publiek onder **[!UICONTROL Advertiser Uploaded]** > **[!UICONTROL aep_audiences]** . U kunt dan uw publiek in de SQL redacteur van AMC met de volgende clausule vragen:

`select count(user_id) from adobeexperienceplatf_audience_view_000xyz where external_audience_segment_name = '1234567'`

![ de bevestiging van de het publieksverwezenlijking van Amazon Marketing Cloud ](../../assets/catalog/advertising/amazon-ads/amazon_ads_image_5.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Raadpleeg de volgende [!DNL Amazon Ads] Help-bronnen voor aanvullende Help-documentatie:

* [ Amazon DSP Help Center ](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Februari 2025 | De vereiste om **[!UICONTROL Amazon Ads Consent Signal]** toe te voegen aan het exporteren van gegevens is toegevoegd en de bestemming van bèta naar algemeen beschikbaar bevorderd. |
| Mei 2024 | Bijwerken van functionaliteit en documentatie | De toewijzingsoptie voor het exporteren van de parameter `countryCode` naar Amazon Ads is toegevoegd. Gebruik `countryCode` in de [toewijzingsstap](#map) om uw afstemmingspercentages voor identiteiten met Amazon te verbeteren. |
| Maart 2024 | Bijwerken van functionaliteit en documentatie | De optie voor het exporteren van soorten publiek die in [!DNL Amazon Marketing Cloud] (AMC) moeten worden gebruikt, is toegevoegd. |
| Mei 2023 | Bijwerken van functionaliteit en documentatie | <ul><li>Toegevoegde steun voor de selectie van het Gebied Advertiser in het [ werkschema van de bestemmingsverbinding ](#destination-details).</li><li>Bijgewerkte documentatie waarin de toevoeging van de selectie van het advertentiegebied wordt weergegeven. Voor meer informatie bij het selecteren van het correcte Gebied Advertiser, zie de [ documentatie van Amazon ](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Maart 2023 | Eerste release | Eerste doelversie en documentatie gepubliceerd. |

{style="table-layout:auto"}

+++
