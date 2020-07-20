---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime
topic: guide
translation-type: tm+mt
source-git-commit: 57ef7df4b9323b58a90660d515ade61a3974779f
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Handleiding voor API-ontwikkelaars

[!DNL Real-time Customer Profile] laat u toe om een holistische mening van elk van uw individuele klanten binnen Adobe Experience Platform te zien. [!DNL Profile] staat u toe om verschillende klantengegevens van veelvoudige kanalen, zoals online, off-line, CRM, en derdegegevens, in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

De [!DNL Real-time Customer Profile] API bevat meerdere eindpunten, die hieronder worden beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar de [begonnen gids](getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt bekijken, raadpleegt u de API-naslagwerker voor [realtime-klantprofiel](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

## (Alpha) Berekende kenmerken {#computed-attributes}

>[!IMPORTANT]
>
>De functie voor berekende kenmerken staat in alfa en is niet beschikbaar voor alle gebruikers. Documentatie en functionaliteit kunnen worden gewijzigd.

Met de berekende kenmerken kunt u automatisch de waarde van velden berekenen op basis van andere waarden, berekeningen en expressies. De berekende attributen werken op het profielniveau, betekenend kunt u waarden over alle verslagen en gebeurtenissen bijeenvoegen. Elk berekend kenmerk bevat een expressie, of &#39;regel&#39;, die binnenkomende gegevens evalueert en de resulterende waarde opslaat in een profielkenmerk of in een gebeurtenis. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. U kunt gegevens verwerkte attributen tot stand brengen, bekijken, uitgeven en schrappen gebruikend het `config/computedAttributes` eindpunt. Om te leren hoe te om dit eindpunt te gebruiken, bezoek de [gegevens verwerkte gids](computed-attributes.md)van het attributeneindpunt.

## Edge-prognoses {#edge-projections}

Adobe Experience Platform maakt het mogelijk om in real time de ervaringen van klanten te personaliseren door gegevens gemakkelijk toegankelijk te maken op strategisch gelegen servers die &quot;randen&quot; worden genoemd. De [!DNL Real-time Customer Profile] API verstrekt eindpunten voor het werken met randen door componenten genoemd &quot;projecties.&quot; Dit omvat projectieconfiguraties om te bepalen welke gegevens aan elke rand moeten worden geprojecteerd, evenals projectiebestemmingen om te bepalen waar te om een projectie te leiden. Voor gedetailleerde informatie over het werken met randprojecties, gelieve de [projectieconfiguraties en bestemmingseindpuntgids](edge-projections.md)te bezoeken.

## Entiteiten ([!DNL Profile] toegang) {#entities}

Via Adobe Experience Platform hebt u toegang tot [!DNL Real-time Customer Profile] gegevens met RESTful API&#39;s of de gebruikersinterface. Als u wilt leren hoe u toegang krijgt tot entiteiten, beter bekend als &quot;profielen&quot;, gebruikt u de API, volgt u de stappen die worden beschreven in de handleiding voor het eindpunt van [entiteiten](entities.md). Raadpleeg de gebruikershandleiding bij [!DNL Platform] Profiel voor toegang tot profielen met behulp van de [gebruikersinterface](../ui/user-guide.md).

## Exporttaken ([!DNL Profile] exporteren) {#profile-export}

[!DNL Real-time Customer Profile] de gegevens kunnen naar een dataset voor verdere verwerking, zoals het uitvoeren van publiekssegmenten voor activering of profielattributen voor rapportering worden uitgevoerd. Exporttaken voor publiekssegmenten maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Lees de [eindgebruikershandleiding voor](../../profile/api/export-jobs.md) segmentatietaken voor exporttaken voor meer informatie. Voor stapsgewijze instructies over het maken en beheren van exporttaken voor profielkenmerken raadpleegt u de handleiding voor het eindpunt van [exporttaken](export-jobs.md).

## Beleid samenvoegen {#merge-policies}

Wanneer het brengen van gegevens uit veelvoudige bronnen samen in [!DNL Experience Platform], zijn het fusiebeleid de regels die [!DNL Platform] gebruiken om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om individuele klantenprofielen tot stand te brengen. Met behulp van de [!DNL Real-time Customer Profile] API kunt u een nieuw samenvoegbeleid maken, bestaand beleid beheren en een standaardsamenvoegbeleid voor uw organisatie instellen. Meer over het werken met fusiebeleid gebruikend API, gelieve te bezoeken de gids [van het eindpunt van het](merge-policies.md)fusiebeleid.

Voor een gids aan het werken met fusiebeleid gebruikend [!DNL Platform] UI, te zien gelieve de de gebruikersgids [van het Beleid van de](../ui/merge-policies.md)Samenvoegen.

## Systeemtaken profiel {#profile-system-jobs}

Gegevens die in [!DNL Platform] worden ingevoerd, worden zowel in de [!DNL Data Lake] gegevensopslag als in de [!DNL Real-time Customer Profile] gegevensopslag opgeslagen. Soms kan het nodig zijn om een gegevensset of batch uit de [!DNL Profile] opslagruimte te verwijderen om gegevens te verwijderen die u niet meer nodig hebt of die per ongeluk zijn toegevoegd. Hiervoor moet u de API gebruiken om een bestand te maken, [!DNL Profile System Job]ook wel &quot;[!DNL delete request]&quot; genoemd, dat u indien nodig kunt wijzigen, controleren of verwijderen. Leer hoe te met schrappingsverzoeken te werken gebruikend het `/system/jobs` eindpunt in [!DNL Real-time Customer Profile] API, de stappen volgen die in de de eindpuntgids [van de](profile-system-jobs.md)de banen van het profielsysteem worden geschetst.

## Volgende stappen {#next-steps}

Beginnen het maken vraag gebruikend [!DNL Real-time Customer Profile] API, lees de [begonnen gids](getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke [!DNL Profile]verwante eindpunten te gebruiken. Raadpleeg de gebruikershandleiding [!DNL Profile] van het profiel van de [!DNL Platform] real-time klant voor meer informatie over het werken met [gegevens via de](../ui/user-guide.md)gebruikersinterface.