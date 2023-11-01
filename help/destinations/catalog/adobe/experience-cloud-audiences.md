---
title: Experience Cloud-doelgroepen
description: Leer hoe u publiek kunt delen van Real-time Customer Data Platform naar verschillende Experience Cloud-apps.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1651'
ht-degree: 1%

---


# [!UICONTROL Experience Cloud Audiences] verbinding

>[!AVAILABILITY]
>
> Deze bestemming is beschikbaar voor [Adobe Real-time Customer Data Platform Prime en Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

Gebruik deze bestemming om publiek van Real-Time CDP aan Audience Manager en Adobe Analytics te activeren. U hebt een licentie voor Audience Managers nodig om een publiek naar Adobe Analytics te sturen.

Als u het publiek naar andere oplossingen voor Adobe wilt sturen, gebruikt u de directe verbindingen van Real-Time CDP naar [Adobe Target](../personalization/adobe-target-connection.md), [Adobe Advertising](../advertising/adobe-advertising-cloud-connection.md), [Adobe Campaign](../email-marketing/adobe-campaign.md) en [Marketo Engage](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Dit doel vervangt het [integratie voor delen van erfenis](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) van Real-time Customer Data Platform naar diverse oplossingen voor Experiencen Cloud.
> 
>Als u al publiek deelt van Real-Time CDP naar Audience Manager en andere oplossingen voor Experiencen Cloud via de [integratie voor delen van erfenis](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), dient u contact op te nemen met de klantenservice om de oudere integratie uit te schakelen voordat u deze bestemming gebruikt.

![De bestemming van het publiek van het Experience Cloud, die in de bestemmingscatalogus wordt benadrukt.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Gebruik gevallen en voordelen {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!UICONTROL Experience Cloud Audiences] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Real-Time CDP kunnen oplossen door deze bestemming te gebruiken.

### Gebruiksgevallen van het platform voor gegevensbeheer inschakelen {#dmp-use-cases}

In Audience Manager kunt u Real-Time CDP-publiek gebruiken voor het gebruik van gegevensbeheerplatform, zoals:

* Toevoegen [gegevens van derden](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html#third-party-data) naar uw segmenten;
* [Algorithmming](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html);
* Het activeren van uw publiek naar op cookies gebaseerde doelen die nog niet worden ondersteund in de catalogus met Real-Time CDP-doelen.

### Kortere controle van het geëxporteerde publiek {#segments-control}

Gebruik de nieuwe zelfbedieningspersoneel die integratie via de bestemming van het Soorten publiek van het Experience Cloud deelt om te selecteren welk publiek naar Audience Manager en verder moet uitvoeren. Op deze manier kunt u bepalen welk publiek u wilt delen met andere oplossingen voor Experiencen Cloud en welk publiek u uitsluitend in Real-Time CDP wilt houden.

Dankzij de integratie van het oude publiek voor het delen van het publiek kon er geen korrelige controle worden verkregen over het publiek dat naar de Audience Manager en daarbuiten zou moeten worden geëxporteerd.

### Real-Time CDP-publiek delen met verdere oplossingen voor Experience Cloud {#share-segments-with-other-solutions}

Naast het delen van publiek met Audience Manager, laat de de bestemmingskaart van het Soorten publiek van Real-Time CDP u toe om publiek met een andere oplossing van het Experience Cloud te delen die u wordt voorzien, met inbegrip van:

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
> * U hebt een licentie voor Audience Managers nodig om de [Gebruiksscenario&#39;s van het platform voor gegevensbeheer](#dmp-use-cases) genoemd.
> * U *niet nodig* een Audience Manager-licentie om Real-Time CDP-publiek te delen met Adobe Advertising Cloud, Adobe Target, Marketo en andere oplossingen voor Experiencen Cloud die in het [sectie hierboven](#share-segments-with-other-solutions).

### Voor klanten die de oplossing voor het delen van het verouderde publiek gebruiken

Als u al publiek deelt van Real-Time CDP naar Audience Manager en andere oplossingen voor Experiencen Cloud via de [integratie voor delen van erfenis](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), dient u contact op te nemen met de klantenservice om de oudere integratie uit te schakelen.

De doorlooptijd om het uitstelticket op te lossen is zes werkdagen of minder. Nadat de bestaande oudere integratie is uitgeschakeld, kunt u doorgaan naar [verbinding maken](#connect) via de zelfbedieningsdoelkaart.

>[!IMPORTANT]
>
>Het publiek dat van Real-Time CDP naar uw andere oplossingen wordt uitgevoerd zal worden tegengehouden in de tijd tussen de ticketresolutie en de tijd een nieuwe verbinding door de bestemmingskaart wordt gevestigd. U kunt deze onderbreking minimaliseren door de verbinding via de bestemmingskaart te creëren zodra het kaartje wordt gesloten.

## Bekende beperkingen en bijschriften {#known-limitations}

Merk op de volgende bekende beperkingen en belangrijke callouts terwijl het gebruiken van de kaart van het publiek van het Experience Cloud:

* Momenteel, wordt één enkele bestemming van het publiek van het Experience Cloud gesteund. Het proberen om een tweede bestemmingsverbinding te vormen zal in een fout resulteren.
* Wanneer u verbinding maakt met het doel, kunt u een optie weergeven op [gegevensstroomwaarschuwingen inschakelen](../../ui/alerts.md). Hoewel het zichtbaar is in de UI, **optie voor inschakelen van waarschuwingen wordt momenteel niet ondersteund**.
* **Ondersteuning voor backfill voor het publiek**: De eerste export naar Audience Manager of andere oplossingen voor Experiencen Cloud omvat een historische bevolkingsgroep van het publiek. Gebruikers van de [integratie voor delen van erfenis](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) die deze bestemming vormen zou een backfill verschil van ongeveer 6 uren moeten verwachten.

### Latentie bij activering van publiek {#audience-activation-latency}

Er is een vertraging van vier uur tussen de tijd dat het publiek voor het eerst in Real-Time CDP wordt geactiveerd en de tijd dat het publiek klaar is om te worden gebruikt in Audience Manager en andere oplossingen voor Experiencen Cloud voor bepaalde gebruiksgevallen.

Het kan tot 24 uur duren voordat het publiek volledig beschikbaar is in de Audience Manager voor alle gebruiksgevallen en tot 48 uur voordat het publiek uit het Experience Cloud publiek in de rapporten over de Audience Manager verschijnt.

Metagegevens, zoals publieksnamen, zijn beschikbaar in Audience Manager binnen minuten na het instellen van de exportbewerking naar het doelpubliek van het Experience Cloud.

## Ondersteunde identiteiten {#supported-identities}

De profielen die worden geëxporteerd naar de [!UICONTROL Experience Cloud Audiences] de bestemming wordt toegewezen aan de in de onderstaande tabel beschreven identiteiten. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](/help/identity-service/ecid.md) voor meer informatie . |
| GAID | Google-advertentie-id | Profielen die in Real-Time CDP worden binnengebracht met een primaire identiteit van Google Advertising ID (GAID) kunnen naar deze bestemming worden geëxporteerd. |
| IDFA | Apple-id voor adverteerders | Profielen die in Real-Time CDP worden binnengebracht met de primaire identiteit Apple ID for Advertisers (IDFA) kunnen naar deze bestemming worden geëxporteerd. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Profielen die in Real-Time CDP worden binnengebracht met een primaire identiteit van het gehashte e-mailadres, kunnen naar deze bestemming worden geëxporteerd. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek die zijn afgesneden van de identiteiten die in de bovenstaande sectie worden vermeld. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Real-Time CDP wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Om voor authentiek te verklaren aan de bestemming, uitgezocht **[!UICONTROL Set up]** in de weergave van de doelkaart in de catalogus en selecteer **[!UICONTROL Connect to destination]**.

![Weergave van de optie Verbinden met doel voor het doel Soorten publiek van Experience Cloud.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Vorm nieuw bestemmingsscherm dat de vereiste en facultatieve montages toont om met de bestemming van het Publiek van het Experience Cloud te verbinden.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming. Let op: [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) is vereist en [planstap](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) is beschikbaar voor deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Om succesvolle gegevensuitvoer te bevestigen, kunt u controleren dat uw publiek het tot uw gewenste oplossing van het Experience Cloud met succes heeft gemaakt.

### Gegevens valideren in Audience Manager

Uw Real-Time CDP-publiek wordt in de Audience Manager weergegeven als [signalen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-signals), [kenmerken](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-traits), en [segmenten](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-segments). U kunt in Audience Manager verifiëren of de gegevens zijn weergegeven zoals beschreven in de bovenstaande documentatiekoppelingen.

Segmentnamen worden 15 minuten nadat het publiek vanuit Real-Time CDP is verstuurd, in Audience Manager ingevuld.

De segmentpopulatie begint binnen 6 uur na verzending vanuit Real-Time CDP in de Audience Manager te stromen en wordt elke 24 uur in de Audience Manager bijgewerkt.

Na 72 uur is de volledige populatie zichtbaar in de Audience Manager en de populaties zullen naar de Audience Manager blijven stromen, tenzij het publiek van de bestemming in Real-Time CDP wordt verwijderd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Real-Time CDP] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

Het gegevensbeheer in Real-Time CDP wordt door beide partijen afgedwongen [gegevensgebruikslabels](/help/data-governance/labels/reference.md) en marketingacties.
Labels voor gegevensgebruik worden overgedragen naar toepassingen, maar marketingacties niet. Dit betekent dat wanneer ze in Audience Manager landen, het publiek uit Real-Time CDP naar alle beschikbare bestemmingen kan worden geëxporteerd. In Audience Manager kunt u [besturingselementen voor exporteren van gegevens](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html) om te voorkomen dat het publiek naar bepaalde bestemmingen wordt geëxporteerd.

Met de [!DNL HIPAA] marketingactie wordt niet verzonden van Real-Time CDP naar Audience Manager.

### Machtigingenbeheer in Audience Manager

Soorten publiek en sporen in de Audience Manager zijn onderworpen aan [Op rollen gebaseerde toegangscontroles](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) (RBAC).

Uit Real-Time CDP geëxporteerde soorten publiek worden toegewezen aan een specifieke gegevensbron in de Audience Manager **[!UICONTROL Experience Platform Segments]**.

Om slechts bepaalde gebruikers toegang tot het publiek toe te staan, kunt u toegangscontroles op het publiek toepassen dat tot de gegevensbron behoort. U moet nieuwe toegangsbeheertoestemmingen in Audience Manager voor deze publiek en sporen plaatsen die van de segmenten van Real-Time CDP worden gecreeerd.
