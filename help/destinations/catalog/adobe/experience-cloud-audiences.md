---
title: (Bèta) Experience Cloud-publiek
description: Leer hoe u publiek kunt delen van Experience Platform naar verschillende oplossingen voor Experience Platforms.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# (bèta) [!UICONTROL Experience Cloud Audiences] verbinding

Met deze bestemming kunt u soorten publiek van Experience Platform naar verschillende Experience Cloud-oplossingen delen, zoals Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target of Marketo.

![De bestemming van het publiek van de Experience Cloud, die in de bestemmingscatalogus wordt benadrukt.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Dit doel vervangt het [integratie voor delen van erfenis](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) van Experience Platform naar diverse Experience Cloud oplossingen.
>* Deze bestemming is momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

## Gebruik gevallen en voordelen {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!UICONTROL Experience Cloud Audiences] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Gebruiksgevallen van Platforms voor gegevensbeheer inschakelen {#dmp-use-cases}

In Audience Manager, kunt u het publiek van het Experience Platform voor de gebruiksgevallen van het Platform van het Beheer van Gegevens gebruiken, zoals:

* Toevoegen [gegevens van derden](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) naar uw segmenten;
* [Algorithmming](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Activeer uw publiek aan op koekjes-gebaseerde bestemmingen die nog niet in de catalogus van de bestemmingen van het Experience Platform worden gesteund.

### Kortere controle van het geëxporteerde publiek {#segments-control}

Gebruik de nieuwe zelfbedieningspersoneel die integratie via de bestemming van het Soorten publiek van de Experience Cloud deelt om te selecteren welk publiek naar Audience Manager en verder moet uitvoeren. Hierdoor kunt u bepalen welk publiek u met andere Experience Cloud-oplossingen wilt delen en welk publiek u uitsluitend in het Experience Platform wilt houden.

Dankzij de integratie van het oude publiek voor het delen van het publiek kon er geen korrelige controle worden verkregen over het publiek dat naar de Audience Manager en daarbuiten zou moeten worden geëxporteerd.

### Experience Platform-publiek delen met verdere Experience Cloud-oplossingen {#share-segments-with-other-solutions}

Behalve het delen van publiek met Audience Manager, laat de de bestemmingskaart van het Soorten publiek van het Experience Platform u toe om publiek met om het even welke andere oplossing van Experience Cloud te delen waarvoor u, met inbegrip van wordt voorzien:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share audiences to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
> * Deze bestemming is beschikbaar voor [Adobe Real-time Customer Data Platform Prime en Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.
> * U hebt een licentie voor Audience Managers nodig om de [Gebruiksgevallen van Platforms voor gegevensbeheer](#dmp-use-cases) genoemd.
> * U *niet nodig* een licentie van de Audience Manager om het publiek in de Experience Platform te delen met Adobe Advertising Cloud, Adobe Target, Marketo en andere Experience Cloud oplossingen die in de [sectie hierboven](#share-segments-with-other-solutions).

### Voor klanten die de oplossing voor het delen van het verouderde publiek gebruiken

Als u al publiek deelt van Experience Platform aan Audience Manager en andere oplossingen van Experience Cloud via [integratie voor delen van erfenis](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), dient u contact op te nemen met de klantenservice of uw Adobe-accountteam om de verouderde integratie uit te schakelen. De de rekeningsteams van de Zorg van de klant en van de Adobe- rekening moeten een kaartje van Jira (zie malplaatjekaartje PLAT-160986) indienen om de integratie onbruikbaar te maken.

De doorlooptijd voor het oplossen van het deprovisioning-ticket voor bètaklanten is zes werkdagen of minder. Nadat de bestaande oudere integratie is uitgeschakeld, kunt u doorgaan naar [verbinding maken](#connect) via de zelfbedieningsdoelkaart.

>[!IMPORTANT]
>
>Het publiek dat van Experience Platform naar uw andere oplossingen wordt uitgevoerd zal in de tijd tussen de het kaartresolutie van Jira en de tijd worden tegengehouden een nieuwe verbinding door de bestemmingskaart wordt gevestigd. U kunt deze uitvaltijd minimaliseren door de verbinding via de doelkaart te maken zodra het Jira-ticket is gesloten.

## Bekende beperkingen en bijschriften {#known-limitations}

Neem nota van de volgende bekende beperkingen en belangrijke callouts in de bètaversie van de kaart van het publiek van de Experience Cloud:

* [Controle van gegevensstromen](/help/dataflows/ui/monitor-destinations.md) wordt niet ondersteund.
* Wanneer u verbinding maakt met het doel, kunt u een optie weergeven op [gegevensstroomwaarschuwingen inschakelen](#enable-alerts). Hoewel het zichtbaar is in de UI, **optie voor inschakelen van waarschuwingen wordt niet ondersteund** in de bètaversie.
* **Back-ups worden niet ondersteund**. Bij de eerste export naar Audience Manager of andere Experience Cloud-oplossingen is geen sprake van een historische populatie van het publiek.
* In de bètaversie kunt u **één enkele bestemmingsverbinding aan de bestemming van het publiek van de Experience Cloud**, in alle sandboxen die tot uw organisatie van het Experience Platform behoren.

### Latentie bij activering van publiek {#audience-activation-latency}

Er is een wachttijd van vier uur tussen de tijd dat het publiek voor het eerst in Experience Platform wordt geactiveerd en de tijd dat zij klaar zijn om te worden gebruikt in Audience Manager en andere Experience Cloud oplossingen voor bepaalde gebruiksgevallen.

Het kan tot 24 uur duren voordat het publiek volledig beschikbaar is in de Audience Manager voor alle gebruiksgevallen en tot 48 uur voordat het publiek van het Experience Cloud publiek in de rapporten van de Audience Manager verschijnt.

Metagegevens, zoals publieksnamen, zijn beschikbaar in Audience Manager binnen minuten nadat u het exporteren hebt ingesteld op de bestemming Experience Cloud publiek.

## Ondersteunde identiteiten {#supported-identities}

De profielen die worden geëxporteerd naar de [!UICONTROL Experience Cloud Audiences] de bestemming wordt toegewezen aan de in de onderstaande tabel beschreven identiteiten. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](/help/identity-service/ecid.md) voor meer informatie . |
| GAID | Google-advertentie-id | Profielen die in Experience Platform worden opgenomen met een primaire identiteit van de advertentie-id van Google (GAID) kunnen naar deze bestemming worden geëxporteerd. |
| IDFA | Apple-id voor adverteerders | Profielen die in Experience Platform worden opgenomen met een primaire Apple-id voor adverteerders (IDFA), kunnen naar deze bestemming worden geëxporteerd. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Profielen die in Experience Platform worden opgenomen met een primair e-mailadres voor hashes, kunnen naar dit doel worden geëxporteerd. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie worden alle soorten publiek beschreven die u naar deze bestemming kunt exporteren.

Deze bestemming steunt de activering van alle publiek dat door het Experience Platform wordt geproduceerd [Segmenteringsservice](../../../segmentation/home.md).

*Aanvullend* Deze bestemming ondersteunt ook de activering van het publiek zoals beschreven in de onderstaande tabel.

| Type publiek | Beschrijving |
---------|----------|
| Aangepaste uploads | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek die zijn afgesneden van de identiteiten die in de bovenstaande sectie worden vermeld. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

>[!IMPORTANT]
> 
>In de bètaversie kunt u één doelverbinding maken met de bestemming Experience Cloud publiek, voor alle sandboxen die tot uw organisatie van het Experience Platform behoren.

### Verifiëren voor bestemming {#authenticate}

Om voor authentiek te verklaren aan de bestemming, uitgezocht **[!UICONTROL Set up]** in de weergave van de doelkaart in de catalogus en selecteer **[!UICONTROL Connect to destination]**.

![Weergave van de optie Verbinding maken met doel voor het doel Soorten publiek van Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Vorm nieuw bestemmingsscherm dat de vereiste en facultatieve montages toont om met de bestemming van het Soorten publiek van de Experience Cloud te verbinden.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.


## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming. Let op: [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) is vereist en [planstap](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) is beschikbaar voor deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Om succesvolle gegevensuitvoer te bevestigen, kunt u controleren dat uw publiek het tot uw gewenste oplossing van de Experience Cloud met succes heeft gemaakt.

### Gegevens valideren in Audience Manager

Uw publiek van het Experience Platform verschijnt in Audience Manager als [signalen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [kenmerken](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), en [segmenten](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). U kunt in Audience Manager verifiëren of de gegevens zijn weergegeven zoals beschreven in de bovenstaande documentatiekoppelingen.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

Het gegevensbeheer in Experience Platform wordt door beide partijen afgedwongen [gegevensgebruikslabels](/help/data-governance/labels/reference.md) en marketingacties.
Labels voor gegevensgebruik worden overgedragen naar toepassingen, maar marketingacties niet. Dit betekent dat wanneer ze in Audience Manager landen, het publiek uit Experience Platform naar alle beschikbare bestemmingen kan worden geëxporteerd. In Audience Manager kunt u [besturingselementen voor exporteren van gegevens](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) om te voorkomen dat het publiek naar bepaalde bestemmingen wordt geëxporteerd.

### Machtigingenbeheer in Audience Manager

Soorten publiek en sporen in de Audience Manager zijn onderworpen aan [Op rollen gebaseerde toegangscontroles](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=en) (RBAC).

Het publiek dat van Experience Platform wordt uitgevoerd wordt toegewezen aan een specifieke gegevensbron in Audience Manager genoemd **[!UICONTROL Experience Platform Segments]**.

Om slechts bepaalde gebruikers toegang tot het publiek toe te staan, kunt u toegangscontroles op het publiek toepassen dat tot de gegevensbron behoort. U moet nieuwe toegangsbeheertoestemmingen in Audience Manager voor deze publiek en sporen plaatsen die van de segmenten van het Experience Platform worden gecreeerd.
