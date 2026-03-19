---
title: Bombora ABM Audiences-verbinding
description: Activeer profielen voor uw Bombora-campagnes voor doelgroepen, personalisatie en onderdrukking, op basis van accountpubliek.
exl-id: a2f8e399-e192-4104-876a-fe60f8403143
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# Bombora ABM Audiences-verbinding {#bombora}

>[!AVAILABILITY]
>
>De functionaliteit om rekeningspubliek aan de bestemming van het publiek van Bombora te activeren ABM is beschikbaar voor bedrijven die [ zaken-aan-Zaken ](/help/rtcdp/overview.md#rtcdp-b2b) en [ zaken-aan-Persoon ](/help/rtcdp/overview.md#rtcdp-b2p) uitgaven van Real-Time Customer Data Platform kopen.

Activeer profielen voor uw campagnes Bombora voor publiek gericht, verpersoonlijking, en onderdrukking, die op [ worden gebaseerd rekeningspubliek ](/help/segmentation/types/account-audiences.md).

## Gebruiksscenario&#39;s {#use-case}

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
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [ diverse publieksoorsprong ](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-apps, zoals Adobe Journey Optimizer; </li><li> en meer. </li></ul> |

{style="table-layout:auto"}

Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [ het publiek van Mensen ](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [ publiek van de Rekening ](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [ Het publiek van het Vooruitzicht ](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [ de uitvoer van de Dataset ](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het Data Lake van Adobe Experience Platform. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Ondersteunde identiteiten {#supported-identities}

Voor Bombora moet de doelidentiteit worden toegewezen die in de onderstaande tabel wordt beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| `primaryId` | Bombora vereist het in kaart brengen van deze doelidentiteit voor de integratie correct te werken. U kunt elk bronveld toewijzen aan deze identiteit. Deze toewijzing is verplicht, maar exporteert geen gegevens naar Bombora. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-and-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Bombora] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Als u accountpubliek wilt exporteren naar Bombora, hebt u de volgende informatie nodig.

1. Een Bombora-account. Als u geen hebt, kunt u om een rekening verzoeken Bombora gebruikend de [ Bombora vorm van de het publiekactivering van het publiek van Bombora ](https://customers.bombora.com/artcdp/audience-activation-request).
2. Een Bombora **[!UICONTROL client ID]** en **[!UICONTROL client secret]** .
3. De gegevens die naar Bombora worden verzonden moeten van datasets zijn die **profiel-toegelaten** zijn, zodat is de dataset inbegrepen in Profiel. Zorg ervoor dat uw datasets [ voor Profiel ](/help/catalog/datasets/enable-for-profile.md) worden toegelaten alvorens publiek aan deze bestemming te activeren.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![ voeg dragertoken ](../../assets/catalog/advertising/bombora/add-bearer-token.png) toe

* **[!UICONTROL Client ID]**: voer uw [!DNL Bombora] client-id in.
* **[!UICONTROL Client secret]**: voer het [!DNL Bombora] -clientgeheim in.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ voegt informatie over de bestemmingsverbinding ](../..//assets/catalog/advertising/bombora/name-and-description.png) toe

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

Nu ben je klaar om je publiek in Bombora te activeren.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer rekeningspubliek ](/help/destinations/ui/activate-account-audiences.md) voor instructies bij het activeren van rekeningspubliek aan deze bestemming.

### Verplichte toewijzingen {#mapping}

De bestemming Bombora vereist u om de volgende afbeeldingen voor succesvolle gegevensactivering te vormen.

| Source-veld | Doelveld | Beschrijving |
|---------|----------|---------|
| Willekeurige waarde | `Identity: primaryId` | Deze koppeling is verplicht voor Experience Platform om een verbinding met Bombora tot stand te brengen. Deze waarde wordt niet geëxporteerd naar Bombora, maar is vereist voor de doelconfiguratie. U kunt elk kenmerk voor het bronveld selecteren. |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora gebruikt website- of domeinadressen om een accountlijst te maken. |

![ voeg verplichte afbeeldingen ](../..//assets/catalog/advertising/bombora/mappings.png) toe

## Synchronisatiegedrag van publiek {#sync-behavior}

Na de eerste activering van het publiek worden updates voor het publiek in Experience Platform incrementeel gesynchroniseerd met Bombora. De volgende gedragingen zijn van toepassing:

* **die Rekening aan het publiek** wordt toegevoegd: Wanneer een rekening aan het publiek in Experience Platform wordt toegevoegd, wordt het automatisch toegevoegd aan het overeenkomstige publiek in Bombora.
* **verwijderde Rekening of kwalificeert niet meer**: Wanneer een rekening niet meer voor het publiek kwalificeert of uit het publiek in Experience Platform wordt verwijderd, wordt het verwijderd uit het overeenkomstige publiek in Bombora.
* **verwijderde Rekening of profiel**: Wanneer een rekening of een profiel van Experience Platform wordt geschrapt en die rekening niet meer voor het publiek kwalificeert, wordt het verwijderd uit het overeenkomstige publiek in Bombora.

### Het gedrag van de Auditie schrapen en losmaken {#deletion-disconnect}

Als u een publiek in Experience Platform verwijdert of een publiek uit een Bombora-activeringsgegevensstroom verwijdert, verwijdert u het publiek uit uw Bombora-account.

## Aanvullende opmerkingen en belangrijke bijschriften {#additional-notes}

Als een accountpubliek met dezelfde naam eerder voor Bombora is geactiveerd, wordt er een fout weergegeven als u dit opnieuw probeert te activeren via een andere gegevensstroom naar de Bombora-bestemming.
