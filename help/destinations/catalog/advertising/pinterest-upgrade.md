---
title: Pinterest migratie naar nieuwe API. Actie van de klant is vereist.
description: Pinterest is bezig de API voor v4-adverteerders die momenteel door de Pinterest-bestemming in Real-Time CDP wordt gebruikt, te verouderen. Begrijp uw handelingspunten om naadloos overgang aan nieuwe API zonder onderbreking aan uw campagnes van Pinterest te maken.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: 3968c8e2a0ebd2084a7047fb41e2b85c5da7a6e7
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# Pinterest-doelupgrade naar nieuwe API. Actie van de klant vereist voor 18 januari 2024.

>[!IMPORTANT]
>
>De actiepunten van de klant op deze pagina zijn op u van toepassing als uw organisatie dataflows om gegevens naar Pinterest vóór 16 November 2023, de datum heeft geplaatst uit te voeren wanneer de nieuwe **[!UICONTROL Pinterest]** Doel, met de nieuwste Pinterest API, is toegevoegd aan de doelcatalogus.

## Wat gebeurt er?

Pinterest heeft de API voor v4-adverteerders die door de [Pinterest-bestemming](/help/destinations/catalog/advertising/pinterest.md) in Real-Time CDP. Adobe heeft de bestemming bijgewerkt om de [v5-API voor adverteerders](https://developers.pinterest.com/docs/getting-started/migration/). Lees deze pagina om uw actiepunten te begrijpen zodat u naadloos over kunt schakelen naar de nieuwe API zonder uw Pinterest-campagnes te onderbreken.

## Waarom word ik op de hoogte gesteld?

We hebben vastgesteld dat uw organisatie actieve gegevensstromen heeft om het publiek naar Pinterest te activeren.

## Wat is het plan?

Adobe geeft een nieuwe Pinterest-doelkaart vrij die gebruikmaakt van de Pinterest API v5 en de bestaande gegevensstromen in de nieuwe verbinding behoudt.

## Moet ik iets doen om mijn actieve publiek te laten functioneren?

Ja, voor 18 januari 2024 moet u zich verifiëren bij de nieuwe Pinterest-bestemming met uw Pinterest-advertentieaccount in Real-Time CDP. Zie de gedetailleerde instructies hieronder.

### Opnieuw verifiëren bij Pinterest {#reauthenticate}

1. Ga naar **[!UICONTROL Destinations > Accounts]** en gebruik het filter op het scherm om alleen de Pinterest-bestemming te filteren.
   ![Alleen Pinterest-accounts filteren](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Op de **Pinterest** doel, selecteert u het symbool met de drie punten... en selecteert u **[!UICONTROL Edit details]**.
   ![Details bewerken selecteren](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Selecteren **[!UICONTROL Reconnect OAuth]** en meld u aan bij uw Pinterest-account.
   ![Selecteer OAuth opnieuw verbinden](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Ga naar het actiepunt in de onderstaande sectie

### Stroom naar nieuwe bestemming inschakelen {#disable-old-enable-new-flows}

Vervolgens moet u de gegevensstroom naar de nieuwe kaart inschakelen **[!UICONTROL (New) Pinterest]**.

1. Ga naar **[!UICONTROL Destinations > Browse]** en gebruik het filter op het scherm om het filter **[!UICONTROL Pinterest]** alleen bestemming.
   ![Pinterest-gegevensstromen alleen filteren op het tabblad Bladeren](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Selecteer de naam van de hyperlinkverbinding (de Loyalty-campagne in het bovenstaande voorbeeld) naar de **[!UICONTROL Pinterest]** doel en schakel **[!UICONTROL Enable]** schakelen naar **op**.
   ![Schakel in en uit voor nieuwe verbindingen](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## Kunt u een aantal tijdlijnen op hoog niveau delen?

Ja, zie hieronder:

**Tegen 16 november 2023**: De nieuwe bestemming is klaar en u ziet twee Pinterest-kaarten naast elkaar in de catalogus totdat Pinterest stopt met de ondersteuning van de oude v4 API. Alle bestaande gegevens worden naar de huidige Pinterest-kaart gekopieerd.

![Oude en nieuwe Pinterest-bestemming naast elkaar](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Na 16 november 2023 is de Pinterest-bestemming van de nalatenschap gemarkeerd **[!UICONTROL Deprecating]**. <span class="preview">Om het even welke veranderingen die u aan dataflows aan de (Aftredende) bestemming van Pinterest na 16 november aanbrengt zullen *niet* automatisch worden overgedragen naar de nieuwe bestemming van Pinterest. </span>
>Wij *niet aanbevelen* dat u nieuw publiek aan de oude bestemming na 16 november activeert. Als u dat doet, zult u dan het [regelmatige activeringsstappen](/help/destinations/ui/activate-segment-streaming-destinations.md) om het publiek aan de nieuwe bestemming toe te voegen zodra de klantenacties worden genomen.

**Tegen 15 december 2023**: <span class="preview">Actie van de klant 1</span>. U dient opnieuw te worden geverifieerd op Pinterest, zodat de nieuwe kaart is aangesloten op Pinterest. Volledige instructies weergeven in [deze sectie](#reauthenticate).

<span class="preview">Actie 2 van de klant</span>.Dan, moet u de gegevensstromen aan Pinterest in de oude kaart onbruikbaar maken en de gegevensstromen in de nieuwe kaart toelaten. Volledige instructies weergeven in [deze sectie](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**Na 18 januari 2024**: <span class="preview">Pinterest heeft de toegang tot de V4-API voor adverteerders uitgeschakeld. Om het even welke klanten van Real-Time CDP die niet aan de nieuwe bestemming hebben bevorderd zullen nu hun gegevensstromen aan de bestemming van Pinterest ontbreken. [Opnieuw verifiëren bij Pinterest](#reauthenticate) en [de gegevensstromen inschakelen](#disable-old-enable-new-flows) naar de bijgewerkte bestemming om uw campagnes naar Pinterest te hervatten</span>.

## Andere artikelen

Nadat u de dataflows op de nieuwe bestemmingskaart toelaat en de dataflows op de oude bestemmingskaarten onbruikbaar maakt, zou u geen verstoring in uw campagnes of in de aantallen gekwalificeerde profielen in het publiek moeten zien die uit Adobe Real-Time CDP komen.
