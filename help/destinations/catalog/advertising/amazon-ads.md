---
title: Amazon Adds
description: Amazon Ads biedt verschillende opties om geregistreerde verkopers, verkopers, verkopers van boeken, Kindle Direct Publishing-auteurs (KDP), ontwikkelaars van apps en/of bureaus te helpen uw reclamedoelstellingen te bereiken. De integratie van Amazon Ads met Adobe Experience Platform biedt kant-en-klare integratie voor Amazon Ads-producten, waaronder de Amazon DSP (ADSP). Met de Amazon Ads-bestemming in Adobe Experience Platform kunnen gebruikers adverteerdersoorten definiëren voor doelwitten en activering op de Amazon-DSP.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 24f7463f7005f77f8d93e7cb2c04efc0fb4e3a0b
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 1%

---

# (bèta) Amazon Ads-verbinding {#amazon-ads}

## Overzicht {#overview}

[!DNL Amazon Ads] biedt een aantal opties om u te helpen uw reclamedoelstellingen te bereiken aan geregistreerde verkopers, verkopers, boekverkopers, auteurs van Kindle Direct Publishing (KDP), toepassingsontwikkelaars, en/of agentschappen.

De [!DNL Amazon Ads] integratie met Adobe Experience Platform biedt een sleutelintegratie voor [!DNL Amazon Ads] producten, waaronder de Amazon DSP (ADSP) en Amazon Marekting Cloud (AMC).

Met de [!DNL Amazon Ads] in Adobe Experience Platform kunnen gebruikers adverteerderspubliek definiëren voor activering en doelwittering op de Amazon-DSP.  Bovendien kunnen gebruikers hun gegevens uploaden naar [!DNL Amazon Marketing Cloud] om de prestaties van het publiek te begrijpen, heeft adverteerder afmetingen, lidmaatschap in Amazon-segmenten of andere signalen in AMC verstrekt. Na het uploaden van adverteerders naar AMC kunnen gebruikers [!DNL Amazon Marketing Cloud] om te wijzigen, te verbeteren, of toe te voegen aan publieksleden die de signalen van Amazon van binnen gebruiken [!DNL Amazon Marketing Cloud].

