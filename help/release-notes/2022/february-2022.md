---
title: Opmerkingen bij de release van Adobe Experience Platform, februari 2022
description: In de release van februari 2022 staat een opmerking voor Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: dinsdag 7 maart 2022**

>[!NOTE]
>
>Deze release werd verschoven van de oorspronkelijke datum van 23 februari naar 7 maart.

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform biedt meerdere [!DNL dashboards] waarmee u belangrijke inzichten in de gegevens van uw organisatie kunt bekijken, zoals die tijdens dagelijkse momentopnamen zijn vastgelegd.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe standaarddoelen voor widgets | Met de volgende standaardwidgets kunt u verschillende meetgegevens visualiseren die betrekking hebben op uw doelen.<ul><li>Onlangs geactiveerde segmenten op doel. Deze widget geeft de bovenste vijf laatst geactiveerde segmenten in aflopende volgorde weer, afhankelijk van de gekozen bestemming.</li><li>Ontwikkeling van de omvang van het publiek. Deze widget geeft de relatie weer van de profieltelling over een tijdsperiode voor een segment dat aan die bestemmingsrekening in kaart is gebracht.</li><li>Niet-toegewezen segmenten op identiteit. Deze widget geeft een overzicht van de bovenste vijf niet-toegewezen segmenten die worden gerangschikt op basis van het aantal identiteiten voor een bepaald doel en een bepaalde identiteit.</li><li>Toegewezen segmenten op identiteit. Deze widget geeft een overzicht van de bovenste vijf toegewezen segmenten. De segmenten worden bevolen van hoog tot laag afhankelijk van hun respectieve tellingen van bron IDs die bestemmingsidentiteitskaart aanpassen die van het drop-down menu van widget wordt geselecteerd.</li><li>Veelvoorkomende doelgroepen. Deze widget bevat een lijst met de bovenste vijf segmenten die zijn geactiveerd voor de doelaccount die boven aan de pagina is gekozen, en het doel dat is geselecteerd in het vervolgkeuzemenu van de widget.</li></ul> Voor meer informatie over de beschikbare standaard widgets, zie de [ documentatie van het bestemmingsdashboard.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#standard-widgets). |

Voor meer informatie over [!DNL Dashboards], gelieve te zien het [[!DNL Dashboards]  overzicht ](../../dashboards/home.md).

## Gegevensverzameling {#data-collection}

Het platform biedt een reeks technologieën die u toestaan om cliënt-zijgegevens van de klantenervaring te verzamelen en het te verzenden naar de Edge Network van Adobe Experience Platform waar het kan worden verrijkt, worden getransformeerd, en aan Adobe of niet-Adobe bestemmingen worden gedistribueerd.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde UI-workflow voor configuratie gegevensstroom | De workflow voor het maken van een nieuwe gegevensstroom in de gebruikersinterface voor gegevensverzameling is bijgewerkt. Wanneer u services toevoegt aan een gegevensstroom, worden alleen de services waartoe u toegang hebt, opgenomen in de lijst met opties. Zie de gids op [ vormend een datastream ](../../datastreams/overview.md) voor meer informatie. |
| Gegevensvoorvoegsel voor gegevensverzameling | Als u de SDK van het Web van Adobe Experience Platform gebruikt, kunt u de mogelijkheden van de Prep van Gegevens nu hefboomwerking om uw gegevens aan de server van het Model van de Gegevens van de Ervaring (XDM) in kaart te brengen. Zie de sectie op [ Prep van Gegevens voor de Inzameling van Gegevens ](../../datastreams/data-prep.md) in de gids van gegevensstromen voor meer informatie. |
| Apparaat-id&#39;s van eerste partij | U kunt nu uw eigen apparaat-id&#39;s naar de Adobe Experience Platform-Edge Network sturen wanneer u klantgegevens verzamelt met de Platform Web SDK. Zo kunt u een oplossing bieden voor recente browserbeperkingen voor de levensduur van cookies van derden. Zie de gids op [ eerste-partijapparaat IDs ](../../web-sdk/identity/first-party-device-ids.md) voor meer informatie. |

Voor meer informatie over gegevensinzameling in Platform, zie gelieve het [ overzicht van de gegevensinzameling ](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ----------- | ----------- |
| (Beta) Destination SDK-ondersteuning voor op bestanden gebaseerde doelen | [ Destination SDK steun voor op dossier-gebaseerde bestemmingen ](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) is momenteel in privé bèta en is slechts beschikbaar aan een geselecteerd aantal partners en klanten. De functionaliteit en bijbehorende documentatie kunnen worden gewijzigd voordat de algemene beschikbaarheidsrelease beschikbaar wordt.<br><br> contacteer uw de rekeningsvertegenwoordiger van de Adobe om te leren hoe te om tot de eigenschap toegang te hebben. De Adobe-interne rekeningsvertegenwoordigers zouden uit naar de Experience Platform doelproducten en de technische teams moeten reiken om gesteunde gebruiksgevallen te bespreken. <br><br> in de bètafase van de steun van Destination SDK voor op dossier-gebaseerde bestemmingen, bètapartners en klanten kunnen de [ Destination SDK van het Experience Platform ](../../destinations/destination-sdk/overview.md) gebruiken om privé bestemmingen te bouwen om van de volgende functionaliteit te profiteren: <ul><li>Maak een bestandsgebaseerde (batch) bestemming via Amazon S3, SFTP-servers, Azure Blob, Azure Data Lake Storage, Data Landing Zone storage.</li><li>Configureer en stel standaardopties voor het plannen en uitvoeren van bestanden in.</li><li>Configureer en stel opties in om uw geëxporteerde CSV-bestanden op te maken (scheidingstekens, escape-tekens en andere opties).</li><li>Mogelijkheid om aangepaste bestandsheaders in te stellen en te bewerken.</li><li>Mogelijkheid om gebeurtenismeldingen te ontvangen over het exporteren van bestanden en segmenten.</li><li>Mogelijkheid om aanvullende bestandstypen te exporteren, zoals CSV, TSV, JSON, Parquet.</li></ul>  <br> om met de nieuwe functionaliteit begonnen te worden, lees [ (Beta) Gebruik Destination SDK om een op dossier-gebaseerde bestemming ](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md) te vormen. <br><br> De functionaliteit om privé of geproduceerde *het stromen* bestemmingen tot stand te brengen door Destination SDK te gebruiken is reeds beschikbaar aan alle klanten en partners van het Experience Platform. Lees de gids op hoe te [ gebruik Destination SDK om een het stromen bestemming ](../../destinations/destination-sdk/guides/configure-destination-instructions.md) voor details te vormen. |

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Adobe Experience Platform [!DNL Identity Service] helpt u een beter inzicht te krijgen in uw klanten en hun gedrag door identiteiten te overbruggen tussen apparaten en systemen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe machtiging voor `view-identity-graph` | U kunt nu de machtiging `view-identity-graph` gebruiken om te bepalen of gebruikers in uw organisatie identiteitsgrafiekgegevens kunnen weergeven. Gebruikers zonder deze machtiging hebben geen toegang tot de viewer voor identiteitsgrafieken in de gebruikersinterface of tot API&#39;s van [!DNL Identity Service] die identiteiten retourneren. Zie het [ overzicht van de toegangscontrole ](../../access-control/home.md) voor meer informatie over toestemmingen. |

Voor meer algemene informatie over [!DNL Identity Service], verwijs naar het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Beta-bronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).