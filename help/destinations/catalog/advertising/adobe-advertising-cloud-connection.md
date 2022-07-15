---
title: Adobe Advertising Cloud DSP-verbinding
description: Adobe Advertising Cloud DSP is een geïntegreerde bestemming voor de [!DNL Adobe Real-time Customer Data Profile], zodat u geverifieerde first-party-segmenten kunt delen met goedgekeurde adverteerders en gebruikers voor activering van de campagne.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 27869b91deeb4a5cca580970507845d992d21aaf
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# Adobe Advertising Cloud DSP-verbinding

## Overzicht {#overview}

De Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) de bestemming staat u toe om voor authentiek verklaarde eerste-partijsegmenten met goedgekeurde adverteerders en gebruikers voor campagneactivering met DSP te delen. Ga voor meer informatie over de integratie van Real-Time CDP met DSP naar [Ongeveer het Activeren van Authenticated Segmenten van de Bronnen van het Publiek](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Deze pagina is gemaakt door het DSP team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de ondersteuning van Advertising Cloud op `adcloud_support@adobe.com`.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van Advertising Cloud DSP zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Gebruiksscenario voor reclame

Een online detailhandelaar wil zijn klanten met hoge waarde door een vertoningscampagne opnieuw richten zonder koekjes voor het richten te gebruiken. De detailhandelaar deelt een segment dat bestaat uit de gehashte e-mail-id&#39;s van zijn klanten met een hoge waarde uit zijn [!DNL Real-Time CDP] aan zijn DSP account. DSP zet vervolgens de gehashte e-mailadressen om in geverifieerde [!DNL RampIDs] via een partnerschap tussen DSP en LiveRamp. Het resultaat [!DNL RampIDs] kan in een vertoningscampagne worden gebruikt om het publiek te richten.

### Gebruiksscenario van het Agentschap

Een mediabedrijf met een DSP account voert een herrichtingscampagne namens zijn klant, een topmerk in de gastindustrie. Het merk wil al zijn gasten in het afgelopen jaar opnieuw aanspreken met een nieuw promotieaanbod. Het merk bewaart alle gastinformatie in [!DNL Real-Time CDP]. Het merk kan een segment delen dat bestaat uit de gehashte e-mailadressen van de gasten van het merk [!DNL Real-Time CDP] account aan de DSP van het mediaagentschap om de gasten via een mediacampagne te richten.

## Vereisten {#prerequisites}

* DSP instellingen op accountniveau en op campagnereniveau om delen met segmenten mogelijk te maken [!DNL LiveRamp RampID], waarin klantgegevens worden omgezet in [!DNL RampIDs] om doelsegmenten te maken. Uw DSP accountteam zal deze configuratie uitvoeren. [!DNL RampID] via een partnerschap tussen DSP en [!DNL LiveRamp]en u hebt uw eigen [!DNL LiveRamp] lidmaatschap om het te gebruiken.
* De Experience Cloud organisatie-id voor de account van het Experience Platform. Je kunt je id vinden op je [!DNL Real-Time CDP] pagina met gebruikersprofielen.
* A [[!DNL Real-Time CDP] bron in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) om segmenten te ontvangen voor activering van de campagne. Uw DSP accountteam zal de bron maken met uw Experience Cloud-organisatie-id.
* De bronsleutel voor de DSP account of adverteerder, die wordt gegenereerd wanneer een [[!DNL Real-Time CDP] bron wordt gemaakt in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Uw DSP accountteam zal deze sleutel met u delen. U gaat het binnen het Experience Platform gebruiken om een doelverbinding met de Advertising Cloud DSP-bestemming te maken, zoals [hieronder beschreven](#authenticate).
* Klantgegevens die bestaan uit e-mails of gehashte e-mails.

## Ondersteunde identiteiten {#supported-identities}

De Adobe Advertising Cloud DSP-bestemming ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Experience Platform ondersteunt zowel normale tekst- als SHA256-gehashed e-mailadressen. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** als u wilt dat Experience Platform de gegevens automatisch verbergt bij activering. |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de volgende tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (e-mail of gehashte e-mail) die in de Advertising Cloud DSP-bestemming worden gebruikt. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions) voor Experience Platform. Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Om met de bestemming te verbinden, volg de instructies aan [een doelverbinding maken](/help/destinations/ui/connect-destination.md) het gebruiken van de gebruikersinterface van het Experience Platform. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Om met de bestemming te verbinden, verstrek de volgende parameter in [!UICONTROL Connection type] en selecteert u vervolgens **[!UICONTROL Connect to destination]**.:

* **[!UICONTROL Account or Advertiser Key]**: Dit [!UICONTROL Source Key] wordt gegenereerd wanneer een [[!DNL Real-Time CDP] bron wordt gemaakt in de DSP gebruikersinterface](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Uw DSP accountteam zal deze sleutel met u delen nadat zij de bron hebben gemaakt.

![Veld voor verbindingstype](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

![Detailvelden bestemming](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Controleer het volgende om te controleren of het gegevenssegment met Advertising Cloud is gedeeld:

* De gegevensstroom in uw [!DNL Real-Time CDP] doel is gelukt.

* In DSP is het segment beschikbaar wanneer u een publiek maakt of bewerkt vanuit [!UICONTROL Audiences] > [!UICONTROL All Audiences] of vanuit de [!UICONTROL Audience Targeting] sectie met plaatsingsinstellingen. Het segment moet zichtbaar zijn in het dialoogvenster [!UICONTROL Adobe Segments] onder de [!UICONTROL Real-Time CDP] map.

![Real-Time CDP-segmenten in DSP publieksinstellingen](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).
