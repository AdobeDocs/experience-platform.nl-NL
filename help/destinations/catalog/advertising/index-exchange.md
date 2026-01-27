---
title: Index Exchange
description: Verbind met de Uitwisseling van de Index (Index) en activeer uw gegevens zodat uw publiekssegmenten door overeenkomsten kunnen worden gericht die in de UI van de Index worden gecreeerd.
source-git-commit: 4ecd3b60a6b45a94285785049fd4dee99d7c9bdf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---


# [!DNL Index Exchange] {#index-exchange}

## Overzicht {#overview}

[!DNL Index] is een wereldwijd advertentieplatform dat media-eigenaars helpt de waarde van hun inhoud op elk scherm te maximaliseren. Met meer dan 20 jaar toonaangevend in de branche verbindt [!DNL Index] de grootste merken ter wereld met toonaangevende ervaren makers om hoogwaardige consumentenervaringen te bieden.

Gebruik deze bestemmingsschakelaar om publiekssegmenten van Adobe Experience Platform rechtstreeks naar het programmatic reclameplatform van [!DNL Index Exchange] uit te voeren.

Zodra uitgevoerd, kunnen deze publiekssegmenten worden gebruikt om overeenkomsten door media eigenaars, marktplaatspartners, of met uitgevers en curators door marktplaatsverkopers te richten die worden gedeeld.

>[!IMPORTANT]
>
>De doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Index] . Voor vragen of updateverzoeken, contacteer hen direct in [&#x200B; technical_am_marketplace@indexexchange.com &#x200B;](mailto:technical_am_marketplace@indexexchange.com).

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Index Exchange] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Experience Platform door deze bestemming kunnen oplossen.

### Gebruikers richten op mobiele, web- en CTV-platforms {#targeting-users}

Mediaeigenaren, marketingpartners of leveranciers van markten die een publiek van Experience Platform naar [!DNL Index] willen sturen om gebruikers op mobiele, web- en CTV-platforms als doelgroep te kiezen, met behulp van een groot aantal verschillende id&#39;s.

### Specifieke inhoud richten op mobiele, web- en CTV-platforms {#targeting-content}

Mediaeigenaren, marketingpartners of leveranciers van marketinglocaties die een publiek van Experience Platform naar [!DNL Index] willen sturen om gebruikers te doelgericht naar specifieke inhoud op mobiele, web- en CTV-platforms die specifieke URL&#39;s, App Bundles of inhoud-id&#39;s gebruiken.

## Vereisten {#prerequisites}

De segmenten van het publiek moeten met [!DNL Index] worden geregistreerd gebruikend een extra proces wanneer het gebruiken van deze bestemming alvorens zij in uw rekening zullen verschijnen. Neem contact op met uw accountvertegenwoordiger van [!DNL Index Exchange] voor hulp bij dit proces.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Index] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

