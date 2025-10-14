---
title: Acxiom-perspectiefonderdrukking
description: Exporteer uw eersteklas publiek naar de Acxiom-bestemming, zodat Acxiom bekende of omgezette klanten kan onderdrukken. Dan gebruik de Acxiom bronschakelaar om perspectieflijsten van Acxiom in te voeren en te activeren, met uw bekende of omgezette klanten verwijderd.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: d82e8cd3-970c-44af-99b0-ea154eb3655e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---

# [!DNL Acxiom Prospect-Suppression] doelverbinding

>[!NOTE]
>
>Het doel van [!DNL Acxiom Prospect-Suppression] is in bèta. Deze bestemmings schakelaar en documentatiepagina worden gecreeerd en door het team van Acxiom gehandhaafd. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de afdeling acxiom-adobe-help@acxiom.com.

## Overzicht {#overview}

Gebruik [!DNL Acxiom Prospect-Suppression] om een zo productief mogelijk publiek te bieden. Deze aansluiting exporteert gegevens van de eerste partij veilig uit Real-time Customer Data Platform en voert deze uit via een bekroonde hygiëne- en identiteitsresolutie die een gegevensbestand produceert dat als onderdrukkingslijst moet worden gebruikt. Dit wordt vergeleken met de [!DNL Acxiom Global] -database, die het mogelijk maakt lijsten met mogelijke perspectieven op maat te maken voor importeren. Gebruik vervolgens de [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) -bronconnector om lijsten met perspectieven van Acxiom weer in Real-Time CDP te openen, waarbij uw bekende of geconverteerde klanten zijn verwijderd.

