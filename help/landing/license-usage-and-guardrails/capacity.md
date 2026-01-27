---
title: Gebruik en capaciteit van licenties
description: Meer informatie over het gebruik van licenties en capaciteitsbeperkingen in Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 8cef502f60a42de9c89c29923811215b3a8086c6
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 0%

---


# Gebruik van licenties en capaciteiten

>[!AVAILABILITY]
>
>U moet over de volgende machtigingen beschikken om deze functie te kunnen gebruiken:
>
>- **Dashboard van het Gebruik van de Vergunning van de Mening**
>   - Deze toestemming laat u **mening** het capaciteitshuis.
>- **beheert Sandboxes**
>   - Deze toestemming laat u **&#x200B;**&#x200B;uw capaciteitstoewijzingen uitgeven.
>   - Bovendien, moet u **&#x200B;**&#x200B;toegang tot alle zandbakken worden toegewezen **om het even welke** zandbakcapaciteit uit te geven.
>
>Meer informatie over toestemmingen binnen Experience Platform kan in het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/home.md#permissions) worden gevonden
>
>Bovendien, als u Hoog de Streaming Segmentatie van de Bedrading van de Bedrading hebt gekocht, zult u **niet** uw capaciteit kunnen toewijzen gebruikend Capaciteit. Neem contact op met de klantenservice van Adobe om uw capaciteiten bij te werken.

In Adobe Experience Platform, laat de capaciteit u weten of uw organisatie om het even welk van uw gidsen heeft overschreden en geeft u informatie over hoe te om deze kwesties op te lossen.