[!DNL Index Exchange] -doelen ondersteunen slechts één identiteitstype per upload. U moet het aangewezen herkenningstype specificeren wanneer het vormen van de bestemmingsdetails (zie [&#x200B; &quot;Vul bestemmingsdetails&quot;](#destination-details) hieronder).

Als u meerdere identiteitstypen wilt uploaden, maakt u afzonderlijke instanties van het doel [!DNL Index Exchange] voor elk type identiteit.

| Doelidentiteit | Beschrijving | Overwegingen |
| --- | --- | --- |
| GAID | GOOGLE ADVERTISING ID | Als de bronidentiteit een GAID-naamruimte is, selecteert u GAID als de doelidentiteit. |
| IDFA | Apple-id voor adverteerders | Als uw bronidentiteit een IDFA-naamruimte is, selecteert u de IDFA-doelidentiteit. |
| Windows-ID | Windows Advertising-id | Als uw bronidentiteit een naamruimte voor Windows-HULP is, selecteert u de doelidentiteit voor Windows-HULP. |
| extern_id | Aangepaste gebruikers-id&#39;s | Als uw bronidentiteit een aangepaste naamruimte is, selecteert u deze doelidentiteit. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

Deze sectie verklaart welke publiekstypes u naar deze bestemming kunt uitvoeren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| --------- | ---------- | --------- | 
| Exporttype | **[!UICONTROL Segment export]** | Exporteert alle leden van een segment (publiek) met de id&#39;s (IDFA, GAID of andere id&#39;s) die in de [!DNL Index Exchange] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Batch]** | Hiermee exporteert u bestanden naar downstreamplatforms met intervallen van 3, 6, 8, 12 of 24 uur. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Doelgegevens invullen {#destination-details}

Vul de onderstaande velden in om details voor de bestemming te configureren. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; de details van de Bestemming &#x200B;](../../assets/catalog/advertising/index-exchange/destination-details.png)

* [!UICONTROL Name]: voer een naam in om u te helpen deze bestemming later te herkennen.
* [!UICONTROL Description]: voer een beschrijving in om u te helpen deze bestemming later te identificeren.
* [!UICONTROL Identifier Type]: Selecteer het indextype id dat overeenkomt met de id waarnaar u [!DNL Index] verzendt. Zie de onderstaande tabel met ondersteunde id-typen. Neem contact op met uw [!DNL Index] vertegenwoordiger als u niet zeker weet welk type id u wilt gebruiken. Als u meerdere id-typen wilt verzenden, maakt u afzonderlijke instanties van dit doel.
* [!UICONTROL Account ID]: voer uw [!DNL Index] -account-id in. Dit is niet hetzelfde als uw uitgevers-id. Neem contact op met uw [!DNL Index] vertegenwoordiger als u niet zeker weet welke id u wilt gebruiken.

#### Ondersteunde id-typen

| Type id | Beschrijving |
|------------------ | ------------- |
| [!DNL appbundle] | Mobiele App-bundel |
| [!DNL contentid] | Inhoud-id |
| [!DNL deviceid] | Apparaat-id (bijvoorbeeld IDFA, GAID, WAID, enz.) |
| [!DNL ip] | IP-adres |
| [!DNL postcode] | Postcode |
| [!DNL url] | Site-URL |
| [!DNL ppid_xxx] | Neem voor PPID-id&#39;s contact op met uw accountvertegenwoordiger van [!DNL Index Exchange] voor hulp. |

{style="table-layout:auto"}

### Waarschuwingen inschakelen {#enable-alerts}

U kunt waarschuwingen inschakelen om meldingen te ontvangen over de status van uw gegevensstroom naar deze bestemming. Selecteer een of meer waarschuwingen in de lijst om u te abonneren op statusmeldingen voor uw gegevensstroom. Voor meer informatie, zie de gids op [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).
Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Bronvelden selecteren:

* Selecteer een id (gewoonlijk naamruimten zoals IDFA of een naamruimte van een aangepaste id). Dit moet overeenkomen met het geselecteerde Type van Identifier wanneer het vormen van de bestemming. Wanneer u bijvoorbeeld IDFA-id gebruikt als bronveld, moet de bestemming zijn ingesteld met het id-type &quot;deviceid&quot;.

Doelvelden selecteren:

* Namen van doelvelden worden genegeerd en zijn niet belangrijk. De bestemming geeft slechts om het type van herkenningsteken dat wordt verzonden, dat door het Geselecteerde Type van Herkenningsteken wanneer het vormen van de bestemming wordt bepaald.

![&#x200B; de attributen en de identiteiten van de Kaart &#x200B;](../../assets/catalog/advertising/index-exchange/identity-mapping.png)

### Segmenten registreren met [!DNL Index] {#register-segments}

Neem voor of na het activeren van gegevens naar het doel contact op met de [!DNL Index] -vertegenwoordiger om de segmenten te registreren die u wilt activeren. Uw vertegenwoordiger zal instructies verstrekken over hoe te om extra segmentdetails, met inbegrip van namen, IDs, beschrijvingen, en tarifering, indien van toepassing te registreren.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Zodra de registratie is voltooid, kunnen de segmenten zich richten op uw [!DNL Index] -account. Om te bevestigen dat de gegevens correct worden ontvangen, contacteer uw [!DNL Index] Vertegenwoordiger, die details over het volume van ontvangen segmentgegevens kan verstrekken.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle Experience Platform-doelen zijn bij het verwerken van uw gegevens compatibel met het beleid voor gegevensgebruik. Voor gedetailleerde informatie over hoe Experience Platform gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