AMC verenigt unieke signalen van Amazon-eigendommen en -bediende eigenschappen die zich uitstrekken over verschillende media, waaronder display, video, streaming TV, audio en gesponsorde advertenties. Gebruikers kunnen eenvoudig curated segments van Adobe Experience Platform naar AMC verzenden om het leren te verbeteren, zoals in-market groepen van het publiek, levensstijlcohorten en merkbetrokkenheidspatronen. De gebogen segmenten kunnen dan worden gebruikt om media activering in de DSP van Amazon te optimaliseren.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door *[!DNL Amazon Ads]* team. Dit is momenteel een bètaproduct en de functionaliteit kan worden gewijzigd. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *`amc-support@amazon.com`.*

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het *[!DNL Amazon Ads]* doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Activering en doelversie {#activation-and-targeting}

Dankzij deze integratie met Amazon DSP [!DNL Amazon Ads] adverteerders die CDP-advertenties van Adobe Experience Platform aan Amazon doorgeven, DSP adverteerders een adverteerderspubliek voor reclamedoeleinden te creëren. In de Amazon-DSP kunnen doelgroepen worden geselecteerd voor positieve doelgerichtheid en voor negatieve doelgerichtheid (onderdrukking).

### Analyse en meting {#analytics-and-measurement}

Deze integratie met [!DNL Amazon Marketing Cloud] (AMC) staat [!DNL Amazon Ads] adverteerders om CDP-segmenten door te geven van Adobe Experience Platform-formulier naar AMC. Adverteerders kunnen zich dan bij de CDP-invoer aansluiten met [!DNL Amazon Ads] signalen, en voer douaneanalyses op onderwerpen zoals media effect, publiekssegmenten, en klantenreizen in privacy volgzaam formaat uit. Een adverteerder kan bijvoorbeeld een lijst met zijn bestaande klanten uploaden om inzicht te krijgen in de geaggregeerde prestaties van advertentiecampagnes, of geaggregeerde statistieken van conversiegebeurtenissen in Amazon, zoals het weergeven van een productdetailpagina, het toevoegen van een product aan een winkelwagentje of de aankoop van een product.

### Optimalisatie van reclame:

Deze integratie met [!DNL Amazon Marketing Cloud] (AMC) stelt adverteerders in staat hun eigen klantlijsten te uploaden en [!DNL Amazon Marketing Cloud] SQL, voer overlappende analyse, onderdrukking, toevoegingen, of optimalisering aan publiek in een terugkomende basis uit alvorens een activering-klaar publiek in de DSP van Amazon voor het richten te creëren.

## Vereisten {#prerequisites}

Als u de opdracht [!DNL Amazon Ads] gebruikers eerst toegang hebben tot een Amazon DSP Advertiser-account of een [!DNL Amazon Marketing Cloud] -instantie. Ga naar de volgende pagina op de [!DNL Amazon Ads] website:

* [Aan de slag met Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Aan de slag met Amazon-Marketing Cloud](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Ondersteunde identiteiten {#supported-identities}

De *[!DNL Amazon Ads]* De verbinding steunt de activering van identiteiten die in de hieronder lijst worden beschreven. Meer informatie over [identiteiten](/help/identity-service//features/namespaces.md). Voor meer informatie over de identiteiten die worden ondersteund door [!DNL Amazon Ads], bezoek de [Amazon DSP Ondersteuningscentrum](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster *[!DNL Amazon Ads]* bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

U wordt naar de [!DNL Amazon Ads] verbindingsinterface waarin u eerst de adverteerderaccounts selecteert waarmee u verbinding wilt maken. Als er verbinding is, wordt u weer omgeleid naar Adobe Experience Platform met een nieuwe verbinding, die wordt geleverd met de id van het door u geselecteerde Advertiser-account. Selecteer de juiste Advertiser-account op het scherm met de doelconfiguratie om door te gaan.

* **[!UICONTROL Bearer token]**: Vul het token van de gebruiker in om te verifiëren bij de bestemming.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Amazon Ads Connection]**: Selecteer de id voor het doel [!DNL Amazon Ads] voor de bestemming wordt gebruikt.

>[!NOTE]
>
>Nadat u de doelconfiguratie hebt opgeslagen, kunt u de [!DNL Amazon Ads] Adverteerder-id, zelfs als u opnieuw verifieert via uw Amazon-account. Een andere [!DNL Amazon Ads] Advertiser-id. U moet een nieuwe doelverbinding maken.

* **[!UICONTROL Advertiser Region]**: Selecteer het juiste gebied waarin uw adverteerder wordt gehost. Ga voor meer informatie over de markten die door elke regio worden ondersteund naar de [Amazon Ads-documentatie](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Nieuwe bestemming configureren](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

De [!DNL Amazon Ads] De verbinding steunt gehakt e-mailadres en gehashte telefoonaantallen voor identiteit passende doeleinden. De onderstaande schermafbeelding biedt een voorbeeld dat overeenkomt met de [!DNL Amazon Ads] verbinding:

![Toewijzing van Adobe aan Amazon-advertenties](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Als u gehashte e-mailadressen wilt toewijzen, selecteert u de optie `Email_LC_SHA256` naamruimte van identiteit als bronveld.
* Als u gehashte telefoonnummers wilt toewijzen, selecteert u de optie `Phone_SHA256` naamruimte van identiteit als bronveld.
* Als u niet-gehashte e-mailadressen of telefoonnummers wilt toewijzen, selecteert u de bijbehorende naamruimten als bronvelden en controleert u de `Apply Transformation` als u wilt dat Platform de identiteiten bij activering verbergt.

U selecteert slechts één keer een bepaald doelgebied in een bestemmingsconfiguratie van [!DNL Amazon Ads] -aansluiting.  Als u bijvoorbeeld bedrijfs-e-mail verzendt, kunt u persoonlijke e-mail niet ook toewijzen in dezelfde doelconfiguratie.

U wordt ten zeerste aangeraden om zoveel velden in kaart te brengen als u hebt. Als er slechts één bronkenmerk beschikbaar is, kunt u één veld toewijzen. De [!DNL Amazon Ads] het doel gebruikt alle in kaart gebrachte gebieden voor kaartdoeleinden, die hogere gelijke tarieven opleveren als meer gebieden worden verstrekt. Ga voor meer informatie over de geaccepteerde id&#39;s naar de [Amazon Advertentiepagina met gehakte doelgroepen](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat u het publiek hebt geüpload, kunt u controleren of het publiek correct is gemaakt en geüpload door de volgende stappen uit te voeren:

**Voor Amazon DSP**

Ga naar uw **[!UICONTROL Advertiser ID]** > **[!UICONTROL Audiences]** > **[!UICONTROL Advertiser Audiences]**. Als uw publiek met succes is gemaakt en aan het minimale aantal publieksleden voldoet, wordt de status `Active`. Meer informatie over de grootte en het bereik van uw publiek vindt u in het deelvenster Voorspeld Bereik aan de rechterkant van de gebruikersinterface van Amazon DSP.

![Validatie voor het maken van Amazon-DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

**Voor[!DNL Amazon Marketing Cloud]**

Zoek in de linkerschemabrowser uw publiek onder **[!UICONTROL Advertiser Uploaded]** > **[!UICONTROL aep_audiences]**. U kunt dan uw publiek in de SQL redacteur van AMC met de volgende clausule vragen:

`select count(user_id) from aep_audiences where audienceId = '1234567'`

![Validatie voor het maken van publiek voor Amazon-Marketingen Cloud](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Ga voor aanvullende Help-documentatie naar [!DNL Amazon Ads] Help-bronnen:

* [Amazon DSP Help Center](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Februari 2024 | Bijwerken van functionaliteit en documentatie | De optie voor het exporteren van soorten publiek toegevoegd voor gebruik in [!DNL Amazon Marketing Cloud] (AMC). |
| Mei 2023 | Bijwerken van functionaliteit en documentatie | <ul><li>Toegevoegde ondersteuning voor selectie van advertentiegebied in het dialoogvenster [workflow voor doelverbinding](#destination-details).</li><li>Bijgewerkte documentatie waarin de toevoeging van de selectie van het advertentiegebied wordt weergegeven. Raadpleeg voor meer informatie over het selecteren van het juiste gebied Advertiser de [Amazon-documentatie](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Maart 2023 | Eerste release | Eerste doelversie en documentatie gepubliceerd. |

{style="table-layout:auto"}

+++
