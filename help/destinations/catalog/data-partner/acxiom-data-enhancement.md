---
title: Verbetering van acxiom-gegevens
description: Gebruik deze connector om profielen van eersteklas Adoben in Real-Time CDP te activeren voor gegevensverrijking en gebruik via marketingkanalen. Vervolgens kunt u de Acxiom-bron gebruiken om de profielen met verbeterde gegevens te importeren en ermee te werken in Real-Time CDP.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 0%

---

# [!DNL Acxiom Data Enhancement] doelverbinding

>[!NOTE]
>
>De [!DNL Acxiom Data Enhancement] doel is in bèta.  Deze bestemmings schakelaar en documentatiepagina worden gecreeerd en door het team van Acxiom gehandhaafd. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de afdeling acxiom-adobe-help@acxiom.com.

## Overzicht {#overview}

Gebruik de [!DNL Acxiom Data Enhancement] om extra beschrijvende gegevens aan uw klantenprofielen, voor gebruik in analytische, segmentatie, en gerichte toepassingen te leveren. Met honderden beschikbare elementen, staat dit u toe om gegevens te segmenteren en te modelleren, resulterend in nauwkeuriger het richten en voorspellende modellering.

![Marketing-diagram voor het exporteren van gegevens van eerste partijen naar Acxiom, en het importeren van verrijkte gegevens terug naar Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

Deze zelfstudie bevat stappen om een [!DNL Acxiom Data Enhancement] doelverbinding en gegevensstroom via de Adobe Experience Platform-gebruikersinterface. Deze connector wordt gebruikt om gegevens te leveren aan de Acxiom-verbeteringsservice met Amazon S3 als droppunt.

![De doelcatalogus met het geselecteerde doel van Acxiom.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Acxiom Data Enhancement] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Klantgegevens verbeteren {#enhance-customer-data}

Deze connector moet worden gebruikt door marketingprofessionals die de doeltreffendheid van hun outreach-strategieën willen verbeteren door geselecteerde beschrijvende elementen toe te voegen aan hun klantprofielen en deze te gebruiken om beter doelgerichte campagnes te voeren.

Als een markeerteken wilt u bijvoorbeeld uw inzicht in bestaande doelgroepen verdiepen door hun profielen te verrijken met aanvullende gegevens. Zo verbetert u de segmentatie en doelgerichte strategieën, wat leidt tot een grotere personalisatie en conversie van de campagne.

Het gebruiksgeval wordt uitgevoerd door een combinatie van zowel bestemmings als bronschakelaars.

U zou beginnen door uw bestaande klantenverslagen voor verrijking te exporteren gebruikend deze bestemmingsschakelaar. De service van Acxiom zoekt naar het bestand, haalt het op, verrijkt het met de gegevens van Acxiom en genereert een bestand.

De klant zou dan de overeenkomstige [Acxiale gegevensinname](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) de bronkaart om de gehydrateerde klantenprofielen terug in Adobe Real-Time CDP op te nemen.

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>* Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | x | Soorten publiek [geïmporteerd](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage and Activate Dataset Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

Om tot uw emmer op Experience Platform toegang te hebben, moet u geldige waarden voor de volgende geloofsbrieven verstrekken:

| Credentials | Beschrijving |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3 Toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| S3 Geheime toets | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| Naam van emmertje | Dit is uw emmertje waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |

### Nieuw account

Een nieuwe door Acxiom beheerde S3-locatie definiëren:

![Nieuw account](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Bestaande account

Accounts zijn al gedefinieerd met het [!DNL Acxiom Data Enhancement] doel wordt weergegeven in een pop-uplijst. Als u deze optie selecteert, kunt u details van de account bekijken in de rechtertrack. Bekijk het voorbeeld van UI, wanneer u navigeert aan **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**;

![Bestaande account](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Doeldetails](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Naam (vereist)** - De naam waaronder het doel wordt opgeslagen
* **Beschrijving** - Korte toelichting van het doel van de bestemming
* **Emmernaam (vereist)** - Naam van het Amazon S3-emmertje dat is ingesteld op S3
* **Pad naar map (vereist)** - Als submappen in een emmertje worden gebruikt, moet een pad worden gedefinieerd of moet &#39;/&#39; worden gedefinieerd om naar het hoofdpad te verwijzen.
* **Bestandstype** - Selecteer de indeling die het Experience Platform moet gebruiken voor de geëxporteerde bestanden. Het enige bestandstype dat Acxiom verwerkt, is CSV

>[!IMPORTANT]
>
>Als u de optie CSV selecteert, *Scheidingsteken*, *Aanhalingsteken*, *Escape-teken*, *Lege waarde*, *Null-waarde*, *Compressie-indeling*, en *Inclusief manifestbestand* de opties worden weergegeven. In het volgende document worden deze instellingen nader toegelicht [de opmaakopties configureren](../../ui/batch-destinations-file-formatting-options.md).

![CSV-opties](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Toewijzingssuggesties

Voor een correcte verwerking van bestanden aan de Acxiom-zijde zijn naam- en adreselementen vereist. Hoewel niet alle elementen vereist zijn, zal het zo veel mogelijk helpen om tot een succesvolle overeenkomst te komen.

Toewijzingssuggesties vindt u in de onderstaande tabel met de kenmerken aan uw doelzijde die worden gebruikt door de verwerking van Acxiom waaraan klanten profielkenmerken kunnen toewijzen. Behandel deze elementen als suggesties aangezien niet alle elementen worden vereist en de bronwaarden zullen afhangen van de behoeften van de rekening.

| Doelveld | Source-beschrijving |
|--------------|-------------------------------------------------------------|
| name | De `person.name.fullName` waarde in Experience Platform. |
| firstName | De `person.name.firstName` waarde in Experience Platform. |
| lastName | De `person.name.lastName` waarde in Experience Platform. |
| address1 | De `mailingAddress.street1` waarde in Experience Platform. |
| address2 | De `mailingAddress.street2` waarde in Experience Platform. |
| stad | De `mailingAddress.city` waarde in Experience Platform. |
| state | De `mailingAddress.state` waarde in Experience Platform. |
| zip | De `mailingAddress.postalCode` waarde in Experience Platform. |

>[!NOTE]
>
>Als u extra velden toewijst die niet hierboven in de gegevensstroom worden vermeld, worden deze opgenomen in de gegevensexport, maar worden deze genegeerd door de verwerking van Acxiom.

## Gegevens exporteren valideren {#exported-data}

Controleer uw [!DNL Amazon S3 Storage] emmertje en zorg ervoor dat de uitgevoerde dossiers de verwachte profielpopulaties bevatten.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensstroom gemaakt om profielgegevens van Experience Platform naar uw [!DNL Acxiom] beheerde S3-locatie. Vervolgens moet u contact opnemen met uw vertegenwoordiger van Acxiom met de naam van de account, de bestandsnamen en het emmerpad, zodat de verwerking kan worden ingesteld.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

*Acxiom Infobase:* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
