---
title: Uw doel documenteren in Adobe Experience Platform
description: Stapsgewijze instructies voor het maken van een documentatiepagina voor uw bestemming in Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Uw doel documenteren in Adobe Experience Platform

>[!IMPORTANT]
>
>Het hier gedocumenteerde proces wordt slechts vereist voor partners die geproduceerde (openbare) bestemmingen voorleggen. Als u een privé bestemming voor uw eigen gebruik creeert, te hoeven u niet om documentatie voor uw bestemming tot stand te brengen en te publiceren.

## Overzicht {#overview}

Welkom bij Adobe Experience Platform, geweldig om je hier te hebben!
Het documenteren van uw bestemming is de laatste stap voordat deze live kan worden ingesteld in Adobe Experience Platform.

Deze sectie van documentatie omvat:

* Stapsgewijze instructies voor u om een documentatiepagina voor uw nieuwe bestemming tot stand te brengen;
* Een sjabloon dat u moet invullen voor uw doel.
* [Algemene instructies voor het gebruik van Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Specifieke aanwijzingen voor de Adobe Markdown-aroma](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions) (De Adobe Markdown-smaak lijkt sterk op de gewone Markdown-methode).
* A [pagina met aanbevolen procedures](./authoring-best-practices.md) om u te helpen een documentatiepagina voor uw bestemmingspagina opstellen, die aan de normen van de documentatiekwaliteit van het Experience Platform voldoet.

## Vereisten {#prerequisites}

Om documentatie voor uw bestemming volgens de instructies in dit artikel tot stand te brengen, zijn de volgende punten noodzakelijk:

* **Een GitHub-account**. Aanmelden voor [GitHub](https://github.com/) als je nog geen account hebt.
* **GitHub Desktop**. Als u [de documentatie in uw lokale omgeving maken](./work-in-local-environment.md)moet u [GitHub Desktop](https://desktop.github.com/).
* Uw integratie met Adobe moet zich in een testfase bevinden en uw bestemming moet worden geïmplementeerd in een testomgeving in Adobe Experience Platform.

## Instructies op hoog niveau voor het maken van documentatie voor uw bestemming in Adobe Experience Platform {#high-level-instructions}

Op hoog niveau, om documentatie voor uw bestemming te creëren, moet u [een vork maken](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) van de Adobe Experience Platform-documentatieopslagplaats en bewerk de [meegeleverde documentatiesjabloon](./self-service-template.md) in een nieuwe vertakking. Gebruik het Adobe-Verstrekte malplaatje om een nieuwe bestemmingspagina tot stand te brengen. Open een trekkingsverzoek (PR) wanneer u klaar bent. Hieronder vindt u de instructies voor het gebruik van dit geneesmiddel, zoals beschreven in [Stappen om uw nieuwe bestemmingspagina te creëren](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Documentatiesjabloon {#documentation-template}

Om u te helpen bij het maken van uw documentatiepagina, heeft de Adobe een [documentatiesjabloon](./self-service-template.md) voor jou. Hieronder vindt u instructies voor het bewerken van de sjabloon en het openen van een pull-verzoek. Het documentatieteam van de Adobe zal de documentatie voor uw nieuwe bestemming herzien en publiceren.

[Download de sjabloon hier](../assets/docs-framework/yourdestination-template.zip) en decomprimeer het bestand om het uit te pakken `yourdestination.md` bestand.

Hieronder vindt u instructies over het gebruik van de sjabloon voor het maken van de documentatiepagina.

## Stappen om uw nieuwe bestemmingspagina te creëren {#steps-to-create-docs-page}

U kunt de het Webinterface van GitHub of uw lokaal milieu gebruiken om documentatie voor uw nieuwe bestemming in Adobe Experience Platform tot stand te brengen. Zoek instructies voor beide opties in de onderstaande koppelingen:

* [Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen](./use-github-interface-to-create-documentation.md)
* [Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken](./work-in-local-environment.md)

## Best practices {#best-practices}

Controleer de [best practices ontwerpen](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) voor en terwijl u de pagina van de bestemmingsdocumentatie creeert. Zorg ervoor dat u ook de [schriftelijke richtsnoeren voor Adobe Documentatie](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) voor wat meer het schrijven uiteinden die het de documentatieteam van de Adobe wanneer het ontwerpen van documentatie gebruikt.