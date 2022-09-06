---
description: Adobe Experience Platform Destination SDK is een reeks configuratie APIs die u toestaan om bestemmingsintegratiepatronen voor Experience Platform te vormen om publiek en profielgegevens aan uw eindpunt te leveren, die op gegevens en authentificatieformaten van uw keus wordt gebaseerd. De configuraties worden opgeslagen in het Experience Platform en kunnen via de API voor extra updates worden opgehaald.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: af8718f7d5351993c5e4aa00822ed7d2b290b9f0
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 1%

---

# Adobe Experience Platform Destination SDK

## Overzicht {#destinations-sdk}

Adobe Experience Platform Destination SDK is een reeks configuratie APIs die u toestaan om bestemmingsintegratiepatronen voor Experience Platform te vormen om publiek en profielgegevens aan uw eindpunt te leveren, die op gegevens en authentificatieformaten van uw keus wordt gebaseerd. De configuraties worden opgeslagen in het Experience Platform en kunnen via de API voor extra updates worden opgehaald.

De documentatie van de Destination SDK verstrekt instructies voor u om het Adobe Experience Platform Destination SDK te gebruiken om een productievere bestemmingsintegratie met Adobe Experience Platform te vormen, te testen en vrij te geven, en uw bestemming te hebben deel van de steeds groeiende bestemmingscatalogus worden.

![Overzicht van de doelcatalogus](./assets/destinations-catalog-overview.png)

## Productie- en aangepaste integratie {#productized-custom-integrations}

Als partner van Destination SDK, kunt u van het toevoegen van uw geproduceerde bestemming aan het profiteren [Catalogus Experience Platform](/help/destinations/catalog/overview.md):
1. Standaardiseer integratieconfiguraties voor alle klanten met vooraf geconfigureerde parameters en vereenvoudig de installatie-ervaring voor klanten.
2. Introduceer een branded bestemmingskaart in de catalogus van de bestemmingen van het Experience Platform voor vereenvoudigde klantenopstelling en bewustzijn.
3. Wees uitgerust met een productieve bestemmingsintegratie met Adobe Experience Platform en Real-time Customer Data Platform.

Als klant van het Experience Platform, kunt u een eigen privé douanebestemming ontwerpen, die het best uw activeringsbehoeften kan aanpassen.

![Destination SDK visueel diagram](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Ondersteunde soorten integratie {#supported-integration-types}

Door Destination SDK, steunt Adobe Experience Platform integratie in real time met bestemmingen die een REST API eindpunt hebben. De real-time integratie met Experience Platform ondersteunt mogelijkheden zoals:
* Berichtentransformatie en -aggregatie
* Profiel terugzetten
* Configureerbare metagegevensintegratie om de publieksinstellingen en gegevensoverdracht te initialiseren
* Configureerbare verificatie
* Een pakket test- en validatie-API&#39;s waarmee u uw doelconfiguraties kunt testen en doorlopen

Lees meer over de technische vereisten aan de kant van de bestemmingen in de [integratievereisten](./integration-prerequisites.md) artikel.

## Toegang tot Destination SDK krijgen {#get-access}

De toegang van Destination SDK varieert gebaseerd op uw status als partner of Experience Platform, de klant van Real-Time CDP. Zie de onderstaande tabel voor meer informatie.


| Type van partner of klant | Toegang tot Destination SDK |
---------|----------|
| Independent Software Vendor (ISV) | Verbinden met [Adobe Exchange-programma](https://partners.adobe.com/exchangeprogram/experiencecloud.html) en verzoek om een Experience Platform-sandbox beschikbaar te maken voor toegang tot Destination SDK. |
| Systeemintegrator (SI) | U dient op Gold- of Platinum-niveau te zijn in de [Adobe Solution Partner-programma](https://solutionpartners.adobe.com/home.html)en u krijgt een sandbox met Experience Platforms en toegang tot Destination SDK. |
| De klant van het Experience Platform op de [Real-Time CDP Ultimate-pakket](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Door gebrek, krijgt u toegang tot de zandbakken van het Experience Platform en Destination SDK, die u toestaan om privé bestemmingen voor uw organisatie te bouwen. |

{style=&quot;table-layout:auto&quot;}

## Proces op hoog niveau {#process}

Het proces om uw bestemming in Experience Platform te vormen wordt hieronder geschetst:

1. Als u ISV of SI bent, zie het krijgen toegangsinformatie in de sectie hierboven. [Adobe Experience Platform-activering](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) klanten kunnen deze stap overslaan.
2. [Verzoek om een Experience Platform-sandbox te leveren](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) en laat de toestemming van de bestemmingsauteur toe.
3. Bouw uw integratie op. Volg de instructies in de productdocumentatie om te configureren [streaming doelen](./configure-destination-instructions.md) of [bestandsgebaseerde doelen (bèta)](./configure-file-based-destination-instructions.md).
4. Test uw integratie. Volg de instructies in de productdocumentatie om te testen [streaming doelen](./test-destination.md) of [bestandsgebaseerde doelen (bèta)](./file-based-destination-testing-overview.md).
5. Als u een ISV of SI creeert [productievere integratie](./overview.md#productized-custom-integrations), [uw integratie verzenden](./submit-destination.md) voor Adobe (de standaardresponstijd is vijf werkdagen).
6. Als u ISV of SI creërend een productieve integratie bent, gebruik [zelfbedieningsdocumentatie](./docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie op Experience League voor uw bestemming tot stand te brengen.
7. Voor productieve integratie, zodra goedgekeurd door Adobe, zal uw integratie verschijnen in [Catalogus Experience Platform](/help/destinations/catalog/overview.md).
8. Volg hetzelfde proces als u uw integratie wilt bijwerken.

## Referenties  {#reference}

Adobe raadt u aan de volgende documentatie van het Experience Platform te lezen en te begrijpen:

* [Overzicht Adobe Experience Platform-bestemmingen](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Basis van XDM-schemacompositie](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [Overzicht naamruimte identiteit](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
