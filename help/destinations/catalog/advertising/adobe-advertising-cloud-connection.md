---
title: Adobe Advertising Cloud DSP-verbinding
description: Adobe Advertising Cloud DSP is een geïntegreerde bestemming voor Adobe Real-time Customer Data Platform, zodat u geautoriseerde voorstanders kunt delen met goedgekeurde adverteerders en gebruikers voor activering van de campagne.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Adobe Advertising Cloud DSP-verbinding

## Overzicht {#overview}

Met de Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP)-bestemming kunt u geverifieerde soorten publiek van de eerste partij delen met goedgekeurde adverteerders en gebruikers voor activering van de campagne met DSP. Meer over de integratie van Real-Time CDP met DSP leren, zie [&#x200B; Ongeveer het Activeren van Voor authentiek verklaard publiek van de Bronnen van het Publiek &#x200B;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html?lang=nl-NL).

>[!IMPORTANT]
>
>Deze pagina is gemaakt door het DSP team. Voor vragen of updateverzoeken kunt u rechtstreeks via `adcloud_support@adobe.com` contact opnemen met de ondersteuning van Advertising Cloud.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van Advertising Cloud DSP zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Gebruiksscenario voor reclame

Een online detailhandelaar wil zijn klanten met hoge waarde door een vertoningscampagne opnieuw richten zonder koekjes voor het richten te gebruiken. De detailhandelaar deelt een publiek dat bestaat uit de gehashte e-mailadressen van zijn klanten met een hoge waarde van zijn Adobe Real-time Customer Data Platform (Real-Time CDP)-account tot zijn DSP. DSP converteert de gehashte e-mailid&#39;s vervolgens naar geverifieerde [!DNL RampIDs] via een partnerschap tussen DSP en LiveRamp. De resulterende [!DNL RampIDs] kan in een weergavecampagne worden gebruikt om het publiek te bereiken.

### Gebruiksscenario van het Agentschap

Een mediabedrijf met een DSP account voert een herrichtingscampagne namens zijn klant, een topmerk in de gastindustrie. Het merk wil al zijn gasten in het afgelopen jaar opnieuw aanspreken met een nieuw promotieaanbod. Het merk bewaart alle gastinformatie in [!DNL Real-Time CDP]. Het merk kan een publiek delen dat bestaat uit de gehashte e-mailadressen van de gasten van zijn [!DNL Real-Time CDP] -account naar het DSP account van het mediabureau om de gasten via een mediacampagne te laten omleiden.

## Vereisten {#prerequisites}

* DSP instellingen op accountniveau en op campagnereniveau om het delen van publiek met [!DNL LiveRamp RampID] mogelijk te maken. Hiermee worden klantgegevens naar [!DNL RampIDs] vertaald om doelgerichte segmenten te maken. Uw DSP accountteam zal deze configuratie uitvoeren. [!DNL RampID] is beschikbaar via een partnerschap tussen DSP en [!DNL LiveRamp] en u hebt geen eigen [!DNL LiveRamp] -lidmaatschap nodig om dit te gebruiken.
* De organisatie-id van het Experience Cloud voor de account Experience Platform. U vindt uw id op de pagina met gebruikersprofielen van [!DNL Real-Time CDP] .
* A [[!DNL Real-Time CDP]  bron in DSP &#x200B;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=nl-NL) om publiek voor campagneactivering te ontvangen. Uw DSP accountteam zal de bron maken met uw organisatie-id van het Experience Cloud.
* De bronsleutel voor de DSP rekening of adverteerder, die wordt geproduceerd wanneer de bron van a [[!DNL Real-Time CDP]  in DSP &#x200B;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=nl-NL) wordt gecreeerd. Uw DSP accountteam zal deze sleutel met u delen. U zult het binnen Experience Platform gebruiken om een bestemmingsverbinding aan de bestemming van Advertising Cloud DSP tot stand te brengen, zoals [&#x200B; hieronder verklaard &#x200B;](#authenticate).
* Klantgegevens die bestaan uit e-mails of gehashte e-mails.

## Ondersteunde identiteiten {#supported-identities}

De Adobe Advertising Cloud DSP-bestemming ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Experience Platform ondersteunt zowel normale tekst- als SHA256-gehashed e-mailadressen. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door het Experience Platform. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de volgende tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail of gehashte e-mail) die in de Advertising Cloud DSP-bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) voor Experience Platform nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met de bestemming te verbinden, volg de instructies om [&#x200B; een bestemmingsverbinding &#x200B;](/help/destinations/ui/connect-destination.md) tot stand te brengen gebruikend het gebruikersinterface van het Experience Platform. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u verbinding wilt maken met het doel, geeft u de volgende parameter op in de sectie [!UICONTROL Connection type] en selecteert u vervolgens **[!UICONTROL Connect to destination]** :

* **[!UICONTROL Account or Advertiser Key]**: Dit [!UICONTROL Source Key] wordt geproduceerd wanneer a [[!DNL Real-Time CDP]  bron in het DSP gebruikersinterface &#x200B;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=nl-NL) wordt gecreeerd. Uw DSP accountteam zal deze sleutel met u delen nadat zij de bron hebben gemaakt.

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

Controleer het volgende om te controleren of het gegevenspubliek met Advertising Cloud is gedeeld:

* De gegevensstroom in uw [!DNL Real-Time CDP] -doel is voltooid.

* In DSP is het publiek beschikbaar wanneer u een publiek maakt of bewerkt vanuit [!UICONTROL Audiences] > [!UICONTROL All Audiences] of vanuit de sectie [!UICONTROL Audience Targeting] met plaatsingsinstellingen. Het publiek moet zichtbaar zijn op het tabblad [!UICONTROL Adobe Segments] onder de map [!UICONTROL Real-Time CDP] .

![&#x200B; het publiek van Real-Time CDP in DSP publieksmontages &#x200B;](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
