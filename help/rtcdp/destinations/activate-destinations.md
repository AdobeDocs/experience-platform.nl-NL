---
title: Profielen en segmenten naar een doel activeren
seo-title: Profielen en segmenten naar een doel activeren
description: Activeer de gegevens u in het Platform van de Gegevens van de Klant van Adobe in real time door segmenten aan bestemmingen in kaart te brengen hebt. Volg onderstaande stappen om dit te bereiken.
seo-description: Activeer de gegevens u in het Platform van de Gegevens van de Klant van Adobe in real time door segmenten aan bestemmingen in kaart te brengen hebt. Volg onderstaande stappen om dit te bereiken.
translation-type: tm+mt
source-git-commit: 86ded28b1830d3607c8b5214c8d31dfcbf446252
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 0%

---


# Profielen en segmenten naar een doel activeren

Activeer de gegevens u in het Platform van de Gegevens van de Klant van Adobe in real time door segmenten aan bestemmingen in kaart te brengen hebt. Volg onderstaande stappen om dit te bereiken.

## Vereisten {#prerequisites}

Om gegevens aan bestemmingen te activeren, moet u een bestemming [met succes hebben](/help/rtcdp/destinations/connect-destination.md)verbonden. Als u dit niet reeds hebt gedaan, ga naar de [bestemmingscatalogus](/help/rtcdp/destinations/destinations-catalog.md), doorblader de gesteunde bestemmingen, en opstelling één of meerdere bestemmingen.

## Gegevens activeren {#activate-data}

1. Kies in **[!UICONTROL Doelen]** > **[!UICONTROL Bladeren]** de bestemming waar u de segmenten wilt activeren.
2. Klik op de naam van het doel. Hiermee gaat u naar de flow Activeren.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Merk op dat als een activeringsstroom reeds voor een bestemming bestaat, u de segmenten kunt zien die momenteel naar de bestemming worden verzonden. Selecteer Activering **** bewerken in de rechtertrack en voer de onderstaande stappen uit om de activeringsdetails te wijzigen.
3. Selecteer **[!UICONTROL Activeren]**;
4. In het **[!UICONTROL Activate bestemmingswerkschema]** , op de **[!UICONTROL Uitgezochte pagina van Segmenten]** , selecteer welke segmenten om naar de bestemming te verzenden.
   ![segmenten-naar-bestemming](/help/rtcdp/destinations/assets/email-select-segments.png)
