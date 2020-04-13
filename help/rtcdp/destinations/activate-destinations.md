---
title: Profielen en segmenten naar een doel activeren
seo-title: Profielen en segmenten naar een doel activeren
description: Activeer de gegevens die u in het Platform van de Gegevens van de Klant van Adobe in real time hebt door segmenten aan bestemmingen in kaart te brengen. Volg onderstaande stappen om dit te bereiken.
seo-description: Activeer de gegevens die u in het Platform van de Gegevens van de Klant van Adobe in real time hebt door segmenten aan bestemmingen in kaart te brengen. Volg onderstaande stappen om dit te bereiken.
translation-type: tm+mt
source-git-commit: 2eddd5bb7b62dcc414ad906647b05ce10c766ac6

---


# Profielen en segmenten naar een doel activeren

Activeer de gegevens die u in het Platform van de Gegevens van de Klant van Adobe in real time hebt door segmenten aan bestemmingen in kaart te brengen. Volg onderstaande stappen om dit te bereiken.

## Vereisten {#prerequisites}

Om gegevens aan bestemmingen te activeren, moet u een bestemming [met succes hebben](/help/rtcdp/destinations/assets/connect-destination.png)verbonden. Als u dit niet reeds hebt gedaan, ga naar de [bestemmingscatalogus](/help/rtcdp/destinations/destinations-catalog.md), doorblader de gesteunde bestemmingen, en opstelling één of meerdere bestemmingen.

## Gegevens activeren {#activate-data}

1. Selecteer **[!UICONTROL Destinations > Browse]** in de bestemming waar u de segmenten wilt activeren.
2. Klik op de naam van het doel. Hiermee gaat u naar de flow Activeren.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Merk op dat als een activeringsstroom reeds voor een bestemming bestaat, u de segmenten kunt zien die momenteel naar de bestemming worden verzonden. Selecteer **[!UICONTROL Edit activation]** in het rechterspoor en volg de onderstaande stappen om de activeringsdetails te wijzigen.
3. Selecteren **[!UICONTROL Activate]**;
4. Selecteer in de **[!UICONTROL Activate destination]** workflow op de **[!UICONTROL Select Segments]** pagina welke segmenten naar de bestemming moeten worden verzonden.
   ![segmenten-naar-bestemming](/help/rtcdp/destinations/assets/select-segments.png)
5. *Voorwaardelijk*. Deze stap is slechts voor segmenten van toepassing die aan e-mail marketing bestemmingen in kaart worden gebracht. <br> Selecteer op de **[!UICONTROL Destination Attributes]** pagina de kenmerken die u naar het doel wilt verzenden **[!UICONTROL Add new field]** en selecteer deze.
Wij adviseren één van de attributen om een [uniek herkenningsteken](/help/rtcdp/destinations/email-marketing-destinations.md#identity) van uw unieschema te zijn. Zie Identiteit in het artikel [E-mailmarketingdoelen](/help/rtcdp/destinations/email-marketing-destinations.md#identity) voor meer informatie over verplichte kenmerken.
   ![bestemmingskenmerken](/help/rtcdp/destinations/assets/destination-attributes.png)
6. Op de **[!UICONTROL Segment schedule]** pagina, kunt u de begindatum zien voor het verzenden van gegevens naar de bestemming, evenals de frequentie om gegevens naar de bestemming te verzenden.

   >[!IMPORTANT]
   >
   >Voor sociale bestemmingen, moet u de oorsprong van uw publiek in deze stap selecteren. U kunt pas verdergaan met de volgende stap nadat u een van de opties in de onderstaande afbeelding hebt geselecteerd.

   ![oorsprong van gegevens kiezen](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Op de **[!UICONTROL Review]** pagina ziet u een overzicht van uw selectie. Selecteer **[!UICONTROL Cancel]** om de stroom te verbreken, **[!UICONTROL Back]** **[!UICONTROL Finish]** om uw montages te wijzigen, of uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

![selectie bevestigen](/help/rtcdp/destinations/assets/confirm-selection.png)

## Activering bewerken {#edit-activation}

Voer de onderstaande stappen uit om bestaande activeringsstromen in CDP in real time te bewerken:

1. Selecteer **[!UICONTROL Destinations]** in de linkernavigatiebalk, klik op het **[!UICONTROL Browse]** tabblad en klik op de doelnaam.
2. Selecteer **[!UICONTROL Edit activation]** in de rechterspoorlijn om te veranderen welke segmenten naar de bestemming te verzenden.

## Controleren of segmentactivering is gelukt {#verify-activation}

### E-mailmarketingbestemmingen en cloudopslagbestemmingen

Voor marketingdoelen en opslagdoelen voor de cloud maakt Adobe Real-time CDP een door tabs gescheiden `.txt` of `.csv` bestand op de opslaglocatie die u hebt opgegeven. Verwacht dat er elke dag een nieuw bestand op uw opslaglocatie wordt gemaakt. De bestandsindeling is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

De bestanden die u op drie opeenvolgende dagen ontvangt, kunnen er als volgt uitzien:

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

De aanwezigheid van deze bestanden op de opslaglocatie bevestigt dat de activering is gelukt.

### Reclamebestemmingen

Controleer de respectieve advertentiebestemming u uw gegevens aan activeert. Als de activering is gelukt, worden de doelgroepen in uw advertentieplatform ingevuld.

### Sociale netwerkbestemmingen

Voor Facebook betekent een geslaagde activering dat er via de programmacode een aangepast publiek voor Facebook wordt gemaakt in [Facebook Ads Manager](https://www.facebook.com/adsmanager/manage/). Het lidmaatschap van een segment in het publiek zou worden toegevoegd en verwijderd aangezien de gebruikers voor de geactiveerde segmenten worden gekwalificeerd of worden uitgesloten.

## Activering uitschakelen {#disable-activation}

Volg onderstaande stappen om een bestaande activeringsstroom uit te schakelen:

1. Selecteer **[!UICONTROL Destinations]** in de linkernavigatiebalk, klik op het **[!UICONTROL Browse]** tabblad en klik op de doelnaam.
2. Klik op het **[!UICONTROL Enabled]** besturingselement in de rechterrail om de activeringsstatus te wijzigen.
3. Selecteer in het statusvenster **Gegevens bijwerken de optie** Bevestigen **** om de activeringsstroom uit te schakelen.

