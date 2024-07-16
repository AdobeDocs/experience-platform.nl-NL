---
title: Batchbestemming Magnite Streaming
description: Gebruik deze bestemming om Adobe CDP publiek aan het platform van de Streaming van de Magnite in partij te leveren.
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 0%

---


# Magnietstreaming: Batch-verbinding {#magnite-streaming-batch}

## Overzicht {#overview}

In dit document wordt de Magnite Streaming: Batch-bestemming beschreven en worden voorbeelden gegeven van het gebruik van voorbeelden voor een beter begrip van het activeren en exporteren van soorten publiek.

Het Adobe Real-Time CDP-publiek kan op twee manieren aan de Magnite worden geleverd: het streamingplatform - het kan één keer per dag worden geleverd, of het kan in real-time worden geleverd:

1. Als u slechts één keer per dag een publiek wilt en/of moet leveren, kunt u de Magnite: Streaming Batch-bestemming gebruiken, die een publiek naar Magnite levert: Streaming via een dagelijkse levering van S3-batchbestanden. Deze Batchdoelgroepen worden voor onbepaalde tijd opgeslagen in ons platform, in tegenstelling tot real-time doelgroepen, die slechts een paar dagen worden opgeslagen.

2. Nochtans, als u wilt en/of het publiek in real time moet leveren, zult u Magnite moeten gebruiken: het stromen bestemming in real time. Wanneer het gebruiken van de bestemming in real time, Magnite: Het stromen zal publiek in real time ontvangen, maar wij kunnen slechts publiek in real time tijdelijk in ons platform opslaan, en zij zullen uit ons systeem binnen een paar dagen worden verwijderd. Om deze reden, als u Magnite wilt gebruiken: het stromen bestemming in real time, zult u ook de Magneet moeten gebruiken: het stromen bestemming van de Partij - elk publiek dat u aan de bestemming in real time activeert, moet u ook aan de bestemming van de Partij activeren.

Om opnieuw te kunnen samenvatten: als u slechts één keer per dag Adobe Real-Time CDP-publiek wilt leveren, gebruikt u de toeriet: Alleen streamingbatchbestemming en het publiek wordt één keer per dag geleverd. Als u het publiek van Adobe Real-Time CDP in Echt - tijd wilt leveren, zult u zowel de Magniet gebruiken: het stromen bestemming van de Partij, als de Magniet: Het stromen bestemming in real time. Neem voor meer informatie contact op met Magnite: Streaming.


Lees verder voor meer informatie over de Magnite: Streaming Batch-bestemming, hoe u er verbinding mee kunt maken en hoe u het Adobe Real-Time CDP-publiek activeert.
Voor meer informatie over de bestemming in real time, zie [ dit doc ](magnite-streaming.md) in plaats daarvan.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar is in bèta en slechts beschikbaar om klanten te selecteren. Neem contact op met uw Adobe als u toegang wilt aanvragen.
>
>De doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Magnite] . Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via `adobe-tech@magnite.com` .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de Magnite Streaming: de bestemming van de partij zou moeten gebruiken, zijn hier de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen gebruikend deze bestemming.

### Hoofdletters gebruiken #1 {#use-case-1}

U hebt een publiek geactiveerd op de Magnite Streaming: Real-Time bestemming.

Elk publiek dat via Magnite Streaming wordt geactiveerd: Real-Time bestemming moet ook de Magnite Streaming: Batch-bestemming gebruiken, aangezien de gegevens van de Batch-levering bedoeld zijn om de gegevens van de Real-Time levering binnen het Magnite Streaming platform te vervangen of aan te houden.

### Hoofdletters gebruiken #2 {#use-case-2}

U wilt een publiek alleen activeren in een batch-/dagcursus voor het Magnite Streaming-platform.

Elk publiek dat via de Magnite Streaming wordt geactiveerd: de batchbestemming wordt geleverd in een batch-/dagcadence en zal vervolgens op het Magnite Streaming-platform worden gericht.

## Vereisten {#prerequisites}

