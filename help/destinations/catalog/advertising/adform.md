---
title: Adform
description: Adform is een toonaangevende leverancier van software voor het kopen en verkopen van media. Als u Adobe verbindt met de Adobe Experience Platform, kunt u uw publiek van de eerste partij activeren via Adform op basis van de Experience Cloud-id (ECID).
source-git-commit: 823b2142366ac218ad93279de5f31d60bdc07bbf
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 0%

---


# Verbinding voor Adobe {#adform}

## Overzicht {#overview}

Adform is een toonaangevende leverancier van software voor het kopen en verkopen van media. Als u Adobe verbindt met de Adobe Experience Platform, kunt u uw eerste publiek activeren via Adform op basis van de Experience Cloud-id (ECID).

>[!IMPORTANT]
>
>De doelconnector en documentatiepagina worden gemaakt en onderhouden door het Adform-team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via `support@adform.com` .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van Adform zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Adobe Real-Time CDP-publieksactivering {#use-case-1}

Gebruik deze bestemming om Adobe Real-Time CDP-publiek naar Adobe te sturen voor activering op basis van de Experience Cloud-id (ECID) en de Adobe-id voor Fusion. De Adobe ID Fusion is de service voor het oplossen van id&#39;s van Adobe waarmee u het eerste publiek kunt activeren op basis van de Experience Cloud-id (ECID).

Een veelvoorkomend geval is het opnieuw toewijzen van uw websitebezoekers aan uw website of app op basis van de Experience Cloud-id (ECID). Alles u moet doen moet identiteitskaart van Experience Cloud (ECID) naar Adform via gemakkelijk beschikbare [&#x200B; Gebeurtenis verzenden die &#x200B;](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) stroomt of [&#x200B; cliënt-kant &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/catalog/analytics/adform) uitbreidingen Adform. Daarna kunt u een publiek delen met Adobe via de bestemming Adform voor activering - uitsluitend op basis van de Experience Cloud-id (ECID).

## Vereisten {#prerequisites}

* U moet een bestaande klant van Adobe zijn om deze bestemming te gebruiken.
* U moet over uw geloofsbrieven van de Verbinding van de Gegevens van de Gegevens van de Audience van de Audience hebben.
   * Neem contact op met uw vertegenwoordiger van Adobe als u geen gegevens voor Adform Audience Base-gegevensverbinding hebt.
* Voor juiste synchronisatie moet u of een [&#x200B; Gebeurtenis hebben die &#x200B;](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) stroomt of [&#x200B; cliënt-kant &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/catalog/analytics/adform) verbinding van uw entiteiten aan het Volgen van de Plaats Adform.
   * Neem contact op met uw vertegenwoordiger van Adobe als u geen Streaming van gebeurtenissen of client-side verbinding van uw entiteiten hebt met Adform Site Tracking.
   * Adform verstrekt de uitbreidingen van Adobe Experience Cloud voor zowel [&#x200B; Gebeurtenis het Streamen &#x200B;](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) als [&#x200B; cliënt-kant &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/catalog/analytics/adform).


## Ondersteunde identiteiten {#supported-identities}

Adform ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [&#x200B; ECID &#x200B;](/help/identity-service/features/ecid.md) voor meer informatie. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U voert alle leden van een segment (publiek) met de herkenningstekens (naam, telefoonaantal, of anderen) uit die in *worden gebruikt UwDoel* bestemming. |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![&#x200B; verifieer aan de bestemming &#x200B;](../../assets/catalog/advertising/adform/authenticate-destination.png)

* **[!UICONTROL Account name]**: voer een accountnaam in waarmee u deze doelverbinding in de toekomst kunt identificeren.
* **[!UICONTROL S3 Access Key ID]**: vul de S3 Toegangssleutel in die door Adform wordt verstrekt.
* **[!UICONTROL S3 Secret Access Key]**: vul de S3 Geheime Sleutel van de Toegang in die door Adform wordt verstrekt.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; Vul in de bestemmingsdetails &#x200B;](../../assets/catalog/advertising/adform/configure-destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Provider Name]**: De naam van uw Adobe-account die door Adobe is opgegeven.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

* **ECID** (identiteitskaart van Experience Cloud)

Gebruik tijdens de toewijzingsstap alleen de [!DNL ECID] -doelidentiteitstoewijzing. Neem geen andere identiteitsvelden op, omdat de activering dan niet kan worden voltooid.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

De bestemmingsschakelaar voert slechts de identiteit ECID naar de bestemming uit. Er wordt geen andere identiteit geëxporteerd. Als u wilt controleren of de gegevens zijn geëxporteerd, meldt u zich aan bij uw Adform Audience Base-account en controleert u of het publiek beschikbaar is.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Voor extra informatie over de Adform Basis van het Publiek, zie de [&#x200B; Adform documentatie van de Basis van het Publiek &#x200B;](https://www.adformhelp.com/hc/en-us/categories/9738365991697-Data-Management-Platform).