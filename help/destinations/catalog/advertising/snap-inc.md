---
title: Magnetische Inc-verbinding
description: Leer hoe u verbinding maakt met het Snapchat Ads Platform en uw publiek exporteert vanuit Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 9a80a9b49b1983e8e488d11b114c02130b045686
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Magnetische Inc-verbinding

## Overzicht {#overview}

[&#x200B; Snapchat Ads &#x200B;](https://forbusiness.snapchat.com/) worden gemaakt voor elke zaken, ongeacht de grootte of de industrie. Word onderdeel van de dagelijkse gesprekken van Snapchatters met digitale advertenties op volledig scherm die inspireren tot actie van de mensen die het belangrijkst zijn voor uw bedrijf.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en door het *Onverwachte team van Inc.* gehandhaafd. Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct in *dev-support@snap.com* te contacteren

## Gebruiksscenario’s {#use-cases}

Op deze bestemming kunnen marketers gebruikersgroepen die in Experience Platform zijn gemaakt, importeren in Snapchat-advertenties en deze gebruiken om hun advertenties als doel in te stellen.

## Vereisten {#prerequisites}

Als u deze bestemming wilt gebruiken, moet u een account voor Snapchat Ads hebben. Raadpleeg deze documentatie voor informatie over het maken van een dergelijke documentatie:

[&#x200B; krijgen Begonnen met Snapchat Advertising &#x200B;](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Beperkingen {#limitations}

* Snap Inc ondersteunt geen meervoudige identiteiten voor een bepaald publiekssegment. Wijs slechts één identiteit toe wanneer u een segment activeert.
* Snap Inc biedt geen ondersteuning voor het wijzigen van de naam van segmenten. Als u de naam van een segment wilt wijzigen, moet u het deactiveren, de naam ervan wijzigen en vervolgens het segment activeren.
* Het is niet mogelijk om een bewaarperiode voor de leden van een publiekssegment te bepalen. Alle leden hebben levensbehoud en zullen in het publiek zijn tot zij worden verwijderd.

## Ondersteunde identiteiten {#supported-identities}

De *Magnetische* bestemming van Inc. steunt de activering van identiteiten die in de lijst hieronder worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

Alle herkenningstekens die naar de *Magnetische bestemming Inc* worden verzonden moeten in formaat worden gehashed SHA-256. Als u gewone-tekstid&#39;s wilt hashen voordat u ze naar de bestemming verzendt, controleert u de optie **[!UICONTROL Apply transformation]** wanneer u doelid&#39;s voor de bestemming toewijst.

>[!WARNING]
> 
> Ononderbroken id&#39;s worden niet geaccepteerd door de Magnetische Inc-bestemming en het verzenden ervan kan fouten veroorzaken.


>[!IMPORTANT]
> 
> De Magnetische bestemming Inc steunt geen veelvoudige identiteiten. Selecteer slechts één identiteit.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| E-mailadres | SHA-256 gehasht e-mailadres | De e-mailadressen van de kaart in het gebied van de doelidentiteit *emailAddress*. |
| Telefoonnummer | SHA-256 gehashed telefoonaantal | De e-mailadressen van de kaart in het gebied van de doelidentiteit *phoneNumber*. |
| GAID | SHA-256 hashed Google Advertising ID | De identiteitskaart van Google van de kaart Advertising in het gebied van de doelidentiteit *identiteitskaart*. |
| IDFA | SHA-256 hashed Apple Advertising ID | Apple Advertising IDs van de kaart in het gebied van de doelidentiteit *idfa*. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |
| [!DNL Federated Audience Composition] | ✓ | Het publiek werd ingevoerd in Experience Platform door [&#x200B; Federated Samenstelling van het Publiek &#x200B;](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de Inc-bestemming magnetisch worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinding maken met Magnetische Inc {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

### Verifiëren voor bestemming {#authenticate}

Ga als volgt te werk om te verifiëren bij de bestemming:

1. Vind de *Magnetische Inc.* bestemming van de Catalogus van de Bestemming van Adobe Experience Platform en selecteer **Opstelling**.
2. Selecteer **[!UICONTROL Connect to destination]**. U wordt omgeleid naar het volgende scherm:
   ![&#x200B; Scherm van de Auth 1 &#x200B;](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Ga uw geloofsbrieven van de Snapchat in en selecteer **Login**.
4. De gegevens voor Snapchat waartoe Adobe Experience Platform toegang heeft, worden weergegeven. Selecteer **verdergaan** met het verbindingsproces te werk te gaan.

![&#x200B; Scherm 2 van de Auth &#x200B;](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Nadat u hebt geselecteerd, wacht u tot u weer naar Adobe Experience Platform bent omgeleid.

### Doelgegevens invullen {#destination-details}

![&#x200B; Details van de Bestemming &#x200B;](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Als u details voor het doel wilt configureren, vult u de vereiste velden in en selecteert u **[!UICONTROL Next]** .

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: De id van het Advertentieaccount die is gekoppeld aan het Advertentieaccount waarnaar u uw publiek wilt importeren. Voor meer informatie over hoe te om dit te vinden, gelieve te verwijzen naar [&#x200B; deze documentatie over het Centrum van de Hulp van de Bedrijfs Snapchat &#x200B;](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Als u een onjuiste of ongeldige account-id voor Snapchat-advertentie invoert, mislukt de activering van het publiek. Controleer nogmaals of je de juiste gebruikersnaam voor je advertentieaccount hebt ingevoerd.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Na het activeren van publiek aan de *Magnetische bestemming Inc.*, zult u het publiek in de Magnetische 2&rbrace; sectie **van de Manager van Advertenties [&#128279;](https://businesshelp.snapchat.com/s/article/audience-sharing) kunnen zien.** Ga als volgt te werk om naar deze sectie te navigeren:

1. Logboek in de [&#x200B; Magnetische Manager van Advertenties &#x200B;](https://ads.snapchat.com/)
2. Selecteer **Soorten publiek** van het pulldown menu in de hogere linkerhoek van het scherm. In de Audience Library ziet u het publiek dat u in Adobe Experience Platform hebt geactiveerd:

![Doelgroepen](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Houd er rekening mee dat wanneer een Adobe-publiek voor het eerst wordt geactiveerd op Snap Inc, dit eerst als een leeg publiek wordt weergegeven. Adobe Experience Platform exporteert ledengegevens namelijk pas naar Snap Inc als het publiek wordt geëvalueerd. Voor meer informatie over hoe het publiek in Experience Platform wordt geëvalueerd, gelieve te verwijzen naar het [&#x200B; overzicht van de Dienst van de Segmentatie &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=nl-NL#evaluate-segments).

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
