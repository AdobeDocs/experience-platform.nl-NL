---
title: Experience Cloud-doelgroepen
description: Leer hoe u publiek kunt delen van Real-time Customer Data Platform naar verschillende Experience Cloud-apps.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---


# [!UICONTROL Experience Cloud Audiences] verbinding

>[!AVAILABILITY]
>
> Deze bestemming is beschikbaar aan [ de Première en Ultimate ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten van Adobe Real-time Customer Data Platform.

Gebruik deze bestemming om publiek van Real-Time CDP aan Audience Manager en Adobe Analytics te activeren.

Als u een publiek naar Adobe Analytics wilt sturen, hebt u een licentie voor Audience Managers nodig. Voor meer details, zie het [ overzicht van het Audience Analytics ](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=en).

Om publiek naar andere oplossingen van de Adobe te verzenden, gebruik de directe verbindingen van Real-Time CDP aan [ Adobe Target ](../personalization/adobe-target-connection.md), [ Adobe Advertising ](../advertising/adobe-advertising-cloud-connection.md), [ Adobe Campaign ](../email-marketing/adobe-campaign.md) en [ Marketo Engage ](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Deze bestemming vervangt de [ erfenis publiek-delende integratie ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) van Real-time Customer Data Platform aan diverse oplossingen van het Experience Cloud.
> 
>Als u reeds publiek van Real-Time CDP aan Audience Manager en andere oplossingen van het Experience Cloud via de [ erfenis publiek-delende integratie ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) deelt, moet u de Zorg van de Klant contacteren om de erfenisintegratie onbruikbaar te maken alvorens deze bestemming te gebruiken.

![ de bestemming van het publiek van het Experience Cloud, die in de bestemmingscatalogus wordt benadrukt.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Gebruik gevallen en voordelen {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!UICONTROL Experience Cloud Audiences] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Real-Time CDP door deze bestemming kunnen oplossen.

### Gebruiksgevallen van het platform voor gegevensbeheer inschakelen {#dmp-use-cases}

In Audience Manager kunt u Real-Time CDP-publiek gebruiken voor het gebruik van gegevensbeheerplatform, zoals:

* Het toevoegen van [ derdegegevens ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html#third-party-data) aan uw segmenten;
* [ Algorithmic modelling ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html);
* Het activeren van uw publiek naar op cookies gebaseerde doelen die nog niet worden ondersteund in de catalogus met Real-Time CDP-doelen.

### Kortere controle van het geëxporteerde publiek {#segments-control}

Om te selecteren welk publiek aan Audience Manager en verder te exporteren, gebruik de nieuwe zelf-dienst publiek-delende integratie via de bestemming van het Publiek van het Experience Cloud.  Op deze manier kunt u bepalen welk publiek u wilt delen met andere oplossingen voor Experiencen Cloud en welk publiek u uitsluitend in Real-Time CDP wilt houden.

De verouderde integratie met het delen van het publiek maakte geen korrelige controle mogelijk waarvan het publiek naar Audience Manager en verder moest worden uitgevoerd.

### Real-Time CDP-publiek delen met Adobe Analytics {#share-audiences-with-analytics}

De soorten publiek die u naar de bestemming van het publiek van de Experience Cloud verzendt verschijnen niet automatisch in Adobe Analytics.

Alvorens u publiek naar Adobe Analytics kunt verzenden, moet u de Dienst van de Identiteit van het Experience Cloud voor Analytics en Audience Manager ](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=en) uitvoeren.[

>[!IMPORTANT]
>
>Als u het publiek van Real-Time CDP naar Adobe Analytics wilt sturen via de bestemming Experience Cloud publiek, moet u een licentie voor Audience Managers hebben.

### Real-Time CDP-publiek delen met andere oplossingen voor Experiencen Cloud {#share-segments-with-other-solutions}

U kunt de doelkaart van het publiek van Real-Time CDP gebruiken om publiek met andere oplossingen van het Experience Cloud te delen.

Nochtans, adviseert de Adobe sterk het gebruiken van de volgende specifieke bestemmingskaarten als u publiek met deze oplossingen wilt delen:

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Advertising Cloud](../advertising/adobe-advertising-cloud-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
> * U hebt een vergunning van de Audience Manager nodig om de [ het gebruikscase van het Platform van het Beheer van Gegevens ](#dmp-use-cases) toe te laten hierboven vermeld verder.
> * U *doet* behoefte een vergunning van de Audience Manager om het publiek van Real-Time CDP met Adobe Analytics te delen.
> * U *hebt* geen vergunning van de Audience Manager nodig om het publiek van Real-Time CDP met Adobe Advertising Cloud, Adobe Target, Marketo, en andere oplossingen van het Experience Cloud te delen, die in de [ sectie hierboven ](#share-segments-with-other-solutions) worden vermeld.

### Voor klanten die de oplossing voor het delen van het verouderde publiek gebruiken

Als u reeds publiek van Real-Time CDP aan Audience Manager en andere oplossingen van het Experience Cloud via de [ erfenis publiek-delende integratie ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) deelt, moet u de Zorg van de Klant contacteren om de erfenisintegratie onbruikbaar te maken.

De doorlooptijd om het uitstelticket op te lossen is zes werkdagen of minder. Nadat de bestaande erfenisintegratie is onbruikbaar gemaakt, kunt u te werk gaan [ een verbinding ](#connect) tot stand brengen via de zelfbediening bestemmingskaart.

>[!IMPORTANT]
>
>Het publiek dat van Real-Time CDP naar uw andere oplossingen wordt uitgevoerd wordt tegengehouden in de tijd tussen de ticketresolutie en de tijd dat een nieuwe verbinding door de bestemmingskaart wordt gevestigd. U kunt deze onderbreking minimaliseren door de verbinding via de bestemmingskaart te creëren nadat het kaartje wordt gesloten.

## Bekende beperkingen en bijschriften {#known-limitations}

Merk op de volgende bekende beperkingen en belangrijke callouts terwijl het gebruiken van de kaart van het publiek van het Experience Cloud:

* Momenteel, wordt één enkele bestemming van het publiek van het Experience Cloud gesteund. Als u probeert een tweede doelverbinding te configureren, treedt er een fout op.
* Wanneer het verbinden met de bestemming, kunt u een optie zien om [ dataflow alarm ](../../ui/alerts.md) toe te laten. Hoewel zichtbaar in UI, **toelaat alarm optie momenteel niet wordt gesteund**.
* **de backfill van het publiek steun**: De eerste uitvoer naar Audience Manager of andere oplossingen van het Experience Cloud omvat een historische bevolking van het publiek. De gebruikers van de [ erfenis publiek-delende integratie ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) die deze bestemming vormen zouden een backfill verschil van ongeveer zes uur moeten verwachten.
* Het publiek dat uit [ Samenstelling van het Publiek ](../../../segmentation/ui/audience-composition.md) voortkomt wordt niet direct gesteund. Om samengesteld publiek aan deze bestemming te activeren moet u een publieksdefinitie door [ Bouwer van het Segment ](../../../segmentation/ui/segment-builder.md) tot stand brengen die op uw samengesteld publiek wordt gebaseerd, en het pas gecreëerde publiek activeren.

### Latentie bij activering van publiek {#audience-activation-latency}

Er is een vertraging van vier uur tussen de tijd dat het publiek voor het eerst in Real-Time CDP wordt geactiveerd en de tijd dat het publiek klaar is om te worden gebruikt in Audience Manager en andere oplossingen voor Experiencen Cloud.

Het kan tot 24 uur duren voordat het publiek volledig beschikbaar is in de Audience Manager voor alle gebruiksgevallen. Het kan tot 48 uur duren voordat het publiek van het Experience Cloud publiek in de rapporten van de Audience Manager verschijnt.

Metagegevens, zoals publieksnamen, zijn beschikbaar in Audience Manager binnen minuten na het instellen van de exportbewerking naar het doelpubliek van het Experience Cloud.

## Ondersteunde identiteiten {#supported-identities}

De profielen die naar de [!UICONTROL Experience Cloud Audiences] -bestemming worden geëxporteerd, worden toegewezen aan de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ ECID ](/help/identity-service/features/ecid.md) voor meer informatie. |
| GAID | GOOGLE ADVERTISING ID | Profielen die in Real-Time CDP worden binnengebracht met een primaire identiteit van Google Advertising ID (GAID) kunnen naar deze bestemming worden geëxporteerd. |
| IDFA | Apple-id voor adverteerders | Profielen die in Real-Time CDP worden binnengebracht met de primaire identiteit Apple ID for Advertisers (IDFA) kunnen naar deze bestemming worden geëxporteerd. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Profielen die in Real-Time CDP worden binnengebracht met een primaire identiteit van het gehashte e-mailadres, kunnen naar deze bestemming worden geëxporteerd. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van het Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek die zijn afgesneden van de identiteiten die in de bovenstaande sectie worden vermeld. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Real-Time CDP wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Selecteer **[!UICONTROL Set up]** in de weergave met de doelkaart in de catalogus en selecteer **[!UICONTROL Connect to destination]** om de verificatie naar het doel uit te voeren.

![ Mening van Connect aan bestemmingsoptie voor de bestemming van het publiek van het Experience Cloud.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ vorm nieuw bestemmingsscherm dat de vereiste en facultatieve montages toont om met de bestemming van het publiek van de Experience Cloud te verbinden.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming. Geen [ toewijzingsstap ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) wordt vereist en geen [ het plannen stap ](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) is beschikbaar voor deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Om succesvolle gegevensuitvoer te bevestigen, kunt u controleren dat uw publiek het tot uw gewenste oplossing van het Experience Cloud met succes heeft gemaakt.

### Gegevens valideren in Audience Manager

Uw publiek van Real-Time CDP verschijnt in Audience Manager als [ signalen ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-signals), [ trekken ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-traits), en [ segmenten ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-segments). U kunt in Audience Manager verifiëren of de gegevens zijn weergegeven zoals beschreven in de bovenstaande documentatiekoppelingen.

Segmentnamen beginnen in Audience Manager te vullen 15 minuten nadat het publiek vanuit Real-Time CDP is verstuurd.

De segmentpopulatie begint binnen 6 uur na verzending vanuit Real-Time CDP in de Audience Manager te stromen en wordt elke 24 uur in de Audience Manager bijgewerkt.

Na 72 uur is de volledige populatie zichtbaar in de Audience Manager en de populaties zullen naar de Audience Manager blijven stromen, tenzij het publiek van de bestemming in Real-Time CDP wordt verwijderd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Real-Time CDP] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

Het bestuur van gegevens in Real-Time CDP wordt afgedwongen door zowel [ etiketten van het gegevensgebruik ](/help/data-governance/labels/reference.md) als marketing acties.
Met labels voor gegevensgebruik worden toepassingen overgedragen, maar marketingacties niet. Dit betekent dat wanneer ze in Audience Manager landen, het publiek uit Real-Time CDP naar alle beschikbare bestemmingen kan worden geëxporteerd. In Audience Manager, kunt u [ gegevens gebruiken de uitvoercontroles ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html) om publiek van het worden uitgevoerd naar bepaalde bestemmingen te blokkeren.

Soorten publiek dat is gemarkeerd met de marketingactie [!DNL HIPAA] , worden niet van Real-Time CDP naar de Audience Manager verzonden.

### Machtigingenbeheer in Audience Manager

Het publiek en de sporen in Audience Manager zijn onderworpen aan [ Op rol-Gebaseerde Controles van de Toegang ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) (RBAC).

Uit Real-Time CDP geëxporteerde soorten publiek worden toegewezen aan een specifieke gegevensbron in de Audience Manager **[!UICONTROL Experience Platform Segments]** .

Om slechts bepaalde gebruikers toegang tot het publiek toe te staan, gebruik [ Op rol-Gebaseerde Controles van de Toegang ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) om gebruikerstoegang tot het publiek en sporen te vormen die van het publiek van Real-Time CDP worden gecreeerd.