5. *Voorwaardelijk*. Deze stap is afhankelijk van het type bestemming waar u de segmenten activeert. <br> Voor *e-mail marketing bestemmingen* en *wolkenopslagbestemmingen*, op de **[!UICONTROL Uitgezochte pagina van Attributen]** , selecteer **[!UICONTROL voeg nieuw gebied]** toe en selecteer de attributen die u naar de bestemming wilt verzenden.
Wij adviseren één van de attributen om een [uniek herkenningsteken](/help/rtcdp/destinations/email-marketing-destinations.md#identity) van uw unieschema te zijn. Zie Identiteit in het artikel [E-mailmarketingdoelen](/help/rtcdp/destinations/email-marketing-destinations.md#identity) voor meer informatie over verplichte kenmerken.

   >[!NOTE]
   > 
   >Als er labels voor gegevensgebruik zijn toegepast op bepaalde velden in een gegevensset (in plaats van op de gehele gegevensset), wordt de toepassing van die labels op veldniveau bij activering uitgevoerd onder de volgende voorwaarden:
   >* De velden worden gebruikt in de segmentdefinitie.
   >* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.

   >
   > Bekijk de onderstaande schermafbeelding. Als, bijvoorbeeld, het gebied bepaalde etiketten van het gegevensgebruik `person.name.first.Name` had die met de marketing van de bestemming gebruiksgeval in conflict waren, zou u een schending van het beleid van het gegevensgebruik in de overzichtsstap (stap 7) worden getoond. Voor meer informatie, zie de Governance van [Gegevens in Echt - tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations)

   ![bestemmingskenmerken](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   Voor *sociale bestemmingen*, in de het in kaart brengen **[!UICONTROL van de]** Identiteit stap, kunt u bronattributen selecteren om als doelidentiteiten in de bestemming in kaart te brengen. Deze stap is optioneel of verplicht, afhankelijk van de primaire identiteit die u in het schema gebruikt. <br> 

   *E-mailadres als primaire identiteit*: Als u het e-mailadres als primaire identiteit in uw schema gebruikt, kunt u de stap Identiteitstoewijzing overslaan, zoals hieronder wordt getoond:

   ![E-mailadres als identiteit](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *Een andere id als primaire identiteit*: Als u een andere identiteitskaart, zoals *Uitkerings identiteitskaart* of identiteitskaart *van de* Loyalty, als primaire identiteit in uw schema gebruikt, moet u het e-mailadres van uw identiteitsschema als doelidentiteit in de sociale bestemming manueel in kaart brengen, zoals hieronder getoond:

   ![Loyalty-id als identiteit](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   Selecteer deze optie `Email_LC_SHA256` als doel als u de e-mailadressen van klanten bij het invoeren van gegevens in Adobe Experience Platform hebt gewijzigd volgens de vereisten voor [!DNL Facebook] e- [mailhashing](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements). <br> Selecteer `Email` als doel-id als de e-mailadressen die u gebruikt geen hashing zijn. Adobe In real time CDP zal de e-mailadressen hash om aan [!DNL Facebook] vereisten te voldoen.

   ![identiteitstoewijzing na invullen van velden](/help/rtcdp/destinations/assets/identity-mapping.png)

6. Op de **[!UICONTROL het programmapagina]** van het Segment, kunt u de begindatum zien voor het verzenden van gegevens naar de bestemming, evenals de frequentie om gegevens naar de bestemming te verzenden.

   >[!IMPORTANT]
   >
   >Voor sociale bestemmingen, moet u de oorsprong van uw publiek in deze stap selecteren. U kunt pas verdergaan met de volgende stap nadat u een van de opties in de onderstaande afbeelding hebt geselecteerd.

   ![oorsprong van gegevens kiezen](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Op de pagina **[!UICONTROL Revisie]** ziet u een overzicht van uw selectie. Selecteer **[!UICONTROL Annuleren]** om de stroom te verbreken, **[!UICONTROL Terug]** om uw instellingen te wijzigen of **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

   >[!IMPORTANT]
   >
   >In deze stap, CDP in real time controleert op de schendingen van het beleid van het gegevensgebruik. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](/help/rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie van de documentatie van het gegevensbeheer.

![selectie bevestigen](/help/rtcdp/destinations/assets/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Voltooien]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![selectie bevestigen](/help/rtcdp/destinations/assets/confirm-selection.png)



## Activering bewerken {#edit-activation}

Voer de onderstaande stappen uit om bestaande activeringsstromen in CDP in real time te bewerken:

1. Selecteer **[!UICONTROL Doelen]** in de linkernavigatiebar, klik dan de **[!UICONTROL Browse]** tabel, en klik de bestemmingsnaam.
2. Selecteer Activering **** bewerken in de rechtertrack om te wijzigen welke segmenten naar de bestemming moeten worden verzonden.

## Controleren of segmentactivering is gelukt {#verify-activation}

### E-mailmarketingbestemmingen en cloudopslagbestemmingen {#esp-and-cloud-storage}

Voor e-mailmarketingdoelen en cloudopslagdoelen maakt Adobe Real-time CDP een door tabs gescheiden `.csv` of `.txt` bestand op de opslaglocatie die u hebt opgegeven. Verwacht dat er elke dag een nieuw bestand op uw opslaglocatie wordt gemaakt. De bestandsindeling is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

De bestanden die u op drie opeenvolgende dagen ontvangt, kunnen er als volgt uitzien:

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

De aanwezigheid van deze bestanden op de opslaglocatie bevestigt dat de activering is gelukt. Als u wilt weten hoe de geëxporteerde bestanden zijn gestructureerd, kunt u een voorbeeld-CSV-bestand [](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv)downloaden. Dit voorbeeldbestand bevat de profielkenmerken `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`en `personalEmail.address`.

### Reclamebestemmingen

Controleer je account in de advertentiebestemming waarnaar je gegevens activeert. If activation was successful, audiences are populated in your advertising platform.

### Sociale netwerkbestemmingen

For [!DNL Facebook], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>De integratie tussen Adobe in real time CDP en [!DNL Facebook] steunt historische publieksbackfills. All historical segment qualifications get sent to [!DNL Facebook] when you activate the segments to the destination.

## Activering uitschakelen {#disable-activation}

Volg onderstaande stappen om een bestaande activeringsstroom uit te schakelen:

1. Selecteer **[!UICONTROL Doelen]** in de linkernavigatiebar, klik dan de **[!UICONTROL Browse]** tabel, en klik de bestemmingsnaam.
2. Klik op het besturingselement **[!UICONTROL Ingeschakeld]** in de rechterrail om de activeringsstatus te wijzigen.
3. Selecteer in het statusvenster **Gegevens bijwerken de optie** Bevestigen **** om de activeringsstroom uit te schakelen.
