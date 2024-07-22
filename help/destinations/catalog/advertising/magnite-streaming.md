---
title: Real-Time doelverbinding Magnite
description: Gebruik deze bestemming om Adobe CDP publiek aan het platform van de Streaming van de Magnite in real time te leveren.
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 8314aca706b47c4cbcb993418c287629f5563189
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---


# (Beta) Magnite: Real-Time bestemmingsverbinding

## Overzicht {#overview}

[!DNL Magnite: Real-Time] en [ Magnite: De bestemmingen van de partij ](/help/destinations/catalog/advertising/magnite-batch.md) in Adobe Experience Platform helpen u toehoorden in kaart brengen en uitvoeren voor het richten en de activering op het Magnite Streaming platform.

Het activeren van het publiek voor het [!DNL Magnite Streaming] -platform is een proces in twee stappen waarbij u zowel de Magnite als Real-Time en de Magnite: Batch-doelen moet gebruiken.

Als u uw publiek wilt activeren naar [!DNL Magnite Streaming] , moet u:

* Activeer het publiek op de bestemming [!DNL Magnite: Real-Time], zoals weergegeven op deze pagina.
* Activeer hetzelfde publiek op de toeriet: Batch-bestemming. Het doel van [!DNL Magnite: Batch] is een verplichte component. Als u het publiek niet activeert op de batchbestemming [!DNL Magnite Streaming] , resulteert dit in een mislukte integratie en wordt het publiek niet geactiveerd.

