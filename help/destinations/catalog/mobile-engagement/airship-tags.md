---
keywords: luchtschepen, codes;bestemming van het luchtschip
title: Koppeling met vliegtuigcodes
description: Naadloos gegevens van het publiek van de Adobe doorgeven aan het luchtschip als Poortcodes voor doelgroepen binnen het luchtschip.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---

# [!DNL Airship Tags] verbinding {#airship-tags-destination}

## Overzicht

[!DNL Airship] is het toonaangevende platform voor betrokkenheid van klanten, waarmee u in elke fase van de levenscyclus van de klant betekenisvolle, gepersonaliseerde omnichannel berichten aan uw gebruikers kunt leveren.

Deze integratie geeft Adobe Experience Platform-publieksgegevens door [!DNL Airship] als [Tags](https://docs.airship.com/guides/audience/tags/) voor aanwijzen of activeren.

Meer informatie over [!DNL Airship], zie de [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door [!DNL Airship] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [support.airship.com](https://support.airship.com/).

## Vereisten

Voordat je een Adobe Experience Platform-publiek kunt sturen naar [!DNL Airship], moet u:

* Een taggroep maken in uw [!DNL Airship] project.
* Een token voor toonder genereren voor verificatie.

>[!TIP]
> 
>Een [!DNL Airship] account via [deze koppeling naar aanmelding](https://go.airship.eu/accounts/register/plan/starter/) als u dat nog niet hebt gedaan.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s die worden gebruikt in de bestemming Airship Tags. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Taggroepen

Het begrip publiek in het Adobe Experience Platorm lijkt op [Tags](https://docs.airship.com/guides/audience/tags/) in het luchtschip, met lichte verschillen in uitvoering. Deze integratie brengt de status van de gebruiker in kaart [lidmaatschap in een segment van de Experience Platform](../../../xdm/field-groups/profile/segmentation.md) aan de aanwezigheid of het ontbreken van een [!DNL Airship] -tag. Bijvoorbeeld in een publiek van het Platform waar `xdm:status` wijzigingen in `realized`, wordt de tag toegevoegd aan de [!DNL Airship] kanaal of benoemde gebruiker wordt dit profiel toegewezen aan. Als de `xdm:status` wijzigingen in `exited`, wordt de tag verwijderd.

Als u deze integratie wilt inschakelen, maakt u een *taggroep* in [!DNL Airship] benoemd `adobe-segments`.

>[!IMPORTANT]
>
>Wanneer u een nieuwe taggroep maakt **Niet controleren** het keuzerondje &quot;[!DNL Allow these tags to be set only from your server]&quot;. Als u dit doet, mislukt de integratie van Adobe-tags.

Zie [Taggroepen beheren](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) voor instructies over het maken van de taggroep.

## Dragertoken genereren

Ga naar **[!UICONTROL Settings]** &quot; **[!UICONTROL APIs & Integrations]** in de [Luchtvaartdashboard](https://go.airship.com) en selecteert u **[!UICONTROL Tokens]** in het linkermenu.

Klik op **[!UICONTROL Create Token]**.

Geef uw token een gebruikersvriendelijke naam, bijvoorbeeld Doel van Adobe-tags en selecteer Alle toegang voor de rol.

Klikken **[!UICONTROL Create Token]** en bewaren de gegevens als vertrouwelijk.

## Gebruiksscenario’s

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Airship Tags] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters gebruiken #1

De detailhandelaars of vermaak platforms kunnen gebruikersprofielen op hun loyaliteitklanten tot stand brengen en dat publiek overgaan in [!DNL Airship] voor berichten die gericht zijn op mobiele campagnes.

### Hoofdletters gebruiken #2

U kunt een-op-een berichten in real-time activeren wanneer gebruikers binnen of buiten een bepaald publiek in Adobe Experience Platform vallen.

Een detailhandelaar stelt bijvoorbeeld een specifiek publiek voor jeans op in Platform. Deze detailhandelaar kan nu een mobiel bericht activeren zodra iemand zijn jeans-voorkeur op een bepaald merk instelt.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Bearer token]**: het token dat u hebt gegenereerd op basis van het [!DNL Airship] dashboard.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: voer een naam in die u zal helpen deze bestemming te identificeren.
* **[!UICONTROL Description]**: voer een beschrijving in voor deze bestemming.
* **[!UICONTROL Domain]**: selecteer een Amerikaans of EU-datacenter, afhankelijk van welke [!DNL Airship] het gegevenscentrum is op deze bestemming van toepassing.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Toewijzingsoverwegingen {#mapping-considerations}

[!DNL Airship] -tags kunnen worden ingesteld op een kanaal dat apparaatinstantie vertegenwoordigt, bijvoorbeeld iPhone, of op een benoemde gebruiker, die alle apparaten van een gebruiker toewijst aan een gemeenschappelijke id, zoals een klant-id. Als u onbewerkte (niet-gehashte) e-mailadressen als primaire identiteit in uw schema hebt, selecteert u het e-mailveld in uw schema **[!UICONTROL Source Attributes]** en de kaart aan [!DNL Airship] benoemde gebruiker in de rechterkolom onder **[!UICONTROL Target Identities]**, zoals hieronder weergegeven.

![Toewijzing van benoemde gebruikers](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Voor herkenningstekens die aan een kanaal, d.w.z., een apparaat moeten worden in kaart gebracht, kaart aan het aangewezen kanaal dat op de bron wordt gebaseerd. In de volgende afbeeldingen ziet u hoe u een advertentie-id van Google toewijst aan een [!DNL Airship] Android-kanaal.

![Verbinden met luchtvaartcodes](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Verbinden met luchtvaartcodes](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Kanaaltoewijzing](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](../../../data-governance/home.md).
