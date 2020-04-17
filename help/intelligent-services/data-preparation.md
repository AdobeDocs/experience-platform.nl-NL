---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Gegevens voorbereiden voor gebruik in intelligente services
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 03135f564bd72fb60e41b02557cb9ca9ec11e6e8

---


# Gegevens voorbereiden voor gebruik in intelligente services

Om de Intelligente Diensten inzichten van uw marketing gebeurtenisgegevens te ontdekken, moeten de gegevens semantisch worden verrijkt en in een standaardstructuur worden gehandhaafd. Intelligente services hefboomwerkervaringsgegevensmodel (XDM) om dit te bereiken. Specifiek, moeten alle datasets die in de Intelligente Diensten worden gebruikt met het schema van XDM van **Consumer ExperienceEvent (CEE)** in overeenstemming zijn.

Dit document verstrekt algemene begeleiding bij het in kaart brengen van uw marketing gebeurtenisgegevens van veelvoudige kanalen aan dit schema, schetsend informatie over belangrijke gebieden binnen het schema om u te helpen bepalen hoe te om uw gegevens aan zijn structuur effectief in kaart te brengen.

## Het CEE-schema

Het schema Consumer ExperienceEvent beschrijft het gedrag van een individu aangezien het betrekking heeft op digitale marketing gebeurtenissen (web of mobiel) evenals online of off-line handelsactiviteit. Het gebruik van dit schema wordt vereist voor de Intelligente Diensten wegens zijn semantisch duidelijk bepaalde gebieden (kolommen), vermijdend om het even welke onbekende namen die anders de gegevens minder duidelijk zouden maken.

Net als alle XDM-schema&#39;s is de CEE-mix uitbreidbaar. Met andere woorden, extra velden kunnen worden toegevoegd aan de CEE-mix en verschillende variaties kunnen indien nodig worden opgenomen in meerdere schema&#39;s.

Een volledig voorbeeld van de mix vindt u in de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)en moet worden gebruikt als referentie voor de belangrijkste velden die in de sectie hieronder worden beschreven.

### Hoofdvelden

In de onderstaande tabel worden de belangrijkste velden in de CEE-mix gemarkeerd die moeten worden gebruikt om Intelligent Services nuttige inzichten te laten genereren, waaronder beschrijvingen en koppelingen naar referentiedocumentatie voor meer voorbeelden.

