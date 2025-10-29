---
title: Adobe Advertising Cloud DSP-verbinding
description: Adobe Advertising Cloud DSP is een geïntegreerde bestemming voor Adobe Real-Time Customer Data Platform, waarmee u geverifieerde soorten publiek van de eerste partij kunt delen met goedgekeurde adverteerders en gebruikers voor activering van de campagne.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Adobe Advertising Cloud DSP-verbinding

## Overzicht {#overview}

Met de Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP)-bestemming kunt u geverifieerde soorten publiek van de eerste partij delen met goedgekeurde adverteerders en gebruikers voor activering van de campagne met DSP. Meer over de integratie van Real-Time CDP met DSP leren, zie [&#x200B; Ongeveer het Activeren van Voor authentiek verklaard publiek van de Bronnen van het Publiek &#x200B;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Deze pagina is gemaakt door het DSP-team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de ondersteuning van Advertising Cloud op `adcloud_support@adobe.com` .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van DSP van de Advertising Cloud zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Gebruiksscenario voor reclame

Een online retailer wil zijn klanten met een hoge prijs opnieuw als doel instellen via een weergavecampagne zonder cookies te gebruiken voor het opgeven van doelen. De retailer deelt een publiek dat bestaat uit de gehashte e-mail-id&#39;s van haar klanten met een hoge waarde van haar Adobe Real-Time Customer Data Platform (Real-Time CDP)-account naar haar DSP-account. DSP converteert de gehashte e-mailadressen vervolgens naar geverifieerde [!DNL RampIDs] via een partnerschap tussen DSP en LiveRamp. De resulterende [!DNL RampIDs] kan in een weergavecampagne worden gebruikt om het publiek te bereiken.

### Gebruiksscenario van het Agentschap

Een mediabedrijf met een DSP-account voert een herrichtingscampagne namens zijn klant, een topmerk in de gastensector. Het merk wil al zijn gasten in het afgelopen jaar opnieuw aanspreken met een nieuw promotieaanbod. Het merk bewaart alle gastinformatie in [!DNL Real-Time CDP]. Het merk kan een publiek delen dat bestaat uit de gehashte e-mailadressen van de gasten van zijn [!DNL Real-Time CDP] -account naar het DSP-account van het mediabureau om de gasten via een mediacampagne te laten omleiden.

## Vereisten {#prerequisites}

* DSP-instellingen op accountniveau en op campagnereniveau om gebruikers in staat te stellen te delen met [!DNL LiveRamp RampID] , waarmee klantgegevens worden omgezet in [!DNL RampIDs] om doelgerichte segmenten te maken. Uw DSP-accountteam zal deze configuratie uitvoeren. [!DNL RampID] is beschikbaar via een partnerschap tussen DSP en [!DNL LiveRamp] en u hebt geen eigen [!DNL LiveRamp] -lidmaatschap nodig om dit te gebruiken.
* De Experience Cloud-organisatie-id voor de Experience Platform-account. U vindt uw id op de pagina met gebruikersprofielen van [!DNL Real-Time CDP] .
* A [[!DNL Real-Time CDP]  bron in DSP &#x200B;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) om publiek voor campagneactivering te ontvangen. Uw DSP-accountteam maakt de bron met uw Experience Cloud-organisatie-id.
* De bronsleutel voor de rekening of de adverteerder van DSP, die wordt geproduceerd wanneer a [[!DNL Real-Time CDP]  bron in DSP &#x200B;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) wordt gecreeerd. Uw DSP-accountteam zal deze sleutel met u delen. U zult het binnen Experience Platform gebruiken om een bestemmingsverbinding aan de Advertising Cloud DSP bestemming tot stand te brengen, zoals [&#x200B; hieronder verklaard &#x200B;](#authenticate).
* Klantgegevens die bestaan uit e-mails of gehashte e-mails.

## Ondersteunde identiteiten {#supported-identities}

De Adobe Advertising Cloud DSP-bestemming ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Experience Platform ondersteunt zowel normale tekst- als SHA256-hashed-e-mailadressen. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in zodat Experience Platform de gegevens automatisch hasht bij activering. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de volgende tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail of gehashte e-mail) die worden gebruikt in de DSP-bestemming van de Advertising Cloud. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) voor Experience Platform nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met de bestemming te verbinden, volg de instructies om [&#x200B; een bestemmingsverbinding &#x200B;](/help/destinations/ui/connect-destination.md) tot stand te brengen gebruikend het gebruikersinterface van Experience Platform. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u verbinding wilt maken met het doel, geeft u de volgende parameter op in de sectie [!UICONTROL Connection type] en selecteert u vervolgens **[!UICONTROL Connect to destination]** :

* **[!UICONTROL Account or Advertiser Key]**: Dit [!UICONTROL Source Key] wordt geproduceerd wanneer a [[!DNL Real-Time CDP]  bron in het gebruikersinterface van DSP &#x200B;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) wordt gecreeerd. Uw DSP-accountteam zal deze sleutel met u delen nadat ze de bron hebben gemaakt.

![&#x200B; het typegebied van de Verbinding &#x200B;](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

![&#x200B; de detailgebieden van de Bestemming &#x200B;](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

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

Ga als volgt te werk om te controleren of het gegevenspubliek werd gedeeld met Advertising Cloud:

* De gegevensstroom in uw [!DNL Real-Time CDP] -doel is voltooid.

* In DSP is het publiek beschikbaar wanneer u een publiek maakt of bewerkt vanuit [!UICONTROL Audiences] > [!UICONTROL All Audiences] of vanuit de sectie [!UICONTROL Audience Targeting] met plaatsingsinstellingen. Het publiek moet zichtbaar zijn op het tabblad [!UICONTROL Adobe Segments] onder de map [!UICONTROL Real-Time CDP] .

![&#x200B; het publiek van Real-Time CDP in het publieksmontages van DSP &#x200B;](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