Opmerking: wanneer u de bestemming Real-Time gebruikt, ontvangt [!DNL Magnite Streaming] een publiek in real-time, maar Magnite kan alleen realtime publiek tijdelijk in het platform opslaan en binnen een paar dagen worden verwijderd uit het systeem. Om deze reden, als u Magnite wilt gebruiken: In real time bestemming, zult u *ook* moeten gebruiken Magnite: de bestemming van de partij - elk publiek dat u aan de bestemming in real time activeert, moet u ook aan de bestemming van de Partij activeren.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar is in bèta en slechts beschikbaar om klanten te selecteren. Neem contact op met uw Adobe als u toegang wilt aanvragen.
>
>De doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Magnite] . Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via `adobe-tech@magnite.com` .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Magnite: Real-Time] bestemming zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Activering en doelversie {#activation-and-targeting}

Dankzij deze integratie met Magnite kunnen klanten hun CDP-publiek doorgeven van Adobe Experience Platform naar Magnite voor het maken van advertenties. Soorten publiek kan in Magnite worden geselecteerd voor positieve doelgerichtheid en voor negatieve doelgerichtheid (onderdrukking).

## Vereisten {#prerequisites}

Als u de [!DNL Magnite] -doelen in Adobe Experience Platform wilt gebruiken, moet u eerst een [!DNL Magnite Streaming] -account hebben. Als u een [!DNL Magnite Streaming] -account hebt, vraagt u uw [!DNL Magnite] accountmanager om referenties voor toegang tot [!DNL Magnite's] -doelen.
Als u geen [!DNL Magnite Streaming] -account hebt, kunt u contact opnemen met adobe-tech@magnite.com

## Ondersteunde identiteiten {#supported-identities}

Het doel van [!DNL Magnite: Real-Time] ondersteunt de activering van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Een unieke id voor een apparaat of identiteit. We accepteren alle apparaat-id&#39;s en de eerste-partijid, ongeacht het type. | Identiteitstypen die door Magnite worden ondersteund, zijn onder andere PPUID-, GAID-, IDFA- en TV-apparaat-id&#39;s. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van het Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Magnite: Real-Time] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View destinations]** en **[!UICONTROL Manage destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![ ongevulde gebieden van de bestemmingsconfiguratie ](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Username]**: De gebruikersnaam die door [!DNL Magnite] aan u wordt verstrekt.
* **[!UICONTROL Password]**: Het wachtwoord dat door [!DNL Magnite] aan u wordt verstrekt.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Name of your source partner]**: De naam van uw klant/bedrijf. Alleen ondersteunde [!DNL Magnite Streaming] clients zijn beschikbaar voor selectie.

![ gevulde gebieden van de bestemmingsconfiguratie ](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Selecteer vervolgens de knop **[!UICONTROL Create]** .

![ Facultatief beleid van het bestuur en handhavingsacties ](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View destinations]**, **[!UICONTROL Activate destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en segmenten aan het stromen segment de uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

Zodra de bestemmingsverbinding is gecreeerd, kunt u aan de stroom van de publiekactivering te werk gaan. De volgende sectie loopt door hoe te om publiek te activeren gebruikend de bestemming in real time.

### Kenmerken en identiteiten toewijzen {#map}

De volgende stap is bronherkenningstekens in kaart te brengen aan het apparaat_id herkenningsteken van de Magnite.

* U kunt zoveel toewijzingen toevoegen als u nodig hebt door **[!UICONTROL Add new mapping]** te selecteren.

Dit voorbeeld dat de bestemming in real time gebruikt toont een rij die een generische apparaatId bronherkenningsteken bevat die aan het het doelgebied van Magnite device_id wordt in kaart gebracht. Wanneer u bij de afbeeldingen bent, selecteert u [!UICONTROL Next] .

![ Kaart gewenste gegevensgebieden aan het apparaat_ID gebied ](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Vergeet niet Mapping ID&#39;s in te stellen op alle geactiveerde soorten publiek of NONE in te stellen als er geen toewijzing-id aanwezig is.

![ ben zeker om het Toewijzen IDs aan alle geactiveerde publiek te plaatsen, of NONE te plaatsen als geen Toewijzings identiteitskaart ](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png) aanwezig is

U moet nu een begindatum (verplicht), een einddatum (optioneel) en een toewijzingsid voor elk publiek configureren.

**Uitwisselingsidentiteitskaart**

* Gebruik het veld **[!UICONTROL Mapping ID]** wanneer een publiek een reeds bestaande segment-id heeft die eerder bekend is bij Magnite.

* Als u een **[!UICONTROL Mapping ID]** aan een publiek wilt toevoegen, selecteert u elke publiekstrij afzonderlijk en voert u gegevens in de rechterkolom in (zie bovenstaande afbeelding). Als u geen toewijzings-id wilt toevoegen, voert u GEEN in het veld Toewijzings-id in.

Selecteer **[!UICONTROL Next]** en voltooi de activeringsstroom.

![ selecteer daarna en voltooi activeringsstroom.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat uw publiek is geüpload, kunt u met de volgende stappen controleren of uw publiek is gemaakt en correct is geüpload:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Na-ingest, zullen het publiek naar verwachting binnen [!DNL Magnite Streaming] binnen een paar minuten verschijnen en kunnen op een overeenkomst worden toegepast. U kunt dit bevestigen door de segment-id op te zoeken die tijdens de activeringsstappen in de Adobe Experience Platform is gedeeld.

## Activeer het zelfde publiek door de [!DNL Magnite: Batch] bestemming

Soorten publiek dat met [!DNL Magnite Streaming] wordt gedeeld met gebruik van de bestemming Real-Time, moeten ook worden gedeeld met gebruik van de Magnite: Batch-bestemming. Als de segmentnamen correct zijn geconfigureerd in de gebruikersinterface van [!DNL Magnite Streaming] , worden deze bijgewerkt met de segmentnamen die worden gebruikt in de Adobe Experience Platform-update na de dag.

Tot slot als een bestemming van de Partij niet voor uw integratie is gevormd, plaats het nu via Magnite: het bestemmingsdocument van de Partij.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Voor extra hulpdocumentatie, bezoek het [ Centrum van de Hulp van de Magniet ](https://help.magnite.com/help).