| XDM-veld | Beschrijving | Referentie |
| --- | --- | --- |
| `xdm:channel` | Het marketingkanaal voor de ExperienceEvent. Het veld bevat informatie over het kanaaltype, het mediatype en het locatietype. **Dit veld _moet_worden opgegeven voordat Attribution AI kan werken met uw gegevens**. Zie de [tabel hieronder](#example-channels) voor een aantal voorbeeldtoewijzingen. | [Het kanaalschema van de ervaring](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) |
| `xdm:productListItems` | Een array van items die producten vertegenwoordigen die door een klant zijn geselecteerd, inclusief de SKU, naam, prijs en hoeveelheid van het product. | [Detailschema voor handel](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:commerce` | Bevat specifieke informatie over de handel over ExperienceEvent, inclusief het inkoopordernummer en betalingsgegevens. | [Detailschema voor handel](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:web` | Vertegenwoordigt webdetails met betrekking tot de ExperienceEvent, zoals de interactie, paginadetails en de referentie. | [ExperienceEvent-webdetailschema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) |

### Voorbeeldkanalen {#example-channels}

Het `xdm:channel` veld vertegenwoordigt het marketingkanaal dat betrekking heeft op de ExperienceEvent. In de volgende tabel staan enkele voorbeelden van marketingkanalen die aan XDM zijn toegewezen:

| Kanaal | `channel.mediaType` | `channel._type` | `channel.mediaAction` |
| --- | --- | --- | --- |
| Betaalde zoekopdracht | BETAALD | ZOEKEN | KLIKKEN |
| Sociaal - Marketing | GEOOGD | SOCIAAL | KLIKKEN |
| Weergave | BETAALD | WEERGEVEN | KLIKKEN |
| E-mail | BETAALD | EMAIL | KLIKKEN |
| Interne referentie | EIGEN | DIRECT | KLIKKEN |
| WeergaveThrough weergeven | BETAALD | WEERGEVEN | IMPRESSIE |
| Omleiding QR-code | EIGEN | DIRECT | KLIKKEN |
| SMS-bericht | EIGEN | SMS | KLIKKEN |
| Mobiel | EIGEN | MOBIEL | KLIKKEN |

## Gegevens toewijzen en opnemen

Zodra u hebt bepaald of uw gegevens van de marketinggebeurtenissen aan het CEE schema kunnen worden in kaart gebracht, kunt u het proces beginnen om uw gegevens in de Intelligente Diensten te brengen. Neem contact op met de Adobe Consulting Services om u te helpen uw gegevens toe te wijzen aan het schema en deze in te voeren in de service.

Als u een abonnement op het Adobe Experience Platform hebt en u de gegevens zelf wilt toewijzen en invoeren, volgt u de stappen in de onderstaande sectie.

### Adobe Experience Platform gebruiken

>[!NOTE] Voor de onderstaande stappen is een abonnement op Experience Platform vereist. Als u geen toegang hebt tot Platform, gaat u verder met de [volgende sectie](#next-steps) voor stappen.

In deze sectie wordt de workflow beschreven voor het toewijzen en invoeren van gegevens in het Experience Platform voor gebruik in Intelligente services, inclusief koppelingen naar zelfstudies voor gedetailleerde stappen.

#### Een CEE-schema en gegevensset maken

Wanneer u klaar bent om uw gegevens voor opname voor te bereiden, is de eerste stap een nieuw schema te creëren XDM dat de CEE mengeling gebruikt. De volgende zelfstudies lopen door het proces om een nieuw schema in UI of API tot stand te brengen:

* [Een schema maken in de gebruikersinterface](../xdm/tutorials/create-schema-ui.md)
* [Een schema maken in de API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] De bovenstaande zelfstudies volgen een algemene workflow voor het maken van een schema. Wanneer u een klasse voor het schema kiest, moet u de **klasse** XDM ExperienceEvent gebruiken. Nadat u deze klasse hebt gekozen, kunt u de CEE-mix aan het schema toevoegen.

Nadat u de CEE-mix aan het schema hebt toegevoegd, kunt u desgewenst andere combinaties toevoegen voor extra velden in uw gegevens.

Zodra u het schema hebt gecreeerd en bewaard, kunt u een nieuwe dataset tot stand brengen die op dat schema wordt gebaseerd. De volgende zelfstudies lopen door het proces om een nieuwe dataset in UI of API tot stand te brengen:

* [Creeer een dataset in UI](../catalog/datasets/user-guide.md#create) (volg het werkschema voor het gebruiken van een bestaand schema)
* [Een gegevensset maken in de API](../catalog/datasets/create.md)

#### Gegevens toewijzen en opnemen

Na het creëren van een CEE schema en dataset, kunt u beginnen uw gegevenslijsten aan het schema in kaart te brengen en die gegevens in Platform in te voeren. Zie de zelfstudie over het [toewijzen van een CSV-bestand aan een XDM-schema](../ingestion/tutorials/map-a-csv-file.md) voor stappen over het uitvoeren van dit bestand in de gebruikersinterface. Zodra een dataset is bevolkt, kan de zelfde dataset worden gebruikt om extra gegevensdossiers in te voeren.

## Volgende stappen {#next-steps}

Dit document bevat algemene richtlijnen voor het voorbereiden van uw gegevens voor gebruik in Intelligente services. Neem contact op met de Technische Ondersteuning van Adobe als u extra advies nodig hebt op basis van uw gebruikscase.

Zodra u met succes een dataset met uw gegevens van de klantenervaring hebt bevolkt, kunt u de Intelligente Diensten gebruiken om inzichten te produceren. Raadpleeg de volgende documenten om aan de slag te gaan:

* [Overzicht AI-kenmerken](./attribution-ai/overview.md)
* [AI-overzicht van klant](./customer-ai/overview.md)
