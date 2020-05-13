---
title: Profielen en segmenten naar een doel activeren
seo-title: Profielen en segmenten naar een doel activeren
description: Activeer de gegevens die u in het Platform van de Gegevens van de Klant van Adobe in real time hebt door segmenten aan bestemmingen in kaart te brengen. Volg onderstaande stappen om dit te bereiken.
seo-description: Activeer de gegevens die u in het Platform van de Gegevens van de Klant van Adobe in real time hebt door segmenten aan bestemmingen in kaart te brengen. Volg onderstaande stappen om dit te bereiken.
translation-type: tm+mt
source-git-commit: 7dafdf0dd1ad3af2defab3bf6b784fd37e777062
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# Profielen en segmenten naar een doel activeren

Activeer de gegevens die u in het Platform van de Gegevens van de Klant van Adobe in real time hebt door segmenten aan bestemmingen in kaart te brengen. Volg onderstaande stappen om dit te bereiken.

## Vereisten {#prerequisites}

Om gegevens aan bestemmingen te activeren, moet u een bestemming [met succes hebben](/help/rtcdp/destinations/assets/connect-destination.png)verbonden. Als u dit niet reeds hebt gedaan, ga naar de [bestemmingscatalogus](/help/rtcdp/destinations/destinations-catalog.md), doorblader de gesteunde bestemmingen, en opstelling één of meerdere bestemmingen.

## Gegevens activeren {#activate-data}

1. Kies in **[!UICONTROL Doelen > Bladeren]** de bestemming waar u de segmenten wilt activeren.
2. Klik op de naam van het doel. Hiermee gaat u naar de flow Activeren.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Merk op dat als een activeringsstroom reeds voor een bestemming bestaat, u de segmenten kunt zien die momenteel naar de bestemming worden verzonden. Selecteer Activering **** bewerken in de rechtertrack en voer de onderstaande stappen uit om de activeringsdetails te wijzigen.
3. Selecteer **[!UICONTROL Activeren]**;
4. In het **[!UICONTROL Activate bestemmingswerkschema]** , op de **[!UICONTROL Uitgezochte pagina van Segmenten]** , selecteer welke segmenten om naar de bestemming te verzenden.
   ![segmenten-naar-bestemming](/help/rtcdp/destinations/assets/select-segments.png)
5. *Voorwaardelijk*. Deze stap is alleen van toepassing op segmenten die zijn toegewezen aan cloudopslagdoelen en e-mailmarketingdoelen. <br> Selecteer op de pagina **[!UICONTROL Doelkenmerken]** de optie Nieuw veld **** toevoegen en selecteer de kenmerken die u naar het doel wilt verzenden.
Wij adviseren één van de attributen om een [uniek herkenningsteken](/help/rtcdp/destinations/email-marketing-destinations.md#identity) van uw unieschema te zijn. Zie Identiteit in het artikel [E-mailmarketingdoelen](/help/rtcdp/destinations/email-marketing-destinations.md#identity) voor meer informatie over verplichte kenmerken.
   ![bestemmingskenmerken](/help/rtcdp/destinations/assets/destination-attributes.png)
6. Op de **[!UICONTROL het programmapagina]** van het Segment, kunt u de begindatum zien voor het verzenden van gegevens naar de bestemming, evenals de frequentie om gegevens naar de bestemming te verzenden.

   >[!IMPORTANT]
   >
   >Voor sociale bestemmingen, moet u de oorsprong van uw publiek in deze stap selecteren. U kunt pas verdergaan met de volgende stap nadat u een van de opties in de onderstaande afbeelding hebt geselecteerd.

   ![oorsprong van gegevens kiezen](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Op de pagina **[!UICONTROL Revisie]** ziet u een overzicht van uw selectie. Selecteer **[!UICONTROL Annuleren]** om de stroom te verbreken, **[!UICONTROL Terug]** om uw instellingen te wijzigen of **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![selectie bevestigen](/help/rtcdp/destinations/assets/confirm-selection.png)

## Activering bewerken {#edit-activation}

Voer de onderstaande stappen uit om bestaande activeringsstromen in CDP in real time te bewerken:

1. Selecteer **[!UICONTROL Doelen]** in de linkernavigatiebar, klik dan de **[!UICONTROL Browse]** tabel, en klik de bestemmingsnaam.
2. Selecteer Activering **** bewerken in de rechtertrack om te wijzigen welke segmenten naar de bestemming moeten worden verzonden.

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

1. Selecteer **[!UICONTROL Doelen]** in de linkernavigatiebar, klik dan de **[!UICONTROL Browse]** tabel, en klik de bestemmingsnaam.
2. Klik op het besturingselement **[!UICONTROL Ingeschakeld]** in de rechterrail om de activeringsstatus te wijzigen.
3. Selecteer in het statusvenster **Gegevens bijwerken de optie** Bevestigen **** om de activeringsstroom uit te schakelen.

