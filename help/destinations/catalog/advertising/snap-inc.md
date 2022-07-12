---
title: (Bèta) Magnetische Inc-verbinding
description: Leer hoe u verbinding maakt met het Platform Snapchat Ads en uw publiekssegmenten exporteert vanuit Experience Platform.
source-git-commit: 14f7efc2d893bf081c4e167b46a3e85baeff4ec9
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 1%

---


# (Beta) Snap Inc

## Overzicht {#overview}

[Snapchat-advertenties](https://forbusiness.snapchat.com/) worden gemaakt voor elk bedrijf, ongeacht de grootte of de industrie. Word onderdeel van de dagelijkse gesprekken van Snapchatters met digitale advertenties op volledig scherm die inspireren tot actie van de mensen die het belangrijkst zijn voor uw bedrijf.

>[!IMPORTANT]
>
>Deze documentatiepagina is gemaakt door de *Magnetische Inc.* team. Dit is momenteel een bètaproduct en de functionaliteit kan worden gewijzigd. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *dev-support@snap.com*

## Gebruiksscenario’s {#use-cases}

Met deze bestemming kunnen marketers gebruikerssegmenten die in Experience Platform zijn gemaakt, importeren in Snapchat-advertenties en deze gebruiken om hun advertenties te activeren.

## Vereisten {#prerequisites}

Als u deze bestemming wilt gebruiken, moet u een account voor Snapchat Ads hebben. Raadpleeg deze documentatie voor informatie over het maken van een dergelijke documentatie:

[Aan de slag met Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Beperkingen {#limitations}

* Snap Inc ondersteunt geen meervoudige identiteiten voor een bepaald publiekssegment. Wijs slechts één identiteit toe wanneer u een segment activeert.
* Snap Inc biedt geen ondersteuning voor het wijzigen van de naam van segmenten. Als u de naam van een segment wilt wijzigen, moet u het deactiveren, de naam ervan wijzigen en vervolgens het segment activeren.
* Het is niet mogelijk om een bewaarperiode voor de leden van een publiekssegment te bepalen. Alle leden hebben levenbehoud en zullen in het segment zijn tot zij worden verwijderd.

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

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster *UW BESTEMMING* bestemming. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Verbinding maken met Magnetische Inc. {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

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

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: De account-id voor Advertentie die is gekoppeld aan de advertentierekening waarnaar u de segmenten wilt importeren. Voor meer informatie over hoe u dit kunt vinden, raadpleegt u [deze documentatie op het Snapchat Business Help Center](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Door het invoeren van een onjuiste of ongeldige account-id voor Snapchat wordt het activeren van segmenten mislukt. Controleer nogmaals of je de juiste gebruikersnaam voor je advertentieaccount hebt ingevoerd.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Na het activeren van segmenten op de *Magnetische Inc.* doel, kunt u de segmenten weergeven in de functie voor magnetische advertenties van Manager [**Soorten publiek** sectie](https://businesshelp.snapchat.com/s/article/audience-sharing). Ga als volgt te werk om naar deze sectie te navigeren:

1. Aanmelden bij [Advertentiebeheer magnetisch](https://ads.snapchat.com/)
2. Selecteren **Soorten publiek** in het keuzemenu in de linkerbovenhoek van het scherm. De segmenten die u in Adobe Experience Platform hebt geactiveerd, worden weergegeven in de Audience Library:

![Doelgroepen](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Houd er rekening mee dat wanneer een Adobe-segment voor het eerst wordt geactiveerd op Snap Inc., u dit eerst ziet als een leeg publiek. Dit komt doordat Adobe Experience Platform de lidgegevens niet naar Snap Inc exporteert totdat het segment wordt geëvalueerd. Voor meer informatie over hoe de segmenten in Experience Platform worden geëvalueerd, gelieve te verwijzen naar [Overzicht van segmentatieservice](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).