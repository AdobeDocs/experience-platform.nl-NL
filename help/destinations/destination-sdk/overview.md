---
description: Adobe Experience Platform de Bestemming SDK is een reeks configuratie APIs die u toestaan om bestemmingsintegratiepatronen voor Experience Platform te vormen om publiek en profielgegevens aan uw eindpunt te leveren, die op gegevens en authentificatieformaten van uw keus wordt gebaseerd. De configuraties worden opgeslagen in het Experience Platform en kunnen via de API voor extra updates worden opgehaald.
title: Adobe Experience Platform-doelSDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: bd65cfa557fb42d23022578b98bc5482e8bd50b1
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 1%

---

# Adobe Experience Platform-doelSDK

## Overzicht {#destinations-sdk}

De Doel SDK van Adobe Experience Platform is een reeks configuratie APIs die u toestaan om bestemmingsintegratiepatronen voor Experience Platform te vormen om publiek en profielgegevens aan uw eindpunt te leveren, die op gegevens en authentificatieformaten van uw keus wordt gebaseerd. De configuraties worden opgeslagen in het Experience Platform en kunnen via de API voor extra updates worden opgehaald.

De documentatie van SDK van de Bestemming verstrekt instructies voor u om de Doel SDK van Adobe Experience Platform te gebruiken om een productievere bestemmingsintegratie met Adobe Experience Platform te vormen, te testen en vrij te geven, en uw bestemming te hebben deel van de steeds groeiende bestemmingscatalogus worden.

![Overzicht van de doelcatalogus](./assets/destinations-catalog-overview.png)

## Productie- en aangepaste integratie {#productized-custom-integrations}

Als partner van SDK van de Bestemming, kunt u van het toevoegen van uw geproduceerde bestemming aan [de catalogus van het Experience Platform](/help/destinations/catalog/overview.md) profiteren:
1. Standaardiseer integratieconfiguraties voor alle klanten met vooraf geconfigureerde parameters en vereenvoudig de installatie-ervaring voor klanten.
2. Introduceer een branded bestemmingskaart in de catalogus van de bestemmingen van het Experience Platform voor vereenvoudigde klantenopstelling en bewustzijn.
3. U kunt kiezen voor een productieve doelintegratie met Adobe Experience Platform en Real-time Customer Data Platform.

Als klant van het Experience Platform, kunt u een eigen privé douanebestemming ontwerpen, die het best uw activeringsbehoeften kan aanpassen.

![Zichtbaar diagram van SDK van bestemming](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Ondersteunde soorten integratie {#supported-integration-types}

Door Doel SDK, steunt Adobe Experience Platform integratie in real time met bestemmingen die een REST API eindpunt hebben. De real-time integratie met Experience Platform ondersteunt mogelijkheden zoals:
* Berichtentransformatie en -aggregatie
* Profiel terugzetten
* Configureerbare metagegevensintegratie om de publieksinstellingen en gegevensoverdracht te initialiseren
* Configureerbare verificatie
* Een pakket test- en validatie-API&#39;s waarmee u uw doelconfiguraties kunt testen en doorlopen

Lees over de technische vereisten aan de bestemmingskant in [integratieeerste vereisten](./integration-prerequisites.md) artikel.


## Toegang tot doel-SDK ophalen {#get-access}

De toegang van SDK van de bestemming varieert gebaseerd op uw status als partner of klant van het Experience Platform. Zie de onderstaande tabel voor meer informatie.


| Type van partner of klant | Hoe te om tot Bestemming SDK toegang te hebben |
---------|----------|
| Independent Software Vendor (ISV) | Sluit aan [Adobe uitwisselingsprogramma](https://partners.adobe.com/exchangeprogram/experiencecloud.html) aan en verzoek om een zandbak van het Experience Platform te krijgen provisioned aan de toegang SDK van de Bestemming. |
| Systeemintegrator (SI) | U moet op of het Niveau van het Goud of Platinum in [Adobe Programma van de Partner van de Oplossing ](https://solutionpartners.adobe.com/home.html) zijn, en u zult een zandbak van het Experience Platform provisioned en toegang tot Doel SDK krijgen. |
| Klant van het Experience Platform op [Activeringspakket](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) | Standaard krijgt u toegang tot Experience Platform-sandboxen en de SDK van Doel. |
| De klant van het Experience Platform op [Real-time CDP pakket](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | U hebt geen toegang tot Doel SDK, maar u hebt toegang tot alle geproduceerde bestemmingen die door andere bedrijven worden gevormd gebruikend de SDK van de Bestemming en die over de organisaties van het Experience Platform worden gepubliceerd. |

{style=&quot;table-layout:auto&quot;}

## Proces op hoog niveau {#process}

Het proces om uw bestemming in Experience Platform te vormen wordt hieronder geschetst:

1. Als u ISV of SI bent, zie het krijgen toegangsinformatie in de sectie hierboven. [Klanten van Adobe Experience Platform-](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) activering kunnen deze stap overslaan.
2. [Verzoek om een ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) sandbox van een Experience Platform te voorzien en de toestemming van de bestemmingsauteur toe te laten.
3. [Stel uw ](./configure-destination-instructions.md) integratie op volgens de productdocumentatie.
4. [Test uw ](./test-destination.md) integratie volgens de productdocumentatie.
5. [Verzend uw ](./destination-publish-api.md) integratie voor revisie van Adobe (de standaardresponstijd is 5 werkdagen).
6. Als u een ISV of SI creërend een [productievere integratie](./overview.md#productized-custom-integrations) bent, gebruik [zelfbedienings documentatieproces](./docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie op Experience League voor uw bestemming tot stand te brengen.
7. Zodra goedgekeurd door Adobe, zal uw integratie in [Experience Platform catalogus](/help/destinations/catalog/overview.md) verschijnen.
8. Als u uw integratie wilt bijwerken, volgt u hetzelfde proces.

## Referenties  {#reference}

Adobe raadt u aan de volgende documentatie van het Experience Platform te lezen en te begrijpen:

* [Overzicht Adobe Experience Platform-bestemmingen](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Basis van XDM-schemacompositie](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [Overzicht naamruimte identiteit](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
