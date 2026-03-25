---
title: Uw doel documenteren in Adobe Experience Platform
description: Stapsgewijze instructies voor het maken van een documentatiepagina voor uw bestemming in Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Uw doel documenteren in [!DNL Adobe Experience Platform]

>[!IMPORTANT]
>
>Het hier gedocumenteerde proces wordt slechts vereist voor partners die geproduceerde (openbare) bestemmingen voorleggen. Als u een privé bestemming voor uw eigen gebruik creeert, te hoeven u niet om documentatie voor uw bestemming tot stand te brengen en te publiceren.

## Overzicht {#overview}

Welkom bij [!DNL Adobe Experience Platform] , leuk om je hier te hebben!
Het documenteren van uw bestemming is de laatste stap voordat u deze live kunt instellen in [!DNL Adobe Experience Platform] .

Deze sectie van documentatie omvat:

* Stapsgewijze instructies voor u om een documentatiepagina voor uw nieuwe bestemming tot stand te brengen;
* Een sjabloon dat u moet invullen voor uw doel.
* [ Algemene instructies bij het gebruiken van Markering ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [ Specifieke instructies voor de aroma van de Prijsverhoging van Adobe ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions) (de smaak van de Prijsverlaging van Adobe is zeer gelijkaardig aan regelmatige Prijsverlaging).
* A [ beste praktijken pagina ](./authoring-best-practices.md) om u te helpen een documentatiepagina voor uw bestemmingspagina ontwerpen, die aan de normen van de documentatiekwaliteit van Experience Platform voldoet.

## Vereisten {#prerequisites}

Om documentatie voor uw bestemming volgens de instructies in dit artikel tot stand te brengen, zijn de volgende punten noodzakelijk:

* **de rekening van GitHub van A**. Teken omhoog voor [ GitHub ](https://github.com/) als u nog geen rekening hebt.
* **Desktop GitHub**. Als u selecteert om [ de documentatie in uw lokaal milieu ](./work-in-local-environment.md) tot stand te brengen, moet u [ Desktop GitHub ](https://desktop.github.com/) gebruiken.
* Uw integratie met Adobe moet zich in een testfase bevinden en uw bestemming moet worden geïmplementeerd in een testomgeving in [!DNL Adobe Experience Platform] .

## Instructies op hoog niveau om documentatie voor uw doel te maken in [!DNL Adobe Experience Platform] {#high-level-instructions}

Op een hoog niveau, om documentatie voor uw bestemming tot stand te brengen, moet u [ een vork ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) van de [!DNL Adobe Experience Platform] documentatiebewaarplaats creëren en [ verstrekken documentatiemalplaatje ](./self-service-template.md) in een nieuwe tak uitgeven. Gebruik de door Adobe verschafte sjabloon om een nieuwe doelpagina te maken. Open een trekkingsverzoek (PR) wanneer u klaar bent. De instructies om dit te doen zijn verder hieronder, in [ Stappen om uw nieuwe bestemmingspagina ](./documentation-instructions.md#steps-to-create-docs-page) tot stand te brengen.

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Documentatiesjabloon {#documentation-template}

Om u bij het creëren van uw documentatiepagina bij te staan, heeft Adobe a [ documentatiemalplaatje ](./self-service-template.md) voor u vooraf ingevuld. Hieronder vindt u instructies voor het bewerken van de sjabloon en het openen van een pull-verzoek. Het Adobe-documentatieteam zal de documentatie voor uw nieuwe bestemming controleren en publiceren.

[ Download hier het malplaatje ](../assets/docs-framework/yourdestination-template.zip) en unzip het dossier om het `yourdestination.md` dossier te halen.

Hieronder vindt u instructies over het gebruik van de sjabloon voor het maken van de documentatiepagina.

## Stappen om uw nieuwe bestemmingspagina te creëren {#steps-to-create-docs-page}

U kunt de GitHub Webinterface of uw lokale milieu gebruiken om documentatie voor uw nieuwe bestemming in [!DNL Adobe Experience Platform] tot stand te brengen. Zoek instructies voor beide opties in de onderstaande koppelingen:

* [Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen](./use-github-interface-to-create-documentation.md)
* [Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken](./work-in-local-environment.md)

## Best practices {#best-practices}

Herzie [ auteursbeste praktijken ](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) vóór en terwijl u de pagina van de bestemmingsdocumentatie creeert. Zorg ervoor om [ ook te lezen die begeleiding voor de Documentatie van Adobe ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) voor sommige meer het schrijven uiteinden schrijven die het de documentatieteam van Adobe wanneer het ontwerpen van documentatie gebruikt.