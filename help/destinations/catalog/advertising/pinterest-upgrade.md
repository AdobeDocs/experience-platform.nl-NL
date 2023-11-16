---
title: Pinterest migratie naar nieuwe API. Actie van de klant is vereist.
description: Pinterest is bezig de API voor v4-adverteerders die momenteel door de Pinterest-bestemming in Real-Time CDP wordt gebruikt, te verouderen. Begrijp uw handelingspunten om naadloos overgang aan nieuwe API zonder onderbreking aan uw campagnes van Pinterest te maken.
hide: true
hidefromtoc: true
source-git-commit: dbbdb62c996466499b70990decba58ecaf1be901
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# Pinterest-doelupgrade naar nieuwe API. Actie van de klant vereist voor 15 december 2023

## Wat gebeurt er?

Pinterest heeft de versie4-API voor adverteerders die momenteel door de [Pinterest-bestemming](/help/destinations/catalog/advertising/pinterest.md) in Real-Time CDP. Adobe werkt met Pinterest en werkt de bestemming bij om de [v5-API voor adverteerders](https://developers.pinterest.com/docs/getting-started/migration/). Lees deze pagina om uw actiepunten te begrijpen zodat u naadloos over kunt schakelen naar de nieuwe API zonder uw Pinterest-campagnes te onderbreken.

## Waarom word ik op de hoogte gesteld?

We hebben vastgesteld dat uw organisatie actieve gegevensstromen heeft om het publiek naar Pinterest te activeren.

## Wat is het plan?

Adobe geeft een nieuwe Pinterest-doelkaart vrij die gebruikmaakt van de Pinterest API v5 en de bestaande gegevensstromen in de nieuwe verbinding behoudt.

## Moet ik iets doen om mijn actieve publiek te laten functioneren?

Ja, zodra de Adobe de upgrade heeft voltooid en de nieuwe Pinterest-bestemming heeft uitgebracht, moet u de verificatie opnieuw uitvoeren naar Pinterest met uw Pinterest-advertentieaccount in Real-Time CDP. Zie de gedetailleerde instructies hieronder.

### Opnieuw verifiëren bij Pinterest {#reauthenticate}

1. Ga naar **[!UICONTROL Destinations > Accounts]** en gebruik het filter op het scherm om alleen de Pinterest-bestemming te filteren.
   ![Alleen Pinterest-accounts filteren](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Op de **(Nieuw) Pinterest** doel, selecteert u het symbool met de drie punten... en selecteert u **[!UICONTROL Edit details]**.
   ![Details bewerken selecteren](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Selecteren **[!UICONTROL Reconnect OAuth]** en meld u aan bij uw Pinterest-account.
   ![Selecteer OAuth opnieuw verbinden](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Ga naar het actiepunt in de onderstaande sectie

### Bestaande stromen naar oude bestemming uitschakelen en stromen naar nieuwe bestemming inschakelen {#disable-old-enable-new-flows}

Dan moet u bestaande stromen aan de oude bestemmingskaart manueel onbruikbaar maken **[!UICONTROL (Deprecating) Pinterest]** en stromen naar de nieuwe kaart inschakelen **[!UICONTROL (New) Pinterest]**.

1. Ga naar **[!UICONTROL Destinations > Browse]** en gebruik het filter op het scherm om het filter **[!UICONTROL (New) Pinterest]** en **[!UICONTROL (Deprecating) Pinterest]** alleen bestemmingen.
   ![Pinterest-gegevensstromen alleen filteren op het tabblad Bladeren](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Selecteer de naam van de hyperlinkverbinding (de Loyalty-campagne in het bovenstaande voorbeeld) naar de **[!UICONTROL (Deprecating) Pinterest]** doel en schakel **[!UICONTROL Enable]** schakelen naar **uit**.
   ![Schakel in en uit voor nieuwe verbindingen](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-old-destination.png)
3. Selecteer de naam van de hyperlinkverbinding (de Loyalty-campagne in het bovenstaande voorbeeld) naar de **[!UICONTROL (New) Pinterest]** doel en schakel **[!UICONTROL Enable]** schakelen naar **op**.
   ![Schakel in en uit voor nieuwe verbindingen](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)
4. Vergelijk de geactiveerde publiekslijst in oude en nieuwe gegevensstroom en zorg ervoor dat u geen nieuw publiek in de oude stromen hebt die in de nieuwe stromen missen.

Hoewel er geen onderbrekingen in uw campagnes worden verwacht, moet u in de gebruikersinterface van Pinterest controleren of alles werkt zoals u had verwacht.

## Kunt u een aantal tijdlijnen op hoog niveau delen?

Ja, zie hieronder:

**Tegen 16 november 2023**: De nieuwe bestemming is klaar en u ziet twee Pinterest-kaarten naast elkaar in de catalogus. Alle bestaande gegevensstromen naar de huidige Pinterest-kaart worden naar de nieuwe bestemming gekopieerd.

![Oude en nieuwe Pinterest-bestemming naast elkaar](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Na 16 november 2023 is de Pinterest-bestemming van de nalatenschap gemarkeerd **[!UICONTROL Deprecating]**. <span class="preview">Om het even welke veranderingen die u aan dataflows aan de (Aftredende) bestemming van Pinterest na 16 november aanbrengt zullen *niet* automatisch worden overgedragen naar de nieuwe bestemming van Pinterest. </span>
>Wij *niet aanbevelen* dat u nieuw publiek aan de oude bestemming na 16 november activeert. Als u dat doet, zult u dan het [regelmatige activeringsstappen](/help/destinations/ui/activate-segment-streaming-destinations.md) om het publiek aan de nieuwe bestemming toe te voegen zodra de klantenacties worden genomen.

**Tegen 15 december 2023**: <span class="preview">Actie van de klant 1</span>. U dient opnieuw te worden geverifieerd op Pinterest, zodat de nieuwe kaart is aangesloten op Pinterest. Volledige instructies weergeven in [deze sectie](#reauthenticate).

<span class="preview">Actie 2 van de klant</span>.Dan, moet u de gegevensstromen aan Pinterest in de oude kaart onbruikbaar maken en de gegevensstromen in de nieuwe kaart toelaten. Volledige instructies weergeven in [deze sectie](#disable-old-enable-new-flows).

>[!IMPORTANT]
>
>Na 15 december 2023 garandeert Adobe de integriteit van gegevensstromen naar de oude **[!UICONTROL (Deprecating) Pinterest]** bestemming.

## Andere artikelen

Nadat u de dataflows op de nieuwe bestemmingskaart toelaat en de dataflows op de oude bestemmingskaarten onbruikbaar maakt, zou u geen verstoring in uw campagnes of in de aantallen gekwalificeerde profielen in het publiek moeten zien die uit Adobe Real-Time CDP komen.
