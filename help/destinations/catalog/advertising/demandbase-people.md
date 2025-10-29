---
title: Demandbase People-verbinding
description: Gebruik deze bestemming om uw publiek te activeren en hen te verrijken met de gegevens van de derde partij van de Vraag, voor andere downstreamgebruik-gevallen in marketing en verkoop.
exl-id: 748f5518-7cc1-4d65-ab70-4a129d9e2066
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 1%

---

# Demandbase People-verbinding {#demandbase-people}

Activeer profielen voor uw Demandbase-campagnes voor doelgroepen, personalisatie en onderdrukking.

>[!IMPORTANT]
>
>Voor B2B gebruiksgevallen waar u rekeningspubliek [&#x200B; moet &#x200B;](../../ui/activate-account-audiences.md) activeren, gebruik in plaats daarvan de [&#x200B; Demandbase &#x200B;](demandbase.md) bestemmingsschakelaar.

## Gebruiksscenario {#use-case}

Marketers kunnen Adobe Real-Time CDP gebruiken om een lijst met personen van eerste-partijcontacten te maken en deze in Demandbase te activeren voor een geoptimaliseerde en georkestreerde betrokkenheid op het hele platform aan de vraagzijde (DSP) en op andere kanalen, zoals LinkedIn.

Op deze manier kunnen marketeers prioriteit geven aan campagneuitgaven voor bekende individuen die hun eigen CRM- of marketingautomatiseringssysteem gebruiken, waarbij ervoor wordt gezorgd dat de marketinginspanningen gericht zijn op hoogwaardige vooruitzichten.

Zodra geactiveerd, optimaliseert de Demandbase en levert het, raffineert het richten strategieën om betrokkenheid, bereik, en omzettingspercentages te maximaliseren, uiteindelijk verbeterend campagneefficiency.

## Ondersteunde identiteiten {#supported-identities}

De [!DNL Demandbase People] -verbinding ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email | E-mailadressen met normale tekst | Alleen e-mailadressen met normale tekst worden ondersteund door de [!DNL Demandbase People] -verbinding. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | X | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-and-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|--------------|-----------|---------------------------|
| Exporttype | Publiek exporteren | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de *bestemming van de Demandbase* worden gebruikt. |
| Frequentie | Streaming | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Om publiek naar Demandbase uit te voeren, hebt u het volgende nodig:

1. Een Demandbase-account.
2. Een demandbase-API-token. U kunt een API-token met uw gebruiker genereren in de Demandbase. Om een teken te produceren, navigeer aan [&#x200B; Mijn Profiel > Symbolisch API &#x200B;](https://web.demandbase.com/o/ad/at) na het registreren in uw rekening van de Demandbase.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![&#x200B; voeg dragertoken &#x200B;](../../assets/catalog/advertising/demandbase-people/bearer-token.png) toe

* **[!UICONTROL Bearer token]**: vul de token aan voor de toonder om te verifiëren bij het doel. Bekijk [&#x200B; eerste vereisten &#x200B;](#prerequisites) voor informatie over hoe te om het teken te verkrijgen.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; voegt informatie over de bestemmingsverbinding &#x200B;](../../assets/catalog/advertising/demandbase-people/name-and-description.png) toe

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

Nu ben je klaar om je publiek te activeren in Demandbase People.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Verplichte toewijzingen {#mandatory-mappings}

Wanneer u een publiek activeert naar de [!DNL Demandbase People] -bestemming, moet u de volgende verplichte veldtoewijzingen configureren in de toewijzingsstap:

| Source-veld | Doelveld | Beschrijving |
|--------------|--------------|-------------|
| `xdm: b2b.personKey.sourceKey` | `xdm: externalPersonId` | De unieke id van de persoon |
| `xdm: person.name.lastName` | `xdm: lastName` | De achternaam van de persoon |
| `xdm: person.name.firstName` | `xdm: firstName` | De voornaam van de persoon |
| `xdm: workEmail.address` | `Identity: email` | Het werk-e-mailadres van de persoon |

![&#x200B; De afbeeldingen van Mensen van de Demandbase &#x200B;](/help/destinations/assets/catalog/advertising/demandbase-people/demandbase-people-mapping.png)

Deze toewijzingen zijn vereist voor de bestemming behoorlijk te functioneren en moeten worden gevormd alvorens u met het activeringswerkschema kunt te werk gaan.

## Aanvullende opmerkingen en belangrijke bijschriften {#additional-notes}

* **Vereiste API begeleidingen**: Als u publiek naar Demandbase hebt uitgevoerd en de uitvoer succesvol in Experience Platform zijn, maar niet alle gegevens bereiken Demandbase, zou u API throttling op de BandBase kunnen ontmoet hebben. Neem ze ter verduidelijking.
* **schrapping van de Lijst**: De lijsten van Mensen zijn uniek, zodat kunt u geen nieuwe lijst met een naam opnieuw creëren reeds in gebruik. Wanneer u personen uit een lijst verwijdert, zijn deze niet meer beschikbaar, maar worden ze niet verwijderd.
* **de tijd van de Activering**: Het laden van gegevens in Demandbase is onderworpen aan overnight verwerking.
* **publiek noemend**: Als een rekeningspubliek met de zelfde naam vroeger aan Demandbase werd geactiveerd, kunt u het niet opnieuw door een verschillende dataflow aan de bestemming van de Demandbase activeren.
