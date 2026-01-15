---
title: De Trade Desk - CRM-verbinding
description: Activeer profielen aan uw rekening van het Bureau van de Handel voor publiek gericht en onderdrukking die op de gegevens van CRM wordt gebaseerd.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: b9713d5155f89ee895d9fb623088eda77b931d89
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 0%

---

# De [!DNL Trade Desk] - CRM-verbinding

>[!IMPORTANT]
>
>Met de versie van EUID (Europese Verenigde identiteitskaart), ziet u nu twee [!DNL The Trade Desk - CRM] bestemmingen in de [ bestemmingscatalogus ](/help/destinations/catalog/overview.md).
>
>* Gebruik de **[!DNL The Trade Desk - CRM (EU)]** -bestemming als u gegevens in de EU levert.
>* Gebruik het doel **[!DNL The Trade Desk - CRM (NAMER & APAC)]** als u gegevens in de APAC- of NAMER-gebieden bront.
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van *[!DNL Trade Desk]* . Neem contact op met uw [!DNL Trade Desk] vertegenwoordiger voor meer informatie of verzoeken om updates.

## Overzicht {#overview}

Begrijp hoe u profielen aan uw [!DNL Trade Desk] rekening voor publiek activeert richt en onderdrukking die op de gegevens van CRM wordt gebaseerd.

Deze schakelaar verzendt gegevens naar het [!DNL The Trade Desk] eerste partijeindpunt. De integratie tussen Adobe Experience Platform en [!DNL The Trade Desk] biedt geen ondersteuning voor het exporteren van gegevens naar het eindpunt van derden voor [!DNL The Trade Desk] .

[!DNL The Trade Desk(TTD)] handelt het geüploade bestand met e-mailadressen nooit rechtstreeks af en [!DNL The Trade Desk] slaat uw onbewerkte (ongehashte) e-mails niet op.

>[!TIP]
>
>Gebruik [!DNL The Trade Desk] CRM-doelen voor CRM-gegevenstoewijzing, zoals e-mailadres of gehasht e-mailadres. Gebruik de [ andere bestemming van het Bureau van de Handel ](/help/destinations/catalog/advertising/tradedesk.md) in de catalogus van Adobe Experience Platform voor koekjes en de afbeeldingen van apparatenidentiteitskaart.

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>Voordat u het publiek naar de handelsbank kunt activeren, moet u contact opnemen met uw accountmanager van [!DNL Trade Desk] om het CRM-instapcontract te ondertekenen. [!DNL The Trade Desk] maakt het gebruik van UID2/EUID mogelijk en deelt andere gegevens om u te helpen uw bestemming te configureren.

## Vereisten voor ID-afstemming {#id-matching-requirements}

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen. Gelieve te lezen het [ overzicht van Namespace van de Identiteit ](/help/identity-service/features/namespaces.md) voor meer informatie.

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de sectie met vereisten voor id-afstemming en gebruik de juiste naamruimten voor normale tekst en gehashte e-mailadressen.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| Email | E-mailadressen (tekst wissen) | Voer `email` in als de doelidentiteit wanneer de bronidentiteit een naamruimte of attribuut E-mail is. |
| Email_LC_SHA256 | E-mailadressen moeten worden gehasht met behulp van SHA256 en verlaagd. U kunt deze instelling later niet wijzigen. | Voer `hashed_email` in als de doelidentiteit wanneer uw bronidentiteit een naamruimte of attribuut Email_LC_SHA256 is. |

{style="table-layout:auto"}

## E-mailhashingvereisten {#hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen of onbewerkte e-mailadressen gebruiken.

