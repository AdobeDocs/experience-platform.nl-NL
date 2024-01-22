---
title: Magnetische Inc-verbinding
description: Leer hoe u verbinding maakt met het Snapchat Ads Platform en uw publiek exporteert vanuit Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 1%

---

# Magnetische Inc-verbinding

## Overzicht {#overview}

[Snapchat-advertenties](https://forbusiness.snapchat.com/) worden gemaakt voor elk bedrijf, ongeacht de grootte of de industrie. Word onderdeel van de dagelijkse gesprekken van Snapchatters met digitale advertenties op volledig scherm die inspireren tot actie van de mensen die het belangrijkst zijn voor uw bedrijf.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door *Magnetische Inc.* team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *dev-support@snap.com*

## Gebruiksscenario’s {#use-cases}

Met deze bestemming kunnen marketers gebruikerssoorten die in Experience Platform zijn gemaakt, importeren in Snapchat Advertenties en deze gebruiken om hun advertenties te activeren.

## Vereisten {#prerequisites}

Als u deze bestemming wilt gebruiken, moet u een account voor Snapchat Ads hebben. Raadpleeg deze documentatie voor informatie over het maken van een dergelijke documentatie:

[Aan de slag met Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Beperkingen {#limitations}

* Snap Inc ondersteunt geen meervoudige identiteiten voor een bepaald publiekssegment. Wijs slechts één identiteit toe wanneer u een segment activeert.
* Snap Inc biedt geen ondersteuning voor het wijzigen van de naam van segmenten. Als u de naam van een segment wilt wijzigen, moet u het deactiveren, de naam ervan wijzigen en vervolgens het segment activeren.
* Het is niet mogelijk om een bewaarperiode voor de leden van een publiekssegment te bepalen. Alle leden hebben levensbehoud en zullen in het publiek zijn tot zij worden verwijderd.

## Ondersteunde identiteiten {#supported-identities}

De *Magnetische Inc.* doel ondersteunt de activering van de identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

Alle id&#39;s die naar de *Magnetische Inc.* het doel moet worden gehasht in formaat SHA-256. Om gewone tekstherkenningstekens te hakken alvorens hen naar de bestemming te verzenden, controleer **[!UICONTROL Apply transformation]** optie bij het toewijzen van doel-id&#39;s voor het doel.

>[!WARNING]
> 
> Ononderbroken id&#39;s worden niet geaccepteerd door de Magnetische Inc-bestemming en het verzenden ervan kan fouten veroorzaken.


>[!IMPORTANT]
> 
> De Magnetische bestemming Inc steunt geen veelvoudige identiteiten. Selecteer slechts één identiteit.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| E-mailadres | SHA-256 gehasht e-mailadres | E-mailadressen toewijzen aan het veld Doelidentiteit *emailAddress*. |
| Telefoonnummer | SHA-256 gehashed telefoonaantal | E-mailadressen toewijzen aan het veld Doelidentiteit *phoneNumber*. |
| GAID | SHA-256 gehashte Google Advertising ID | Advertentie-id&#39;s voor Google toewijzen aan het veld Doelidentiteit *onbeschaamd*. |
| IDFA | SHA-256 gehashte Apple Advertising ID | Advertentie-id&#39;s voor Apple toewijzen aan het veld Doelidentiteit *idfa*. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster *UW BESTEMMING* bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinding maken met Magnetische Inc {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

### Verifiëren voor bestemming {#authenticate}

Ga als volgt te werk om te verifiëren bij de bestemming:

1. Zoek de *Magnetische Inc.* doel uit Adobe Experience Platform-doelcatalogus en selecteer **Instellen**.
2. Selecteer **[!UICONTROL Connect to destination]**. U wordt omgeleid naar het volgende scherm:
   ![Auteursscherm 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Voer uw gegevens voor Snapchat in en selecteer **Aanmelden**.
4. De gegevens voor Snapchat waartoe Adobe Experience Platform toegang heeft, worden weergegeven. Selecteren **Doorgaan** om door te gaan met het verbindingsproces.

![Auth Screen 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Nadat u hebt geselecteerd, wacht u tot u weer naar Adobe Experience Platform bent omgeleid.

### Doelgegevens invullen {#destination-details}

![Doelgegevens](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Om details voor de bestemming te vormen, vul de vereiste gebieden in en selecteer **[!UICONTROL Next]**.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: De account-id voor advertenties die is gekoppeld aan het advertentieaccount waarnaar u uw publiek wilt importeren. Voor meer informatie over hoe u dit kunt vinden, raadpleegt u [deze documentatie op het Snapchat Business Help Center](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Als u een onjuiste of ongeldige account-id voor Snapchat-advertentie invoert, mislukt de activering van het publiek. Controleer nogmaals of je de juiste gebruikersnaam voor je advertentieaccount hebt ingevoerd.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Na activering van het publiek naar de *Magnetische Inc.* doel, kunt u het publiek weergeven in het venster Beheer magnetische advertenties [**Soorten publiek** sectie](https://businesshelp.snapchat.com/s/article/audience-sharing). Ga als volgt te werk om naar deze sectie te navigeren:

1. Aanmelden bij [Advertentiebeheer magnetisch](https://ads.snapchat.com/)
2. Selecteren **Soorten publiek** in het keuzemenu in de linkerbovenhoek van het scherm. In de Audience Library ziet u het publiek dat u in Adobe Experience Platform hebt geactiveerd:

![Doelgroepen](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Houd er rekening mee dat wanneer een publiek van een Adobe voor het eerst wordt geactiveerd op Snap Inc., dit eerst als een leeg publiek wordt weergegeven. Adobe Experience Platform exporteert ledengegevens namelijk pas naar Snap Inc als het publiek wordt geëvalueerd. Voor meer informatie over de manier waarop het publiek in Experience Platform wordt beoordeeld, raadpleegt u de [Overzicht van segmentatieservice](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments).

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).
