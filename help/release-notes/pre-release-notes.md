---
title: Opmerkingen bij de release Experience Platform
description: Een voorvertoning van de meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: de95e9a51c979e9249ddf9ceb262fc521d2b38f4
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 30%

---

# Opmerkingen bij de release Adobe Experience Platform

>[!IMPORTANT]
>
>Dit document is voorgenomen als a **voorproef** van de versienota&#39;s voor de huidige maand. Release-items kunnen worden gewijzigd en worden toegevoegd of verwijderd in de definitieve versie.

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/pre-release-notes)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Datum van de Versie: Oktober 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [Bestemmingen](#destinations)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Waarschuwing foutpercentage bestemming | Een nieuw alarm is toegevoegd voor bestemmingen: **het mislukkingstarief van de Bestemming overschrijdt drempel**. Deze waarschuwing geeft een melding wanneer het aantal mislukte records tijdens de gegevensactivering de toegestane drempel heeft overschreden, zodat u snel kunt reageren op activeringsproblemen. |

{style="table-layout:auto"}

Raadpleeg het [[!DNL Observability Insights] overzicht](../observability/home.md) voor meer informatie over meldingen.

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [!DNL AdForm] | Gebruik deze bestemming om Adobe Real-Time CDP-gebruikers naar [!DNL AdForm] te sturen voor activering op basis van de Experience Cloud-id (ECID) en de ID-versie van [!DNL AdForm] . De ID Fusion van [!DNL AdForm] is een service voor het oplossen van id&#39;s waarmee u uw eerste publiek kunt activeren op basis van de Experience Cloud-id (ECID). |
| [!DNL Amazon Ads] | Er zijn aanvullende ondersteuning voor persoonlijke id&#39;s toegevoegd, zoals `firstName` , `lastName` , `street` , `city` , `state` , `zip` en `country` . Door deze velden toe te wijzen als doelidentiteiten, kunt u de overeenkomende populatiegraad verbeteren. |
| [!DNL Snowflake Batch] (beperkte beschikbaarheid) | Maak een live [!DNL Snowflake] gegevensuitwisseling om dagelijkse publieksupdates rechtstreeks als gedeelde tabellen in uw account te ontvangen. Deze integratie is momenteel beschikbaar voor klantenorganisaties die in de VA7-regio zijn gevestigd. |
| [!DNL Snowflake Streaming] (beperkte beschikbaarheid) | Maak een live [!DNL Snowflake] gegevensuitwisseling om streaming publiek-updates rechtstreeks als gedeelde tabellen in uw account te ontvangen. Deze integratie is momenteel beschikbaar voor klantenorganisaties die in de VA7-regio zijn gevestigd. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor [!DNL AES256] servercodering in [!DNL Amazon S3] -doelen | [!DNL Amazon S3] -doelen bieden nu ondersteuning voor [!DNL AES256] server-side codering, waardoor uw geëxporteerde gegevens beter worden beveiligd. U kunt deze coderingsmethode configureren wanneer u de [!DNL Amazon S3] -doelverbindingen instelt of bijwerkt, zodat uw gegevens in rust worden gecodeerd met de gangbare [!DNL AES256] -coderingsalgoritmen. Raadpleeg de [[!DNL Amazon] documentatie](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html) voor meer informatie. |
| [ Verscheidene nieuwe bestemmingen die publiek-vlakke controle ](../dataflows/ui/monitor-destinations.md#audience-level-view) steunen | De volgende bestemmingen steunen nu publiek-vlakke controle: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud] Betrokkenheid account</li><li>[!DNL The Trade Desk]</li></ul> |
| Oplossing voor instructies voor het exporteren van gegevens | Er is een correctie toegepast op de exportinstructies voor de gegevensset. Eerder, werden sommige datasets die een timestamp kolom omvatten maar __ gebaseerd op het schema van de Gebeurtenissen van de Ervaring XDM niet verkeerd behandeld als datasets van de Gebeurtenissen van de Ervaring, die de uitvoer beperken tot een terugkijkvenster van 365 dagen. De gedocumenteerde naslaggids voor 365 dagen is nu uitsluitend van toepassing op datasets van Experience Events. Datasets die een ander schema gebruiken dan het schema voor XDM Experience Events worden nu beheerst door de handleiding voor 10 miljard records. Sommige klanten kunnen verhoogde uitvoeraantallen voor datasets zien die verkeerd onder het terugkijkvenster van 365 dagen vielen. Dit laat u toe om datasets voor vooruitlopende werkschema&#39;s uit te voeren die een lang raadplegingsvenster hebben. Voor meer informatie, lees de [ de uitvoergidsen van de dataset ](../destinations/guardrails.md#dataset-exports). |
| Verbeterde publieksrapportage voor zakelijke doelen | Verbeterde publiek-vlakke rapporteringslogica voor ondernemingsbestemmingen. Na deze release zullen klanten nauwkeurigere publieksrapportagenummers zien met alleen publiek dat relevant is voor de geselecteerde bestemming. Deze aanpassing van de bewaking zorgt ervoor dat de rapportage alleen betrekking heeft op publiek dat is toegewezen aan de dataflow, zodat duidelijker inzicht wordt verkregen in de feitelijke activering van gegevens. Dit heeft geen invloed op de hoeveelheid gegevens die wordt geactiveerd, maar is louter een verbetering van de controle om de nauwkeurigheid van de rapportage te verbeteren. |

Voor meer informatie leest u het [overzicht van bestemmingen](../destinations/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Bewaking van streaming segmentering | Controle in real time voor het stromen segmentatie verstrekt transparantie in evaluatiesnelheid, latentie, en de metriek van de gegevenskwaliteit op de zandbak, dataset, en publieksniveaus. Dit ondersteunt proactieve waarschuwingen en bruikbare inzichten om data-engineers te helpen bij het identificeren van capaciteitsschendingen en problemen met de opname. De metriek van de controle omvatten evaluatiesnelheid, P95 ingesliplatentie, evenals ontvangen, geëvalueerde, ontbroken verslagen, en overgeslagen verslagen. De mening-door-dataset en mening-door-publiek mogelijkheden verstrekken uitvoerige zicht in netto nieuwe profielen die worden gekwalificeerd en worden gedeskwalificeerd. |

Voor meer informatie raadpleegt u het [[!DNL Segmentation Service] overzicht](../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| [!BADGE  Beta ]{type=Informative} [!DNL Talon.one] bronnen voor loyaliteitsgegevens | Met de [!DNL Talon.One] -bronnen kunt u batchgegevens en streaming loyaliteitsgegevens invoeren in Experience Platform. De schakelaar steunt het stromen van profielgegevens, transactiegegevens, en loyaliteitsgegevens met inbegrip van verdiende punten, afgeloste punten, verlopen punten, en rijgegevens. |

**Bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van [!DNL Google Ads] source (alleen API) | De API-versie van de [!DNL Google Ads] -bron bevindt zich nu in Algemene beschikbaarheid. De API-documentatie is bijgewerkt om aan te geven dat de nieuwste versie nu `v21` is en Experience Platform ondersteunt alle versies v19 en hoger. De versie van de UI blijft in bèta en steunt slechts éénmalige opname. Gebruik de API-route om incrementele gegevensinvoer te gebruiken. |
| [!DNL Azure Event Hubs] virtuele netwerkondersteuning | Adobe ondersteunt nu expliciet virtuele netwerkverbindingen met Azure Event Hubs, waardoor gegevensoverdracht via particuliere netwerken mogelijk wordt in plaats van via openbare netwerken. De klanten kunnen Experience Platform VNet lijsten van gewenste personen om het verkeer van de Hubs van de Gebeurtenis door de Azure privé backbone privé te leiden, die verbeterde veiligheid en naleving voor de werkschema&#39;s van de gegevensopname verstrekt. |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../sources/home.md).