Als u de Magnite-doelen in Adobe Experience Platform wilt gebruiken, moet u eerst een Magnite Streaming-account hebben. Als u een [!DNL Magnite Streaming] -account hebt, vraagt u uw [!DNL Magnite] accountmanager om referenties voor toegang tot [!DNL Magnite's] -doelen. Als u geen [!DNL Magnite Streaming] -account hebt, kunt u contact opnemen met adobe-tech@magnite.com

## Ondersteunde identiteiten {#supported-identities}

De toeristenstroom: De bestemming van de partij kan *om het even welke* identiteitsbronnen van de Adobe CDP ontvangen. Deze bestemming heeft momenteel drie doelidentiteitsvelden waarnaar u de koppeling wilt maken.

>[!NOTE]
>
>*Om het even welke* identiteitsbronnen kunnen aan om het even welk van het doel magnite_deviceId in kaart brengen.

| Doelidentiteit | Beschrijving | Overwegingen |
|:--------------------------- |:------------------------------------------------------------------------------------------------ |:------------------------------------------------------------------------------------- |
| magnite_deviceId_GAID | GOOGLE ADVERTISING ID | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID is |
| magnite_deviceId_IDFA | Apple-id voor adverteerders | Selecteer deze doelidentiteit als uw bronidentiteit een IDFA is |
| magnite_deviceId_CUSTOM | Aangepaste id/door gebruiker gedefinieerde id | Selecteer deze doelidentiteit als uw bronidentiteit geen GAID of IDFA is of als het een aangepaste of door de gebruiker gedefinieerde id is |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

| Oorsprong publiek | Ondersteund | Beschrijving |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van het Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

| Item | Type | Notities |
|-----------------------------|----------|----------|
| Exporttype | Publiek exporteren | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in Magnite Streaming: Batchbestemming. |
| Exportfrequentie | Batch | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over partij [ op dossier-gebaseerde bestemmingen ](/help/destinations/destination-types.md). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

Zodra uw bestemmingsgebruik is goedgekeurd en de Streaming van de Magnite uw geloofsbrieven heeft gedeeld, te volgen gelieve de onderstaande stappen om voor authentiek te verklaren, gegevens in kaart te brengen en te delen.

### Verifiëren voor bestemming {#authenticate}

Zoek de Magnite Streaming: Batchbestemming in de Adobe Experience-catalogus. Klik op de knop Extra opties (\...) en configureer vervolgens de doelverbinding/doelinstantie.

Als u al een bestaand account hebt, kunt u dit vinden door de optie Account te wijzigen in &quot;Existing account&quot;. Anders maakt u hieronder een account:

Als u een nieuwe account wilt maken en deze voor het eerst wilt verifiëren bij de bestemming, vult u de velden &quot;S3-toegangssleutel&quot; en &quot;S3 geheime sleutel&quot; in (die u via uw accountmanager ontvangt) en selecteert u **[!UICONTROL Connect to destination]**

![ ongevulde gebieden van de bestemmingsconfiguratie ](../../assets/catalog/advertising/magnite/destination-batch-config-auth-unfilled.png)

>[!NOTE]
>
>Het beveiligingsbeleid van Magnite Streaming vereist een regelmatige rotatie van S3-sleutels. U zou moeten verwachten om uw rekening in de toekomst met nieuwe S3 toegang en S3 geheime sleutels bij te werken. U hoeft alleen de account zelf bij te werken. Voor bestemmingen die dat account gebruiken, worden automatisch de bijgewerkte sleutels gebruikt. Als u de nieuwe toetsen niet uploadt, worden de gegevens niet naar deze bestemming verzonden.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u deze doelverbinding/-instantie herkent in het dialoogvenster
de toekomst.
* **[!UICONTROL Description]**: Een beschrijving die u helpt dit te identificeren
doelverbinding/-instantie in de toekomst.
* **[!UICONTROL Name of your source partner]**: De naam die u als bron wilt opgeven in het platform van Magnite Streaming

![ gevulde gebieden van de bestemmingsconfiguratie ](../../assets/catalog/advertising/magnite/destination-batch-config-auth-filled.png)

>[!NOTE]
>
>Als u meerdere id-typen wilt verzenden (GAID, IDFA, enz.) wanneer u de Batch-bestemming gebruikt, is voor elke verbinding een nieuwe doelverbinding/nieuwe doelinstantie vereist. Neem voor meer informatie contact op met uw vertegenwoordiger van uw Magnite-account.

U kunt vervolgens doorgaan door **[!UICONTROL Next]** te selecteren

Op het volgende scherm, getiteld &quot;Governance Policy and Enforcement Actions (Optional)&quot;, kunt u naar keuze om het even welk relevant beleid van het gegevensbeheer selecteren. &quot;Gegevens exporteren&quot; wordt over het algemeen geselecteerd voor de bestemming Magnite Streaming Batch.

![ Facultatief beleid van het bestuur en handhavingsacties ](../../assets/catalog/advertising/magnite/destination-batch-config-grouping-policy.png)

Selecteer **[!UICONTROL Create]** wanneer deze optie is geselecteerd of wanneer u dit optionele scherm wilt overslaan

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

In **[!UICONTROL Source field]**, kunt u om het even welk attribuut of identiteit voor uw apparaten selecteren. In dit voorbeeld hebben we een aangepaste IdentityMap met de naam &#39;DeviceId&#39; geselecteerd
![ kaart gewenste gegevensgebieden aan het apparaat_id gebied ](../../assets/catalog/advertising/magnite/destination-batch-active-audience-field-mapping.png)

In de lus **[!UICONTROL Target field]** :
![ selecteer de aangewezen doelidentiteit van het apparatentype ](../../assets/catalog/advertising/magnite/destination-batch-active-audience-select-device-type.png) zie [ Gesteunde Identiteiten ](#supported-identities) voor meer informatie.
In dit voorbeeld hebben we **[!UICONTROL Target field]**: magnite_deviceId_CUSTOM geselecteerd, omdat onze **[!UICONTROL Source field]** is gedefinieerd als een aangepaste IdentityMap: DeviceID.

>[!NOTE]
>
>Als u meerdere id-typen wilt verzenden/toewijzen (GAID, IDFA, enz.) wanneer u de Batch-bestemming gebruikt, is voor elke verbinding een nieuwe doelverbinding/nieuwe doelinstantie vereist. Neem voor meer informatie contact op met uw vertegenwoordiger van uw Magnite-account.


Op het scherm &quot;Vorm filename en de uitvoerplanning voor elk publiek&quot;, moet u een Datum van het Begin (verplicht), Einddatum (facultatief), en (verplichte) identiteitskaart van de Afbeelding voor elk publiek nu vormen.

>[!IMPORTANT]
>
> Voor deze bestemming is een toewijzingsid of &quot;NONE&quot; vereist.
>
> Een toewijzings-id moet worden opgegeven wanneer een publiek een bestaande segment-id heeft die eerder bekend is bij Magnite Streaming. Anders moet &#39;NONE&#39; worden gebruikt als de toewijzing-id.
>
> Wanneer u de bestandsnaam voor elk publiek configureert, neemt u de toewijzingsid op via het veld Aangepaste tekst dat u wilt toevoegen. Aan de toewijzen-id wordt het volgende toegevoegd: `{previous_filename}\_\[MAPPING_ID\].` Als dit publiek nieuw is voor Magnite Streaming en u geen toewijzings-id opgeeft, wordt &#39;NONE&#39; weergegeven in het veld &#39;Aangepaste tekst&#39;. De nieuwe bestandsnaam in dit geval moet zijn: `{previous_filename}\_\[NONE\]` .

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat uw publiek is geüpload, kunt u controleren of uw publiek op de juiste wijze is gemaakt en geüpload.

* De Magnite Streaming Batch-bestemming levert S3-bestanden naar Magnite Streaming op een dagelijkse snelheid. Na levering en opname, zullen de soorten publiek/segmenten naar verwachting in het Streamen van de Magnite verschijnen, en kunnen op een overeenkomst worden toegepast. U kunt dit bevestigen door de segment-id of segmentnaam te zoeken die tijdens de activeringsstappen in de Adobe Experience Platform is gedeeld.

>[!NOTE]
>
>Het publiek activeerde/geleverde aan de Magnite die Batch bestemming stroomt zal ** het zelfde publiek vervangen dat via de Magnite die in real time bestemming stroomt werd geactiveerd/geleverd. Als u omhoog een segment gebruikend de segmentnaam kijkt, kunt u niet het segment in real time vinden, tot de partij is opgenomen en door het platform van de Streaming van de Magnite verwerkt.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Voor extra hulpdocumentatie, bezoek het [ Centrum van de Hulp van de Magniet ](https://help.magnite.com/help).
