---
title: Pinterest migratie naar nieuwe API. Actie van de klant is vereist.
description: Pinterest is bezig de API voor v4-adverteerders die momenteel door de Pinterest-bestemming in Real-Time CDP wordt gebruikt, te verouderen. Begrijp uw handelingspunten om naadloos overgang aan nieuwe API zonder onderbreking aan uw campagnes van Pinterest te maken.
hide: true
hidefromtoc: true
source-git-commit: 10bf63677c66366c226d647b1174093c1704a8b9
workflow-type: tm+mt
source-wordcount: '697'
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

Ja, zodra de Adobe de upgrade heeft voltooid (bedoeld op 16 november), moet u opnieuw verifiëren bij Pinterest met uw Pinterest-advertentieaccount in Adobe Experience Platform. Zie de gedetailleerde instructies hieronder.

### Opnieuw verifiëren bij Pinterest {#reauthenticate}

1. Ga naar **[!UICONTROL Destinations > Accounts]** en gebruik het filter op het scherm om alleen de Pinterest-bestemming te filteren.
   ![Alleen Pinterest-accounts filteren](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Op de **(Nieuw) Pinterest** doel, selecteert u het symbool met de drie punten... en selecteert u **[!UICONTROL Edit details]**.
   ![Details bewerken selecteren](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Selecteren **[!UICONTROL Reconnect OAuth]** en meld u aan bij uw Pinterest-account.
   ![Selecteer OAuth opnieuw verbinden](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Laat de Adobe weten dat u opnieuw geautoriseerd bent aan de **[!UICONTROL (New) Pinterest]** bestemming.

### Bestaande stromen naar oude bestemming uitschakelen en stromen naar nieuwe bestemming inschakelen {#disable-old-enable-new-flows}

Vervolgens moet u bestaande stromen naar de oude kaart handmatig uitschakelen en stromen naar de nieuwe kaart inschakelen.

>[!IMPORTANT]
>
>Nadat u opnieuw hebt geverifieerd, kunt u naar de Adobe reiken en zullen wij deze tweede stap voor u uitvoeren. Voer de onderstaande stappen uit als u deze stap liever handmatig wilt uitvoeren:

1. Ga naar **[!UICONTROL Destinations > Browse]** en gebruik het filter op het scherm om het filter **[!UICONTROL (New) Pinterest]** en **[!UICONTROL (Deprecating) Pinterest]** alleen bestemmingen.
   ![Pinterest-gegevensstromen alleen filteren op het tabblad Bladeren](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Selecteer de naam van de hyperlinkverbinding (Loyalty-campagne in het bovenstaande voorbeeld) en schakel de optie **[!UICONTROL Enable]** schakelen naar **uit** voor de oude verbinding en **op** voor de nieuwe verbinding.
   ![Schakel in en uit voor nieuwe verbindingen](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle.png)
3. Vergelijk de geactiveerde publiekslijst in oude en nieuwe gegevensstroom en zorg ervoor dat u geen nieuw publiek in de oude stromen hebt die in de nieuwe stromen missen.

Hoewel er geen onderbrekingen in uw campagnes worden verwacht, moet u in de gebruikersinterface van Pinterest controleren of alles werkt zoals u had verwacht.

## Kunt u een aantal tijdlijnen op hoog niveau delen?

Ja, zie hieronder:

**Uiterlijk 16 november**: De nieuwe bestemming is klaar en u ziet twee Pinterest-kaarten naast elkaar in de catalogus. Alle bestaande gegevensstromen naar de huidige Pinterest-kaart worden naar de nieuwe bestemming gekopieerd.

![Oude en nieuwe Pinterest-bestemming naast elkaar](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Na 16 november, is de erfenisbestemming van Pinterest duidelijk **[!UICONTROL Deprecating]**. <span class="preview">Om het even welke veranderingen die u aan dataflows aan de (Aftredende) bestemming van Pinterest na 16 november aanbrengt zullen *niet* automatisch worden overgedragen naar de nieuwe bestemming van Pinterest. </span>
>Wij *niet aanbevelen* dat u nieuw publiek aan de oude bestemming na 16 november activeert. Als u dat doet, zult u dan het [regelmatige activeringsstappen](/help/destinations/ui/activate-segment-streaming-destinations.md) om het publiek aan de nieuwe bestemming toe te voegen zodra de klantenacties worden genomen.

**Uiterlijk op 15 december**: <span class="preview">Klantenactie</span>. U moet opnieuw verifiëren op Pinterest zodat de nieuwe kaart is aangesloten op Pinterest (instructies hierboven). Als u dat hebt gedaan, richt u ons dan tot u.

De gegevensstromen naar Pinterest op de oude kaart moeten worden uitgeschakeld en de gegevens op de nieuwe kaart moeten worden ingeschakeld. U kunt dat handmatig doen in de gebruikersinterface, of u kunt naar de Adobe reiken en dat zullen we voor u doen.

## Andere artikelen

Nadat u de dataflows op de nieuwe bestemmingskaart toelaat en de dataflows op de oude bestemmingskaarten onbruikbaar maakt, zou u geen verstoring in uw campagnes of in de aantallen gekwalificeerde profielen in het publiek moeten zien die uit Adobe Real-Time CDP komen.
