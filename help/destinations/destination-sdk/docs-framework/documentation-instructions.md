---
title: Uw doel documenteren in Adobe Experience Platform
description: Stapsgewijze instructies voor het maken van een documentatiepagina voor uw bestemming in Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '502'
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
* [&#x200B; Algemene instructies bij het gebruiken van Markering &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=nl-NL);
* [&#x200B; Specifieke instructies voor de aroma van de Vermindering van de Adobe &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=nl-NL#custom-markdown-extensions) (de geur van de Vermindering van de Adobe is zeer gelijkaardig aan regelmatige Vermindering).
* A [&#x200B; best practices pagina &#x200B;](./authoring-best-practices.md) om u te helpen een documentatiepagina voor uw bestemmingspagina ontwerpen, die aan de de documentatiekwaliteitsnormen van het Experience Platform voldoet.

## Vereisten {#prerequisites}

Om documentatie voor uw bestemming volgens de instructies in dit artikel tot stand te brengen, zijn de volgende punten noodzakelijk:

* **de rekening van GitHub van A**. Teken omhoog voor [&#x200B; GitHub &#x200B;](https://github.com/) als u nog geen rekening hebt.
* **Desktop GitHub**. Als u selecteert om [&#x200B; de documentatie in uw lokaal milieu &#x200B;](./work-in-local-environment.md) tot stand te brengen, moet u [&#x200B; Desktop GitHub &#x200B;](https://desktop.github.com/) gebruiken.
* Uw integratie met Adobe moet zich in een testfase bevinden en uw bestemming moet worden geïmplementeerd in een testomgeving in Adobe Experience Platform.

## Instructies op hoog niveau voor het maken van documentatie voor uw bestemming in Adobe Experience Platform {#high-level-instructions}

Op een hoog niveau, om documentatie voor uw bestemming tot stand te brengen, moet u [&#x200B; een vork &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=nl-NL#fork-the-repository) van de de documentatiebewaarplaats van Adobe Experience Platform tot stand brengen en het [&#x200B; verstrekte documentatiemalplaatje &#x200B;](./self-service-template.md) in een nieuwe tak uitgeven. Gebruik het Adobe-Verstrekte malplaatje om een nieuwe bestemmingspagina tot stand te brengen. Open een trekkingsverzoek (PR) wanneer u klaar bent. De instructies om dit te doen zijn verder hieronder, in [&#x200B; Stappen om uw nieuwe bestemmingspagina &#x200B;](./documentation-instructions.md#steps-to-create-docs-page) tot stand te brengen.

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/nl-NL/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Documentatiesjabloon {#documentation-template}

Om u bij het creëren van uw documentatiepagina bij te staan, heeft de Adobe a [&#x200B; documentatiemalplaatje &#x200B;](./self-service-template.md) voor u vooraf ingevuld. Hieronder vindt u instructies voor het bewerken van de sjabloon en het openen van een pull-verzoek. Het documentatieteam van de Adobe zal de documentatie voor uw nieuwe bestemming herzien en publiceren.

[&#x200B; Download hier het malplaatje &#x200B;](../assets/docs-framework/yourdestination-template.zip) en unzip het dossier om het `yourdestination.md` dossier te halen.

Hieronder vindt u instructies over het gebruik van de sjabloon voor het maken van de documentatiepagina.

## Stappen om uw nieuwe bestemmingspagina te creëren {#steps-to-create-docs-page}

U kunt de het Webinterface van GitHub of uw lokaal milieu gebruiken om documentatie voor uw nieuwe bestemming in Adobe Experience Platform tot stand te brengen. Zoek instructies voor beide opties in de onderstaande koppelingen:

* [Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen](./use-github-interface-to-create-documentation.md)
* [Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken](./work-in-local-environment.md)

## Best practices {#best-practices}

Herzie [&#x200B; auteursbeste praktijken &#x200B;](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) vóór en terwijl u de pagina van de bestemmingsdocumentatie creeert. Zorg ervoor om de [&#x200B; het schrijven begeleiding voor de Documentatie van de Adobe &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=nl-NL) voor sommige meer het schrijven uiteinden ook te lezen die het de documentatieteam van de Adobe gebruikt wanneer het ontwerpen van documentatie.