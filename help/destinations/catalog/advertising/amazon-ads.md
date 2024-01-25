---
title: Amazon Adds
description: Amazon Ads biedt verschillende opties om geregistreerde verkopers, verkopers, verkopers van boeken, Kindle Direct Publishing-auteurs (KDP), ontwikkelaars van apps en/of bureaus te helpen uw reclamedoelstellingen te bereiken. De integratie van Amazon Ads met Adobe Experience Platform biedt kant-en-klare integratie voor Amazon Ads-producten, waaronder de Amazon DSP (ADSP). Met de Amazon Ads-bestemming in Adobe Experience Platform kunnen gebruikers adverteerdersoorten definiëren voor doelwitten en activering op de Amazon-DSP.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 1%

---

# (bèta) Amazon Ads-verbinding {#amazon-ads}

## Overzicht {#overview}

Amazon Ads biedt verschillende opties om geregistreerde verkopers, verkopers, verkopers van boeken, Kindle Direct Publishing-auteurs (KDP), ontwikkelaars van apps en/of bureaus te helpen uw reclamedoelstellingen te bereiken.

De integratie van Amazon Ads met Adobe Experience Platform biedt kant-en-klare integratie voor Amazon Ads-producten, waaronder de Amazon DSP (ADSP). Met de Amazon Ads-bestemming in Adobe Experience Platform kunnen gebruikers adverteerdersoorten definiëren voor doelwitten en activering op de Amazon-DSP.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door *Amazon Adds* team. Dit is momenteel een bètaproduct en de functionaliteit kan worden gewijzigd. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *`amc-support@amazon.com`.*

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het *Amazon Adds* doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Activering en doelversie {#activation-and-targeting}

Dankzij deze integratie met Amazon DSP kunnen adverteerders van Amazon Ads CDP-advertenties doorgeven van Adobe Experience Platform naar Amazon DSP om adverteerders aan te zetten voor reclamedoeleinden. In de Amazon-DSP kunnen doelgroepen worden geselecteerd voor positieve doelgerichtheid en voor negatieve doelgerichtheid (onderdrukking).

## Vereisten {#prerequisites}

Als u de Amazon Ads-verbinding met Adobe Experience Platform wilt gebruiken, moeten gebruikers eerst toegang hebben tot een Amazon DSP Advertiser-account. Ga naar de volgende pagina op de website Amazon Ads om deze instanties op te geven:

* [Aan de slag met Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## Ondersteunde identiteiten {#supported-identities}

De *Amazon Adds* De verbinding steunt de activering van identiteiten die in de hieronder lijst worden beschreven. Meer informatie over [identiteiten](/help/identity-service//features/namespaces.md). Ga voor meer informatie over de identiteiten die worden ondersteund door Amazon Ads naar de [Amazon DSP Ondersteuningscentrum](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster *Amazon Adds* bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

U gaat naar de Amazon Ads-verbindingsinterface waar u eerst de adverteerderaccounts selecteert waarmee u verbinding wilt maken. Als er verbinding is, wordt u weer omgeleid naar Adobe Experience Platform met een nieuwe verbinding, die wordt geleverd met de id van het door u geselecteerde Advertiser-account. Selecteer de juiste Advertiser-account op het scherm met de doelconfiguratie om door te gaan.

* **[!UICONTROL Bearer token]**: Vul het token van de gebruiker in om te verifiëren bij de bestemming.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Amazon Ads Advertiser ID]**: Selecteer de id voor de Amazon Ads-doelaccount die voor de bestemming wordt gebruikt.

>[!NOTE]
>
>Nadat u de doelconfiguratie hebt opgeslagen, kunt u de Adobe Advertiser-id voor Amazon Ads niet meer wijzigen, zelfs niet als u de verificatie opnieuw uitvoert via uw Amazon-account. Als u een andere advertentie-ID voor Amazon Ads wilt gebruiken, moet u een nieuwe doelverbinding maken.

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

De Amazon Ads-verbinding biedt ondersteuning voor gehashte e-mailadressen en gehashte telefoonnummers voor overeenstemmende identiteiten. De onderstaande schermafbeelding biedt een voorbeeld dat overeenkomt met de Amazon Ads-verbinding:

![Toewijzing van Adobe aan Amazon-advertenties](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Als u gehashte e-mailadressen wilt toewijzen, selecteert u de optie `Email_LC_SHA256` naamruimte van identiteit als bronveld.
* Als u gehashte telefoonnummers wilt toewijzen, selecteert u de optie `Phone_SHA256` naamruimte van identiteit als bronveld.
* Als u niet-gehashte e-mailadressen of telefoonnummers wilt toewijzen, selecteert u de bijbehorende naamruimten als bronvelden en controleert u de `Apply Transformation` als u wilt dat Platform de identiteiten bij activering verbergt.

U wordt ten zeerste aangeraden om zoveel velden in kaart te brengen als u hebt. Als er slechts één bronkenmerk beschikbaar is, kunt u één veld toewijzen. Het doel Amazon Ads gebruikt alle toegewezen velden voor toewijzingsdoeleinden, wat hogere overeenkomende snelheden oplevert als er meer velden zijn opgegeven. Ga voor meer informatie over de geaccepteerde id&#39;s naar de [Amazon Advertentiepagina met gehakte doelgroepen](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat u het publiek hebt geüpload, kunt u controleren of het publiek correct is gemaakt en geüpload door de volgende stappen uit te voeren:

**Voor Amazon DSP**

Navigeer naar uw advertentie-id → Soorten publiek → Advertiser-soorten. Als uw publiek met succes is gemaakt en aan het minimale aantal publieksleden voldoet, wordt de status `Active`. Meer informatie over de grootte en het bereik van uw publiek vindt u in het deelvenster Voorspeld Bereik aan de rechterkant van de gebruikersinterface van Amazon DSP.

![Validatie voor het maken van Amazon-DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Raadpleeg de volgende Help-bronnen voor Amazon Ads voor aanvullende Help-documentatie:

* [Amazon DSP Help Center](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Mei 2023 | Bijwerken van functionaliteit en documentatie | <ul><li>Toegevoegde ondersteuning voor selectie van advertentiegebied in het dialoogvenster [workflow voor doelverbinding](#destination-details).</li><li>Bijgewerkte documentatie waarin de toevoeging van de selectie van het advertentiegebied wordt weergegeven. Raadpleeg voor meer informatie over het selecteren van het juiste gebied Advertiser de [Amazon-documentatie](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Maart 2023 | Eerste release | Eerste doelversie en documentatie gepubliceerd. |

{style="table-layout:auto"}

+++
