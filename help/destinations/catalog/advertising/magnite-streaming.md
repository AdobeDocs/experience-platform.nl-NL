---
title: Magnite Streaming Real-Time doelverbinding
description: Gebruik deze bestemming om Adobe CDP publiek aan het platform van de Streaming van de Magnite in real time te leveren.
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# (Beta) Magnite Streaming: Real-Time bestemmingsverbinding

## Overzicht {#overview}

De [!DNL Magnite Streaming: Real-Time] en de Magnite Streaming: Batch-bestemmingen in Adobe Experience Platform helpen u bij het toewijzen en exporteren van doelgroepen en activering op het Magnite Streaming-platform.

Het publiek activeren voor de [!DNL Magnite Streaming] -platform is een proces in twee stappen waarbij u zowel de Magnite Streaming: Real-Time als de Magnite Streaming: Batch-doelen moet gebruiken.

Uw publiek activeren op [!DNL Magnite Streaming], moet u:

* Het publiek op de knop [!DNL Magnite Streaming: Real-Time] doel, zoals weergegeven op deze pagina.
* Activeer hetzelfde publiek bij Magnite Streaming: Batch-bestemming. De [!DNL Magnite Streaming: Batch] doel is een verplicht onderdeel. Kan het publiek niet activeren op het [!DNL Magnite Streaming] Batchbestemming resulteert in een mislukte integratie en uw publiek wordt niet geactiveerd.

Nota: Wanneer het gebruiken van de bestemming Echt - tijd, [!DNL Magnite: Streaming] In real-time zullen we een publiek ontvangen, maar we kunnen alleen in real-time publiek tijdelijk opslaan op ons platform, en ze zullen binnen een paar dagen uit ons systeem worden verwijderd. Om deze reden, als u Magnite wilt gebruiken: Het stromen bestemming in real time, zult u *ook* moet de functie Magnite Streaming: Batch-bestemming gebruiken - elk publiek dat u activeert naar de Real-Time bestemming, moet u ook activeren naar de Batch-bestemming.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar is in bèta en slechts beschikbaar om klanten te selecteren. Neem contact op met uw Adobe als u toegang wilt aanvragen.
>
>De bestemmingsschakelaar en documentatiepagina worden gecreeerd en door [!DNL Magnite] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via `adobe-tech@magnite.com`.

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL Magnite Streaming: Real-Time] doel, hier is een geval van steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Activering en doelversie {#activation-and-targeting}

Dankzij deze integratie met Magnite kunnen klanten hun CDP-publiek doorgeven van Adobe Experience Platform naar Magnite voor het maken van advertenties. Soorten publiek kan in Magnite worden geselecteerd voor positieve doelgerichtheid en voor negatieve doelgerichtheid (onderdrukking).

## Vereisten {#prerequisites}

Als u de opdracht [!DNL Magnite] bestemmingen in Adobe Experience Platform, moet u eerst een [!DNL Magnite Streaming] account. Als u een [!DNL Magnite Streaming] account, neem contact op met je [!DNL Magnite] accountmanager moet gegevens krijgen voor toegang tot [!DNL Magnite's] bestemmingen.
Als u geen [!DNL Magnite Streaming] account, surf naar adobe-tech@magnite.com

## Ondersteunde identiteiten {#supported-identities}

De [!DNL Magnite Streaming: Real-Time] doel ondersteunt de activering van de identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Een unieke id voor een apparaat of identiteit. We accepteren alle apparaat-id&#39;s en de eerste-partijid, ongeacht het type. | Identiteitstypen die wij ondersteunen, zijn onder andere PPUID-, GAID-, IDFA- en tv-apparaat-id&#39;s. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster [!DNL Magnite Streaming: Real-Time] bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View destinations]** en **[!UICONTROL Manage destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

![doelconfiguratie, automatische velden niet ingevuld](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Username]**: De gebruikersnaam die door [!DNL Magnite].
* **[!UICONTROL Password]**: Het wachtwoord dat u van [!DNL Magnite].

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Name of your source partner]**: De naam van uw klant/bedrijf. Alleen ondersteund [!DNL Magnite Streaming] clients kunnen worden geselecteerd.

![aangepaste doelconfiguratievelden ingevuld](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Selecteer de optie **[!UICONTROL Create]** knop.

![Optioneel governancebeleid en handhavingsmaatregelen](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View destinations]**, **[!UICONTROL Activate destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

Zodra de bestemmingsverbinding is gecreeerd, kunt u aan de stroom van de publiekactivering te werk gaan. De volgende sectie loopt door hoe te om publiek te activeren gebruikend de bestemming in real time.

### Kenmerken en identiteiten toewijzen {#map}

De volgende stap is bronherkenningstekens in kaart te brengen aan het apparaat_id herkenningsteken van de Magnite.

* U kunt zoveel toewijzingen toevoegen als u nodig hebt door **[!UICONTROL Add new mapping]**.

Dit voorbeeld dat de bestemming in real time gebruikt toont een rij die een generische apparaatId bronherkenningsteken bevat die aan het het doelgebied van Magnite device_id wordt in kaart gebracht. Als u bij de toewijzingen bent, selecteert u [!UICONTROL Next].

![Wijs de gewenste gegevensvelden toe aan het veld device_ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Vergeet niet Mapping ID&#39;s in te stellen op alle geactiveerde soorten publiek of NONE in te stellen als er geen toewijzing-id aanwezig is.

![Vergeet niet Mapping-id&#39;s in te stellen op alle geactiveerde soorten publiek, of NONE in te stellen als er geen toewijzing-id aanwezig is](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

U moet nu een begindatum (verplicht), een einddatum (optioneel) en een toewijzingsid voor elk publiek configureren.

**Toewijzing-id**

* Gebruik de **[!UICONTROL Mapping ID]** veld wanneer een publiek een reeds bestaande segment-id heeft die eerder aan Magnite bekend was.

* Als u een **[!UICONTROL Mapping ID]** aan een publiek, selecteer elke publiekstrij individueel, en ga gegevens in de juiste kolom (zie beeld hierboven) in. Als u geen toewijzings-id wilt toevoegen, voert u GEEN in het veld Toewijzings-id in.

Selecteren **[!UICONTROL Next]** en voltooit u de activeringsstroom.

![Selecteer Volgende en voltooi de activeringsstroom.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat uw publiek is geüpload, kunt u met de volgende stappen controleren of uw publiek is gemaakt en correct is geüpload:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Post-ingest, publiek wordt verwacht te verschijnen in [!DNL Magnite Streaming] binnen een paar minuten en kan op een overeenkomst worden toegepast. U kunt dit bevestigen door de segment-id op te zoeken die tijdens de activeringsstappen in de Adobe Experience Platform is gedeeld.

## Hetzelfde publiek activeren via het dialoogvenster [!DNL Magnite Streaming: Batch]doel

Soorten publiek gedeeld met [!DNL Magnite Streaming] het gebruiken van de bestemming in real time zal ook moeten worden gedeeld gebruikend de Magnite Streaming: de bestemming van de Partij. Indien correct gevormd, segmentnamen in [!DNL Magnite Streaming] De gebruikersinterface wordt bijgewerkt met de gebruikersinterface die wordt gebruikt in de post-dagelijkse Adobe Experience Platform-update.

Tot slot als een bestemming van de Partij niet voor uw integratie is gevormd, opstelling het nu via de Magnite Streaming: het bestemmingsdocument van de Partij.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Ga voor aanvullende Help-documentatie naar de [Magnite Help Center](https://help.magnite.com/help).
