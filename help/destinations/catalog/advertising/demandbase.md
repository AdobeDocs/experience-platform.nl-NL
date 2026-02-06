---
title: Demandbase-verbinding
description: Gebruik dit doel om uw accountdoelgroepen te activeren voor gebruiksscenario's van Account-Based Marketing (ABM). Adverteer aan relevante personen en rollen in uw doelaccounts via het B2B Demand Side Platform (DSP) van DemandBase. Doelaccounts kunnen ook worden verrijkt met gegevens van derden van Demandbase, voor andere downstreamgebruiksscenario's in marketing en verkoop.
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 044306709747c32c4ce265d03d3908bbae169edc
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 13%

---

# Demandbase-verbinding {#demandbase}

>[!AVAILABILITY]
>
>De functionaliteit om rekeningspubliek aan de bestemming van de Demandbase te activeren is beschikbaar voor bedrijven die [ zaken-aan-Zaken ](/help/rtcdp/overview.md#rtcdp-b2b) en [ zaken-aan-Persoon ](/help/rtcdp/overview.md#rtcdp-b2p) uitgaven van Real-Time Customer Data Platform kopen.

Activeer profielen voor uw campagnes van de Demandase voor publiek het richten, verpersoonlijking, en onderdrukking, die op [ worden gebaseerd rekeningspubliek ](/help/segmentation/types/account-audiences.md).

## Gebruiksscenario {#use-case}

Gebruik dit doel om uw accountdoelgroepen te activeren voor gebruiksscenario&#39;s van Account-Based Marketing (ABM). Adverteer aan relevante personen en rollen in uw doelaccounts via het B2B Demand Side Platform (DSP) van DemandBase. Doelaccounts kunnen ook worden verrijkt met gegevens van derden van Demandbase, voor andere downstreamgebruiksscenario&#39;s in marketing en verkoop.

Zo kunt u bijvoorbeeld de ad-tech DSP van Demandbase gebruiken om specifieke personen of rollen binnen sleutelaccounts te richten voor het genereren van leads van top-of-funnel, of koopgroepen maken en uitbreiden. Gebruik de bestemming Demandbase om andere gebruiksgevallen te onderzoeken om uw rekeningen effectief te richten.

Met deze integratie kunt u de ervaring van de website ook personaliseren door accountinformatie in real-time op te zoeken om de betrokkenheid te optimaliseren.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
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

### Verplichte toewijzingen {#mandatory-mappings}

Wanneer u een publiek activeert naar de [!DNL Demandbase] -bestemming, moet u de volgende verplichte veldtoewijzingen configureren in de toewijzingsstap:

| Source-veld | Doelveld | Beschrijving |
|--------------|--------------|-------------|
| `xdm: accountName` | `xdm: accountName` | De naam van de account |
| `xdm: accountOrganization.domain` | `xdm: accountEmailDomain` | Het e-maildomein van de accountorganisatie |
| `xdm: accountKey.sourceKey` | `Identity: primaryId` | De primaire identificatiecode van de rekening |

![ Vereiste basisafbeeldingen ](/help/destinations/assets/catalog/advertising/demandbase/demandbase-mapping.png)

Deze toewijzingen zijn vereist voor de bestemming behoorlijk te functioneren en moeten worden gevormd alvorens u met het activeringswerkschema kunt te werk gaan.

## Aanvullende opmerkingen en belangrijke bijschriften {#additional-notes}

* **publiek noemend**: Als een rekeningspubliek met de zelfde naam vroeger aan Demandbase werd geactiveerd, kunt u het niet opnieuw door een verschillende dataflow aan de bestemming van de Demandbase activeren.
* **Vereiste API begeleidingen**: Als u publiek naar Demandbase hebt uitgevoerd en de uitvoer succesvol in Experience Platform zijn, maar niet alle gegevens bereiken Demandbase, zou u API throttling op de BandBase kunnen ontmoet hebben. Neem ze ter verduidelijking.
* **schrapping van de Lijst**: De lijsten van de rekening zijn uniek, zodat kunt u geen nieuwe lijst met een naam opnieuw creëren reeds in gebruik. Als u accounts uit een lijst verwijdert, zijn ze niet meer beschikbaar, maar worden ze niet verwijderd.
* **de tijd van de Activering**: Het laden van gegevens in Demandbase is onderworpen aan overnight verwerking.
