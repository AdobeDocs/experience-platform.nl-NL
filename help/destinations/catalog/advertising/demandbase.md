---
title: Demandbase-verbinding
description: Gebruik dit doel om uw accountdoelgroepen te activeren voor gebruiksscenario's van Account-Based Marketing (ABM). Adverteer aan relevante personen en rollen in uw doelaccounts via het B2B Demand Side Platform (DSP) van DemandBase. Doelaccounts kunnen ook worden verrijkt met gegevens van derden van Demandbase, voor andere downstreamgebruiksscenario's in marketing en verkoop.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 08c2c7f5080f0e6afb7be53aad9f88ba0fccf923
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 15%

---

# Demandbase-verbinding {#demandbase}

>[!AVAILABILITY]
>
>>De functionaliteit om rekeningspubliek aan de bestemming van de Demandbase te activeren is beschikbaar voor bedrijven die [ zaken-aan-Zaken ](/help/rtcdp/overview.md#rtcdp-b2b) en [ zaken-aan-Persoon ](/help/rtcdp/overview.md#rtcdp-b2p) uitgaven van Real-Time Customer Data Platform kopen.

Activeer profielen voor uw campagnes van de Demandase voor publiek het richten, verpersoonlijking, en onderdrukking, die op [ worden gebaseerd rekeningspubliek ](/help/segmentation/types/account-audiences.md).

## Gebruiksscenario {#use-case}

Gebruik dit doel om uw accountdoelgroepen te activeren voor gebruiksscenario&#39;s van Account-Based Marketing (ABM). Adverteer aan relevante personen en rollen in uw doelaccounts via het B2B Demand Side Platform (DSP) van DemandBase. Doelaccounts kunnen ook worden verrijkt met gegevens van derden van Demandbase, voor andere downstreamgebruiksscenario&#39;s in marketing en verkoop.

Bijvoorbeeld, hefboomwerking de ad-tech DSP van Demandbase om specifieke persona&#39;s of rollen binnen zeer belangrijke rekeningen voor de productie van de top-of-funnel lood, of creeer en kweek koopgroepen. Gebruik de bestemming Demandbase om andere gebruiksgevallen te onderzoeken om uw rekeningen effectief te richten.

Met deze integratie kunt u de ervaring van de website ook personaliseren door accountinformatie in real-time op te zoeken om de betrokkenheid te optimaliseren.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | X | Het publiek [ ingevoerde ](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-and-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|--------------|-----------|---------------------------|
| Exporttype | Publiek exporteren | Alle publieksleden zullen met zeer belangrijke herkenningstekens zoals naam, telefoonaantal, en meer worden uitgevoerd. |
| Frequentie | Streaming | &quot;Altijd aan&quot; API-gebaseerde verbindingen. Updates worden direct na het wijzigen van het profiel verzonden. |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Als u accountsoorten wilt exporteren naar Demandbase, hebt u het volgende nodig:

1. Een Demandbase-account.
2. Een demandbase-API-token. U kunt een API-token met uw gebruiker genereren in de Demandbase. Om een teken te produceren, navigeer aan [ Mijn Profiel > Symbolisch API ](https://web.demandbase.com/o/ad/at) na het registreren in uw rekening van de Demandbase.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![ voeg dragertoken ](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png) toe

* **[!UICONTROL Bearer token]**: vul de token aan voor de toonder om te verifiëren bij het doel. Bekijk [ eerste vereisten ](#prerequisites) voor informatie over hoe te om het teken te verkrijgen.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ voegt informatie over de bestemmingsverbinding ](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png) toe

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Entity type]**: selecteer **[!UICONTROL Account]** als het entiteitstype.

Nu ben je klaar om je publiek te activeren in Demandbase.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer rekeningspubliek ](/help/destinations/ui/activate-account-audiences.md) voor instructies bij het activeren van rekeningspubliek aan deze bestemming.

## Aanvullende opmerkingen en belangrijke bijschriften {#additional-notes}

* Als een accountpubliek met dezelfde naam eerder is geactiveerd voor Demandbase, kunt u dit niet opnieuw activeren via een andere gegevensstroom naar de bestemming Demandbase.
* Als u het publiek naar de Demandbase hebt geëxporteerd en de exportbewerkingen in Experience Platform zijn geslaagd, maar niet alle gegevens in de Demandbase-indeling zijn bereikt, kan het zijn dat de API-vertraging aan de demandbase-zijde is opgetreden. Neem ze ter verduidelijking.
