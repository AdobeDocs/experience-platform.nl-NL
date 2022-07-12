---
keywords: luchtschepen, codes;bestemming van het luchtschip
title: Koppeling met vliegtuigcodes
description: Geef naadloos Adobe-geluidsgegevens van het publiek door aan het luchtschip als Publiek-tags voor doelwit binnen het luchtschip.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# [!DNL Airship Tags] verbinding {#airship-tags-destination}

## Overzicht

[!DNL Airship] is het toonaangevende Platform voor betrokkenheid van klanten, waarmee u in elke fase van de levenscyclus van de klant betekenisvolle, gepersonaliseerde omnichanale berichten aan uw gebruikers kunt leveren.

Deze integratie geeft Adobe Experience Platform-segmentgegevens door in [!DNL Airship] als [Tags](https://docs.airship.com/guides/audience/tags/) voor aanwijzen of activeren.

Meer informatie over [!DNL Airship], zie de [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Deze documentatiepagina is gemaakt door de [!DNL Airship] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [support.airship.com](https://support.airship.com/).

## Vereisten

Voordat u uw Adobe Experience Platform-segmenten kunt verzenden naar [!DNL Airship]moet u:

* Een taggroep maken in uw [!DNL Airship] project.
* Een token voor toonder genereren voor verificatie.

>[!TIP]
> 
>Een [!DNL Airship] account via [deze link](https://go.airship.eu/accounts/register/plan/starter/) als u dat nog niet hebt gedaan.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s die worden gebruikt in de bestemming Airship Tags. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Taggroepen

Het concept van segmenten in het Adobe Experience Platform lijkt op [Tags](https://docs.airship.com/guides/audience/tags/) in het luchtschip, met lichte verschillen in uitvoering. Deze integratie brengt de status van de gebruiker in kaart [lidmaatschap in een segment van de Experience Platform](../../../xdm/field-groups/profile/segmentation.md) de aanwezigheid of het ontbreken van een [!DNL Airship] tag. Bijvoorbeeld in een segment van het Platform waar `xdm:status` wijzigingen in `realized`, wordt de tag toegevoegd aan de [!DNL Airship] kanaal of benoemde gebruiker wordt dit profiel toegewezen aan. Als de `xdm:status` wijzigingen in `exited`, wordt de tag verwijderd.

Als u deze integratie wilt inschakelen, maakt u een *taggroep* in [!DNL Airship] benoemd `adobe-segments`.

>[!IMPORTANT]
>
>Wanneer u een nieuwe taggroep maakt **Niet controleren** het keuzerondje &quot;[!DNL Allow these tags to be set only from your server]&quot;. Als u dit doet, mislukt de integratie van de Adobe-tags.

Zie [Taggroepen beheren](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) voor instructies over het maken van de taggroep.

## Dragertoken genereren

Ga naar **[!UICONTROL Settings]** &quot; **[!UICONTROL APIs & Integrations]** in de [Luchtvaartdashboard](https://go.airship.com) en selecteert u **[!UICONTROL Tokens]** in het linkermenu.

Klik op **[!UICONTROL Create Token]**.

Geef uw token een gebruikersvriendelijke naam, bijvoorbeeld &quot;Doel van Adobe-tags&quot;, en selecteer &quot;Alle toegang&quot; voor de rol.

Klikken **[!UICONTROL Create Token]** en bewaren de gegevens als vertrouwelijk.

## Gebruiksscenario’s

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Airship Tags] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters gebruiken #1

De detailhandelaars of de entertainmentplatforms kunnen gebruikersprofielen op hun loyaliteitklanten tot stand brengen en die segmenten overgaan in [!DNL Airship] voor berichten die gericht zijn op mobiele campagnes.

### Hoofdletters gebruiken #2

U kunt een-op-een berichten in real-time activeren wanneer gebruikers binnen of buiten specifieke segmenten in Adobe Experience Platform vallen.

Een detailhandelaar stelt bijvoorbeeld een merkspecifiek segment voor jeans in Platform in. Deze detailhandelaar kan nu een mobiel bericht activeren zodra iemand zijn jeans-voorkeur op een bepaald merk instelt.

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

[!DNL Airship] -tags kunnen worden ingesteld op een kanaal dat apparaatinstantie vertegenwoordigt, bijvoorbeeld iPhone, of op een benoemde gebruiker, die alle apparaten van een gebruiker toewijst aan een gemeenschappelijke id, zoals een klant-id. Als u onbewerkte (niet-gehashte) e-mailadressen als primaire identiteit in uw schema hebt, selecteert u het e-mailveld in uw schema **[!UICONTROL Source Attributes]** en de kaart aan [!DNL Airship] benoemde gebruiker in de rechterkolom onder **[!UICONTROL Target Identities]**, zoals hieronder weergegeven.

![Toewijzing van benoemde gebruikers](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Voor herkenningstekens die aan een kanaal, d.w.z., een apparaat moeten worden in kaart gebracht, kaart aan het aangewezen kanaal dat op de bron wordt gebaseerd. In de volgende afbeeldingen ziet u hoe u een advertentie-id van Google toewijst aan een [!DNL Airship] Android-kanaal.

![Verbinden met luchtvaartcodes](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Verbinden met luchtvaartcodes](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Kanaaltoewijzing](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](../../../data-governance/home.md).
