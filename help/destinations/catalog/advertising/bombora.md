---
title: Bombora-verbinding
description: Activeer profielen voor uw Bombora-campagnes voor doelgroepen, personalisatie en onderdrukking, op basis van accountpubliek.
exl-id: a2f8e399-e192-4104-876a-fe60f8403143
source-git-commit: 044306709747c32c4ce265d03d3908bbae169edc
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# Bombora-verbinding {#bombora}

>[!AVAILABILITY]
>
>De functionaliteit om rekeningspubliek aan de bestemming van Bombora te activeren is beschikbaar voor bedrijven die [&#x200B; zaken-aan-Zaken &#x200B;](/help/rtcdp/overview.md#rtcdp-b2b) en [&#x200B; zaken-aan-Persoon &#x200B;](/help/rtcdp/overview.md#rtcdp-b2p) uitgaven van Real-Time Customer Data Platform kopen.

Activeer profielen voor uw campagnes Bombora voor publiek gericht, verpersoonlijking, en onderdrukking, die op [&#x200B; worden gebaseerd rekeningspubliek &#x200B;](/help/segmentation/types/account-audiences.md).

## Gebruiksscenario’s {#use-case}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming zou moeten gebruiken Bombora, zijn hier de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### DSP-integratie {#dsp-integration}

Als een B2B-markering kunt u een accountlijst in Real-Time CDP maken, waarbij bedrijven worden geïdentificeerd die hoge intenties voor uw producten tonen. Vervolgens kunt u deze bestemming gebruiken om deze lijst in Bombora te activeren.

Door de integratie van Bombora met DSPs kunt u gerichte advertentiecampagnes in werking stellen gebruikend gegevens Bombora. Zo weet u zeker dat uw advertentie-uitgaven vooral gericht zijn op bedrijven die het meest waarschijnlijk zullen converteren.

### Account-Based Marketing {#abm}

Als B2B-markeerteken kunt u een accountlijst maken op basis van CRM- en marketingsignalen. Dan, kunt u deze bestemming gebruiken om deze lijst in Bombora te activeren, waar ABM-bewuste controles u helpen besluitvormers bij deze bedrijven richten.

### Meerkanaals account-gebaseerde marketingactivering {#multi-channel-abm}

Als B2B-markeerteken kunt u een accountlijst maken in Real-Time CDP, waarbij bedrijven met een hoge intentie worden geïdentificeerd. Vervolgens kunt u deze bestemming gebruiken om de lijst in Bombora te activeren en doelgerichte campagnes op meerdere kanalen uit te voeren.

Op betaalde sociale media kunt u persoonlijke advertenties leveren aan professionals op doelaccounts op platforms als [!DNL LinkedIn] en [!DNL Facebook] . Met native advertentieplatforms kunt u ervoor zorgen dat de inhoud relevante besluitvormers bereikt.

U kunt campagnes ook uitbreiden naar geavanceerde tv en advertenties leveren aan belangrijke accounts.

Deze multikanaalsbenadering zorgt voor consistent overseinen op verschillende platforms, waarbij de betrokkenheid en conversietarieven worden gemaximaliseerd.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | X | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Ondersteunde identiteiten {#supported-identities}

Voor Bombora moet de doelidentiteit worden toegewezen die in de onderstaande tabel wordt beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| `primaryId` | Bombora vereist het in kaart brengen van deze doelidentiteit voor de integratie correct te werken. U kunt elk bronveld toewijzen aan deze identiteit. Deze toewijzing is verplicht, maar exporteert geen gegevens naar Bombora. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-and-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Bombora] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Als u accountpubliek wilt exporteren naar Bombora, hebt u de volgende informatie nodig.

1. Een Bombora-account.
2. Een Bombora **[!UICONTROL client ID]** en **[!UICONTROL client secret]** .

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![&#x200B; voeg dragertoken &#x200B;](../../assets/catalog/advertising/bombora/add-bearer-token.png) toe

* **[!UICONTROL Client ID]**: voer uw [!DNL Bombora] client-id in.
* **[!UICONTROL Client secret]**: voer het [!DNL Bombora] -clientgeheim in.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; voegt informatie over de bestemmingsverbinding &#x200B;](../..//assets/catalog/advertising/bombora/name-and-description.png) toe

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

Nu ben je klaar om je publiek in Bombora te activeren.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer rekeningspubliek &#x200B;](/help/destinations/ui/activate-account-audiences.md) voor instructies bij het activeren van rekeningspubliek aan deze bestemming.

### Verplichte toewijzingen {#mapping}

De bestemming Bombora vereist u om de volgende afbeeldingen voor succesvolle gegevensactivering te vormen.



| Source-veld | Doelveld | Beschrijving |
|---------|----------|---------|
| Willekeurige waarde | `Identity: primaryId` | Deze koppeling is verplicht voor Experience Platform om een verbinding met Bombora tot stand te brengen. Deze waarde wordt niet geëxporteerd naar Bombora, maar is vereist voor de doelconfiguratie. U kunt elk kenmerk voor het bronveld selecteren. |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora gebruikt website- of domeinadressen om een accountlijst te maken. |

![&#x200B; voeg verplichte afbeeldingen &#x200B;](../..//assets/catalog/advertising/bombora/mappings.png) toe


## Aanvullende opmerkingen en belangrijke bijschriften {#additional-notes}

Als een accountpubliek met dezelfde naam eerder voor Bombora is geactiveerd, wordt er een fout weergegeven als u dit opnieuw probeert te activeren via een andere gegevensstroom naar de Bombora-bestemming.
