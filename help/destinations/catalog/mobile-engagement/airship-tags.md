---
keywords: luchtschepen, codes;bestemming van het luchtschip
title: Koppeling met vliegtuigcodes
description: Geef naadloos Adobe Audience Data door aan het luchtschip als Publiek Tags om zich binnen het luchtschip te richten.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---

# [!DNL Airship Tags]-verbinding {#airship-tags-destination}

## Overzicht

[!DNL Airship] is het toonaangevende platform voor betrokkenheid van klanten, waarmee u in elke fase van de levenscyclus van de klant betekenisvolle, gepersonaliseerde omnichannel berichten voor uw gebruikers kunt leveren.

Deze integratie gaat de publieksgegevens van Adobe Experience Platform in [!DNL Airship] als [ Markeringen ](https://docs.airship.com/guides/audience/tags/) voor het richten van of het teweegbrengen over.

Meer over [!DNL Airship] leren, zie [ Dokken van het Luchtschip ](https://docs.airship.com).


>[!TIP]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Airship] . Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct bij [ support.airship.com ](https://support.airship.com/) te contacteren.

## Vereisten

Voordat u uw Adobe Experience Platform-publiek naar [!DNL Airship] kunt sturen, moet u:

* Maak een taggroep in uw [!DNL Airship] -project.
* Een token voor toonder genereren voor verificatie.

>[!TIP]
> 
>Creeer een [!DNL Airship] rekening via [ deze signaleringsverbinding ](https://go.airship.eu/accounts/register/plan/starter/) als u niet reeds hebt.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s die worden gebruikt in de bestemming Airship Tags. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Taggroepen

Het concept publiek in het Platform van de Ervaring van Adobe is gelijkaardig aan [ Markeringen ](https://docs.airship.com/guides/audience/tags/) in Luchtschip, met lichte verschillen in implementatie. Deze integratie brengt het statuut van een gebruiker [ lidmaatschap in een segment van Experience Platform ](../../../xdm/field-groups/profile/segmentation.md) aan de aanwezigheid of de afwezigheid van een [!DNL Airship] markering in kaart. In een Experience Platform-publiek waar `xdm:status` verandert in `realized` , wordt de tag bijvoorbeeld toegevoegd aan het [!DNL Airship] -kanaal of aan een benoemde gebruiker wordt dit profiel toegewezen. Als de `xdm:status` verandert in `exited` , wordt de tag verwijderd.

Om deze integratie toe te laten, creeer de groep van de a *markering* in [!DNL Airship] genoemd `adobe-segments`.

>[!IMPORTANT]
>
>Wanneer het creëren van uw nieuwe markeringsgroep **controleert** niet het radioknoop dat &quot; [!DNL Allow these tags to be set only from your server]&quot;zegt. Als u dit doet, mislukt de integratie van Adobe-tags.

Zie [ Leiden de Groepen van de Markering ](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) voor instructies bij het creëren van de markeringsgroep.

## Dragertoken genereren

Ga naar **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** in [ het dashboard van het Luchtschip ](https://go.airship.com) en selecteer **[!UICONTROL Tokens]** in het linkermenu.

Klik op **[!UICONTROL Create Token]**.

Geef uw token een gebruikersvriendelijke naam, bijvoorbeeld &quot;Doel Adobe-tags&quot;, en selecteer &quot;All Access&quot; voor de rol.

Klik op **[!UICONTROL Create Token]** en sla de details op als vertrouwelijk.

## Gebruiksscenario’s

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Airship Tags] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Hoofdletters gebruiken #1

Detailhandelaars of entertainmentplatforms kunnen gebruikersprofielen maken voor hun klanten die aan hun verplichtingen voldoen en die doelgroepen doorgeven aan [!DNL Airship] voor berichten die bestemd zijn voor mobiele campagnes.

### Hoofdletters gebruiken #2

U kunt een-op-een berichten in real-time activeren wanneer gebruikers binnen of buiten een bepaald publiek in Adobe Experience Platform vallen.

Een retailer vestigt bijvoorbeeld een specifiek publiek voor jeans in Experience Platform. Dat retailer nu een mobiel bericht kan activeren zodra iemand zijn jeans-voorkeur instelt op een bepaald merk.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

* **[!UICONTROL Bearer token]** : het token dat u hebt gegenereerd op het dashboard van [!DNL Airship] .

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: voer een naam in die u helpt bij het identificeren van dit doel.
* **[!UICONTROL Description]** : voer een beschrijving in voor dit doel.
* **[!UICONTROL Domain]**: selecteer een Amerikaans of EU-datacenter, afhankelijk van welk [!DNL Airship] -datacenter op dit doel van toepassing is.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Zie [ publieksgegevens aan het stromen publiek de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Toewijzingsoverwegingen {#mapping-considerations}

[!DNL Airship] -tags kunnen worden ingesteld op een kanaal dat apparaatinstantie vertegenwoordigt, bijvoorbeeld iPhone, of een benoemde gebruiker, die alle apparaten van een gebruiker toewijst aan een gemeenschappelijke id, zoals een klant-id. Als u normale (niet-gehashte) e-mailadressen als primaire identiteit in uw schema hebt, selecteert u het e-mailveld in uw **[!UICONTROL Source Attributes]** en wijst u deze toe aan de [!DNL Airship] benoemde gebruiker in de rechterkolom onder **[!UICONTROL Target Identities]** , zoals hieronder wordt weergegeven.

![ Benoemde Toewijzing van de Gebruiker ](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Voor herkenningstekens die aan een kanaal, d.w.z., een apparaat moeten worden in kaart gebracht, kaart aan het aangewezen kanaal dat op de bron wordt gebaseerd. In de volgende afbeeldingen ziet u hoe u een Google Advertising-id toewijst aan een [!DNL Airship] Android-kanaal.

![ verbind met de Markeringen van het Luchtschip ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![ verbind met de Markeringen van het Luchtschip ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![ Toewijzing van het Kanaal ](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie [ Overzicht van de Governance van Gegevens ](../../../data-governance/home.md).
