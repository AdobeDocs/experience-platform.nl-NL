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
>De [!DNL Acxiom Prospect-Suppression] doel is in bèta. Deze bestemmings schakelaar en documentatiepagina worden gecreeerd en door het team van Acxiom gehandhaafd. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de afdeling acxiom-adobe-help@acxiom.com.

## Overzicht {#overview}

Gebruiken [!DNL Acxiom Prospect-Suppression] een zo productief mogelijk publiek te bieden. Deze aansluiting exporteert gegevens van de eerste partij veilig uit Real-time Customer Data Platform en voert deze uit via een bekroonde hygiëne- en identiteitsresolutie die een gegevensbestand produceert dat als onderdrukkingslijst moet worden gebruikt. Dit wordt vergeleken met het [!DNL Acxiom Global] database die het mogelijk maakt dat de lijsten met perspectieven op maat worden gemaakt voor importeren. Gebruik vervolgens de [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) bronaansluiting voor perspectieflijsten van Acxiom terug naar Real-Time CDP, waarbij uw bekende of geconverteerde klanten zijn verwijderd.

![Marketing-diagram voor het exporteren van gegevens van de eerste partij naar Acxiom, en vervolgens de gegevens van het vooruitzicht weer in Real-Time CDP importeren](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom biedt het best presterende publiek in de branche met de grootste catalogus van meer dan 12.000 wereldwijde gegevenskenmerken die specifiek gericht zijn op het bieden van persoonlijke ervaringen. Tik in oneindige combinaties van gegevens van hoge kwaliteit om een publiek te maken en te verspreiden dat voldoet aan specifieke campagnebehoeften.

Deze zelfstudie bevat stappen om een [!DNL Acxiom Prospect-Suppression] doelverbinding en gegevensstroom via de Adobe Experience Platform-gebruikersinterface. Deze schakelaar wordt gebruikt om gegevens aan de dienst van het Vooruitzicht van Acxiom te leveren gebruikend Amazon S3 als dalingspunt. Neem contact op met uw accountvertegenwoordiger van Acxiom wanneer u bestanden gaat exporteren naar het Amazon S3-droppunt.

![De doelcatalogus met het geselecteerde doel van Acxiom.](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Acxiom Prospect-Suppression] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Een suppressielijst maken voor het doorzoeken van gegevenssets {#create-suppression-list}

Marketing-professionals die de doeltreffendheid van hun voorlichtingsstrategieën willen verbeteren, maken vaak gebruik van het opstellen van een onderdrukkingslijst. Deze lijst omvat bestaande klanten en specifieke segmenten, zodat zij tijdens gerichte campagnes van prospectie worden uitgesloten. Deze strategische aanpak helpt het publiek te verfijnen, vermijdt overbodige communicatie en draagt bij aan een meer gerichte en efficiënte marketinginspanning.

Als markeerteken wilt u bijvoorbeeld het bereik van uw campagne uitbreiden door doelgerichte perspectiefprofielen toe te voegen aan uw campagnes op basis van de segmentatie- en onderdrukkingscriteria die u hebt opgegeven.

Het gebruiksgeval wordt uitgevoerd door een combinatie van zowel bestemmings als bronschakelaars.

Eerst exporteert u uw bestaande klantprofielen met behulp van deze doelaansluiting die u als onderdrukkingsbestand wilt gebruiken. Dit zorgt ervoor dat geen bestaande klantenverslagen worden omvat.

De dienst van Acxiom zou naar het dossier zoeken, het terugwinnen en het naast extra selectiecriteria gebruiken en een perspectiefdossier produceren. Vervolgens gebruikt u het bijbehorende [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) bronaansluiting om de perspectiefprofielen in te voeren in Adobe Real-Time CDP.

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
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

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

Accounts zijn al gedefinieerd met het [!DNL Acxiom Prospect Suppression] doel wordt weergegeven in een pop-uplijst. Als u deze optie selecteert, kunt u details van de account bekijken in de rechtertrack. Bekijk het voorbeeld van UI, wanneer u navigeert aan **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**:

![Bestaande account](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

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

De verwerking vereist naam en adreselementen, terwijl niet alle elementen worden vereist die zo veel mogelijk helpen in succesvolle aanpassing.  Toewijzingssuggesties vindt u in de onderstaande tabel met de kenmerken aan uw doelzijde die worden gebruikt door de verwerking van Acxiom waaraan klanten profielkenmerken kunnen toewijzen.  Dit moet worden beschouwd als suggesties omdat niet alle elementen vereist zijn en de bronwaarden afhankelijk zijn van de behoeften van de account.

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

{style="table-layout:auto"}

>[!NOTE]
>
>Extra velden die hierboven niet worden vermeld, worden wel in de exportbewerking opgenomen, maar worden door de verwerking van Acxiom genegeerd.

## Controleer uw gegevensstroom

Gebruik de overzichtspagina voor een overzicht van uw gegevensstroom voorafgaand aan verzending

![Controleren](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## Gegevens exporteren valideren {#exported-data}

Controleer uw [!DNL Amazon S3 Storage] emmertje en zorg ervoor dat de uitgevoerde dossiers de verwachte profielpopulaties bevatten.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensstroom gemaakt om batchgegevens van Experience Platform naar uw [!DNL Acxiom] beheerde S3-locatie. U moet contact opnemen met uw vertegenwoordiger van Acxiom met de naam van het account, de bestandsnaam en het emmerpad, zodat de verwerking kan worden ingesteld.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

*Gegevens en distributie van acxiom-publiek:* https://www.acxiom.com/customer-data/audience-data-distribution/