Om over het opnemen van e-mailadressen in Experience Platform te leren, lees het [ overzicht van de partijingestitie ](/help/ingestion/batch-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

* Voorloopspaties en volgspaties verwijderen.
* Zet alle ASCII-tekens om in kleine letters.
* Verwijder in het gedeelte Gebruikersnaam van het e-mailadres van `gmail.com` de volgende tekens uit het e-mailadres:
   * De periode (. (ASCII-code 46). U kunt `jane.doe@gmail.com` bijvoorbeeld normaliseren naar `janedoe@gmail.com` .
   * Het plusteken (+ (ASCII-code 43)) en alle daaropvolgende tekens. U kunt `janedoe+home@gmail.com` bijvoorbeeld normaliseren naar `janedoe@gmail.com` .

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail of gehashte e-mail) die worden gebruikt in de bestemming Handelsbureau. |
| Exportfrequentie | **[!UICONTROL Daily Batch]** | Aangezien een profiel in Experience Platform wordt bijgewerkt op basis van publieksevaluatie, wordt het profiel (de identiteiten) eenmaal per dag bijgewerkt naar het doelplatform. Lees meer over [ partijuitvoer ](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

### Verifiëren voor doel {#authenticate}

[!DNL The Trade Desk] CRM-bestemming is een dagelijkse bestandsupload waarvoor geen verificatie door de gebruiker is vereist.

### Bestemmingsdetails invullen {#fill-in-details}

Voordat u publieksgegevens naar een doel kunt verzenden of activeren, moet u een verbinding met uw eigen doelplatform instellen. Terwijl [ vestiging ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Account Type]**: Kies de optie **[!UICONTROL Existing Account]** .
* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Advertiser ID]**: uw [!DNL Trade Desk Advertiser ID] , die kan worden gedeeld door uw [!DNL Trade Desk] accountmanager of kan worden gevonden onder [!DNL Advertiser Preferences] in de gebruikersinterface van [!DNL Trade Desk] .

{het schermschot van 0} Experience Platform UI die tonen hoe te om bestemmingsdetails in te vullen.![](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Wanneer u verbinding maakt met de bestemming, is het instellen van een beleid voor gegevensbeheer volledig optioneel. Gelieve te herzien Experience Platform [ overzicht van het gegevensbeheer ](/help/data-governance/policies/overview.md) voor meer details.

## Soorten publiek naar dit doel activeren {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttdg"
>title="Vooraf geconfigureerde toewijzingssets"
>abstract="Wij hebben deze vier kaartreeksen voor u vooraf gevormd. Als u gegevens activeert op Trade Desk, hoeven de profielen die zijn gekwalificeerd voor het actieve publiek niet noodzakelijkerwijs alle vier de identiteiten te hebben die aanwezig zijn in de profielen, aangezien deze bestemming werkt met een van de hier weergegeven doelidentiteiten."

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiek aan een bestemming.

Op de pagina **[!UICONTROL Scheduling]** kunt u het schema en de bestandsnamen configureren voor elk publiek dat u exporteert. Het is verplicht het schema te configureren, maar het configureren van de bestandsnaam is optioneel.

{het schermschot van 0} Experience Platform UI aan de activering van het programmapubliek.![](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alle soorten publiek die op [!DNL The Trade Desk] CRM-bestemming worden geactiveerd, worden automatisch ingesteld op een dagelijkse frequentie en het volledige bestand wordt geëxporteerd.

{het schermschot van 0} Experience Platform UI aan de activering van het programmapubliek.![](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Op de pagina **[!UICONTROL Mapping]** moet u kenmerken of naamruimten selecteren in de bronkolom en toewijzen aan de doelkolom.

{het schermschot van 0} Experience Platform UI aan de activering van het kaartpubliek.![](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het activeren van soorten publiek naar [!DNL The Trade Desk] CRM-bestemming.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM-bestemming accepteert geen onbewerkte en gehashte e-mailadressen als identiteiten in dezelfde activeringsstroom. Maak afzonderlijke activeringsstromen voor onbewerkte en gehashte e-mailadressen.

Bronvelden selecteren:

* Selecteer de naamruimte of het kenmerk `Email` als bronidentiteit als u het onbewerkte e-mailadres bij gegevensinvoer gebruikt.
* Selecteer de naamruimte of het kenmerk `Email_LC_SHA256` als bronidentiteit als u de e-mailadressen van klanten bij het invoeren van gegevens in Experience Platform hebt gewijzigd.

Doelvelden selecteren:

* Voer `email` in als doelidentiteit wanneer uw bronnaamruimte of -kenmerk `Email` is.
* Voer `hashed_email` in als doelidentiteit wanneer uw bronnaamruimte of -kenmerk `Email_LC_SHA256` is.

## Gegevens exporteren valideren {#validate}

Als u wilt controleren of gegevens correct vanuit Experience Platform en naar [!DNL The Trade Desk] worden geëxporteerd, zoekt u het publiek onder de Adobe 1PD-gegevenstabel in [!DNL The Trade Desk] Data Management Platform (DMP). Hier volgen de stappen voor het zoeken van de bijbehorende id in de gebruikersinterface van [!DNL Trade Desk] :

1. Selecteer eerst de tab **[!UICONTROL Data]** en bekijk de sectie **[!UICONTROL First-Party]** .
2. Schuif omlaag op de pagina, onder **[!UICONTROL Imported Data]** , zoekt u de **[!UICONTROL Adobe 1PD Tile]** .
3. Klik op de tegel** [!UICONTROL Adobe 1PD]** en hierin worden alle soorten publiek weergegeven die zijn geactiveerd voor de [!DNL Trade Desk] -bestemming voor uw adverteerder. U kunt ook de zoekfunctie gebruiken.
4. Het segment-id # van Experience Platform wordt weergegeven als de segmentnaam in de gebruikersinterface van [!DNL Trade Desk] .

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
