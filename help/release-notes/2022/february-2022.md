---
title: Aanvullende informatie voor Adobe Experience Platform van februari 2022
description: Aanvullende informatie voor Adobe Experience Platform van februari 2022.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 14%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum:dinsdag 7 maart 2022**

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

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe standaarddoelen voor widgets | Met de volgende standaardwidgets kunt u verschillende meetgegevens visualiseren die betrekking hebben op uw doelen.<ul><li>Onlangs geactiveerde segmenten op doel. Deze widget geeft de bovenste vijf laatst geactiveerde segmenten in aflopende volgorde weer, afhankelijk van de gekozen bestemming.</li><li>Ontwikkeling van de omvang van het publiek. Deze widget geeft de relatie weer van de profieltelling over een tijdsperiode voor een segment dat aan die bestemmingsrekening in kaart is gebracht.</li><li>Niet-toegewezen segmenten op identiteit. Deze widget geeft een overzicht van de bovenste vijf niet-toegewezen segmenten die worden gerangschikt op basis van het aantal identiteiten voor een bepaald doel en een bepaalde identiteit.</li><li>Toegewezen segmenten op identiteit. Deze widget geeft een overzicht van de bovenste vijf toegewezen segmenten. De segmenten worden bevolen van hoog tot laag afhankelijk van hun respectieve tellingen van bron IDs die bestemmingsidentiteitskaart aanpassen die van het drop-down menu van widget wordt geselecteerd.</li><li>Veelvoorkomende doelgroepen. Deze widget bevat een lijst met de bovenste vijf segmenten die zijn geactiveerd voor de doelaccount die boven aan de pagina is gekozen, en het doel dat is geselecteerd in het vervolgkeuzemenu van de widget.</li></ul> Voor meer informatie over de beschikbare standaard widgets, zie de [ documentatie van het bestemmingsdashboard.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#standard-widgets). |

Voor meer informatie over [!DNL Dashboards] raadpleegt u het [[!DNL Dashboards] overzicht](../../dashboards/home.md).

## Dataverzameling {#data-collection}

Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen op de client kunt verzamelen en naar de Adobe Experience Platform Edge Network kunt sturen waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde UI-workflow voor configuratie gegevensstroom | De workflow voor het maken van een nieuwe gegevensstroom in de gebruikersinterface voor gegevensverzameling is bijgewerkt. Wanneer u services toevoegt aan een gegevensstroom, worden alleen de services waartoe u toegang hebt, opgenomen in de lijst met opties. Zie de gids op [ vormend een datastream ](../../datastreams/overview.md) voor meer informatie. |
| Gegevensvoorvoegsel voor gegevensverzameling | Als u Adobe Experience Platform Web SDK gebruikt, kunt u nu de mogelijkheden van de Prep van Gegevens gebruiken om uw gegevens aan de server van het Model van de Gegevens van de Ervaring (XDM) in kaart te brengen. Zie de sectie op [ Prep van Gegevens voor de Inzameling van Gegevens ](../../datastreams/data-prep.md) in de gids van gegevensstromen voor meer informatie. |
| Apparaat-id&#39;s van eerste partij | U kunt nu uw eigen apparaat-id&#39;s naar de Adobe Experience Platform Edge Network sturen wanneer u klantgegevens verzamelt met de Experience Platform Web SDK. Zo kunt u een oplossing bieden voor recente browserbeperkingen voor de levensduur van cookies van derden. Zie de gids op [ eerste-partijapparaat IDs ](/help/collection/use-cases/identity/first-party-device-ids.md) voor meer informatie. |

Voor meer informatie over gegevensinzameling in Experience Platform, te zien gelieve het [ overzicht van de gegevensinzameling ](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| (Beta) Destination SDK-ondersteuning voor op bestanden gebaseerde doelen | [ de steun van Destination SDK voor op dossier-gebaseerde bestemmingen ](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) is momenteel in privé bèta en is slechts beschikbaar aan een geselecteerd aantal partners en klanten. De functionaliteit en bijbehorende documentatie kunnen worden gewijzigd voordat de algemene beschikbaarheidsrelease beschikbaar wordt.<br><br> contacteer uw Adobe rekeningsvertegenwoordiger om te leren hoe te om tot de eigenschap toegang te hebben. Adobe-interne accountvertegenwoordigers moeten contact opnemen met de Experience Platform-teams voor producten en engineering om ondersteunde gebruiksgevallen te bespreken. <br><br> in de bètafase van de steun van Destination SDK voor op dossier-gebaseerde bestemmingen, bètapartners en klanten kunnen [ Experience Platform Destination SDK ](../../destinations/destination-sdk/overview.md) gebruiken om privé bestemmingen te bouwen om van de volgende functionaliteit te profiteren: <ul><li>Maak een bestandsgebaseerde (batch) bestemming via Amazon S3, SFTP-servers, Azure Blob, Azure Data Lake Storage, Data Landing Zone storage.</li><li>Configureer en stel standaardopties voor het plannen en uitvoeren van bestanden in.</li><li>Configureer en stel opties in om uw geëxporteerde CSV-bestanden op te maken (scheidingstekens, escape-tekens en andere opties).</li><li>Mogelijkheid om aangepaste bestandsheaders in te stellen en te bewerken.</li><li>Mogelijkheid om gebeurtenismeldingen te ontvangen over het exporteren van bestanden en segmenten.</li><li>Mogelijkheid om aanvullende bestandstypen te exporteren, zoals CSV, TSV, JSON, Parquet.</li></ul>  <br> om met de nieuwe functionaliteit te beginnen, lees [ (Beta) Gebruik Destination SDK om een op dossier-gebaseerde bestemming ](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md) te vormen. <br><br> De functionaliteit om privé of geproduceerde *het stromen* bestemmingen tot stand te brengen door Destination SDK te gebruiken is reeds beschikbaar aan alle klanten en partners van Experience Platform. Lees de gids op hoe te [ gebruik Destination SDK om een het stromen bestemming ](../../destinations/destination-sdk/guides/configure-destination-instructions.md) voor details te vormen. |

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Adobe Experience Platform [!DNL Identity Service] helpt u een beter inzicht te krijgen in uw klanten en hun gedrag door identiteiten te overbruggen tussen apparaten en systemen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe machtiging voor `view-identity-graph` | U kunt nu de machtiging `view-identity-graph` gebruiken om te bepalen of gebruikers in uw organisatie identiteitsgrafiekgegevens kunnen weergeven. Gebruikers zonder deze machtiging hebben geen toegang tot de viewer voor identiteitsgrafieken in de gebruikersinterface of tot API&#39;s van [!DNL Identity Service] die identiteiten retourneren. Zie het [ overzicht van de toegangscontrole ](../../access-control/home.md) voor meer informatie over toestemmingen. |

Voor meer algemene informatie over [!DNL Identity Service], verwijs naar het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Beta-bronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li></ul> |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).