Voor meer informatie over geleiders in Experience Platform, te lezen gelieve het [&#x200B; overzicht van de Bewindingen van Real-Time CDP &#x200B;](../../rtcdp/guardrails/overview.md).

## Capaciteit, gedrag {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Streaming doorvoer"
>abstract="De het stromen productiewaarde meet de gecombineerde piekbinnenkomende gebeurtenissen per seconde voor het stromen van opname in de dienst van het Profiel, over uw productie en ontwikkelingszandbakken."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Aantal gestreamde doelgroepen"
>abstract="Het maximum aantal streaming publiek per sandbox. Dit getal is inclusief het aantal randsoorten dat u in de sandbox hebt."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Edge-publiek"
>abstract="Het maximumaantal randpubliek per sandbox."

Capaciteit ondersteunt momenteel de volgende services:

- Streaming segmentering
- Streaming opname

Binnen deze diensten, worden de volgende gidsen gevolgd:

- Het maximumaantal streamingdeelnemers is 500
   - Van deze 500 streamingdeelnemers is het maximumaantal randsoorten 150
- De aanvankelijke gecombineerde productie voor het stromen opname is 1500 verslagen per seconde (rps)
   - Deze gecombineerde stroomproductie meet de gecombineerde piekbinnenkomende gebeurtenissen per seconde voor het stromen van opname in het Profiel van de Klant in real time over uw productie en ontwikkelingszandbakken.
   - U kunt extra ondersteuning voor streamingsegmentatie aanschaffen voor maximaal 13.500 records per seconde. Meer informatie over het kopen van extra rechten kan in de [&#x200B; het productbeschrijving van Real-Time CDP &#x200B;](https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) worden gevonden.

De publiekscapaciteit is op a **zandbak** niveau. Dit betekent dat u voor elke sandbox die u in uw organisatie hebt, 500 streaming publiek kunt hebben, waarvan 150 Edge-publiek.

De het stromen productiecapaciteit van de productie is op een **organisatie** niveau en kan aan uw individuele zandbakken worden verdeeld. Met de 1500 rps voor het streamen van opname-doorvoer kunt u bijvoorbeeld de productie-sandbox instellen op 1300 rps en de ontwikkelingssandbox op 200 rps.

Experience Platform berekent de doorvoer van de sandbox in telkens 15 minuten. Deze productie wordt gemeten in real time, met de gegevens die elke 60 seconden verfrissen.

Als uw gebruik 80% en 90% van uw gelicentieerde capaciteit bereikt, zal Experience Platform een alarm afgeven, op het bericht dat u het maximum van uw gespecificeerde capaciteit bereikt. U kunt de instellingen wijzigen om het capaciteitspercentage aan te passen aan de waarschuwing of de waarschuwing volledig verwijderen.

Als uw gebruik meer dan 100% van uw vergunning capaciteit gaat, zult u beschouwd in strijd met uw capaciteit worden. Als u uw capaciteit schendt, zullen de volgende beperkingen worden toegepast:

>[!NOTE]
>
>Als u toegang tot Adobe Journey Optimizer hebt, zullen de volgende beperkingen **&#x200B;**&#x200B;niet van toepassing zijn.

- De gegevens van de gebeurtenis **kunnen** van het stromen verpersoonlijking worden verwijderd als de rij van de gebeurtenisverwerking 12 uren overschrijdt
- Verwijderd gebeurtenisgegevens zullen **niet** in Profiel worden opgenomen
   - U kunt zien wanneer gebeurtenissen zijn verwijderd
   - Gebeurtenissen zijn beschikbaar in het datumpeer, afhankelijk van uw rechten
   - U *kan* de Dienst van de Vraag gebruiken om de gegevens direct opnieuw in te voeren, indien vereist

## Toegang {#access}

Als u het overzicht Capaciteit wilt openen, selecteert u **[!UICONTROL License usage]** gevolgd door **[!UICONTROL Capacity]** .

![&#x200B; de methode om tot de sectie van de Capaciteit toegang te hebben wordt benadrukt.](/help/landing/images/capacity/access-capacity.png)

De pagina met het overzicht van de capaciteit wordt weergegeven, met informatie zoals een geschiedenis van waarschuwingen en details over de capaciteiten van uw organisatie.

![&#x200B; de het overzichtspagina van de Capaciteit wordt getoond volledig, tonend de waakzame geschiedenis en de secties van de capaciteitsdetails.](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

### Waarschuwingsgeschiedenis {#alert-history}

In de sectie **[!UICONTROL Alert history]** wordt een lijst weergegeven met de meest recente capaciteitsovertredingen binnen uw organisatie.

![&#x200B; de Alert geschiedenissectie wordt getoond.](/help/landing/images/capacity/alert-history.png)

| Kolomnaam | Beschrijving |
| ----------- | ----------- |
| Sandbox | De naam van de sandbox waar de capaciteitsfout zich heeft voorgedaan. |
| Melding | De capaciteit die in de zandbak is geschonden. |
| Tijdstempel | De gegevens en het tijdstip waarop de schending heeft plaatsgevonden. |

Om een volledige geschiedenis van het alarm voor uw organisatie te bekijken, selecteer het ![&#x200B; drie puntenpictogram &#x200B;](/help/images/icons/more.png), dat door **[!UICONTROL View all]** wordt gevolgd.

![&#x200B; de volledige waakzame geschiedenis wordt getoond voor een organisatie.](/help/landing/images/capacity/full-alert-history.png)

### Capaciteitsdetails {#capacity-details}

In de sectie Capaciteitsdetails wordt informatie over de capaciteiten van uw organisatie beschreven. In deze sectie kunt u filteren per sandbox en de terugzoekperiode wijzigen.

![&#x200B; de zandbakselecteur en de datumplukker voor de raadplegingsperiode worden benadrukt.](/help/landing/images/capacity/filter-sandbox-and-date.png)

Op dit moment wordt er capaciteitsinformatie weergegeven over streamingdoorvoer, streaming publiek en randpubliek.

#### Streaming doorvoer {#streaming-throughput}

In de sectie voor streamingdoorvoer wordt informatie weergegeven over de streamingdoorvoer in de sandboxen van uw organisatie. De het stromen productiewaarde meet de gecombineerde piekbinnenkomende gebeurtenissen per seconde voor het stromen opname in de dienst van het Profiel.

![&#x200B; de het stromen productiesectie binnen de pagina van capaciteitsdetails wordt getoond.](/help/landing/images/capacity/streaming-throughput-section.png)

| Kolomnaam | Beschrijving |
| ----------- | ----------- |
| Sandbox | De naam van de sandbox. |
| Services | De service die door de sandbox wordt gebruikt. Momenteel is de enige ondersteunde waarde Profile. |
| Gebruik (pieken) | De piekstreamingdoorvoer van gegevens in de sandbox binnen de geselecteerde terugzoekperiode. |
| Capaciteit | De maximale streamingdoorvoer voor pieken voor de sandbox. |
| Schending | Als er een schending is opgetreden, het type van schending voor het stromen van productie. |
| Aanbevolen acties | Een kolom die de aanbevolen actie beschrijft om de schending te verlichten. |

U kunt de afzonderlijke sandbox selecteren om een gedetailleerdere weergave van de streamingdoorvoer van de sandbox weer te geven.

![&#x200B; de zandbak van A wordt benadrukt binnen de het stromen productiesectie.](/help/landing/images/capacity/select-sandbox.png)

De pagina met de details van de streamingdoorvoer wordt weergegeven. U kunt een grafiek zien die de verzoekproductie in vergelijking met de capaciteitsgrens, een lijst van zandbakken en hun productie, evenals een knoop toont om de capaciteiten van uw organisatie toe te wijzen.

![&#x200B; de het stromen productiepagina wordt getoond, tonend gedetailleerde informatie over de het stromen productie voor de geselecteerde zandbak.](/help/landing/images/capacity/streaming-capacity-allocation.png)

Selecteer **[!UICONTROL Allocate capacities]** als u de streamingdoorvoer van de organisatie wilt bijwerken.

![&#x200B; de knoop van de Capaciteiten van de Toewijzing wordt benadrukt binnen de het stromen pagina van de productiedetails.](/help/landing/images/capacity/select-allocate.png)

De toewijzingspagina wordt weergegeven. Op deze pagina kunt u de capaciteiten instellen voor de verschillende sandboxen. De som van alle capaciteiten **moet** aan het de capaciteitstotaal van de organisatie gelijk zijn.

![&#x200B; de pagina van de capaciteitstoewijzing wordt getoond.](/help/landing/images/capacity/allocate-capacity.png)

>[!NOTE]
>
>U kunt de nieuwe capaciteit in orden van **slechts plaatsen 100**. Bijvoorbeeld, kunt u de waarde van de nieuwe capaciteit van de zandbak aan 300 of 500 plaatsen, maar u **kunt niet** deze waarde aan 450 plaatsen.
>
>Als de waarde niet in de orde van 100 is, zal het naar boven of naar onder dienovereenkomstig worden afgerond.

Nadat u de capaciteitstoewijzingen hebt bijgewerkt, selecteert u **[!UICONTROL Save]** om de updates te voltooien. Houd er rekening mee dat het maximaal 10 minuten kan duren voordat de wijzigingen in uw organisatie worden doorgevoerd.

#### Aantal deelnemers {#audience-count}

In de secties **[!UICONTROL Streaming audience count]** en **[!UICONTROL Edge audience count]** worden het aantal streaming- en Edge-doelgroepen in de sandbox weergegeven, evenals het maximumaantal streaming- en randdoelgroepen dat is toegestaan in de sandbox.

![&#x200B; de de tellingen van de Publiek secties worden getoond.](/help/landing/images/capacity/audience-count.png)

| Kolomnaam | Beschrijving |
| ----------- | ----------- |
| Sandbox | De naam van de sandbox. |
| Services | De service die wordt gebruikt voor de sandbox. |
| Gebruik | Het aantal soorten publiek van het vermelde type dat zich in de sandbox bevindt. |
| Capaciteit | Het maximum aantal soorten publiek van het vermelde type dat is toegestaan in de sandbox. |

## Best practices voor streaming doorvoer {#suggestions}

U kunt uw het stromen productieschendingen door één van de volgende aanbevelingen op te volgen oplossen:

1. Verhoog de toegewezen capaciteit voor de sandbox.
2. Identificeer hoge productiedataflows in het [&#x200B; controledashboard &#x200B;](/help/dataflows/ui/monitor-streaming-profile.md) en pas throttling of het filtreren tegen deze dataflows toe indien nodig.
3. Optimaliseer uw inname door batch-inname te gebruiken voor een lagere latentie.

Bovendien kunt u naar uw gegevensstromen kijken en zien of kunt u uw gegevensstrategie optimaliseren.

| bijdragende factor | Wat het is | Gevolgen van het gebruik | Best practices |
| --- | --- | --- | --- |
| Batch naar streaming conversie | Batchwerklasten die in streaming worden omgezet, kunnen de doorvoer aanzienlijk verhogen, wat van invloed is op de prestaties en de toewijzing van bronnen. Bijvoorbeeld het uitvoeren van een bulkprofielupdate na een gebeurtenis zonder tariefgrenzen. | Streaming strategieën zijn niet nodig voor batchgebruik wanneer verwerking met lage latentie niet vereist is. | Evalueer de eisen van het gebruikscase. Voor partij uitgaande marketing, denk na gebruikend [&#x200B; partij ingestie &#x200B;](/help/ingestion/batch-ingestion/overview.md) in plaats van het stromen om gegevensopname efficiënter te beheren. |
| Onnodige gegevensinvoer | Het invoeren van gegevens die niet voor verpersoonlijking worden vereist verhoogt productie zonder waarde toe te voegen, die middelen verspillen. Bijvoorbeeld, het opnemen van al analyseverkeer in profielen ongeacht relevantie. | Overbodige, niet-relevante gegevens zorgen voor ruis, waardoor het moeilijker wordt om onechte gegevenspunten te identificeren. Het kan ook wrijving veroorzaken wanneer het bepalen van en het leiden van publiek en profielen. | Vermeld alleen de gegevens die nodig zijn voor uw gebruiksgevallen. Zorg ervoor dat u overbodige gegevens verwijdert.<ul><li>**Adobe Analytics**: Het 2&rbrace; rij-vlakke filtreren van het gebruik [&#x200B; om uw gegevensopname te optimaliseren.](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile)</li><li>**Bronnen**: Gebruik [[!DNL Flow Service]  API aan filter rij-vlakke gegevens &#x200B;](/help/sources/tutorials/api/filter.md) voor gesteunde bronnen zoals [!DNL Snowflake] en [!DNL Google BigQuery].</li></li>**Edge datastream**: Vorm [&#x200B; dynamische gegevensstromen &#x200B;](/help/datastreams/configure-dynamic-datastream.md) om rij-vlakke het filtreren van verkeer uit te voeren dat binnen van WebSDK komt.</li></ul> |

## Video-overzicht {#video}

De volgende video biedt een overzicht van Capaciteit.

>[!VIDEO](https://video.tv.adobe.com/v/3475272/?learn=on&enablevpops)

## Veelgestelde vragen {#faq}

In de volgende sectie worden veelgestelde vragen over de mogelijkheden van Capaciteit beschreven.

### Kan ik een maximum gecombineerde productielimiet hebben die tot minder dan mijn doelmaximum samenvat?

+++ Antwoord

Nee. De maximum gecombineerde productielimiet **moet** som tot de guardrail van uw organisatie.

+++

### Wat gebeurt er als ik mijn maximale capaciteit overschrijd?

+++ Antwoord

Dit hangt af van de vraag welke capaciteit wordt overschreden.

Als u het maximale aantal toegestane doelgroepen overschrijdt, heeft dit momenteel geen invloed op uw buitensporige doelgroepen. Het vermogen om een nieuw publiek te creëren kan in de toekomst echter beperkt zijn.

Als u uw het stromen productie overschrijdt, zult u prestatieslatentie in uw opname en segmentatie ervaren.

+++

### Waarom zou ik mijn maximale capaciteit moeten respecteren?

+++ Antwoord

Uw gegevens blijven consistent en de integriteit van uw gegevens blijft intact als u binnen uw maximale capaciteit werkt.

U verzekert verenigbare prestaties tijdens piekgebeurtenissen, vermijdend technische kwesties die systeemprestaties negatief zouden kunnen beïnvloeden en uw stroomafwaartse klantenervaring beïnvloeden, uiteindelijk verbeterend uw gegevenshygiëne en algemene systeemprestaties.

+++

### Wat zijn beste praktijken om het stromen inslikken productie te beheren?

+++ Antwoord

Om uw het stromen inslikken productie het best te beheren, zou u uw datasets moeten evalueren om ervoor te zorgen zij aan gegevens noodzakelijk voor verpersoonlijking voorrang geven.


Als verwerking in real time niet vereist is, moet u batch-opname gebruiken in plaats van streaming opname.

+++
