---
title: Experience Cloud-doelgroepen
description: Leer hoe u publiek kunt delen van Real-Time Customer Data Platform naar verschillende Experience Cloud-apps.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 00da5d8c0eaaecb5b1f5ad5bff7482f3bf4023e2
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# [!UICONTROL Experience Cloud Audiences] verbinding

>[!AVAILABILITY]
>
> Deze bestemming is beschikbaar aan [&#x200B; Adobe Real-Time Customer Data Platform Prime en Ultimate &#x200B;](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

Met deze bestemming activeert u het publiek van Real-Time CDP naar Audience Manager en Adobe Analytics.

Als u een publiek naar Adobe Analytics wilt sturen, hebt u een Audience Manager-licentie nodig. Voor meer details, zie het [&#x200B; overzicht van Audience Analytics &#x200B;](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=nl-NL).

Om publiek naar andere oplossingen van Adobe te verzenden, gebruik de directe verbindingen van Real-Time CDP aan [&#x200B; Adobe Target &#x200B;](../personalization/adobe-target-connection.md), [&#x200B; Adobe Advertising &#x200B;](../advertising/adobe-advertising-cloud-connection.md), [&#x200B; Adobe Campaign &#x200B;](../email-marketing/adobe-campaign.md) en [&#x200B; Marketo Engage &#x200B;](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Deze bestemming vervangt de [&#x200B; erfenis publiek-delende integratie &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL#aep-segments-in-aam) van Real-Time Customer Data Platform aan diverse oplossingen van Experience Cloud.
> 
>Als u reeds publiek van Real-Time CDP aan Audience Manager en andere oplossingen van Experience Cloud via de [&#x200B; erfenis publiek-delende integratie &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL#aep-segments-in-aam) deelt, moet u de Zorg van de Klant contacteren om de erfenisintegratie onbruikbaar te maken alvorens deze bestemming te gebruiken.

![&#x200B; de bestemming van het publiek van Experience Cloud, die in de bestemmingscatalogus wordt benadrukt.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Gebruik gevallen en voordelen {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!UICONTROL Experience Cloud Audiences] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Real-Time CDP door deze bestemming kunnen oplossen.

### Gebruiksgevallen van het platform voor gegevensbeheer inschakelen {#dmp-use-cases}

In Audience Manager kunt u een Real-Time CDP-publiek gebruiken voor het gebruik van gegevensbeheerplatforms, zoals:

* Het toevoegen van [&#x200B; derdegegevens &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=nl-NL#third-party-data) aan uw segmenten;
* [&#x200B; Algorithmic modelling &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=nl-NL);
* Het activeren van uw publiek naar op cookies gebaseerde doelen die nog niet worden ondersteund in de catalogus met Real-Time CDP-doelen.

### Kortere controle van het geëxporteerde publiek {#segments-control}

Om te selecteren welk publiek aan Audience Manager en verder te exporteren, gebruik de nieuwe zelf-dienst publiek-delende integratie via de bestemming van het Publiek van Experience Cloud.  Op deze manier kunt u bepalen welk publiek u met andere Experience Cloud-oplossingen wilt delen en welk publiek u alleen in Real-Time CDP wilt behouden.

Dankzij de integratie van het publiek in het verleden was er geen korrelige controle mogelijk, waarvan het publiek naar Audience Manager en daarbuiten zou moeten worden geëxporteerd.

### Real-Time CDP-publiek delen met Adobe Analytics {#share-audiences-with-analytics}

Publiek dat u naar de bestemming van het publiek van Experience Cloud verzendt, verschijnt niet automatisch in Adobe Analytics.

Alvorens u publiek naar Adobe Analytics kunt verzenden, moet u de Dienst van de Identiteit van Experience Cloud voor Analytics en Audience Manager [&#128279;](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=nl-NL) uitvoeren.

>[!IMPORTANT]
>
>Als u een publiek van Real-Time CDP naar Adobe Analytics wilt sturen via de bestemming Experience Cloud Publiek, moet u een Audience Manager-licentie hebben.

### Real-Time CDP-publiek delen met andere Experience Cloud-oplossingen {#share-segments-with-other-solutions}

U kunt de doelkaart van het publiek van Real-Time CDP gebruiken om publiek met andere oplossingen van Experience Cloud te delen.

Adobe raadt echter ten zeerste aan de volgende speciale doelkaarten te gebruiken als u het publiek met deze oplossingen wilt delen:

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Advertising Cloud](../advertising/adobe-advertising-cloud-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
> * U hebt een vergunning van Audience Manager nodig om de [&#x200B; het gebruiksgevallen van het Platform van het Beheer van Gegevens &#x200B;](#dmp-use-cases) toe te laten hierboven vermeld verder.
> * U *doet* behoefte een vergunning van Audience Manager om het publiek van Real-Time CDP met Adobe Analytics te delen.
> * U *hebt* geen vergunning van Audience Manager nodig om het publiek van Real-Time CDP met de Wolk van Adobe te delen Advertising, Adobe Target, Marketo, en andere oplossingen van Experience Cloud, die in de [&#x200B; sectie hierboven &#x200B;](#share-segments-with-other-solutions) worden vermeld.

### Voor klanten die de oplossing voor het delen van het verouderde publiek gebruiken

Als u reeds publiek van Real-Time CDP aan Audience Manager en andere oplossingen van Experience Cloud via de [&#x200B; erfenis publiek-delende integratie &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL#aep-segments-in-aam) deelt, moet u de Zorg van de Klant contacteren om de erfenisintegratie onbruikbaar te maken.

De doorlooptijd om het uitstelticket op te lossen is zes werkdagen of minder. Nadat de bestaande erfenisintegratie is onbruikbaar gemaakt, kunt u te werk gaan [&#x200B; een verbinding &#x200B;](#connect) tot stand brengen via de zelfbediening bestemmingskaart.

>[!IMPORTANT]
>
>Het publiek dat van Real-Time CDP naar uw andere oplossingen wordt uitgevoerd wordt tegengehouden in de tijd tussen de ticketresolutie en de tijd dat een nieuwe verbinding door de bestemmingskaart wordt gevestigd. U kunt deze onderbreking minimaliseren door de verbinding via de bestemmingskaart te creëren nadat het kaartje wordt gesloten.

## Bekende beperkingen en bijschriften {#known-limitations}

Let op de volgende bekende beperkingen en belangrijke callouts bij gebruik van de Experience Cloud Audiences-kaart:

* Momenteel kunt u de bestemming Experience Cloud-soorten publiek configureren in één sandbox per organisatie. Als u probeert een tweede doelverbinding te configureren in een andere sandbox, treedt een fout op.
* Wanneer het verbinden met de bestemming, kunt u een optie zien om [&#x200B; dataflow alarm &#x200B;](../../ui/alerts.md) toe te laten. Hoewel zichtbaar in UI, **toelaat alarm optie momenteel niet wordt gesteund**.
* **de backfill van het publiek steun**: De eerste uitvoer naar Audience Manager of andere oplossingen van Experience Cloud omvat een historische bevolking van het publiek. De gebruikers van de [&#x200B; erfenis publiek-delende integratie &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL#aep-segments-in-aam) die deze bestemming vormen zouden een backfill verschil van ongeveer zes uur moeten verwachten.
* Het publiek dat uit [&#x200B; Samenstelling van het Publiek &#x200B;](../../../segmentation/ui/audience-composition.md) voortkomt wordt niet direct gesteund. Om samengesteld publiek aan deze bestemming te activeren moet u een publieksdefinitie door [&#x200B; Bouwer van het Segment &#x200B;](../../../segmentation/ui/segment-builder.md) tot stand brengen die op uw samengesteld publiek wordt gebaseerd, en het pas gecreëerde publiek activeren.

### Latentie bij activering van publiek {#audience-activation-latency}

Er is een vertraging van vier uur tussen de tijd dat het publiek voor het eerst in Real-Time CDP wordt geactiveerd en de tijd dat het publiek klaar is om te worden gebruikt in Audience Manager en andere Experience Cloud-oplossingen.

Het kan tot 24 uur duren voordat het publiek volledig beschikbaar is in Audience Manager voor alle gebruiksgevallen. Het kan tot 48 uur duren voordat het publiek van Experience Cloud Audiences in Audience Manager-rapporten verschijnt.

Metagegevens, zoals publieksnamen, zijn beschikbaar in Audience Manager binnen minuten nadat u het exporteren hebt ingesteld op de bestemming Experience Cloud Publiek.

## Ondersteunde identiteiten {#supported-identities}

De profielen die naar de [!UICONTROL Experience Cloud Audiences] -bestemming worden geëxporteerd, worden toegewezen aan de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [&#x200B; ECID &#x200B;](/help/identity-service/features/ecid.md) voor meer informatie. |
| GAID | GOOGLE ADVERTISING ID | Profielen die in Real-Time CDP worden binnengebracht met een primaire identiteit van Google Advertising ID (GAID) kunnen naar deze bestemming worden geëxporteerd. |
| IDFA | Apple-id voor adverteerders | Profielen die in Real-Time CDP worden binnengebracht met de primaire identiteit Apple ID for Advertisers (IDFA) kunnen naar deze bestemming worden geëxporteerd. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Profielen die in Real-Time CDP worden binnengebracht met een primaire identiteit van het gehashte e-mailadres, kunnen naar deze bestemming worden geëxporteerd. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek die zijn afgesneden van de identiteiten die in de bovenstaande sectie worden vermeld. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Real-Time CDP wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Selecteer **[!UICONTROL Set up]** in de weergave met de doelkaart in de catalogus en selecteer **[!UICONTROL Connect to destination]** om de verificatie naar het doel uit te voeren.

![&#x200B; Mening van Connect aan bestemmingsoptie voor de bestemming van het publiek van Experience Cloud.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; vorm nieuw bestemmingsscherm dat de vereiste en facultatieve montages toont om met de bestemming van het publiek van Experience Cloud te verbinden.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming. Geen [&#x200B; toewijzingsstap &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) wordt vereist en geen [&#x200B; het plannen stap &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) is beschikbaar voor deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Om succesvolle gegevensuitvoer te bevestigen, kunt u controleren dat uw publiek het tot uw gewenste oplossing van Experience Cloud met succes heeft gemaakt.

### Gegevens valideren in Audience Manager

Uw publiek van Real-Time CDP verschijnt in Audience Manager als [&#x200B; signalen &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL#aep-segments-as-aam-signals), [&#x200B; trekken &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL#aep-segments-as-aam-traits), en [&#x200B; segmenten &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL#aep-segments-as-aam-segments). U kunt in Audience Manager controleren of de gegevens zijn weergegeven zoals beschreven in de bovenstaande documentatiekoppelingen.

Segmentnamen worden 15 minuten nadat het publiek vanuit Real-Time CDP is verstuurd, in Audience Manager ingevuld.

De segmentpopulatie begint binnen 6 uur na verzending vanuit Real-Time CDP naar Audience Manager te stromen en wordt elke 24 uur bijgewerkt in Audience Manager.

Na 72 uur zal de volledige bevolking in Audience Manager zichtbaar zijn en zullen de populaties naar Audience Manager blijven stromen, tenzij het publiek van de bestemming in Real-Time CDP wordt verwijderd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Real-Time CDP] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

Het bestuur van gegevens in Real-Time CDP wordt afgedwongen door zowel [&#x200B; etiketten van het gegevensgebruik &#x200B;](/help/data-governance/labels/reference.md) als marketing acties.
Met labels voor gegevensgebruik worden toepassingen overgedragen, maar marketingacties niet. Dit betekent dat wanneer ze in Audience Manager landen, het publiek uit Real-Time CDP naar alle beschikbare bestemmingen kan worden geëxporteerd. In Audience Manager, kunt u [&#x200B; controles van de gegevensuitvoer &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=nl-NL) gebruiken om publiek van het worden uitgevoerd naar bepaalde bestemmingen te blokkeren.

Soorten publiek dat is gemarkeerd met de marketingactie [!DNL HIPAA] , worden niet verzonden van Real-Time CDP naar Audience Manager.

### Machtigingenbeheer in Audience Manager

Het publiek en de sporen in Audience Manager zijn onderworpen aan [&#x200B; Op rol-Gebaseerde Controles van de Toegang &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=nl-NL) (RBAC).

Uit Real-Time CDP geëxporteerde soorten publiek worden toegewezen aan een specifieke gegevensbron in Audience Manager met de naam **[!UICONTROL Experience Platform Segments]** .

Om slechts bepaalde gebruikers toegang tot het publiek toe te staan, gebruik [&#x200B; Op rol-Gebaseerde Controles van de Toegang &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=nl-NL) om gebruikerstoegang tot het publiek en sporen te vormen die van het publiek van Real-Time CDP worden gecreeerd.
