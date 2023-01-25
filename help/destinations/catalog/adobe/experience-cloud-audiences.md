---
title: (Bèta) Experience Cloud-publiek
description: Leer hoe te om segmenten van Experience Platform aan diverse oplossingen van het Experience Platform te delen.
source-git-commit: 75eb72a8325c92961d9fe26f7e86d15fecf97043
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 0%

---


# (bèta) [!UICONTROL Experience Cloud Audiences] verbinding

Deze bestemming staat u toe om segmenten van Experience Platform aan diverse oplossingen van Experience Cloud, zoals Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Doel, of Marketo te delen.

![De bestemming van het publiek van de Experience Cloud, die in de bestemmingscatalogus wordt benadrukt.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Deze bestemming vervangt [integratie van oudere segmenten delen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) van Experience Platform naar diverse Experience Cloud oplossingen.
>* Deze bestemming is momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.


## Gebruik gevallen en voordelen {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!UICONTROL Experience Cloud Audiences] doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Gebruiksgevallen van Platforms voor gegevensbeheer inschakelen {#dmp-use-cases}

In Audience Manager, kunt u de segmenten van het Experience Platform voor de gebruiksgevallen van het Platform van het Beheer van Gegevens gebruiken, zoals:

* Toevoegen [gegevens van derden](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) naar uw segmenten;
* [Algorithmming](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Activeer uw segmenten aan op cookie-gebaseerde bestemmingen die nog niet in de de bestemmingscatalogus van het Experience Platform worden gesteund.

### Kortere controle van uitgevoerde segmenten {#segments-control}

Gebruik de nieuwe zelfbediening segmentdelingsintegratie via de bestemming van het Soorten publiek van de Experience Cloud om te selecteren welke segmenten naar Audience Manager en verder moeten uitvoeren. Dit staat u toe om te bepalen welke segmenten u met andere oplossingen van Experience Cloud wilt delen en welke segmenten u in Experience Platform exclusief wilt houden.

De integratie van het delen van oudere segmenten maakte geen korrelige controle mogelijk van welke segmenten naar Audience Manager en verder zouden moeten worden uitgevoerd.

### De segmenten van het Experience Platform van het aandeel met verdere oplossingen van Experience Cloud {#share-segments-with-other-solutions}

Behalve het delen van segmenten met Audience Manager, laat de de bestemmingskaart van het Soorten publiek van het Experience Platform u toe om segmenten met een andere oplossing van Experience Cloud te delen die u wordt voorzien, die omvat:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
> * Deze bestemming is beschikbaar voor [Adobe Real-time Customer Data Platform Prime en Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.
> * U hebt een licentie voor Audience Managers nodig om de in de bovenstaande sectie vermelde gebruiksgevallen voor het Platform voor gegevensbeheer in te schakelen.
> * U *niet nodig* een licentie van de Audience Manager om Experience Platform-segmenten te delen met Adobe Advertising Cloud, Adobe Target, Marketo en andere Experience Cloud-oplossingen, via de integratie van het Experience Cloud publiek.


### Voor klanten die de oplossing voor het delen van het verouderde segment gebruiken

Als u reeds segmenten van Experience Platform aan Audience Manager en andere oplossingen van Experience Cloud via deelt [integratie van oudere segmenten delen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam), dient u contact op te nemen met de klantenservice of met de succesmanager van de klant om de integratie van oudere systemen uit te schakelen. De teams van het Beheer van de Zorg van de Klant en van de Steun van de Klant moeten een Jira kaartje (zie malplaatjekaartje AAM-52354) indienen om de integratie onbruikbaar te maken.

De doorlooptijd voor het oplossen van het deprovisioning-ticket voor bètaklanten is zes werkdagen of minder. Nadat de bestaande oudere integratie is uitgeschakeld, kunt u doorgaan naar [verbinding maken](#connect) via de zelfbedieningsdoelkaart.

>[!IMPORTANT]
>
>De segmentexport van Experience Platform naar uw andere oplossingen wordt gestopt in de tijd tussen de Jira-ticketresolutie en de tijd dat een nieuwe verbinding tot stand wordt gebracht via de doelkaart. U kunt deze uitvaltijd minimaliseren door de verbinding via de doelkaart te maken zodra het Jira-ticket is gesloten.

## Bekende beperkingen en bijschriften {#known-limitations}

Neem nota van de volgende bekende beperkingen en belangrijke callouts in de bètaversie van de kaart van het publiek van de Experience Cloud:

* [Controle van gegevensstromen](/help/dataflows/ui/monitor-destinations.md) wordt niet ondersteund.
* Wanneer u verbinding maakt met het doel, kunt u een optie weergeven op [gegevensstroomwaarschuwingen inschakelen](#enable-alerts). Hoewel het zichtbaar is in de UI, **optie voor inschakelen van waarschuwingen wordt niet ondersteund** in de bètaversie.
* **Back-ups worden niet ondersteund**. De eerste uitvoer naar Audience Manager of andere Experience Cloud-oplossingen omvat geen historische populatie van de segmenten.
* In de bètaversie kunt u **één enkele bestemmingsverbinding aan de bestemming van het publiek van de Experience Cloud**, in alle sandboxen die tot uw organisatie van het Experience Platform behoren.
* Er is een **4-uurs latentie** tussen de tijd dat de gegevens in het Experience Platform worden geactiveerd en de tijd dat de gegevens klaar zijn om te worden gebruikt in Audience Manager- en andere Experience Cloud-oplossingen.

## Ondersteunde identiteiten {#supported-identities}

De profielen die worden geëxporteerd naar de [!UICONTROL Experience Cloud Audiences] de bestemming wordt toegewezen aan de in de onderstaande tabel beschreven identiteiten. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Naar deze naamruimte kan ook worden verwezen door de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](/help/identity-service/ecid.md) voor meer informatie . |
| GAID | Google-advertentie-id | Profielen die in Experience Platform worden opgenomen met een primaire Google-advertentie-id (GAID) kunnen naar deze bestemming worden geëxporteerd. |
| IDFA | Apple-id voor adverteerders | Profielen die in Experience Platform worden opgenomen met een primaire Apple-id voor adverteerders (IDFA), kunnen naar deze bestemming worden geëxporteerd. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Profielen die in Experience Platform worden opgenomen met een primair e-mailadres voor hashes, kunnen naar dit doel worden geëxporteerd. |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) die zijn afgesneden van de identiteiten die in de bovenstaande sectie worden vermeld. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

>[!IMPORTANT]
> 
>In de bètaversie kunt u één doelverbinding maken met de bestemming Experience Cloud publiek, voor alle sandboxen die tot uw organisatie van het Experience Platform behoren.

### Verifiëren voor bestemming {#authenticate}

Om voor authentiek te verklaren aan de bestemming, selecteer **[!UICONTROL Set up]** in de weergave van de doelkaart in de catalogus en selecteer **[!UICONTROL Connect to destination]**.

![Weergave van de optie Verbinding maken met doel voor het doel Soorten publiek van Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Vorm nieuw bestemmingsscherm dat de vereiste en facultatieve montages toont om met de bestemming van het Soorten publiek van de Experience Cloud te verbinden.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.


## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming. Let op: [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) is vereist en [planstap](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) is beschikbaar voor deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Om succesvolle gegevensuitvoer te bevestigen, kunt u controleren dat uw segmenten het tot uw gewenste oplossing van de Experience Cloud met succes hebben gemaakt.

### Gegevens valideren in Audience Manager

Uw Experience Platform-segmenten worden in Audience Manager weergegeven als [signalen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [kenmerken](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), en [segmenten](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). U kunt in Audience Manager verifiëren of de gegevens zijn weergegeven zoals beschreven in de bovenstaande documentatiekoppelingen.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

Het gegevensbeheer in Experience Platform wordt door beide partijen afgedwongen [gegevensgebruikslabels](/help/data-governance/labels/reference.md) en marketingacties.
Labels voor gegevensgebruik worden overgedragen naar toepassingen, maar marketingacties niet. Dit betekent dat segmenten van Experience Platform die in Audience Manager worden aangevoerd, naar alle beschikbare bestemmingen kunnen worden uitgevoerd. In Audience Manager kunt u [besturingselementen voor exporteren van gegevens](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) om segmenten te blokkeren van wordt uitgevoerd naar bepaalde bestemmingen.

### Machtigingenbeheer in Audience Manager

Segmenten en kenmerken in Audience Manager zijn onderworpen aan [Op rollen gebaseerde toegangscontroles](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=en) (RBAC).

De segmenten die van Experience Platform worden uitgevoerd worden toegewezen aan een specifieke gegevensbron in Audience Manager genoemd **[!UICONTROL Experience Platform Segments]**.

Om slechts bepaalde gebruikers toegang tot de segmenten toe te staan, kunt u toegangscontroles op de segmenten toepassen die tot de gegevensbron behoren. U moet nieuwe toegangsbeheertoestemmingen in Audience Manager voor deze segmenten en trekken plaatsen die van de segmenten van het Experience Platform worden gecreeerd.