![&#x200B; op de markt brengend diagram om eerste-partijgegevens naar Acxiom uit te voeren, dan de gegevens van het invoerperspectief terug in Real-Time CDP &#x200B;](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom biedt het best presterende publiek in de branche met de grootste catalogus van meer dan 12.000 wereldwijde gegevenskenmerken die specifiek gericht zijn op het bieden van persoonlijke ervaringen. Tik in oneindige combinaties van gegevens van hoge kwaliteit om een publiek te maken en te verspreiden dat voldoet aan specifieke campagnebehoeften.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Acxiom Prospect-Suppression] doelverbinding en gegevensstroom via de Adobe Experience Platform-gebruikersinterface. Deze schakelaar wordt gebruikt om gegevens aan de dienst van het Vooruitzicht van Acxiom te leveren gebruikend Amazon S3 als dalingspunt. Neem contact op met uw accountvertegenwoordiger van Acxiom wanneer u bestanden gaat exporteren naar het Amazon S3-droppunt.

![&#x200B; de bestemmingscatalogus met de geselecteerde bestemming van Acxiom.](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Acxiom Prospect-Suppression] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Een suppressielijst maken voor het doorzoeken van gegevenssets {#create-suppression-list}

Marketing-professionals die de doeltreffendheid van hun voorlichtingsstrategieën willen verbeteren, maken vaak gebruik van het opstellen van een onderdrukkingslijst. Deze lijst omvat bestaande klanten en specifieke segmenten, zodat zij tijdens gerichte campagnes van prospectie worden uitgesloten. Deze strategische aanpak helpt het publiek te verfijnen, vermijdt overbodige communicatie en draagt bij aan een meer gerichte en efficiënte marketinginspanning.

Als markeerteken wilt u bijvoorbeeld het bereik van uw campagne uitbreiden door doelgerichte perspectiefprofielen toe te voegen aan uw campagnes op basis van de segmentatie- en onderdrukkingscriteria die u hebt opgegeven.

Het gebruiksgeval wordt uitgevoerd door een combinatie van zowel bestemmings als bronschakelaars.

Eerst exporteert u uw bestaande klantprofielen met behulp van deze doelaansluiting die u als onderdrukkingsbestand wilt gebruiken. Dit zorgt ervoor dat geen bestaande klantenverslagen worden omvat.

De dienst van Acxiom zou naar het dossier zoeken, het terugwinnen en het naast extra selectiecriteria gebruiken en een perspectiefdossier produceren. Vervolgens gebruikt u de bijbehorende [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) bronconnector om de perspectiefprofielen in te voeren in Adobe Real-Time CDP.

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>* Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** nodig, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions). Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van het Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | x | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [&#x200B; werkschema van de bestemmingsactivering &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

Om tot uw emmer op Experience Platform toegang te hebben, moet u geldige waarden voor de volgende geloofsbrieven verstrekken:

| Credentials | Beschrijving |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3 Toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |
| S3 Geheime toets | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |
| Naam van emmertje | Dit is uw emmertje waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |

### Nieuw account

Een nieuwe door Acxiom beheerde S3-locatie definiëren:

![&#x200B; Nieuwe Rekening &#x200B;](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Bestaande account

Accounts die al zijn gedefinieerd met het doel [!DNL Acxiom Prospect Suppression] , worden weergegeven in een pop-uplijst. Als u deze optie selecteert, kunt u details van de account bekijken in de rechtertrack. Bekijk het voorbeeld in de gebruikersinterface wanneer u naar **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** navigeert:

![&#x200B; Bestaande Rekening &#x200B;](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; Detail van de Bestemming &#x200B;](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Naam (Vereist)** - de naam de bestemming onder zal worden bewaard
* **Beschrijving** - Korte verklaring van het doel van de bestemming
* **Naam van het Emmertje (Vereist)** - Naam van de Amazon S3 emmer opstelling op S3
* **Weg van de Omslag (Vereist)** - als subdirectories in een emmertje worden gebruikt moet een weg worden bepaald, of &quot;/&quot;om de wortelweg van verwijzingen te voorzien.
* **Type van Dossier** - selecteer het formaat Experience Platform voor de uitgevoerde dossiers zou moeten gebruiken. Het enige bestandstype dat Acxiom verwerkt, is CSV

>[!IMPORTANT]
>
>Wanneer het selecteren van de optie CSV, *Scheidingsteken*, *het Karakter van het Citaat*, *Escape Karakter*, *Lege Waarde*, *Null Waarde*, *het formaat van de Compressie*, en *omvat duidelijke dossier* opties zullen worden voorgesteld, verklaart het volgende document meer in deze montages. detail [&#x200B; vormt de het formatteren opties &#x200B;](../../ui/batch-destinations-file-formatting-options.md).

![&#x200B; CSV Opties &#x200B;](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Toewijzingssuggesties

De verwerking vereist naam en adreselementen, terwijl niet alle elementen worden vereist die zo veel mogelijk helpen in succesvolle aanpassing.  Toewijzingssuggesties vindt u in de onderstaande tabel met de kenmerken aan uw doelzijde die worden gebruikt door de verwerking van Acxiom waaraan klanten profielkenmerken kunnen toewijzen.  Dit moet worden beschouwd als suggesties omdat niet alle elementen vereist zijn en de bronwaarden afhankelijk zijn van de behoeften van de account.

| Doelveld | Source-beschrijving |
|--------------|-------------------------------------------------------------|
| name | De `person.name.fullName` -waarde in Experience Platform. |
| firstName | De `person.name.firstName` -waarde in Experience Platform. |
| lastName | De `person.name.lastName` -waarde in Experience Platform. |
| address1 | De `mailingAddress.street1` -waarde in Experience Platform. |
| address2 | De `mailingAddress.street2` -waarde in Experience Platform. |
| stad | De `mailingAddress.city` -waarde in Experience Platform. |
| state | De `mailingAddress.state` -waarde in Experience Platform. |
| zip | De `mailingAddress.postalCode` -waarde in Experience Platform. |

{style="table-layout:auto"}

>[!NOTE]
>
>Extra velden die hierboven niet worden vermeld, worden wel in de exportbewerking opgenomen, maar worden door de verwerking van Acxiom genegeerd.

## Controleer uw gegevensstroom

Gebruik de overzichtspagina voor een overzicht van uw gegevensstroom voorafgaand aan verzending

![&#x200B; Overzicht &#x200B;](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## Gegevens exporteren valideren {#exported-data}

Om te controleren of gegevens zijn geëxporteerd, controleert u het emmertje van [!DNL Amazon S3 Storage] en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensstroom gemaakt om batchgegevens van Experience Platform naar uw [!DNL Acxiom] beheerde S3-locatie te exporteren. U moet contact opnemen met uw vertegenwoordiger van Acxiom met de naam van het account, de bestandsnaam en het emmerpad, zodat de verwerking kan worden ingesteld.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

*Gegevens en de Distributie van het publiek Acxiom:* https://www.acxiom.com/customer-data/audience-data-distribution/
