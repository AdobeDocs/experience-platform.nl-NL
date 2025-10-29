---
keywords: kenmerken van het luchtschip;bestemming van het luchtschip
title: Koppeling met kenmerken van het luchtschip
description: Geef naadloos Adobe Audience Data door aan Airship als Audience Attributes voor Doelstelling binnen Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# [!DNL Airship Attributes]-verbinding {#airship-attributes-destination}

## Overzicht {#overview}

[!DNL Airship] is de toonaangevende Experience Platform voor betrokkenheid van klanten, die u helpt bij het leveren van betekenisvolle, gepersonaliseerde omnichannel berichten aan uw gebruikers in elke fase van de levenscyclus van de klant.

Deze integratie gaat het profielgegevens van Adobe in [!DNL Airship] als [&#x200B; Attributen &#x200B;](https://docs.airship.com/guides/audience/attributes/) voor het richten van of het teweegbrengen over.

Meer over [!DNL Airship] leren, zie [&#x200B; Dokken van het Luchtschip &#x200B;](https://docs.airship.com).

>[!TIP]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Airship] . Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct bij [&#x200B; support.airship.com &#x200B;](https://support.airship.com/) te contacteren.

## Vereisten {#prerequisites}

Voordat u uw publiek naar [!DNL Airship] kunt sturen, moet u:

* Kenmerken inschakelen in uw [!DNL Airship] -project.
* Een token voor toonder genereren voor verificatie.

>[!TIP]
>
>Creeer een [!DNL Airship] rekening via [&#x200B; deze signaleringsverbinding &#x200B;](https://go.airship.eu/accounts/register/plan/starter/) als u niet reeds hebt.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam) en/of identiteiten volgens uw veldtoewijzing. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Kenmerken inschakelen {#enable-attributes}

Adobe Experience Platform-profielkenmerken lijken op [!DNL Airship] -kenmerken en kunnen in Experience Platform eenvoudig aan elkaar worden toegewezen met het toewijzingsgereedschap dat hieronder op deze pagina wordt getoond.

[!DNL Airship] -projecten hebben verschillende vooraf gedefinieerde en standaardkenmerken. Als u een aangepast kenmerk hebt, moet u dit eerst definiëren in [!DNL Airship] . Zie [&#x200B; Opstelling en beheer Attributen &#x200B;](https://docs.airship.com/tutorials/audience/attributes/) voor details.

## Dragertoken genereren {#bearer-token}

Ga naar **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** in [&#x200B; het dashboard van het Luchtschip &#x200B;](https://go.airship.com) en selecteer **[!UICONTROL Tokens]** in het linkermenu.

Klik op **[!UICONTROL Create Token]**.

Geef uw token een gebruikersvriendelijke naam, bijvoorbeeld &quot;Doel Adobe-kenmerken&quot;, en selecteer &quot;All Access&quot; voor de rol.

Klik op **[!UICONTROL Create Token]** en sla de details op als vertrouwelijk.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Airship Attributes] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Hoofdletters gebruiken #1

Gebruik profielgegevens die in Adobe Experience Platform zijn verzameld voor personalisatie van het bericht en rijke inhoud binnen de kanalen van [!DNL Airship]. Gebruik bijvoorbeeld [!DNL Experience Platform] -profielgegevens om locatiekenmerken in te stellen binnen [!DNL Airship] . Hierdoor kan een hotelmerk voor elke gebruiker een afbeelding weergeven voor de dichtstbijzijnde hotellocatie.

### Hoofdletters gebruiken #2

Gebruik kenmerken van Adobe Experience Platform om [!DNL Airship] -profielen verder te verrijken en deze te combineren met SDK of [!DNL Airship] voorspellende gegevens. Een retailer kan bijvoorbeeld een publiek met loyaliteitsstatus en locatiegegevens (kenmerken van Experience Platform) en [!DNL Airship] maken dat gegevens naar verwachting zal doorsturen om zeer gerichte berichten te verzenden naar gebruikers in de status van gouden loyaliteit die in Las Vegas, NV wonen en met een grote kans op churning.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

* **[!UICONTROL Bearer token]** : het token dat u hebt gegenereerd op het dashboard van [!DNL Airship] .

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: voer een naam in die u helpt bij het identificeren van dit doel.
* **[!UICONTROL Description]** : voer een beschrijving in voor dit doel.
* **[!UICONTROL Domain]**: selecteer een Amerikaans of EU-datacenter, afhankelijk van welk [!DNL Airship] -datacenter op dit doel van toepassing is.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [&#x200B; publieksgegevens aan het stromen publiek de uitvoerbestemmingen &#x200B;](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Toewijzingsoverwegingen {#mapping-considerations}

[!DNL Airship] -kenmerken kunnen worden ingesteld op een kanaal dat apparaatinstantie vertegenwoordigt, bijvoorbeeld iPhone, of op een benoemde gebruiker, die alle apparaten van een gebruiker toewijst aan een gemeenschappelijke id, zoals een klant-id. Als u normale (niet-gehashte) e-mailadressen als primaire identiteit in uw schema hebt, selecteert u het e-mailveld in uw **[!UICONTROL Source Attributes]** en wijst u deze toe aan de [!DNL Airship] benoemde gebruiker in de rechterkolom onder **[!UICONTROL Target Identities]** , zoals hieronder wordt weergegeven.

![&#x200B; Benoemde Toewijzing van de Gebruiker &#x200B;](../../assets/catalog/mobile-engagement/airship/mapping.png)

Voor herkenningstekens die aan een kanaal, d.w.z., een apparaat moeten worden in kaart gebracht, kaart aan het aangewezen kanaal dat op de bron wordt gebaseerd. De volgende afbeeldingen laten zien hoe twee toewijzingen worden gemaakt:

* IDFA iOS Advertising ID to an [!DNL Airship] iOS channel
* Adobe `fullName` -kenmerk naar [!DNL Airship] &quot;Full Name&quot;-kenmerk

>[!NOTE]
>
>Gebruik de gebruikersvriendelijke naam die in het dashboard van [!DNL Airship] verschijnt wanneer het selecteren van het doelgebied voor uw attributenafbeelding.

**Identiteit van de Kaart**

Bronveld selecteren:

![&#x200B; verbind met de Attributen van het Luchtschip &#x200B;](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Doelveld selecteren:

![&#x200B; verbind met de Attributen van het Luchtschip &#x200B;](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**attributen van de Kaart**

Bronkenmerk selecteren:

![&#x200B; Uitgezochte brongebied &#x200B;](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Doelkenmerk selecteren:

![&#x200B; Uitgezochte doelgebied &#x200B;](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Toewijzing verifiëren:

![&#x200B; de afbeelding van het Kanaal &#x200B;](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](../../../data-governance/home.md).
