---
title: Pinterest migratie naar nieuwe API. Actie van de klant is vereist.
description: Pinterest is bezig de API voor v4-adverteerders die momenteel door de Pinterest-bestemming in Real-Time CDP wordt gebruikt, te verouderen. Begrijp uw handelingspunten om naadloos overgang aan nieuwe API zonder onderbreking aan uw campagnes van Pinterest te maken.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: e3341ec6f62844858ecda7dd4db70d085f0bf217
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Pinterest-doelupgrade naar nieuwe API. Actie van de klant vereist voor 18 januari 2024.

>[!IMPORTANT]
>
>De actiepunten van de klant op deze pagina zijn op u van toepassing als uw organisatie dataflows om gegevens naar Pinterest vóór 16 november 2023, de datum heeft geplaatst uit te voeren toen nieuwe **[!UICONTROL Pinterest]** bestemming, gebruikend recentste Pinterest API, aan de bestemmingscatalogus werd toegevoegd.

## Wat gebeurt er?

Pinterest heeft v4 adverteerder API verouderd die door de [ bestemming van Pinterest ](/help/destinations/catalog/advertising/pinterest.md) in Real-Time CDP werd gebruikt. De Adobe werkte de bestemming bij om [ v5 adverteerder API ](https://developers.pinterest.com/docs/getting-started/migration/) te gebruiken. Lees deze pagina om uw actiepunten te begrijpen zodat u naadloos over kunt schakelen naar de nieuwe API zonder uw Pinterest-campagnes te onderbreken.

## Waarom word ik op de hoogte gesteld?

We hebben vastgesteld dat uw organisatie actieve gegevensstromen heeft om het publiek naar Pinterest te activeren.

## Wat is het plan?

Adobe heeft een nieuwe Pinterest-doelkaart uitgebracht die gebruikmaakt van de Pinterest API v5 en de bestaande gegevensstromen in de nieuwe verbinding behoudt.

## Moet ik iets doen om mijn actieve publiek te laten functioneren?

Ja, voor 18 januari 2024 moet u zich verifiëren bij de nieuwe Pinterest-bestemming met uw Pinterest-advertentieaccount in Real-Time CDP. Zie de gedetailleerde instructies hieronder.

### Opnieuw verifiëren bij Pinterest {#reauthenticate}

1. Ga naar **[!UICONTROL Destinations > Accounts]** en gebruik het filter op het scherm om alleen de Pinterest-bestemming te filteren.
   ![ slechts de rekeningen van Pinterest van de Filter ](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Voor de **bestemming van Pinterest**, selecteer het drie puntensymbool... en selecteer **[!UICONTROL Edit details]**.
   ![ uitgezocht geef details ](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png) uit
3. Selecteer **[!UICONTROL Reconnect OAuth]** en meld u aan bij uw Pinterest-account.
   ![ Uitgezocht opnieuw verbind OAuth ](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Ga naar het actiepunt in de onderstaande sectie

### Stroom naar nieuwe bestemming inschakelen {#disable-old-enable-new-flows}

Vervolgens moet u de gegevensstromen naar de nieuwe **[!UICONTROL Pinterest]** -kaart inschakelen.

1. Ga naar **[!UICONTROL Destinations > Browse]** en gebruik het filter op het scherm om alleen het **[!UICONTROL Pinterest]** -doel te filteren.
   ![ dataflows van Pinterest van de Filter slechts in het Browse lusje ](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Selecteer de hyperlinked verbindingsnaam (de campagne van de Loyalty in het het schermschot hierboven) aan de **[!UICONTROL Pinterest]** bestemming en schakelaar **[!UICONTROL Enable]** knevel aan **&#x200B;**.
   ![ knevel aan voor nieuwe verbindingen en weg voor oude verbindingen ](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## Kunt u een aantal tijdlijnen op hoog niveau delen?

Ja, zie hieronder:

**tegen 16 november, 2023**: De nieuwe bestemming is klaar, en u zou twee kaarten van Pinterest naast elkaar in de catalogus moeten zien tot Pinterest ophoudt ondersteunend oude v4 API. Alle bestaande gegevens worden naar de huidige Pinterest-kaart gekopieerd.

![ Oude en nieuwe bestemming van Pinterest zij aan zij ](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**tegen 15 December, 2023**: <span class="preview"> actie van de Klant 1 </span>. U dient opnieuw te worden geverifieerd op Pinterest, zodat de nieuwe kaart is aangesloten op Pinterest. Volledige instructies van de mening in [ deze sectie ](#reauthenticate).

<span class="preview"> actie 2 van de Klant </span>.Dan, moet u de dataflows in de nieuwe kaart toelaten. Volledige instructies van de mening in [ deze sectie ](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**na 18 Januari, 2024**: <span class="preview"> Pinterest heeft toegang tot V4 adverteerder API uitgezet. Om het even welke klanten van Real-Time CDP die niet aan de nieuwe bestemming hebben bevorderd zullen nu hun gegevensstromen aan de bestemming van Pinterest ontbreken. [ opnieuw voor authentiek verklaren aan Pinterest ](#reauthenticate) en [ laat de dataflows ](#disable-old-enable-new-flows) aan de promotiebestemming toe om uw campagnes aan Pinterest te hervatten.</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
