---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: 5f6b46245781051da01a8051f023df11ff4c7d51
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 7 maart 2022**

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

Adobe Experience Platform biedt meerdere [!DNL dashboards] waardoor u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals die tijdens dagelijkse momentopnamen worden gevangen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe standaarddoelen voor widgets | Met de volgende standaardwidgets kunt u verschillende meetgegevens visualiseren die betrekking hebben op uw doelen.<ul><li>Onlangs geactiveerde segmenten op doel. Deze widget geeft de bovenste vijf laatst geactiveerde segmenten in aflopende volgorde weer, afhankelijk van de gekozen bestemming.</li><li>Ontwikkeling van de omvang van het publiek. Deze widget geeft de relatie weer van de profieltelling over een tijdsperiode voor een segment dat aan die bestemmingsrekening in kaart is gebracht.</li><li>Niet-toegewezen segmenten op identiteit. Deze widget geeft een overzicht van de bovenste vijf niet-toegewezen segmenten die worden gerangschikt op basis van het aantal identiteiten voor een bepaald doel en een bepaalde identiteit.</li><li>Toegewezen segmenten op identiteit. Deze widget geeft een overzicht van de bovenste vijf toegewezen segmenten. De segmenten worden bevolen van hoog tot laag afhankelijk van hun respectieve tellingen van bron IDs die bestemmingsidentiteitskaart aanpassen die van het drop-down menu van widget wordt geselecteerd.</li><li>Veelvoorkomende doelgroepen. Deze widget bevat een lijst met de bovenste vijf segmenten die zijn geactiveerd voor de doelaccount die boven aan de pagina is gekozen, en het doel dat is geselecteerd in het vervolgkeuzemenu van de widget.</li></ul> Zie voor meer informatie over de beschikbare standaardwidgets de [documentatie van het dashboard van bestemmingen.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

Voor meer informatie over [!DNL Dashboards], zie de [[!DNL Dashboards] overzicht](../../dashboards/home.md).

## Gegevensverzameling {#data-collection}

Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar het kan worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde UI-workflow voor configuratie gegevensstroom | De workflow voor het maken van een nieuwe gegevensstroom in de gebruikersinterface voor gegevensverzameling is bijgewerkt. Wanneer u services toevoegt aan een gegevensstroom, worden alleen de services waartoe u toegang hebt, opgenomen in de lijst met opties. Zie de handleiding op [configureren van een gegevensstroom](../../edge/fundamentals/datastreams.md) voor meer informatie . |
| Gegevensvoorvoegsel voor gegevensverzameling | Als u de SDK van het Web van Adobe Experience Platform gebruikt, kunt u de mogelijkheden van de Prep van Gegevens nu hefboomwerking om uw gegevens aan de server van het Model van de Gegevens van de Ervaring (XDM) in kaart te brengen. Zie de sectie over [Gegevensvoorvoegsel voor gegevensverzameling](../../edge/fundamentals/datastreams.md#data-prep) in de gids voor gegevensstromen voor meer informatie. |
| Apparaat-id&#39;s van eerste partij | U kunt nu uw eigen apparaat-id&#39;s naar het Adobe Experience Platform Edge Network sturen wanneer u klantgegevens verzamelt met de SDK van het Web Platform, waarmee u een oplossing kunt vinden voor recente browserbeperkingen met betrekking tot de levensduur van cookies van derden. Zie de handleiding op [apparaat-id&#39;s van eerste partij](../../edge/identity/first-party-device-ids.md) voor meer informatie . |

Voor meer informatie over gegevensverzameling in Platform raadpleegt u de [overzicht van gegevensverzameling](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| (Bèta) Destination SDK-ondersteuning voor op bestanden gebaseerde doelen | [Destination SDK-ondersteuning voor op bestanden gebaseerde doelen](../../destinations/destination-sdk/file-based-destination-configuration.md) is momenteel in privé bèta en is slechts beschikbaar aan een geselecteerd aantal partners en klanten. De functionaliteit en bijbehorende documentatie kunnen worden gewijzigd voordat de algemene beschikbaarheidsrelease beschikbaar wordt.<br><br>Neem contact op met uw Adobe-accountvertegenwoordiger voor meer informatie over de functie. De Adobe-interne rekeningsvertegenwoordigers zouden uit naar de Experience Platform doelproducten en de technische teams moeten reiken om gesteunde gebruiksgevallen te bespreken. <br><br> In de bètafase van de steun van Destination SDK voor op dossier-gebaseerde bestemmingen, bètapartners en klanten kunnen gebruiken [Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) om privé bestemmingen te bouwen om van de volgende functionaliteit te profiteren: <ul><li>Maak een bestandsgebaseerde (batch) bestemming via Amazon S3, SFTP-servers, Azure Blob, Azure Data Lake Storage, Data Landing Zone storage.</li><li>Configureer en stel standaardopties voor het plannen en uitvoeren van bestanden in.</li><li>Configureer en stel opties in om uw geëxporteerde CSV-bestanden op te maken (scheidingstekens, escape-tekens en andere opties).</li><li>Mogelijkheid om aangepaste bestandsheaders in te stellen en te bewerken.</li><li>Mogelijkheid om gebeurtenismeldingen te ontvangen over het exporteren van bestanden en segmenten.</li><li>Mogelijkheid om aanvullende bestandstypen te exporteren, zoals CSV, TSV, JSON, Parquet.</li></ul>  <br>Om aan de slag te gaan met de nieuwe functionaliteit, leest u [(Bèta) Gebruik Destination SDK om een op dossier-gebaseerde bestemming te vormen](../../destinations/destination-sdk/file-based-destination-configuration.md). <br><br> De functionaliteit om privé of tot stand te brengen *streaming* de bestemmingen door Destination SDK te gebruiken zijn reeds beschikbaar aan alle klanten en partners van het Experience Platform. Lees de handleiding over hoe u [gebruik Destination SDK om een het stromen bestemming te vormen](/help/destinations/destination-sdk/configure-destination-instructions.md) voor meer informatie. |

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Adobe Experience Platform [!DNL Identity Service] helpt u een beter inzicht te krijgen in uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe machtiging voor `view-identity-graph` | U kunt nu de opdracht `view-identity-graph` toestemming om te controleren of de gebruikers in uw organisatie de gegevens van de identiteitsgrafiek kunnen bekijken. Gebruikers zonder deze machtiging hebben geen toegang tot de viewer voor identiteitsgrafieken in de gebruikersinterface of bij toegang tot [!DNL Identity Service] API&#39;s die id&#39;s retourneren. Zie de [toegangsbeheeroverzicht](../../access-control/home.md) voor meer informatie over machtigingen. |

Meer algemene informatie over [!DNL Identity Service], verwijst u naar de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bètabronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).