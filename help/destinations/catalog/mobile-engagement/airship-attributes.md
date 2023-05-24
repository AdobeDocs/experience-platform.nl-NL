---
keywords: kenmerken van het luchtschip;bestemming van het luchtschip
title: Koppeling met kenmerken van luchtschip
description: Geef naadloos Adobe-geluidsgegevens van het publiek door aan het luchtschip als publiekskenmerken voor het aansturen van vluchten binnen het luchtschip.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# [!DNL Airship Attributes] verbinding {#airship-attributes-destination}

## Overzicht {#overview}

[!DNL Airship] is het toonaangevende Platform voor betrokkenheid van klanten, waarmee u in elke fase van de levenscyclus van de klant betekenisvolle, gepersonaliseerde omnichanale berichten aan uw gebruikers kunt leveren.

Door deze integratie worden Adobe-profielgegevens doorgegeven aan [!DNL Airship] als [Attributen](https://docs.airship.com/guides/audience/attributes/) voor aanwijzen of activeren.

Meer informatie over [!DNL Airship], zie de [Airship Docs](https://docs.airship.com).

>[!TIP]
>
>Deze documentatiepagina is gemaakt door de [!DNL Airship] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [support.airship.com](https://support.airship.com/).

## Vereisten {#prerequisites}

Voordat u publiekssegmenten kunt verzenden naar [!DNL Airship]moet u:

* Kenmerken inschakelen in uw [!DNL Airship] project.
* Een token voor toonder genereren voor verificatie.

>[!TIP]
>
>Een [!DNL Airship] account via [deze link](https://go.airship.eu/accounts/register/plan/starter/) als u dat nog niet hebt gedaan.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam) en/of identiteiten, afhankelijk van uw veldtoewijzing. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Kenmerken inschakelen {#enable-attributes}

Adobe Experience Platform-profielkenmerken lijken op [!DNL Airship] -kenmerken en kunnen gemakkelijk aan elkaar worden toegewezen in Platform met behulp van het toewijzingsgereedschap dat hieronder verder op deze pagina wordt getoond.

[!DNL Airship] de projecten hebben verscheidene vooraf bepaalde en standaardattributen. Als u een aangepast kenmerk hebt, moet u dit definiëren in [!DNL Airship] eerst. Zie [Kenmerken instellen en beheren](https://docs.airship.com/tutorials/audience/attributes/) voor meer informatie.

## Dragertoken genereren {#bearer-token}

Ga naar **[!UICONTROL Settings]** &quot; **[!UICONTROL APIs & Integrations]** in de [Luchtvaartdashboard](https://go.airship.com) en selecteert u **[!UICONTROL Tokens]** in het linkermenu.

Klik op **[!UICONTROL Create Token]**.

Geef een gebruikersvriendelijke naam voor uw token op, bijvoorbeeld &quot;Doel Adobe-kenmerken&quot;, en selecteer &quot;Alle toegang&quot; voor de rol.

Klikken **[!UICONTROL Create Token]** en bewaren de gegevens als vertrouwelijk.

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Airship Attributes] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters gebruiken #1

Gebruik profielgegevens die in Adobe Experience Platform zijn verzameld voor personalisatie van het bericht en rijke inhoud binnen een van de volgende [!DNL Airship]Kanalen. Bijvoorbeeld, hefboomwerking [!DNL Experience Platform] profielgegevens om locatiekenmerken in te stellen binnen [!DNL Airship]. Hierdoor kan een hotelmerk voor elke gebruiker een afbeelding weergeven voor de dichtstbijzijnde hotellocatie.

### Hoofdletters gebruiken #2

Kenmerken van Adobe Experience Platform benutten om verder te verrijken [!DNL Airship] profielen en deze combineren met SDK of [!DNL Airship] voorspellende gegevens. Een detailhandelaar kan bijvoorbeeld een segment met loyaliteitsstatus en locatiegegevens (kenmerken van Platform) maken en [!DNL Airship] voorspeld om gegevens te sturen om hoogst gerichte berichten naar gebruikers in de gouden loyaliteitsstatus te verzenden die in Las Vegas, NV wonen, en een hoge waarschijnlijkheid van het kurken hebben.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Bearer token]**: het token dat u hebt gegenereerd op basis van het [!DNL Airship] dashboard.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Voer een naam in die u helpt deze bestemming te identificeren.
* **[!UICONTROL Description]**: Voer een beschrijving in voor deze bestemming.
* **[!UICONTROL Domain]**: een Amerikaans of EU-datacenter selecteren, afhankelijk van [!DNL Airship] het gegevenscentrum is op deze bestemming van toepassing.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Toewijzingsoverwegingen {#mapping-considerations}

[!DNL Airship] attributen kunnen op of een kanaal worden geplaatst, dat apparateninstantie, b.v., iPhone, of een genoemde gebruiker vertegenwoordigt, die alle apparaten van een gebruiker aan een gemeenschappelijk herkenningsteken zoals een klant identiteitskaart in kaart brengt. Als u onbewerkte (niet-gehashte) e-mailadressen als primaire identiteit in uw schema hebt, selecteert u het e-mailveld in uw schema **[!UICONTROL Source Attributes]** en de kaart aan [!DNL Airship] benoemde gebruiker in de rechterkolom onder **[!UICONTROL Target Identities]**, zoals hieronder weergegeven.

![Toewijzing van benoemde gebruikers](../../assets/catalog/mobile-engagement/airship/mapping.png)

Voor herkenningstekens die aan een kanaal, d.w.z., een apparaat moeten worden in kaart gebracht, kaart aan het aangewezen kanaal dat op de bron wordt gebaseerd. De volgende afbeeldingen laten zien hoe twee toewijzingen worden gemaakt:

* IDFA iOS Advertising ID to an [!DNL Airship] iOS-kanaal
* Adobe `fullName` kenmerk naar [!DNL Airship] Kenmerk &quot;Volledige naam&quot;

>[!NOTE]
>
>Gebruik de gebruikersvriendelijke naam die wordt weergegeven in het dialoogvenster [!DNL Airship] dashboard wanneer het selecteren van het doelgebied voor uw attributenafbeelding.

**Identiteit kaart**

Bronveld selecteren:

![Verbinden met kenmerken van het luchtschip](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Doelveld selecteren:

![Verbinden met kenmerken van het luchtschip](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Kenmerk Kaart**

Bronkenmerk selecteren:

![Bronveld selecteren](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Doelkenmerk selecteren:

![Doelveld selecteren](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Toewijzing verifiëren:

![Kanaaltoewijzing](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](../../../data-governance/home.md).
