---
title: TikTok-verbinding
description: Bouw een aangepast publiek op TikTok met uw gegevens voor doelgerichte advertentiecampagnes. Dit soort publiek zou kunnen bestaan uit mensen die uw website hebben bezocht of interactie hebben gehad met uw inhoud. Snel en veilig het gewenste publiek van Adobe Experience Platform naar TikTok sturen met behulp van Adobe real-time integratie met TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# TikTok-verbinding

## Overzicht {#overview}

Bouw een aangepast publiek op TikTok met uw gegevens voor doelgerichte advertentiecampagnes. Dit soort publiek zou kunnen bestaan uit mensen die uw website hebben bezocht of interactie hebben gehad met uw inhoud. Snel en veilig het gewenste publiek van Adobe Experience Platform naar TikTok sturen met behulp van Adobe real-time integratie met TikTok Ads Manager. Bezoek [TikTok Business Help Center](https://ads.tiktok.com/help/article/audiences?lang=en) voor meer informatie .

>[!IMPORTANT]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het TikTok-team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van TikTok zou moeten gebruiken, is hier een voorbeeld gebruiksgeval voor klanten van Adobe Experience Platform.

### Gebruiksscenario {#use-case-1}

Een atletisch merk kledingartikelen wil bestaande klanten bereiken via hun sociale-mediakanalen. Het merk apparel kan e-mailadressen van zijn eigen CRM aan Adobe Experience Platform opnemen, publiek maken van zijn eigen offline gegevens en deze soorten publiek naar TikTok sturen om advertenties weer te geven in de sociale media van hun klanten.

## Vereisten {#prerequisites}

Voordat u gegevens naar uw [!DNL TikTok Ads Manager] -account, moet je Adobe Experience Platform toestemming geven om je advertentieaccount te openen voor `Audience Management`. U kunt deze machtiging opgeven door uw adverteerder-id in te voeren in het Experience Platform en de machtiging opnieuw te sturen om de machtiging te verlenen. Meer instructies vindt u in het gedeelte [TikTok API-documentatie](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## Ondersteunde identiteiten {#supported-identities}

TikTok ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | Google-advertentie-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| Telefoonnummer | Telefoonnummers die zijn hashed met het SHA256-algoritme | Onbewerkte tekst en gehashte telefoonnummers van SHA256 worden ondersteund door Adobe Experience Platform en moeten de indeling E.164 hebben. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| Email | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de TikTok-bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Om voor authentiek te verklaren aan de bestemming, zult u aan login aan uw worden opnieuw gericht [!DNL TikTok Ads Manager] account en geef Adobe toestemming om namens u het publiek te beheren.

![Selectie TikTok-machtiging](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Afbeelding van TikTok-gebruikersinterface voor het selecteren van machtigingen")

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Gegevens doelverbinding](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Afbeelding van de interface van het Platform, met gegevens over de doelverbinding die moeten worden ingevuld")

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL TikTok Ads Manager ID]**: Uw [!DNL TikTok Ads Manager ID]. U kunt dit vinden in uw [!DNL TikTok Ads manager] account.

![TikTok Ads Manager-id](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Afbeelding van de gebruikersinterface van TikTok Ads Manager en tonen hoe u de TikTok Ads Manager-id kunt ophalen")

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Identiteiten toewijzen {#map}

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het exporteren van soorten publiek naar TikTok Ads Manager.

Bronvelden selecteren:

* Selecteer een id (bijvoorbeeld:` Email_LC_SHA256`) als bronidentiteit die een profiel in Adobe Experience Platform uniek identificeert en [!DNL TikTok Ads Manager].

Doelvelden selecteren:

* Selecteer de naamruimte E-mail als doel-id.

![Identiteitskaart](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Afbeelding van de interface van het Platform, toewijzen van identiteiten")

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL TikTok Ads Manager] rekening (onder **Middelen > Soorten publiek**) om te controleren of het publiek van uw Experience Platform is geëxporteerd. Het publiek wordt gevuld met een type publiek: `Partner Audience`.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Raadpleeg de [TikTok Help Center-pagina](https://ads.tiktok.com/help/article/audiences?lang=en) voor aanvullende informatie.
